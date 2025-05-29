---
title: アダプティブフォームの高速分析のために Adobe Analytics を有効にする方法
description: Experience Cloud 設定自動化は、Adobe Analytics をアダプティブフォームに接続して、訪問者のインタラクションとエンゲージメントの高速分析を実行し、インサイトを得るのに役立ちます。
keywords: Experience Cloud 設定自動化を使用してアダプティブフォームの Adobe Analytics を有効にする, フォームで Adobe Analytics を有効にする, アダプティブフォームでの Adobe Analytics, フォームの Analytics の統合, フォームと Adobe Analytics
feature: Adaptive Forms
role: Admin, User
exl-id: 0e1aa040-08b4-4c1a-b247-ad6fff410187
source-git-commit: 56a3d50d7cc8db532097b97f0898f87fc6ba0b3d
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 99%

---

# Experience Cloud 設定自動化を使用してアダプティブフォームの Adobe Analytics を有効にする {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

>[!CAUTION]
>
>Experience Cloud設定の自動化機能は廃止されました。

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | この記事 |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html?lang=ja) |

Experience Cloud 設定自動化は、Adobe Analytics をアダプティブフォームに接続するのに役立ちます。これにより、フォームでのユーザーインタラクションの高速分析を実行し、訪問者のインタラクションとエンゲージメントに関するインサイトを得られます。Experience Cloud 設定自動化は、完了時間やドロップオフポイントなどの指標の評価を含むフォームのパフォーマンスの監視にも役立ちます。この分析は、ログインステータスに基づいてユーザーの行動（匿名ユーザーなど）を区別し、一般的なトレンドとパターンを特定しながら、ユーザーエクスペリエンスを向上させるためにフォームを最適化するのに役立ちます。

## Adobe Analytics とアダプティブフォームを統合するメリット {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **エンドユーザーの行動に関するインサイト**：Adobe Analytics は、エンドユーザーの行動に関するインサイトを取得するのに役立ち、ユーザーのアクション、ドロップオフ、完了率を明らかにして、個人がフォームをどのように操作するかを詳しく理解できるようにします。
* **技術者以外のビジネスユーザーがインサイトを取得できるようにする**：Adobe Analytics は、使いやすいインターフェイスを通じて、技術者以外のユーザーでもフォームの使用状況データにアクセスして解釈できるようにし、登録エクスペリエンスを向上させるためのデータ主導型の意思決定を促進します。
* **使用状況に基づいてデータキャプチャエクスペリエンスを最適化**：組織はデータキャプチャの問題点を容易に特定し、フォームの操作性を向上させて送信の成功率を高める、ターゲットを絞った改善につなげることができます。

## アダプティブフォームの使用状況指標の範囲 {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics は、フォームの使用状況に関する貴重なインサイトを提供するように設計されたアダプティブフォームのパフォーマンス指標の包括的な配列と、高速分析を提供します。これらの指標を以下に示します。

* **フォームのレンディション数、フォームの送信数、検証エラー数およびユニーク訪問者数**：フォームの使用状況と効果を評価できます。

* **訪問者インサイト**：訪問頻度と送信頻度、ユニーク訪問者数が含まれます。フォームのオーディエンスの包括的なビューを提供します。

* **デバイスタイプ**：ユーザーがフォームにアクセスする際に使用するデバイスについて通知するデータです。

* **地理的分類**：フォームユーザーの地域分布を表示します。

* **トラフィックソース**&#x200B;と&#x200B;**人気の高いフォーム**：上位の参照ドメインと最も訪問回数の多いフォームで構成される指標は、トラフィックの発生元と一番人気のフォームを理解するのに役立ちます。

* **上位フォームでのユーザーアクティビティ**：フィールド訪問、フォームのレンディション、検証エラー、放棄されたフォームおよびフォームの送信に関するインサイトを提供し、ユーザーの行動を分析できるようにします。

* **フォームでの滞在時間のタイムライン**：フォームに対するユーザーエンゲージメントをタイムラインベースで表示できます。

* **訪問者の支援が必要な領域**：ヘルプビュー、検証エラーのインスタンス、フィールド訪問の頻度などの指標により、ユーザーがフォームに入力する際に支援が必要な場所がハイライト表示されます。

![分析レポート](assets/analytics-report.png){width="100%"}


各指標について詳しくは、[AEM Forms 分析レポートの表示と理解](/help/forms/view-understand-aem-forms-analytics-reports.md)を参照してください。

## 前提条件 {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloud 設定自動化には、**Adobe Analytics ライセンス**、トラッキングスクリプトを管理するための&#x200B;**データ収集（旧 Adobe Launch）**&#x200B;および効率的なデータ集計とインサイト生成のための **Experience Manager Forms ライセンス**&#x200B;が必要です。

**Adobe Analytics** と **Experience Manager Forms** のアクティブなライセンスを使用し、**データ収集（旧 Adobe Launch）**&#x200B;と統合している場合は、Developer Console 内で使用可能であることを確認する必要があります。

Forms as a Cloud Service 環境で上記の機能が使用可能であることを確認するには、[Developer Console](https://developer.adobe.com/console/projects) にアクセスし、プロジェクトに移動して、プログラム ID - 環境 ID でプロジェクトを検索します。例えば、URL が `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html` の環境の場合、プログラム ID - 環境 ID は `p45913-e175111` です。Experience Cloud 設定自動化、Adobe Analytics および Experience Platform Launch API がリストされていることを確認します。リストされている場合は、アダプティブフォームの高速分析を実行するために Adobe Analytics を有効にできます。

![Forms Analytics 統合の前提条件](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html?lang=ja)
-->

## Adobe Analytics の設定 {#configure-adobe-analytics}

アダプティブフォームの高速分析のために Adobe Analytics を有効にして設定するには、以下の手順を実行します。

* [基盤コンポーネントに基づくアダプティブフォームに対して Adobe Analytics を有効にする](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [コアコンポーネントに基づくアダプティブフォームに対して Adobe Analytics を有効にする](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### 基盤コンポーネントのアダプティブフォームを使用して Adobe Analytics を有効にする {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. クラウドサービス用の設定コンテナを作成します。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定コンテナを選択または作成し、**[!UICONTROL クラウド設定]**&#x200B;のフォルダーを有効にします。
   1. 「**[!UICONTROL 保存して閉じる]**」を選択して設定内容を保存し、ダイアログを閉じます。
1. AEM インスタンスで、**[Forms]**／**[フォームとドキュメント]**&#x200B;に移動します。
1. **[!UICONTROL フォーム]**／**[!UICONTROL プロパティ]**&#x200B;を選択し、**[!UICONTROL 設定コンテナ]**&#x200B;で、手順 1 の&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;で作成または選択した設定コンテナを選択します。
1. 左側のパネルでタスクパネルを選択し、「**Analytics を設定**」、「**Adobe Analytics をアクティベート**」の順にクリックします。
1. レポートスイートに使用する名前を入力し、「**[!UICONTROL 次へ]**」、「**[!UICONTROL 保存]**」の順にクリックします。
1. プロジェクトを保存すると、Adobe Analytics とアダプティブフォームが統合されるまで、設定がしばらく実行されます。また、**統合ステータス**&#x200B;を確認することもできます。

   >[!NOTE]
   >
   >設定に 15 分以上かかる場合は、フォームの分析を有効にするように再試行してください。

1. AEM インスタンスで、**[!UICONTROL Forms]**／**[フォームとドキュメント]**&#x200B;に移動し、**[!UICONTROL フォーム]**&#x200B;を選択すると、以下の画像に示すように、Adobe Analytics がフォームに統合されていることがわかります。
1. これで、[アダプティブフォームの Adobe Analytics レポート](#view-adobe-analytics-report)を表示できるようになります。

![統合された AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### コアコンポーネント用のアダプティブフォームを使用して Adobe Analytics を有効にする {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. AEM インスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動し、**[!UICONTROL フォーム]**&#x200B;を選択します。
1. 左側のタスクパネルを選択し、「**Analytics を設定**」をクリックして、「**Adobe Analytics をアクティベート**」をクリックします。
1. レポートスイートに使用する名前を入力し、「**[!UICONTROL 次へ]**」、「**[!UICONTROL 保存]**」の順にクリックします。
1. プロジェクトを保存すると、Adobe Analytics とアダプティブフォームが統合されるまで、設定がしばらく実行されます。また、**統合ステータス**&#x200B;を確認することもできます。

   >[!NOTE]
   >
   >設定に 15 分以上かかる場合は、フォームの分析を有効にするように再試行してください。

1. AEM インスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動し、**[!UICONTROL フォーム]**&#x200B;を選択すると、Adobe Analytics がフォームに統合されていることがわかります。
1. これで、[アダプティブフォームの Adobe Analytics レポート](#view-adobe-analytics-report)を表示できるようになります。

## アダプティブフォームの Adobe Analytics レポートの表示 {#view-adobe-analytics-report}

1. AEM インスタンスで、**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. フォームを選択すると、左側に示すように、Adobe Analytics が Adobe Analytics 用にアクティベートされたフォームに統合されていることがわかります。

   ![レポートの表示](assets/activ-aa.png){width="100%"}

1. 「**Adobe Analytics**」をクリックしてレポートを表示し、パフォーマンスデータを分析します。

手動による方法を使用してアダプティブフォームを Adobe Analytics に接続するには、[AEM Forms と Adobe Analytics の統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)を参照してください。

## Sites でアダプティブフォームに対して Analytics を有効にする {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

AEM Sites のアダプティブフォームの高速分析を設定すると、Sites ページのフォームでのユーザーインタラクションとフォーム送信を追跡できるようになります。分析をSites フォームにシームレスに統合することで、ユーザーの行動、コンバージョン率、フォームの改善すべき領域に関する貴重なインサイトを取得できます。

### 前提条件 {#Prerequisites-to-connect-forms-analytics-to-sites}

AEM Sites のアダプティブフォームに接続して分析を有効にするには、AEM Sites にアクティブな Adobe Analytics があることを確認する必要があります。

### Sites でアダプティブフォームを接続して Analytics を有効にする {#Connect-analytics-to-adaptive-forms}

AEM Sites ページでアダプティブフォームを接続して、高速分析のために Analytics を有効にするには、AEM アーキタイプ／Git リポジトリとデプロイメントパイプラインを使用して、AEM Sites ページに `customfooterlibs` クライアントライブラリを含めます。

1. [AEM Forms アーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)プロジェクトをテキストエディターで開きます。例えば Visual Studio Code などです。

1. アダプティブフォームが存在する Sites のページに移動します。例えば、このデモプロジェクトでは `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml` に移動します。

1. `sling:resourceSuperType` の値をコピーします。例えば、値は `core/wcm/components/page/v3/page` です。

   ![Sling リソース](/help/forms/assets/slingresource.png){width="100%"}

1. `core/wcm/components/page/v3/page` と同じ場所 `ui.apps/src/main/content/jcr_root/apps` に類似した構造を作成します。

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png){width="100%"}

1. `customfooterlibs.html` ファイルを追加します。

   ```
   // customheaderlibs.html
   <sly data-sly-use.page="com.adobe.cq.wcm.core.components.models.Page">
   <sly data-sly-test="${page.data && page.dataLayerClientlibIncluded}" data-sly-call="${clientlib.js @ categories='core.forms.components.commons.v1.datalayer', async=true}"></sly>
   </sly>
   ```

   `customfooterlibs.html` は JavaScript で使用します。

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して変更をデプロイします。

### Sites でフォームに対する Form Analytics ルールを有効にする {#bind-forms-analytics-rules-to-forms-in-sites}

1. **Adobe Experience Platform データ収集**&#x200B;にアクセスします。
1. 左側にある「**タグ**」をクリックします。
1. 以下の画像に示すように、プログラム ID を使用してプロジェクトを検索します。例えば、URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html` の環境の場合、プログラム ID は `45921` です。

   ![データ収集内のフォームの検索](/help/forms/assets/aep-data-collection.png){width="100%"}

1. 以下に示すように、**フォームルール**&#x200B;と&#x200B;**データ要素**&#x200B;の設定を追加します。

#### フォームルールの追加 {#form-rules}

1. フォームを選択し、右上にある&#x200B;**新しいプロパティ**&#x200B;を追加するか、フォームをクリックします。
1. プロパティページで、「**ルール**」をクリックし、フォームのイベントを選択します。以下の画像の例では、**フォームイベント**&#x200B;です。

   ![データ収集内のフォームの検索](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. フォームのすべてのイベントを選択し、右上のパネルにある&#x200B;**コピー**&#x200B;を実行します。
1. コピーしたら、プロジェクト ID で Sites ページを検索し、フォームルールをペーストする&#x200B;**ルールをコピー**&#x200B;ポップアップが表示されます。

   ![フォームルールのコピー](/help/forms/assets/copy-form-rules.png){width="100%"}

1. 「**コピー**」をクリックして、フォームルールを Sites ページにペーストします。

#### データ要素の追加 {#data-elements}

1. フォームを選択し、右上にある&#x200B;**新しいプロパティ**&#x200B;を追加するか、フォームをクリックします。
1. プロパティページで、「**データ要素**」をクリックし、フォームのイベントを選択します。
1. フォームのすべてのイベントを選択し、右上のパネルにある&#x200B;**コピー**&#x200B;を実行します。
1. コピーしたら、プロジェクト ID で Sites ページを検索し、フォームルールをペーストする&#x200B;**ルールをコピー**&#x200B;ポップアップが表示されます。
1. 「**コピー**」をクリックして、フォームルールを Sites ページにペーストします。

   ![フォームのデータ要素](/help/forms/assets/form-data-elements.png){width="100%"}

上記の手順でフォームと Sites のルールをバインドしたら、次の手順を実行して、Sites ページのアダプティブフォームで Analytics を有効にします。

1. 左側にある「**公開フロー**」をクリックします。
1. 「**ライブラリを追加**」をクリックし、使用する名前を入力します。
1. 右側にある&#x200B;**環境**&#x200B;ドロップダウンで、「**開発**」を選択します。
1. 「**Add All Changed Resources**」をクリックします。
1. 「**保存して開発用にビルド**」をクリックします。

![開発に公開](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## 関連トピック {#see-also}

* [アダプティブフォームの分析レポートの確認方法と詳細](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [AEM Sites ページまたはエクスペリエンスフラグメントにアダプティブフォームの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [AEM Forms と Adobe Analytics の統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
