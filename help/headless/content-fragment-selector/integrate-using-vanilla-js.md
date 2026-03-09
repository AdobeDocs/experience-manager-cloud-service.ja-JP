---
title: Vanilla JS を使用したコンテンツフラグメントセレクターの統合
description: コンテンツフラグメントセレクターを様々なAdobe、Adobe以外およびサードパーティ製アプリケーションと統合します。
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# Vanilla JS を使用したコンテンツフラグメントセレクターの統合 {#integrate-content-fragment-selector-using-vanilla-js}

任意のAdobeまたはAdobe以外のアプリケーションをAdobe Experience Manager （AEM） as a Cloud リポジトリーと統合し、そのアプリケーション内からコンテンツフラグメントを選択できます。

統合は、コンテンツフラグメントセレクターパッケージを読み込み、Vanilla JavaScript ライブラリを使用してAEM as a Cloud Serviceに接続することで行われます。 アプリケーション内の `index.html` または適切なファイルを、次の目的で編集します。

* 認証の詳細を定義する
* AEM as a Cloud Service リポジトリへのアクセス
* コンテンツフラグメントセレクターの表示プロパティを設定する

次の場合は、一部の IMS プロパティを定義せずに認証を実行できます。

* [ 統合シェル ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell) でAdobe アプリケーションを統合している
* 認証用に既に IMS トークンが生成されている
