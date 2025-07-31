---
title: コアコンポーネントまたは Edge Delivery Services テンプレートに基づいてスタンドアロンフォームを作成し、Edge Delivery Services で公開する方法
description: この記事では、フォーム作成ウィザードでコアコンポーネントベースまたは Edge Delivery Services ベースのテンプレートを選択して、アダプティブフォームを作成する方法について説明します。また、フォームを AEM Edge Delivery Services に公開することもできます。
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: ht
source-wordcount: '1687'
ht-degree: 100%

---


# オーサリングからパブリッシングへ：Edge Delivery Services での AEM Forms

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセス権をリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は「adobe」、リポジトリ名は「abc」になります。</span>

Adobe Experience Manager（AEM）を使用すると、魅力的でレスポンシブ、かつ動的なフォームを作成できます。それぞれ異なる要件やユーザーの専門知識のレベルに適した、複数のオーサリング方法を提供します。

この記事では、AEM 環境内でフォームを作成し、Edge Delivery Services を通じてフォームを公開するアプローチに重点を置いて説明します。コアコンポーネントベースのテンプレートを使用して構築されたフォームは、AEM と Edge Delivery Services の両方で公開でき、柔軟なデプロイメントが可能です。これに対し、Edge Delivery Services ベースのテンプレートを使用して作成したフォームは、Edge Delivery Services でのみ公開できます。

![アダプティブフォームの作成と公開](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## AEM でのフォームのオーサリングと Edge Delivery Services を使用したパブリッシングの利点：

* **既存の AEM ワークフローの保持**：組織は確立された AEM ワークフローとガバナンス構造を引き続き使用して、コンテンツ作成の一貫性と制御を確保できます。

* **パフォーマンスの向上**：Edge Delivery Services を通じて公開すると、レンダリング時間が短縮され、ユーザーエクスペリエンスが向上し、ページ読み込み時間が短縮されます。

* **SEO の向上**：Edge Delivery Services は、Google Lighthouse のスコアが高いコンテンツを配信するように設計されているので、検索エンジンの最適化と可視性の向上につながります。

* **柔軟なデプロイメントオプション**：コアコンポーネントで構築されたフォームは、AEM と Edge Delivery Services の両方で公開でき、柔軟なデプロイメント戦略を実現します。

## 開始する前に

AEM でフォームのオーサリングを開始し、Edge Delivery Services を使用してフォームを公開する前に、次の前提条件が満たされていることを確認してください。

* Edge Delivery Services 用に Github リポジトリが設定されていることを確認します。
   * リポジトリがない場合は、[アダプティブフォームブロックにより事前設定された新しい AEM プロジェクト](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)を使用します。
   * リポジトリがある場合は、アダプティブフォームブロックを既存のリポジトリに追加します。手順について詳しくは、[AEM Forms 用 Edge Delivery Services の概要](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)を参照してください。
* AEM 環境と GitHub リポジトリの間の接続を確立します。[その方法](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

アダプティブフォームの設定とパブリッシングをガイドする決定フロー図：

![Github リポジトリのワークフロー](/help/forms/assets/repo-workflow.png){width=auto}

## AEM でのフォームのオーサリングと Edge Delivery Services へのパブリッシング

AEM でのフォームのオーサリングと Edge Delivery Services での公開を行うには、次の手順に従います。

[&#x200B;1. テンプレートを選択し、フォームを作成します](#choose-a-template-and-create-the-form)

[&#x200B;2. フォームをオーサリングします](#author-the-form)

[&#x200B;3. フォームを公開します](#publish-a-form)

### テンプレートの選択とフォームの作成

次の方法を使用して、AEM インスタンスでフォームを作成し、Edge Delivery Services に公開できます。

>[!BEGINTABS]

>[!TAB Edge Delivery Services ベースのテンプレート]

テンプレートを選択してフォームを作成するには、次の手順を実行します。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。ウィザードが開きます。
1. 「**ソース**」タブで、**Edge Delivery Services ベースのテンプレート**&#x200B;を選択します。

   ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png)

   **Edge Delivery Services ベースのテンプレート**&#x200B;を選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。
1. （オプション）「**[!UICONTROL データソース]**」タブまたは「**[!UICONTROL 送信]**」タブで、データソースまたは送信アクションを選択できます。
1. （オプション）「**[!UICONTROL 配信]**」タブで、フォームの公開日または非公開日を指定できます。
1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。

   1. 「**名前**」と「**タイトル**」を指定します。
   1. **GitHub URL** を指定します。例えば、GitHub リポジトリの名前が `edsforms` で、アカウント `wkndforms` の下にある場合、URL は次のようになります。
      `https://github.com/wkndforms/edsforms`

   ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png)

   「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![左側にコンポーネントパレット、中央にフォームキャンバス、右側にプロパティパネルが表示され、オーサリングされているフォームを示すユニバーサルエディターのスクリーンショット](/help/edge/assets/author-form.png)
1. 「**[!UICONTROL 作成]**」をクリックしてフォームを作成します。これで、[ユニバーサルエディターを使用してフォームをオーサリング](#author-the-form)できます。

>[!TAB コアコンポーネントベースのテンプレート]

テンプレートを選択してフォームを作成するには、次の手順を実行します。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。ウィザードが開きます。
1. 「**ソース**」タブで、**コアコンポーネントベースのテンプレート**&#x200B;と&#x200B;**テーマ**&#x200B;を選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。

   ![コアコンポーネントベースのテンプレート](/help/forms/assets/core-component-based-template.png)

1. （オプション）「**[!UICONTROL データソース]**」タブまたは「**[!UICONTROL 送信]**」タブで、データソースまたは送信アクションを選択できます。
1. （オプション）「**[!UICONTROL 配信]**」タブで、フォームの公開日または非公開日を指定できます。
1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
   1. 「**名前**」と「**タイトル**」を指定します。
   1. アダプティブフォームを保存する場所を「**パス**」フィールドで指定します。

   ![フォームを作成ウィザード](/help/forms/assets/create-cc-form.png)

   「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のアダプティブフォームエディターで開きます。

   ![アダプティブフォームエディター](/help/forms/assets/af-editor-form.png)

1. 「**[!UICONTROL 作成]**」をクリックしてフォームを作成します。これで、[アダプティブフォームエディターを使用してフォームをオーサリング](#author-the-form)できます。

>[!ENDTABS]

### フォームのオーサリング

Edge Delivery Services ベースのテンプレートを使用して作成されたフォームは、オーサリング用に[ユニバーサルエディター](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)で開きます。ただし、コアコンポーネントベースのテンプレートを使用して作成されたフォームは、オーサリング用にアダプティブフォームエディターで開きます。

Edge Delivery Services ベースのテンプレートのユニバーサルエディターや、コアコンポーネントベースのテンプレートのアダプティブフォームエディターを使用してフォームを作成するには、次の手順を実行します。

>[!BEGINTABS]

>[!TAB Edge Delivery Services ベースのテンプレート]


1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。

   ![コンテンツツリー](/help/edge/assets/content-tree.png)

1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**リストから目的のコンポーネントを追加します。
   ![コンポーネントを追加](/help/edge/assets/add-component.png)

   以下のスクリーンショットは、ユニバーサルエディターでオーサリングした `Registration Form` フォームを示しています。

   ![適切なスタイル設定とレイアウトを使用した名前、メール、電話番号、メッセージのフォームフィールドを示す、ユニバーサルエディターの入力済みお問い合わせフォームのスクリーンショット](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> ユニバーサルエディターを使用したアダプティブフォームのオーサリング手順について詳しくは、[こちらをクリック](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)してください。

これで、[フォームの送信アクションを設定およびカスタマイズ](/help/edge/docs/forms/universal-editor/submit-action.md)できます。

>[!TAB コアコンポーネントベースのテンプレート]

1. 「**コンポーネントをここにドラッグ**」セクションで「**[!UICONTROL コンポーネントを挿入]**」をクリックします。

   ![コンポーネントをここにドラッグ](/help/forms/assets/drag-components-af-editor.png)

1. **アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

   ![コンポーネントを追加](/help/forms/assets/add-component-af.png)

以下のスクリーンショットは、アダプティブフォームエディターでオーサリングした `Enrollment Form` フォームを示しています。

![アダプティブフォームエディター](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> コアコンポーネントテンプレートに基づくアダプティブフォームの作成に関するガイダンスについて詳しくは、[こちらをクリック](/help/forms/creating-adaptive-form-core-components.md)してください。

これで、[フォームの送信アクションを設定](/help/forms/configure-submit-actions-core-components.md)できます。

>[!ENDTABS]

### フォームの公開

Edge Delivery Services でアダプティブフォームを公開するには、[AEM インスタンスで Edge Delivery Services 設定を作成](#create-an-edge-delivery-services-configuration)する必要があります。

#### Edge Delivery Services 設定の作成

Edge Delivery Services 設定を作成するには、次の手順を実行します。

>[!BEGINTABS]
>[!TAB Edge Delivery Services ベースのテンプレート]


Edge Delivery Services ベースのテンプレートに基づくフォームの Edge Delivery Services 設定は、フォームの設定コンテナに自動的に作成されます。

![Edge Delivery Services 設定](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB コアコンポーネントベースのテンプレート]

1. AEM Forms as a Cloud Service オーサーインスタンスで、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Edge Delivery Services 設定]**&#x200B;に移動します。

   ![Edge Delivery Services 設定を選択](/help/edge/assets/select-eds-conf.png)

2. フォームの名前に一致するフォルダーを選択します。例えば、フォームの名前が `enrollment-form` の場合は、フォルダー `forms/enrollment-form` を選択し、**[!UICONTROL 作成]**／**[!UICONTROL 設定]**&#x200B;をクリックします。

   ![Edge Delivery Services 設定](/help/forms/assets/create-eds-conf.png)

3. 「**[!UICONTROL Edge Delivery Services 設定]**」をクリックし、「**[!UICONTROL プロパティ]**」をクリックしてプロパティを開きます。

   ![自動作成された設定](/help/forms/assets/eds-conf.png)

   Edge Delivery Services 設定が表示されます。

4. Edge Delivery Services 設定で、次を指定します。

   * **組織**：GitHub の組織名を指定します。

   * **サイト名**：GitHub のリポジトリ名を指定します。
   * **分岐**：分岐名を指定します。main 分岐を使用する場合は、テキストボックスを空のままにします。
   * **（オプション）Edge ホスト**：「Edge ホスト」オプションはそのままにしておきます。フォームは、プレビュー（.page）環境とライブ（.live）環境の両方に公開されます。
   * **（オプション）サイト認証トークン**：サイト認証トークンを使用して、AEM インスタンスと Edge Delivery Services 間のリクエストを安全に認証します。

5. 「**[!UICONTROL 保存して閉じる]**」をクリックします。設定が作成されます。

>[!ENDTABS]

#### Edge Delivery Services のフォームへのアクセス

Edge Delivery Services のフォームにアクセスするには、フォームの公開が必須です。フォームを公開するには、次の手順を実行します。

>[!BEGINTABS]
>[!TAB ユニバーサルエディターの場合]

1. ユニバーサルエディターの右上隅にある「**[!UICONTROL 公開]**」ボタンをクリックして、フォームを公開します。

![フォームの公開オプションと確認ボタンを含む公開ダイアログを示すユニバーサルエディターのスクリーンショット](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> フォームを Edge Delivery Services に公開する方法について詳しくは、[公開とデプロイ](/help/edge/docs/forms/universal-editor/publish-forms.md)の記事を参照してください。

>[!TAB アダプティブフォームエディターの場合]

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。

1. ツールバーの「**[!UICONTROL 公開]**」オプションをクリックし、フォームと共に公開されるすべての参照アセットを確認します。

![アダプティブフォームエディターでフォームを公開](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> アダプティブフォームエディターでフォームを公開する方法について詳しくは、[Experience Manager Forms での公開の管理](/help/forms/manage-publication.md)を参照してください。

>[!ENDTABS]

* **ステージングされたバージョン（テスト用）**：ステージングされたバージョンには、テスト目的でフォームの非公開の作業用バージョンが表示されます。 フォームを公開する前にプレビューするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **ライブバージョン（公開済みフォーム）**：ライブバージョンには、エンドユーザーがアクセスできるフォームの最新公開バージョンが表示されます。 フォームの公開済みライブバージョンにアクセスするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  URL 構造は、ステージングされたバージョンとライブバージョンの両方で同じままです。ただし、表示されるコンテンツはコンテキストに基づいて異なります。

以下のスクリーンショットでは、Edge Delivery Services ベースおよびコアコンポーネントベースのテンプレートを使用して作成されたフォームのステージング済みフォーム URL とライブフォーム URL、およびビジュアルプレビューを比較しています。

>[!BEGINTABS]
>[!TAB Edge Delivery Services ベースのテンプレート]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>バージョン</strong></th>
      <th style="width: 80%;"><strong>画像</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>ステージング済みバージョン</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="登録フォームのステージング済みバージョン" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>ライブバージョン</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="登録フォームのライブバージョン" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB コアコンポーネントベースのテンプレート]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>バージョン</strong></th>
      <th style="width: 80%;"><strong>画像</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ステージング済みバージョン</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="登録フォームのステージング済みバージョン" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>ライブバージョン</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="登録フォームのライブバージョン" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## トラブルシューティング

フォームの読み込みに問題がありますか？ 一般的な問題と修正方法を以下に示します。

* **フォーム URL**：フォームの URL の末尾に「.html」拡張子が含まれていないことを再確認します。 Edge Deliver Service では、この拡張機能は必要ありません。

* **AEM オーサー URL**：`fstab.yaml` ファイルにリストされている AEM オーサー URL が正しい形式であることを確認します。 これには、次の詳細を含める必要があります。

   * 正しい GitHub 所有者
   * 正しいリポジトリ名
   * Edge Delivery Services に使用している特定の分岐

## フォームの作成の開始

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
