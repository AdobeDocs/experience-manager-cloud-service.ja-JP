---
title: Cloud Acceleration Manager の準備段階
description: このページでは、Cloud Acceleration Manager の準備段階の概要を説明します。
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 12%

---

# Cloud Acceleration Manager の準備段階 {#readiness-phase-cam}

Cloud Acceleration Manager でプロジェクトを作成したら、準備段階で現在のAEM実装の評価を開始できます。

準備段階には、次の内容が含まれます。

* [ベストプラクティス分析](#best-practices-analysis)
* [計画と設定](#planning-setup)

次の手順に従って、準備段階に進みます。

1. プロジェクトカードをクリックして、プロジェクトのランディングページを開きます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. 次の図に示すように、**準備** セクションに移動します。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >詳しくは、 Cloud Acceleration Manager でのプロジェクトの作成と管理を参照してください。

## ベストプラクティス分析カードの使用 {#best-practices-analysis}

次の手順に従って、ベストプラクティス分析カードを使用します。

1. 「**ベストプラクティス分析**」カードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. 次の手順に従って、ベストプラクティスアナライザー (BPA) をダウンロードします。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、実稼動環境にできる限り近いオーサー環境で BPA を実行することをお勧めします。または、実稼動版のオーサー環境のクローンで実行することもできます。

   1. [ ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) ポータルに移動し、ベストプラクティスアナライザーを zip ファイルとしてダウンロードします。

      >[!NOTE]
      >[ ベストプラクティスアナライザー ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) の使用を参照して、BPA の実行方法を確認してください。

   1. レポートを CSV 形式で書き出す

1. 「**新しいレポートをアップロード**」をクリックして、CAM で BPA レポートをアップロードします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >ブラウザーの匿名モードの場合、レポートをアップロードできません。

1. 新しいレポートをアップロードすると、ベストプラクティス分析レポートが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. CAM のベストプラクティス分析ダッシュボードを確認して確認します。 詳しくは、以下の [ ベストプラクティス分析レポートの確認 ](#analysis-report) の節を参照してください。

   >[!NOTE]
   >新しいレポートをアップロードすると、すべての評価がリセットされます。

### ベストプラクティス分析レポートの確認 {#analysis-report}

ベストプラクティス分析レポートページで使用できる次のカードを確認します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 各カードには、次の機能があります。
>* 各カードをクリックして、関連するタブを開きます。
>* 共有または将来の取得のために、すべてのレポートタブをブックマーク（フィルタリングを含む）
>* 「詳細」アイコンを使用して、各レポートの結果の詳細を表示します


#### レポートのプロパティ {#report-properties}

**レポートのプロパティ** カードは、レポートの日付、期間、フィルター、アップロード日、Adobe Experience Manager(AEM) の詳細など、レポートのプロパティに関する情報を提供します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### レポートの概要 {#report-overview}

この **レポートの概要** カードは、次の図に示すように、AEM as a Cloud Serviceへの移行準備状況を評価する際に適用されるレポートの結果と重大度レベルを示します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

このレポートをクリックすると、「**レポート**」タブが開きます。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

重要度、サブタイプまたはカウントに基づいて、レポートをフィルタリングできます。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>結果カテゴリと重要度レベルについては、[Best Practices Analyzer レポートの解釈 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) を参照してください。

#### ベストプラクティス評価 {#best-practices-assessment}

「ベストプラクティスの評価」オプションでは、現在のAEMインスタンスの評価を提供し、AEMのベストプラクティスを採用するための次の手順に関するガイダンスを提供します。 このタブでは、次の情報を確認できます。

* AEM Instance の概要
* カスタムコンポーネントとテンプレート
* その他の所見
* 処理に時間のかかるクエリ
* メンテナンスタスク

#### 移行の複雑さの評価 {#migration-complexity-assessment}

「移行の複雑さの評価」オプションでは、既存のAEM実装をAEM as a Cloud Serviceに移行する複雑さの評価を提供します。

このタブでは、次の情報を確認できます。

* AEM Instance の概要
* 評価
* コンテンツ移行に関する考慮事項

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 計画および設定カードの使用 {#planning-setup}

この項では、「計画と設定」アクティビティ・カードを参照します。

1. **Planning And Setup** カードの **View** ボタンをクリックします。 このカードには、AEM移行の計画とセットアップに役立つすべての関連コンテンツが含まれています。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. コンテンツカルーセルに、移行ジャーニーのこのフェーズに関連するすべての情報が表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## 次の手順 {#whats-next}

Cloud Acceleration Manager へのログイン方法とプロジェクトの作成方法を学習したら、次の手順に進んで、[ 実装フェーズ ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en) を参照してください。
