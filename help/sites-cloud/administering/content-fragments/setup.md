---
title: コンテンツフラグメント - 設定
description: コンテンツフラグメントと GraphQL、AEM ヘッドレス配信機能およびページオーサリングで使用する機能を有効にする方法について説明します。
feature: Content Fragments
role: Developer
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: b3e1d3a3770531728d696be125f074881f179573
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 97%

---

# コンテンツフラグメント - 設定 {#content-fragments-setup}

Adobe Experience Manager（AEM）as a Cloud Service 内のコンテンツフラグメントを使用すると、複数の場所や複数のチャネルで使用できるコンテンツを準備できます。これは、ヘッドレス配信やページオーサリングに最適です。

コンテンツフラグメント機能用のインスタンスを有効にするには、次を有効にする必要があります。

* **コンテンツフラグメントモデル** - 必須

  >[!CAUTION]
  >
  >**コンテンツフラグメントモデル**&#x200B;を有効にしない場合：
  >
  >* 「**作成**」オプションは、モデルの作成には使用できません。
  >* [Sites 設定を選択して関連するエンドポイントを作成する](/help/headless/graphql-api/graphql-endpoint.md)ことはできません。

* **GraphQL 永続クエリ** - オプション

インスタンスの設定を完了させるには、次の操作を実行します。

* [設定ブラウザーで機能を有効にする](#enable-content-fragment-functionality-configuration-browser)
* [個々の Assets フォルダーに設定を適用する](#apply-the-configuration-to-your-folder)

>[!TIP]
>
>コンテンツフラグメントは [Edge Delivery Servicesに公開 &#x200B;](https://www.aem.live/developer/content-fragment-overlay) できます。

## 設定ブラウザーでコンテンツフラグメント機能を有効にする {#enable-content-fragment-functionality-configuration-browser}

コンテンツフラグメントモデルと GraphQL 永続クエリのコンテンツフラグメント機能を使用するには、まず&#x200B;**設定ブラウザー**&#x200B;で有効にする&#x200B;**必要**&#x200B;があります。

>[!NOTE]
>
>詳しくは、[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)を参照してください。

>[!NOTE]
>
>[サブ設定](/help/implementing/developing/introduction/configurations.md#configuration-resolution)（別の設定内にネストされた設定）は、コンテンツフラグメント、コンテンツフラグメントモデルおよび GraphQL クエリでの使用が完全にサポートされています。
>
>注意：
>
>* サブ設定でモデルを作成した後は、モデルを別のサブ設定に移動またはコピーすることはできません。
>
>* GraphQL エンドポイントは（引き続き）親（ルート）設定に基づいています。
>
>* 永続クエリは（引き続き）親（ルート）設定に関連して保存されます。

1. **ツール**／**一般**&#x200B;に移動し、**設定ブラウザー**&#x200B;を開きます。

1. 「**作成**」を使用してダイアログを開き、次の操作を行います。

   1. 「**タイトル**」を指定します。
   1. 作成時に、**名前**&#x200B;はリポジトリ内のノード名になります。
名前を入力できます。フィールドを空白のままにすると、タイトルに基づいて自動的に名前が生成された後、[AEM 命名規則](/help/implementing/developing/introduction/naming-conventions.md)に従って調整されます。必要に応じて結果を調整できます。
   1. 使用できるようにするには、以下を選択します。
      * **コンテンツフラグメントモデル**
      * **GraphQL 永続クエリ**

      ![設定の定義](assets/cf-setup-create-conf.png)

1. 「**作成**」を選択して、定義を保存します。

## フォルダーへの設定の適用 {#apply-the-configuration-to-your-folder}

**グローバル**&#x200B;設定がコンテンツフラグメント機能に対して有効になっている場合、これは任意のアセットフォルダー（**Assets** コンソールからアクセス可）に適用されます。

他の設定（グローバル以外）を同等のアセットフォルダーで使用するには、接続を定義する必要があります。そのためには、適切なフォルダーの「**フォルダーのプロパティ**」の「**クラウドサービス**」タブで、適切な&#x200B;**設定**&#x200B;を選択します。

![設定を適用](assets/cf-setup-apply-conf.png)
