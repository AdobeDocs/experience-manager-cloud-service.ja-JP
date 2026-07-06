---
title: 承認されたビデオにビデオスマート切り抜きを適用する
description: OpenAPI機能を備えたDynamic Mediaを使用すると、Adobe Experience Manager（AEM）でビデオアセット用のビデオスマート切り抜き出力を生成できます。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用されます。"
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%

---

# 承認されたビデオにビデオスマート切り抜きを適用する {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities]を使用すると、[!DNL Adobe Experience Manager (AEM)]でビデオアセットのビデオスマート切り抜き出力を生成できます。

ビデオスマート切り抜きビデオコンテンツを分析し、フレームを動的に調整して、様々な縦横比やデバイスをまたいで主要な被写体に焦点を当てることができます。

この機能を使用するには、ビデオアセットのメタデータスキーマを設定します。 有効にすると、ユーザーはアセットのメタデータを更新してアセットを承認することで、ビデオスマート切り抜きを適用できます。

## 始める前に {#prerequisites-for-video-smart-crops}

次の点を確認します。

* [!DNL AEM Assets as a Cloud Service] にアクセスします。
* メタデータスキーマを編集する権限。
* お使いの環境でOpenAPI機能が有効になっているDynamic Media。
* AEM Assetsで利用可能なビデオアセット。

## ビデオのスマート切り抜きを有効にする（管理者） {#enable-video-smart-crops}

ビデオスマート切り抜きを有効にするには、ビデオアセットに使用するメタデータスキーマを設定します。

次の手順を実行します。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. ビデオアセットに適用されているメタデータスキーマを開き、**[!UICONTROL 編集]**&#x200B;をクリックします。
1. メタデータスキーマエディターで、「**[!UICONTROL ビデオ]**」タブを選択します。
1. 「**[!UICONTROL フォームを作成]**」セクションから、**[!UICONTROL ドロップダウン]** コンポーネントをフォームにドラッグします。

   ![&#x200B; メタデータ スキーマに追加されたビデオ スマート切り抜きフィールドの作成](/help/assets/assets/metadata-schema-form.png)

1. 新しく追加したフィールドを選択し、**[!UICONTROL 設定]** パネルで次の設定を行います。

   * **フィールドラベル**：選択したフィールドラベルを指定します。
   * **プロパティにマッピング**：`./jcr:content/dam:applyVideoSmartCrop`

1. 「**[!UICONTROL 選択肢]**」セクションで、次の値を追加します。

   * はい→true
   * No → false

   ![&#x200B; ビデオ スマート切り抜きフィールドの作成の設定](/help/assets/assets/edit-setting1.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>環境で`dm_video` メタデータスキーマが使用されている場合は、同じ設定が`dm_video` スキーマにも適用されていることを確認してください。 これにより、すべてのビデオスキーマタイプでビデオスマート切り抜きの一貫性のある動作が保証されます。

## 承認されたビデオにビデオスマート切り抜きを適用する {#apply-video-smart-crops}

メタデータフィールドを有効にしてアセットを承認すると、ビデオスマート切り抜きをビデオアセットに適用できます。

次の手順を実行します。

1. [!DNL Assets View] で「**[!UICONTROL Assets]**」を選択し、フォルダーに移動します。
1. ビデオアセットの選択。
1. 「**[!UICONTROL プロパティ]**」をクリックします。
1. メタデータパネルで、**[!UICONTROL ビデオのスマートクロップを作成]**&#x200B;を&#x200B;**はい**&#x200B;に設定し、アセットステータスを&#x200B;**[!UICONTROL 承認済み]**&#x200B;に更新して、**[!UICONTROL 保存]**&#x200B;をクリックします。

   ![&#x200B; ビデオ スマート切り抜きが有効になっている承認済みビデオアセット &#x200B;](/help/assets/assets/assets-create-video-smartcrops1.png)

プロパティが正常に更新されると、確認メッセージが表示されます。

## ビデオのスマート切り抜き出力の表示 {#view-video-smart-crops}

ビデオスマート切り抜きが生成されたら、`/play` エンドポイントのビデオ配信リクエストに`mode=smartcrop` パラメーターを含めてレンダリングします。

* `mode=smartcrop` パラメーターを使用すると、再生中にビデオスマート切り抜きが動的に適用されます。
* Dynamic Media ビューアは、デバイスと縦横比に基づいて最適な切り抜きを自動的に選択します。
* ビデオの再生は動的に調整され、主要な被写体の焦点が合うように調整されます。


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
