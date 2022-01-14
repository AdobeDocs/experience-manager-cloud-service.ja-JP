---
title: Adobe Analytics との統合
description: 'Adobe Analytics との統合 '
feature: Administering
role: Admin
source-git-commit: 4bf5ee1218f775efdc7829b790360033ad756c9a
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---


# Adobe AnalyticsとExperience Cloud自動化の統合 {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> この機能は、現在、内部ベータ版です。 Target のリリースは 2022 年第 1 四半期です。

Experience Cloud設定の自動化は、Experience Manager SitesとExperience Platform Launch、Adobe Analyticsを統合し、簡単な UI ウィザードインターフェイスで実装するための、シンプルで自動化された方法を提供します。

Adobe AnalyticsとAEM Sitesを統合するのはこれまで以上に簡単ではありません。 Experience Cloudのセットアップ自動化を使用すると、パフォーマンス分析をキャプチャし、顧客の関心とコンバージョンをいかに良く把握するために、サイトのセットアップ、統合、実装を数回のクリックで行うことができます。

このビデオでは、AEM Site とExperience Platform Launchおよび Analytics の統合方法を、Setup Automation を使用して説明します。

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## 要件

自動化の設定は、を使用して構築されたAEM Site で、すぐに使用できるように設計されています。 [AEMコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) と [Adobeクライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja) 有効。 新しいサイトを生成し、これらの機能を自動的に有効にするには、 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) または、 [サイトテンプレート](/help/journey-sites/quick-site/create-site.md).

## 設定方法

1. に移動します。 **サイト** Adobe Analyticsと統合するサイトのルートを選択します。
1. サイドレールメニューを展開し、をタップします。 **Analytics を設定**.

   これはサイドレールの新しいオプションで、パネルが開き、Experience Cloud設定の自動化のコントロールとステータスを提供します。
1. 次をタップします。 **Analytics の統合** 」ボタンをクリックします。
1. 表示されたダイアログで、 **レポートスイート ID**.

   この文字列は、新しい [レポートスイート ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) 選択したAEMサイトの analytics データのデータストアとしてAdobe Analyticsに保存されます。 提供された文字列には、一意性を確保するために環境および層識別子が追加されます。

1. ページとパネルを更新し、をタップします。 **統合ステータスの確認** 自動化のステータスを確認します。

   自動化の設定は非同期で実行されます。 この **統合ステータスの確認** 統合の現在のステータスが表示されます。

   * **処理中**  — ジョブが実行中であることを示します。
   * **統合の完了**  — ジョブが Analytics と Launch の統合、Launch の拡張機能と Launch ルールの設定、Adobe Analyticsでの新しいレポートスイートの作成を完了したことを示します。
   * **失敗**  — 自動ジョブが正常に完了できなかったことを示します。 「ログ」リンクをクリックして、このジョブのログファイルを確認します。

## AEM設定の検証

自動化が完了したら、サイトで Analytics イベントが発生していることを検証します。

1. 次を使用してサイトのページを開く **サイトエディター**.
1. 以下を使用： **公開済みとして表示** オプションを使用して、公開されたバージョンのページを読み込みます。
1. ブラウザーの開発者ツールを使用して、ネットワークトラフィックと、 **起動** および `AppMeasurement.js` ファイルを読み込み中です。
1. Inspectのコンソールを使用して、Adobeクライアントデータレイヤーによってページおよびコンポーネントレベルのイベントが発生し、収集されることを確認します。

## Analytics 設定の検証

次に、Adobe Analyticsに移動して、AEMサイト上のイベントからフローするデータを表示します。

1. AEMサイトと同じ IMS 組織のAdobe Analyticsに移動します。
1. AEM Sitesでの移動先の新しい概要レポートの作成 **レポート** > **エンゲージメント** > **Adobe Experience Manager** > **サイトパフォーマンスの概要**.
1. タップ **レポートを開く**.
1. を選択します。 **レポートスイート ID** 前の演習で使用したレポートスイート名に一致する名前。
1. 分析データフローを時間の経過と共に新しいテンプレートに表示します。

   >[!NOTE]
   >
   > 新しい統合では、レポートにデータが入力されるまでに数時間かかる場合があります。
