---
title: AEM Forms のメタデータはどのように管理できますか？
description: メタデータを使用すると、アセットの分類および編成を容易に行うことができ、特定のアセットを検索しやすくなります。
feature: Adaptive Forms, Foundation Components
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 97%

---

# アダプティブフォームのメタデータの追加、削除、編集 {#manage-form-metadata}

>[!NOTE]
>
> Adobeでは、（新しいアダプティブFormsの作成 [ または ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)[ AEM SitesページへのアダプティブFormsの追加 [ に、最新の拡張可能なデータキャプチャ ](/help/forms/creating-adaptive-form-core-components.md) コアコンポーネント ](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) を使用することをお勧めします。 これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古いアプローチを説明します。


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

メタデータを使用すると、アセットの分類および編成を容易に行うことができ、特定のアセットを検索しやすくなります。

[!DNL AEM Forms] では、デフォルトで各アセットタイプに対してメタデータの定義済みセットが提供されます。デフォルトのメタデータに加え、各アセットタイプにカスタムメタデータを追加することができます。[!DNL AEM Forms] では、フォーム用のメタデータすべてを効率よく作成、管理およびやり取りを行う適切な方法も提供されます。

<!-- If you are a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you are using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## [!DNL AEM Forms] でのメタデータ {#metadata-in-aem-forms}

[!DNL AEM Forms] では、アセットに関連付けられたメタデータのプロパティのリストはタイプによって異なります。また、任意のカスタムメタデータのプロパティを追加すると、カスタムメタデータが追加されたタイプのすべてのアセットに追加されます。

### アセットタイプ {#asset-types}

次のアセットタイプは [!DNL AEM Forms] でサポートされます。

* フォームテンプレート（XFA フォーム）
* PDF のフォーム
* ドキュメント（フラット PDF）
* アダプティブフォーム
* Forms データモデル
* XFS

#### 広範なメタデータのリスト {#extensive-list-of-metadata}

次のリストは、[!DNL AEM Forms] でサポートされるメタデータのプロパティの広範なリストです。

<table>
 <tbody> 
  <tr> 
   <td><strong>プロパティ名</strong></td> 
   <td><strong>アセットタイプ</strong></td> 
   <td><strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>タイトル</td> 
   <td>リソース以外のすべて</td> 
   <td>アセットの名前を表示します。<br /> </td> 
  </tr> 
  <tr> 
   <td>説明</td> 
   <td>リソース以外のすべて</td> 
   <td>アセットの説明。ユーザーはこの値を指定できます。<br /> </td> 
  </tr> 
  <tr> 
   <td>タイプ</td> 
   <td>すべて</td> 
   <td><p>アセットのタイプを指定する読み取り専用の値です。次のいずれかの値になります。</p> 
    <ul> 
     <li>フォームテンプレート</li> 
     <li>PDF フォーム、PDF フォーム（Acroform）または PDF フォーム（署名済み）</li> 
     <li>ドキュメント、ドキュメント（署名付き）</li> 
     <li>アダプティブフォーム</li> 
     <li>フォームデータモデル（FDM）</li>
     <li>リソース</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>作成日</td> 
   <td>すべて</td> 
   <td>アセット作成の時間を指定する、読み取り専用の値です。</td> 
  </tr> 
  <tr> 
   <td>最終変更日</td> 
   <td>すべて</td> 
   <td>アセットが最後に変更された時間を指定する、読み取り専用の値です。</td> 
  </tr> 
  <tr> 
   <td>作成者</td> 
   <td>リソース以外のすべて</td> 
   <td><p>フォームタイプに基づいて自動で算出される、読み取り専用の値です。</p> 
    <ul> 
     <li>PDF／フォームテンプレート／ドキュメント - アップロードされたバイナリファイルから取得。</li> 
     <li>アダプティブフォーム - フォームが作成されたときにログインしたユーザー。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>ステータス</td> 
   <td>リソース以外のすべて</td> 
   <td><p> 次のフォームのいずれかの状態を定義する読み取り専用の値です。</p> 
    <ul> 
     <li>値なし：フォームが一度も公開されていない場合。</li> 
     <li>公開済み：フォームが公開されたとき。</li> 
     <li>変更済み：一度公開された後にフォームが変更されたとき。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>最終公開日</td> 
   <td>リソース以外のすべて</td> 
   <td>フォームが最後に公開されたときの時間を指定する読み取り専用の値です。</td> 
  </tr> 
  <tr> 
   <td>公開オン／オフ時間</td> 
   <td>リソース以外のすべて</td> 
   <td><p>フォームが自動で公開または未公開になるようにスケジュールされる時間です。ユーザーはこの値をメタデータの編集で設定します。</p> 
    <ul> 
     <li>公開オンおよび公開オフのどちらの時間も、現在の日付よりも後の日付にする必要があります。 </li> 
     <li>「オフタイムに公開」は、「オンタイムに公開」よりも後の時間にする必要があります。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>URL を送信</td> 
   <td><p>フォームテンプレート</p> <p>PDF フォーム</p> </td> 
   <td><p>フォームデータをサーブレットに送信するためにユーザー指定の URL を設定する方法です。</p> <p>「URL を送信」は、次の方法（好ましい順）のいずれかを使用して設定できます。</p> 
    <ul> 
     <li>AEM Forms Designer で XFA フォームを作成しているときに、「HTTP 送信」ボタンを使用して、「URL を送信」をフォームテンプレートに直接指定します。</li> 
     <li>AEM Forms の UI で、メタデータのプロパティ編集時にフォームを選択し、送信 URL を指定します。</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML レンダリングプロファイル</td> 
   <td>フォームテンプレート</td> 
   <td>HTML 形式のフォームテンプレートのレンダリング中に使用される HTML レンダリングプロファイル。</td> 
  </tr> 
  <tr> 
   <td>レンダリング形式</td> 
   <td><p>フォームテンプレート</p> <p>アダプティブフォーム</p> </td> 
   <td><p>このオプションを使用すると、ユーザーはフォームが公開されるときのフォームのレンダリング形式を指定できます。</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>両方</li> 
    </ul> <p>このオプションは、ユーザーに表示されるフォームポータルでのみフォームのレンダリング形式を制限する場合に使用されます。</p> </td> 
  </tr> 
  <tr> 
   <td>タグ</td> 
   <td>リソース以外のすべて</td> 
   <td>検索をすばやく容易に行うために、フォームに関連付けられたラベルです。</td> 
  </tr> 
  <tr> 
   <td>参照</td> 
   <td><p>アダプティブフォーム</p> <p>フォームテンプレート</p> <p>リソース</p> </td> 
   <td><p>このフォームが関連付けられているアセット（その他のフォームまたはリソース）のリストです。これらのアセットは、次の 2 つに分類されます。</p> 
    <ul> 
     <li>参照先：現在のフォームが参照しているアセット。</li> 
     <li>参照元：現在のアセットを参照しているアセット。</li> 
    </ul> <p>これらのアセットはリンクとして表示され、リンクをクリックすると、そのメタデータに直接アクセスできます。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>フォームモデル（XDP/XSD）選択</td> 
   <td>アダプティブフォーム</td> 
   <td><p>アダプティブフォームのオーサリング中に使用されるフォームモデルを指定します。このプロパティは次の値を含めることができます。</p> 
    <ul> 
      <li>フォームデータモデル（FDM）</li>
      <li>スキーマ：JSON スキーマの XML</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>なし</li> 
    </ul> 
    <div>
      フォームモデルを選択すると、更新できますが削除できません。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## フォームメタデータの表示 {#view-form-metadata}

アセットには既存のプロパティの値が含まれ、これは読み取り専用モードで表示できます。このメタデータは、フォームのアプロード時またはフォーム作成時に生成されます。

1. メタデータを表示するアセットの場所に移動します。

1. 次のいずれかの方法を使用してプロパティページを開きます。

   * クイックアクションで、**[!UICONTROL プロパティ]** ![プロパティ](assets/Smock_Info_18_N.svg) アイコンをクリックします。

     >[!NOTE]
     >
     >クイックアクションは、マウスのカーソルを合わせたときにサムネール上に表示されるアクション項目です。

   * フォームを選択し、ツールバーに表示される&#x200B;**[!UICONTROL プロパティ]** ![プロパティ](assets/Smock_Info_18_N.svg) アイコンをクリックします。
   * 選択モードではない場合にフォームのサムネールをクリックして、フォーム詳細ページに移動します。ここで、右上にある ![プロパティ](assets/Smock_Info_18_N.svg) 目のアイコンをクリックして、その下にあるリストで「プロパティ」をクリックします。

1. プロパティページが開き、いくつかの値を保持するメタデータのプロパティのみを含むスキーマが表示されます。

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   コンテンツ部分は 2 つのパートに分かれています。

   * 左のパネルにはフォームのサムネールが含まれます
   * 右のパネルには、様々なタブに配布されるメタデータのプロパティが読み取り専用モードで含まれます。

## フォームメタデータの値の追加および更新 {#add-update-form-metadata-values}

既存のメタデータプロパティの値を編集したり、既存のメタデータプロパティのフィールドに新しい値を追加する（例えば、メタデータフィールドが空白の場合など）ことができます。

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### フォームサムネールの更新 {#update-the-form-thumbnail}

プロパティページの左のパネルには、フォームのサムネールが表示されます。デフォルトでは、表示されるサムネールはフォーム（アダプティブフォーム）作成時またはフォームアップロード時に生成されたサムネールです。

すべてのフォームタイプには、「**[!UICONTROL 画像をアップロード]**」をクリックして画像をアップロードするオプション、およびローカルディレクトリから画像ファイルを参照するオプションがあります。デフォルトのサムネールの代わりに、選択された画像がサムネールとして使用されます。

アダプティブフォームでは、ユーザーが現在のアダプティブフォームプレビューのスナップショットとしてサムネールを生成できる追加機能が提供されています。[!DNL AEM Forms] はアダプティブフォームのオーサリングもサポートするため、アダプティブフォームを変更するたびにアダプティブフォームのプレビューが変更される可能性があります。サムネールを生成するこの機能により、現在のプレビューステータスに基づいてアダプティブフォーム用に新規サムネールを取得できます。「**[!UICONTROL プレビューを生成]**」をクリックし、このアクションを実行します。

>[!NOTE]
>
>* サムネールには四角形の画像を使用します。四角形以外の画像を使用し、サムネールを一覧表示で表示すると、サムネールはクリップされて表示されます。
>* 新しい画像がアップロードまたは生成されると、サムネールはこの画像に置き換えられ、以前の画像にリセットすることはできません。
>

## カスタムメタデータの追加 {#add-custom-metadata}

初期設定の状態で提供されているメタデータとは別に、[!DNL AEM Forms] は新規のカスタムメタデータをサポートします。

メタデータレイアウトのスキーマを定義するためのツール（メタデータスキーマエディター）が提供されます。これは、フォームの「**[!UICONTROL プロパティ]**」ページにおける表示レイアウトです。メタデータスキーマエディターを使用して、アセットのカスタムスキーマを追加または変更できます。

[!DNL AEM Forms] は、このツールでサポート対象のフォームタイプのメタデータスキーマを公開します。この方法で、これらのスキーマにアクセスし、メタデータスキーマエディターで提供される機能を使用してカスタムプロパティを追加できます。

### メタデータスキーマエディターに移動 {#navigate-the-metadata-schema-editor}

1. **[!UICONTROL ツール／Assets／メタデータスキーマ]** に移動します。

1. 一覧表示されたスキーマフォームで&#x200B;**[!UICONTROL 「]**&#x200B;フォーム」をクリックします。

1. 開いたリストで、カスタムメタデータを追加するアセットタイプをクリックします。

   >[!NOTE]
   >
   >これらのスキーマには初期設定で提供されるメタデータプロパティが含まれていますが、機能的な問題の発生を防ぐため、変更および編集（チェックボックスの選択およびツールバーで編集をクリック）することはできません。

1. 任意のアセットタイプをクリックすると、`extendedmetadata` オプションを含むリストが開きます。このスキーマを編集します。

1. `extendedmetadata` の横にあるチェックボックスを選択し、ツールバーに表示される編集 ![編集](assets/Smock_Edit_18_N.svg) アイコンをクリックします。

1. 選択されたアセットタイプ（この場合はアダプティブフォーム）のメタデータスキーマエディターまたはフォームビルダーが、[!DNL AEM Forms] で開きます。

   メタデータエディター

   1. 左のパネルにはフィールドが配置されるタブ付きセクションが含まれ、左のパネルで選択したフィールドの使用可能なすべての UI コンポーネントとプロパティが右のパネルに表示されます。

   1. ロックされたセクションは編集することができず、初期設定で提供されるすべてのメタデータプロパティのフィールドが含まれます。

   1. 「+」 記号をクリックして、追加のタブを追加できます。

   1. 「**[!UICONTROL フォームを作成]**」セクションからスキーマページにフィールドコンポーネントをドラッグして、必要なタイプのカスタムフィールドを追加できます。
   1. このフィールドの仕様は、フィールドをクリックした後に「**[!UICONTROL 設定]**」セクションの下に提供されます。

### カスタムメタデータプロパティのスキーマエディターへの追加 {#add-custom-metadata-property-in-schema-editor}

1. カスタムプロパティを追加する既存または新規のタブに移動します。

1. 必要なタイプのコンポーネントを「**[!UICONTROL フォームをビルド]**」セクションから左のパネルにドラッグし、適切な場所に配置します。

   >[!NOTE]
   >
   >ロックされたセクションは移動できませんが、空いている場所であればどこでもコンポーネントを配置できます。

1. ドラッグしたコンポーネントをクリックします。右のパネルに開いた「設定」タブで、次のフィールドに情報を入力します。

   1. スキーマに配置されるフィールドの上に表示される名前に使用するフィールドラベルを指定します（例えば、部門など）
   1. プロパティにマッピングフィールドの下に、事前入力された値 **「./jcr:content/metadata/default」**&#x200B;が表示されます。「**default**」を、必要なプロパティ名に変更します。これは、crx リポジトリにプロパティを保存するために使用されます（例えば、「./jcr:content/metadata/department&#39;）。

      >[!NOTE]
      >
      >プレフィックス「./jcr:content/metadata/」は、プロパティが保存されるパスを定義しているので、変更しないでください。
      >
      >また、リポジトリーの同じ場所に 2 つ以上のプロパティの値が書き込まれるのを防ぐため、プロパティ名は一意にする必要があります。そのため、「default」の値は変更することをお勧めします。

   1. 要件に基づいてその他の設定を入力します。例えば、フィールドを必須フィールドにする場合は、必須オプションを選択します。
   1. 追加したフィールドを削除するには、フィールドを選択して削除 ![削除](assets/Smock_Delete_18_N.svg) アイコンをクリックします。

1. 必要に応じて、手順 1 から 3 に従って、別のプロパティを追加します。
1. すべての変更を行ったら、「**[!UICONTROL 保存]**」をクリックします。

   カスタムメタデータのプロパティを正常に追加しました。

[!DNL AEM Forms] のすべてのアダプティブフォームに、この追加のメタデータプロパティが含まれるようになりました。このプロパティは、プロパティページから編集できます。


## 関連トピック {#see-also}

{{see-also}}