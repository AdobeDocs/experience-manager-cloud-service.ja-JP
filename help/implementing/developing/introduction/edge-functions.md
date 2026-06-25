---
title: AEM Edge Functions
description: AEM Edge Functionsを使用して、CDN レイヤーでJavaScriptを実行し、エンドユーザーの近くでパーソナライズ、セキュリティ、動的エクスペリエンスを実現する方法を説明します。
feature: Developing, Edge Delivery Services
role: Developer
exl-id: 9cebe65c-6aea-4096-9c58-f88295a80639
source-git-commit: a42d2318380061c0ce9f894145e1812d0ec1fe1f
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 2%

---

# AEM Edge Functions {#aem-edge-functions}

>[!IMPORTANT]
>
>AEM Edge Functionsは&#x200B;**公開ベータ版**&#x200B;機能なので、Adobeに連絡して有効にすることなく、セルフサービス方式で試すことができます。 Adobeでは、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com)に電子メールを送信して、ユースケースについて説明することを推奨しています。これにより、Adobeでサポートされていることを確認し、ガイダンスを提供できます。 AEM Edge Functions Betaを使用することにより、お客様は、本ソフトウェアがまだ開発中であり、本ソフトウェアの正しい機能やデータの可用性に依存してはならないことを認めます。 この機能は現状のまま提供され、予告なく変更される可能性があり、本番環境ではカバーされません。

AEM Edge Functionsでは、JavaScriptをCDN レイヤーで実行し、データ処理をエンドユーザーに近づけることができます。 これにより、遅延を低減し、コンテンツの配信元を何度も訪問することなく、レスポンシブでダイナミックなエクスペリエンスを提供できます。

一般的なユースケースを次に示します。

- 位置情報、デバイスの種類、ユーザー属性などの情報にもとづくコンテンツのパーソナライズ
- CDN と接触チャネルの間のミドルウェアとして機能させる
- サードパーティ APIからの応答をブラウザーに届く前に再フォーマットまたは集約する
- 複数のバックエンドから合成したコンテンツを使用して、サーバーレンダリングされたHTMLをエッジで合成して配信する

AEM Edge Functionsは、AEM Sitesのお客様向けに、Edge Delivery ServicesとAEM as a Cloud Service Java スタックの両方と互換性があります。

<!-- Follow this tutorial for a concrete walk-through for both Edge Delivery Services and AEM as a Cloud Service Java-stack variations. -->

## 主なメリット {#key-benefits}

| メリット | 説明 |
|---|---|
| **パフォーマンス** | 完全にレンダリングされたHTMLを返すエッジ SSRによる高速TTFB。 並列フェッチと最適化されたネットワークホップによる低遅延API呼び出し。 |
| **SEO / GEO** | AIweb クローラーは、サーバーサイドで結合されたコンテンツにインデックスを作成できます。 |
| **セキュリティ** | クライアント JavaScriptから非表示のAPI資格情報をサーバーサイドに保持します。 ID プロバイダーで認証し、コンテンツへのアクセスを制限します。 |
| **パーソナライゼーション** | 位置情報やデバイスのシグナルにもとづいて、ページが読み込まれる前にコンテンツをパーソナライズします。 ターゲット配信のために、エッジでオーディエンス検索を実行します。 |

## 前提条件 {#prerequisites}

- Cloud Manager プログラム。AEM Java スタック環境またはEdge Delivery Services サイトのいずれかを含みます。 [ オンボード EDS サイトをCloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)に移行する方法について説明します。
- Cloud Manager設定パイプライン（EDS サイトのEdge Delivery Services パイプラインと呼ばれます）。
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

## AEM Edge機能の登録 {#register-your-function}

AEM Edge関数は、YAML設定ファイルで宣言され、Cloud Manager設定パイプラインを通じてデプロイされます。

### &#x200B;1. 設定パイプラインの設定 {#configuration-pipeline}

エッジ関数を作成する前に、Cloud Managerに環境のコンフィギュレーションパイプラインが存在することを確認します（AEM Java スタックを使用している場合）。または、プロジェクトがEdge Delivery Servicesで実装されている場合は、Edge Delivery Services パイプラインが存在することを確認します。 パイプラインの設定について詳しくは、[設定パイプラインの使用](/help/operations/config-pipeline.md)を参照してください。

>[!NOTE]
>
>迅速な開発環境（RDE）を使用している場合は、設定パイプラインを経由する代わりに、`aio aem rde:install -t env-config ./config`を使用して直接設定をデプロイできます。

### &#x200B;2. Edge関数の宣言 {#declare-functions}

設定ディレクトリに`edgeFunctions.yaml`という名前のファイルを作成します。

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
    # add advanced configuration under here
```

Java スタック環境には1つのエッジ関数があり、Edge Delivery Servicesの実装には3つのエッジ関数があります。 オプションのトップレベルキーは次のとおりです。

| キー | 説明 |
|---|---|
| `functions` | エッジ関数のリスト。各エッジ関数は`name`によって識別されます。 後方互換性については、`services`も使用できますが、`functions`が優先キーです。 同じファイルで両方を使用することは許可されていません。 |
| `configs` | 環境のエッジ関数に公開されるキーと値のペアを環境変数として指定します。 |
| `secrets` | Cloud Manager シークレットを環境のエッジ関数に参照するキーと値のペア |
| `kvs` | 環境内のすべてのエッジ関数で共有される実行時の読み取り/書き込みキー値データ用にKV ストアをプロビジョニングするためのブール型トグル。 |

以下の[詳細設定セクション ](#advanced-function-configuration)の`configs`、`secrets`、`kvs`などの詳細設定を参照してください。

### &#x200B;3. Cloud Managerを使用したEdge機能のデプロイ {#deploy-functions-via-cm}

Cloud Managerを使用して、エッジ関数がCDNに登録されるようにパイプラインをデプロイします。

## AEM Edge関数コードの作成、ビルド、デプロイ {#build-deploy}

### 作成者 {#author}

[ ボイラープレートの`src` フォルダー](https://github.com/adobe/aem-edge-functions-boilerplate/tree/main/src)を出発点として使用して、エッジ関数コードビジネスロジックを記述します。

### ビルド {#build}

デプロイメント用にEdge関数コードをパッケージ化します。

```bash
aio aem edge-functions build
```

### デプロイ {#deploy}

パッケージ化されたエッジ関数コードを、指定されたエッジ関数にデプロイします。 `function-name`引数は`edgeFunctions.yaml`の`name`値と一致する必要があります：

```bash
aio aem edge-functions deploy <function-name>
```

### テスト {#test}

エッジ関数が期待どおりに機能することを確認します。 テストは次の場所で実施できます。

`edgefunction-pXXXXX-eYYYYY-<function name>.adobeaemcloud.com/<path>`

例えば、AEM Java スタックの場合：<br/>
`edgefunction-pXXXXX-eYYYYY-my-edge-function.adobeaemcloud.com/weather`

またはEdge Delivery Servicesの場合：<br/>
`edgefunction-pXXXXX-dYYYYY-my-edge-function.adobeaemcloud.com/weather`

*edgefunction*&#x200B;というプレフィックスが付いたこのドメインは、デバッグ用のみですが、*はライブトラフィック*&#x200B;に対して参照しないでください。安定した名前であることが保証されていません。 dYYYYYの値を決定するには、deploy コマンドの出力を参照してください。


## コンテンツ配信フローへのワイヤー接続 {#wiring}

Edge関数のトラフィックは、web サイトのドメインに送信する必要があります。これは、通常、AEM Java スタックのカスタムドメインであり、*はEdge Delivery Services Sitesのカスタムドメインである必要があります。*

### &#x200B;1. 原点セレクターの定義 {#origin-selectors}

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

オリジン選択ルールを使用すると、特定のパス、ドメイン、リクエストヘッダーなど、CDN ルールエンジンで利用可能なあらゆる条件に基づいて、トラフィックをエッジ関数にルーティングできます。 複数のルールで異なるパスを同じエッジ関数にルーティングできます。 完全なルール構文については、[ オリジンセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)を参照してください。

### &#x200B;2. 設定のデプロイ {#deploy-to-cdn}

Cloud Manager Git リポジトリに`cdn.yaml`をコミットし、コンフィギュレーション パイプラインをトリガーします。 パイプラインが正常に完了すると、エッジ関数エンドポイントは次の場所で使用できるようになります。

- `example.com/weather`
- `example.com/hello-world`

デバッグの場合は、ドメイン `publish-pXXXXX-eYYYYY.adobeaemcloud.com` （AEM Java スタック）または`publish-pXXXXX-dYYYYY.adobeaemcloud.com` （Edge Delivery Services サイト）のエッジ関数を参照できます。 安定した名前であることが保証されていないため、このドメインを実稼動用に使用しないでください。 dYYYYYの値を決定するには、deploy コマンドの出力を参照してください。

## ローカル開発 {#local-development}

### ローカルで実行 {#local-run}

`http://127.0.0.1:7676`でローカル開発サーバーを起動します。

```bash
aio aem edge-functions serve
```

ローカル ランタイムがサポートする内容について詳しくは、[Compute JavaScript ドキュメント ](https://www.fastly.com/documentation/guides/compute/javascript/)を参照してください。

### テスト {#test-localdev}

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

キャッシュ動作の設定、キャッシュの有効期間の制御、サロゲートキーの使用、キャッシュされたコンテンツのパージに関する詳細な技術的ガイダンスについては、[AEM Edge Functionsでのキャッシュ ](/help/implementing/developing/introduction/edge-functions-caching.md)を参照してください。

## 制限事項 {#limitations}

- 各Edge関数の呼び出しは、基になるコンピューティングプラットフォームによって適用されるリソース制限を伴うサンドボックス内で実行されます。

- 構築されたweb アセンブリ（wasm）アーティファクトの最大サイズは100 MBです

- 最大メモリ消費量は1 MB バイト スタック、128 MB ヒープです

- エッジ関数の実行に関する重要な情報：
   - 120秒後に実行が終了します
   - 実行は、計算の1秒で終了します（壁時間ではなく）
   - 平均エッジ関数の実行時間は100 ミリ秒未満である必要があります。

- [Edge Function Config Variables](#function-configuration)、[Edge Function Secret Variables](#function-secrets)、[Edge Function KV Stores](#function-kv-store)に関する制限事項を参照してください。

### 呼び出しあたりの最大アウトバウンドフェッチ呼び出し {#max-fetch-calls}

AEM Edge関数は、実行単位&#x200B;**で** 32件のバックエンドリクエスト（つまり、関数が処理する受信リクエスト単位）のハードリミットを適用します。 この制限に達すると、以降の`fetch()`呼び出しは失敗し、次のエラーが発生します。

```
Requested backend named '…' does not exist
```

このエラーが表示され、オリジン設定が正しい場合、最も可能性の高い原因は、呼び出し単位のバックエンド要求クォータが使い果たされたことです。 プラットフォーム制限の完全なリストについては、[Fastly Compute リソース制限](https://docs.fastly.com/products/compute-resource-limits#default-limits)を参照してください。

## Edgeの高度な機能設定 {#advanced-function-configuration}

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
>設定、シークレット、およびkvは、[ サンドボックスプログラム ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)では使用できません。 Edgeの機能は通常、サンドボックス環境で実行されますが、これらのエンティティはプロビジョニングされません。

### Edge関数の設定変数 {#function-configuration}

`edgeFunctions.yaml`の`configs` キーを使用して、環境変数を関数に公開します。 値は、`config_default`という名前の設定ストアに格納されます。

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
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
>- 設定ストアは、同じ環境のすべてのエッジ関数で共有されます。
>- 設定ストアは、Adobeが管理するCDNのグローバルネットワーク全体でレプリケートされます
>- 最大500 エントリ
>- 名前/値の最大サイズ：255文字および8000文字


### Edge関数の秘密変数 {#function-secrets}

秘密鍵は参照され、保存されません。`edgeFunctions.yaml` `value` フィールドは、`${{SECRET_REFERENCE}}`構文を使用してCloud Manager シークレットを指している必要があります。 最初にCloud Managerで基になる秘密鍵を定義します。[Cloud Manager秘密変数](/help/implementing/cloud-manager/environment-variables.md)を参照してください。


```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
  secrets:
    - key: API_TOKEN
      value: ${{API_TOKEN_SECRET}}
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
>- シークレットストアは、同じ環境のすべてのエッジ関数で共有されます。
>- シークレットストアは、Adobeが管理するCDNのグローバルネットワーク全体でレプリケートされます
>- すべてのシークレットの最大サイズは64 kbです

### Edgeファンクション KV ストア {#function-kv-store}

Edge関数は、KV ストアを介して、実行時に任意のキー値データを読み取り、書き込むことができます。 有効にするには、`edgeFunctions.yaml`で`kvs: true`を設定します。


```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
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
>- KV ストアは、同じ環境のすべてのエッジ機能で共有されます。
>- KV ストアは、Adobeが管理するCDNのグローバルネットワーク全体で複製されます
>- KV ストアは最終的な一貫性を提供します。つまり、キーを書き込んだ直後にキーを読み取っても、更新された値が返されない場合があります。
>- KV キー名は最大1024 バイトのUTF-8 ファイルです
>- KV エントリサイズは最大25M
>- KV ストアのアイテムのレート制限は、1つのアイテムにつき1秒あたり1回の書き込みです。
>- KV ストア項目のバッチリクエストは、リクエストごとに100,000個のアイテムの制限があります。


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
>AEM Edge関数ログエントリを含むCDN ログは、Java スタック環境用のCloud Managerからダウンロードできますが、Edge Delivery サイト用にはダウンロードできません。
>
