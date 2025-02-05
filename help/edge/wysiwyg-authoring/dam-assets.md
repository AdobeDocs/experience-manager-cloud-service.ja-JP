---
title: Edge Delivery Servicesを使用した DAM Assetsでのページの公開
description: ページの DAM アセットがEdge Delivery Servicesにシームレスに公開されるために必要な設定について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---

# Edge Delivery Servicesを使用した DAM Assetsでのページの公開 {#dam-assets}

ページの DAM アセットがEdge Delivery Servicesにシームレスに公開されるために必要な設定について説明します。

## ユニバーサルエディター、DAM AssetsおよびEdge Delivery {#overview}

ユニバーサルエディターのコンテンツを編集する場合、もちろん、DAM からアセットを選択できます。 コンテンツをEdge Delivery Servicesに公開すると、関連する DAM コンテンツも公開されます。

このシームレスな動作を確実に行うには、AEMとEdge Delivery Servicesが公開するために DAM に適切にアクセスできる必要があります。 変更してはいけないものの一例は、次のとおりです。

* [ アセットフォルダーへのアクセスの確保 ](#accessible)
* [ 必要に応じて、アセットフォルダーに適切な設定が割り当てられていることを確認する ](#configuration)

## Assets フォルダーへのアクセスの確保 {#accessible}

AEMからEdge Delivery Servicesにページを公開する場合、[ テクニカルアカウント ](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) が使用されます。 このアカウントは、`<hash>@techacct.adobe.com` 形式の名前で、ユニバーサルエディターで作成されたページを最初に公開するたびに、AEM by Cloud Managerによって自動的にユーザーとして作成されます。

![ テクニカルアカウント ](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

このテクニカルアカウントは、コンテンツを公開するためにすべての DAM フォルダーへのアクセス権を持っている必要があります。 次のいずれかを実行できます。

* プライベート DAM フォルダーは使用しません。
* テクニカルアカウントのユーザーに DAM フォルダーへのアクセス権を付与します。

## Assets フォルダーに適切な設定が割り当てられていることの確認 {#configuration}

通常は、アセットをEdge Delivery Servicesにページと共に公開するには、テクニカルアカウントが DAM のアセットにアクセスできることを確認すれば十分です。

ただし、次の 2 つの追加のケースでは、追加の設定が必要です。

* PDFやビデオなどの画像以外のアセットを含むページをEdge Delivery Servicesに公開する場合。
* ページとは独立してEdge Delivery Servicesに画像アセットを公開する場合。

これらの両方のユースケースをサポートするには、[ 設定 ](/help/implementing/developing/introduction/configurations.md) を DAM フォルダーに割り当てる必要があります。

1. AEM オーサリング環境にログインします。
1. **サイト** で、アセットを公開するサイトまたはアセットを関連付けるサイトを選択します。
1. ツールバーの **プロパティ** をタップまたはクリックします。
1. プロパティウィンドウの「**詳細**」タブで、「**クラウド設定**」フィールドの設定をメモします。
   * これは、`/conf/<site-name>` の形式でサイトを作成すると、自動的に作成されます。
1. プロパティウィンドウで **キャンセル** をタップまたはクリックし、**Assets**/**ファイル** に移動して、DAM フォルダーを選択します。
1. ツールバーの **プロパティ** をタップまたはクリックします。
1. プロパティウィンドウの **Cloud Service** タブで、「**クラウド設定**」フィールドで、前に説明したのと同じ設定を選択します。
1. 「**保存して閉じる**」をタップまたはクリックします。
