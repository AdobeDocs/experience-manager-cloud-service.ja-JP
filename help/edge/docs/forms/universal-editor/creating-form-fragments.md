---
title: WYSIWYG ベースのオーサリング用にフォームフラグメントを作成する方法
description: ユニバーサルエディターでフォームフラグメントを作成し、フォームに追加する方法を説明します。
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 16%

---


# ユニバーサルエディターでのEdge Delivery Services フォームフラグメントの作成と使用

Formsには、多くの場合、連絡先情報、id の詳細、同意契約などの共通セクションが含まれています。 フォーム開発者は、新しいフォームを作成するたびに、これらのセクションを作成しますが、これは繰り返し行われ、時間がかかります。
こうした作業の重複を排除するために、ユニバーサルエディターでは、パネルやフィールドのグループなどの再利用可能なフォームセグメントを 1 回だけ作成し、様々なフォームで再利用する方法を提供しています。 これらの再利用可能なモジュール型スタンドアロンのセグメントは、フォームフラグメントと呼ばれます。 例えば、従業員と管理者の連絡先の詳細など、同じ緊急連絡先フラグメントを、フォームの異なるセクションで使用できます。

この記事の最後では、ユニバーサルエディターを使用してフォーム内でフラグメントを作成および使用する方法について説明します。

## Edge Delivery Services フォームフラグメントの機能

* **フォームフラグメントとの一貫性の維持**
フラグメントを様々なフォームに統合して、一貫性のあるレイアウトと標準化されたコンテンツを維持できます。 「1 回の変更であらゆる場所を反映」アプローチを使用すると、フラグメントに対する更新はすべてのフォームに自動的に適用されます。

* **フォームフラグメントのフォーム内での複数回追加**
フォームフラグメントは、フォーム内に複数回追加し、そのデータ連結プロパティをデータソースまたはスキーマに設定することができます。

* **フラグメント内でのフラグメントの使用**
入れ子のフォームフラグメントを作成できます。このことはフラグメント内に別のフラグメントを追加し、入れ子のフラグメント構造を構築できることを意味します。

  >[!NOTE]
  >
  > フラグメント自体の中にフラグメントをネストすることはできません。再帰的な参照や意図しない動作が発生し、エラーやレンダリングの問題を引き起こす可能性があるからです。

## Edge Delivery Services フォームフラグメント使用時の考慮事項

* フラグメントと、フラグメントを使用するフォームの両方に、同じ GitHub URL を追加する必要があります。
* 参照によって挿入されたフォームフラグメントは、フォーム内から編集できません。 編集するには、スタンドアロンのフォームフラグメントを変更します。

## Edge Delivery Services フォームフラグメントを作成するための前提条件

* [GitHub リポジトリを設定 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) して、AEM環境と GitHub リポジトリの間の接続を確立します。
* 既に Edge Delivery Services を使用している場合は、最新バージョンの[アダプティブフォームブロック](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)を GitHub リポジトリに追加します。
* AEM Forms オーサーインスタンスには、Edge Delivery Services に基づくテンプレートが含まれます。 使用する環境に[最新バージョンのコアコンポーネント](https://github.com/adobe/aem-core-forms-components)がインストールされていることを確認します。
* AEM Forms as a Cloud Service オーサーインスタンスの URL と GitHub リポジトリをすぐに使用できる状態にします。

## Edge Delivery Services フォームフラグメントの操作

ユニバーサルエディターでEdge Delivery Services フォームフラグメントを作成し、作成したフラグメントをEdge Delivery Services forms に追加できます。 Edge Delivery Services フォームフラグメントで実行できるアクションは次のとおりです。

* [フォームフラグメントの作成](#creating-form-fragments)
* [フォームフラグメントのフォームへの追加](#adding-form-fragments-to-a-form)
* [フォームフラグメントの管理](#managing-form-fragments)

### フォームフラグメントの作成

ユニバーサルエディターでフォームフラグメントを作成するには、次の手順を実行します。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **作成／アダプティブフォームセグメント**&#x200B;をクリックします。

   ![ フラグメントを作成 ](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   **アダプティブフォームフラグメントの作成** ウィザードが表示されます。
1. **テンプレートを選択** タブから、Egde 配信サービスベースのテンプレートを選択し、**[!UICONTROL 次へ]** をクリックします。
   ![Edge Delivery Services テンプレートを選択 ](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. フラグメントのタイトル、名前、説明およびタグを指定します。 フラグメントには一意の名前を指定してください。同じ名前を持つ別のフラグメントが存在する場合、フラグメントの作成は失敗します。
1. **GitHub URL** を指定します。 例えば、GitHub リポジトリの名前が `edsforms` の場合は、アカウント `wkndforms` の下にあり、URL は `https://github.com/wkndforms/edsforms` となります。

   ![ 基本プロパティ ](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （オプション）をクリックして「**フォームモデル**」タブを開き、「**次から選択**」ドロップダウンメニューから、フラグメントに対して次のいずれかのモデルを選択します。

   ![「フォームモデル」タブにモデルタイプを表示](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **フォームデータモデル（FDM）**：データソースから取得したデータモデルオブジェクトとサービスをフラグメントに統合します。 フォームで複数のソースからのデータの読み取りと書き込みが必要な場合は、フォームデータモデル（FDM）を選択します。

   * **JSON スキーマ**：データ構造を定義する JSON スキーマを関連付けて、フォームをバックエンドシステムに統合します。 スキーマ要素を使用して動的コンテンツを追加できます。
   * **なし**：フォームモデルを使用しないで最初からフラグメントを作成するときに指定します。

   >[!NOTE]
   >
   > ユニバーサルエディターでフォームまたはフラグメントをフォームデータモデル（FDM）に統合して様々なバックエンドデータソースを使用する方法については、[ ここをクリック ](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) を参照してください。

1. （オプション）「**詳細**」タブでフラグメントの **公開日** または **非公開日** を指定します。

   ![ 「詳細」タブ ](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. **作成** をクリックすると、ウィザードが表示されます。

   ![ フラグメントを編集 ](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. **編集** をクリックすると、デフォルトのテンプレートを使用して作成されたフラグメントがオーサリング用のユニバーサルエディターで開きます。

   ![ オーサリング用のユニバーサルエディター内のフラグメント ](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   編集モードでは、任意のフォームコンポーネントをフラグメントに追加できます。 ユニバーサルエディターでフラグメントを作成する方法については、[ ユニバーサルエディターを使用したAEM FormsのEdge Delivery Servicesの概要 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) 記事を参照してください。

   次のスクリーンショットは、ユニバーサルエディターで作成された `contact fragment` を示しています。

   ![ 連絡先フラグメント ](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   フラグメントを作成したら、作成したフラグメントをEdge Delivery Services Formsに追加 [ できます ](#adding-form-fragments-in-forms)。

### フォームフラグメントのフォームへの追加

従業員と管理者の両方の情報を含むシンプルな `Employee Details` フォームを作成しましょう。 `Contact Details` フラグメントは、従業員パネルとスーパーバイザーパネルの両方で使用できます。 フォームフラグメントをフォームで使用するには、次の手順を実行します。

1. フォームを編集モードで開きます。
1. フォームフラグメントコンポーネントをフォームに追加します。
1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。
1. フラグメントを追加するセクションに移動します。 例えば、「**従業員詳細** パネルに移動します。

   ![ 次のセクションに移動 ](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. **[!UICONTROL 追加]** アイコンをクリックし、**[!UICONTROL アダプティブフォームコンポーネント]** リストから **フォームフラグメント** コンポーネントを追加します。
   ![ フォームフラグメントの追加 ](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   **[!UICONTROL フォームフラグメント]** コンポーネントを選択すると、フラグメントがフォームに追加されます。 追加されたフラグメントのプロパティを設定するには、そのプロパティ **プロパティ** を開きます。 例えば、フラグメントのタイトルを **プロパティ** から非表示にします。

   ![ フラグメントのプロパティの設定 ](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 「**基本**」タブで「**フラグメント参照**」を選択します。フォームのモデルに応じて、フォームで使用可能なすべてのフラグメントが表示されます。

   例えば、`/content/forms/af` に移動し、`Contact Details` フラグメントを選択します。

   ![ フラグメントを選択 ](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. **[!UICONTROL 選択]** をクリックします。

   フォームフラグメントは、参照によってフォームに追加され、スタンドアロンのフォームフラグメントと同期されたままになります。 つまり、フラグメントに加えられた変更は、フラグメントがフォーム内に組み込まれるすべてのインスタンスにミラーリングされます。

   ![ フォーム内のフラグメント ](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   フォームをプレビューして、**プレビュー** モードでフォームがどのように表示されるかを確認できます。

   ![プレビュー](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同様に、手順 3 ～ 7 を繰り返して、`Supervisor Details` パネル用の `Contact Details` フラグメントを挿入できます。

   ![ 従業員の詳細フォーム ](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### フォームフラグメントの管理

AEM Forms ユーザーインターフェイスを使用して、フォームフラグメントに対して複数の操作を実行できます。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. フォームフラグメントを選択すると、ツールバーに、選択されているフラグメントに対して実行できる次の操作が表示されます。

   ![ フラグメントの管理 ](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
    </tr>
    <tr>
   <td><p>編集</p> </td>
   <td><p>フォームフラグメントを編集モードで開きます。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>プロパティ</p> </td>
   <td><p>フォームフラグメントのプロパティを変更するためのオプションを提供します。<br /> <br /> </p> </td>
    </tr>
    <td><p>コピー</p> </td>
   <td><p> フォームフラグメントをコピーして目的の場所に貼り付けるオプションが用意されています。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>プレビュー</p> </td>
   <td><p>フラグメントをHTMLとしてプレビューするオプションや、XML ファイルからのデータをフラグメントと結合してカスタムプレビューを実行するオプションが用意されています。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>ダウンロード</p> </td>
   <td><p>選択されているフラグメントをダウンロードします。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>レビューの開始／レビューの管理</p> </td>
   <td><p>選択されているフラグメントのレビューを開始したり管理したりできます。<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>公開／非公開</p> </td>
   <td><p>選択されているフラグメントを公開／非公開します。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>削除</p> </td>
   <td><p>選択されているフラグメントを削除します。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>比較</p> </td>
   <td><p>プレビュー目的で 2 つの異なるフォームフラグメント <br /> 比較します。<br /> </p> </td>
    </tr>
    </tbody>
    </table>

## ベストプラクティス

* フラグメント名が一意であることを確認します。同じ名前の既存のフラグメントが存在する場合、フラグメントは作成できません。
* スタンドアロンフォームフラグメント内の式、スクリプト、またはスタイルは、参照によって挿入されたときや、フォームに埋め込まれたときにも保持されます。
* フォームを公開すると、フォーム内の参照によって挿入されたフォームフラグメントが自動的に公開されます。

## 関連トピック

{{universal-editor-see-also}}