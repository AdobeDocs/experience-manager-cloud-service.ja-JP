---
title: AEM Edge Functions
description: AEM Edge Functionsを使用して、CDN レイヤーでJavaScriptを実行し、エンドユーザーの近くでパーソナライズ、セキュリティ、動的エクスペリエンスを実現する方法を説明します。
feature: Developing, Edge Delivery Services
role: Developer
exl-id: 9cebe65c-6aea-4096-9c58-f88295a80639
source-git-commit: 3d12f495e0f1a07c81033b93fd607fd260023c48
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 2%

---

# AEM Edge Functions {#aem-edge-functions}

>[!IMPORTANT]
>
>AEM Edge Functionsは&#x200B;**ベータ**&#x200B;機能です。 機能やドキュメントは予告なく変更される場合があります。 早期アクセスプログラムに参加してフィードバックを提供するには、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)にメールを送信してください。

AEM Edge Functionsでは、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより、遅延を低減し、コンテンツの配信元を何度も訪問することなく、レスポンシブでダイナミックなエクスペリエンスを提供できます。

一般的なユースケースを次に示します。

- 位置情報、デバイスの種類、ユーザー属性などの情報にもとづくコンテンツのパーソナライズ
- CDN と接触チャネルの間のミドルウェアとして機能させる
- サードパーティ APIからの応答をブラウザーに届く前に再フォーマットまたは集約する
- 複数のバックエンドから合成したコンテンツを使用して、サーバーレンダリングされたHTMLをエッジで合成して配信する

AEM Edge Functionsは、Edge Delivery ServicesとAEM as a Cloud Service Java スタックの両方に対応しています。

## 主なメリット {#key-benefits}

| メリット | 説明 |
|---|---|
| **パフォーマンス** | 完全にレンダリングされたHTMLを返すエッジ SSRによる高速TTFB。 並列フェッチと最適化されたネットワークホップによる低遅延API呼び出し。 |
| **SEO / GEO** | Server HTMLは、最初のクロール時にインデックスが作成されます。 AIweb クローラーに対応したレンダリング済みコンテンツ： |
| **セキュリティ** | クライアント JavaScriptから非表示のAPI資格情報をサーバーサイドに保持します。 ID プロバイダーで認証し、コンテンツへのアクセスを制限します。 |
| **パーソナライゼーション** | 位置情報やデバイスのシグナルにもとづいて、ページが読み込まれる前にコンテンツをパーソナライズします。 ターゲット配信のために、エッジでオーディエンス検索を実行します。 |

## 前提条件 {#prerequisites}

- AEM as a Cloud Service環境
- Cloud Service環境のオーサーインスタンス上のAEM Administrator製品プロファイル、Admin Console for Edge Delivery Services サイトのCloud Manager Deployment Manager ロール **または**
- [Node.jsとnpm](https://nodejs.org/)

## セットアップ {#setup}

### Adobe CLIのインストール {#install-adobe-cli}

Adobe Developer CLI （`aio`）をインストールします。

```bash
npm install -g @adobe/aio-cli
```

AEM Edge Functions プラグインをインストールします。

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

環境のプラグインを認証して設定します。

```bash
aio login
aio aem edge-functions setup
```

setup コマンドを使用すると、ログインして、AEM Edge Functionsを使用するAEM環境を選択するように求められます。

### Boilerplateの複製 {#boilerplate}

[aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate)を独自のリポジトリにコピーしてから、依存関係をインストールします。

```bash
npm install
```

## 最初の関数を作成する {#create-your-function}

AEM Edge関数サービスは、YAML設定ファイルで宣言され、Cloud Manager設定パイプラインを通じてデプロイされます。

### &#x200B;1. 設定パイプラインの設定 {#configuration-pipeline}

エッジ関数を作成する前に、Cloud Managerで環境用の設定パイプラインが存在することを確認します。 そうでない場合は、最初に[設定パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を作成します。

>[!NOTE]
>
>迅速な開発環境（RDE）を使用している場合は、設定パイプラインを経由する代わりに、`aio aem rde:install -t env-config ./config`を使用して直接設定をデプロイできます。

### &#x200B;2. Edge Function Servicesの宣言 {#declare-services}

設定ディレクトリに`edgeFunctions.yaml`という名前のファイルを作成します。

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: my-edge-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

デフォルトの制限は、AEM as a Cloud Service環境の場合は1関数、Edge Delivery Services サイトの場合は3です。 最上位のキーは次のとおりです。

| キー | 説明 |
|---|---|
| `services` | エッジ関数サービスのリスト。各サービスは`name`によって識別されます。 |
| `configs` | すべてのエッジ関数サービスに環境変数として公開されるキーと値のペア。 |
| `secrets` | すべてのedge function サービスに公開される、Cloud Manager シークレットを参照するキーと値のペア。 |
| `kvs` | すべてのエッジ関数サービスで共有されるランタイム読み取り/書き込みキー値データ用にKV ストアをプロビジョニングするためのブール型トグル。 |

### &#x200B;3. CDN オリジン セレクタ ルールの追加 {#cdn-routing}

Edge関数は、オリジンセレクタールールを介してCDN トラフィックをルーティングすることで呼び出されます。 `cdn.yaml`設定ファイルに次のファイルを追加します（または、存在しない場合は作成します）。

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-weather-to-edge-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
      - name: route-hello-world-to-edge-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
```

オリジン選択ルールを使用すると、特定のパス、ドメイン、リクエストヘッダーなど、CDN ルールエンジンで利用可能なあらゆる条件に基づいて、トラフィックをエッジ関数にルーティングできます。 複数のルールで異なるパスを同じエッジ関数にルーティングできます。 完全なルール構文については、[&#x200B; オリジンセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)を参照してください。

### &#x200B;4. 設定のデプロイ {#deploy-configuration}

`edgeFunctions.yaml`と`cdn.yaml`の両方をCloud Manager Git リポジトリにコミットし、設定パイプラインをトリガーします。 パイプラインが正常に完了すると、エッジ関数エンドポイントは次の場所で使用できるようになります。

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

ここで、`pXXXXX-eYYYYY`は環境座標です。 カスタムドメインが設定されている場合、関数はこれらのドメインパスでも到達できます（例：`example.com/weather`）。

## AEM Edge関数コードのビルドとデプロイ {#build-deploy}

### ビルド {#build}

デプロイメント用にEdge関数コードをパッケージ化します。

```bash
aio aem edge-functions build
```

### デプロイ {#deploy}

ビルドされたパッケージを名前付きエッジ関数サービスにデプロイします。 `function-name`引数は`edgeFunctions.yaml`の`name`値と一致する必要があります：

```bash
aio aem edge-functions deploy <function-name>
```

## ローカル開発 {#local-development}

### ローカルで実行 {#local-run}

`http://127.0.0.1:7676`でローカル開発サーバーを起動します。

```bash
aio aem edge-functions serve
```

ローカル ランタイムがサポートする内容について詳しくは、[Compute JavaScript ドキュメント &#x200B;](https://www.fastly.com/documentation/guides/compute/javascript/)を参照してください。

### テスト {#test}

[Mocha](https://mochajs.org/)でテストスイートを実行します。

```bash
npm run test
```

### リモートデバッグ {#remote-debugging}

Adobe Managed CDNは、リモートデバッガーを公開しませんが、ログストリーミングを公開します。 デプロイされた関数のログをテールして、ターミナルで`console.log`出力を直接受信します。

```bash
aio aem edge-functions tail-logs <function-name>
```

## キャッシュとキャッシュのパージ {#caching}

Edge Functionsは、エッジにデータをキャッシュすることで、オリジンの読み込みを大幅に削減し、応答時間を短縮できます。 ただし、キャッシュには意図的な設計が必要です。特に、**2つの独立したキャッシュレイヤー**&#x200B;が関与するEdge関数では、次のようになります。

```
Browser → AEM CDN (CDN Cache) → AEM Edge Functions (Fetch Cache) → Backend (AEM, APIs, etc.)
```

キャッシュを設定する前に、コンテンツの動作を考慮してください。

- **リクエストごとの真に一意のコンテンツ** （セッショントークン、特定のユーザーのリアルタイム価格）は、誤った結果を提供しないようにするために、キャッシュをバイパスする必要があります。
- **コホートベースのパーソナライゼーション** （地域、デバイスの種類、またはオーディエンスセグメントによってカスタマイズされたコンテンツ）は、多くのユーザーが同じバリエーションを共有するため、短いTTLまたは`Vary` ヘッダーでキャッシュされることがよくあります。
- **安定した共有コンテンツ** （製品カタログ、CMS ページ、既知のスケジュールで変化するAPI レスポンス）は、サロゲートキーを介した明示的な無効化による積極的なキャッシュの利点があります。
- **いずれかの方向で間違えると、結果が発生します。** オーバーキャッシュすると、古いコンテンツのバグが発生し、2つのキャッシュレイヤーをまたいで診断することが困難になります。 Edge関数を使用する場合、アンダーキャッシュはパフォーマンスとオリジンオフロードの目的をまったく損ないます。

CDNとEdge関数の内部フェッチ キャッシュは独立して動作するため、基になるデータを変更するには、**両方** レイヤーを意図的に無効化する必要があります。 このアーキテクチャを理解することは、信頼性の高いキャッシュ管理に不可欠です。

キャッシュ動作の設定、キャッシュの有効期間の制御、サロゲートキーの使用、キャッシュされたコンテンツのパージに関する詳細な技術的ガイダンスについては、[AEM Edge Functionsでのキャッシュ &#x200B;](/help/implementing/developing/introduction/edge-functions-caching.md)を参照してください。

## 制限事項 {#limitations}

各Edge関数の呼び出しは、基になるコンピューティングプラットフォームによって適用されるリソース制限を伴うサンドボックス内で実行されます。

### 呼び出しあたりの最大アウトバウンドフェッチ呼び出し {#max-fetch-calls}

AEM Edge関数は、実行単位&#x200B;**で** 32件のバックエンドリクエスト（つまり、関数が処理する受信リクエスト単位）のハードリミットを適用します。 この制限に達すると、以降の`fetch()`呼び出しは失敗し、次のエラーが発生します。

```
Requested backend named '…' does not exist
```

このエラーが表示され、オリジン設定が正しい場合、最も可能性の高い原因は、呼び出し単位のバックエンド要求クォータが使い果たされたことです。 プラットフォーム制限の完全なリストについては、[Fastly Compute リソース制限](https://docs.fastly.com/products/compute-resource-limits#default-limits)を参照してください。

## 設定リファレンス {#configuration-reference}

### オリジン {#origins}

デフォルトでは、エッジ関数は任意のオリジンから取得できます。 関数を定義済みのオリジンのセットに制限するには、`edgeFunctions.yaml`の`origins`で宣言します。

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

`backend` フェッチ オプションを使用して、関数コード内の名前付きオリジンを参照します。

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

>[!NOTE]
>
>サービスストア （`configs`、`secrets`、および`kvs`）は、[&#x200B; サンドボックスプログラム &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)では利用できません。 Edge機能サービス自体は、通常、サンドボックス環境で実行されます。ストアのみがプロビジョニングされません。

### サービス設定 {#service-configuration}

`edgeFunctions.yaml`の`configs` キーを使用して、環境変数を関数に公開します。 値は、`config_default`という名前の設定ストアに格納されます。

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

関数コードで設定値を読み取ります。

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- 構成ストアの名前は常に`config_default`です。
>- キー名では大文字と小文字が区別されます。
>- 設定ストアは、同じ環境のすべてのエッジ関数サービスで共有されます。

### サービス秘密鍵 {#service-secrets}

秘密鍵は参照され、保存されません。`edgeFunctions.yaml` `value` フィールドは、`${{SECRET_REFERENCE}}`構文を使用してCloud Manager シークレットを指している必要があります。 最初にCloud Managerで基になる秘密鍵を定義します。[Cloud Manager秘密変数](/help/implementing/cloud-manager/environment-variables.md)を参照してください。

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

ボイラープレートから`SecretStoreManager` ヘルパーを使用して、関数コードのシークレットを取得します。

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- 秘密鍵ストアの名前は常に`secret_default`です。
>- キー名では大文字と小文字が区別されます。
>- 秘密鍵は一度作成されると不変です。
>- シークレットストアは、同じ環境のすべてのエッジ機能サービスで共有されます。

### サービス KV ストア {#service-kv-store}

Edge関数は、KV ストアを介して、実行時に任意のキー値データを読み取り、書き込むことができます。 有効にするには、`edgeFunctions.yaml`で`kvs: true`を設定します。

```yaml
kvs: true
```

これにより、`kv_default`という名前の空のKV ストアがプロビジョニングされます。 [Fastly KV Store API](https://js-compute-reference-docs.edgecompute.app/docs/fastly:kv-store/KVStore)を使用して、エッジ関数コードから実行時に設定します。

```js
import { KVStore } from "fastly:kv-store";

const kv = new KVStore('kv_default');

// Read a value
const entry = await kv.get('visit-count');
const count = entry ? Number(await entry.text()) : 0;

// Write a value
await kv.put('visit-count', String(count + 1));
```

>[!NOTE]
>
>- KV ストアの名前は常に`kv_default`です。
>- プロビジョニング時にKV ストアが空です。[Fastly KV Store API](https://js-compute-reference-docs.edgecompute.app/docs/fastly:kv-store/KVStore)を使用して、実行時に設定します。 `edgeFunctions.yaml`の宣言型キー/値エントリはサポートされていません。
>- KV ストアは、同じ環境のすべてのエッジ機能サービスで共有されます。

### ログ {#logging}

AEM Edge Functionsは、[AEM ログ転送機能](/help/implementing/developing/introduction/log-forwarding.md)と統合されています。 `edgeFunctions.yaml`と一緒に`logForwarding.yaml` ファイルを作成します。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

関数コードでロガーを使用して、構造化ログエントリを書きます。

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>AEM Edge関数ログエントリを含むCDN ログは、Java スタック環境用のCloud Managerからダウンロードできますが、Edge Delivery Services サイト用にはダウンロードできません。
>
