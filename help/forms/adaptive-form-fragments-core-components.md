---
title: アダプティブフォームフラグメントとは
description: アダプティブフォームでは、任意のアダプティブフォームで使用できるパネルやフィールドのグループなどのフォームセグメントを作成できます。また、既存のパネルをフラグメントとして保存することもできます。
topic-tags: author
keywords: アダプティブフォームフラグメントを追加、アダプティブフォームフラグメント、フォームフラグメントを作成、アダプティブフォームにフラグメントを追加、フラグメントを管理
feature: Adaptive Forms, Core Components
exl-id: 3a9ad1b7-2f6f-4ca9-a1c9-549c4238c59e
role: User, Developer
source-git-commit: a99bd181a079713571fd659ec2a04207c5eeee90
workflow-type: ht
source-wordcount: '1479'
ht-degree: 100%

---

# コアコンポーネントに基づくアダプティブフォームでのアダプティブフォームフラグメントの作成と使用 {#adaptive-form-fragments}


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service（コアコンポーネント） | この記事 |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/adaptive-form-fragments.md) |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=ja) |

すべてのフォームは特定の目的のために設計されますが、ほとんどのフォームにはいくつかの共通するセグメントがあります（例：名前と住所、家族の詳細、収入の詳細などの個人情報を入力するためのセグメント）。フォーム開発者は、新しいフォームを作成するたびに、これらの共通セグメントを作成する必要があります。

アダプティブフォームには、パネルやフィールドグループなどのフォームセグメントを 1 回だけ作成するための便利な機能が用意されています。作成したフォームセグメントは、アダプティブフォームで再利用することができます。この再利用可能なスタンドアロンのセグメントは、アダプティブフォームフラグメントと呼ばれます。

フォームフラグメントは複数のフォームにシームレスに統合され、一貫性のあるプロフェッショナルな外観のフォームを効率的に作成できます。フォームフラグメントは、「一度変更すればすべてに反映」機能を通じて、再利用性、標準化、ブランドの一貫性を確保します。1 か所で行われた更新が、これらのフラグメントを利用するすべてのフォームに自動反映されるので、メンテナンス性と効率性が向上します。

フラグメントを 1 つのドキュメントに複数回追加し、そのコンポーネントのデータ連結プロパティを使用すると、フラグメントを別のデータソースやスキーマに結び付けることができます。例えば、同じアドレスフラグメントを永続アドレス、通信アドレス、請求先アドレスに使用し、それをデータソースやスキーマの様々なフィールドに接続することができます。

>[!NOTE]
>
> [フォームフラグメントコンポーネントの設定ダイアログとデザインダイアログ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment)を使用して、ユーザーのフラグメントエクスペリエンスを簡単にカスタマイズできます。

## アダプティブフォームフラグメントの作成 {#create-a-fragment}

アダプティブフォームフラグメントは、最初から作成することも、既存のアダプティブフォーム内にパネルをフラグメントとして保存することもできます。フォームフラグメントを作成するには、次の手順を行います。

1. AEM Forms オーサーインスタンス（https://[*hostname*]:[*port*]/aem/forms.html）にログインします。
1. **作成／アダプティブフォームセグメント**&#x200B;をクリックします。

   ![アダプティブフォームフラグメントを作成](/help/forms/assets/adaptive-form-fragment.png)

1. フラグメントのタイトル、名前、説明、タグを指定します。フラグメントには一意の名前を指定してください。同じ名前を持つ別のフラグメントが存在する場合、フラグメントの作成は失敗します。
1. フォームテンプレートを選択します。コアコンポーネントベースのアダプティブフォーム、または基盤コンポーネントベースのアダプティブフォーム用のフォームフラグメントを作成できます。コアコンポーネントベースのフォームフォームフラグメントを作成するには、コアコンポーネントベースのテンプレートを選択します。

   コアコンポーネントベースのフォーム用のフォームフラグメントを作成する場合は、「フォームテーマを選択」オプションを使用して、コアコンポーネントベースのテーマを選択します。

1. 「**フォームモデル**」タブをクリックして開き、「**次から選択**」ドロップダウンメニューから、フラグメントに対して次のいずれかのモデルを選択します。

   ![「フォームモデル」タブにモデルタイプを表示](assets/create-af-1-1.png)

   * **なし**：フォームモデルを使用しないで最初からフラグメントを作成するときに指定します。

     >[!NOTE]
     >
     > アダプティブフォームでは、（コアコンポーネントに基づく）単一のフォームフラグメントを複数回使用できます。ベースがないのフォームフラグメントおよびスキーマベースのフォームフラグメントの両方をサポートします。

   * **スキーマ**：AEM フォームにアップロードされた XML または JSON スキーマを使用してフラグメントを作成する場合に指定します。アップロードするかまたはフラグメントのフォームモデルとして使用可能な XML または JSON スキーマから選択できます。XML スキーマを選択する場合、「**[!UICONTROL XML スキーマの複合型]**」ドロップダウンボックスから選択したスキーマ内に存在する complexType を選択することにより、アダプティブフォームフラグメントを作成することもできます。JSON スキーマを選択する場合、「**[!UICONTROL JSON スキーマの定義]**」ドロップダウンボックスから選択したスキーマ内に存在するスキーマを選択することにより、アダプティブフォームフラグメントを作成することもできます。
   * **フォームデータモデル**：フォームデータモデル（FDM）を使用してフラグメントを作成する場合に指定します。フォームデータモデル（FDM）内の 1 つのデータモデルオブジェクトのみに基づいて、アダプティブフォームフラグメントを作成できます。フォームデータモデル（FDM）定義ドロップダウンを展開します。指定したフォームデータモデル（FDM）内のすべてのデータモデルオブジェクトをリスト表示します。リストからデータモデルオブジェクトを選択します。

   ![フォームデータモデル（FDM）](assets/create-af-3.png)

1. 「**作成**」をクリックし、次に「**開く**」をクリックして、編集モードでデフォルトのテンプレートを使ってフラグメントを開きます。編集モードでは、任意のアダプティブフォームコンポーネントをフラグメントに追加できます。

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> また、フラグメントのフォームモデルとして XML スキーマを選択した場合は、フォームモデル階層を示す新しいタブがコンテンツファインダーに表示されます。これにより、フォームモデルの要素をフラグメントにドラッグ＆ドロップできます。<!--The added form-model elements get converted into form components while retaining the original properties from the associated XDP or XSD. -->

スキーマまたはフォームデータモデル（FDM）に基づいてアダプティブフォームフラグメントを作成すると、アダプティブフォームエディターでコンテンツブラウザーの「データソース」タブに、フォームデータモデル（FDM）またはスキーマ要素が表示されます。フォームモデルの要素をフラグメントにドラッグ＆ドロップできます。追加されたフォームモデルの要素はフォームコンポーネントに変換されますが、関連したスキーマからの元のプロパティは保持されます。


## アダプティブフォームにフラグメントを追加 {#insert-a-fragment-in-an-adaptive-form}

アダプティブフォームフラグメントをアダプティブフォームに追加するには、次の手順を実行します。

1. アダプティブフォームを編集モードで開きます。
1. **アダプティブフォームフラグメント**&#x200B;コンポーネントをフォームに追加します。
1. **アダプティブフォームフラグメント**&#x200B;コンポーネントの設定ダイアログを開きます。
1. 「**基本**」タブで「**フラグメント参照**」を選択します。フォームのモデルに応じて、フォームで使用可能なすべてのアダプティブフォームフラグメントが表示されます。

1. アダプティブフォームの&#x200B;**アダプティブフォームフラグメント**&#x200B;コンポーネントでアダプティブフォームフラグメントを選択します。

   ![「アダプティブフォームフラグメント」オプションを選択](/help/forms/assets/adaptive-form-fragment-basic.png)

<!-- >[!NOTE]
   >
   >The Adaptive Form fragment is not enabled for authoring from within the Adaptive Form. Moreover, you cannot use an XSD-based fragment in a JSON-based Adaptive Form and the opposite way. -->

アダプティブフォームフラグメントは、アダプティブフォーム内の参照により追加され、スタンドアロンのアダプティブフォームフラグメントと同期されたままとなります。つまり、アダプティブフォームフラグメントに加えた変更は、そのフラグメントがアダプティブフォームに組み込まれるすべてのインスタンスに反映されます。

<!--### Embed a fragment in Adaptive Form {#embed-a-fragment-in-adaptive-form}

You can choose to embed an Adaptive Form fragment in an Adaptive Form by clicking the ![Embed](assets/Smock_Import_18_N.svg) icon the panel toolbar of the added fragment

The embedded fragment is no longer linked with the standalone fragment. You can edit the components in the embedded fragment from within the Adaptive Form.-->

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### フラグメント内でのフラグメントの使用 {#using-fragments-within-fragments}

ネストされたアダプティブフォームフラグメントを作成できます。つまり、フラグメントを別のフラグメントに追加し、ネストされたフラグメント構造を持つことができます。

### アダプティブフォーム内でのフォームフラグメントの複数回の使用 {#using-form-fragment-mutiple-times-in-af}

ベースがないフォームフラグメントおよびスキーマベースのフォームフラグメントをアダプティブフォーム内で複数回使用して、各フォームフラグメントフィールドに対して一意にデータを保存できます。例えば、住所フォームフラグメントを使用して、ローン申し込みフォームの本住所、連絡先住所、および現居住住所に関する詳細な住所を収集できます。

![アダプティブフォームでの複数のフラグメントの使用](/help/forms/assets/using-multiple-fragment-af.gif)

## アダプティブフォーム内のフラグメントの自動マッピングサポート

JSON スキーマ定義に基づいてアダプティブフォームフラグメントを作成すると、同じスキーマから作成されたフォームで自動的に再利用できます。
アダプティブフォームフラグメントの JSON スキーマ定義マッピングに一致するスキーマオブジェクトまたはネストされたオブジェクトをドラッグ＆ドロップすると、オブジェクトは一致したアダプティブフォームフラグメントに置き換えられます。 個々のフィールドを含むパネルを追加する代わりに、フォームは、マッピングされたアダプティブフォームフラグメントを挿入します。

![フラグメントをドラッグ＆ドロップ](/help/forms/assets/fragment.png)

また、AEM コンテンツファインダーのアダプティブフォームフラグメントライブラリからバインドされたアダプティブフォームフラグメントをドラッグアンドドロップし、アダプティブフォームフラグメントパネルのコンポーネントの編集ダイアログから正しいバインド参照を与えることもできます。

## フラグメントの管理 {#manage-fragments}

AEM Forms UI を使用して、アダプティブフォームフラグメントに対して複数の操作を実行できます。

1. `https://[hostname]/aem/forms.html` にアクセスします。

1. AEM Forms UI ツールバーで「**選択**」をクリックし、アダプティブフォームフラグメントを選択します。ツールバーには、選択されているアダプティブフォームフラグメントに対して実行できる次の操作が表示されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>編集</p> </td>
   <td><p>選択されているアダプティブフォームフラグメントを編集モードで開きます。<br /><br /> </p> </td>
  </tr>
   <tr>
   <td><p>プレビュー</p> </td>
   <td><p>フラグメントを HTML でプレビューするか、あるいは XML ファイルからのデータをフラグメントとマージしてカスタムプレビューを生成するかのオプションが与えられます。詳しくは、<a>フォームのプレビュー</a>を参照してください。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>ダウンロード</p> </td>
   <td><p>選択されているフラグメントをダウンロードします。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>レビューの開始／レビューの管理</p> </td>
   <td><p>選択されているフラグメントのレビューを開始したり管理したりできます。詳しくは、<a>レビューの作成と管理</a>を参照してください。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>辞書を追加</p> </td>
   <td><p>選択されているフラグメントをローカライズするための辞書を生成します。詳しくは、<a>アダプティブフォームのローカライズ</a>を参照してください。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>公開／非公開</p> </td>
   <td><p>選択されているフラグメントを公開／非公開します。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>削除</p> </td>
   <td><p>選択されているフラグメントを削除します。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## フラグメントで作業するときの考慮事項 {#key-points-to-remember-when-working-with-fragments}

* フラグメント名が一意であることを確認します。同じ名前の既存のフラグメントが存在する場合、フラグメントは作成できません。
* スタンドアロンのアダプティブフォームフラグメント内の式、スクリプト、またはスタイルは、アダプティブフォームの参照によって挿入された場合や埋め込まれた場合にも保持されます。
* アダプティブフォームフラグメントを編集することはできません。これはアダプティブフォーム内から参照によって挿入されたものです。編集するには、スタンドアロンのアダプティブフォームフラグメントを変更します。
* アダプティブフォームを公開する場合、参照によってアダプティブフォームに挿入されたスタンドアロンのアダプティブフォームフラグメントを公開する必要があります。
* 更新されたアダプティブフォームフラグメントを再公開すると、フラグメントが使用されているアダプティブフォームの公開済みインスタンスに変更が反映されます。
* 検証コンポーネントが含まれているアダプティブフォームの場合、匿名ユーザーはサポートされません。また、アダプティブフォームフラグメントで検証コンポーネントを使用することはお勧めしません。

## リファレンスフラグメント {#reference-fragments}

フォームを作成するために使用できる参照用のアダプティブフォームフラグメントが使用できます。
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->



## 関連トピック {#see-also}

{{see-also}}