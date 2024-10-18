---
title: プライベートリポジトリの GitHub チェック設定
description: プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0a08d5fc033f4f4f57b824492766e5b42a801b6e
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 33%

---

# プライベートリポジトリの GitHub チェック設定 {#github-check-config}

プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。

## GitHub チェック設定 {#configuration}

[プライベートリポジトリ](private-repositories.md#using)を使用すると、[フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)が自動的に作成されます。このパイプラインは、プルリクエストの更新のたびに開始されます。

プライベートリポジトリのデフォルトブランチに `.cloudmanager/pr_pipelines.yml` 設定ファイルを作成すると、これらのチェックを制御できます。

```yaml
github:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| パラメーター | 可能な値 | デフォルト | 説明 |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` または `false` | `false` | この GitHub プルリクエストで、コードスキャンの結果を含んだ最後のコメントのみを保持するか、すべてを保持するか。 `false` （デフォルト）に設定すると、以前のコメントは削除されません。 |
| `shouldSkipCheckAnnotations` | `true` または `false` | `false` | GitHub プルリクエストチェックに追加の注釈が表示されているかどうか。 これを `false` （デフォルト）に設定すると、チェック注釈はスキップされず、フィードバックに含められます。 |
| `type` | `CI_CD` | 該当なし | CI/CD （継続的統合/継続的デプロイメント）パイプライン設定の動作を定義します。 |
| `template.programId` | 整数 | パイプライン変数は再使用されない | これを使用すると、各プルリクエストによって自動的に作成された既存のパイプラインに設定された [ パイプライン変数 ](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) を再利用できます。 |
| `template.pipelineId` | 整数 | パイプライン変数は再使用されない | これを使用すると、各プルリクエストによって自動的に作成された既存のパイプラインに設定された [ パイプライン変数 ](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) を再利用できます。 |
| `namePrefix` | 文字列 | `Full Stack Code Quality Pipeline for PR` | 自動的に作成されるパイプラインの名前のプレフィックスを設定するために使用されます。 |
| `importantMetricsFailureBehavior` | `CONTINUE` または `FAIL` または `PAUSE` | `CONTINUE` | パイプラインの重要な指標の動作を設定し <br>`CONTINUE` す。=重要な指標が失敗した場合、パイプラインは自動的に先に進みます <br>`FAIL` =重要な指標が失敗した場合、パイプラインは失敗ステータスで終了します <br>`PAUSE` = コードスキャンステップは、重要な指標が失敗した場合、待機中ステータスを受け取り、手動で再開する必要があります |




