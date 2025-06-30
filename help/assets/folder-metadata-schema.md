---
title: フォルダーメタデータスキーマ
description: '  [!DNL Experience Manager Assets] のアセットフォルダーのメタデータスキーマを作成する方法について説明します。'
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 100%

---

# フォルダーメタデータスキーマ {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] では、フォルダープロパティページに表示されるレイアウトおよびメタデータを定義する、アセットフォルダーのメタデータスキーマを作成できます。

## フォルダーメタデータスキーマフォームの追加 {#add-a-folder-metadata-schema-form}

フォルダーメタデータスキーマフォームエディターを使用して、フォルダーのメタデータスキーマを作成および編集します。

1. [!DNL Experience Manager] のロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL フォルダーメタデータスキーマ]**&#x200B;に移動します。
1. フォルダーメタデータスキーマフォームページで、「**[!UICONTROL 作成]**」を選択します。
1. フォームの名前を指定し、「**[!UICONTROL 作成]**」を選択します。新しいスキーマフォームがスキーマフォームページにリストされます。

## フォルダーメタデータスキーマフォームの編集 {#edit-folder-metadata-schema-forms}

以下を含む、新しく追加された、または既存のメタデータスキーマフォームを編集できます。

* タブ
* タブ内のフォーム項目。

これらのフォーム項目を CRX リポジトリーのメタデータノード内のフィールドにマップしたり、フォーム項目を設定したりできます。新しいタブまたはフォーム項目をメタデータスキーマフォームに追加できます。

1. スキーマフォームページで、作成したフォームを選択し、ツールバーの「**[!UICONTROL 編集]**」アイコンを選択します。
1. フォルダーメタデータスキーマエディターページで、**[!UICONTROL +]** アイコンを選択して、フォームにタブを追加します。タブの名前を変更するには、デフォルト名をクリックし、「**[!UICONTROL 設定]**」に新しい名前を指定します。

   ![custom_tab](assets/custom_tab.png)

   さらにタブを追加するには、**[!UICONTROL +]** アイコンを選択します。**[!UICONTROL X]** を選択してタブを削除します。

1. アクティブになっているタブで、「**[!UICONTROL フォームを作成]**」タブから 1 つ以上のコンポーネントを追加します。

   ![adding_components](assets/adding_components.png)

   複数のタブを作成する場合は、特定のタブを選択して、コンポーネントを追加します。

1. コンポーネントを設定するには、コンポーネントを選択して、「**[!UICONTROL 設定]**」タブでそのプロパティを変更します。

   必要に応じて、「**[!UICONTROL 設定]**」タブからコンポーネントを削除します。

   ![configure_properties](assets/configure_properties.png)

1. ツールバーの「**[!UICONTROL 保存]**」を選択して、変更内容を保存します。

### フォームを作成するコンポーネント {#components-to-build-forms}

「**[!UICONTROL フォームを作成]**」タブには、フォルダーメタデータスキーマフォーム内で使用するフォーム項目が一覧表示されます。「**[!UICONTROL 設定]**」タブには、「**[!UICONTROL フォームを作成]**」タブで選択した各項目の属性が表示されます。以下は、「**[!UICONTROL フォームを作成]**」タブで使用可能なフォーム項目のリストです。

<table>
 <tbody>
  <tr>
   <td><p><strong>コンポーネント名</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>セクションヘッダー</p> </td>
   <td><p> 共通コンポーネントのリストに対してセクションヘッダーを追加します。</p> </td>
  </tr>
  <tr>
   <td><p>1 行のテキスト</p> </td>
   <td><p> 1 行のテキストのプロパティを追加します。これは文字列として保存されます。</p> </td>
  </tr>
  <tr>
   <td><p>複数値テキスト</p> </td>
   <td><p> 複数値テキストプロパティを追加します。これは文字列の配列として保存されます。</p> </td>
  </tr>
  <tr>
   <td><p>番号</p> </td>
   <td><p> 数値コンポーネントを追加します。</p> </td>
  </tr>
  <tr>
   <td><p>日付</p> </td>
   <td><p> 日付コンポーネントを追加します。</p> </td>
  </tr>
  <tr>
   <td><p>ドロップダウン</p> </td>
   <td><p> ドロップダウンリストを追加します。</p> </td>
  </tr>
  <tr>
   <td><p>標準タグ</p> </td>
   <td><p> タグを追加します。 </p> </td>
  </tr>
  <tr>
   <td><p>非表示のフィールド</p> </td>
   <td><p> 非表示のフィールドを追加します。このフィールドは、アセットの保存時に POST パラメーターとして送信されます。</p> </td>
  </tr>
 </tbody>
</table>

### フォーム項目の編集 {#editing-form-items}

フォーム項目のプロパティを編集するには、コンポーネントを選択し、「**[!UICONTROL 設定]**」タブで次のプロパティのすべてまたは一部を編集します。1 つのフィールドのみをメタデータスキーマの特定のプロパティにマップすることをお勧めします。それ以外の場合は、プロパティにマッピングされた最新の追加フィールドがシステムによって選択されます。

**[!UICONTROL フィールドラベル]**：フォルダーのプロパティページに表示されるメタデータプロパティの名前。

**[!UICONTROL プロパティにマッピング]**：このプロパティは、フォルダーノードが保存されている CRX リポジトリ内でのフォルダーノードの相対パスを指定します。「**/**」で始まり、パスがそのフォルダーのノードの配下にあることを示します。

プロパティの有効な値の例を次に示します。

* `./jcr:content/metadata/dc:title`：フォルダーのメタデータノードにある値を、プロパティ `dc:title` として格納します。

* `./jcr:created`:アセットの作成日時が格納されます。これは保護プロパティーです。これらのプロパティを設定する場合は、「[!UICONTROL 編集を無効にする]」とマークすることをお勧めします。

プロパティパスにスペースを含めないでください。コンポーネントがメタデータスキーマフォームに適切に表示されなくなります。

**[!UICONTROL JSON パス]**：オプションのキーと値のペアを指定する JSON ファイルのパスを指定します。

**[!UICONTROL プレースホルダー]**：このプロパティを使用して、メタデータプロパティに関連するプレースホルダーテキストを指定します。

**[!UICONTROL 選択肢]**：リストの選択肢を指定するには、このプロパティを使用します。

**[!UICONTROL 説明]**：メタデータコンポーネントの短い説明を追加するには、このプロパティを使用します。

**[!UICONTROL クラス]**：プロパティが関連付けられているオブジェクトクラス。

## フォルダーメタデータスキーマフォームを削除 {#delete-folder-metadata-schema-forms}

フォルダーメタデータスキーマフォームページから、フォルダーメタデータスキーマフォームを削除できます。フォームを削除するには、フォームを選択し、ツールバーの削除アイコンを選択します。

![delete_form](assets/delete_form.png)

## フォルダーメタデータスキーマの割り当て {#assign-a-folder-metadata-schema}

フォルダーメタデータスキーマフォームページから、またはフォルダーの作成時に、フォルダーにフォルダーメタデータスキーマを割り当てることができます。

フォルダーのメタデータスキーマを設定すると、スキーマフォームのパスは、フォルダーノードの `folderMetadataSchema` プロパティ（.*/jcr:content*.

### フォルダーメタデータスキーマページからのスキーマへの割り当て {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. [!DNL Experience Manager] のロゴを選択し、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL フォルダーメタデータスキーマ]**&#x200B;に移動します。
1. フォルダーメタデータスキーマフォームページから、フォルダーに適用するスキーマフォームを選択します。
1. ツールバーの「**[!UICONTROL フォルダーに適用]**」を選択します。

1. スキーマを適用するフォルダーを選択し、「**[!UICONTROL 適用]**」を選択します。既にフォルダーにメタデータスキーマが適用されている場合は、既存のメタデータスキーマを上書きするかどうかを確認する警告メッセージが表示されます。「**[!UICONTROL 上書き]**」を選択します。
1. メタデータスキーマを適用したフォルダーのメタデータプロパティを開きます。

   ![folder_properties](assets/folder_properties.png)

   「フォルダーメタデータ」フィールドを表示するには、「**[!UICONTROL フォルダーメタデータ]**」タブを選択します。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

### フォルダー作成時のスキーマの割り当て {#assign-a-schema-when-creating-a-folder}

フォルダーの作成時に、フォルダーメタデータスキーマを割り当てることができます。システムに 1 つ以上のフォルダーメタデータスキーマが存在する場合は、**[!UICONTROL フォルダーを作成]**&#x200B;ダイアログに追加リストが表示されます。目的のスキーマを選択できます。 デフォルトでは、スキーマは選択されていません。

1. [!DNL Experience Manager Assets] のユーザーインターフェイスで、ツールバーの「**[!UICONTROL 作成]**」を選択します。
1. フォルダーのタイトルと名前を指定します。
1. フォルダーメタデータスキーマリストで、目的のスキーマを選択します。次に、「**[!UICONTROL 作成]**」を選択します。

   ![select_schema](assets/select_schema.png)

1. メタデータスキーマを適用したフォルダーのメタデータプロパティを開きます。
1. 「フォルダーメタデータ」フィールドを表示するには、「**[!UICONTROL フォルダーメタデータ]**」タブを選択します。

## フォルダーメタデータスキーマの使用 {#use-the-folder-metadata-schema}

フォルダーメタデータスキーマが設定されたフォルダーのプロパティを開きます。フォルダープロパティページに「**[!UICONTROL フォルダーメタデータ]**」タブが表示されます。フォルダーメタデータスキーマフォームを表示するには、このタブを選択します。

各種フィールドにメタデータ値を入力し、「**[!UICONTROL 保存]**」を選択して値を保存します。指定した値は、CRX リポジトリ内のフォルダーノードに保存されます。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
