---
title: コンテンツのオーサリングのためのサイト認証の設定
description: AEM Live でのトークンベースの認証サポート形式、WYSIWYG オーサリングで認証を使用するように AEM を設定する方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: b2838da2-79c7-49b1-a101-15c21e80197e
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---

# コンテンツのオーサリングのためのサイト認証の設定 {#site-authentication}

AEM Live でのトークンベースの認証サポート形式、WYSIWYG オーサリングで認証を使用するように AEM を設定する方法について説明します。

## 概要 {#overview}

AEM Live は、トークンベースの認証をサポートしています。サイト認証は通常、プレビューサイトとパブリッシュサイトの両方に適用されますが、どちらか一方のサイトを個別に保護するように設定することもできます。

>[!NOTE]
>
>サイト認証を有効にする場合は、AEM オーサリング環境でもサイト認証を設定する必要があります

## 要件 {#requirements}

コンテンツのオーサリングで使用するサイト認証を設定するには、まず次のタスクを実行する必要があります。

* このドキュメントは、[Edge Delivery Services を使用した WYSIWYG オーサリングの開発者向け入門ガイド](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)に基づいて、プロジェクトのサイトを既に作成していることを前提としています。
* [プロジェクトの repoless 機能が既に有効になっている](/help/edge/wysiwyg-authoring/repoless.md)必要があります。

## サイト認証の設定 {#configure-authentication}

サイト認証の設定方法について詳しくは、[サイト認証の設定](https://www.aem.live/docs/authentication-setup-site)のドキュメントを参照してください。

認証を設定する際には、次の情報をメモしておいてください。

* テクニカルアカウントの ID
* サイト認証トークン

これらの項目は、AEM オーサリング環境でサイト認証の設定を行うために必要です。

## オーサリング環境の設定 {#authoring-environment}

設定したサイト認証は、AEM オーサリング環境で有効にすることができます。

1. AEM オーサーインスタンスにログインして、**ツール**／**クラウドサービス**／**Edge Delivery Services 設定**&#x200B;に移動し、サイト用に自動作成された設定を選択して、ツールバーの「**プロパティ**」をタップまたはクリックします。
1. **Edge Delivery Services 設定**&#x200B;ウィンドウで、「**認証**」タブを選択し、以前にコピーした&#x200B;**サイト認証トークン**&#x200B;を指定します。

   ![Edge Delivery Services 設定](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. **テクニカルアカウント ID** が以前にコピーしたアカウントと一致することを確認します。

   * このフィールドは読み取り専用で、あらかじめ定義されています。
   * テクニカルアカウントは、同じ AEM オーサー環境にあるすべてのサイトで同じです。

1. 「**保存して閉じる**」をタップまたはクリックします。
