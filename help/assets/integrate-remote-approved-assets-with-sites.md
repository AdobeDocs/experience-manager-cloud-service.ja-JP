---
title: リモート AEM AssetsとAEM Sitesの統合
description: Creative CloudでAEM サイトを設定し、承認済みAEM Assetsに接続する方法を説明します。
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# リモート AEM AssetsとAEM Sitesの統合  {#integrate-approved-assets}

様々なオンラインプラットフォームにわたって魅力的で一貫性のあるブランドエクスペリエンスを提供するには、デジタルアセットを効果的に管理することが重要です。 OpenAPI 機能を備えたDynamic Mediaは、AEM Sitesとリモート AEM Assetsのシームレスな統合を可能にすることで、デジタルアセット管理を強化します。 この革新的な機能により、複数のAEM環境にわたって様々なタイプの承認済みデジタルアセットを簡単に共有および管理し、サイト作成者およびコンテンツ編集者のワークフローを合理化できます。

OpenAPI 機能を備えたDynamic Mediaを使用すると、サイト作成者はリモート DAM のアセットをAEM ページエディター内で直接使用できます。 [コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)、コンテンツの作成プロセスと管理プロセスを簡素化します。

最大の数に制限なく複数のAEM Sites インスタンスをリモート DAM デプロイメントに接続できます。これは、以上の主な利点です [接続された Assets](use-assets-across-connected-assets-instances.md) 機能

![画像](/help/assets/assets/connected-assets-rdam.png)

初期設定が完了したら、AEM Sites インスタンス上にページを作成し、必要に応じてアセットを追加できます。 アセットを追加する際は、ローカル DAM に保存されているアセットを選択するか、リモート DAM で使用可能なアセットを参照して使用できます。

OpenAPI 機能を備えたDynamic Mediaには、コンテンツフラグメントでのリモートアセットへのアクセスと使用、リモートアセットのメタデータの取得など、他のいくつかの利点があります。 もう一方について詳しく知る [connected Assets と比較した OpenAPI 機能のDynamic Mediaのメリット](/help/assets/new-dynamic-media-apis-faqs.md).

## 事前準備

* 以下を設定します [環境変数](/help/implementing/cloud-manager/environment-variables.md#add-variables) AEMas a Cloud Serviceの場合：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` はプログラム ID を参照します <br>
     `eYYYY` は環境 ID を指します

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  または、 [OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) AEM Sites インスタンスのAEM 6.5 の場合は、次の手順に従います。

   1. コンソールにログインし、 **[!UICONTROL OSGi] >** またはダイレクト URL を使用します。例： `http://localhost:4502/system/console/configMgr`

   1. を追加 **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;および **[!UICONTROL imsClient]**= [IMSClientId]
の詳細情報 [IMS 認証](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* リモート DAM AEMas a Cloud Serviceインスタンスにログインするための IMS アクセス。

* リモート DAM で「OpenAPI 機能を使用したDynamic Media」トグルをオンにします。

* AEM Sites インスタンスに Image v3 コンポーネントを設定します。 コンポーネントが存在しない場合は、 [コンテンツパッケージ](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## リモート DAM からのアセットへのアクセス {#fetch-assets}

OpenAPI 機能を備えたDynamic Mediaを使用すると、ローカルのAEM Sites ページエディターおよびAEM コンテンツフラグメント上のリモート DAM インスタンスで使用可能なアセットにアクセスできます。

![画像](/help/assets/assets/open-APIs.png)

### AEM ページエディターでのリモートアセットへのアクセス

AEM Sites インスタンスのAEM ページエディターでリモートアセットを使用するには、次の手順に従います。 この統合は、AEM as a Cloud ServiceとAEM 6.5 で行えます。

1. に移動 **[!UICONTROL Sites]** > _web サイト_ AEMが **[!UICONTROL ページ]** は、リモートアセットを追加する必要がある場所に存在します。
1. 特定のAEMへの移動 **[!UICONTROL ページ]** web サイト内の **[!UICONTROL Sites]** リモートアセットを追加するセクション。
1. ページを選択し、 **[!UICONTROL 編集（_e_）]**. AEM **[!UICONTROL ページエディター]** が開きます。
1. レイアウトコンテナをクリックして、 **[!UICONTROL 画像]** コンポーネント。
1. 「」をクリックします **[!UICONTROL 画像]** コンポーネントして、 ![設定アイコン](/help/assets/assets/do-not-localize/settings-icon.svg) アイコン。
1. 「」をオフにします **[!UICONTROL ページからアイキャッチ画像を継承]** オプション。
1. クリック **[!UICONTROL 選択]** を選択して、 **[!UICONTROL リモート]**.
   ![画像](/help/assets/assets/uncheck-inherit-option.jpg)

   ログインするように求められます。
1. アセットを選択し、 **[!UICONTROL を選択]**.
1. 代替テキストを追加し、をクリックします **[!UICONTROL 完了]**.
   <br> リモートアセットが画像コンポーネントに表示されます。 また、アセットがページに読み込まれたとき、または「プレビュー」タブを使用して、アセットの配信 URL を確認することもできます。 配信 URL は、アセットがリモートからアクセスされていることを示します。

#### ビデオ：AEM ページエディターでのリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### AEM コンテンツフラグメント内のリモートアセットへのアクセス

AEM Sites インスタンスのAEM コンテンツフラグメント内でリモートアセットを使用するには、次の手順に従います。 この統合は、AEM as a Cloud Service環境ではなく、AEM 6.5 で行えます。

1. に移動 **[!UICONTROL アセット]** > **[!UICONTROL ファイル]**.
1. コンテンツフラグメントが存在するアセットフォルダーを選択します。
1. コンテンツフラグメントを選択し、 **[!UICONTROL 編集（_e_）]**.

   >[!NOTE]
   >
   >AEM コンテンツフラグメントモデルがない場合は、次が必要な場合があります。 [1 つ作成](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. 「」をクリックします ![チェックマークアイコン](/help/assets/assets/do-not-localize/checkmark-icon.svg) アイコンがテキストコンポーネントの隣に表示されます。
1. を選択 **[!UICONTROL リモート]** をクリックしてリモート DAM からアセットを取得します。 <br>
次のいずれかを選択できます **[!UICONTROL ローカル]** または **[!UICONTROL リモート]** 必要に応じて DAM リポジトリを設定します。

   ![画像](/help/assets/assets/cf-pick.jpg)
ログインするように求められます。
1. アセットを選択し、 **[!UICONTROL を選択]**.
   <br> リモートアセットの URL がテキストコンポーネントに表示されます。

#### ビデオ：AEM コンテンツフラグメント内のリモートアセットへのアクセス

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
