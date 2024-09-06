---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを様々なAdobe、Adobe以外のアプリケーションおよびサードパーティアプリケーションと統合します。
role: Admin, User
source-git-commit: fb1350c91468f9c448e34b66dc938fa3b5a3e9a9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 86%

---


# Vanilla JS を使用したアセットセレクターの統合 {#integration-using-vanilla-js}

あらゆる [!DNL Adobe] アプリケーションまたはアドビ以外のアプリケーションを [!DNL Experience Manager Assets] リポジトリと統合し、アプリケーション内からアセットを選択できます。[アセットセレクターと様々なアプリケーションの統合](#integrate-asset-selector.md)を参照してください。

統合は、アセットセレクターパッケージを読み込み、Vanilla JavaScript ライブラリを使用して Assets as a Cloud Service に接続することで行われます。アプリケーション内の `index.html` または適切なファイルを、次の目的で編集します。

* 認証の詳細を定義する
* Assets as a Cloud Service リポジトリにアクセスする
* アセットセレクターの表示プロパティを設定する

次の場合は、一部の IMS プロパティを定義せずに認証を実行できます。

* [統合シェル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=ja)の [!DNL Adobe] アプリケーションを統合している場合。
* 認証用に既に IMS トークンが生成されている場合。

## アセットセレクターと様々なアプリケーションの統合 {#asset-selector-integration-with-apps}

アセットセレクターは、次のような様々なアプリケーションと統合できます。

* [アセットセレクターと  [!DNL Adobe]  アプリケーションの統合](#integrate-asset-selector.md)
* [アセットセレクターとアドビ以外のアプリケーションの統合](#integrate-asset-selector-non-adobe.md)
* [OpenAPI 機能を備えた Dynamic Media の統合](#integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [ アセットセレクターのカスタマイズ ](/help/assets/asset-selector-customization.md)
>* [ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md)
>* [ アセットセレクター Dynamic Media オープン API の統合 ](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)

