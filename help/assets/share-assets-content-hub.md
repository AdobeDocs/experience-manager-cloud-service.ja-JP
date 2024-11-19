---
title: Assetsを  [!DNL the Content Hub] で共有
description: Assetsを  [!DNL the Content Hub] で共有
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 6%

---

# コンテンツハブでのアセットの共有 {#search-assets-as-a-link}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![ アセットを共有のバナー画像 ](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

リンクによるアセットの共有は、[!DNL the Content Hub] ユーザーがリソースを利用できるようにする便利な方法です。 この機能を使用すると、権限のあるユーザーは、共有されているアセットにアクセスしてダウンロードできます。 共有リンクからアセットをダウンロードする場合、[!DNL the Content Hub] では、より高速で中断のないダウンロードを提供する非同期サービスを使用します。

## 前提条件 {#prerequisites}

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) は、この記事で説明されるアクションを実行できます。

## 単一アセットの共有 {#share-a-single-asset}

次の手順を実行することで、1 つのアセットを共有できます。

1. アセットを選択し、![ 共有アイコン ](assets/share.svg) アイコンをクリックしてアセットを共有します。

   ![ 単一アセットの共有 ](assets/sharing-single-asset.png)

1. 「**[!UICONTROL 有効期限]**」フィールドを使用して、リンクの有効期限を指定します。 24 時間、1 週間、30 日、90 日、1 年など、使用可能なオプションの 1 つを選択するか、カスタムの日付を指定します。

1. **[!UICONTROL 共有リンクをコピー]** をクリックします。 コピーしたリンクは受信者と共有できます。

## 複数アセットの共有 {#share-multiple-assets}

共有リンク [!DNL The Content Hub] 使用して複数のアセットを共有できます。 次の手順を実行します。

1. 承認済み受信者と共有する必要があるアセットを選択します。 複数のアセットを 1 つずつ選択することも、**[!UICONTROL すべてを選択]** をクリックして使用可能なすべてのアセットを一度に選択することもできます。 **[!UICONTROL すべてを選択]** オプションは、少なくとも 1 つのアセットを選択した場合にのみ表示されます。

1. ![ 共有アイコン ](assets/share.svg) アイコンをクリックします。

   ![ 複数アセットの共有 ](assets/sharing-multiple-assets.png)

1. 「プレビュー」セクションでは、必要に応じてアセットを削除することもできます。 「**[!UICONTROL 有効期限]**」フィールドを使用して、リンクの有効期限を指定します。 24 時間、1 週間、30 日、90 日、1 年など、使用可能なオプションの 1 つを選択するか、カスタムの日付を指定します。

1. **[!UICONTROL 共有リンクをコピー]** をクリックします。 コピーしたリンクは受信者と共有できます。

## アセットのプレビューと共有 {#preview-assets}

リンク受信者と共有する前に、共有するデジタルアセットの外観をプレビューして確認できます。 プレビューするアセットをクリックします。 [!DNL Content Hub] に [ アセットの詳細表示 ](asset-properties-content-hub.md) が表示されます。

![ 共有アイコン ](assets/share.svg) アイコンをクリックして、アセットを共有します。 「**[!UICONTROL 有効期限]**」フィールドを使用して、リンクの有効期限を指定します。 24 時間、1 週間、30 日、90 日、1 年など、使用可能なオプションの 1 つを選択するか、カスタムの日付を指定します。 **[!UICONTROL 共有リンクをコピー]** をクリックします。 コピーしたリンクは受信者と共有できます。

![Content Hubでのアセットのプレビュー ](assets/preview-assets-content-hub.png)

## 共有アセットにアクセス {#access-shared-assets}

アセットのリンクを共有した後、認証済み受信者は、リンクをクリックし、web ブラウザーで共有アセットをプレビューまたはダウンロードできます。

共有リンクをクリックし、アセットカードにあるダウンロードアイコンをクリックして、アセットをダウンロードします。  複数のアセットを選択して、「**[!UICONTROL ダウンロード]**」をクリックすることもできます。<!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub] は、各アセットを 1 つずつローカルファイルシステムにダウンロードします。

![ 共有リンクへのアクセス ](assets/content-hub-access-shared-links.png)
