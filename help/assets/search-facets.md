---
title: 検索ファセット
description: この記事では、AEM で検索ファセットを作成、変更および使用する方法について説明します。
translation-type: tm+mt
source-git-commit: dfa9b099eaf7f0d155986bbab7d56901876d98f6

---


# Search facets {#search-facets}

AEM で検索ファセットを作成、変更および使用する方法について説明します。

Adobe Experience Manager（AEM）アセットの企業全体のデプロイメントには、多くのアセットが格納されています。AEM の一般的な検索機能だけでは、正しいアセットを見つけることが困難で時間がかかる場合があります。

フィルターパネルの検索ファセットを使用すると、より詳細な検索が可能になり、検索機能がより効率的で柔軟になります。検索ファセットは、複数のディメンション（述語）を追加するので、ユーザーはより複雑な検索を実行できます。フィルターパネルには、いくつかの標準ファセットが含まれます。カスタム検索ファセットを追加することもできます。

要約すると、検索ファセットでは、事前に決定された単一の分類順ではなく、複数の方法でアセットを検索できます。 より焦点を絞った検索のために、目的の詳細レベルまで簡単にドリルダウンできます。

例えば、画像を検索する場合、ビットマップとベクトル画像のどちらを検索するかを選択できます。画像の MIME タイプを指定して、検索の範囲をさらに絞り込むことができます。同様に、ドキュメントを検索する場合は、PDF や MS Word などの形式を指定できます。

## Add a predicate {#adding-a-predicate}

フィルターパネルに表示される検索ファセットは、述語を使用した基盤となる検索フォームで定義されます。複数のファセットを表示するには、デフォルトのフォームに述語を追加するか、選択したファセットを含むカスタムフォームを使用します。

For full-text searches, add the `Fulltext` predicate to the form. 「プロパティの述語」を使用すると、ユーザーが指定した 1 つのプロパティと一致するアセットが検索されます。「オプションの述語」を使用すると、特定のプロパティについて 1 つ以上の値と一致するアセットが検索されます。「日付の範囲の述語」を追加すると、指定した期間内に作成されたアセットが検索されます。

1. Tap/click the AEM logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. フォームの検索ページで、「アセット管理者 **[!UICONTROL 」「検索レール]**」を選択し、「 **aemassets** _editを ![編集」をタップします](assets/aemassets_edit.png)。

   ![アセット管理者の検索レールを探して選択します](assets/assets_admin_searchrail.png)

1. 検索フォームを編集ページで、「**[!UICONTROL 述語を選択]**」タブからメインウィンドウに述語をドラッグします。例えば、「**[!UICONTROL プロパティの述語]**」をドラッグします。

   ![述語をドラッグ&amp;ドロップして検索フィルターをカスタマイズ](assets/drag_predicate.png)

   述語をドラッグ&amp;ドロップして検索フィルターをカスタマイズ

1. 「設定」タブで、その述語のラベル、プレースホルダーテキストおよび説明を入力します。述語に関連付けるメタデータプロパティの有効な名前を指定します。

   「設定」タブのヘッダーラベルは、選択した述語のタイプを示します。

   ![「設定」タブを使用して、述語の必要なオプションを指定します](assets/settings.png)

   「設定」タブを使用して、述語の必要なオプションを指定します

1. In the **[!UICONTROL Property Name]** field, specify a valid name for the metadata property you want to associate with the predicate. 実行される検索に基づく名前です。例えば、`jcr:content/metadata/dc:description` や `./jcr:content/metadata/dc:description` を入力します。

   選択ダイアログから既存のノードを選択することもできます。

   ![「Property Name」フィールドでメタデータプロパティを述語に関連付けます](assets/property_settings.png)

   「Property Name」フィールドでメタデータプロパティを述語に関連付けます

1. Tap/click the **[!UICONTROL Preview]** ![preview](assets/preview.png) to generate a preview of the Filters panel as it appears after you add the predicate.
1. プレビューモードで述語のレイアウトを確認します。

   ![変更を送信する前に検索フォームをプレビューする](assets/preview-1.png)

   変更を送信する前に検索フォームをプレビューする

1. To close the preview, tap/click the **[!UICONTROL Close]** ![close](assets/do-not-localize/close_icon.png) on the upper-right corner of the preview.
1. Tap **[!UICONTROL Done]** to save the settings.
1. アセットユーザーインターフェイスの検索パネルに移動します。「Property predicate」がパネルに追加されます。
1. 検索するアセットの説明をテキストボックスに入力します。例えば、&quot;Adobe&quot; と入力します。検索を実行すると、「Adobe」に一致する説明を含むアセットが検索結果に表示されます。

## オプション述語の追加 {#adding-an-options-predicate}

オプションの述語を使用すると、フィルターパネルに複数の検索オプションを追加できます。フィルターパネルで 1 つ以上のオプションを選択して、アセットを検索できます。例えば、ファイルタイプに基づいてアセットを検索するには、検索フォームに「画像」、「マルチメディア」、「ドキュメント」、「アーカイブ」などのオプションを設定します。これらのオプションを設定した後、フィルターパネルで「画像」オプションを選択すると、GIF、JPEG、PNGなどのタイプのアセットに対して検索が実行されます。

オプションをそれぞれのプロパティにマップするには、オプション用のノード構造を作成し、「オプションの述語」の「プロパティ名」プロパティに親ノードのパスを指定します。The parent node should be of type `sling`: `OrderedFolder`. The options should be of type `nt:unstructured`. The option nodes should have the properties `jcr:title` and `value` configured.

`jcr:title` プロパティは、フィルターパネルに表示される、オプションのわかりやすい名前です。`value` フィールドは、指定されたプロパティと照合するためにクエリで使用されます。

オプションを選択すると、検索がオプションノードの `value` プロパティとその子ノード（存在する場合）に基づいて実行されます。オプションノード以下のツリー全体がトラバースされ、各子ノードの `value` プロパティが OR 演算子によって結合されて、検索クエリが作成されます。

例えば、ファイルタイプとして「画像」を選択した場合、アセットの検索クエリは OR 演算子によって `value` プロパティを結合することで作成されます。For example, the search query for images is built by combining the results matched for *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, and *image/tiff* for the property `jcr:content/metadata/dc:format` using an OR operation.

CRXDEに示すように、ファイルタイプの値プロパティは、検索クエリが機能するために使用されます

CRX リポジトリのオプションでノード構造を手動で作成する代わりに、対応するキーと値のペアを指定することで JSON ファイルでオプションを定義することもできます。Specify the path of the JSON file in the **[!UICONTROL Property Name]** field. For example, you can define the key-value pairs, `image/bmp`, `image/gif`, `image/jpeg`, and `image/png` and specify their values as shown in the following sample JSON file. In the **[!UICONTROL Property Name]** field, you can specify the CRX path for this file.

```
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

既存のノードを使用する場合は、選択ダイアログを使用して指定します。

>[!NOTE]
>
>Options述語は、説明された動作を示すプロパティ述語を含むカスタムラッパーです。 現時点で、この機能をネイティブにサポートする REST エンドポイントは存在しません。

1. Tap the AEM logo, and then go to **[!UICONTROL Tools > General > Search Forms]**.
1. From the **[!UICONTROL Search Forms]** page, select **[!UICONTROL Assets Admin Search Rail]**, then tap the Edit icon.
1. In the **[!UICONTROL Edit Search Form]** page, drag **[!UICONTROL Options Predicate]** from the **[!UICONTROL Select Predicate]** tab to the main pane.
1. In the **[!UICONTROL Settings]** tab, enter a label and a name for the property. For example, to search assets based on their format, specify a user-friendly name for the label, for example **[!UICONTROL File Type]**. Specify the property based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:format.`
1. 次のいずれかの操作をおこないます。

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * Tap ![](assets/do-not-localize/aem_assets_add_icon.png) next to the Options field to specify the display text and value for the options you want to supply in the Filters panel. To add another option, tap/click ![](assets/do-not-localize/aem_assets_add_icon.png) and repeat the step.

1. ユーザーが一度に複数のファイルタイプのオプション（例：「画像」、「ドキュメント」、「マルチメディア」、「アーカイブ」）を選択可能にするには、「**[!UICONTROL 単一の選択]**」チェックボックスをオフにします。If you select **[!UICONTROL Single Select]**, the user can select only one option for file types at a time.

   ![Options predicateで使用可能なフィールド](assets/options_predicate.png)

   Options predicateで使用可能なフィールド

1. 「**説明**」フィールドに説明を任意で入力し、「**[!UICONTROL 完了]**」をクリックします。
1. 検索パネルに移動します。「Options」述語が「 **Search** 」パネルに追加されます。 **[!UICONTROL ファイルタイプ]**&#x200B;のオプションがチェックボックスとして表示されます。

## Add a Multi Value Property predicate {#adding-a-multi-value-property-predicate}

述語を使 `Multi Value Property` 用すると、アセットで複数の値を検索できます。 AEM Assets で複数の製品の画像があり、各画像のメタデータには製品の SKU 番号が含まれているとします。この述語を利用すれば、複数の SKU 番号で製品の画像を検索できます。

1. Click the AEM logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. フォームを検索ページで、「アセット管理者 **[!UICONTROL 」「検索レール]**」を選択し、「 **aemassets** _edit ![を編集」をタップします](assets/aemassets_edit.png)。
1. In the Edit Search Form page, drag a **[!UICONTROL Multi Value Property Predicate]** from the **[!UICONTROL Select Predicate]** tab to the main pane.
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. 選択ダイアログを使用してノードを選択することもできます。
1. 「**[!UICONTROL 区切り文字サポート]**」が選択されていることを確認します。「**[!UICONTROL 入力区切り文字]**」フィールドで、それぞれの値を区切る文字を指定します。デフォルトでは、コンマが区切り文字に指定されています。別の区切り文字を指定できます。
1. In the **Description** field, enter an optional description and then tap **[!UICONTROL Done]**.
1. アセットユーザーインターフェイスのフィルターパネルに移動します。 The **[!UICONTROL Multi Value Property]** predicate is added to the panel.
1. 「複数値」フィールドに、複数の値を区切り文字で区切って検索します。述語は、指定した値とテキストが完全に一致するものを返します。

## Add a Tags predicate {#adding-a-tags-predicate}

The `Tags` predicate allows you to perform tag-based searches for assets. デフォルトでは、AEM Assetsは、指定したタグに基づいて、1つ以上の一致するタグをアセット内で検索します。 言い換えれば、検索クエリは指定したタグを用いて OR 演算を実行します。ただし、「すべてのタグに一致」オプションを使用すれば、すべての指定したタグを含むアセットを検索することも可能です。

1. Click the AEM logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]** and then tap **Edit** ![aemassets_edit](assets/aemassets_edit.png).
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. 「設定」タブで、述語のプレースホルダーテキストを入力します。 Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. または、選択ダイアログからCRXDEでノードを選択できます。
1. この述語の「ルートタグ」の「パス」プロパティを設定して、「タグ」リストに様々なタグを表示させます。
1. すべての指定したタグを含むアセットを検索するには、「**[!UICONTROL すべてのタグに一致オプションを表示]**」を選択します。

   ![Tags predicateの一般的な設定](assets/tags_predicate.png)

   Tags predicateの一般的な設定

1. In the **[!UICONTROL Description]** field, enter an optional description and then click/tap **[!UICONTROL Done]**.
1. 検索パネルに移動します。 The **[!UICONTROL Tags]** predicate is added to the Search panel.
1. アセットの検索に使用するタグを指定または表示されたリストから選択します。
1. すべての指定したタグに一致するアセットを検索するには、「**[!UICONTROL すべてに一致]**」を選択します。

## その他の述語の追加 {#adding-other-predicates}

プロパティの述語やオプションの述語の追加と同様の手順で、検索パネルにその他の次の述語を追加できます。

<table>
 <tbody>
  <tr>
   <td><p><strong>述語名</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
   <td><p><strong>プロパティ</strong></p> </td>
  </tr>
  <tr>
   <td><p>フルテキスト</p> </td>
   <td>アセットノード全体に対してフルテキスト検索を実行する検索用述語。<code>jcr</code> 次のURLにマッピングされま <code>contains</code>す。演算子を使用します。 アセットノードの特定の部分に対してフルテキスト検索を実行する場合は、相対パスを指定できます。</td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プレースホルダー</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>パス ブラウザー</td>
   <td>事前設定されたルートパスでフォルダーとサブフォルダー内のアセットを検索するための検索述語</td>
   <td>
    <ul>
     <li>プレースホルダー</li>
     <li>ルートパス</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>パス</p> </td>
   <td><p>場所で結果をフィルタリングするために使用します。オプションとして複数のパスを指定できます。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>パス</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>公開ステータス</p> </td>
   <td><p>公開ステータスに基づいてアセットを検索するための検索用述語。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>相対的な日付</p> </td>
   <td><p>アセットの相対的な作成日に基づいてアセットを検索するための検索用述語。例えば、2 ヶ月前、3 週間前などのようにオプションを設定できます。 </p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>相対的な日付</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>範囲</p> </td>
   <td><p>指定した範囲内にあるアセットを検索するための検索用述語。検索パネルで、範囲の最小値と最大値を指定できます。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日付 範囲</p> </td>
   <td><p>指定した日付プロパティの範囲内で作成されたアセットを検索するための検索用述語。検索パネルで、日付選択を使用して開始日と終了日を指定できます。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プレースホルダー</li>
     <li>プロパティ名</li>
     <li>範囲テキスト (開始)</li>
     <li>範囲テキスト (終了)</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日付</p> </td>
   <td><p>日付プロパティに基づいて、スライダーを使用してアセットを検索するための検索用述語。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>ファイルサイズ</p> </td>
   <td><p>サイズに基づいてアセットを検索するための検索用述語。スライダーベースの述語で、設定可能なノードからスライダーのオプションを選択します。デフォルトのオプションは、CRX リポジトリの /libs/dam/options/predicates/filesize で定義されています。ファイルサイズはバイト単位で示します。</p> </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>パス</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>最終変更アセット</td>
   <td>最近変更されたアセットを検索するための述語の検索 </td>
   <td>
    <ul>
     <li>プロパティ名</li>
     <li>プロパティ値</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>公開ステータス</td>
   <td>発行ステータスに基づいてアセットを検索するための検索述語 </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>評価</td>
   <td>平均評価に基づいてアセットを検索するための検索述語 </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>オプションパス</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>有効期限ステータス</td>
   <td>有効期限ステータスに基づいてアセットを検索するための検索述語 </td>
   <td>
    <ul>
     <li>ラベル</li>
     <li>プロパティ名</li>
     <li>説明</li>
    </ul> </td>
  </tr>
  <tr>
   <td>非表示</td>
   <td>非表示のフィールドプロパティを定義してアセットを検索するための検索用述語。</td>
   <td>
    <ul>
     <li>プロパティ名</li>
     <li>プロパティ値</li>
     <li>説明</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## デフォルトの検索ファセットを復元 {#restoring-default-search-facets}

By default, a Lock icon appears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page. フォームに検索ファセットを追加した場合、ロックアイコンが表示されなくなります。これはデフォルトのフォームが変更されたことを示します。

「フォームを検索」ページのオプションに対するロックアイコンは、デフォルト設定がそのままで、カスタマイズされていないことを示します。

デフォルトの検索ファセットを復元するには、次の手順を実行します。

1. Select **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.
1. ツールバ **[!UICONTROL ーで]**![](assets/do-not-localize/deleteoutline.png) 削除アイコンをタップします。
1. In the confirmation dialog, tap **[!UICONTROL Delete]** to remove the custom changes.

   After you delete the custom changes to search facets, the Lock icon reappears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.

## ユーザーの権限 {#user-permissions}

管理者の役割が割り当てられていない場合に、検索ファセットに関連する編集、削除およびプレビューアクションを実行するために必要な権限を次に示します。

<table>
 <tbody>
  <tr>
   <td><strong>アクション</strong></td>
   <td><strong>権限</strong></td>
  </tr>
  <tr>
   <td>編集 </td>
   <td>Read and Write permissions on the <code>/apps</code> node in CRX<br /> </td>
  </tr>
  <tr>
   <td>削除</td>
   <td>Read, Write, and Delete permissions on the <code>/apps</code> node in CRX</td>
  </tr>
  <tr>
   <td>プレビュー</td>
   <td>Read, Write, and Delete permissions on the <code>/var/dam/content</code> node in CRX. Also, Read and Write permissions on <code>/apps</code> node.</td>
  </tr>
 </tbody>
</table>

>[!MORELIKETHIS]
>
>* [デジタルアセットの検索](search-assets.md)

