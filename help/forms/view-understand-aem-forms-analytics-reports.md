---
title: アダプティブForms分析レポートの表示と理解
description: アダプティブFormsはAdobe Analyticsとシームレスに統合され、公開済みのフォームやドキュメントのパフォーマンス指標を取得して追跡します。
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 39ea959cb0a0568fd94ca455be935228479c0415
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---


# アダプティブForms分析レポートの表示と理解 {#viewing-and-understanding-aem-forms-analytics-reports}

<span class="preview"> これはプレリリース機能で、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

急速に進化するデジタル分析の状況では、十分な情報に基づく意思決定を行い、デジタルエクスペリエンスを最適化するために、グローバルなトレンドに常に従うことが不可欠です。 これに対応するため、アダプティブFormsはAdobe Analyticsとシームレスに統合して、公開済みのフォームやドキュメントのパフォーマンス指標を取得し、追跡します。 これらの指標の分析の目的は、指標と分析を使用して、フォームの使いやすさと効果を高め、データ主導型の意思決定を行うことです。

主要業績評価指標を取り込み、追跡することで、企業は改善点を特定し、ユーザーエクスペリエンスを最適化し、最終的により良い結果をもたらして、優れた顧客体験を生み出すことができます。

## Adobe AnalyticsをアダプティブFormsに設定する {#setup-adobe-analytics-to-aem-forms}

AEM Forms Analytics レポートの場合、まず、Experience Cloud設定の自動化を通じてAdobe AnalyticsをAEM Formsに統合します。 Adaptive FormsでのExperience Cloud設定の自動化では、データ集計とインサイト生成を効率化するために、Adobe Analyticsライセンス、データ収集 ( 旧Adobe版 Launch)、Experience Platform LaunchAPI との統合が必要です。 訪問 [アダプティブフォームのAdobe Analyticsを有効にする (Experience Cloud設定の自動化を使用 )](/help/forms/forms-experience-cloud-setup-automation.md) を参照してください。

## アダプティブForms Adobe Analyticsレポートの表示 {#view-adobe-analytics-report}

1. AEMインスタンスで、に移動します。 **[!UICONTROL Forms]** >> **[!UICONTROL Formsとドキュメント]**.
1. フォームを選択すると、左側に示すように、Adobe AnalyticsがAdobe Analytics用にアクティブ化されたFormsに統合されています。

   ![レポートを表示](assets/activ-aa.png){width="100%"}

1. クリック **Adobe Analytics** レポートを表示し、パフォーマンスデータを分析します。

## アダプティブForms分析レポートについて {#understanding-aem-forms-analytics-reports}

Adobe Analyticsは、アダプティブFormsのパフォーマンス指標の包括的な配列を提供し、フォームの使用状況に関する有益なインサイトを提供します。 以下の指標があります。

### **アダプティブFormsのパフォーマンス** {#how-your-adaptive-form-is-performing}

フォームレンディション、フォーム送信、検証エラーおよび実訪問者数の指標が含まれ、フォームの使用状況と有効性を評価できます。

* **フォームレンディション**：フォームのレンディションは、フォームがレンダリングまたは開かれた回数を表示します。

* **フォームの送信**：フォームの送信は、アダプティブフォームが正常に完了し、ユーザーによって送信された回数を示します。

* **検証エラー**：検証エラーは、フォームのフィールドで発生した検証関連のエラーの合計数を表示します。

* **実訪問者数**：実訪問者数は、訪問者がフォームをレンダリングした回数を表します。 個別訪問者数について詳しくは、 [個別訪問者数、訪問回数、顧客の行動](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).

  ![Forms Performance](assets/forms-performance.png){width="100%"}

### **フォームの訪問者** {#visitors-to-your-forms}

これにより、フォーム上の訪問者のアクティビティに関する有益なインサイトを得ることができます。

* **訪問と送信**：日付範囲でのフォームへの訪問の頻度と、対応するフォーム送信数を表し、このクリックに関する詳細を示します [訪問回数](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).
* **個別訪問者数と合計訪問回数**：新しいユーザーと再訪問者を区別します。 例えば、ある訪問者が 1 ヶ月間毎日サイトを訪問しても、1 人の個別訪問者としてカウントされることがあります。 訪問 [実訪問者数](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) を参照してください。

  ![Forms Visitors](assets/forms-visitors.png){width="100%"}

### **デバイスタイプ** {#device-type}

デバイスタイプを使用すると、フォームへのアクセスに使用するデバイスの種類を識別できます。 このコードは、デバイスタイプをモバイルデバイスタイプに分類します。 例えば、この場合は「モバイルデバイスタイプ」が「その他」に、「モバイルデバイスタイプ」が「携帯電話」になります。 様々な種類のモバイルデバイスには、携帯電話、タブレット、メディアプレーヤー、ゲームコンソールなどが含まれます。

![デバイスタイプ](assets/device-type.png){width="100%"}

### **地理的分類** {#geographical-breakdown}

Formsのアクセス元が表示されます。 フォームユーザーに関する地域固有の情報を提供します。例えば、画像で示すように、フォームユーザーに関する地域固有の情報はインドです。

![地理的分類](assets/geographical-breakdown.png){width="100%"}

### **トラフィックおよび人気の高いフォームの上位のソース** {#top-sources-of-traffic-and-popular-forms}

これにより、フォームの参照元となるプライマリソースやリンクを識別できます。 例えば、以下の図では、18.9%がアダプティブフォームの検索インスタンスが表示されています **手動入力/ブックマーク** 70.49%、基準 **検索エンジン**、24%がから **その他の Web サイト**. 必要に応じて、ディメンション項目を定義できます。 また、最も訪問回数の多いフォームと人気の高いフォームを並べ替えることもできます。

![参照元のサイト](assets/referred-sites.png){width="100%"}

### **トップフォームでのユーザーアクティビティ** {#user-activity-on-top-forms}

フィールド訪問、フォームレンディション、検証エラー、破棄されたフォーム、フォーム送信に関するユーザーのエンゲージメントを包括的に表示することで、最もアクティブなフォームに関するインサイトを得ることができます。 以下の画像では、フォームイベント指標に基づくアプリケーションフォームが最もアクティブであることがわかります。

![ユーザーアクティビティ](assets/user-activity.png){width="100%"}

### **フォームでの滞在時間のタイムライン** {#timeline-for-time-spent-on-forms}

ユーザーが時間の経過と共にフォームに滞在する時間が、エンゲージメントパターンを識別するのに役立ちます。

![フォームでの滞在時間](assets/time-spent-on-forms.png){width="100%"}

### **訪問者がフォームの入力に関するサポートが必要な領域** {#areas-requiring-assistance}

ヘルプビュー、検証エラー、フィールド訪問などの指標は、ユーザーがサポートを必要とする場所や、フィールド内のエラーの追跡方法を明らかにします。 例えば、以下の画像では、次のようなフィールドを持つフォームに表示されています。 **姓名**, **電話番号**, **DoB**. The **姓名** フィールドには 12 回の訪問があり、12 回の訪問のうち 8 回の訪問には検証エラーが発生し、1 回のクリックでこのフィールドのヘルプ表示のヘルプアイコンが表示されます。 他のフォームフィールドの指標データを表示できます。

![支援エリア](assets/assisting-areas.png){width="100%"}

### **訪問者がフォームを破棄する前に表示した最後のフォームフィールド** {#last-form-field-that-visitors-viewed}

これは、ユーザーがフォームを破棄する前に時間を費やしたフォームフィールドを分析するのに役立ちます。 例えば、以下の画像では、5 つの廃止されたフォームの中から 2 つがフィールドに残っています。 **姓名**、フィールドに左に 2 **電話番号**、1 つがフィールドに残り **テキスト入力**.

![フィールド訪問者](assets/field-visitors.png){width="100%"}