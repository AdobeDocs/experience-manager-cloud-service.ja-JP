---
title: Cloud Acceleration Manager での準備フェーズ
description: このページでは、Cloud Acceleration Manager における準備フェーズの概要について説明します。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 97%

---

# Cloud Acceleration Manager での準備フェーズ {#readiness-phase-cam}

Cloud Acceleration Manager（CAM）でプロジェクトを作成したら、準備フェーズで現在の Adobe Experience Manager（AEM）実装の評価を開始できます。

準備フェーズには以下が含まれます。

* [ベストプラクティス分析](#best-practices-analysis)
* [計画とセットアップ](#planning-setup)

準備フェーズに移動するには、次の手順に従います。

1. プロジェクトカードをクリックします。

   ![プロジェクトカード](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. プロジェクトのランディングページで、「**準備**」セクションに移動します（下図を参照）。

   ![準備](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >詳しくは、Cloud Acceleration Manager でのプロジェクトの作成と管理を参照してください。

## ベストプラクティス分析カードの使用 {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="ベストプラクティス分析レポート"
>abstract="BPA レポートを CAM にアップロードして、AEM as a Cloud Service への移行に関する分析を提供できます。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="ベストプラクティスアナライザーの使用"

1. **ベストプラクティス分析**&#x200B;カードの「**レビュー**」をクリックします。

   ![ベストプラクティス分析 - レビュー](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. ベストプラクティスアナライザー（BPA）をダウンロードします。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、アドビでは、オーサー環境で BPA を実行することをお勧めします。環境は、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、実稼動環境にできる限り近いものにする必要があります。または、実稼動版のオーサー環境のクローンで実行することもできます。

   1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*)ポータルに移動し、ベストプラクティスアナライザーを zip ファイルとしてダウンロードします。

      >[!NOTE]
      >BPA の実行方法については、[ベストプラクティスアナライザーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja#imp-considerations)を参照してください。

1. CAM で「**アップロードキーを取得**」をクリックすると、BPA レポートを CAM に直接自動的にアップロードするためのシステム設定に必要なキーを取得できます。

   ![アップロードキーを取得](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >レポートは手動でアップロードすることもできますが、アップロードキーを使用すると操作が効率化されます。レポートのサイズが約 200 MB 以上の場合、手動でアップロードすることはできないことに注意してください。 また、ブラウザーの匿名モードを使用してレポートをアップロードすることもできません。

1. 新しいレポートがアップロードされると、CAM でベストプラクティス分析レポートを表示できます。

   ![ベストプラクティス分析レポート](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >複数の異なるレポートをアップロードする場合、詳細が表示されるレポートは、常に（アップロード日ではなく）作成日が最新のレポートです。

1. CAM のベストプラクティス分析ダッシュボードを確認し、表示内容を検討します。詳しくは、[ベストプラクティス分析レポートの確認](#analysis-report)を参照してください。

   >[!NOTE]
   >新しいレポートをアップロードすると、以前に読み込んだレポートよりも新しい場合、すべての評価がリセットされます。

### 印刷プレビューの使用 {#print-preview-cam}

Cloud Acceleration Manager で印刷プレビューオプションを選択して、レポートの印刷可能なプレビューを表示したり、共有しやすいようにレポートを PDF 形式で印刷したりできます。

次の手順に従います。

1. **印刷プレビュー**&#x200B;アクションをクリックします。

   ![印刷プレビュー](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. レポートが印刷可能なプレビューに表示された新しいタブで、「**印刷**」をクリックして、レポートを PDF 形式で印刷します。

   >[!IMPORTANT]
   >
   >* 上記の機能には、「**PDF として保存**」オプションをお勧めします。このオプションはサポートされています。
   >* ブラウザーの印刷ボタンを使用すると、1 ページのみが印刷されます。

   ![印刷](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 「トレンドラインを表示」の使用 {#trendline-view-cam}

1 つのプロジェクトに複数の個別のベストプラクティスアナライザー（BPA）レポートをアップロードする場合、「**トレンドラインを表示**」オプションを選択して、履歴 BPA レポートの結果を表示および比較できます。

トレンドラインオプションからレポートを表示するには、次の手順に従います。

>[!NOTE]
>1 つのプロジェクトに複数の個別の BPA レポートをアップロードすると、「**...**」アイコンが表示されます。ホストと作成時間が同じ場合、レポートは同じ（個別ではない）と見なされます。

1. プロジェクトに移動し、**準備**&#x200B;フェーズの&#x200B;**ベストプラクティス分析**&#x200B;カードから「**レビュー**」をクリックします。

   ![ベストプラクティス分析 - レビュー](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. **表示**&#x200B;ドロップダウンリストから、「**トレンドラインレポート**」をクリックします（下図を参照）。

   ![トレンドラインレポート](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 「**トレンドラインレポート**」をクリックすると、レポートのトレンドライン表示が開きます。

   ![トレンドライン表示](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >トレンドラインレポートには、履歴 BPA レポートの結果がグラフで表示されます。
   >
   >次の項目のトレンドを示す 2 つのグラフが表示されます。
   > 
   >1. **レポート結果のトレンド**
   >1. **カスタムコンポーネントとテンプレートのトレンド**
   >
   >次の図に示すように、ドロップダウンからグラフィック表示を追加または変更できます。
   >![グラフィック表示の選択](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### ベストプラクティス分析レポートの確認 {#analysis-report}

ベストプラクティス分析レポートページで使用可能な以下のカードの情報を検討します。

![ベストプラクティス分析レポート](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 各カードを使用すると、次の操作を実行できます。
>
>* 関連するタブを開く
>* 共有または後日取得するために、すべてのレポートタブ（フィルタリングを含む）をブックマークする
>* 詳細アイコンを使用して、各レポートの結果の詳細を表示する

#### レポートのプロパティ {#report-properties}

**レポートのプロパティ**&#x200B;カードでは、レポートの日付、期間、フィルター、アップロード日、Adobe Experience Manager（AEM）の詳細など、レポートのプロパティに関する情報を提供します。

![レポートのプロパティ](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### レポートの概要 {#report-overview}

この&#x200B;**レポートの概要**&#x200B;カードでは、AEM as a Cloud Service に移行するための準備状況を評価する際に適用される、レポートの結果と重大度レベルを示します（下図を参照）。

![レポートの概要](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

このレポートをクリックすると、「**レポート**」タブが開きます。

![「レポート」タブ](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

重要度、サブタイプまたはカウントに基づいてレポートをフィルタリングできます。

![レポートフィルター](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>結果カテゴリと重要度レベルについては、[ベストプラクティスアナライザーレポートの説明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja)を参照してください。

#### ベストプラクティス評価 {#best-practices-assessment}

「ベストプラクティス評価」オプションでは、現在の AEM インスタンスの評価と、次の手順で AEM のベストプラクティスを採用するうえでのガイダンスを提供します。このタブでは、次の情報を確認できます。

* AEM インスタンスの概要
* カスタムコンポーネントとテンプレート
* その他の結果
* 処理に時間のかかるクエリ
* メンテナンスタスク

#### 移行の複雑さの評価 {#migration-complexity-assessment}

「移行の複雑さの評価」オプションでは、既存の AEM 実装を AEM as a Cloud Service に移行する際の複雑さの評価を示します。

このタブでは、次の情報を確認できます。

* AEM インスタンスの概要
* 評価
* コンテンツの移行に関する考慮事項

  ![移行の複雑性の評価](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 「計画とセットアップ」カードの使用 {#planning-setup}

1. **計画と設定**&#x200B;カードの「**表示**」をクリックします。このカードには、AEM 移行の計画と設定に役立つ、すべての関連コンテンツが用意されています。

   ![計画と設定 - 表示](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のあるすべての情報が表示されます。

   ![計画と設定カルーセル](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### トレンドラインビューからのベストプラクティス分析レポートの削除 {#delete-trendline}

>[!IMPORTANT]
>レポートは、複数のレポートがプロジェクトにアップロードされている場合にのみ削除できます。

1. プロジェクトに移動し、**準備**&#x200B;フェーズの&#x200B;**ベストプラクティス分析**&#x200B;カードから「**レビュー**」をクリックします。

   ![ベストプラクティス分析 - レビュー](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 「**...**」をクリックします。

   ![楕円形](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. ドロップダウンリストで、「**トレンドラインを表示**」をクリックします（下の図を参照）。

   ![トレンドラインを表示](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. **トレンドラインレポート**&#x200B;画面の削除アイコンをクリックします。

   ![トレンドラインレポート - 削除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 「**削除**」をクリックして削除を確認します。

   ![削除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法とプロジェクトの作成方法を理解したら、次のステップの[実装フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=ja)に進みます。
