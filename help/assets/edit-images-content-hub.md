---
title: Adobe Express を使用したコンテンツハブでの画像の編集
description: Adobe Express を使用したコンテンツハブでの画像の編集
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 93%

---

# コンテンツハブでの画像の編集 {#edit-images-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

![Adobe Express を使用したコンテンツハブでの画像の編集](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コンテンツハブを使用すると、Adobe Express を使用して新しいコンテンツを作成できます。使いやすいツールを使用して既存のコンテンツを編集し、テンプレートとブランド要素を使用してオンブランドのバリエーションを作成し、Adobe Firefly の最新の生成 AI 機能を使用して新しいコンテンツを作成できます。

## 前提条件 {#prereqs-edit-image-content-hub}

Adobe Express および[コンテンツハブにアクセスする権限を持ち、アセットを新しいバリエーションにリミックスする権限を持つユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)は、コンテンツハブを使用して画像を編集できます。

>[!NOTE]
>
>[!DNL Adobe Express] を使用すると、PNG および JPG／JPEG ファイルタイプの画像を編集できます。

## [!DNL Adobe Express] を使用した画像の編集 {#edit-images-using-content-hub}

コンテンツハブを使用して画像を編集するには：

1. 編集する必要がある画像のアセットカードにある「**[!DNL Open in Adobe Express]**」をクリックします。または、画像をクリックして詳細を開き、[!DNL Adobe Express] ロゴをクリックします。その後、コンテンツハブを離れることなく、Adobe Express の埋め込みエディターが読み込まれます。

   [!DNL Adobe Express] の機能を活用して、[画像のサイズを変更](https://helpx.adobe.com/jp/express/using/resize-image.html)、[背景色を削除または変更](https://helpx.adobe.com/jp/express/using/remove-background.html)、[画像を切り抜き](https://helpx.adobe.com/jp/express/using/crop-image.html)、AI 生成画像またはテキストと画像を結合など、画像編集に関連するすべてのアクションを実行できます。

1. 変更を実行し、「**[!UICONTROL 保存]**」をクリックして、編集したアセットを次のいずれかの形式タイプで保存します。

   * **[!UICONTROL PNG]**（高画質形式として使用）
   * **[!UICONTROL JPG]**（小さいファイルに適切）
   * **[!UICONTROL PDF]**（ドキュメントに適切）

   ![Adobe Express を使用した画像の保存](assets/adobe-express-save-as.png)

1. 「**[!UICONTROL 名前を付けて保存]**」フィールドにアセットの名前を指定します。

1. 「**[!UICONTROL キャンペーン名]**」フィールドを使用して、アセットのキャンペーン名を指定します。既存の名前を使用するか、新しい名前を作成できます。コンテンツハブでは、名前を入力する際にさらに多くのオプションが提供されます。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   ベストプラクティスとして、アドビでは、アップロードしたアセットの検索エクスペリエンスを強化すると共に、残りのフィールドに値を指定することをお勧めします。

1. [オプション]「**[!UICONTROL キーワード]**」、「**[!UICONTROL チャネル]**」、「**[!UICONTROL 期間]**」、「**[!UICONTROL 地域]**」の各フィールドの値を定義します。キーワード、チャネル、場所でアセットのタグ付けとグループ化を行うと、承認済みの会社のコンテンツを使用するすべてのユーザーがこれらのアセットを見つけて整理できるようになります。

1. 「**[!UICONTROL 新しいアセットとして保存]**」をクリックして、アセットを保存します。

また、管理者は、キャンペーン名、キーワード、チャネルなど、コンテンツハブへのアセットの追加中に表示される必須フィールドとオプションフィールドを設定することもできます。詳しくは、[コンテンツハブユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-upload-options-content-hub)を参照してください。
