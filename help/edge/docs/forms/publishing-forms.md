---
title: Edge Delivery Services向けのFormsの公開
description: フォームの公開がEdge Delivery Servicesと連携する仕組みと、AEM forms をEdge Delivery Servicesと共に公開する方法について説明します。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# Edge Delivery Services向けのFormsの公開

この記事では、AEM Edge Delivery Servicesへのフォームの公開プロセスについて説明します。
フォームをEdge Delivery Servicesに公開するには、まずAEM環境と GitHub リポジトリの間の接続を確立する必要があります。 接続したら、ユニバーサルエディターを使用してフォームを作成できます。このエディターはWYSIWYG（What You See Is What You Get）アプローチに従うため、Sites とのシームレスで一貫性のあるユーザーエクスペリエンスが実現します。

## 前提条件

* アダプティブFormsを初めて使用する場合は、 提供された [ チュートリアル ](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) に従って、GitHub リポジトリを設定します。
* 既にEdge Delivery Servicesを使用している場合は、最新バージョンの [ アダプティブ Forms ブロック ](/help/edge/docs/forms/tutorial.md#) を GitHub リポジトリに追加してください。
* AEM Forms オーサーインスタンスには、Edge Delivery Servicesに基づいたテンプレートが含まれます。 お使いの環境に [ コアコンポーネントの最新バージョン ](https://github.com/adobe/aem-core-forms-components) がインストールされていることを確認します。
* AEM Formsas a Cloud Serviceのオーサーインスタンスと GitHub リポジトリの URL を手元に用意しておいてください。

## Edge Delivery Services向けPublish Forms

Edge Delivery Services用のフォームを公開するには、次の手順を実行します。

[1. GitHub リポジトリをAEM インスタンスにリンクする](#link-github-repository-to-aem-instance)

[2. AEM インスタンスを GitHub リポジトリにリンクする](#link-aem-instance-to-github-repository)

### GitHub リポジトリのAEM インスタンスへのリンク

[GitHub リポジトリ上のプロジェクト ](/help/edge/docs/forms/tutorial.md) をAEM Forms オーサーインスタンスにリンクするには、次の手順を実行します。

1. Edge Delivery Services用に作成または設定した GitHub リポジトリに移動します。
1. `fstab.yaml` ファイルを編集用に開きます。
1. GitHub リポジトリの `fstab.yaml` ファイルをAEM Formsas a Cloud Serviceインスタンスの URL で更新します。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例えば、GitHub リポジトリーの名前が「aemcrosswalk」で、「wkndform」のアカウントの下にあり、「main」ブランチを使用している場合、オーサーインスタンスの URL は次のようになります。

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. 変更を `fstab.yaml` ファイルにコミットします。

### AEM インスタンスを GitHub リポジトリにリンクする

AEM Forms オーサーインスタンスを [GitHub リポジトリ上のプロジェクト ](/help/edge/docs/forms/tutorial.md) にリンクするには、次の手順を実行します。

[1. Edge Delivery Servicesテンプレートに基づくアダプティブフォームの作成](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. AEM オーサーインスタンスでフォームの設定コンテナを見つけます。](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. ユニバーサルエディターでのフォームの作成](#3-author-the-form-in-the-universal-editor)

[4. Publishとフォームのプレビュー](#4-publish-and-preview-the-form)

#### 1. Edge Delivery Servicesテンプレートに基づくアダプティブフォームの作成

1. AEM Formsのas a Cloud Serviceオーサーインスタンスにアクセスします。
1. **[!UICONTROL Adobe Experience Manager]** /**[!UICONTROL Forms]** / **[!UICONTROL Formsとドキュメント]**.1 を選択します。**[!UICONTROL 作成]** / **[!UICONTROL アダプティブForms]** を選択します。 ウィザードが開きます。「Source」タブで、Edge Delivery Servicesベースのフォームテンプレートを選択します。

   ![EDS Formsを作成 ](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. 「**[!UICONTROL 作成]**」をクリックすると、「**フォームを作成** ウィザードが表示されます。
1. **GitHub URL** を指定します。 例えば、GitHub リポジトリの名前が「aemcrosswalk」の場合は、アカウント「wkndForm」の下に配置されています。URL は次のとおりです。
   `https://github.com/wkndform/aemcrosswalk`
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![ フォーム作成ウィザード ](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![ フォームのオーサリング ](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > Edge Delivery Servicesテンプレートに基づくフォームのEdge Delivery Services設定は、フォームの設定コンテナで自動的に作成されます。

#### 2. AEM オーサーインスタンスでフォームの設定コンテナを見つけます。

1. AEM Formsas a Cloud Serviceオーサーインスタンスで **[!UICONTROL ツール]**/**[!UICONTROL Cloud Service]**/**[!UICONTROL Edge Delivery Services設定]** に移動します。
1. フォーム名と一致するフォルダーを選択します。 例えば、フォームの名前が「contact-us」の場合は、フォルダー `forms/contact-us` を選択し、設定を選択して設定を公開します。

   ![Edge Delivery Services設定 ](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. **[!UICONTROL プロパティ]** をクリックして、設定を確認します。\
   ![ 自動作成された設定 ](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   「Edge ホスト」オプションはそのままにすることができます。 フォームは、プレビュー（.page）環境とライブ（.live）環境の両方に公開されます。

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。設定が保存されます。

#### 3. ユニバーサルエディターでのフォームの作成

**[!UICONTROL 作成]** をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

1. コンテンツブラウザーを開き、**[!UICONTROL コンテンツツリー** の **アダプティブフォーム]** コンポーネントに移動します。

   ![ コンテンツツリー ](/help/edge/assets/content-tree.png){width=50%, align-center}

1. **[!UICONTROL 追加]** アイコンをクリックし、**アダプティブフォームコンポーネント** リストから目的のコンポーネントを追加します。

   ![ コンポーネントを追加 ](/help/edge/assets/add-component.png){width=50%, align-center}

1. 追加されたアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]** を使用してそのプロパティを更新します。

   ![ プロパティを開く ](/help/edge/assets/component-properties.png){width=50%, align-center}

   次のスクリーンショットは、ユニバーサルエディターで作成したシンプルな「お問い合わせ」フォームを示しています。

   ![ お問い合わせフォーム ](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Publishとフォームのプレビュー

次に、ユニバーサルエディターの右上隅にある「**[!UICONTROL Publish]**」ボタンをクリックして、フォームをEdge Delivery Servicesに公開します。

![ フォームを公開 ](/help/edge/assets/publish-form.png){width=50%, align-center}


Edge Delivery Servicesのフォームにアクセスする方法は次のとおりです。

* **ステージバージョン（テスト用）**：ステージバージョンは、テスト目的でフォームの非公開の作業用バージョンを表示します。 以下の URL 形式を使用して、運用開始前にフォームをプレビューします。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「aemcrosswalk」で、「wkndform」アカウントの下にあり、「main」ブランチとフォームを「contact us」として使用している場合、ステージングバージョンの URL は次のようになります。
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **ライブバージョン （公開済みフォーム）**:   ライブバージョンには、フォームの最新の公開バージョンが表示され、エンドユーザーからアクセスできます。 次の URL 形式を使用して、フォームの公開済みライブバージョンにアクセスします。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「aemcrosswalk」で、「wkndform」アカウントの下にあり、「main」ブランチとフォームを「contact us」として使用している場合、ステージングバージョンの URL は次のようになります。
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

ステージングバージョンとライブバージョンの URL 構造は同じままです。 ただし、表示されるコンテンツは、コンテキストに基づいて異なります。

![ 公開されたフォームを表示 ](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## トラブルシューティング

フォームの読み込みに問題がありますか？ 一般的な問題と修正方法を次に示します。

* **フォーム URL**：フォーム URL の末尾に「.html」拡張子が含まれていないことを再確認します。 Edge配信サービスには、この拡張機能は必要ありません。

* **AEM オーサー URL** L: `fstab.yaml` ファイルにリストされているAEM オーサー URL の形式が正しいことを確認してください。 これには、次の詳細が含まれる必要があります。

   * 正しい GitHub 所有者
   * 正しいリポジトリ名
   * Edge Delivery Servicesに使用する特定のブランチ

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 関連トピック

{{see-more-forms-eds}}