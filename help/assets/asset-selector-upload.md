---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] のアセットセレクター'
description: アセットセレクターを使用し、アプリケーション内のアセットのメタデータとレンディションを検索および取得します。
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# アセットセレクターへのファイルおよびフォルダーのアップロード {#upload-files-folders}

| [ 検索のベストプラクティス ](/help/assets/search-best-practices.md) | [ メタデータのベストプラクティス ](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えたDynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開発者向けドキュメント ](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

ローカルファイルシステムからアセットセレクターにファイルまたはフォルダーをアップロードできます。 ローカルファイルシステムを使用してファイルをアップロードするには、通常、アセットセレクターマイクロフロントエンドアプリケーションが提供するアップロード機能を使用する必要があります。

## ローカルファイルシステムからのアセットのアップロード {#basic-upload}

アセットセレクターにアセットを追加するには、次の手順を実行します。

1. パネルビューを使用している場合は、省略記号に移動して、![ アップロードアイコン ](assets/upload-icon.svg)**[!UICONTROL アップロード]** をクリックします。 一方、モーダルビューの場合は、右上の ![ アップロードアイコン ](assets/upload-icon.svg)**[!UICONTROL アップロード]** をクリックします。 [!UICONTROL Assetsをアップロード ] 画面が表示されます。

   ![ アセットセレクターへのアセットのアップロード ](assets/upload-assets.png)

   さらに、「**[!UICONTROL ファイルまたはフォルダーをここにドラッグします]**」セクションでは、ローカルファイルシステムからアセットをドラッグするか、**[!UICONTROL 参照]** をクリックして、ローカルファイルシステムで使用可能なファイルまたはフォルダーを手動で選択できます。 アップロードに含まれるファイルのリストは、リストとして使用できます。

   ![ アセットセレクターへの基本的なアセットのアップロード ](assets/basic-upload.png)

   また、サムネールを使用して選択した画像をプレビューし、X アイコンをクリックして、リストから特定の画像を削除することもできます。 X アイコンは、画像の名前またはサイズの上にマウスを置いた場合にのみ表示されます。 また、「**[!UICONTROL すべてを削除]**」をクリックして、アップロードリストからすべての項目を削除することもできます。

1. アップロードプロセスを完了するには、「**[!UICONTROL アップロード]**」をクリックします。 アップロードしたアセットが表示されます。 設定可能なコードについては、[ 基本アップロード ](/help/assets/asset-selector-customization.md#basic-upload) を参照してください。

## メタデータを使用したアセットのアップロード {#upload-assets-with-metadata}

アセットをアプリケーションに直ちにアップロードしながら、アセットにメタデータを追加できます。 メタデータには、ビジネスの件名、製品の詳細、キャンペーンなど、様々なフィールドが含まれます。 それには、プロパティ `metadataSchema` 使用します。 プロパティについて詳しくは、[ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md) を参照 `metadataSchema` てください。

設定に必要なコードスニペットについては、[ メタデータを使用してアップロード ](/help/assets/asset-selector-customization.md#upload-with-metadata) を参照してください。

![ メタデータを使用したアセットのアップロード ](assets/upload-with-metadata.png)

1. 「**[!UICONTROL キャンペーン名]**」フィールドを使用して、アップロードする名前を定義します。 既存の名前を使用することも、新しい名前を作成することもできます。 アセットセレクターを使用すると、名前を入力する際に追加のオプションを使用できます。

   ベストプラクティスとして、Adobeでは残りのフィールドに値を指定し、アップロードしたアセットの検索エクスペリエンスを強化することをお勧めします。

1. 同様に、「**[!UICONTROL キーワード]**」、「**[!UICONTROL チャネル]**」、「**[!UICONTROL 期間]**」、「**[!UICONTROL 地域]** の各フィールドの値を定義します。 キーワード、チャネル、場所別にアセットのタグ付けとグループ化を行うと、承認済みの会社コンテンツを使用するすべてのユーザーがこれらのアセットを検索し、整理しておくことができます。

1. **[!UICONTROL アップロード]** をクリックして、アセットセレクターにアセットをアップロードします。 [!UICONTROL  詳細を確認 ] 確認ボックスが表示されます。 「[!UICONTROL 続行]」をクリックします。

1. Assetsがアップロードを開始します。 [!UICONTROL  新規アップロード ] をクリックして、アップロード手順を再開します。 「[!UICONTROL  完了 ]」をクリックしてアップロードを完了します。


## カスタマイズされたアップロード {#customize-upload}

アセットセレクターを使用すると、カスタマイズされたアップロードフォームを追加できます。 複数のカスタマイズを使用できます。 例えば、[hideUploadButton](/help/assets/asset-selector-properties.md) プロパティを使用すると、アプリケーションでデフォルトに表示されるアップロードボタンを非表示にできます。 代わりに、要件に応じて MFE アプリケーションの外部でレンダリングするようにカスタマイズできます。 設定については、[ カスタマイズされたアップロード ](/help/assets/asset-selector-customization.md#customized-upload) を参照してください。

![ カスタマイズされたアップロード ](assets/customized-upload.png)

>[!MORELIKETHIS]
>
>* [ アセットセレクターの例 ](/help/assets/asset-selector-examples.md)
>* [ アセットセレクターと様々なアプリケーションの統合 ](/help/assets/integrate-asset-selector.md)
>* [ アセットセレクターのプロパティ ](/help/assets/asset-selector-properties.md)
