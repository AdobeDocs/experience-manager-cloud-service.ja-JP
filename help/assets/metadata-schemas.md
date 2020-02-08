---
title: メタデータのスキーマ
description: メタデータスキーマを使用することで、プロパティページのレイアウトと、アセットに関して表示されるメタデータプロパティを定義します。カスタムメタデータスキーマを作成する方法、メタデータスキーマを編集する方法およびメタデータスキーマをアセットに適用する方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# メタデータスキーマ {#metadata-schemas}

Adobe Experience Manager(AEM)Assetsでは、メタデータスキーマは、特定のスキーマを使用するアセットに対して表示されるプロパティページのレイアウトとメタデータプロパティを定義します。 メタデータプロパティには、タイトル、説明、MIME タイプなどが含まれます。

メタデータスキーマフォームエディターを使用して、既存のスキーマを変更したり、カスタムメタデータスキーマを追加したりできます。

1. アセットのプロパティページを表示するには、カード表示のアセットタイル上のクイックアクションで&#x200B;**[!UICONTROL プロパティを表示]**&#x200B;アイコンをクリックまたはタップします。Alternatively, select the asset in the UI and then click or tap the **[!UICONTROL Properties]** icon from the toolbar.
1. 様々なタブで様々なメタデータプロパティを編集します。 ただし、プロパティページではアセットタイプを変更できません。アセットの MIME タイプを変更するには、カスタムメタデータスキーマフォームを使用するか、既存のフォームを変更します。詳しくは、[メタデータスキーマフォームの編集](#edit-metadata-schema-forms)を参照してください。特定の MIME タイプのメタデータスキーマを変更すると、現在の MIME タイプのアセットおよびすべてのアセットサブタイプのプロパティページのレイアウトが変更されます。For example, modifying a jpeg schema under `default/image` only modifies the metadata layout (asset properties) for assets with MIME type `image/jpeg`. ただし、デフォルトスキーマを編集する場合は、すべてのタイプのアセットのメタデータのレイアウトを変更します。

1. To view a list of forms/templates, click the AEM logo and then navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
AEM では次のテンプレートが用意されています。

   * **デフォルト**：アセットのメタデータスキーマの基本フォームです。
   次の子フォームは、デフォルトフォームのプロパティを継承します。i. **image**:MIMEタイプが「image」のアセット（、など）のスキ `image/jpeg`ーマ `image/png`フォームです。
「image」フォームには、次の子フォームテンプレートが含まれます。a. **jpeg**:サブタイプを持つアセットのスキーマフォー `jpeg`ム。
b. **tiff**: Schema form for the assets with sub type `tiff`.

   ii.**application**:MIMEタイプを持つアセットのスキ `application`ーマフォーム( `application/pdf`例：、 `application/zip`など)。
a. **pdf**: Schema form for assets with sub type `pdf`.

   iii. **ビデオ**:MIMEタイプを持つアセットのスキ `video`ーマフォ `video/avi`ーム( `video/mp4`、など)。

   * **コレクション**:コレクションのスキーマフォーム。
   * **** contentfragment:コンテンツフラグメントのスキーマフォーム


>[!NOTE]
>
>スキーマフォームの子フォームを表示するには、スキーマフォーム名をクリックまたはタップします。

## メタデータスキーマフォームの追加 {#add-a-metadata-schema-form}

1. To add a custom template to the list, click **[!UICONTROL Create]** from the toolbar.

   >[!NOTE]
   >
   >未編集のテンプレートの前には、鍵のアイコンが付いています。テンプレートをカスタマイズすると、テンプレートの前のロックアイコンが消えます。

1. In the dialog, enter the title of the Schema form, and then click **[!UICONTROL Create]** to complete the form creation process.

## メタデータスキーマフォームの編集 {#edit-metadata-schema-forms}

新しく追加したメタデータスキーマフォームまたは既存のメタデータスキーマフォームを編集できます。メタデータスキーマフォームには、以下の要素が含まれています。

* タブ
* タブ内のフォーム項目

これらのフォーム項目を CRX リポジトリのメタデータノード内のフィールドにマップしたり、フォーム項目を設定したりできます。

新しいタブまたはフォーム項目をメタデータスキーマフォームに追加できます。親から派生したタブとフォームアイテムはロック状態です。 子レベルではこれらを変更できません。

1. In the Schema Forms page, select the check box before a form and then click the **Edit icon** on the toolbar.
1. In the **[!UICONTROL Metadata Schema Editor]** page, customize the properties page of the asset by dragging one or more components from the list of component types in the **[!UICONTROL Build Form]** tab to the **[!UICONTROL Basic]** tab.
1. コンポーネントを設定するには、コンポーネントを選択して、「**設定**」タブでそのプロパティを変更します。

### 「フォームを作成」タブ内のコンポーネント{#components-within-the-build-form-tab}

The **[!UICONTROL Build Form]** tab lists form items that you use in your schema form. 「**[!UICONTROL 設定]**」タブに、「**[!UICONTROL フォームを作成]**」タブで選択した各項目の属性が表示されます。「**[!UICONTROL フォームを作成]**」タブで使用できるフォーム項目を次の表に示します。

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント名</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>セクションヘッダー</td>
   <td>共通コンポーネントのリストに対してセクションヘッダーを追加します。</td>
  </tr>
  <tr>
   <td>1 行のテキスト</td>
   <td>1 行のテキストプロパティを追加します。これは文字列として保存されます。</td>
  </tr>
  <tr>
   <td>複数値テキスト</td>
   <td>複数値テキストプロパティを追加します。これは文字列の配列として保存されます。</td>
  </tr>
  <tr>
   <td>番号</td>
   <td>数値コンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>日付</td>
   <td>日付コンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>ドロップダウン</td>
   <td>ドロップダウンリストを追加します。</td>
  </tr>
  <tr>
   <td>標準タグ</td>
   <td>タグを追加します。 </td>
  </tr>
  <tr>
   <td>スマートタグ</td>
   <td>メタデータタグを自動的に追加して、検索機能を強化します。<br /> </td>
  </tr>
  <tr>
   <td>非表示のフィールド</td>
   <td>非表示のフィールドを追加します。このフィールドは、アセットの保存時に POST パラメーターとして送信されます。</td>
  </tr>
  <tr>
   <td>アセットの参照元</td>
   <td>このアセットが参照しているアセットのリストを表示するには、このコンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>アセットの参照</td>
   <td>このアセットを参照しているアセットのリストを表示するには、このコンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>製品リファレンス</td>
   <td>このアセットとリンクされている製品のリストを表示するには、このコンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>アセット評価</td>
   <td>アセットを評価するオプションを表示するには、このコンポーネントを追加します。</td>
  </tr>
  <tr>
   <td>コンテキストメタデータ</td>
   <td>アセットのプロパティページにある他のメタデータタブの表示を制御するために追加します。</td>
  </tr>
 </tbody>
</table>

#### メタデータコンポーネントの編集 {#edit-the-metadata-component}

フォームのメタデータコンポーネントのプロパティを編集するには、コンポーネントをクリックし、「**[!UICONTROL 設定]**」タブで次のすべてのプロパティまたはサブセットを編集します。

**フィールドラベル**:アセットのプロパティページに表示されるメタデータプロパティの名前。

**プロパティにマッピング**：このプロパティには、CRX リポジトリ内の保存先のアセットノードへの相対パスまたは名前を指定します。It starts with `./` because indicating that the path is under the asset&#39;s node.

このプロパティの有効な値は次のとおりです。

* にあることで画像コンポーネントに問題が生じる。`/jcr:content/metadata/dc:title`:アセットのメタデータノードにプロパティとして値を格納します `dc:title`。

* にあることで画像コンポーネントに問題が生じる。`/jcr:created`:アセットのノードにjcrプロパティを表示します。 表示プロパティ上でこれらのプロパティを設定する場合は、これらのプロパティは保護されているので、「編集を無効にする」としてマークすることをお勧めします。そうしない場合、アセットのプロパティを保存したときに、「アセットの変更に失敗しました」というエラーが発生します。

コンポーネントがメタデータスキーマフォームに適切に表示されるように、プロパティのパスにはスペースを含めないでください。

**プレースホルダー**：このプロパティを使用して、メタデータプロパティに関連するプレースホルダーテキストを指定します。

**必須**：プロパティページでメタデータプロパティを必須としてマークするには、このプロパティを使用します。

**編集を無効にする**:このプロパティを使用して、メタデータプロパティをプロパティページで編集できないようにします。

**空白のフィールドを読み取り専用として表示**：プロパティページでメタデータプロパティに値がなくても表示するには、このプロパティをオンにします。デフォルトでは、メタデータプロパティに値がない場合、プロパティページには表示されません。

**順序付きリストを表示**:このプロパティを使用して、選択肢の順番付きリストを表示します

**選択肢**：リストの選択肢を指定するには、このプロパティを使用します。

**説明**：メタデータコンポーネントの短い説明を追加するには、このプロパティを使用します。

**クラス**：プロパティに関連付けられているオブジェクトクラス。

**削除**:をクリックして、スキーマフォームからコンポーネントを削除します。

>[!NOTE]
>
>非表示のフィールドコンポーネントには、これらの属性は含まれていません。代わりに、属性の名前、値、フィールドラベル、説明などのプロパティが含まれています。非表示のフィールドコンポーネントの値は、アセットの保存時に常に POST パラメーターとして送信されます。この値は、アセットのメタデータとして保存されません。

「**[!UICONTROL 必須]**」オプションを選択した場合、必須のメタデータが設定されていないアセットを検索できます。**[!UICONTROL フィルター]**&#x200B;パネルで、「**[!UICONTROL メタデータの検証]**」述語を展開して、「**[!UICONTROL 無効]**」オプションを選択します。検索結果に、スキーマフォームで設定した必須のメタデータが設定されていないアセットが表示されます。

スキーマフォームのいずれかのタブにコンテキストメタデータコンポーネントを追加した場合、コンポーネントは、その特定のスキーマが適用されているアセットのプロパティページに  スキーマが適用されます。 このリストには、Contextual Metadataコンポーネントを適用したタブを除く他のすべてのタブが含まれます。 現在、この機能は、コンテキストに応じてメタデータの表示を制御する基本的な機能を提供しています。

コンテキストメタデータコンポーネントが適用されているタブに加えて、プロパティページの任意のタブを組み込むには、リストからタブを選択します。タブがプロパティページに追加されます。

### Specify properties in JSON file {#specify-properties-in-json-file}

「**[!UICONTROL 設定]**」タブのオプションでプロパティを指定する代わりに、対応するキーと値のペアを指定することで JSON ファイルでオプションを定義できます。Specify the path of the JSON file in the **[!UICONTROL JSON Path]** field.

#### Add and delete a tab in the schema form {#add-delete-a-tab-in-the-schema-form}

スキーマエディターで、タブを追加または削除できます。The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs, by default.

Click `+` to add a new tab on a schema form. By default, the new tab has the name `Unnamed-1`. You can modify the name from the **[!UICONTROL Settings]** tab. Click `X` to delete a tab.

## メタデータスキーマフォームの削除 {#deleting-metadata-schema-forms}

AEM では、カスタムのスキーマフォームのみを削除できます。デフォルトのスキーマフォームまたはテンプレートを削除することはできません。ただし、これらのフォームでのカスタムの変更内容は削除できます。

フォームを削除するには、フォームを選択し、削除アイコンをクリックします。

>[!NOTE]
>
>デフォルトのフォームに対するカスタム変更を削除すると、メタデータスキーマインターフェイス上で、その前にロックアイコンが再び表示され、フォームがデフォルトの状態に戻ったことを示します。

>[!NOTE]
>
>AEM Assets の既製のメタデータスキーマフォームは削除できません。

## MIME タイプ用のスキーマフォーム {#schema-forms-for-mime-types}

AEM Assets には、様々な MIME タイプですぐに使用できるデフォルトのフォームが用意されています。ただし、様々な MIME タイプのアセットにカスタムのフォームを追加することができます。

### MIME タイプ用の新しいフォームの追加 {#adding-new-forms-for-mime-types}

適切なフォームタイプに新規フォームを作成します。例えば、**image/png** サブタイプの新しいテンプレートを追加するには、「image」フォームの下にフォームを作成します。スキーマフォームのタイトルはサブタイプ名です。この場合、タイトルは「png **」です。**

#### 様々な MIME タイプ用の既存のスキーマテンプレートの使用 {#using-an-existing-schema-template-for-various-mime-types}

別のMIMEタイプに対して既存のテンプレートを使用できます。 例えば、MIMEタイプのアセ `image/jpeg` ットに対してフォームを使用しま `image/png`す。

この場合は、CRX リポジトリ内の `/etc/dam/metadataeditor/mimetypemappings` に新しいノードを作成します。そのノードの名前を指定し、次のプロパティを定義します。

| **名前** | **説明** | **種類** | **値** |
|---|---|---|---|
| `exposedmimetype` | マッピングする既存のフォームの名前 | 文字列 | `image/jpeg` |
| `mimetypes` | List of MIME types that use the form defined in the `exposedmimetype` attribute | 文字列 | `image/png` |

AEM Assets では、次の MIME タイプとスキーマフォームがマッピングされます。

| スキーマフォーム | MIME タイプ |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## メタデータスキーマへのアクセス権の付与 {#granting-access-to-metadata-schemas}

メタデータスキーマ機能は、管理者のみが使用できます。ただし、管理者は一部の権限を変更して、管理者以外のユーザーにアクセス権を付与することができます。The non administrator should have create, modify, and delete permissions on the `/conf` folder.

## フォルダー固有のメタデータの適用 {#applying-folder-specific-metadata}

AEM Assets では、メタデータスキーマのバリアントを定義して、それを特定のフォルダーに適用できます。

例えば、デフォルトのメタデータスキーマのバリアントを定義して、それをフォルダーに適用できます。変更したスキーマを適用すると、フォルダー内のアセットに適用されている元のデフォルトのメタデータスキーマがオーバーライドされます。

このスキーマが適用されているフォルダーにアップロードされたアセットのみが、バリアントのメタデータスキーマに定義されている変更されたメタデータに従います。

元のスキーマが適用されている他のフォルダーのアセットは、引き続き元のスキーマに定義されているメタデータに従います。

アセットごとのメタデータの継承は、階層の第 1 レベルのフォルダーに適用されているスキーマに基づきます。言い換えると、フォルダーにサブフォルダーがない場合、そのフォルダー内のアセットはそのフォルダーに適用されているスキーマからメタデータを継承します。

フォルダーにサブフォルダーがあり、サブフォルダーレベルで別のスキーマが適用されている場合、そのサブフォルダー内のアセットはそのサブフォルダーレベルで適用されているスキーマからメタデータを継承します。ただし、サブフォルダーレベルにスキーマが適用されていない、または同じスキーマが適用されている場合、サブフォルダーのアセットは親フォルダーレベルに適用されているスキーマからメタデータを継承します。

1. Click the AEM logo and then navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. The **[!UICONTROL Metadata Schema Forms]** page is displayed.
1. デフォルトのメタデータフォームなど、フォームの前にあるチェックボックスを選択し、コピーアイコンをクリックまたはタップして、カスタムフォームとして保存します。 Specify a custom name for the form, for example `my_default`. カスタムフォームを作成することもできます。

1. In the **[!UICONTROL Metadata Schema Forms]** page, select the `my_default` form, and then click the **[!UICONTROL Edit]** icon.
1. In the **[!UICONTROL Metadata Schema Editor]** page, add a text field to the schema form. For example add a field with the label **[!UICONTROL Category]**.
1. 「**[!UICONTROL 保存]**」をクリックします。変更されたフォームは&#x200B;**[!UICONTROL メタデータスキーマフォーム]**&#x200B;ページにリストされます。
1. ツールバーの「**[!UICONTROL フォルダーに適用]**」をクリックまたはタップしてカスタムメタデータをフォルダーに適用します。
1. Select the folder on which to apply the modified schema and then click/tap **[!UICONTROL Apply]**.
1. フォルダーに他のメタデータが適用されている場合は、既存のメタデータスキーマを上書きする旨の警告メッセージが表示されます。Click **Overwrite**.
1. Click **OK** to close the success message.
1. 変更したメタデータスキーマを適用したフォルダーに移動します。

## 必須のメタデータの定義 {#defining-mandatory-metadata}

必須フィールドをフォルダーレベルで定義すると、そのフォルダーにアップロードされるアセットに強制的に適用されます。以前に定義した必須フィールドにメタデータが指定されていないアセットをアップロードすると、アセットに指定されていないメタデータをカード表示で視覚的に確認できます。

>[!NOTE]
>
>メタデータフィールドは、別のフィールドの値に基づいて、必須フィールドとして定義できます。AEM のカード表示では、このような必須メタデータフィールドのメタデータがなくても警告メッセージは表示されません。

1. Click the AEM logo and then navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. The **[!UICONTROL Metadata Schema Forms]** page is displayed.
1. デフォルトのメタデータフォームをカスタムフォームとして保存します。For example, save it as `my_default`.
1. カスタムフォームを編集します。必須フィールドを追加します。For example, add a **[!UICONTROL Category]** field and make the field mandatory.
1. 「**[!UICONTROL 保存]**」をクリックします。変更されたフォームは&#x200B;**[!UICONTROL メタデータスキーマフォーム]**&#x200B;ページにリストされます。フォームを選択し、ツールバーの「**[!UICONTROL フォルダーに適用]**」をクリックまたはタップしてカスタムメタデータをフォルダーに適用します。
1. フォルダーに移動し、カスタムフォームに追加した必須フィールドにメタデータが指定されていないアセットをアップロードします。必須フィールドの指定されていないメタデータに関するメッセージが、アセットのカード表示に表示されます。
1. （オプション）アクセス `https://[server]:[port]/system/console/components/`。 Configure and enable `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` component that is disabled by default. AEM がアセット上にあるメタデータの妥当性をチェックする頻度を設定します。

   This configuration adds a property `hasValidMetadata` to `jcr:content` of assets. AEM はこのプロパティを使用して検索の結果をフィルターできます。

   >[!NOTE]
   >
   >If an asset is added after the scheduled check, the asset is not flagged with `hasValidMetadata` until the next scheduled check. アセットは中間検索結果に表示されません。

   >[!CAUTION]
   >
   >メタデータの検証チェックは、大量のリソースを必要とするので、システムのパフォーマンスに影響を及ぼす可能性があります。検証チェックのスケジュール設定は、適切におこなう必要があります。サーバーがチェックの負荷に対処できない場合は、このジョブを無効にしてください。
