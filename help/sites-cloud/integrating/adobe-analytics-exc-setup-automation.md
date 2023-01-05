---
title: Adobe Analytics と Experience Cloud 設定自動化の統合
description: Experience Cloud設定の自動化は、Experience Manager SitesとExperience Platformタグ、Adobe Analyticsを統合し、シンプルな UI ウィザードインターフェイスで実装する、シンプルで自動化された方法を提供します。 ご利用のサイトで自動設定を使用する方法を説明します。
feature: Administering
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: f91885a7d15c0ff927c6e10f65852f787cf26eb3
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 66%

---

# Adobe Analytics と Experience Cloud 設定自動化の統合 {#integrate-adobe-analytics-automation-setup}

Experience Cloud設定の自動化は、Experience Manager SitesとExperience Platformタグ、Adobe Analyticsを統合し、シンプルな UI ウィザードインターフェイスで実装する、シンプルで自動化された方法を提供します。

Adobe Analytics と AEM Sites の統合は、かつてないほどシンプルになりました。Experience Cloud 設定自動化を使用すると、顧客のエンゲージメントとコンバージョンの状況を把握するパフォーマンス分析をキャプチャするためのサイトの設定、統合、ツール化を、数回のクリックですべて行うことができます。

このビデオでは、AEMサイトとExperience Platformタグおよび Analytics を統合する方法について、自動Experience Cloud設定を使用して説明します。

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## 要件

[Adobe クライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja) を有効にして [AEM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) を使用して構築した AEM Site では、自動化設定はデフォルトで動作するように設計されています。[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) を使用するか、 [サイトテンプレート](/help/journey-sites/quick-site/create-site.md) を使用してサイトを作成することにより、これらの機能が自動的に有効になる新しいサイトを生成できます。

## 前提条件 {#prerequisites}

この機能を使用する前に、次の手順に従って、お使いの環境で前提条件のサービスが正しく設定されていることを確認することが重要です。

1. Adobe Admin Console(https://adminconsole.adobe.com/) にログインします。
1. 右上隅で適切な IMS Org ID が選択されていることを確認します。
1. 「製品」ナビゲーションオプションをクリックします。
1. 「Adobe Experience Manager as a Cloud Service」が IMS Org 用にプロビジョニングされていることを確認します。
1. 「Adobe Analytics」が IMS Org 用にプロビジョニングされていることを確認します。
1. Cloud Manager(https://experience.adobe.com/cloud-manager) に移動します。
1. 適切なプログラムを選択します。
1. 環境が最新バージョンのCloud Serviceであることを確認します（存在しない場合は、メニューオプションの「更新」を選択します）。
1. Cloud Manager でフルスタックパイプラインを実行します。

これで、環境のセットアップ自動化のExperience Cloud準備が整いました。

## 設定方法

1. **Sites** に移動して、Adobe Analytics と統合するサイトのルートを選択します。
1. サイドパネルメニューを展開して、 **Analytics を設定** をタップします。

   これはサイドレールの新しいオプションであり、Experience Cloud 設定自動化のコントロールとステータスを提供するパネルが開きます。
1. 「**Analytics の統合** 」ボタンをタップします。
1. 表示されたダイアログで、**レポートスイート ID** の名前を入力します。

   この文字列は、選択した AEM サイトの分析データのデータストアとして、Adobe Analytics に新しい [レポートスイート ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=ja) を作成するために使用されます。提供された文字列には、一意性を確保するために環境および層の識別子が追加されます。

1. ページとパネルを更新し、 **統合ステータスの確認** をタップして、自動化のステータスを確認します。

   自動化の設定は非同期で実行されます。**統合ステータスの確認** には、統合の現在のステータスが表示されます。

   * **処理中** - ジョブが実行中であることを示します。
   * **統合の完了**  — ジョブが Analytics とタグの統合、タグの拡張機能とタグルールの設定、Adobe Analyticsでの新しいレポートスイートの作成を完了したことを示します。
   * **失敗** - 自動ジョブを正常に完了できなかったことを示します。「ログ」リンクをクリックして、このジョブのログファイルを確認します。

## AEM 設定の検証

自動化が完了したら、サイトで Analytics イベントが発生していることを検証します。

1. **サイトエディター** を使用してサイトのページを開きます。
1. **公開済みとして表示** オプションを使用して、公開されたバージョンのページを読み込みます。
1. ブラウザーの開発者ツールを使用して、ネットワークトラフィックと、 **タグ** および `AppMeasurement.js` ファイルを読み込み中です。
1. ブラウザーのコンソールを検査し、ページおよびコンポーネントレベルのイベントが発生し、Adobe クライアントデータレイヤーによって収集されることを確認します。

## Analytics 設定の検証

次に、Adobe Analytics に移動して、AEM サイト上のイベントから流入するデータを表示します。

1. AEM サイトと同じ IMS 組織の Adobe Analytics に移動します。
1. **レポート**／**エンゲージメント**／**Adobe Experience Manager**／**サイトのパフォーマンスの概要** に移動して、AEM Sites の新しい概要レポートを作成します。
1. **レポートを開く** をタップします。
1. 前の演習で使用したレポートスイート名と一致する **レポートスイート ID** を選択します。
1. 新しいテンプレートに流入する分析データを経時的に表示します。

   >[!NOTE]
   >
   > 新しい統合では、レポートにデータが入力されるまでに数時間かかる場合があります。
