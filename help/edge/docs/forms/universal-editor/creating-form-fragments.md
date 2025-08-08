---
title: WYSIWYG ベースのオーサリング用のフォームフラグメントを作成する方法
description: ユニバーサルエディターでフォームフラグメントを作成し、フォームに追加する方法を説明します。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 97%

---

# ユニバーサルエディターでのフォームフラグメントの作成

<!--
<span class="preview"> This feature is available through the early access program. To request access, send an email with your GitHub organization name and repository name from your official address to <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . For example, if the repository URL is https://github.com/adobe/abc, the organization name is adobe and the repository name is abc.</span> 

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>
-->

Forms には、多くの場合、連絡先情報、ID の詳細、同意契約などの共通セクションが含まれています。フォーム開発者は、新しいフォームを作成するたびに、これらのセクションを作成しますが、この作業は繰り返し行われ、時間がかかります。
こうした作業の重複を排除するには、ユニバーサルエディターでは、パネルやフィールドのグループなどの再利用可能なフォームセグメントを 1 回だけ作成し、様々なフォームで再利用する方法を提供しています。この再利用可能で、モジュール化されたスタンドアロンのセグメントは、フォームフラグメントと呼ばれています。例えば、従業員や管理者の連絡先の詳細など、同じ緊急連絡先フラグメントを、フォームの異なるセクションで使用できます。

この記事の最後では、ユニバーサルエディターを使用してフォーム内でフラグメントを作成し、使用する方法について説明します。

## Edge Delivery Services フォームフラグメントの機能

- **フォームフラグメントとの一貫性の維持**
フラグメントを様々なフォームに統合して、一貫性のあるレイアウトと標準化されたコンテンツを維持できます。

  >[!NOTE]
  >
  > 「1 回の変更でどこにでも反映」アプローチを使用すると、フラグメントに対する更新はプレビューモードのすべてのフォームに自動的に適用されます。ただし、公開モードで、変更を反映するには、フラグメントを公開するか、フォームを再公開する必要があります。

- **フォーム内でフォームフラグメントを複数回追加**
フォーム内でフォームフラグメントを複数回追加し、そのデータバインディングプロパティをデータソースまたはスキーマに設定できます。

- **フラグメント内でのフラグメントの使用**
ネストされたフォームフラグメントを作成できます。つまり、フラグメントを別のフラグメントに追加し、ネストされたフラグメント構造を持つことができます。

  >[!NOTE]
  >
  > フラグメントをフラグメント自体の中にネストすることはできません。再帰的な参照や意図しない動作が発生し、エラーやレンダリングの問題を引き起こす可能性があります。

## Edge Delivery Services フォームフラグメント使用時の考慮事項

- フラグメントと、フラグメントを使用するフォームの両方に、同じ GitHub URL を追加する必要があります。
- フォーム内のフォームフラグメントは編集できません。変更を行うには、スタンドアロンのフォームフラグメントを変更します。

## 前提条件

- [GitHub リポジトリを設定](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)して、AEM 環境と GitHub リポジトリの間の接続を確立します。
- 既に Edge Delivery Services を使用している場合は、最新バージョンの[アダプティブフォームブロック](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)を GitHub リポジトリに追加します。
- AEM Forms オーサーインスタンスには、Edge Delivery Services に基づくテンプレートが含まれます。
- AEM Forms as a Cloud Service オーサーインスタンスの URL と GitHub リポジトリをすぐに使用できる状態にします。

## Edge Delivery Services フォームフラグメントの操作

ユニバーサルエディターで Edge Delivery Services フォームフラグメントを作成し、作成したフラグメントを Edge Delivery Services フォームに追加できます。Edge Delivery Services フォームフラグメントで実行できるアクションは次のとおりです。

- [フォームフラグメントの作成](#creating-form-fragments)
- [フォームへのフォームフラグメントの追加](#adding-form-fragments-to-a-form)
- [フォームフラグメントの管理](#managing-form-fragments)

### フォームフラグメントの作成

ユニバーサルエディターでフォームフラグメントを作成するには、次の手順を実行します。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **作成／アダプティブフォームセグメント**&#x200B;をクリックします。

   ![フラグメントの作成](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   **アダプティブフォームフラグメントを作成**&#x200B;ウィザードが表示されます。
1. 「**テンプレートを選択**」タブから、Edge Delivery Services ベースのテンプレートを選択し、「**[!UICONTROL 次へ]**」をクリックします。
   ![Edge Delivery Services テンプレートを選択](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. フラグメントのタイトル、名前、説明およびタグを指定します。フラグメントには一意の名前を指定してください。同じ名前を持つ別のフラグメントが存在する場合、フラグメントの作成は失敗します。
1. **GitHub URL** を指定します。例えば、GitHub リポジトリの名前が `edsforms` で、アカウント `wkndforms` の下にある場合、URL は `https://github.com/wkndforms/edsforms` になります。

   ![基本プロパティ](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （オプション）「**フォームモデル**」タブをクリックして開き、**次から選択**&#x200B;ドロップダウンメニューから、フラグメントに対して次のいずれかのモデルを選択します。

   ![「フォームモデル」タブにモデルタイプを表示](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **フォームデータモデル（FDM）**：データソースから取得したデータモデルオブジェクトとサービスをフラグメントに統合します。フォームで複数のソースからのデータの読み取りと書き込みが必要な場合は、フォームデータモデル（FDM）を選択します。

   - **JSON スキーマ**：データ構造を定義する JSON スキーマを関連付けることで、フォームをバックエンドシステムと統合します。これにより、スキーマ要素を使用して動的コンテンツを追加できます。
   - **なし**：フォームモデルを使用しないで最初からフラグメントを作成するときに指定します。

   >[!NOTE]
   >
   > ユニバーサルエディターでフォームまたはフラグメントをフォームデータモデル（FDM）に統合して様々なバックエンドデータソースを使用する方法については、[ ユニバーサルエディターでのフォームとフォームデータモデルの統合 ](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) を参照してください。

1. （オプション）「**詳細**」タブでフラグメントの&#x200B;**公開日**&#x200B;または&#x200B;**非公開日**&#x200B;を指定します。

   ![「詳細」タブ](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 「**作成**」をクリックすると、ウィザードが表示されます。

   ![フラグメントを編集](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 「**編集**」をクリックすると、デフォルトのテンプレートを使用して作成されたフラグメントがオーサリング用ユニバーサルエディターで開きます。

   ![オーサリング用ユニバーサルエディターのフラグメント](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   編集モードでは、任意のフォームコンポーネントをフラグメントに追加できます。ユニバーサルエディターでフラグメントを作成する方法について詳しくは、[ユニバーサルエディターでの AEM Forms の Edge Delivery Services の基本を学ぶ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)の記事を参照してください。

   次のスクリーンショットは、ユニバーサルエディターで作成した `contact fragment` を示しています。

   ![複数のフォームをまたいで再利用できる名前、電話番号、メール、住所のフィールドを示す、ユニバーサルエディターで入力済みの連絡先詳細フォームフラグメントのスクリーンショット](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   フラグメントを作成したら、[作成したフラグメントを Edge Delivery Services Forms に追加](#adding-form-fragments-in-forms)できます。

### フォームへのフォームフラグメントの追加

従業員とスーパーバイザーの両方の情報を含むシンプルな `Employee Details` フォームを作成しましょう。`Contact Details` フラグメントは、従業員パネルとスーパーバイザーパネルの両方で使用できます。フォームフラグメントをフォームで使用するには、次の手順を実行します。

1. フォームを編集モードで開きます。
1. フォームフラグメントコンポーネントをフォームに追加します。
1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。
1. フラグメントを追加するセクションに移動します。例えば、**従業員詳細**&#x200B;パネルに移動します。

   ![セクションに移動](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから&#x200B;**[!UICONTROL フォームフラグメント]**を追加します。
   ![フォームフラグメントを追加](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   **[!UICONTROL フォームフラグメント]**&#x200B;コンポーネントを選択すると、フラグメントがフォームに追加されます。追加したフラグメントのプロパティは、この&#x200B;**プロパティ**&#x200B;を開いて設定できます。例えば、フラグメントのタイトルをこの&#x200B;**プロパティ**&#x200B;から非表示にします。

   ![フラグメントのプロパティの設定](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 「**基本**」タブで「**フラグメント参照**」を選択します。フォームのモデルに応じて、フォームで使用可能なすべてのフラグメントが表示されます。

   例えば、`/content/forms/af` に移動して、`Contact Details` フラグメントを選択します。

   ![フラグメントを選択](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 「**[!UICONTROL 選択]**」をクリックします。

   フォームフラグメントは、フォームへの参照により追加され、スタンドアロンのフォームフラグメントと同期を維持します。

   ![ユニバーサルエディター内の従業員フォームに連絡先詳細フラグメントが正常に統合され、フラグメントの構造が再利用時にどのように維持されるかを示すスクリーンショット](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   **プレビュー**&#x200B;モードでフォームをプレビューして、フォームがどのように表示されるかを確認できます。

   ![プレビュー](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同様に、手順 3～7 を繰り返して、`Supervisor Details` パネルの `Contact Details` フラグメントを挿入できます。

   ![従業員の詳細フォーム](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### フォームフラグメントの管理

AEM Forms ユーザーインターフェイスを使用して、フォームフラグメントに対して複数の操作を実行できます。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. フォームフラグメントを選択すると、選択したフラグメントに対して実行できる次の操作がツールバーに表示されます。

   ![フラグメントを管理](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
    </tr>
    <tr>
   <td><p>編集</p> </td>
   <td><p>フォームフラグメントを編集モードで開きます。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>プロパティ</p> </td>
   <td><p>フォームフラグメントのプロパティを変更するオプションを指定します。<br /> <br /> </p> </td>
    </tr>
    <td><p>コピー</p> </td>
   <td><p> フォームフラグメントを目的の場所にコピー＆ペーストするオプションを指定します。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>プレビュー</p> </td>
   <td><p>フラグメントを HTML としてプレビューするか、XML ファイルのデータをフラグメントと結合してカスタムプレビューを実行するオプションを指定します。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>ダウンロード</p> </td>
   <td><p>選択されているフラグメントをダウンロードします。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>レビューの開始／レビューの管理</p> </td>
   <td><p>選択されているフラグメントのレビューを開始したり管理したりできます。<br /> <br /> </p> </td>
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
   <td><p>プレビュー目的で 2 つの異なるフォームフラグメントを比較します。<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## ベストプラクティス

- フラグメント名が一意であることを確認します。同じ名前の既存のフラグメントが存在する場合、フラグメントは作成できません。
- スタンドアロンのフォームフラグメント内の式、スクリプト、またはスタイルは、フォームの参照によって挿入されたときや、埋め込まれたときにも保持されます。
- フォームを公開すると、フォーム内で参照によって挿入されたフォームフラグメントが自動的に公開されます。


