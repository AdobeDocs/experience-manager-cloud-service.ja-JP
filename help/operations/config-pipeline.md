---
title: 設定パイプラインの使用
description: 設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定の AEM as a Cloud Service をデプロイする方法について説明します。
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 5e0626c57f233ac3814355d7efe7db010897d72b
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 50%

---

# 設定パイプラインの使用 {#config-pipelines}

設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定の AEM as a Cloud Service をデプロイする方法について説明します。

## 概要 {#overview}

Cloud Manager 設定パイプラインでは、設定ファイル（YAML 形式で作成）をターゲット環境にデプロイします。この方法では、ログ転送、パージ関連のメンテナンスタスク、いくつかの CDN 機能など、AEM as a Cloud Service の多くの機能を設定できます。

**パブリッシュ配信** プロジェクトの場合、設定パイプラインは、Cloud Managerを介して、開発環境、ステージング環境、実稼動環境の各タイプにデプロイできます。 設定ファイルは、[コマンドラインツール](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)を使用して高速開発環境（RDE）にデプロイできます。

設定パイプラインは、**Edge Delivery** プロジェクトのCloud Managerを通じてデプロイすることもできます。

このドキュメントの以降の節では、設定パイプラインの使用方法と、それらの設定を構造化する方法に関する重要な情報の概要を示します。設定パイプラインでサポートされる機能のすべてまたはサブセットで共有される一般的な概念について説明します。

* [&#x200B; サポートされている設定 &#x200B;](#configurations) – 設定パイプラインでデプロイできる設定のリスト。
* [&#x200B; 設定パイプラインの作成と管理 &#x200B;](#creating-and-managing) – 設定パイプラインの作成方法
* [&#x200B; 共通構文 &#x200B;](#common-syntax) – 設定間で共有される構文。
* [&#x200B; フォルダー構造 &#x200B;](#folder-structure) – 設定に必要な構造設定パイプラインについて説明します。
* [&#x200B; シークレット環境変数 &#x200B;](#secret-env-vars) – 設定でシークレットを開示しない環境変数の使用例。
* [&#x200B; シークレットパイプライン変数 &#x200B;](#secret-pipeline-vars) - Edge Delivery Services プロジェクトの設定内でシークレットを公開しないように環境変数を使用する例。

## サポートされる設定 {#configurations}

次の表に、このような設定の包括的なリストと、その個別の設定構文やその他の情報を説明する専用ドキュメントへのリンクを示します。

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
| [ログ転送](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Azure Blob Storage、Datadog、HTTPS、Elasticsearch、Splunk など、様々な宛先にログを転送するエンドポイントと資格情報を設定します。 | X | X |
| [クライアント ID の登録](/help/implementing/developing/open-api-based-apis.md) | `API` | クライアント ID を登録して、Adobe Developer Console API プロジェクトの範囲を特定のAEM環境に限定します。 認証が必要な OpenAPI ベースの API の使用に必要 | X |  |

## 設定パイプラインの作成と管理 {#creating-and-managing}

**パブリッシュ配信** 設定パイプラインの作成および設定方法について詳しくは、[CI/CD パイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline) を参照してください。 Cloud Managerで config パイプラインを作成する場合は、パイプラインの設定時に **フルスタックコード** ではなく **ターゲットデプロイメント** を選択してください。 前述のように、RDE の設定は、パイプラインではなく[コマンドラインツール](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)を使用してデプロイされます。

**Edge Delivery** 設定パイプラインの作成および設定方法について詳しくは、[Edge Delivery パイプラインの追加 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md) を参照してください。

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
| `metadata` | （オプション）設定を処理する環境タイプを決定する文字列 `envTypes` の配列が含まれます。 **公開配信** の場合、使用可能な値は `dev`、`stage`、`prod` です。 **Edge Delivery** の場合は、`prod` の値のみを使用する必要があります。 例えば、配列に `dev` のみが含まれている場合、設定がステージング環境または実稼動環境にデプロイされていても、設定は読み込まれません。 | すべての環境タイプ（パブリッシュ配信の場合は開発、ステージ、実稼動、Edge Deliveryの場合は実稼動）。 |

`yq` ユーティリティを使用すると、設定ファイル（例：`yq cdn.yaml`）の YAML 形式をローカルで検証できます。

## 公開配信 {#yamls-for-aem}

**パブリッシュ配信** 設定がターゲット環境にデプロイされます。 複数の環境をターゲットにする場合、異なるファイルを異なる方法で整理できます。 例えば、配列に `dev` のみが含まれている場合、設定がステージング環境または実稼動環境にデプロイされていても、設定は読み込まれません。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### フォルダー構造 {#folder-structure}

`/config` または類似の名前のフォルダーをツリーの最上部に存在させ、その下のツリー内にもう 1 つの YAML ファイルを存在させる必要があります。

例：

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

`/config` の下のフォルダー名とファイル名は任意です。ただし、YAML ファイルには有効な [`kind` プロパティ値](#configurations)を含める必要があります。

通常、設定はすべての環境にデプロイされます。すべてのプロパティ値が各環境で同じ場合は、1 つの YAML ファイルで十分です。 ただし、下位環境のテスト時など、環境間でプロパティ値が異なることは一般的です。

次の節では、ファイルを構造化するいくつかの戦略について説明します。

### すべての環境に対して 1 つの設定ファイル {#single-file}

ファイル構造は次のようになります。

```text
/config
  cdn.yaml
  logForwarding.yaml
```

この構造は、すべての環境とすべての設定のタイプ（CDN、ログ転送など）に対して同じ設定で十分な場合に使用します。このシナリオでは、`envTypes` 配列プロパティにすべての環境タイプが含まれます。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

秘密鍵タイプの環境（またはパイプライン）変数を使用すると、次の [&#x200B; リファレンスに示すように、環境ごとに &#x200B;](#secret-env-vars) 秘密鍵プロパティ `${{SPLUNK_TOKEN}}` を変更できます。

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

### 環境タイプごとに別個のファイル {#file-per-env}

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

プロパティ値に違いがある可能性がある場合は、この構造を使用します。ファイルでは、`envTypes` 配列の値がサフィックスに対応することを想定しています。 例えば、`cdn-dev.yaml` と `logForwarding-dev.yaml` の値は `["dev"]`、`cdn-stage.yaml` と `logForwarding-stage.yaml` の値は `["stage"]` などです。

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

Edge Delivery設定パイプラインには、開発環境、ステージング環境および実稼動環境は個別に設定されません。 パブリッシュ配信環境では、開発、ステージ、実稼動層を通じて変更の進行状況が示されます。 一方、Edge Delivery設定パイプラインは、Edge Delivery サイトのCloud Managerに登録されているすべてのドメインマッピングに設定を直接適用します。


したがって、次のような単純なファイル構造をデプロイします。

```text
/config
  cdn.yaml
  logForwarding.yaml
```

ルールをEdge Delivery サイトごとに異なる必要がある場合は、構文 *when* を使用してルールを区別します。 例えば、以下のスニペットで、ドメインがdev.example.comと一致することに注意してください。これは、ドメイン `www.example.com` と区別できます。

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

*envTypes* メタデータフィールドを含める場合は、値 **prod** のみを使用してください（envTypes メタデータフィールドを省略しても問題ありません）。 *tier* reqProperty の場合は、値 **publish** のみを使用する必要があります。

## シークレットの環境変数 {#secret-env-vars}

ソースコントロールに機密情報を保存する必要がないように、設定ファイルでは&#x200B;**秘密鍵**&#x200B;タイプの Cloud Manager 環境変数をサポートします。ログ転送を含む一部の設定では、特定のプロパティに対して秘密鍵の環境変数が必須です。

シークレットの環境変数は、配信プロジェクトの公開に使用します。Edge Delivery Services プロジェクトについては、シークレットパイプライン変数の節を参照してください。

次のスニペットは、シークレット環境変数 `${{SPLUNK_TOKEN}}` が設定でどのように使用されるかを示しています。

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

環境変数の使用方法について詳しくは、[Cloud Manager環境変数 &#x200B;](/help/implementing/cloud-manager/environment-variables.md) を参照してください。

## 秘密鍵パイプライン変数 {#secret-pipeline-vars}

Edge Delivery Services プロジェクトの場合は、**secret** 型のCloud Manager パイプライン変数を使用します。そのため、ソース管理に機密情報を保存する必要はありません。 「*適用されたステップ*」選択ボックスでは、「**デプロイ**」オプションを使用する必要があります。

構文は前の節で示したスニペットと同じです。

パイプライン変数の使用方法について詳しくは、[Cloud Managerのパイプライン変数 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) を参照してください。
