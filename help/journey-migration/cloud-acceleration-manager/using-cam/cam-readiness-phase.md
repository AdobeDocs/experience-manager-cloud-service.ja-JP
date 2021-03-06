---
title: Cloud Acceleration Manager での準備フェーズ
description: このページでは、Cloud Acceleration Manager における準備フェーズの概要について説明します。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 100%

---

# Cloud Acceleration Manager での準備フェーズ {#readiness-phase-cam}

Cloud Acceleration Manager でプロジェクトを作成したら、準備フェーズで現在の AEM 実装の評価を開始できます。

準備フェーズには以下が含まれます。

* [ベストプラクティス分析](#best-practices-analysis)
* [計画とセットアップ](#planning-setup)

準備フェーズに移動するには、次の手順に従います。

1. プロジェクトカードをクリックして、プロジェクトのランディングページを開きます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 「**準備**」セクションに移動します（下図を参照）。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >詳しくは、「Cloud Acceleration Manager でのプロジェクトの作成と管理」を参照してください。

## ベストプラクティス分析カードの使用 {#best-practices-analysis}

ベストプラクティス分析カードを使用するには、次の手順に従います。

1. **ベストプラクティス分析** カードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. ベストプラクティスアナライザー（BPA）をダウンロードするには、次の手順に従います。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、実稼動環境にできる限り近いオーサー環境で BPA を実行することをお勧めします。または、実稼動版のオーサー環境のクローンで実行することもできます。

   1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) ポータルに移動し、ベストプラクティスアナライザーを zip ファイルとしてダウンロードします。

      >[!NOTE]
      >BPA の実行方法については、 [ベストプラクティスアナライザーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja#imp-considerations) を参照してください。

   1. レポートを CSV 形式で書き出します。

1. 「**新しいレポートをアップロード**」をクリックして、BPA レポートを CAM にアップロードします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >ブラウザーの匿名モードになっている場合は、レポートをアップロードできません。

1. 新しいレポートをアップロードしたら、ベストプラクティス分析レポートが表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. CAM のベストプラクティス分析ダッシュボードを確認し、表示内容を検討します。詳しくは、次の [ベストプラクティス分析レポートの確認](#analysis-report) の節を参照してください。

   >[!NOTE]
   >新しいレポートをアップロードすると、すべての評価がリセットされます。

### 印刷プレビューの使用 {#print-preview-cam}

Cloud Acceleration Manager で印刷プレビューオプションを選択して、レポートの印刷可能なプレビューを表示したり、レポートを PDF 形式に出力して共有しやすくすることができます。

次の手順に従います。

1. 「**印刷プレビュー**」アイコンをクリックします（下図を参照）。

   ![画像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. 「**印刷プレビュー**」をクリックすると、新しいタブが開き、印刷可能なプレビューでレポートが表示されます。「**印刷**」をクリックして、レポートを PDF 形式で出力します。

   >[!IMPORTANT]
   >* 上記の機能には、「**PDF として保存**」オプションをお勧めします。このオプションはサポートされています。
   >* ブラウザの印刷ボタンを使用すると、1 ページのみ印刷されます。


   ![画像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 「トレンドラインを表示」の使用 {#trendline-view-cam}

1 つのプロジェクトに複数のベストプラクティスアナライザー（BPA）レポートをアップロードする場合、「**トレンドラインを表示**」オプションを選択して、履歴 BPA レポートの結果を表示および比較できます。

トレンドラインオプションからレポートを表示するには、次の手順に従います。

>[!NOTE]
>1 つのプロジェクトに複数の BPA レポートをアップロードすると、 「**...**」アイコンが表示されます。

1. プロジェクトに移動し、 **準備** 段階の **ベストプラクティス分析** カードから「**レビュー**」をクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 「**...**」アイコンをクリックしてドロップダウンを表示します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >表示されるレポートは常に、最新のレポート日付を持つレポートです。

1. 「**トレンドラインを表示**」をクリックします（下図を参照）。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 「**トレンドラインを表示**」をクリックすると、次の図に示すように、レポートのトレンドライン表示が開きます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >トレンドラインレポートには、履歴 BPA レポートの結果がグラフで表示されます。
   >
   >次の項目のトレンドを示す 2 つのグラフが表示されます。
   >1. **レポート結果のトレンド**
   >1. **カスタムコンポーネントとテンプレートのトレンド**
   >
   >次の図に示すように、ドロップダウンからグラフィック表示を追加または変更できます。
   >![画像](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### ベストプラクティス分析レポートの確認 {#analysis-report}

ベストプラクティス分析レポートページで使用可能な以下のカードの情報を検討します。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 各カードには、次の機能があります。
>* 各カードをクリックして、関連するタブを開く
>* 共有または後日取得するために、すべてのレポートタブ（フィルタリングを含む）をブックマークする
>* 詳細アイコンを使用して、各レポートの結果の詳細を表示する


#### レポートのプロパティ {#report-properties}

**レポートのプロパティ**&#x200B;カードでは、レポートの日付、期間、フィルター、アップロード日、Adobe Experience Manager（AEM）の詳細など、レポートのプロパティに関する情報を提供します。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### レポートの概要 {#report-overview}

この&#x200B;**レポートの概要**&#x200B;カードでは、AEM as a Cloud Service に移行するための準備状況を評価する際に適用される、レポートの結果と重大度レベルを示します（下図を参照）。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

このレポートをクリックすると、「**レポート**」タブが開きます。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

重要度、サブタイプまたはカウントに基づいてレポートをフィルタリングできます。

![画像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>結果カテゴリと重要度レベルについては、 [ベストプラクティスアナライザーレポートの説明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja) を参照してください。

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

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 「計画とセットアップ」カードの使用 {#planning-setup}

この節では、「計画とセットアップ」アクティビティカードについて説明します。

1. **計画とセットアップ**&#x200B;カードの「**表示**」ボタンをクリックします。このカードには、AEM 移行の計画とセットアップに役立つ、すべての関連コンテンツが用意されています。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. コンテンツカルーセルには、移行ジャーニーのこのフェーズに関係のあるすべての情報が表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### ベストプラクティス分析レポートの削除 {#delete-trendline}

トレンドライン表示からレポートを削除するには、次の手順に従います。

>[!IMPORTANT]
>レポートは、複数のレポートがプロジェクトにアップロードされている場合にのみ削除できます。

1. プロジェクトに移動し、 **準備** 段階の **ベストプラクティス分析** カードから「**レビュー**」をクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 「**...**」アイコンをクリックしてドロップダウンを表示します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 「**トレンドラインを表示**」をクリックします（下図を参照）。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. **トレンドラインレポート** 画面の削除アイコンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 「**削除**」をクリックして、削除を確認します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法とプロジェクトの作成方法を理解したら、次のステップの[実装フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=ja)に進みます。
