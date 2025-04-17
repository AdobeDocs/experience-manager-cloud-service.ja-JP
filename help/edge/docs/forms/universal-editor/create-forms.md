---
title: ユニバーサルエディターを使用して Edge Delivery Services テンプレートに基づいてスタンドアロンフォームを作成する方法
description: この記事では、フォーム作成ウィザードで Edge Delivery Services ベースのテンプレートを選択して、ユニバーサルエディターを使用してフォームを作成する方法について説明します。また、フォームを AEM Edge Delivery Services に公開することもできます。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: b0cedf31a8759cdf403e1e7d6aadcab3bba03bab
workflow-type: ht
source-wordcount: '1060'
ht-degree: 100%

---

# ユニバーサルエディターによるアダプティブフォームの作成

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセス権をリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は「adobe」、リポジトリ名は「abc」になります。</span>

ユニバーサルエディターは、フォームを編集する WYSIWYG（見たままが得られる）エクスペリエンスを備えた多用途なビジュアルエディターです。テキストボックス、ラジオボタン、チェックボックスなどの使用可能なアダプティブフォームコンポーネントを使用して、ドラッグ＆ドロップ機能で、レスポンシブでユーザーにわかりやすいフォームを簡単に作成できます。

AEM には、アダプティブフォームブロックと呼ばれるブロックが用意されており、ユニバーサルエディターを使用して、データを取得して保存する Edge Delivery Services フォームを簡単に作成できます。[アダプティブフォームブロックで事前設定済みの新しい AEM プロジェクトを作成](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)することも、[アダプティブフォームブロックを既存の AEM サイトプロジェクトに追加](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)することもできます。

![Github リポジトリのワークフロー](/help/edge/assets/repo-workflow.png)

この記事では、フォーム作成ウィザードから Edge Delivery Services ベースのテンプレートを選択して、ユニバーサルエディターを使用してスタンドアロンフォームの作成とオーサリングを行うプロセスについて説明します。

## 前提条件

* [GitHub リポジトリを設定](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)して、AEM 環境と GitHub リポジトリの間の接続を確立します。
* 既に Edge Delivery Services を使用している場合は、最新バージョンの[アダプティブフォームブロック](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)を GitHub リポジトリに追加します。
* AEM Forms オーサーインスタンスには、Edge Delivery Services に基づくテンプレートが含まれます。 使用する環境に[最新バージョンのコアコンポーネント](https://github.com/adobe/aem-core-forms-components)がインストールされていることを確認します。
* AEM Forms as a Cloud Service オーサーインスタンスの URL と GitHub リポジトリをすぐに使用できる状態にします。

## ユニバーサルエディターでのフォームの操作

ユニバーサルエディターを使用すると、レスポンシブでインタラクティブなスタンドアロンのフォームを簡単に作成できます。ユニバーサルエディターのフォームに対して、次のアクションを実行できます。
* [フォームの作成](#create-a-form)
* [フォームのオーサリング](#author-a-form)
* [フォームの公開](#publish-a-form)
* [フォームの管理](#manage-a-form)

>[!NOTE]
>
> また、[ユニバーサルエディターの Edge Delivery Services サイトテンプレートを使用して AEM サイトでフォームを作成し、Edge Delivery Services に公開](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project)することもできます。


### フォームの作成

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。ウィザードが開きます。
1. 「**ソース**」タブで、Edge Delivery Services ベースのフォームテンプレートを選択します。

   ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png)


   Edge Delivery Services ベースのテンプレートを選択すると、「**[!UICONTROL 作成]**」ボタンが有効になります。
1. （オプション）「**[!UICONTROL データソース]**」タブまたは「**[!UICONTROL 送信]**」タブで、データソースまたは送信アクションを選択できます。
1. （オプション）「**[!UICONTROL 配信]**」タブで、フォームの公開日または非公開日を指定できます。

1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
1. 「**名前**」と「**タイトル**」を指定します。
1. **GitHub URL** を指定します。例えば、GitHub リポジトリの名前が `edsforms` で、アカウント `wkndforms` の下にある場合、URL は次のようになります。
   `https://github.com/wkndforms/edsforms`
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png)

   「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![フォームを送信](/help/edge/assets/author-form.png)

   <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

   「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

### フォームのオーサリング

1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。

   ![コンテンツツリー](/help/edge/assets/content-tree.png)

1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

   ![コンポーネントを追加](/help/edge/assets/add-component.png)

1. 追加されたアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]**&#x200B;を使用して、そのプロパティを更新します。

   ![プロパティを開く](/help/edge/assets/component-properties.png)

   以下のスクリーンショットは、ユニバーサルエディターで作成したシンプルな `Registration Form` フォームを示しています。

   ![お問い合わせフォーム](/help/edge/assets/contact-us.png)

   これで、[フォームの送信アクションを設定およびカスタマイズ](/help/edge/docs/forms/universal-editor/submit-action.md)できます。


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

### フォームの公開

次に、ユニバーサルエディターの右上隅にある「**[!UICONTROL 公開]**」ボタンをクリックして、スタンドアロンのフォームを Edge Delivery Services に公開します。

![フォームを公開](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> フォームを Edge Delivery Services に公開する方法について詳しくは、[公開とデプロイ](/help/edge/docs/forms/universal-editor/publish-forms.md)の記事を参照してください。

Edge Delivery Services のフォームにアクセスする方法は、次のとおりです。

* **ステージングされたバージョン（テスト用）**：ステージングされたバージョンには、テスト目的でフォームの非公開の作業用バージョンが表示されます。 フォームを公開する前にプレビューするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「edsforms」で、アカウント「wkndforms」の下にあり、「main」分岐とフォームを「登録フォーム」として使用している場合、ステージングされたバージョンの URL は次のようになります。
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **ライブバージョン（公開済みフォーム）**：ライブバージョンには、エンドユーザーがアクセスできるフォームの最新公開バージョンが表示されます。 フォームの公開済みライブバージョンにアクセスするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「edsforms」で、アカウント「wkndforms」の下にあり、「main」分岐とフォームを「登録フォーム」として使用している場合、ステージングされたバージョンの URL は次のようになります。
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

URL 構造は、ステージングされたバージョンとライブバージョンの両方で同じままです。 ただし、表示されるコンテンツはコンテキストに基づいて異なります。

![公開済みフォームを表示](/help/edge/assets/eds-view-publish-form.png)

### フォームの管理

AEM Forms ユーザーインターフェイスを使用して、フォームに対して複数の操作を実行できます。

1. AEM Forms as a Cloud Service オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。

1. フォームを選択すると、選択したフォームに対して実行できる次の操作がツールバーに表示されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>編集</p> </td>
   <td><p>フォームを編集モードで開きます。<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>プロパティ</p> </td>
   <td><p>フォームのプロパティを変更するオプションを指定します。<br /> <br /> </p> </td>
  </tr>
  <td><p>コピー</p> </td>
   <td><p> フォームを目的の場所にコピー＆ペーストするオプションを指定します。<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>プレビュー</p> </td>
   <td><p>フォームを HTML としてプレビューするか、XML ファイルのデータをフォームと結合してカスタムプレビューを実行するオプションを指定します。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>ダウンロード</p> </td>
   <td><p>選択されているフォームをダウンロードします。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>レビューの開始／レビューの管理</p> </td>
   <td><p>選択されているフォームのレビューを開始したり管理したりできます。<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>-->
  <tr>
   <td><p>公開／非公開</p> </td>
   <td><p>選択されているフォームを公開／非公開します。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>削除</p> </td>
   <td><p>選択されているフォームを削除します。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>比較</p> </td>
   <td><p>プレビュー目的で 2 つの異なるフォームを比較します。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## トラブルシューティング

フォームの読み込みに問題がありますか？ 一般的な問題と修正方法を以下に示します。

* **フォーム URL**：フォームの URL の末尾に「.html」拡張子が含まれていないことを再確認します。 Edge Deliver Service では、この拡張機能は必要ありません。

* **AEM オーサー URL**：`fstab.yaml` ファイルにリストされている AEM オーサー URL が正しい形式であることを確認します。 これには、次の詳細を含める必要があります。

   * 正しい GitHub 所有者
   * 正しいリポジトリ名
   * Edge Delivery Services に使用している特定の分岐

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## フォームの作成の開始

{{universal-editor-see-also}}
