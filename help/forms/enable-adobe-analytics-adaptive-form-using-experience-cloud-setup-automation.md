---
title: アダプティブフォーム用にAdobe Analyticsを有効にする
description: Experience Cloudの自動設定を使用すると、Adobe Analyticsをアダプティブフォームに接続して、訪問者のインタラクションとエンゲージメントに関するインサイトを追跡できます。
keywords: Experience Cloud設定の自動化、FormsでのAdobe Analyticsの有効化、アダプティブFormsでのAdobe Analyticsの有効化、Forms分析の統合、FormsとAdobe Analyticsを使用したアダプティブフォームのAdobe Analyticsの有効化
source-git-commit: 4daba42c9d8a7eff5d3ef6f9581c52c787666ed1
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 7%

---


# アダプティブフォームのAdobe Analyticsを有効にする (Experience Cloud設定の自動化を使用 ) {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | この記事 |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |

Experience Cloudの自動設定を使用すると、Adobe AnalyticsをアダプティブFormsに連携でき、フォームとのユーザーインタラクションを追跡し、分析し、訪問者のインタラクションとエンゲージメントに関するインサイトを提供できます。 Experience Cloudのセットアップ自動化は、完了時間やドロップオフポイントなどの指標の評価を含む、フォームのパフォーマンスの監視にも役立ちます。 この分析により、フォームを最適化してユーザーエクスペリエンスを向上させると同時に、ログインステータスに基づいてユーザーの行動を区別し、一般的な傾向やパターンを特定することができます。

## Adobe AnalyticsとアダプティブFormsの統合のメリット {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **エンドユーザーの行動に対するインサイト**:Adobe Analyticsは、エンドユーザーの行動に関するインサイトを取得し、ユーザーのアクション、ドロップオフ、完了率を明らかにし、個人がフォームにどのように関わっているかをより深く理解できるようにします。
* **技術系以外のビジネスユーザーがインサイトを得ることを可能にする**:Adobe Analyticsは、使いやすいインターフェイスを通じて、技術を持たないユーザーでもフォームの使用状況データにアクセスし、解釈できるようにし、登録エクスペリエンスを強化するためのデータ主導型の意思決定を促進します。
* **使用状況に基づくデータキャプチャエクスペリエンスの最適化**：組織はデータ取得に関する問題点を容易に特定でき、ターゲットを絞り込んで、フォームの操作性を高め、送信の成功を促進する改善につながります。

## アダプティブForms使用指標の範囲 {#scope-of-adaptive-forms-usage-metrics}

Adobe Analyticsは、アダプティブFormsのパフォーマンス指標の包括的な配列を提供し、フォームの使用状況に関する有益なインサイトを提供します。 以下の指標があります。

* **フォームレンディション、フォーム送信、検証エラーおよび個別訪問者**&#x200B;を使用して、フォームの使用状況と効果を評価できます。

* **訪問者インサイト** 訪問回数と送信頻度、および個別訪問者数を含み、フォームのオーディエンスの包括的なビューを提供します。

* **デバイスタイプ** ユーザーがフォームにアクセスする際に使用するデバイスについて通知するデータ。

* **地理的分類** フォームユーザーの地域分布を表示します。

* **トラフィックソース** および **人気の高いフォーム** 上位の参照ドメインと最も訪問回数の多いフォームで構成される指標は、トラフィックの発生元と最も人気の高いフォームを把握するのに役立ちます。

* **トップフォームでのユーザーアクティビティ** では、フィールド訪問、フォームレンディション、検証エラー、破棄されたフォーム、フォーム送信に関するインサイトを提供し、ユーザーの行動を分析できます。

* **フォームでの滞在時間のタイムライン** これにより、フォームに対するユーザーのエンゲージメントをタイムラインベースで表示することができます。

* **訪問者の支援が必要な領域** ヘルプビュー、検証エラーインスタンス、フィールド訪問の頻度などの指標。フォーム入力に関するサポートが必要な場所を強調表示します。

![分析レポート](assets/analytics-report.png){width="100%"}


各指標について詳しくは、 [AEM Forms Analytics レポートの表示と理解](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 前提条件 {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Experience Cloudの自動設定には、 **Adobe Analyticsライセンス**, **データ収集 ( 以前のAdobeLaunch)** トラッキングスクリプトを管理するには、および **Experience Manager Formsライセンス** データの集計とインサイトの生成を合理化しました。

のアクティブなライセンスをお持ちの場合 **Adobe Analytics** および **Experience Manager Forms**&#x200B;と統合されている **データ収集 ( 以前のAdobeLaunch)**&#x200B;を使用する場合は、開発者コンソール内で使用可能かを確認する必要があります。

上記がFormsのas a Cloud Serviceの環境で使用できることを確認するには、 [開発者コンソール](https://developer.adobe.com/console/projects)をクリックし、プロジェクトに移動し、プログラム id — 環境 id（例えば、URL を持つ環境）でプロジェクトを検索します。 `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`、プログラム id — 環境 id はです。 `p45913-e175111`. Experience Cloud設定の自動化、Adobe AnalyticsおよびExperience Platform LaunchAPI が表示されていることを確認します。 これらが一覧に表示されている場合は、アダプティブFormsに対してAdobe Analyticsを有効にすることができます。

![Forms Analytics の統合の前提条件](assets/analytics-aem.png){width="100%"}

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## Adobe Analytics の設定 {#configure-adobe-analytics}

アダプティブFormsでAdobe Analyticsを有効にして設定するには、以下の手順を実行します。

* [基盤コンポーネントに基づくアダプティブForms向けAdobe Analyticsの有効化](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [コアコンポーネントに基づいて、Adobe Analytics for Adaptive Formsを有効にする](#integrate-adobe-analytics-with-aem-forms-for-core-components)

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

### Adobe Analytics for Foundation コンポーネントでのアダプティブFormsの有効化 {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. クラウドサービスの設定コンテナを作成します。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定コンテナを選択または作成し、次のフォルダーを有効にします。 **[!UICONTROL クラウド設定]**.
   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。
1. AEMインスタンスで、に移動します。 **[Forms]** >> **[Formsとドキュメント]**.
1. を選択します。 **[!UICONTROL フォーム]** >> **[!UICONTROL プロパティ]**、 **[!UICONTROL 設定コンテナ]**」で、 **[!UICONTROL 設定ブラウザー]** 手順 1.
1. 左側のパネルでタスクパネルを選択し、 **Analytics を設定** および **Adobe Analyticsをアクティベート**.
1. レポートスイートの名前を入力し、 **[!UICONTROL 次へ]** および **[!UICONTROL 保存]**.
1. プロジェクトを保存すると、Adobe Analyticsとアダプティブフォームの統合が完了するまで、設定はしばらくの間実行されます。また、 **統合ステータス**.

   >[!NOTE]
   >
   >設定に 15 分以上かかる場合は、フォームの Analytics を有効にするように再試行してください。

1. AEMインスタンスで、に移動します。 **[!UICONTROL Forms]** >> **[Formsとドキュメント]** を選択し、 **[!UICONTROL フォーム]**&#x200B;を使用すると、次の画像に示すように、Adobe Analyticsがフォームに統合されています。
1. これで、 [アダプティブフォームAdobe Analyticsレポート](#view-adobe-analytics-report).

![統合AEM Analytics](assets/analytics-aem-integrated.png){width="100%"}


### コアコンポーネント用のアダプティブFormsでのAdobe Analyticsの有効化 {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. AEMインスタンスで、に移動します。 **[!UICONTROL Forms]** >> **[!UICONTROL Formsとドキュメント]** を選択し、 **[!UICONTROL フォーム]**.
1. 左側のタスクパネルを選択し、 **Analytics を設定** および **Adobe Analyticsをアクティベート**.
1. レポートスイートの名前を入力し、 **[!UICONTROL 次へ]** および **[!UICONTROL 保存]**.
1. プロジェクトを保存すると、Adobe Analyticsとアダプティブフォームの統合が完了するまで、設定はしばらくの間実行されます。また、 **統合ステータス**.

   >[!NOTE]
   >
   >設定に 15 分以上かかる場合は、フォームの Analytics を有効にするように再試行してください。

1. AEMインスタンスで、に移動します。 **[!UICONTROL Forms]** >> **[!UICONTROL Formsとドキュメント]** を選択し、 **[!UICONTROL フォーム]**&#x200B;に設定されている場合、Adobe Analyticsがフォームに統合されていることがわかります。
1. これで、 [アダプティブフォームAdobe Analyticsレポート](#view-adobe-analytics-report).

## アダプティブForms Adobe Analyticsレポートの表示 {#view-adobe-analytics-report}

1. AEMインスタンスで、に移動します。 **[!UICONTROL Forms]** >> **[!UICONTROL Formsとドキュメント]**.
1. フォームを選択すると、左側に示すように、Adobe AnalyticsがAdobe Analytics用にアクティブ化されたFormsに統合されています。

   ![レポートを表示](assets/activ-aa.png){width="100%"}

1. クリック **Adobe Analytics** レポートを表示し、パフォーマンスデータを分析します。

手動による方法でアダプティブフォームをAdobe Analyticsに接続するには、次にアクセスします： [AEM FormsとAdobe Analyticsの統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Sites で Analytics からアダプティブFormsへの有効化 {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

AEM Sitesでアダプティブフォームの分析を設定すると、Sites ページのフォームに対するユーザーのインタラクションとフォームの送信を追跡するのに役立ちます。 分析を Sites Formsにシームレスに統合することで、ユーザーの行動、コンバージョン率、フォームの改善点に関する貴重なインサイトを得ることができます。

### 前提条件 {#Prerequisites-to-connect-forms-analytics-to-sites}

Adaptive Forms for AEM Sitesで Analytics を接続して有効にするには、AEM SitesにアクティブなAdobe Analyticsがあることを確認する必要があります。

### Sites の Adaptive Formsに接続して Analytics を有効にする {#Connect-analytics-to-adaptive-forms}

AEM Sitesページでアダプティブフォームに接続して Analytics を有効にするには、 `customfooterlibs` AEMアーキタイプ/Git リポジトリーとデプロイメントパイプラインを使用して、AEM Sitesページに対するクライアントライブラリ。

1. [AEM Forms アーキタイプまたは複製された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)プロジェクトをテキストエディターで開きます。例えば Visual Studio Code などです。

1. アダプティブフォームが存在する Sites のページに移動します ( 例：このデモプロジェクトでは、 `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. `sling:resourceSuperType` の値をコピーします。例えば、値は `core/wcm/components/page/v3/page` です。

   ![Sling リソース](/help/forms/assets/slingresource.png){width="100%"}

1. `core/wcm/components/page/v3/page` と同じ場所 `ui.apps/src/main/content/jcr_root/apps` に類似した構造を作成します。

   ![オーバーレイ構造](/help/forms/assets/overlaystructure.png){width="100%"}

1. を追加します。 `customfooterlibs.html` ファイル。

       &quot;&#39;
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       &quot;&#39;
   
   The `customfooterlibs.html` は JavaScript で使用されます。

1. [パイプラインを実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=ja)して変更をデプロイします。

### Sites でフォーム分析ルールをFormsに有効化 {#bind-forms-analytics-rules-to-forms-in-sites}

1. 次にアクセス： **Adobe Experience Platform Data Collection**.
1. クリック **タグ** は左側にあります。
1. 以下の画像に示すように、URL を持つ環境のプログラム ID でプロジェクトを検索します。 `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`、プログラム ID は `45921`.

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-data-collection.png){width="100%"}

1. の設定を追加 **フォームルール** および **データ要素** 以下に示すように。

#### フォームルールを追加 {#form-rules}

1. フォームを選択して、 **新しいプロパティ** は右上にあるか、フォームをクリックします。
1. プロパティページで、「 **ルール** フォームのイベントを選択します。以下の例では、次のようになります。 **フォームイベント**.

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. フォームのすべてのイベントを選択し、 **コピー** 右上のパネルにある
1. コピーした後、 **ルールをコピー** ポップアップが表示され、サイトページを project-id で検索してフォームルールを貼り付けることができます。

   ![Copy-form-rules](/help/forms/assets/copy-form-rules.png){width="100%"}

1. クリック **コピー** をクリックして、フォームルールをサイトページに貼り付けます。

#### データ要素を追加 {#data-elements}

1. フォームを選択して、 **新しいプロパティ** は右上にあるか、フォームをクリックします。
1. プロパティページで、「 **データ要素** フォームのイベントを選択します。
1. フォームのすべてのイベントを選択し、 **コピー** は右上のレールに配置されています。
1. コピーした後、 **ルールをコピー** ポップアップが表示され、サイトページを project-id で検索してフォームルールを貼り付けることができます。
1. クリック **コピー** をクリックして、フォームルールをサイトページに貼り付けます。

   ![Form-data-elements](/help/forms/assets/form-data-elements.png){width="100%"}

上記の手順でフォームとサイトのルールをバインドしたら、次の手順を実行して、 Analytics を Sites ページのアダプティブフォームに対して有効にします。

1. クリック **公開フロー** 左側に
1. クリック **ライブラリを追加** をクリックし、任意の名前を入力します。
1. Adobe Analytics の **環境** 右側のドロップダウンで、「 」を選択します。 **開発**.
1. 「**Add All Changed Resources**」をクリックします。
1. クリック **開発用に保存およびビルド**.

![publish-to-development](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## 関連トピック {#see-also}

* [アダプティブForms分析レポートの表示と理解](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [アダプティブフォームをAEM Sitesページまたはエクスペリエンスフラグメントに追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [AEM FormsとAdobe Analyticsの統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
