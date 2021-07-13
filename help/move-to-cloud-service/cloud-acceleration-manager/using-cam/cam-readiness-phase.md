---
title: Cloud Acceleration Managerの準備段階
description: このページでは、Cloud Acceleration Managerの準備段階の概要を説明します。
source-git-commit: 4041e3fd9a479a64ed38e2bf1a6251fda39e55c2
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 4%

---


# Cloud Acceleration Managerの準備段階 {#readiness-phase-cam}

Cloud Acceleration Managerでプロジェクトを作成したら、準備段階で使用可能なツールの実行を開始できます。

準備段階には、次の内容が含まれます。

* [ベストプラクティス分析](#best-practices-analysis)
* [計画と設定](#planning-setup)

次の手順に従って、準備段階に進みます。

1. プロジェクトカードをクリックして、プロジェクトのランディングページを開きます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. 次の図に示すように、**準備**&#x200B;セクションに移動します。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >詳しくは、 Cloud Acceleration Managerのプロジェクトの作成と管理を参照してください。

## ベストプラクティス分析カードの使用 {#best-practices-analysis}

以下の手順に従って、ベストプラクティス分析カードを使用します。

1. **ベストプラクティス分析**&#x200B;カードの「**レビュー**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. 次の手順に従って、ベストプラクティスアナライザー(BPA)をダウンロードし、AEMシステムのクローンで実行します。

   1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aemcloud.html)ポータルに移動し、ベストプラクティスアナライザーをzipファイルとしてダウンロードします。

      >[!NOTE]
      >BPAの実行方法については、[ベストプラクティスアナライザー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations)の使用を参照してください。

   1. レポートをCSV形式で書き出す

1. 「**新しいレポートをアップロード**」をクリックして、CAMでBPAレポートをアップロードします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

1. 新しいレポートをアップロードすると、ベストプラクティス分析レポートが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. CAMのベストプラクティス分析ダッシュボードを確認し、確認します。 詳しくは、以下の[ベストプラクティス分析レポートの確認](#analysis-report)の節を参照してください。

   >[!NOTE]
   >新しいレポートをアップロードすると、すべての評価がリセットされます。

### ベストプラクティス分析レポートの確認 {#analysis-report}

ベストプラクティス分析レポートページで使用可能な次のカードを確認します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 各カードには、次の機能があります。
>* 各カードをクリックして、関連するタブを開きます。
>* 共有または将来の取得のために、すべてのレポートタブ（フィルタリングを含む）をブックマークします。
>* 「詳細」アイコンを使用して、各レポートの結果の詳細を表示します


#### レポートのプロパティ {#report-properties}

**レポートのプロパティ**&#x200B;カードは、レポートの日付、期間、フィルター、アップロード日、Adobe Experience Manager(AEM)の詳細など、レポートのプロパティに関する情報を提供します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### レポートの概要 {#report-overview}

この&#x200B;**レポートの概要**&#x200B;カードは、次の図に示すように、レポートの結果を示します。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

このレポートをクリックすると、「**レポート**」タブが開きます。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

重要度、サブタイプまたはカウントに基づいてレポートをフィルタリングできます。

![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>結果カテゴリと重要度レベルについては、 [Best Practices Analyzer Report](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en)の解釈を参照してください。

#### ベストプラクティス評価 {#best-practices-assessment}

「ベストプラクティスの評価」オプションでは、現在のAEMインスタンスの評価を提供し、AEMのベストプラクティスを採用する次の手順に関するガイダンスを提供します。 このタブでは、次の情報を確認できます。

* AEMインスタンスの概要
* カスタムコンポーネントとテンプレート
* その他の結果
* 処理に時間のかかるクエリ
* メンテナンスタスク

#### 移行の複雑さの評価 {#migration-complexity-assessment}

「移行の複雑さの評価」オプションでは、既存のAEM実装をCloud ServiceとしてAEMに移行する際の複雑さを評価できます。

このタブでは、次の情報を確認できます。

* AEMインスタンスの概要
* 評価
* コンテンツ移行に関する考慮事項

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 計画および設定カードの使用 {#planning-setup}

この節では、「計画と設定」アクティビティカードを参照します。

1. AEM移行の計画と設定に役立つ関連コンテンツをすべて提供する&#x200B;**Planning And Setup**&#x200B;カードの「**View**」ボタンをクリックします。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. 移行ジャーニーのこのフェーズに関連する情報を含むコンテンツカルーセルが表示されます。

   ![画像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## 次の手順 {#whats-next}

Cloud Acceleration Managerへのログイン方法とプロジェクトの作成方法を学習したら、次の手順を確認し、[実装段階](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en)を使用します。
