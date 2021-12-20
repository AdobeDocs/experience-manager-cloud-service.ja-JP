---
title: Cloud Acceleration Manager での準備フェーズ
description: このページでは、Cloud Acceleration Manager における準備フェーズの概要について説明します。
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 64%

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

1. **ベストプラクティス分析**&#x200B;カードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. ベストプラクティスアナライザー（BPA）をダウンロードするには、次の手順に従います。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、実稼動環境にできる限り近いオーサー環境で BPA を実行することをお勧めします。または、実稼動版のオーサー環境のクローンで実行することもできます。

   1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)ポータルに移動し、ベストプラクティスアナライザーを zip ファイルとしてダウンロードします。

      >[!NOTE]
      >BPA の実行方法については、[ベストプラクティスアナライザーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja#imp-considerations)を参照してください。

   1. レポートを CSV 形式で書き出します。

1. 「**新しいレポートをアップロード**」をクリックして、BPA レポートを CAM にアップロードします。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >ブラウザーの匿名モードの場合は、レポートをアップロードできません。

1. 新しいレポートをアップロードしたら、ベストプラクティス分析レポートが表示されます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. CAM のベストプラクティス分析ダッシュボードを確認し、表示内容を検討します。詳しくは、次の[ベストプラクティス分析レポートの確認](#analysis-report)の節を参照してください。

   >[!NOTE]
   >新しいレポートをアップロードすると、すべての評価がリセットされます。

### 印刷プレビューの使用 {#print-preview-cam}

Cloud Acceleration Manager で、印刷プレビューオプションを選択して、レポートの印刷可能なプレビューを表示したり、PDF形式でレポートを印刷して共有しやすくすることができます。

次の手順に従います。

1. クリック **印刷プレビュー** アイコンに表示されます。

   ![画像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. クリック **印刷プレビュー** 新しいタブが開き、レポートが印刷可能なプレビューで表示されます。 クリック **印刷** をクリックして、レポートをPDF形式で印刷します。

   >[!IMPORTANT]
   >* オプション **「名前を付けて保存」PDF** 上記の機能に対しては、をお勧めし、サポートしています。
   >* ブラウザの印刷ボタンを使用すると、1 ページだけが印刷されます。


   ![画像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 近似曲線の表示の使用 {#trendline-view-cam}

1 つのプロジェクトに複数のベストプラクティスアナライザー (BPA) レポートをアップロードする場合、 **トレンドラインを表示** オプションを使用して、履歴 BPA レポートの結果を表示および比較できます。

トレンドラインオプションからレポートを表示するには、次の手順に従います。

>[!NOTE]
>1 つのプロジェクトに複数の BPA レポートをアップロードすると、 **...** アイコン

1. プロジェクトに移動し、をクリックします。 **レビュー** から **ベストプラクティス分析** カード **準備** フェーズ。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. をクリックします。 **...** アイコンをクリックしてドロップダウンを表示します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >表示されるレポートは常に、最新のレポート日付を持つレポートです。

1. クリック **トレンドラインを表示**（下の図を参照）。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. クリック **トレンドラインを表示** 次の図に示すように、レポートのトレンドライン表示を開きます。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >トレンドラインレポートは、履歴 BPA レポートの結果をグラフで表示します。
   >
   >次の 2 つのグラフが表示され、
   >1. **結果トレンドのレポート**
   >1. **カスタムコンポーネントとテンプレートトレンド**

   >
   >次の図に示すように、ドロップダウンからグラフィカルビューを追加または変更できます。
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
>結果カテゴリと重要度レベルについては、[ベストプラクティスアナライザーレポートの説明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=ja)を参照してください。

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

トレンドラインビューからレポートを削除するには、次の手順に従います。

>[!IMPORTANT]
>レポートは、プロジェクトに複数のレポートがアップロードされている場合にのみ削除できます。

1. プロジェクトに移動し、をクリックします。 **レビュー** から **ベストプラクティス分析** カード **準備** フェーズ。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. をクリックします。 **...** アイコンをクリックしてドロップダウンを表示します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. クリック **トレンドラインを表示**（下の図を参照）。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 次から削除アイコンをクリックします。 **トレンドラインレポート** 画面

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. クリック **削除** 削除を確定します。

   ![画像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法とプロジェクトの作成方法を理解したら、次のステップの[実装フェーズ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=ja)に進みます。
