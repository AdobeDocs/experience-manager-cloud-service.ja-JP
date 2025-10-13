---
title: プライベートリポジトリのプルリクエストチェック
description: プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0ec47218d598aad6b225a9d5d8faeab20e606716
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# プライベートリポジトリのプルリクエストチェック {#github-check-config}

プライベートリポジトリへの各プルリクエストを検証する自動的に作成されるパイプラインを制御する方法について説明します。

## プライベートリポジトリのチェックの設定 {#configuration}

[プライベートリポジトリ](private-repositories.md#using)を使用すると、[フルスタックコード品質パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)が自動的に作成されます。このパイプラインは、プルリクエストを更新するたびに開始されます。

プライベートリポジトリのデフォルトのブランチに `.cloudmanager/pr_pipelines.yml` 設定ファイルを作成して、これらのチェックを制御できます。

```yaml
pullRequest:
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
| `shouldDeletePreviousComment` | `true` または `false` | `false` | この GitHub プルリクエストで、コードスキャン結果の最後のコメントのみを保持するか、すべてを保持するか。これを `false`（デフォルト）に設定すると、以前のコメントは削除されません。 |
| `shouldSkipCheckAnnotations` | `true` または `false` | `false` | GitHub プルリクエストチェックに追加の注釈が存在するか。これを `false`（デフォルト）に設定すると、チェック注釈はスキップされず、フィードバックに含まれます。 |
| `type` | `CI_CD` | 該当なし | CI/CD（継続的統合/継続的デプロイメント）パイプライン設定の動作を定義します。 |
| `template.programId` | 整数 | パイプライン変数は再使用されない | 各プルリクエストによって自動的に作成される既存のパイプラインに設定されている[パイプライン変数](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)を再利用するために使用できます。 |
| `template.pipelineId` | 整数 | パイプライン変数は再使用されない | 各プルリクエストによって自動的に作成される既存のパイプラインに設定されている[パイプライン変数](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)を再利用するために使用できます。 |
| `namePrefix` | 文字列 | `Full Stack Code Quality Pipeline for PR` | 自動的に作成されるパイプラインの名前の接頭辞を設定するのに使用されます。 |
| `importantMetricsFailureBehavior` | `CONTINUE` または `FAIL` または `PAUSE` | `CONTINUE` | パイプラインの重要な指標動作を設定します <br>`CONTINUE` = 重要な指標が失敗した場合、パイプラインは自動的に前方向へ移動します <br>`FAIL` = 重要な指標が失敗した場合、パイプラインは失敗ステータスで終了します <br>`PAUSE` = 重要な指標が失敗し、手動で再開する必要がある場合、コードスキャンステップでは待機中ステータスを受け取ります |




