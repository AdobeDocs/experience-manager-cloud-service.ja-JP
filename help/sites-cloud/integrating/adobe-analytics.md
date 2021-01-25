---
title: 'Adobe Analytics との統合 '
description: 'Adobe Analytics との統合 '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 100%

---


# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM as a Cloud Service の統合により、Web ページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* Adobe Analytics レポートスイートに送信されたデータはフレームワークで特定されます。

データには、例えば、次のようなページおよびユーザーデータが含まれます。

* AEM コンポーネントで収集されるデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問されるページの数

以下に示す記事は、統合の設定に役立ちます。なお、Experience Platform Launch は、Analytics 機能（JS ライブラリ）を備えた AEM サイトを実装するための事実上の標準ツールになっています。したがって、AEM as a Cloud Service を Launch や Adobe Analytics と統合すると、連携が強化されます。

* [Adobe Analytics への接続とフレームワークの作成](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/adobeanalytics-connect.html) - 「Analytics フレームワーク」は AEM のレガシー機能であり、分析の作成にはクラシック UI が必要なので AEM as a Cloud Service では機能しないことに注意してください。代わりに、変数マッピングにも JS ライブラリのページへのデプロイにも Experience Platform Launch を使用してください。
* [Experience Platform Launch の統合](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Adobe I/O を使用した AEM と Adobe Launch の統合](https://helpx.adobe.com/jp/experience-manager/using/aem_launch_adobeio_integration.html)
* [AEM と Experience Platform Launch、Analytics、Target の統合について](https://helpx.adobe.com/jp/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Adobe Analytics のリンクトラッキングの設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Adobe Analytics のビデオトラッキングの設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe 分類](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>既存の Analytics アカウントを持たない Adobe Experience Manager as a Cloud Service ユーザーは、Experience Cloud 用の Analytics Foundation パックへのアクセスをリクエストできます。この Foundation パックでは、Analytics の使用量が制限されます。

>[!NOTE]
>
>Experience Platform Launch の IMS 設定（技術アカウント）は、AEM as a Cloud Service に事前に設定されています。ユーザーはこの設定を作成する必要はありません。

## その他の情報 {#further-information}

次のページを参照してください。

* ユーザーデータを収集するコンポーネントの開発と Adobe Analytics フレームワークのカスタマイズに関する情報については、[Adobe Analytics 統合の拡張](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html)を参照してください。「Analytics フレームワーク」は AEM のレガシー機能であり、分析の作成にはクラシック UI が必要なので AEM as a Cloud Service では機能しないことに注意してください。代わりに、変数マッピングにも JS ライブラリのページへのデプロイにも Experience Platform Launch を使用してください。
* Adobe Analytics 統合のトラブルシューティングに関する情報については、[Adobe Analytics 統合 - 問題のトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)に関するナレッジベースの記事を参照してください。

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、（例えば、Web コンソールで）**Apache HTTP Client** プロキシ設定に必要な [2 つの OSGi バンドルを設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/deploying/configuring/configuring-osgi.html)する必要があります。AEM の一部の機能では 3.x API を使用し、他の機能では 4.x API を使用するので、両方とも必要です。設定：
>
>* **Day Commons HTTP Client 3.1**（3.x API を設定）。
>  例：[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP コンポーネントプロキシ設定**（4.x API を設定）。
>  例：[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


