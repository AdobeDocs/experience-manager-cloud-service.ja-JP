---
title: Adobe Express を使用したコンテンツハブでの画像の編集
description: Adobe Express を使用したコンテンツハブでの画像の編集
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 55%

---

# コンテンツハブでの画像の編集 {#edit-images-content-hub}

コンテンツハブを使用すると、Adobe Express を使用して新しいコンテンツを作成できます。 使いやすいツールを使用して既存のコンテンツを編集し、テンプレートとブランド要素を使用してオンブランドのバリエーションを作成し、Adobe Firefly の最新の生成 AI 機能を使用して新しいコンテンツを作成できます。

>[!VIDEO](https://video.tv.adobe.com/v/3435003/?learn=on){transcript=true}

## 前提条件 {#prereqs-edit-image-content-hub}

Adobe Express および[コンテンツハブにアクセスする権限を持ち、アセットを新しいバリエーションにリミックスする権限を持つユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)は、コンテンツハブを使用して画像を編集できます。

>[!NOTE]
>
>[!DNL Adobe Express] を使用すると、PNG および JPG／JPEG ファイルタイプの画像を編集できます。

## [!DNL Adobe Express] を使用した画像の編集 {#edit-images-using-content-hub}

コンテンツハブを使用して画像を編集するには：

1. 編集する必要がある画像のアセットカードにある「**[!DNL Open in Adobe Express]**」をクリックします。 または、画像をクリックして詳細を開き、[!DNL Adobe Express] ロゴをクリックします。 その後、コンテンツハブを離れることなく、Adobe Express の埋め込みエディターが読み込まれます。

   [!DNL Adobe Express] の機能を活用して、[画像のサイズを変更](https://helpx.adobe.com/jp/express/using/resize-image.html)、[背景色を削除または変更](https://helpx.adobe.com/jp/express/using/remove-background.html)、[画像を切り抜き](https://helpx.adobe.com/jp/express/using/crop-image.html)、AI 生成画像またはテキストと画像を結合など、画像編集に関連するすべてのアクションを実行できます。

1. 変更を実行し、「**[!UICONTROL 保存]**」をクリックして、編集したアセットを次のいずれかの形式タイプで保存します。

   * **[!UICONTROL PNG]**（高画質形式として使用）
   * **[!UICONTROL JPG]**（小さいファイルに適切）
   * **[!UICONTROL PDF]**（ドキュメントに適切）

   ![Adobe Express を使用した画像の保存](assets/adobe-express-save-as.png)

1. 「**[!UICONTROL 名前を付けて保存]**」フィールドにアセットの名前を指定します。

1. 「**[!UICONTROL キャンペーン名]**」フィールドを使用して、アセットのキャンペーン名を指定します。 既存の名前を使用するか、新しい名前を作成できます。 コンテンツハブでは、名前を入力する際にさらに多くのオプションが提供されます。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   ベストプラクティスとして、アドビでは、アップロードしたアセットの検索エクスペリエンスを強化すると共に、残りのフィールドに値を指定することをお勧めします。

1. [オプション]「**[!UICONTROL キーワード]**」、「**[!UICONTROL チャネル]**」、「**[!UICONTROL 期間]**」、「**[!UICONTROL 地域]**」の各フィールドの値を定義します。 キーワード、チャネル、場所でアセットのタグ付けとグループ化を行うと、承認済みの会社のコンテンツを使用するすべてのユーザーがこれらのアセットを見つけて整理できるようになります。

1. 「**[!UICONTROL 新しいアセットとして保存]**」をクリックして、アセットを保存します。

また、管理者は、キャンペーン名、キーワード、チャネルなど、コンテンツハブへのアセットの追加中に表示される必須フィールドとオプションフィールドを設定することもできます。 詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-upload-options-content-hub)を参照してください。

## よくある質問 {#faqs-edit-images-content-hub}

### AEM Assets Content Hubで画像を編集できるのは誰ですか？

Adobe ExpressおよびAEM Assets Content Hubへのアクセス権を持ち、新しいバリエーションにアセットを再構成する権限を持つユーザーは、AEM Assets Content Hubを使用して画像を編集できます。

### AEM Assets Content HubでAdobe Expressを使用して画像を編集するにはどうすればよいですか？

AEM Assets Content Hubで画像を編集するには、画像のアセットカードにある&#x200B;**Adobe Expressで開く**&#x200B;をクリックするか、画像の詳細を開いてAdobe Express ロゴをクリックします。 これにより、AEM Assets Content Hubに組み込まれたAdobe Expressエディターが読み込まれ、プラットフォームから離れることなく編集を行うことができます。

### Adobe Expressは、AEM Assets Content Hub内でどのような編集機能を提供しますか？

Adobe Expressは、AEM Assets Content Hub内で、画像のサイズ変更、背景色の削除や変更、画像の切り抜き、AI生成の画像やテキストとの組み合わせなど、さまざまな画像編集機能を提供します。

### AEM Assets Content Hubで編集した画像を保存できるファイル形式はどれですか？

編集済みの画像は、PNG （高品質）、JPG（小さなファイルに適しています）、またはPDF（ドキュメントに適しています）形式でAEM Assets Content Hubに保存できます。

### AEM Assets Content Hubで編集済みの画像を保存する際に、どのフィールドを入力すればよいですか？

AEM Assets Content Hubで編集した画像を保存する場合は、**別名で保存** フィールドにアセットの名前を、キャンペーン名&#x200B;**フィールドにキャンペーン名を指定する必要があります。** Adobeでは、検索性と整理性を高めるために、キーワード、チャネル、タイムフレーム、リージョンなどの追加フィールドに値を指定することをお勧めします。

### AEM Assets Content Hubで編集内容を新しいアセットとして保存できますか？

はい。編集後、**新しいアセットとして保存**&#x200B;をクリックして、変更内容を新しいアセットとしてAEM Assets Content Hubに保存できます。

### AEM Assets Content Hubにアセットをアップロードする際に、管理者はフィールドをカスタマイズできますか？

はい。管理者は、キャンペーン名、キーワード、チャネルなど、AEM Assets Content Hubにアセットを追加する際に、組織のニーズに合わせて必須またはオプションのフィールドを設定できます。 設定UIの「**インポート**」タブを使用して、フィールドを設定します。



**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

