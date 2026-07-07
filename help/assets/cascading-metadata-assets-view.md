---
title: カスケードメタデータ
description: この記事では、アセットビューでアセットのカスケーディングメタデータを定義する方法について説明します。
feature: Metadata
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: e7c80792-f4db-4604-a51f-b20f066b2c1b
source-git-commit: bcdfc9bb418ab405faa82c55820a6ec6062c2b17
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 33%

---

# メタデータのカスケーディング Assets ビュー{#cascading-metadata-assets-view}

アセットのメタデータ情報を取得するときに、ユーザーは様々なフィールドに情報を指定します。 他のフィールドで選択されているオプションに応じて、特定のメタデータフィールドやフィールド値を表示できます。 こうした条件に応じたメタデータの表示は、カスケードメタデータと呼ばれます。 つまり、特定のメタデータフィールドや値と、1 つ以上のフィールドまたはその値（あるいはその両方）との依存関係を作成できます。

メタデータ Formsを使用して、メタデータのカスケーディングルールを定義します。 例えば、メタデータフォームにアセットタイプフィールドが含まれている場合、ユーザーが選択したアセットのタイプに基づいて、表示する関連するフィールドセットを定義できます。

次に、カスケードメタデータを定義できるいくつかの使用例を示します。

* ユーザーの所在地が必要な場合に、ユーザーが選択した国および都道府県に基づいて、関連する都市名を表示します。
* ユーザーが選択した製品カテゴリに基づいて、関連するブランド名をリストに読み込みます。
* 別のフィールドで指定された値に基づいて、特定のフィールドの表示と非表示を切り替えます。 例えば、ユーザーが別の住所への配送を希望した場合に、別の発送先住所フィールドを表示します。
* 別のフィールドに指定された値に基づいて、特定のフィールドを必須として指定します。
* 別のフィールドで指定された値に基づいて、特定のフィールドに表示されるオプションを変更します。
* 別のフィールドで指定された値に基づいて、特定のフィールドにデフォルトのメタデータ値を設定します。

## [!DNL Experience Manager] でのカスケードメタデータの設定 {#configure-cascading-metadata-in-aem}

選択されたアセットタイプに基づいて、カスケードメタデータを表示するシナリオを検討します。 例 – 

* ビデオの場合、形式やコーデック、長さなど、適用可能なフィールドを表示します。
* Word 文書や PDF ドキュメントの場合は、ページ数や作成者などのフィールドを表示します。

画像タイプに基づいてファイルを分類する例として、`Image`という名前のドロップダウンフィールドを使用しています。 ドロップダウンには、サポートされている画像拡張機能（JPG/JPEG、GIFなど）を表すオプションが含まれています。 データの一貫性を確保し、サポートされていない形式が選択または処理されないようにするには、検証ルールがこのフィールドに適用されます。 このルールは、選択したドロップダウン値を評価し、受け入れられる画像形式に沿った制約を適用します。

>[!IMPORTANT]
>
>ドロップダウンフィールドのみに基づいてルールを作成できます。

選択したアセットタイプに関係なく、著作権情報を必須フィールドとして表示します。 [定義済みのメタデータコンポーネント &#x200B;](metadata-assets-view.md#property-components)と[&#x200B; メタデータをフォルダー](metadata-assets-view.md#assign-metadata-form-folder)に割り当てることができます。

### Build Metadata Forms {#build-metadata-schema-forms}

新しいメタデータフォームを作成するには、次の手順を検討します。

1. [!DNL Experience Manager] ロゴを選択し、**[!UICONTROL Settings]** > **[!UICONTROL Metadata Forms]** > **[!UICONTROL Create]**&#x200B;に移動します。

1. 「**[!UICONTROL タイプ]**」ドロップダウンから、適切なフォームタイプ（**[!UICONTROL ファイル]**、**[!UICONTROL フォルダー]**、または&#x200B;**[!UICONTROL コレクション]**）を選択します。

1. **[!UICONTROL 名前]** フィールドにメタデータフォームのタイトルを指定します。

1. または、**[!UICONTROL 既存のフォームテンプレートから選択]** ドロップダウンから既存のメタデータフォームテンプレートを選択します。

1. 空白のメタデータフォームが表示されます。 新しいタブを追加します。

   ![&#x200B; メタデータフォーム UI](assets/metadata-form-ui.png)

   * **A:** [!UICONTROL 編集]または[!UICONTROL &#x200B; プレビュー]を切り替えます
   * **B:** [&#x200B; メタデータフォームのコンポーネント &#x200B;](metadata-assets-view.md#property-components)
   * **C:**&#x200B;他のメタデータフォームへの切り替え
   * **D:**&#x200B;新しいタブを追加
   * **E:** キャンバス
   * **F:**&#x200B;選択したコンポーネントの一般設定
   * **G:** ルール タブ
   * **H:** コンポーネントのプロパティ

このビデオでは、一連の手順（[&#x200B; メタデータ Formsの設定](https://video.tv.adobe.com/v/341275)）を確認できます。

### 既存のメタデータフォームの変更 {#modify-existing-metadata-form}

既存のメタデータフォームを変更するには、次の手順に従います。

1. 既存のメタデータフォームを開き、フォームに追加する[事前定義済みコンポーネント &#x200B;](metadata-assets-view.md#property-components)に移動し、キャンバスに要素をドロップします。

   **画像**&#x200B;の使用例に従って、画像アセットタイプを定義するドロップダウンフィールドを追加します。 **設定**&#x200B;で名前とプロパティのパスを指定し、オプションでフィールドを&#x200B;**[!UICONTROL 読み取り専用]**&#x200B;または&#x200B;**[!UICONTROL 複数選択]**&#x200B;に設定します。

1. ドロップダウンのキー値オプションは、手動で入力するか、JSON パスを指定するか、CSV ファイルを読み込むことで指定します。

   * 値を手動で指定するには、**[!UICONTROL 選択肢]**&#x200B;の下の&#x200B;**[!UICONTROL 手動で追加]**&#x200B;を選択し、`Add`をクリックして、オプションのラベルと値を指定します。 例えば、ビデオ、PDF、画像のアセットタイプを指定します。

     ![画像アセットタイプ &#x200B;](assets/image-asset-type.png)

   * JSON パスから値を取得するには、**[!UICONTROL JSON パスを使用して追加]**&#x200B;を選択し、JSON ファイルのパスを指定します。

     >[!NOTE]
     >
     >すべてのDAM編集者と作成者がアクセスできる共有場所にJSON ファイルを保存します。

     ![JSON パスを通じて選択肢を追加](assets/add-json-choices.png)

   * CSVから値を動的に取得するには、**[!UICONTROL CSVのインポート]**&#x200B;をクリックし、CSV ファイルのパスを指定します。 [!DNL Experience Manager] は、フォームがユーザーに提供されたときに、キーと値のペアをリアルタイムで取得します。

     ![CSV](assets/import-csv-choices.png)を通じて選択肢を追加

   >[!NOTE]
   > 
   >両方のオプションは相互に排他的なので、CSV ファイルからオプションを読み込んで手動で編集することはできません。

1. 画像フィールドと他のフィールドの間に依存関係を作成するには、依存フィールドを選択して「**[!UICONTROL ルール]**」タブを開きます。 各コンポーネントは、特定のルールのセットをサポートしています。 このユースケースでは、画像アセットタイプ オプションを使用してルールロジックを定義します。

   <!--![Image Asset Type Rule](assets/image-asset-type-rule.png)-->

   <!--![rule tab](assets/rule-tab.png)-->

1. **[!UICONTROL 必須]**&#x200B;で、**[!UICONTROL 新しいルール]**&#x200B;に基づいて必須オプションを選択します。 ![&#x200B; プラスアイコン &#x200B;](assets/do-not-localize/aem_assets_add_icon.png)をクリックして、新しいルールを追加します。

   ![ルール](assets/image-required-rule1.png)

   現在のユースケースでは、画像アセットのフォーマットがJPG/JPEG、PNG、GIF、TIFF、またはWEBPの場合、「アセットタイプ」フィールドが必要です。 さらに、![編集アイコン &#x200B;](assets/do-not-localize/edit.svg)をクリックしてルールを再定義するか、![削除アイコン &#x200B;](assets/do-not-localize/delete.svg)をクリックして定義されたルールを削除します。

   ![ルール](assets/image-required-rule2.png)

1. 「**[!UICONTROL 視認性]**」の下で、「**[!UICONTROL 表示可、新しいルールに基づく]**」オプションを選択します。 ![&#x200B; プラスアイコン &#x200B;](assets/do-not-localize/aem_assets_add_icon.png)をクリックして、新しいルールを追加します。

   >[!NOTE]
   >
   >**[!UICONTROL 要件]**&#x200B;条件と&#x200B;**[!UICONTROL 表示]**&#x200B;条件を互いに独立して適用できます。

   ![ルール](assets/image-visible-rule1.png)

   現在のユースケースでは、画像アセットのフォーマットがJPG/JPEG、PNG、またはGIFの場合、「アセットの種類」フィールドが表示されます。 さらに、![編集アイコン &#x200B;](assets/do-not-localize/edit.svg)をクリックしてルールを再定義するか、![削除アイコン &#x200B;](assets/do-not-localize/delete.svg)をクリックして定義されたルールを削除します。

   ![ルール](assets/image-visible-rule2.png)

1. **[!UICONTROL ルールに基づく選択肢]**&#x200B;を選択して、依存関係を作成し、ルールを定義します。 ![&#x200B; プラスアイコン &#x200B;](assets/do-not-localize/aem_assets_add_icon.png)をクリックして、新しいルールを追加します。

   ![ルール](assets/image-choices-rule1.png)

   アセットタイプ ドロップダウンのルールベースの選択肢を設定するには、ルールを作成し、依存フィールドとして「画像」を設定します。 次に、「JPG/JPEG、PNG、GIF、TIFFの画像」を選択し、「WEBPのビデオ」を選択して、各画像フォーマットの表示値を定義します。各フォーマットに対して目的の値のみがチェックされ、関連するオプションが動的に表示されるようにします。 さらに、![編集アイコン &#x200B;](assets/do-not-localize/edit.svg)をクリックしてルールを再定義するか、![削除アイコン &#x200B;](assets/do-not-localize/delete.svg)をクリックして定義されたルールを削除します。

   ![ルール](assets/image-choices-rule2.png)

1. 同様に、[!UICONTROL Asset Type] フィールドのPDFやWordなどの他のアセットと、[!UICONTROL Page Count]や[!UICONTROL Author]などのフィールドとの間に依存関係を作成する手順を繰り返します。

1. 「**[!UICONTROL 保存]**」をクリックします。 メタデータフォームをフォルダーに適用します。

1. メタデータフォームを適用したフォルダーに移動し、アセットのプロパティページを開きます。 「アセットの種類」フィールドでの選択に応じて、関連するカスケードメタデータのフィールドが表示されます。

   ![&#x200B; メタデータ フォーム出力のカスケーディング &#x200B;](assets/cascading-metadata-form-output.png)


## 次の手順 {#next-steps}

* [Assets ビューでメタデータフォームを管理するビデオを見る](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=ja)

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる


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

