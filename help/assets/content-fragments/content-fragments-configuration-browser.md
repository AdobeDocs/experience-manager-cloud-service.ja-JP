---
title: コンテンツフラグメント — 設定ブラウザー
description: 設定ブラウザーで特定のコンテンツフラグメント機能を有効にする方法を説明します。
translation-type: tm+mt
source-git-commit: c821baff208e563009e68f51700555ea1d516886
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 38%

---


# コンテンツフラグメント — 設定ブラウザー{#content-fragments-configuration-browser}

>[!CAUTION]
>
>AEM GraphQL API(コンテンツフラグメント配信用)は、2021年の初めにリリースされます。
>
>関連ドキュメントは、既にプレビュー目的でご利用いただけます。

## インスタンスのコンテンツフラグメント機能を有効にする{#enable-content-fragment-functionality-instance}

コンテンツフラグメントを使用する前に、**設定ブラウザー**&#x200B;を使用して以下を有効にする必要があります。

* **コンテンツフラグメントモデル**  — 必須
* **GraphQLの永続的なクエリ**  — オプション

>[!CAUTION]
>
>**コンテンツフラグメントモデル**&#x200B;を有効にしないと、新しいモデルを作成するための「**作成**」オプションを使用できません。

コンテンツフラグメント機能を有効にするには、次の操作を行う必要があります。

* 設定ブラウザーを使用して、コンテンツフラグメント機能の使用を有効にする
* アセットフォルダーへの設定の適用

### 設定ブラウザーでコンテンツフラグメント機能を有効にする{#enable-content-fragment-functionality-in-configuration-browser}

[特定のコンテンツフラグメント機能](#creating-a-content-fragment-model)を使用するには、**まず**&#x200B;設定ブラウザ&#x200B;**を使用して**&#x200B;有効にする必要があります。

>[!NOTE]
>
>詳しくは、[設定ブラウザー：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)も参照してください。

>[!CAUTION]
>
>サブ設定（設定内にネストされた設定）は、コンテンツフラグメントでの使用をサポートしていません。

1. **ツール**／**一般**&#x200B;に移動し、**設定ブラウザー**&#x200B;を開きます。

1. 「**作成**」を使用してダイアログを開き、次の操作をおこないます。

   1. 「**タイトル**」を指定します。
   1. ユーザーが使用できるようにするには、
      * **コンテンツフラグメントモデル**
      * **GraphQLの永続的なクエリ**

      ![設定の定義](assets/cfm-conf-01.png)


1. 「**作成**」を選択して、定義を保存します。

<!-- 1. Select the location appropriate to your website. -->

### アセットフォルダーへの設定の適用 {#apply-the-configuration-to-your-assets-folder}

設定&#x200B;**グローバル**&#x200B;がコンテンツフラグメント機能に対して有効になっている場合、すべてのアセットフォルダーに適用されます。

他の設定（グローバル以外）を同等のアセットフォルダーで使用するには、接続を定義する必要があります。そのためには、適切なフォルダーの「**フォルダーのプロパティ**」の「**クラウドサービス**」タブで「**設定**」を適切に選択します。

![設定の適用](assets/cfm-conf-02.png)