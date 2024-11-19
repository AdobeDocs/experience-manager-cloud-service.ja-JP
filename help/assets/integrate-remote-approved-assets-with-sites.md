---
title: リモート AEM Assets と AEM Sites の統合
description: AEM Sites を設定して承認済みAEM Assetsに接続する方法を説明します。
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 15%

---

# リモート AEM Assets と AEM Sites の統合  {#integrate-approved-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

様々なオンラインプラットフォームにわたって魅力的で一貫性のあるブランドエクスペリエンスを提供するには、デジタルアセットを効果的に管理することが重要です。 OpenAPI 機能を備えたDynamic Mediaは、AEM SitesとAEM Assetsas a Cloud Service間のシームレスな統合を可能にすることで、デジタルアセット管理を強化します。 この革新的な機能により、複数のAEM環境にわたって様々なタイプの承認済みデジタルアセットを簡単に共有および管理し、サイト作成者およびコンテンツ編集者のワークフローを合理化できます。

OpenAPI 機能を備えたDynamic Mediaを使用すると、サイト作成者はリモート DAM のアセットをAEM ページエディターおよび [ コンテンツフラグメント ](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html?lang=ja) 内で直接使用して、コンテンツの作成プロセスと管理プロセスをシンプル化できます。

複数のAEM Sites インスタンスを、最大数に制限なくリモート DAM デプロイメントに接続できます。これは、[Connected Assets](use-assets-across-connected-assets-instances.md) 機能よりも大きな利点です。

![画像](/help/assets/assets/connected-assets-rdam.png)

初期設定が完了したら、AEM Sites インスタンス上にページを作成し、必要に応じてアセットを追加できます。 アセットを追加する際は、ローカル DAM に保存されているアセットを選択するか、リモート DAM で使用可能なアセットを参照して使用できます。

OpenAPI 機能を備えたDynamic Mediaには、コンテンツフラグメントでのリモートアセットへのアクセスと使用、リモートアセットのメタデータの取得など、他のいくつかの利点があります。 他の [Connected Assetsと比較した OpenAPI 機能を備えたDynamic Mediaのメリット ](/help/assets/dynamic-media-open-apis-faqs.md) についての詳細をご覧ください。

## 事前準備 {#pre-requisites-sites-integration}

Dynamic Mediaを OpenAPI 機能と共に使用してリモートアセットをサポートするには、次が必要です。

* AEM 6.5 SP 18 以降または AEM as a Cloud Service

* コアコンポーネントリリース 2.23.2 以降

* AEM as a Cloud Service用に次の [ 環境変数 ](/help/implementing/cloud-manager/environment-variables.md#add-variables) を設定します。

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` はプログラム ID <br> を参照します
     `eYYYY` は環境 ID を指します

  これらの変数は、ローカル Sites インスタンスとして機能するAEM as a Cloud Service環境のCloud Manager ユーザーインターフェイスを使用して設定されます。

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]:IMS クライアント ID を取得するには、Adobeサポートチケットを送信する必要があります。

     または、次の手順に従って、AEM Sites インスタンスでAEM 6.5 の [OSGi 設定 ](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) を指定します。

   1. コンソールにログインし、**[!UICONTROL OSGi]/** をクリックするか
ダイレクト URL を使用する例：`https://localhost:4502/system/console/configMgr`

   1. **Next Generation Dynamic Media Config** （`NextGenDynamicMediaConfigImpl`）の OSGi 設定を次のように行い、値をリモートアセット環境の値に置き換えます。

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` は必須入力ではありません。
      `repositoryId` = &quot;delivery-pxxxxx-eyyyy.adobeaemcloud.com&quot;
ここで、`pXXXX` はプログラム ID を表します
      `eYYYY` は環境 ID を指します

      ![次世代の Dynamic Media 設定 OSGi の設定ウィンドウ](/help/assets/assets/remote-assets-osgi.png)

  [IMS 認証 ](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html) の詳細情報。

  OSGi の設定方法について詳しくは、次のドキュメントを参照してください。

   * AEM as a Cloud Service 用の [Adobe Experience Manager as a Cloud Service の OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=ja)
   * AEM 6.5 用の [OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=ja)

* リモート DAM AEM as a Cloud Service インスタンスにログインするための IMS アクセス。 リモート DAM 環境への IMS アクセス権を持つ Sites オーサーを指します。

* AEM Sites インスタンスに Image v3 コンポーネントを設定します。 コンポーネントが存在しない場合は、[ コンテンツパッケージ ](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0) をダウンロードしてインストールします。

## HTTPS を設定 {#https}

通常は、HTTP を使用して、すべての実稼動 AEM インスタンスを実行することをお勧めします。ただし、ローカル開発環境がこのように設定されていない場合があります。しかし、OpenAPI 搭載 Dynamic Media を使用するリモートアセットを機能させるには HTTPS が必要です。

[このガイドを使用](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=ja)して、開発環境を含むリモートアセットを使用する場所で HTTPS を設定します。

## リモート DAM からのアセットへのアクセス {#fetch-assets}

OpenAPI 機能を備えたDynamic Mediaを使用すると、ローカルのAEM Sites ページエディターおよびAEM コンテンツフラグメント上のリモート DAM インスタンスで使用可能なアセットにアクセスできます。

![画像](/help/assets/assets/open-APIs.png)

### AEM ページエディターでのリモートアセットへのアクセス {#access-assets-page-editor}

AEM Sites インスタンスのAEM ページエディターでリモートアセットを使用するには、次の手順に従います。 統合はAEM as a Cloud ServiceとAEM 6.5 で行えます。

1. **[!UICONTROL Sites]**/_自分の web サイト_ に移動します。ここにAEM **[!UICONTROL Page]** があり、リモートアセットを追加する必要があります。
1. ページを選択し、「**[!UICONTROL 編集（_e_）]**」をクリックします。 AEM **[!UICONTROL ページエディター]** が開きます。
1. レイアウトコンテナをクリックし、**[!UICONTROL 画像]** コンポーネントを追加します。
1. **[!UICONTROL 画像]** コンポーネントをクリックし、![ 設定アイコン ](/help/assets/assets/do-not-localize/settings-icon.svg) アイコンをクリックします。
1. 「**[!UICONTROL ページからアイキャッチ画像を継承]**」オプションのチェックを外します。
1. **[!UICONTROL 選択]** をクリックし、**[!UICONTROL リモート]** を選択します。
   ![画像](/help/assets/assets/uncheck-inherit-option.jpg)

   ログインするように求められます。
1. アセットを選択し、「**[!UICONTROL 選択]** をクリックします。
1. 代替テキストを追加し、「完了 **[!UICONTROL をクリックし]** す。
   <br> リモートアセットが画像コンポーネントに表示されます。 また、アセットがページに読み込まれたとき、または「プレビュー」タブを使用して、アセットの配信 URL を確認することもできます。 配信 URL は、アセットがリモートからアクセスされていることを示します。

画像コアコンポーネント v3 およびティーザーコアコンポーネント v2 の場合のみ、AEM ページエディターで標準でリモートアセットにアクセスできます。 カスタムコンポーネントなど、他のコンポーネントを使用する場合は、アセットセレクターをそれらのコンポーネントと統合するためにカスタマイズが必要です。

#### ビデオ：AEM ページエディターでのリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### AEM コンテンツフラグメント内のリモートアセットへのアクセス {#access-assets-content-fragment}

AEM Sites インスタンスのAEM コンテンツフラグメント内でリモートアセットを使用するには、次の手順に従います。 この統合は、AEM as a Cloud ServiceではなくAEM 6.5 で行えます。

1. **[!UICONTROL Assets]** / **[!UICONTROL ファイル]** に移動します。
1. コンテンツフラグメントが存在するアセットフォルダーを選択します。
1. コンテンツフラグメントを選択し、**[!UICONTROL 編集（_e_）]** をクリックします。

   >[!NOTE]
   >
   AEM コンテンツフラグメントモデルがない場合は、[ 作成 ](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en) が必要になる場合があります。

1. テキストコンポーネントの横にある ![ チェックマークアイコン ](/help/assets/assets/do-not-localize/checkmark-icon.svg) アイコンをクリックします。
1. 「**[!UICONTROL リモート]**」を選択して、リモート DAM からアセットを取得します。 <br>
必要に応じて、**[!UICONTROL ローカル]** または **[!UICONTROL リモート]** DAM リポジトリを選択できます。

   ![ 画像 ](/help/assets/assets/cf-pick.jpg)
ログインするように求められます。
1. アセットを選択し、「**[!UICONTROL 選択]** をクリックします。
   <br> リモートアセットの URL がテキストコンポーネントに表示されます。

#### ビデオ：AEM コンテンツフラグメント内のリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Edge Delivery Servicesでのリモートアセットへのアクセス {#access-assets-eds}

また、Edge Delivery Servicesでリモートアセットにアクセスすることもできます。 詳しくは、[Dynamic Mediaを使用して OpenAPI 機能で配信される、Assetsas a Cloud Serviceのアセットの利用 ](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi) を参照してください。
