---
title: コアコンポーネントまたはEdge Delivery Services テンプレートに基づいてスタンドアロンフォームを作成し、Edge Delivery Servicesで公開する方法
description: この記事では、フォーム作成ウィザードでコアコンポーネントベースまたはFormsベースのテンプレートを選択してアダプティブEdge Delivery Servicesを作成する方法について説明します。 また、フォームを AEM Edge Delivery Services に公開することもできます。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: bcf8f9e5273819eaee09875ec81251fe4330701c
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 27%

---


# オーサリングから公開へ：Edge Delivery ServicesでのAEM Forms

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセス権をリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は「adobe」、リポジトリ名は「abc」になります。</span>

Adobe Experience Manager（AEM）を使用すると、魅力的でレスポンシブ、かつ動的なフォームを作成できます。 それぞれ異なる要件やユーザーの専門知識のレベルに適した、複数のオーサリング方法を提供&#x200B;ます。

この記事では、AEM環境内でフォームを作成し、Edge Delivery Servicesを通じてフォームを公開する、アプローチに重点を置いて説明します。 コアコンポーネントベースのテンプレートを使用して構築されたFormsは、AEMとEdge Delivery Servicesの両方で公開でき、柔軟なデプロイが可能です。 これに対し、Edge Delivery Services ベースのテンプレートを使用して作成したフォームは、Edge Delivery Servicesでのみ公開でき&#x200B;す。

![ アダプティブフォームの作成と公開 ](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## AEMでのフォームのオーサリングとEdge Delivery Servicesを使用した公開の利点：

* **既存のAEM ワークフローの保持**：確立されたAEM ワークフローとガバナンス構造を引き続き使用して、コンテンツ作成の一貫性と制御を確保できます。&#x200B;

* **パフォーマンスの向上**:Edge Delivery Servicesを通じて公開すると、レンダリング時間が短縮され、ユーザーエクスペリエンスが向上し、ページ読み込み時間が短縮されます&#x200B;

* **SEO の向上**:Edge Delivery Servicesは、Google Lighthouse のスコアが高いコンテンツを配信するように設計されています。これにより、検索エンジンの最適化が向上し、可視性が向上します。&#x200B;

* **柔軟なデプロイメントオプション**：コアコンポーネントで構築されたFormsは、AEMとEdge Delivery Servicesの両方で公開でき、柔軟なデプロイメント戦略を実現します&#x200B;

## 始める前に

AEMでフォームのオーサリングを開始し、Edge Delivery Servicesを使用してフォームを公開する前に、次の前提条件が満たされていることを確認してください。

* Edge Delivery Services用に Github リポジトリが設定されていることを確認します。
   * リポジトリがない場合は、[ アダプティブ AEM ブロックを使用して新しいForms プロジェクトが事前設定されている ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) 必要があります。
   * リポジトリがある場合は、アダプティブFormsブロックを既存のリポジトリに追加します。 手順について詳しくは、[AEM Forms用Edge Delivery Servicesの概要 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) を参照してください。
* AEM環境と GitHub リポジトリの間の接続を確立します。 [ どうすればよいですか？](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

<!--A decision flow diagram to guide the setup and publishing of Adaptive Forms:

![Github Repository Workflow](/help/edge/assets/repo-workflow.png){width=auto}-->

## AEMでのフォームの作成とEdge Delivery Servicesへの公開

AEMでフォームを作成してEdge Delivery Servicesに公開するには、次の手順に従います。

[1. テンプレートを選択し、フォームを作成する](#choose-a-template-and-create-the-form)

[2. フォームを作成する](#author-the-form)

[3. Edge Delivery Services設定の作成](#create-an-edge-delivery-services-configuration)

[4. フォームを公開する](#publish-a-form)

[5. Edge Delivery Servicesのフォームにアクセスする](#access-the-form-on-edge-delivery-services)

### テンプレートを選択し、フォームを作成します

AEM インスタンス上にフォームを作成し、Edge Delivery Servicesに公開するには、次を使用します。

* Edge Delivery Servicesベースのテンプレート
* コアコンポーネントベースのテンプレート

次の手順を実行してテンプレートを選択し、フォームを作成します。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。ウィザードが開きます。
1. テンプレートを選択します。 次のいずれかを選択できます。
   * **Edge Delivery Servicesベースのテンプレートの場合**

     「**Source**」タブで、**Edge Delivery Servicesベースのテンプレート** を選択します。

     ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png)

     **Edge Delivery Servicesベースのテンプレート** を選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。

      * **コアコンポーネントベースのテンプレートの場合**

     「**Source**」タブで **コアコンポーネントベースのテンプレート** と **テーマ** を選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。

     ![ コアコンポーネントベースのテンプレート ](/help/forms/assets/core-component-based-template.png)

1. （オプション）「**[!UICONTROL データソース]**」タブまたは「**[!UICONTROL 送信]**」タブで、データソースまたは送信アクションを選択できます。
1. （オプション）「**[!UICONTROL 配信]**」タブで、フォームの公開日または非公開日を指定できます。
1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成** ウィザードが次の項目に対して表示されます。

   * **Edge Delivery Services テンプレートベースのフォーム**

      1. 「**名前**」と「**タイトル**」を指定します。
      2. **GitHub URL** を指定します。例えば、GitHub リポジトリの名前が `edsforms` で、アカウント `wkndforms` の下にある場合、URL は次のようになります。
         `https://github.com/wkndforms/edsforms`

         ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png)

         「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

         ![フォームを送信](/help/edge/assets/author-form.png)

   * **コアコンポーネントのテンプレートベースのフォーム**

      1. 「**名前**」と「**タイトル**」を指定します。
      1. アダプティブフォームを保存する場所を「**パス**」フィールドで指定します。

         ![ フォーム作成ウィザード ](/help/forms/assets/create-cc-form.png)

         「**[!UICONTROL 作成]**」をクリックすると、アダプティブフォームエディターでフォームが開き、オーサリングできるようになります。

         ![ アダプティブフォームエディター ](/help/forms/assets/af-editor-form.png)

1. 「**[!UICONTROL 作成]**」をクリックしてフォームを作成します。 ユニバーサルエディターまたはアダプティブフォームエディターを使用してフォームを作成できるようになりました。

### フォームの作成

Edge Delivery Servicesベースのテンプレートを使用して作成されたフォームは、オーサリング用に [ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) で開きます。 ただし、コアコンポーネントベースのテンプレートを使用して作成されたフォームは、オーサリング用にアダプティブフォームエディターで開きます。

Edge Delivery Servicesベースのテンプレート用のユニバーサルエディターまたはコアコンポーネントベースのテンプレート用のアダプティブフォームエディターを使用してフォームを作成するには、次の手順を実行します。

>[!BEGINTABS]

>[!TAB Edge Delivery Servicesベースのテンプレート ]


1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。

   ![コンテンツツリー](/help/edge/assets/content-tree.png)

1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**リストから目的のコンポーネントを追加します。
   ![コンポーネントを追加](/help/edge/assets/add-component.png)

   以下のスクリーンショットは、ユニバーサルエディターで作成した `Registration Form` を示しています。

   ![お問い合わせフォーム](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> ユニバーサルエディターを使用したアダプティブフォームのオーサリング手順について詳しくは、[ ここをクリック ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) してください。

これで、[フォームの送信アクションを設定およびカスタマイズ](/help/edge/docs/forms/universal-editor/submit-action.md)できます。

>[!TAB  コアコンポーネントベースのテンプレート ]

1. **[!UICONTROL コンポーネントをここにドラッグ]** セクションの **コンポーネントを挿入** をクリックします。

   ![ コンポーネントをここにドラッグ ](/help/forms/assets/drag-components-af-editor.png)

1. **アダプティブフォームコンポーネント** リストから目的のコンポーネントを追加します。

   ![コンポーネントを追加](/help/forms/assets/add-component-af.png)

以下のスクリーンショットは、アダプティブフォームエディターで作成した `Enrollment Form` を示しています。

![ アダプティブフォームエディター ](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> コアコンポーネントテンプレートに基づくアダプティブフォームの作成に関する詳細なガイダンスについては、[ ここをクリック ](/help/forms/creating-adaptive-form-core-components.md) してください。

ここで [ フォームの送信アクションを設定 ](/help/forms/configure-submit-actions-core-components.md) できます。

>[!ENDTABS]

### Edge Delivery Services設定の作成

Edge Delivery Servicesでアダプティブフォームを公開するには、AEM インスタンス上にEdge Delivery Services設定を作成する必要があります。 Edge Delivery Services設定を作成するには、以下の手順を実行します。

>[!BEGINTABS]
>[!TAB Edge Delivery Servicesベースのテンプレートを使用して作成されたフォームの場合 ]


Edge Delivery Services ベースのテンプレートをベースとするフォームのEdge Delivery Services設定は、フォームの設定コンテナに自動的に作成されます。

![Edge Delivery Servicesの設定 ](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB  コアコンポーネントベースのテンプレートを使用して作成されたフォームの場合 ]

1. AEM Forms as a Cloud Service オーサーインスタンスで、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Edge Delivery Services 設定]**&#x200B;に移動します。

   ![Edge Delivery Services設定を選択 ](/help/edge/assets/select-eds-conf.png)

1. フォームの名前に一致するフォルダーを選択します。 例えば、フォームの名前が `enrollment-form` の場合は、フォルダー `forms/enrollment-form` を選択し、**[!UICONTROL 作成]**/**[!UICONTROL 設定]** をクリックします。

   ![Edge Delivery Servicesの設定 ](/help/forms/assets/create-eds-conf.png)

1. **[!UICONTROL Edge Delivery Services設定]** をクリックし、**[!UICONTROL プロパティ]** をクリックしてプロパティを開きます。

   ![ 自動作成された設定 ](/help/forms/assets/eds-conf.png)

   Edge Delivery Services設定が表示されます。

1. Edge Delivery Services設定で、以下を指定します。

   * **組織**:GitHub の組織名を指定します。

   * **サイト名**:GitHub リポジトリ名を指定します。
   * **ブランチ**：ブランチ名を指定します。 main ブランチを使用する場合は、テキストボックスを空のままにします。
   * **（オプション）Edge ホスト**:「Edge ホスト」オプションはそのままにしておきます。 フォームはプレビュー（.page）環境とライブ（.live）環境の両方に公開されます。
   * **（オプション）サイト認証トークン**：サイト認証トークンを使用して、AEM インスタンスとEdge Delivery Servicesの間のリクエストを安全に認証します。

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。 設定が作成されます。

>[!ENDTABS]

### フォームの公開

Edge Delivery Servicesでフォームにアクセスするには、フォームを公開する必要があります。

フォームを公開するには、次の手順を実行します。

>[!BEGINTABS]
>[!TAB  ユニバーサルエディター上 ]

1. ユニバーサルエディターの右上隅にある「**[!UICONTROL 公開]**」ボタンをクリックしてフォームを公開します。

![フォームを公開](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> フォームを Edge Delivery Services に公開する方法について詳しくは、[公開とデプロイ](/help/edge/docs/forms/universal-editor/publish-forms.md)の記事を参照してください。

>[!TAB  アダプティブフォームエディター上 ]

1. Experience Manager Forms コンソールで、親フォルダーに移動し、公開するフォームを選択します。

1. ツールバーの「**[!UICONTROL 公開]**」オプションをクリックし、フォームと共に公開されるすべての参照アセットを確認します。

![ アダプティブフォームエディターでのフォームの公開 ](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> アダプティブフォームエディターでフォームを公開する方法については、[Experience Manager Formsでの公開の管理 ](/help/forms/manage-publication.md) を参照してください。

>[!ENDTABS]

## Edge Delivery Servicesのフォームにアクセスする

* **ステージングされたバージョン（テスト用）**：ステージングされたバージョンには、テスト目的でフォームの非公開の作業用バージョンが表示されます。 フォームを公開する前にプレビューするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **ライブバージョン（公開済みフォーム）**：ライブバージョンには、エンドユーザーがアクセスできるフォームの最新公開バージョンが表示されます。 フォームの公開済みライブバージョンにアクセスするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  URL 構造は、ステージングされたバージョンとライブバージョンの両方で同じままです。 ただし、表示されるコンテンツは、コンテキストによって異なります。

以下のスクリーンショットでは、Edge Delivery Servicesベースおよびコアコンポーネントベースのテンプレートを使用して作成されたフォームのステージング済みフォーム URL とライブフォーム URL およびビジュアルプレビューを比較しています。

>[!BEGINTABS]
>[!TAB Edge Delivery Servicesベースのテンプレートを使用して作成されたフォームへのアクセス ]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>バージョン</strong></th>
      <th style="width: 80%;"><strong>画像</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>ステージングされたバージョン</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="登録フォームのステージング版" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>ライブバージョン</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="登録フォームのライブバージョン" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB  コアコンポーネントベースのテンプレートを使用して作成されたフォームへのアクセス ]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>バージョン</strong></th>
      <th style="width: 80%;"><strong>画像</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ステージングされたバージョン</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="登録フォームのステージング版" style="width: 100%; height: auto;" /></td>
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
