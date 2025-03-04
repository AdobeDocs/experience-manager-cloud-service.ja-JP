---
title: ユニバーサルエディターを使用してスタンドアロンのアダプティブFormsを作成する方法
description: この記事では、AEM オーサーインスタンスでフォーム作成ウィザードを使用してアダプティブFormsを作成し、フォームをAEM Edge Delivery Servicesに公開する方法について説明します。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: d7e59c16e90e3632140eae08dc2c25b2dd1df5a7
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 49%

---


# ユニバーサルエディターを使用したスタンドアロンフォームの作成（WYSIWYG）

<span class="preview"> この機能は、早期アクセスプログラムを通じて利用できます。 アクセスをリクエストするには、公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に、GitHub の組織名とリポジトリ名を記載したメールを送信します。 例えば、リポジトリ URL がhttps://github.com/adobe/abcの場合、組織名は adobe で、リポジトリ名は abc.</span> です

この記事では、フォーム作成ウィザードからEdge Delivery Servicesベースのテンプレートを選択してユニバーサルエディターを使用してスタンドアロンフォームを作成するプロセスについて説明します。 作成したフォームをユニバーサルエディターと共にAEM Edge Delivery Servicesに公開することもできます。

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

開始する前に、使用可能な Forms コンポーネントのタイプについて学習します。

* [Edge Delivery Services for AEM Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) は、作成者がユニバーサルエディターを使用して新しいフォームを迅速に更新、公開、起動できる、迅速な開発環境を可能にする構成可能なサービスセットです。 ユニバーサルエディターは、使いやすい視覚的なWYSIWYG インターフェイスを使用して、Adobe Edge 配信サービスのフォームを簡単に作成できます。

* [アダプティブフォームコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)：標準化されたデータキャプチャコンポーネントです。 これらのコンポーネントは、デジタル登録エクスペリエンスのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。 開発者は、これらのコンポーネントを簡単にカスタマイズし、スタイルを設定できます。 次にアクセスできます： [https://aemcomponents.dev/](https://aemcomponents.dev/) 使用可能なコアコンポーネントの動作を表示するには **Adobeでは、アダプティブFormsの開発に、最新の拡張可能なコンポーネントを使用することをお勧めします**.

* [アダプティブフォーム基盤コンポーネント](/help/forms/creating-adaptive-form.md)：従来の（古い）データキャプチャコンポーネントです。 引き続きこれらを使用して、既存の基盤コンポーネントベースのアダプティブフォームを編集できます。 新しいフォームを作成する場合は、[アダプティブフォームコアコンポーネントを使用してアダプティブフォームを作成することをお勧めします。](#create-an-adaptive-form-core-components)

AEM Forms には、アダプティブフォームブロックと呼ばれるブロックが用意されており、データを取得して保存する Edge Delivery Services フォームを簡単に作成できます。[ アダプティブAEM ブロックを使用して事前設定された新しいForms プロジェクトを作成する ](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) または [ 既存のAEM サイトプロジェクトにアダプティブForms ブロックを追加する ](#add-adaptive-forms-block-to-your-existing-aem-project) ことができます。

![Github リポジトリーワークフロー ](/help/edge/assets/repo-workflow.png)

## 前提条件

* [GitHub リポジトリを設定 ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) して、AEM環境と GitHub リポジトリの間の接続を確立します。
* 既に Edge Delivery Services を使用している場合は、最新バージョンの[アダプティブフォームブロック](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)を GitHub リポジトリに追加します。
* AEM Forms オーサーインスタンスには、Edge Delivery Services に基づくテンプレートが含まれます。 使用する環境に[最新バージョンのコアコンポーネント](https://github.com/adobe/aem-core-forms-components)がインストールされていることを確認します。
* AEM Forms as a Cloud Service オーサーインスタンスの URL と GitHub リポジトリをすぐに使用できる状態にします。

## ユニバーサルエディターを使用したアダプティブフォームの作成

ユニバーサルエディターを使用すると、テキストフィールド、チェックボックス、ラジオボタンなどの既製のコンポーネントを使用して、レスポンシブでインタラクティブなスタンドアロンフォームを簡単に作成できます。 動的ルール、スムーズなデータ統合、カスタマイズオプションなどの強力な機能を提供し、正確な要件に従ってフォームを作成できます。

>[!NOTE]
>
> [ ユニバーサルエディターのAEM サイトテンプレートを使用してEdge Delivery Services サイトでフォームを作成し、Edge Delivery Servicesに公開する ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project) こともできます。

ユニバーサルエディターを使用してスタンドアロンのアダプティブフォームを作成するには、次の手順を実行します。

1. **AEM Forms オーサーインスタンスでのアダプティブフォームの作成**

   1. AEM Forms as a Cloud Service オーサーインスタンスにアクセスします。
   1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 ウィザードが開きます。
   1. 「**Source**」タブで、Edge Delivery Services ベースのフォームテンプレートを選択します。

      ![EDS Formsの作成 ](/help/edge/assets/create-eds-forms.png)

   1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
   1. **GitHub URL** を指定します。 例えば、GitHub リポジトリの名前が `edsforms` の場合は、アカウント `wkndforms` の下に配置され、URL はとなります。
      `https://github.com/wkndforms/edsforms`
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![ フォーム作成ウィザード ](/help/edge/assets/create-form-wizard.png)

      「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

      ![ フォームのオーサリング ](/help/edge/assets/author-form.png)

      <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

      「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

1. **ユニバーサルエディターでのフォームの作成**

   1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。

      ![コンテンツツリー](/help/edge/assets/content-tree.png)

   1. 「**[!UICONTROL 追加]**」アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

      ![コンポーネントを追加](/help/edge/assets/add-component.png)

   1. 追加されたアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]**&#x200B;を使用して、そのプロパティを更新します。

      ![プロパティを開く](/help/edge/assets/component-properties.png)

      次のスクリーンショットは、ユニバーサルエディターで作成した単純な `Registration Form` フォームを示しています。

      ![ お問い合わせフォーム ](/help/edge/assets/contact-us.png)

      これで [ フォーム送信アクションを設定およびカスタマイズ ](/help/edge/docs/forms/universal-editor/submit-action.md) できます。


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

## フォームを公開します

次に、ユニバーサルエディターの右上隅にある「**[!UICONTROL 公開]**」ボタンをクリックして、スタンドアロンフォームをEdge Delivery Servicesに公開します。

![フォームを公開](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> フォームをEdge Delivery Servicesに公開する方法については、[ 公開とデプロイ ](/help/edge/docs/forms/universal-editor/publish-forms.md) の記事を参照してください。

Edge Delivery Services のフォームにアクセスする方法は、次のとおりです。

* **ステージングされたバージョン（テスト用）**：ステージングされたバージョンには、テスト目的でフォームの非公開の作業用バージョンが表示されます。 フォームを公開する前にプレビューするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「edsforms」で、アカウントが「wkndforms」の下にあり、「main」ブランチとフォームを「登録フォーム」として使用している場合、ステージングバージョンの URL は次のようになります。
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **ライブバージョン（公開済みフォーム）**：ライブバージョンには、エンドユーザーがアクセスできるフォームの最新公開バージョンが表示されます。 フォームの公開済みライブバージョンにアクセスするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「edsforms」で、アカウントが「wkndforms」の下にあり、「main」ブランチとフォームを「登録フォーム」として使用している場合、ステージングバージョンの URL は次のようになります。
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

URL 構造は、ステージングされたバージョンとライブバージョンの両方で同じままです。 ただし、表示されるコンテンツはコンテキストに基づいて異なります。

![ 公開されたフォームを表示 ](/help/edge/assets/eds-view-publish-form.png)

## トラブルシューティング

フォームの読み込みに問題がありますか？ 一般的な問題と修正方法を以下に示します。

* **フォーム URL**：フォームの URL の末尾に「.html」拡張子が含まれていないことを再確認します。 Edge Deliver Service では、この拡張機能は必要ありません。

* **AEM オーサー URL**：`fstab.yaml` ファイルにリストされている AEM オーサー URL が正しい形式であることを確認します。 これには、次の詳細を含める必要があります。

   * 正しい GitHub 所有者
   * 正しいリポジトリ名
   * Edge Delivery Services に使用している特定の分岐

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## フォームの作成を開始

{{universal-editor-see-also}}


