---
title: Adobe Expressを使用したContent Hubでの画像の編集
description: Adobe Expressを使用したContent Hubでの画像の編集
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 6%

---

# Content Hubでの画像の編集 {#edit-images-content-hub}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Adobe Expressを使用したContent Hubでの画像の編集 ](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hubでは、Adobe Expressを使用して新しいコンテンツを作成できます。 使いやすいツールで既存のコンテンツを編集したり、テンプレートやブランド要素を使用してオンブランドのバリエーションを作成したり、Adobe Fireflyの最新の GenAI 機能で新しいコンテンツを作成したりできます。

## 前提条件 {#prereqs-edit-image-content-hub}

Adobe Expressにアクセスする権限および [ 新しいバリエーションにアセットを混在させる権限を持つContent Hub ユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)Content Hubを使用して画像を編集できます。

>[!NOTE]
>
[!DNL Adobe Express] を使用して、PNG およびJPG/JPEGファイルタイプの画像を編集できます。

## [!DNL Adobe Express] を使用して画像を編集する {#edit-images-using-content-hub}

Content Hubを使用して画像を編集するには：

1. 編集 **[!DNL Open in Adobe Express]** る画像のアセットカードで使用可能な「」をクリックします。 または、画像をクリックして詳細を開き、[!DNL Adobe Express] ロゴをクリックします。 その後、Content Hubを離れることなく、Adobe Express用の埋め込みエディターが読み込まれます。

   [!DNL Adobe Express] の機能を活用して、[ 画像のサイズ変更 ](https://helpx.adobe.com/express/using/resize-image.html)、[ 背景色の削除または変更 ](https://helpx.adobe.com/express/using/remove-background.html)、[ 画像の切り抜き ](https://helpx.adobe.com/express/using/crop-image.html) などのすべての画像編集関連アクションを実行したり、画像を AI 生成画像やテキストと組み合わせたりできます。

1. 変更を実行し、**[!UICONTROL 保存]** をクリックして、編集したアセットを次のいずれかの形式タイプで保存します。

   * **[!UICONTROL PNG]** （良質の画像形式として使用）
   * **[!UICONTROL JPG]** （小さいファイルに適しています）
   * **[!UICONTROL PDF]** （ドキュメントに適しています）

   ![Adobe Express を使用した画像の保存](assets/adobe-express-save-as.png)

1. アセットの名前を「**[!UICONTROL 名前を付けて保存]**」フィールドに入力します。

1. **[!UICONTROL キャンペーン名]** フィールドを使用して、アセットのキャンペーン名を指定します。 既存の名前を使用することも、新しい名前を作成することもできます。 Content Hubには、名前を入力する際に表示される追加のオプションが用意されています。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   ベストプラクティスとして、Adobeでは残りのフィールドに値を指定し、アップロードしたアセットの検索エクスペリエンスを強化することをお勧めします。

1. [ オプション ] 「**[!UICONTROL キーワード]**」、「**[!UICONTROL チャネル]**」、「**[!UICONTROL 期間]**」、「**[!UICONTROL 地域]**」フィールドの値を定義します。 キーワード、チャネル、場所別にアセットのタグ付けとグループ化を行うと、承認済みの会社コンテンツを使用するすべてのユーザーがこれらのアセットを検索し、整理しておくことができます。

1. **[!UICONTROL 新しいアセットとして保存]** をクリックして、アセットを保存します。

また、管理者は、Content Hubにアセットを追加する際に表示される必須フィールドとオプションフィールド（キャンペーン名、キーワード、チャネルなど）を設定することもできます。 詳しくは、[Content Hub ユーザーインターフェイスの設定 ](configure-content-hub-ui-options.md#configure-upload-options-content-hub) を参照してください。
