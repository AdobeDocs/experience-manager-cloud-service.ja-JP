---
title: Adobe Analytics と Experience Cloud 設定自動化を統合する
description: Experience Cloud 設定自動化を使用すると、シンプルな UI ウィザードインターフェイスを介して、わかりやすく自動化された方法で、Experience Manager Sites を Experience Platform タグおよび Adobe Analytics と統合してツール化することができます。ご利用のサイトで自動設定を使用する方法を説明します。
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 4a3e65ef6a8aa08c8bc78db31f94272334994ac5
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 98%

---

# Adobe Analytics と Experience Cloud 設定自動化を統合する {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
>Experience Cloud設定の自動化機能は廃止されました。

Experience Cloud 設定自動化を使用すると、シンプルな UI ウィザードインターフェイスを介して、わかりやすく自動化された方法で、Experience Manager Sites を Experience Platform タグおよび Adobe Analytics と統合してツール化することができます。

Adobe Analytics と AEM Sites の統合は、かつてないほどシンプルになりました。Experience Cloud 設定自動化を使用すると、顧客のエンゲージメントとコンバージョンの状況を把握するパフォーマンス分析をキャプチャするためのサイトの設定、統合、ツール化を、数回のクリックですべて行うことができます。

このビデオでは、Experience Cloud 設定自動化を使用して AEM サイトを Experience Platform タグおよび Analytics と統合する方法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## 要件

[Adobe クライアントデータレイヤー](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=ja) を有効にして [AEM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) を使用して構築した AEM Site では、自動化設定はデフォルトで動作するように設計されています。[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) を使用するか、 [サイトテンプレート](/help/journey-sites/quick-site/create-site.md) を使用してサイトを作成することにより、これらの機能が自動的に有効になる新しいサイトを生成できます。

## 前提条件 {#prerequisites}

この機能を使用する前に、次の手順に従って、お使いの環境で前提条件のサービスが正しく設定されていることを確認することが重要です。

1. Adobe Admin Console（https://adminconsole.adobe.com/）にログインします。
1. 右上隅で適切な IMS 組織 ID が選択されていることを確認します。
1. 「製品ナビゲーション」オプションをクリックします。
1. 「Adobe Experience Manager as a Cloud Service」が IMS 組織用にプロビジョニングされていることを確認します。
1. 「Adobe Analytics」が IMS 組織用にプロビジョニングされていることを確認します。
1. Cloud Manager（https://experience.adobe.com/cloud-manager）に移動します。
1. 適切なプログラムを選択します。
1. 環境が最新バージョンの Cloud Service であることを確認します（そうでない場合は、メニューオプションの「更新」を選択します）。
1. Cloud Manager でフルスタックパイプラインを実行します。

これで、Experience Cloud 設定自動化の環境の準備ができました。

## 設定方法

1. **Sites** に移動して、Adobe Analytics と統合するサイトのルートを選択します。
1. サイドパネルメニューを展開して、「**Analytics を設定**」を選択します。

   これはサイドレールの新しいオプションであり、Experience Cloud 設定自動化のコントロールとステータスを提供するパネルが開きます。
1. 「**Analytics を統合**」ボタンを選択します。
1. 表示されたダイアログで、**レポートスイート ID** の名前を入力します。

   この文字列は、選択した AEM サイトの分析データのデータストアとして、Adobe Analytics に[レポートスイート ID](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=ja) を作成するために使用されます。提供された文字列には、一意性を確保するために環境および層の識別子が追加されます。

1. ページとパネルを更新し、「**統合ステータスを確認**」を選択して、自動化のステータスを確認します。

   自動化の設定は非同期で実行されます。**統合ステータスの確認** には、統合の現在のステータスが表示されます。

   * **処理中** - ジョブが実行中であることを示します。
   * **統合完了** - ジョブが Analytics とタグの統合、タグの拡張機能とタグルールの設定、Adobe Analytics での新しいレポートスイートの作成を完了したことを示します。
   * **失敗** - 自動ジョブを正常に完了できなかったことを示します。「ログ」リンクをクリックして、このジョブのログファイルを確認します。

## AEM 設定の検証

自動化が完了したら、サイトで Analytics イベントが発生していることを検証します。

1. **サイトエディター** を使用してサイトのページを開きます。
1. **公開済みとして表示** オプションを使用して、公開されたバージョンのページを読み込みます。
1. ブラウザーの開発者ツールを使用して、ネットワークトラフィックを検査し、**タグ**&#x200B;および `AppMeasurement.js` ファイルを読み込み中であることを確認します。
1. ブラウザーのコンソールを検査し、ページおよびコンポーネントレベルのイベントが発生し、Adobe クライアントデータレイヤーによって収集されることを確認します。

## Analytics 設定の検証

次に、Adobe Analytics に移動して、AEM サイト上のイベントから流入するデータを表示します。

1. AEM サイトと同じ IMS 組織の Adobe Analytics に移動します。
1. **レポート**／**エンゲージメント**／**Adobe Experience Manager**／**サイトのパフォーマンスの概要** に移動して、AEM Sites の新しい概要レポートを作成します。
1. 「**レポートを開く**」を選択します。
1. 前の演習で使用したレポートスイート名と一致する **レポートスイート ID** を選択します。
1. 新しいテンプレートに流入する分析データを経時的に表示します。

   >[!NOTE]
   >
   > 新しい統合では、レポートにデータが入力されるまでに数時間かかる場合があります。
