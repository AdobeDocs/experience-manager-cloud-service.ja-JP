---
title: Adobe Analytics との統合
description: 'Adobe Analytics との統合 '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a

---


# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe AnalyticsとAEMをクラウドサービスとして統合すると、Webページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* フレームワークは、Adobe Analyticsレポートスイートに送信されるデータを識別します。

データには、次のようにページとユーザーデータが含まれます。

* AEM コンポーネントが収集するデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問するページ数

以下に示すページは、統合の設定に役立ちます。 アドビによる起動は、AEMサイトにAnalytics機能（JSライブラリ）を実装するデファクトツールです。 したがって、AEMをクラウドサービスとしてLaunchとAdobe Analyticsを統合すると、Adobe Analyticsが連携します。

* [Adobe Analyticsへの接続とフレームワークの作成](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) - 「Analyticsフレームワーク」はAEMではレガシーで、クラシックUIが必要なので、AEMでクラウドサービスとして機能しないことに注意してください。 代わりに、変数マッピングとJSライブラリのページへのデプロイの両方で、Adobeによる起動を使用する必要があります。
* [Integrate Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [Adobe I/Oを使用したAEMとAdobe launchの統合](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [AEMとAdobe、Analytics、およびTargetのLaunchとの統合について](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [Adobe Analytics のリンクトラッキングの設定](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [Adobe Analytics のビデオトラッキングの設定](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe 分類](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>既存のAnalyticsアカウントを持たないクラウドサービスのお客様は、Adobe Experience Managerを使用して、Analytics Foundation Pack for Experience cloudへのアクセスをリクエストできます。  このFoundation packは、Analyticsの使用量を制限します。

>[!NOTE]
>
>アドビが起動するIMS設定（技術アカウント）は、クラウドサービスとしてAEMに事前に設定されています。 ユーザーはこの設定を作成する必要はありません。

## その他の情報 {#further-information}

次のページを参照してください。

* [Adobe Analytics統合の拡張を参照してください](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) 。 「Analyticsフレームワーク」はAEMでは従来のものであり、クラシックUIが必要なので、AEMでのクラウドサービスとしての作成は機能しません。 代わりに、変数マッピングとJSライブラリのページへのデプロイの両方で、Adobeによる起動を使用する必要があります。
* The knowledge base article, [Adobe Analytics integration - troubleshooting issues](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), for information about troubleshooting your Adobe Analytics integration.

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、**Apache HTTP Client** プロキシ設定に必要な、[2 つの OSGi バンドルを設定](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/configuring-osgi.html)する必要があります（例えば、Web コンソールで）。AEM の一部の機能で 3.x API を使用し、他の機能で 4.x API を使用するので、両方とも必要です。次の設定をおこないます。
>
>* **Day Commons HTTP Client 3.1** to configure the 3.x API;
   >  例えば、 [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTPコンポーネントプロキシ設定** （4.x APIを設定）
   >  例えば、 [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


