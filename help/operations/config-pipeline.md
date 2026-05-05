---
title: 設定パイプラインの使用
description: 設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定の AEM as a Cloud Service をデプロイする方法について説明します。
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 4ec024236cc1054206ea789d755dd4e76fb9cd79
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 44%

---

# 設定パイプラインの使用 {#config-pipelines}

設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定の AEM as a Cloud Service をデプロイする方法について説明します。

## 概要 {#overview}

Cloud Manager 設定パイプラインでは、設定ファイル（YAML 形式で作成）をターゲット環境にデプロイします。 この方法では、ログ転送、パージ関連のメンテナンスタスク、いくつかの CDN 機能など、AEM as a Cloud Service の多くの機能を設定できます。

**Publish Delivery** プロジェクトの場合、設定パイプラインをCloud Managerを介してデプロイし、デベロッパー、ステージ、実稼動環境のタイプを指定できます。 設定ファイルは、[コマンドラインツール](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)を使用して高速開発環境（RDE）にデプロイできます。 パブリッシュ配信環境に接続されたドメインのトラフィックを設定する必要がある場合は、ターゲットのデプロイメント [**パブリッシュ配信パイプライン**](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment) （[実稼動](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)または[実稼動以外](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)）を使用します。

構成パイプラインは、**Edge Delivery** プロジェクト用にCloud Managerを通じてデプロイすることもできます。 ドメインが&#x200B;**Edge Delivery サイト**&#x200B;にアタッチされている場合は、[**Edge Delivery パイプライン**](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)&#x200B;を使用します。

このドキュメントの以降の節では、設定パイプラインの使用方法と、それらの設定を構造化する方法に関する重要な情報の概要を示します。 設定パイプラインでサポートされる機能のすべてまたはサブセットで共有される一般的な概念について説明します。

* [&#x200B; サポートされる設定](#configurations) – 設定パイプラインでデプロイできる設定のリスト。
* [設定パイプラインの作成と管理](#creating-and-managing) – 設定パイプラインの作成方法
* [共通の構文](#common-syntax) – 構成間で共有される構文。
* [&#x200B; フォルダー構造](#folder-structure) – 構成に対して期待される構造構成パイプラインについて説明します。
* [&#x200B; シークレット環境変数](#secret-env-vars) – 環境変数を使用して設定のシークレットを公開しない例。
* [&#x200B; シークレット パイプライン変数](#secret-pipeline-vars) – 環境変数を使用して、Edge Delivery Services プロジェクトの前に設定のシークレットを公開しない例。

## サポートされる設定 {#configurations}

次の表に、このような設定の包括的なリストと、その個別の設定構文やその他の情報を説明する専用ドキュメントへのリンクを示します。

CDNに関連する設定については、表のリンクされた記事に加えて、[CDN Configuration Snippets for Common Scenarios](/help/implementing/dispatcher/cdn-configuration-snippets-common-scenarios.md)の記事も参照してください。

| タイプ | YAML `kind` 値 | 説明 | 公開配信 | エッジ配信 |
|---|---|---|---|---|
| [WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | 悪意のあるトラフィックをブロックするルールを宣言します | X | X |
| [リクエスト変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | トラフィックリクエストの形式を変換するルールを宣言します | X | X |
| [応答変換](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | 特定のリクエストに対する応答の形式を変換するルールを宣言します。 | X | X |
| [サーバーサイドのリダイレクト](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | 301/302 スタイルのサーバーサイドのリダイレクトを宣言します。 | X | X |
| [接触チャネルセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | アドビ以外のアプリケーションを含む様々なバックエンドにトラフィックをルーティングするルールを宣言します | X | X |
| [CDN エラーページ](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | AEM オリジンに到達できない場合は、設定ファイルの自己ホスト型静的コンテンツの場所を参照して、デフォルトのエラーページを上書きします | X |  |
| [CDN パージ](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | CDN のパージに使用するパージ API キーを宣言します | X |  |
| [顧客管理 CDN の HTTP トークン](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | 顧客 CDN から Adobe CDN を呼び出すために必要な X-AEM-Edge-Key の値を宣言します | X |  |
| [基本認証](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | 特定の URL を保護する基本認証ダイアログのユーザー名とパスワードを宣言します。 | X | X |
| [バージョンのパージメンテナンスタスク](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | コンテンツのバージョンをパージするタイミングに関するルールを宣言して、AEM リポジトリを最適化します | X |  |
| [監査ログのパージメンテナンスタスク](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | ログをパージするタイミングに関するルールを宣言して、AEM 監査ログを最適化し、パフォーマンスを向上させます | X |  |
| [&#x200B; ワークフローのパージ メンテナンス タスク &#x200B;](/help/operations/maintenance.md) | `MaintenanceTasks` | ワークフローエンジンのパフォーマンスを向上させるために、ワークフローインスタンスの数を最小限に抑えます。<br><br> ワークフローインスタンスの定期的なパージ [も参照してください](/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances) | X |  |
| [ログ転送](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Azure Blob Storage、Datadog、HTTPS、Elasticsearch、Splunk など、様々な宛先にログを転送するエンドポイントと資格情報を設定します。 | X | X |
| [クライアント ID の登録](/help/implementing/developing/open-api-based-apis.md) | `API` | クライアント IDを登録して、Adobe Developer Console API プロジェクトを特定のAEM環境にスコープします。 認証を必要とするOpenAPI ベースのAPIの使用に必要 | X |  |

## 設定パイプラインの作成と管理 {#creating-and-managing}

**パブリッシュ配信**&#x200B;設定パイプラインを作成および設定する方法について詳しくは、[CI/CD パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)を参照してください。 Cloud Managerで設定パイプラインを作成する場合は、パイプラインの設定時に&#x200B;**フルスタックコード**&#x200B;ではなく&#x200B;**ターゲットデプロイメント**&#x200B;を選択してください。 前述のように、RDE の設定は、パイプラインではなく[コマンドラインツール](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)を使用してデプロイされます。

**Edge Delivery**&#x200B;設定パイプラインを作成および設定する方法について詳しくは、[Edge Delivery パイプラインを追加](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)の記事を参照してください。

## 共通の構文 {#common-syntax}

各設定ファイルは、次の例のスニペットに類似したプロパティで始まります。

```yaml
   kind: "CDN"
   version: "1"
   metadata: ...
   data: ...
```

| プロパティ | 説明 | デフォルト |
|---|---|---|
| `kind` | ログ転送、トラフィックフィルタールール、リクエスト変換などの設定のタイプを決定する文字列 | 必須、デフォルトなし |
| `version` | スキーマバージョンを表す文字列 | 必須、デフォルトなし |
| `metadata` | （オプション）これには、設定が処理される環境タイプを決定する文字列`envTypes`の配列が含まれます。 **Publish Delivery**&#x200B;の場合、使用可能な値は`dev`、`stage`、`prod`です。 **Edge Delivery**&#x200B;の場合は、値`prod`のみを使用してください。 例えば、配列に`dev`のみが含まれている場合、設定がそこにデプロイされていても、ステージング環境または実稼動環境には設定が読み込まれません。 | すべての環境タイプ （開発、ステージ、実稼動環境）は、パブリッシュ配信またはEdge Deliveryの実稼動環境タイプです。 |

`yq` ユーティリティを使用すると、設定ファイル（例：`yq cdn.yaml`）の YAML 形式をローカルで検証できます。

## 公開配信 {#yamls-for-aem}

**パブリッシュ配信**&#x200B;設定がターゲット環境にデプロイされます。 複数の環境をターゲットにする場合、異なる方法で異なるファイルを整理できます。 例えば、配列に`dev`のみが含まれている場合、設定がそこにデプロイされていても、ステージング環境または実稼動環境には設定が読み込まれません。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### フォルダー構造 {#folder-structure}

`/config` または類似の名前のフォルダーをツリーの最上部に存在させ、その下のツリー内にもう 1 つの YAML ファイルを存在させる必要があります。

次に例を示します。

```text
/config
  cdn.yaml
```

または

```text
/config
  /dev
    cdn.yaml
```

`/config` の下のフォルダー名とファイル名は任意です。 ただし、YAML ファイルには有効な [`kind` プロパティ値](#configurations)を含める必要があります。

通常、設定はすべての環境にデプロイされます。 すべてのプロパティ値が各環境で同じ場合は、1つのYAML ファイルで十分です。 ただし、下位環境のテスト時など、環境間でプロパティ値が異なることは一般的です。

次の節では、ファイルを構造化するいくつかの戦略について説明します。

### すべての環境に対する単一の設定ファイル {#single-file}

ファイル構造は次のようになります。

```text
/config
  cdn.yaml
  logForwarding.yaml
```

この構造は、すべての環境とすべての設定のタイプ（CDN、ログ転送など）に対して同じ設定で十分な場合に使用します。 このシナリオでは、`envTypes` 配列プロパティにすべての環境タイプが含まれます。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

シークレット タイプの環境（またはパイプライン）変数を使用すると、次の`${{SPLUNK_TOKEN}}`参照に示すように、[&#x200B; シークレット プロパティ &#x200B;](#secret-env-vars)が環境ごとに異なる可能性があります。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

### 環境タイプごとに個別のファイル {#file-per-env}

ファイル構造は次のようになります。

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

プロパティ値に違いがある可能性がある場合は、この構造を使用します。 ファイルでは、`envTypes`配列値が接尾辞に対応することが期待されます。 例えば、`cdn-dev.yaml`と`logForwarding-dev.yaml`の値が`["dev"]`、`cdn-stage.yaml`と`logForwarding-stage.yaml`の値が`["stage"]`であるなど。

### 環境ごとのフォルダー {#folder-per-env}

この戦略では、環境ごとに個別の `config` フォルダーがあり、それぞれに対して Cloud Manager で個別のパイプラインが宣言されます。

このアプローチは、それぞれに一意のプロパティ値を持つ複数の開発環境がある場合に特に便利です。

ファイル構造は次のようになります。

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

このアプローチのバリエーションとして、環境ごとに個別のブランチを維持する方法があります。

## Edge Delivery Services {#yamls-for-eds}

Edge Delivery設定パイプラインには、開発環境、ステージング環境および実稼動環境が分離されていません。 パブリッシュ配信環境では、変更は開発、ステージ、実稼動階層を通じて進行します。 対照的に、Edge Delivery設定パイプラインでは、Edge Delivery サイト用にCloud Managerに登録されているすべてのドメインマッピングに直接設定が適用されます。


したがって、次のような単純なファイル構造をデプロイします。

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Edge Delivery サイトごとにルールを変更する必要がある場合は、構文&#x200B;*when*&#x200B;を使用してルールを区別します。 例えば、ドメインが以下のスニペットのdev.example.comと一致し、ドメイン `www.example.com`と区別できることに注意してください。

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

*envTypes* メタデータフィールドを含める場合は、値&#x200B;**prod**&#x200B;のみを使用します（envTypes メタデータフィールドを省略しても問題ありません）。 *tier* reqPropertyでは、値&#x200B;**publish**&#x200B;のみを使用する必要があります。

## 設定シークレット  {#secret-in-configuration}

機密情報をソース管理に保存する必要がないように、設定ファイルでは、Config パイプライン変数または環境変数からシークレットを参照できます。 ログ転送を含む一部の設定では、特定のプロパティにシークレット変数が必須です。 CDN設定でのシークレットの使用について詳しくは、[CDN認証情報と認証の設定](/help/implementing/dispatcher/cdn-credentials-authentication.md)を参照してください。

次のスニペットは、秘密変数`${{SPLUNK_TOKEN}}`が設定でどのように使用されるかを示す例です。

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```



### シークレットパイプライン変数 {#secret-pipeline-vars}

**好みの方法**&#x200B;では、Cloud Manager パイプライン変数タイプ **secret**&#x200B;を使用するので、機密情報をソースコントロールに保存する必要はありません。 **手順が適用されました**&#x200B;選択ボックスでは、**デプロイ** オプションを使用する必要があります。

パイプライン変数の使用方法について詳しくは、[Cloud Managerのパイプライン変数](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)を参照してください。


### シークレット環境変数 {#secret-env-vars}

シークレット環境変数は、環境ごとに異なるシークレット値を設定する場合に使用します。

環境変数の使用方法について詳しくは、[Cloud Manager環境変数](/help/implementing/cloud-manager/environment-variables.md)を参照してください。

>[!NOTE]
>シークレット環境変数の使用は、より面倒で、厳密な規律が必要です。環境変数は、設定パイプラインと一緒にデプロイされません。 パイプラインを実行する前にデプロイする必要があり、パイプライン設定が引き続きそれらを参照している間は削除しないでください。 パイプラインのシークレットが好まれるのはこのためです。


