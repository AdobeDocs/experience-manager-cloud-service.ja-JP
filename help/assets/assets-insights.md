---
title: アセットインサイト
description: サードパーティの web サイト、マーケティングキャンペーン、アドビのクリエイティブソリューションで使用される画像のユーザー評価と使用状況統計を追跡します。
contentOwner: AG
feature: Asset Insights, Asset Reports
role: User, Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '901'
ht-degree: 100%

---

# アセットインサイト {#asset-insights}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

アセットインサイトの機能を使用すると、サードパーティの Web サイト、マーケティングキャンペーン、アドビのクリエイティブソリューションで使用される画像のユーザー評価と使用状況統計を追跡できます。これにより、画像のパフォーマンスと人気に関するインサイトが提供されます。

アセットインサイトでは、画像の評価回数、クリック数、インプレッション数（画像が Web サイトに読み込まれた回数）など、ユーザーのアクティビティの詳細を取得します。これらの統計情報に基づいて画像にスコアを割り当てます。スコアとパフォーマンス統計を使用して、人気が高い画像を選び、カタログやマーケティングキャンペーンなどに含めることができます。このような統計に基づいて、アーカイブやライセンス更新のポリシーを策定することもできます。

アセットインサイトが画像の使用状況統計を web サイトから取得するためには、画像の埋め込みコードを web サイトのコードに組み込む必要があります。

アセットインサイトでアセットの使用状況統計を表示できるようにするには、最初に [!DNL Adobe Analytics] からのレポートデータをフェッチするようにこの機能を設定します。詳しくは、[アセットインサイトの設定](#configure-asset-insights)を参照してください。この機能を使用するには、[!DNL Adobe Analytics] ライセンスを別途購入してください。

>[!NOTE]
>
>インサイトは画像に対してのみサポートされており、提供されています。

## 画像の統計情報の表示 {#viewing-statistics-for-an-image}

メタデータページでアセットインサイトのスコアを確認できます。

1. Assets ユーザーインターフェイスから、画像を選択し、ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。
1. プロパティページで、「**[!UICONTROL インサイト]**」をクリックします。
1. 「**[!UICONTROL インサイト]**」タブで、アセットの使用状況の詳細を確認します。「**[!UICONTROL スコア]**」セクションには、アセットの全体的な使用状況とパフォーマンスのスコアが表示されます。

   使用状況のスコアは、アセットが様々なソリューションで使用された回数です。

   「**[!UICONTROL インプレッション数]**」のスコアは、アセットが web サイトに読み込まれた回数です。「**[!UICONTROL クリック数]**」の下に表示される数値は、アセットがクリックされた回数です。

1. 「**[!UICONTROL 使用状況の統計]**」セクションを見て、アセットが含まれているエンティティや最近使用されたクリエイティブソリューションを確認します。使用率が高いほど、ユーザーの間で人気のあるアセットであることを意味します。使用状況データは、次の見出しの下に表示されます。

   * **[!UICONTROL アセット]**：アセットが、コレクションまたは複合アセットに含まれた回数
   * **[!UICONTROL Web およびモバイル]**：アセットが Web サイトまたはアプリに含まれた回数
   * **[!UICONTROL ソーシャル]**：アセットが [!DNL Adobe Campaign] などの他のソリューションで使用された回数。
   * **[!UICONTROL メール]**：アセットがメールキャンペーンで使用された回数

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >アセットインサイト機能は、通常 [!DNL Adobe Analytics] のソリューションデータを定期的にフェッチするので、「ソリューション」セクションには最新データが表示されていない場合があります。表示されるデータが対応する期間は、アセットインサイトが Analytics のデータを取得するために実行するフェッチ操作のスケジュールによって決まります。

1. 特定の期間のアセットのパフォーマンス統計をグラフィカルに表示するには、「**[!UICONTROL パフォーマンス統計]**」セクションで期間を選択します。クリック数やインプレッション数などの詳細がグラフの傾向線として表示されます。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >「ソリューション」セクションのデータとは異なり、「パフォーマンス統計」セクションには最新データが表示されます。

1. パフォーマンスデータを得るために Web サイトに組み込んだアセットの埋め込みコードを取得するには、アセットのサムネールの下の「**[!UICONTROL 埋め込みコードの取得]**」をクリックします。<!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## 画像の総統計の表示 {#viewing-aggregate-statistics-for-images}

**[!UICONTROL インサイト表示]**&#x200B;を使用すると、フォルダー内のすべてのアセットのスコアを同時に表示できます。

1. Assets ユーザーインターフェイスで、インサイトを表示するアセットを含むフォルダーに移動します。
1. ツールバーの「**[!UICONTROL レイアウト]**」オプションをクリックして、「**[!UICONTROL インサイト表示]**」を選択します。
1. このページには、アセットの使用状況スコアが表示されます。様々なアセットの評価を比較し、インサイトを引き出します。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## アセットインサイトの設定 {#configure-asset-insights}

[!DNL Experience Manager Assets] では、サードパーティ Web サイトで使用されているデジタルアセットの使用状況データを [!DNL Adobe Analytics] から取得します。アセットインサイトでこのようなデータを取得して洞察を得るためには、まず、[!DNL Adobe Analytics] と連携するようにこの機能を設定します。

>[!NOTE]
>
>インサイトのサポートおよび提供が行われるのは、画像に対してのみです。

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. 「**[!UICONTROL Insights 設定]**」カードをクリックします。

1. Analytics web サービスのアクセス情報については、 **[!UICONTROL Analytics]**／**[!UICONTROL 管理]**／**[!UICONTROL 管理ツール]**／**[!UICONTROL 会社設定]**／**[!UICONTROL web サービス]** に移動し、 **[!UICONTROL 共有された秘密鍵]** をコピーします。

   ウィザードで、 **[!UICONTROL データセンター]** を選択し、 **[!UICONTROL 会社]** の表示名、web サービスの **[!UICONTROL ユーザー名]** を入力して、 **[!UICONTROL 共有暗号鍵]** を貼り付けます。

   「**[!UICONTROL 認証]**」をクリックします。

   ![[!DNL Experience Manager]](assets/analytics-insight-config.png)のアセットインサイトに Adobe Analytics を設定する

   *図：[!DNL Experience Manager]*&#x200B;のアセットインサイトに Adobe Analytics を設定する

1. 認証が成功すると、ドロップダウンにレポートスイートが表示されます。Assets Insights でデータを取得する場所から Adobe Analytics **[!UICONTROL レポートスイート]** を選択します。「**[!UICONTROL 追加]**」をクリックします。

1. [!DNL Experience Manager] でレポートスイートが設定されたら、「**[!UICONTROL 完了]**」をタップします。

詳しくは、 [Adobe Analytics web サービス](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html?lang=ja) を参照してください。

### ページトラッカー {#page-tracker}

Adobe Analytics アカウントを設定すると、ページトラッカーコードが生成されます。サードパーティの Web サイトで使用されている [!DNL Experience Manager] アセットをアセットインサイトで追跡できるようにするには、Web サイトコードにトラッカーコードを組み込みます。Assets のページトラッカーユーティリティを使用してページトラッカーコードを生成してください。<!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. [!DNL Experience Manager] で&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL アセット]**&#x200B;をクリックします。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. 「**[!UICONTROL ダウンロード]**」をクリックして、ページトラッカーコードをダウンロードします。

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
次のサンプルコードスニペットは、サンプル Web ページに組み込まれたページトラッカーコードです。

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
