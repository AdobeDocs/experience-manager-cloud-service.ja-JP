---
title: コンテンツオーサリングのためのサイト認証の設定
description: AEM Live がトークンベースの認証をサポートする方法と、WYSIWYG オーサリングで認証を使用するようにAEMを設定する方法について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 6d28b831fb902173bb5fbadd4aa2a52ba58e0a3b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 2%

---


# コンテンツオーサリングのためのサイト認証の設定 {#site-authentication}

AEM Live がトークンベースの認証をサポートする方法と、WYSIWYG オーサリングで認証を使用するようにAEMを設定する方法について説明します。

## 概要 {#overview}

AEM Live は、トークンベースの認証をサポートしています。 サイト認証は通常、プレビューサイトとパブリッシュサイトの両方に適用されますが、どちらか一方のサイトを個別に保護するように設定することもできます。

>[!NOTE]
>
>サイト認証を有効にする場合は、AEM オーサリング環境でも設定する必要があります

## 要件 {#requirements}

コンテンツのオーサリングで使用するサイト認証を設定するには、まず次のタスクを実行する必要があります。

* このドキュメントは、[Edge Delivery ServicesでのWYSIWYG オーサリングの開発者向けスタートガイド ](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) に基づいて、プロジェクトのサイトを既に作成していることを前提としています。
* [ プロジェクトのリソース機能を有効にする ](/help/edge/wysiwyg-authoring/repoless.md) 必要があります。

## サイト認証の設定 {#configure-authentication}

サイト認証の設定方法について詳しくは、[ サイト認証の設定 ](https://www.aem.live/docs/authentication-setup-site) のドキュメントを参照してください。

認証を設定する際には、次の情報に注意してください。

* テクニカルアカウントの ID
* サイト認証トークン

これらの項目は、AEM オーサリング環境でサイト認証の設定を行うために必要です。

## オーサリング環境の設定 {#authoring-environment}

サイト認証を設定したら、AEM オーサリング環境で有効にすることができます。

1. AEM オーサーインスタンスにサインインして **ツール**/**クラウドサービス**/**Edge Delivery Services Configuration** に移動し、サイト用に自動的に作成された設定を選択して、ツールバーの **プロパティ** をタップまたはクリックします。
1. **Edge Delivery Services設定** ウィンドウで、「**認証**」タブを選択して次の値を指定します。これは、サイト認証を設定した際に確認しました。

   * **テクニカルアカウント ID**
   * **サイト認証トークン**

   ![Edge Delivery Servicesの設定 ](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. 「**保存して閉じる**」をタップまたはクリックします。
