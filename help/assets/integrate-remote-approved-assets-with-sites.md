---
title: リモート AEM Assets と AEM Sites の統合
description: AEM Sites を設定し、承認済み AEM Assets に接続する方法について説明します。
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: 2ec0b4125aa0990b6e022350a1f861fe394e6b1f
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 91%

---

# リモート AEM Assets と AEM Sites の統合  {#integrate-approved-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>OpenAPI 機能搭載 Dynamic Media のガイドを、PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE OpenAPI 機能搭載 Dynamic Media ガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

デジタルアセットを効果的に管理することは、様々なオンラインプラットフォームにわたって魅力的で一貫性のあるブランドエクスペリエンスを提供するのに重要です。OpenAPI 機能を備えた Dynamic Media は、AEM Sites と AEM Assets as a Cloud Service 間のシームレスな統合を有効にして、デジタルアセット管理を強化します。この革新的な機能により、複数の AEM 環境間で様々なタイプの承認済みデジタルアセットを簡単に共有および管理でき、サイト作成者とコンテンツ編集者のワークフローが効率化されます。

OpenAPI 機能を備えた Dynamic Media を使用すると、サイト作成者はリモート DAM のアセットを AEM ページエディターおよび[コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html?lang=ja)内で直接使用できるので、コンテンツの作成および管理プロセスが簡素化されます。

ユーザーは、最大数の制限なしに複数の AEM Sites インスタンスをリモート DAM デプロイメントに接続できます。これは、[接続されたアセット](use-assets-across-connected-assets-instances.md)機能に比べて著しく優れています。

![画像](/help/assets/assets/connected-assets-rdam.png)

初期設定後、ユーザーは AEM Sites インスタンス上にページを作成し、必要に応じてアセットを追加できます。アセットを追加する際は、ローカル DAM に保存されているアセットを選択するか、リモート DAM で使用可能なアセットを参照して使用することができます。

OpenAPI 機能を備えた Dynamic Media には、コンテンツフラグメント内のリモートアセットへのアクセスと使用、リモートアセットのメタデータの取得など、他にもいくつかのメリットがあります。詳しくは、[接続されたアセットと比較した OpenAPI 機能を備えた Dynamic Media のその他のメリット](/help/assets/dynamic-media-open-apis-faqs.md)を参照してください。

## 始める前に {#pre-requisites-sites-integration}

OpenAPI 機能を備えた Dynamic Media を使用したリモートアセットのサポートには、以下が必要です。

* AEM 6.5 SP 18 以降または AEM as a Cloud Service

* コアコンポーネントリリース 2.23.2 以降

* AEM as a Cloud Service に次の[環境変数](/help/implementing/cloud-manager/environment-variables.md#add-variables)を設定します。

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` はプログラム ID を参照します<br>。
     `eYYYY` は環境 ID を参照します。

  これらの変数は、ローカル Sites インスタンスとして機能する AEM as a Cloud Service 環境の Cloud Manager ユーザーインターフェイスを使用して設定されます。

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]：IMS クライアント ID を取得するには、アドビサポートチケットを送信する必要があります。

     または、次の手順に従って、AEM Sites インスタンスで AEM 6.5 の [OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html?lang=ja)を行います。

   1. コンソールにログインして「**[!UICONTROL OSGi] >**」をクリックするか、
直接 URL を使用します。例：`https://localhost:4502/system/console/configMgr`

   1. **次世代の Dynamic Media 設定**（`NextGenDynamicMediaConfigImpl`）OSGi の設定を次のように行って、値をリモートアセット環境の値に置き換えます。

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` は必須の入力ではありません。
      `repositoryId` = &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;
ここで、`pXXXX` はプログラム ID を参照します。
      `eYYYY` は環境 ID を参照します

      ![次世代の Dynamic Media 設定 OSGi の設定ウィンドウ](/help/assets/assets/remote-assets-osgi.png)

  詳しくは、[IMS 認証](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html?lang=ja)を参照してください。

  OSGi の設定方法について詳しくは、次のドキュメントを参照してください。

   * AEM as a Cloud Service 用の [Adobe Experience Manager as a Cloud Service の OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=ja)
   * AEM 6.5 用の [OSGi の設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=ja)

* リモート DAM AEM as a Cloud Service インスタンスにログインする IMS アクセス。これは、リモート DAM 環境への IMS アクセス権を持つ Sites 作成者を参照します。

* AEM Sites インスタンスで画像 v3 コンポーネントを設定します。コンポーネントが存在しない場合は、[コンテンツパッケージ](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0)をダウンロードしてインストールします。

## HTTPS を設定 {#https}

通常は、HTTP を使用して、すべての実稼動 AEM インスタンスを実行することをお勧めします。ただし、ローカル開発環境がこのように設定されていない場合があります。しかし、OpenAPI 搭載 Dynamic Media を使用するリモートアセットを機能させるには HTTPS が必要です。

[このガイドを使用](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=ja)して、開発環境を含むリモートアセットを使用する場所で HTTPS を設定します。

## リモート DAM からのアセットへのアクセス {#fetch-assets}

OpenAPI 機能を備えた Dynamic Media を使用すると、ローカルの AEM Sites ページエディターおよび AEM コンテンツフラグメント上のリモート DAM インスタンスで使用可能なアセットにアクセスできます。

![画像](/help/assets/assets/open-APIs.png)

### AEM ページエディターでのリモートアセットへのアクセス {#access-assets-page-editor}

AEM Sites インスタンスの AEM ページエディター内でリモートアセットを使用するには、次の手順に従います。この統合は、AEM as a Cloud Service および AEM 6.5 で実行できます。

1. **[!UICONTROL Sites]**／_自分の web サイト_&#x200B;に移動します。この web サイト内に、リモートアセットを追加する必要がある AEM **[!UICONTROL ページ]**&#x200B;が存在します。
1. ページを選択し、「**[!UICONTROL 編集（_e_）]**」をクリックします。AEM **[!UICONTROL ページエディター]**&#x200B;が開きます。
1. レイアウトコンテナをクリックし、**[!UICONTROL 画像]**&#x200B;コンポーネントを追加します。
1. **[!UICONTROL 画像]**&#x200B;コンポーネントをクリックし、![設定アイコン](/help/assets/assets/do-not-localize/settings-icon.svg) アイコンをクリックします。
1. 「**[!UICONTROL ページからアイキャッチ画像を継承]**」オプションをオフにします。
1. 「**[!UICONTROL 選択]**」をクリックして、「**[!UICONTROL リモート]**」を選択します。
   ![画像](/help/assets/assets/uncheck-inherit-option.jpg)

   ログインを求めるプロンプトが表示されます。
1. アセットを選択し、「**[!UICONTROL 選択]**」をクリックします。
1. 代替テキストを追加し、「**[!UICONTROL 完了]**」をクリックします。
   <br>リモートアセットが画像コンポーネントに表示されます。また、アセットの配信 URL は、ページに読み込まれた際や、「プレビュー」タブを使用して確認することもできます。配信 URL は、アセットがリモートでアクセスされていることを示します。

画像コアコンポーネント v3 とティーザーコアコンポーネント v2 の場合のみ、AEM ページエディターで標準のリモートアセットにアクセスできます。カスタムコンポーネントを含むその他のコンポーネントについては、アセットセレクターをこれらのコンポーネントと統合するのにカスタマイズが必要です。

#### ビデオ：AEM ページエディターでのリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### AEM コンテンツフラグメントでのリモートアセットへのアクセス {#access-assets-content-fragment}

AEM Sites インスタンスの AEM コンテンツフラグメント内でリモートアセットを使用するには、次の手順に従います。この統合は AEM 6.5 で実行できますが、AEM as a Cloud Service では実行できません。

1. **[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;に移動します。
1. コンテンツフラグメントが存在するアセットフォルダーを選択します。
1. コンテンツフラグメントを選択し、「**[!UICONTROL 編集（_e_）]**」をクリックします。

   >[!NOTE]
   >
   AEM コンテンツフラグメントモデルがない場合は、[作成](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=ja)する必要があります。

1. テキストコンポーネントの横にある ![チェックマークアイコン](/help/assets/assets/do-not-localize/checkmark-icon.svg) アイコンをクリックします。
1. 「**[!UICONTROL リモート]**」を選択して、リモート DAM からアセットを取得します。<br>
ニーズに応じて、**[!UICONTROL ローカル]**&#x200B;または&#x200B;**[!UICONTROL リモート]**&#x200B;の DAM リポジトリを選択できます。

   ![画像](/help/assets/assets/cf-pick.jpg)
ログインを求めるプロンプトが表示されます。
1. アセットを選択し、「**[!UICONTROL 選択]**」をクリックします。
   <br>リモートアセット URL がテキストコンポーネントに表示されます。

#### ビデオ：AEM コンテンツフラグメントでのリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Edge Delivery Services でのリモートアセットへのアクセス {#access-assets-eds}

Microsoft Word、Google Docsまたはユニバーサルエディターでコンテンツを作成してEdge Delivery Servicesに公開する際に、リモートアセットにアクセスできます。 また、Dynamic Media を OpenAPI と共に使用して、ブランド承認済みのアセットを配信し、他にも多くの利点を利用できます。 詳しくは、[Edge Delivery Services用のコンテンツのオーサリング中のAEM Assetsの統合 ](/help/assets/integrate-aem-assets-edge-delivery-services.md) を参照してください。
