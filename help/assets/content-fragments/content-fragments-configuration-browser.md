---
title: コンテンツフラグメント - 設定ブラウザー
description: AEM の強力なヘッドレス配信機能を活用するために、設定ブラウザーで特定のコンテンツフラグメント機能を有効にする方法を説明します。
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 92%

---

# コンテンツフラグメント - 設定ブラウザー{#content-fragments-configuration-browser}

AEM の強力なヘッドレス配信機能を活用するために、設定ブラウザーで特定のコンテンツフラグメント機能を有効にする方法を説明します。

## インスタンスに対するコンテンツフラグメント機能の有効化 {#enable-content-fragment-functionality-instance}

コンテンツフラグメントを使用する前に、**設定ブラウザー**&#x200B;を使用して以下を有効にする必要があります。

* **コンテンツフラグメントモデル** - 必須
* **GraphQL の永続的なクエリ** - オプション

>[!CAUTION]
>
>**コンテンツフラグメントモデル**&#x200B;を有効にしない場合：
>
>* 新しいモデルを作成する&#x200B;**作成**&#x200B;オプションは使用できません。
>* [Sites 設定を選択して関連するエンドポイントを作成する](/help/headless/graphql-api/graphql-endpoint.md)ことはできません。


コンテンツフラグメント機能を有効にするには、次の操作を実行する必要があります。

* 設定ブラウザーを使用して、コンテンツフラグメント機能の使用を有効にする
* アセットフォルダーへの設定の適用

### 設定ブラウザーでコンテンツフラグメント機能を有効にする {#enable-content-fragment-functionality-in-configuration-browser}

[特定のコンテンツフラグメント機能](#creating-a-content-fragment-model)を使用するには、まず&#x200B;**設定ブラウザー**&#x200B;を使用して有効にする&#x200B;**必要があります**。

>[!NOTE]
>
>詳しくは、「[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)」も参照してください。

>[!CAUTION]
>
>サブ設定（設定内にネストされた設定）は、コンテンツフラグメントでの使用はサポートされますが、GraphQL クエリには使用できません。

1. **ツール**／**一般**&#x200B;に移動し、**設定ブラウザー**&#x200B;を開きます。

1. 「**作成**」を使用してダイアログを開き、次の操作を行います。

   1. 「**タイトル**」を指定します。
   1. 使用できるようにするには、以下を選択します。
      * **コンテンツフラグメントモデル**
      * **GraphQL の永続的なクエリ**

      ![設定の定義](assets/cfm-conf-01.png)


1. 「**作成**」を選択して、定義を保存します。

<!-- 1. Select the location appropriate to your website. -->

### アセットフォルダーへの設定の適用 {#apply-the-configuration-to-your-assets-folder}

「**グローバル**」がコンテンツフラグメント機能に対して有効になっている場合、設定はすべてのアセットフォルダーに適用されます。

他の設定（グローバル以外）を同等のアセットフォルダーで使用するには、接続を定義する必要があります。そのためには、適切なフォルダーの「**フォルダーのプロパティ**」の「**クラウドサービス**」タブで「**設定**」を適切に選択します。

![設定の適用](assets/cfm-conf-02.png)
