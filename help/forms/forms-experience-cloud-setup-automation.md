---
title: アダプティブフォームのAdobe Analyticsを有効にする (Experience Cloud設定の自動化を使用 )
description: Experience Cloudの自動設定は、Adobe Analyticsをアダプティブフォームに接続する際に役立ちます。 これは、アダプティブフォームでのユーザーインタラクションの追跡と分析に役立ち、訪問者のインタラクションとエンゲージメントに関するインサイトを提供します。
source-git-commit: c88f8f61cf54059b1d141d08b77983dd45edfaa6
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 2%

---


# アダプティブフォームのAdobe Analyticsを有効にする (Experience Cloud設定の自動化を使用 ) {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

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

![分析レポート](assets/analytics-report.png)


各指標について詳しくは、 [AEM Forms Analytics レポートの表示と理解](/help/forms/view-understand-aem-forms-analytics-reports.md)

## 前提条件 {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

Adobe Experience Manager FormsでのExperience Cloud設定の自動化には、 **Adobe Analyticsライセンス**, **データ収集 ( 以前のAdobeLaunch)** トラッキングスクリプトを管理し、 **Experience Platform Launch(API)** データの集計とインサイトの生成を合理化しました。

Experience Cloud設定の自動化、Adobe Analytics、Experience Platform LaunchAPI のアクティブなライセンスがある場合、開発者コンソール内で使用可能かどうかを確認する必要があります。

上記がFormsのas a Cloud Serviceの環境で使用できることを確認するには、 [開発者コンソール](https://developer.adobe.com/console/projects)を開き、プロジェクトに移動し、例えば、URL を持つ環境のプログラム id でプロジェクトを検索します。 `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`、プログラム ID は `p45913-e175111`. Experience Cloud設定の自動化、Adobe AnalyticsおよびExperience Platform LaunchAPI が表示されていることを確認します。 これらが一覧に表示されている場合は、アダプティブFormsに対してAdobe Analyticsを有効にすることができます。

![Forms Analytics の統合の前提条件](assets/analytics-aem.png)

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

![統合AEM Analytics](assets/analytics-aem-integrated.png)

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

   ![レポートを表示](assets/activ-aa.png)

1. クリック **Adobe Analytics** レポートを表示し、パフォーマンスデータを分析します。


古い方法でアダプティブフォームをAdobe Analyticsに接続するには、次にアクセスします： [AEM FormsとAdobe Analyticsの統合](/help/forms/integrate-aem-forms-with-adobe-analytics.md).
