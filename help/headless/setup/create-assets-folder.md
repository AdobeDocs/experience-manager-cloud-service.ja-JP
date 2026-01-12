---
title: アセットフォルダーの作成 - ヘッドレスセットアップ
description: AEM コンテンツフラグメントモデルを使用すると、ヘッドレスコンテンツの基盤となるコンテンツフラグメントの構造を定義できます。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 95624ebf1a77dac1f535e199b660096c8efdfa76
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 81%

---

# アセットフォルダーの作成 - ヘッドレスセットアップ {#creating-an-assets-folder}

AEM コンテンツフラグメントモデルを使用すると、ヘッドレスコンテンツの基盤となるコンテンツフラグメントの構造を定義できます。コンテンツフラグメントはアセットフォルダーに保存されます。

## Assets フォルダーとは {#what-is-an-assets-folder}

今後のコンテンツフラグメントに必要な構造を定義する[コンテンツフラグメントモデルを作成](create-content-model.md)できたので、フラグメントを作成するのが楽しみかと思います。

ただし、最初にアセットフォルダーを作成して、それらを保存する必要があります。

アセットフォルダーは、コンテンツフラグメントと一緒に、画像やビデオなどの[従来のコンテンツアセットを整理する](/help/assets/manage-digital-assets.md)ために使用できます。

## Assets フォルダーの作成と設定 {#create-and-configure-an-assets-folder}

管理者は、コンテンツの作成時にフォルダーを作成してコンテンツを整理するだけで済みます。Assets コンソールを使用して新しいフォルダーを作成します。

作成したら、[ 設定 ](/help/headless/setup/create-configuration.md) をフォルダーに適用する必要があります。 詳しくは [ フォルダーへの設定の適用 ](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder) を参照してください。

作成したフォルダー内に、追加のサブフォルダーを作成できます。サブフォルダーは、親フォルダーの&#x200B;**クラウド設定**&#x200B;を継承します。別の設定モデルを使用する場合は、この設定を上書きできます。

ローカライズされたサイト構造を使用している場合は、新しいフォルダーの下に[言語ルートを作成](/help/assets/translate-assets.md)できます。

## 次の手順 {#next-steps}

コンテンツフラグメント用のフォルダーを作成したので、「はじめる前に」の 4 番目のパートに進み、[コンテンツフラグメントを作成](create-content-fragment.md)します。

>[!TIP]
>
>コンテンツフラグメントの管理について詳しくは、[コンテンツフラグメントのドキュメント](/help/sites-cloud/administering/content-fragments/overview.md)を参照してください。
