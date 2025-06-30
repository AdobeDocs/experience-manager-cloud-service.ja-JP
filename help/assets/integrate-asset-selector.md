---
title: Vanilla JS を使用したアセットセレクターの統合
description: アセットセレクターを様々なアドビ、アドビ以外、サードパーティのアプリケーションと統合します。
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%

---

# Vanilla JS を使用したアセットセレクターの統合 {#integration-using-vanilla-js}

あらゆる [!DNL Adobe] アプリケーションまたはアドビ以外のアプリケーションを [!DNL Experience Manager Assets] リポジトリと統合し、アプリケーション内からアセットを選択できます。[アセットセレクターと様々なアプリケーションの統合](#asset-selector-integration-with-apps)を参照してください。

統合は、アセットセレクターパッケージを読み込み、Vanilla JavaScript ライブラリを使用して Assets as a Cloud Service に接続することで行われます。アプリケーション内の `index.html` または適切なファイルを、次の目的で編集します。

* 認証の詳細を定義する
* Assets as a Cloud Service リポジトリにアクセスする
* アセットセレクターの表示プロパティを設定する

次の場合は、一部の IMS プロパティを定義せずに認証を実行できます。

* [統合シェル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=ja)の [!DNL Adobe] アプリケーションを統合している場合。
* 認証用に既に IMS トークンが生成されている場合。

## アセットセレクターと様々なアプリケーションの統合 {#asset-selector-integration-with-apps}

アセットセレクターは、次のような様々なアプリケーションと統合できます。

* [アセットセレクターと  [!DNL Adobe]  アプリケーションの統合](/help/assets/integrate-asset-selector-adobe-app.md)
* [アセットセレクターとアドビ以外のアプリケーションの統合](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [OpenAPI 機能を備えた Dynamic Media の統合](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [アセットセレクターのカスタマイズ](/help/assets/asset-selector-customization.md)
>* [アセットセレクターのプロパティ](/help/assets/asset-selector-properties.md)
>* [OpenAPI 機能を備えた Dynamic Media とのアセットセレクターの統合](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
