---
title: 設定パイプラインの使用
description: 設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定のAEM as a Cloud Serviceをデプロイする方法について説明します。
feature: Operations
role: Admin
source-git-commit: 3a10a0b8c89581d97af1a3c69f1236382aa85db0
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 1%

---


# 設定パイプラインの使用 {#config-pipelines}

設定パイプラインを使用して、ログ転送の設定、パージ関連のメンテナンスタスク、様々な CDN 設定など、様々な設定のAEM as a Cloud Serviceをデプロイする方法について説明します。

## 概要 {#overview}

Cloud Manager設定パイプラインは、YAML 形式で作成された設定ファイルを対象環境にデプロイします。 この方法では、ログ転送、パージ関連のメンテナンスタスク、いくつかの CDN 機能など、AEM as a Cloud Serviceの多数の機能を設定できます。

Config パイプラインは、Cloud Managerを介して、実稼動（サンドボックス以外）プログラムの開発環境、ステージング環境および実稼動環境タイプにデプロイできます。 RDE はサポートされていません。

このドキュメントの以降の節では、設定パイプラインの使用方法と設定の構造に関する重要な情報の概要を説明します。 設定パイプラインでサポートされるすべての機能または機能のサブセットで共有される一般的な概念について説明します。

* [ サポートされている設定 ](#configurations) – 設定パイプラインでデプロイできる設定のリスト
* [ 設定パイプラインの作成と管理 ](#creating-and-managing) – 設定パイプラインの作成方法。
* [ 共通の構文 ](#common-syntax) – 設定間で共有される構文
* [ フォルダー構造 ](#folder-structure) – 設定に必要な構造設定パイプラインについて説明します。
* [ シークレット環境変数 ](#secret-env-vars) – 環境変数を使用して設定でシークレットを開示しない例

## サポートされる設定 {#configurations}

次の表は、そのような設定の包括的なリストと、個別の設定構文やその他の情報を説明する専用ドキュメントへのリンクを示しています。

| タイプ | YAML `kind` Value | 説明 |
|---|---|---|
| [ トラフィックフィルタールール（WAFを含む） ](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | 悪意のあるトラフィックをブロックするルールの宣言 |
| [ リクエスト変換 ](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | トラフィックリクエストの形状を変換するルールを宣言 |
| [ レスポンス変換 ](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | 特定のリクエストに対する応答の形状を変換するルールを宣言する |
| [ クライアントサイドのリダイレクト ](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) | `CDN` | 301/302 スタイルのクライアントサイドリダイレクト [ を宣言する（早期導入ユーザーのみ利用可能） ](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter) |
| [ 接触チャネルセレクター ](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Adobe以外のアプリケーションを含む様々なバックエンドにトラフィックをルーティングするルールの宣言 |
| [CDN エラーページ ](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | AEM オリジンに到達できない場合は、設定ファイル内の自己ホスト型の静的コンテンツの場所を参照して、デフォルトのエラーページを上書きします |
| [CDN パージ ](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | CDN のパージに使用するパージ API キーを宣言 |
| [ 顧客の管理による CDN HTTP トークン ](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Adobe CDN をカスタマー CDN から呼び出すために必要な X-AEM-Edge-Key の値を宣言します。 |
| [基本認証](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | 特定の URL を保護する基本認証ダイアログのユーザー名とパスワードを宣言します [ （早期導入ユーザーのみ使用可能） ](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter) |
| [ バージョンパージのメンテナンスタスク ](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | コンテンツバージョンをパージするタイミングに関するルールを宣言して、AEM リポジトリを最適化します |
| [ 監査ログパージのメンテナンスタスク ](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | ログをパージするタイミングに関するルールを宣言することで、AEM監査ログのパフォーマンスを向上させ、最適化します |
| [ ログ転送 ](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | まだ使用できません – 様々な宛先（Splunk、Datadog、HTTPS など）にログを転送するためのエンドポイントと資格情報を設定します |

## 設定パイプラインの作成と管理 {#creating-and-managing}

パイプラインの作成および設定方法について詳しくは、[CI/CD パイプライン ](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline) ドキュメントを参照してください。

Cloud Managerで Config パイプラインを作成する場合は、パイプラインの設定時に **フルスタックコード** ではなく **ターゲットデプロイメント** を選択してください。

## 共通の構文 {#common-syntax}

各設定ファイルは、次のサンプルスニペットに類似したプロパティで始まります。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
```

| プロパティ | 説明 | デフォルト |
|---|---|---|
| `kind` | ログ転送、トラフィックフィルタールール、リクエスト変換などの設定のタイプを決定する文字列 | 必須、デフォルトなし |
| `version` | スキーマバージョンを表す文字列 | 必須、デフォルトなし |
| `envTypes` | この文字列の配列は、`metadata` ノードの子プロパティです。 可能な値は、開発、ステージ、実稼動、または任意の組み合わせであり、設定を処理する環境タイプを決定します。 例えば、配列に `dev` のみが含まれている場合、設定がステージング環境または実稼動環境にデプロイされていても、設定は読み込まれません。 | すべての環境タイプ（開発、ステージ、実稼動） |

`yq` ユーティリティを使用して、設定ファイル（`yq cdn.yaml` など）の YAML 形式をローカルで検証できます。

## フォルダー構造 {#folder-structure}

`/config` または同様の名前のフォルダーがツリーの上部に表示され、ツリー内のどこかにもう 1 つの YAML ファイルが存在する必要があります。

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

`/config` の下のフォルダー名とファイル名は任意です。 ただし、YAML ファイルには有効な [`kind` プロパティ値が含まれている必要があります。](#configurations)

通常、設定はすべての環境にデプロイされます。 すべてのプロパティ値が各環境で同じ場合は、1 つの YAML ファイルで十分です。 ただし、プロパティの値は、環境間で異なることが一般的です（例えば、より低い環境のテスト時）。

以下の節では、ファイルを構造化するための戦略をいくつか説明します。

### すべての環境に対して 1 つの設定ファイル {#single-file}

ファイル構造は次のようになります。

```text
/config
  cdn.yaml
  logForwarding.yaml
```

この構造は、すべての環境とすべてのタイプの設定（CDN、ログ転送など）で同じ設定で十分な場合に使用します。 このシナリオでは、`envTypes` 配列プロパティにすべての環境タイプが含まれます。

```yaml
   kind: "cdn"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

秘密鍵タイプの環境変数を使用すると、`${{SPLUNK_TOKEN}}` 参照で示すように、環境ごとに [ 秘密鍵プロパティ ](#secret-env-vars) を変更できます

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

プロパティ値に違いがある可能性がある場合は、この構造を使用します。 ファイルでは、`envTypes` の配列値がサフィックスに対応していることを想定します。例えば、次のようになります
値が `["dev"]` の `cdn-dev.yaml` および `logForwarding-dev.yaml`、値が `["stage"]` の `cdn-stage.yaml` および `logForwarding-stage.yaml` など。

### 環境ごとのフォルダー {#folder-per-env}

この方法では、環境ごとに個別の `config` フォルダーがあり、それぞれに対して個別のパイプラインがCloud Managerで宣言されます。

この方法は、開発環境が複数あり、それぞれに一意のプロパティ値がある場合に特に便利です。

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

このアプローチのバリエーションは、環境ごとに個別のブランチを維持することです。

## シークレットの環境変数 {#secret-env-vars}

ソース管理に機密情報を保存する必要がないように、設定ファイルでは **secret** タイプのCloud Manager環境変数をサポートしています。 ログ転送などの一部の設定では、特定のプロパティに対してシークレットの環境変数が必須です。

以下のスニペットは、シークレット環境変数 `${{SPLUNK_TOKEN}}` が設定でどのように使用されるかを示しています。

```
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

環境変数の使用方法について詳しくは、[Cloud Manager環境変数 ](/help/implementing/cloud-manager/environment-variables.md) を参照してください。
