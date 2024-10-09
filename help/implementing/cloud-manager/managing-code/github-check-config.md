---
title: プライベートリポジトリの GitHub チェック設定
description: プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6eabf593a7566129d32d9a5888cc480117bef51f
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 63%

---

# プライベートリポジトリの GitHub チェック設定 {#github-check-config}

プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。

## GitHub チェック設定 {#configuration}

[プライベートリポジトリ](private-repositories.md#using)を使用すると、[フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)が自動的に作成されます。このパイプラインは、プルリクエストの更新のたびに開始されます。

プライベートリポジトリのデフォルトブランチに `.cloudmanager/pr_pipelines.yml` ファイルを作成して、これらのチェックを制御できます。

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| パラメーター | 可能な値 | デフォルト | 説明 |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` か `false` のいずれか | `false` | この GitHub プルリクエストで、コードスキャン結果の最後のコメントのみを保持するか、すべてを保持するか |
| `type` | `CI_CD` | n/a | CI/CD パイプラインの動作を定義します |
| `template.programID` | 整数 | パイプライン変数は再使用されない | これを使用すると、各プルリクエストによって自動的に作成された既存のパイプラインに設定された [ パイプライン変数 ](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) を再利用できます。 |
| `template.pipelineID` | 整数 | パイプライン変数は再使用されない | これを使用すると、各プルリクエストによって自動的に作成された既存のパイプラインに設定された [ パイプライン変数 ](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) を再利用できます。 |
| `namePrefix` | 文字列 | `Full Stack Code Quality Pipeline for PR` | 自動的に作成されるパイプライン名の設定に使用します |
| `importantMetricsFailureBehavior` | `CONTINUE` または `FAIL` または `PAUSE` | `CONTINUE` | パイプラインの重要な指標の動作を設定し <br>`CONTINUE` す。=重要な指標が失敗した場合、パイプラインは自動的に先に進みます <br>`FAIL` =重要な指標が失敗した場合、パイプラインは失敗ステータスで終了します <br>`PAUSE` = コードスキャンステップは、重要な指標が失敗した場合、待機中ステータスを受け取り、手動で再開する必要があります |
