---
title: コードのデプロイ - Cloud Services
description: コードのデプロイ - Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: bcd106a39bec286e2a09ac7709758728f76f9544
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 95%

---

# コードのデプロイ {#deploy-your-code}

## AEM as a Cloud Service での Cloud Manager を使用したコードのデプロイ {#deploying-code-with-cloud-manager}

実稼動パイプライン（リポジトリー、環境、テスト環境）を設定したら、コードをデプロイする準備が整います。

1. Cloud Manager で「**デプロイ**」をクリックして、デプロイメントプロセスを開始します。

   ![](assets/deploy-code1.png)


1. **パイプライン実行**&#x200B;画面が表示されます。

   「**ビルド**」をクリックしてプロセスを開始します。

   ![](assets/deploy-code2.png)

1. 完全なビルドプロセスによってコードがデプロイされます。

   ビルドプロセスには、以下のステージが含まれます。

   1. ステージのデプロイメント
   1. ステージテスト
   1. 実稼動のデプロイメント

   >[!NOTE]
   >
   >さらに、テスト条件のログを表示したり、結果を確認したりすることで、様々なデプロイメントプロセスから手順を確認できます。

   **ステージのデプロイメント**&#x200B;には、以下の手順が含まれます。

   * 検証：この手順では、現在使用できるリソース（設定済みのブランチが存在する場合など）を使用するようにパイプラインが設定され、環境が使用できることを確認します。
   * ビルドおよび単体テスト：この手順では、コンテナ化されたビルドプロセスを実行します。ビルド環境について詳しくは、「[ビルド環境の詳細](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)」を参照してください。
   * コードスキャン：この手順では、アプリケーションコードの品質を評価します。テストプロセスの詳細については、「[コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)」を参照してください。
   * イメージのビルド：このステップには、イメージのビルドに使用されたプロセスのログファイルが含まれます。このプロセスでは、ビルドステップで生成されたコンテンツおよび Dispatcher パッケージを Docker イメージと Kubernetes 設定に変換します。
   * ステージへのデプロイ

      ![](assets/stage-deployment.png)
   **ステージテスト**&#x200B;には、以下のステップが含まれます。

   * **製品機能テスト**：Cloud Manager のパイプライン実行では、ステージ環境に対するテストの実行をサポートしています。
詳しくは、「[製品機能テスト](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)」を参照してください。

   * **カスタム機能テスト**：パイプライン内のこのステップは常に存在し、スキップできません。ただし、ビルドでテスト JAR が生成されない場合、テストはデフォルトで合格します。\
      詳しくは、「[カスタム機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)」を参照してください。

   * **カスタム UI テスト**：（オプション）顧客はアプリケーションの UI テストを作成し、自動的に実行できます。UI テストは、言語とフレームワークの幅広い選択肢（Java と Maven、Node と WebDriver.io、Selenium に基づいて構築されたその他のフレームワークとテクノロジーなど）を可能にするために Docker イメージにパッケージ化された Selenium ベースのテストです。詳しくは、[カスタム UI テスト](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=ja#custom-ui-testing)を参照してください。


   * **エクスペリエンス監査**：パイプライン内のこのステップは常に存在し、スキップできません。実稼動パイプラインの実行時に、チェックを実行するカスタム機能テストの後に、エクスペリエンスの監査手順が組み込まれます。設定されたページがサービスに送信され、評価されます。結果は情報提供であり、ユーザーはスコアおよび現在のスコアと以前のスコアの変化を確認できます。このインサイトは、現在のデプロイメントで前のバージョンになかった不具合が導入されるかどうかを判断するのに役立ちます。
詳しくは、「[エクスペリエンス監査結果について](/help/implementing/cloud-manager/experience-audit-testing.md)」を参照してください。

      ![](assets/stage-testing.png)





## デプロイメントプロセス {#deployment-process}

すべてのCloud Serviceデプロイメントは、周期的なプロセスに従って、ダウンタイムをゼロにします。 詳しくは、[ローリングデプロイメントの仕組み](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#how-rolling-deployments-work)を参照してください。

### 実稼動フェーズへのデプロイメント {#deployment-production-phase}

AEM サイト訪問者への影響を最小限に抑えるために、実稼動トポロジへのデプロイプロセスはわずかに異なります。

実稼動のデプロイメントは、通常、上記と同じ手順に従いますが、周期的な方法で実行します。

1. オーサーに AEM パッケージをデプロイします。
1. dispatcher1 をロードバランサーから分離します。
1. AEM パッケージを publish1 にデプロイし、Dispatcher を dispatcher1 にデプロイして、Dispatcher キャッシュをフラッシュします。
1. dispatcher1 をロードバランサーに戻します。
1. dispatcher1 がサービスを再開したら、dispatcher2 をロードバランサーから分離します。
1. AEM パッケージを publish2 にデプロイし、Dispatcher パッケージを dispatcher2 にデプロイして、Dispatcher キャッシュをフラッシュします。
1. dispatcher2 をロードバランサーに戻します。
このプロセスは、デプロイメントがトポロジのすべてのパブリッシャーおよび Dispatcher に到達するまで続行されます。
