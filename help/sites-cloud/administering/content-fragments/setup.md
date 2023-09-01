---
title: コンテンツフラグメント — 設定
description: コンテンツフラグメントとGraphQL機能でAEMヘッドレス配信機能を使用する方法を説明します。
feature: Content Fragments
role: Developer, Architect
source-git-commit: 676173813b6ea4defeafe25c95be9668d32aac38
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 27%

---


# コンテンツフラグメント — 設定 {#content-fragments-setup}

Adobe Experience Manager(AEM)as a Cloud Service内のコンテンツフラグメントを使用すると、複数の場所や複数のチャネルで使用できるようにコンテンツを準備できます。 これは、ヘッドレス配信やページオーサリングに最適です。

コンテンツフラグメント機能用のインスタンスを有効にするには、次を有効にする必要があります。

* **コンテンツフラグメントモデル** - 必須

  >[!CAUTION]
  >
  >**コンテンツフラグメントモデル**&#x200B;を有効にしない場合：
  >
  >* の **作成** オプションは、モデルの作成には使用できません。
  >* [Sites 設定を選択して関連するエンドポイントを作成する](/help/headless/graphql-api/graphql-endpoint.md)ことはできません。

* **GraphQL 永続クエリ** - オプション

インスタンスの設定が完了しました。

* 作成者 [設定ブラウザーでの機能の有効化](#enable-content-fragment-functionality-configuration-browser)
* その後 [個々の Assets フォルダーへの設定の適用](#apply-the-configuration-to-your-folder)

## 設定ブラウザーでコンテンツフラグメント機能を有効にする {#enable-content-fragment-functionality-configuration-browser}

コンテンツフラグメントモデルとGraphQL永続化クエリのコンテンツフラグメント機能を使用するには、次の手順を実行します。 **必須** 最初に、 **設定ブラウザー**:

>[!NOTE]
>
>詳しくは、 [設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[下位設定](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （別の設定内にネストされた設定）は、コンテンツフラグメント、コンテンツフラグメントモデル、GraphQLクエリで使用できます。
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
   1. 作成時に、 **名前** はリポジトリ内のノード名になります。
名前を入力できます。 このフィールドを空白のままにすると、タイトルに基づいて自動的に生成され、 [AEM命名規則](/help/implementing/developing/introduction/naming-conventions.md)必要に応じて、結果を調整できます。
   1. 使用できるようにするには、以下を選択します。
      * **コンテンツフラグメントモデル**
      * **GraphQL 永続クエリ**

      ![設定の定義](assets/cf-setup-create-conf.png)

1. 「**作成**」を選択して、定義を保存します。

## フォルダーへの設定の適用 {#apply-the-configuration-to-your-folder}

設定時 **global** がコンテンツフラグメント機能に対して有効になっている場合は、この機能が適用されます。この機能は、 **Assets** コンソール。

他の設定（したがってグローバルを除く）を同等の Assets フォルダーで使用するには、接続を定義する必要があります。 これをおこなうには、 **設定** （内） **Cloud Service** タブ **フォルダーのプロパティ** 」と入力します。

![設定の適用](assets/cf-setup-apply-conf.png)
