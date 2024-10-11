---
title: コードのデプロイ
description: AEM as a Cloud Service の Cloud Manager パイプラインを使用してコードをデプロイする方法を説明します。
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2573eb5f8a8ff21a8e30b94287b554885cd1cd89
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 41%

---


# コードのデプロイ {#deploy-your-code}

AEM as a Cloud Service の Cloud Manager パイプラインを使用して、コードを実稼動環境にデプロイする方法を説明します。

![実稼働パイプラインのダイアグラム](./assets/configure-pipeline/production-pipeline-diagram.png)

コードをステージング環境に、さらには実稼動環境にシームレスにデプロイするには、実稼動パイプラインを使用します。 実稼動パイプラインの実行は、次の 2 つの論理フェーズに分かれます。

1. **ステージング環境へのデプロイメント** - コードは構築され、ステージング環境にデプロイされて、自動化された機能テスト、UI テスト、エクスペリエンス監査、ユーザー受け入れテスト（UAT）が行われます。
1. **実稼動環境へのデプロイメント** - ビルドがステージング環境で検証され、実稼動環境への昇格が承認されると、同じビルドアーティファクトが実稼動環境にデプロイされます。

_コードスキャン、機能テスト、UI テスト、エクスペリエンス監査をサポートしているのは、フルスタックコードパイプラインタイプのみです。_

## デプロイメントプロセス {#deployment-process}

Cloud Service のすべてのデプロイメントでは、ダウンタイムをなくすために、ローリングプロセスに従います。詳しくは、[ローリングデプロイメントの仕組み](/help/implementing/deploying/overview.md#how-rolling-deployments-work)を参照してください。

>[!NOTE]
>
>Dispatcher のキャッシュは、デプロイメントのたびに消去されます。その後、新しいパブリッシュノードがトラフィックを受け入れる前に「ウォームアップ」されます。

## AEM as a Cloud ServiceのCloud Managerでコードをデプロイします {#deploying-code-with-cloud-manager}

リポジトリー、環境およびテスト環境を含め、[実稼動パイプラインを設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)したら、コードをデプロイする準備が整います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、コードをデプロイするプログラムをクリックします。

1. **概要** ページのコールトゥアクション領域で、「**デプロイ**」をクリックします。

   ![CTA](assets/deploy-code1.png)

1. **実稼動へのデプロイ** ページで、「**ビルド**」をクリックします。

   ![パイプライン実行画面](assets/deploy-code2.png)

ビルドプロセスでは、次の 3 つの順序付けられたフェーズを通じてコードがデプロイされます。

1. [ステージデプロイメントフェーズ](#stage-deployment)
1. [ステージテストフェーズ](#stage-testing)
1. [実稼動デプロイメントフェーズ](#production-deployment)

>[!TIP]
>
>テスト条件のログを表示したり結果を確認したりすることで、様々なデプロイメントプロセスのステップを確認できます。

### ステージデプロイメントフェーズ {#stage-deployment}

**ステージデプロイメント** フェーズには、次のステップが含まれます。

| ステージデプロイメント手順 | 説明 |
| --- | --- |
| 検証 | 現在使用可能なリソースを使用するようにパイプラインが設定されていることを確認します。 例えば、設定済みのブランチが存在し、環境が使用可能であることをテストします。 |
| ビルドおよび単体テスト | コンテナ化されたビルドプロセスを実行します。<br> ビルド環境について詳しくは、[ ビルド環境の詳細 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) を参照してください。 |
| コードスキャン | アプリケーションコードの品質を評価します。<br> テストプロセスについて詳しくは、[ コード品質テスト ](/help/implementing/cloud-manager/code-quality-testing.md) を参照してください。 |
| 画像を作成 | このプロセスでは、ビルドステップのコンテンツパッケージとDispatcher パッケージが Docker イメージに変換されます。 また、これらのパッケージに基づいて Kubernetes 設定も生成します。 |
| ステージにデプロイ | [ ステージテストステージ ](#stage-testing) に備えて、イメージがステージング環境にデプロイされます。 |

![ステージデプロイメント](assets/stage-deployment.png)

### ステージテストフェーズ {#stage-testing}

**ステージテスト** フェーズには、次のステップが含まれます。

| ステージテスト手順 | 説明 |
| --- | --- |
| 製品機能テスト | Cloud Manager パイプラインは、ステージング環境に照らして実行されるテストを実行します。<br>[ 製品機能テスト ](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) も参照してください。 |
| カスタム機能テスト | パイプラインのこのステップは常に実行され、スキップできません。 ビルドでテスト JAR が生成されない場合、テストは自動的に合格します。<br>[ カスタム機能テスト ](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) も参照してください。 |
| カスタム UI テスト | カスタムアプリケーション用に作成された UI テストを自動的に実行するオプション機能。<br>UI テストは Selenium ベースで、言語とフレームワークに柔軟性を持たせるために Docker イメージにパッケージ化されています。 このアプローチを使用すると、Java と Maven、Node と WebDriver.io、または Selenium ベースのフレームワークやテクノロジーを使用できます。<br>[ カスタム UI テスト ](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) も参照してください。 |
| エクスペリエンス監査 | パイプラインのこのステップは常に実行され、スキップできません。 実稼動パイプラインの実行時に、チェックを実行するカスタム機能テストの後に、エクスペリエンスの監査手順が組み込まれます。<ul><li>設定されたページがサービスに送信され、評価されます。</li><li>結果は情報提供であり、スコアおよび現在のスコアと以前のスコア間の変化を示します。</li><li>このインサイトは、現在のデプロイメントでリグレッションが導入されいないか判断するのに役立ちます。</li></ul>[ エクスペリエンス監査結果について ](/help/implementing/cloud-manager/experience-audit-dashboard.md) を参照してください。</li></ul> |

![ステージテスト](assets/stage-testing.png)

### 実稼動デプロイメントフェーズ {#production-deployment}

AEM サイト訪問者への影響を最小限に抑えるために、実稼動トポロジへのデプロイプロセスはわずかに異なります。

実稼動デプロイメントは、通常、前述と同じステップに従いますが、周期的な方法で実行されます。 手順は次のとおりです。

1. オーサーに AEM パッケージをデプロイします。
1. ロードバランサーから `dispatcher1` を分離します。
1. AEM パッケージを `publish1` にデプロイし、Dispatcher パッケージを `dispatcher1` にデプロイして、Dispatcher キャッシュをフラッシュします。
1. `dispatcher1` をロードバランサーに戻します。
1. `dispatcher1` がサービスを再開したら、ロードバランサーから `dispatcher2` を切り離します。
1. AEM パッケージを `publish2` にデプロイし、Dispatcher パッケージを `dispatcher2` にデプロイして、Dispatcher キャッシュをフラッシュします。
1. `dispatcher2` をロードバランサーに戻します。

このプロセスは、デプロイメントがトポロジのすべてのパブリッシャーおよび Dispatcher に到達するまで続行されます。

![実稼動デプロイメントフェーズ](assets/production-deployment.png)

## デプロイメント中のタイムアウト {#timeouts}

デプロイメント中にユーザーからのフィードバックを待ち続けると、次の手順はタイムアウトします。

| ステップ | タイムアウト |
|--- |--- |
| コード品質テスト | 14 日 |
| セキュリティテスト | 14 日 |
| パフォーマンステスト | 14 日 |
| アプリケーションの承認 | 14 日 |
| 実稼動デプロイメントをスケジュール | 14 日 |
| CSE サポート | 14 日 |

## 実稼動デプロイメントの再実行 {#reexecute-deployment}

まれに、一時的な理由で実稼動デプロイメントステップが失敗すること場合があります。その場合、実稼動デプロイメントステップの再実行がサポートされるのは、完了のタイプ（キャンセルや失敗など）に関係なく、実稼動デプロイメントステップが完了している限りです。 再実行では、次の 3 つのステップで構成される同じパイプラインを使用して新しい実行を作成します。

1. **検証** – 通常のパイプライン実行時に行われる検証と同じ検証。
1. **ビルド** – 再実行のコンテキストでは、ビルドステップは、新しいビルドプロセスを実際に実行するのではなく、アーティファクトをコピーします。
1. **実稼動デプロイメント** – 通常のパイプライン実行における実稼動デプロイメントステップと同じ設定およびオプションを使用します。

再実行が可能な状況では、実稼動パイプラインステータスページには、通常の「**ビルドログをダウンロード**」オプションの横に「**再実行**」オプションが表示されます。

![パイプラインの概要ウィンドウの「再実行」オプション](assets/re-execute.png)

>[!NOTE]
>
>再実行の場合、ビルドステップには UI でラベルが付けられて、アーティファクトを再ビルドではなくコピーしていることが示されます。

### 制限事項 {#limitations}

* 実稼動デプロイメントステップの再実行は、最後の実行に対してのみ使用できます。
* プッシュ更新実行には、再実行を使用できません。 最後の実行がプッシュ更新実行の場合、再実行はできません。
* 実稼動デプロイメントステップ以前の任意の時点で最後の実行が失敗した場合、再実行はできません。

### API の再実行 {#reexecute-API}

UI で使用できるだけでなく、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) を使用して再実行をトリガーしたり、再実行としてトリガーされた実行を識別したりすることもできます。

#### 再実行のトリガー {#reexecute-deployment-api}

再実行をトリガーするには、実稼動デプロイメントステップの状態で HAL リンク（`https://ns.adobe.com/adobecloud/rel/pipeline/reExecute`）に対して PUT リクエストを行います。

* このリンクが存在する場合は、そのステップから実行を再開できます。
* 存在しない場合は、そのステップから実行を再開することはできません。

このリンクは、実稼動デプロイメントステップでのみ使用できます。

```JavaScript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```

HAL リンクの href 値の構文は一例に過ぎません。実際の値は、常に HAL リンクから読み取られるべきものであり、生成されるものではありません。

このエンドポイントにPUTリクエストを送信すると、成功した場合は 201 応答が返され、応答の本文には新しい実行が表現されています。 このワークフローは、API を使用して通常の実行を開始する場合と似ています。

#### 再実行の識別 {#identify-reexecution}

システムは、`trigger` フィールドに値 `RE_EXECUTE` を設定することで再実行を識別します。
