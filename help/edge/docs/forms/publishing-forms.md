---
title: Edge Delivery Services 向けのフォームの公開
description: フォームの公開が Edge Delivery Services と連携する仕組みと、AEM フォームを Edge Delivery Services と共に公開する方法について説明します。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: b90c27e3-22ea-4b18-b16e-a5c5a0ed58b8
source-git-commit: 67384a9141ced3bf5be63c8489dd5c329a288056
workflow-type: ht
source-wordcount: '993'
ht-degree: 100%

---

# Edge Delivery Services 向けのフォームの公開

この記事では、AEM Edge Delivery Services へのフォームの公開プロセスについて説明します。
フォームを Edge Delivery Services に公開するには、まず AEM 環境と GitHub リポジトリの間の接続を確立する必要があります。 接続すると、WYSIWYG（What You See Is What You Get）アプローチに従うユニバーサルエディターを使用してフォームを作成でき、Sites とのシームレスで一貫性のあるユーザーエクスペリエンスを実現します。

## 前提条件

* アダプティブフォームを初めて使用する場合 提供されている[チュートリアル](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)に従って GitHub リポジトリを設定します。
* 既に Edge Delivery Services を使用している場合は、最新バージョンの[アダプティブフォームブロック](/help/edge/docs/forms/tutorial.md#)を GitHub リポジトリに追加します。
* AEM Forms オーサーインスタンスには、Edge Delivery Services に基づくテンプレートが含まれます。 使用する環境に[最新バージョンのコアコンポーネント](https://github.com/adobe/aem-core-forms-components)がインストールされていることを確認します。
* AEM Forms as a Cloud Service オーサーインスタンスの URL と GitHub リポジトリをすぐに使用できる状態にします。

## Edge Delivery Services 向けのフォームの公開

Edge Delivery Services 向けのフォームを公開するには、次の手順を実行します。

[1. GitHub リポジトリを AEM インスタンスにリンク](#link-github-repository-to-aem-instance)

[2. AEM インスタンスを GitHub リポジトリにリンク](#link-aem-instance-to-github-repository)

### GitHub リポジトリを AEM インスタンスにリンク

[GitHub リポジトリ上のプロジェクト](/help/edge/docs/forms/tutorial.md)を AEM Forms オーサーインスタンスにリンクするには、次の手順を実行します。

1. Edge Delivery Services 用に作成または設定した GitHub リポジトリに移動します。
1. `fstab.yaml` ファイルを編集用に開きます。
1. GitHub リポジトリ内の `fstab.yaml` ファイルを、AEM Forms as a Cloud Service インスタンスの URL で更新します。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例えば、GitHub リポジトリの名前が「aemcrosswalk」で、アカウント「wkndform」の下にあり、「main」分岐を使用している場合、オーサーインスタンスの URL は次のようになります。

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. `fstab.yaml` ファイルへの変更をコミットします。

### AEM インスタンスを GitHub リポジトリにリンク

AEM Forms オーサーインスタンスを [GitHub リポジトリ上のプロジェクト](/help/edge/docs/forms/tutorial.md)にリンクするには、次の手順を実行します。

[1. Edge Delivery Services テンプレートに基づいてアダプティブフォームを作成](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. AEMオーサーインスタンスでフォームの設定コンテナを見つける](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. ユニバーサルエディターでフォームを作成](#3-author-the-form-in-the-universal-editor)

[4. フォームを公開およびプレビュー](#4-publish-and-preview-the-form)

#### 1. Edge Delivery Services テンプレートに基づいてアダプティブフォームを作成

1. AEM Forms as a Cloud Service オーサーインスタンスにアクセスします。
1. **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。1. **[!UICONTROL 作成]**／**[!UICONTROL アダプティブフォーム]**&#x200B;を選択します。 ウィザードが開きます。 「ソース」タブで、Edge Delivery Services ベースのフォームテンプレートを選択します。

   ![EDS フォームを作成](/help/edge/assets/create-eds-forms.png) {width=50%, align-center}

1. 「**[!UICONTROL 作成]**」をクリックすると、**フォームを作成**&#x200B;ウィザードが表示されます。
1. **GitHub URL** を指定します。 例えば、GitHub リポジトリの名前が「aemcrosswalk」で、アカウント「wkndform」の下にある場合、URL は次のようになります。
   `https://github.com/wkndform/aemcrosswalk`
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![フォームを作成ウィザード](/help/edge/assets/create-form-wizard.png) {width=50%, align-center}

   「**[!UICONTROL 作成]**」をクリックするとすぐに、フォームがオーサリング用のユニバーサルエディターで開きます。

   ![フォームをオーサリング](/help/edge/assets/author-form.png) {width=50%, align-center}

   >[!NOTE]
   >
   > Edge Delivery Services テンプレートに基づくフォームの Edge Delivery Services 設定は、フォームの設定コンテナに自動的に作成されます。

#### 2. AEMオーサーインスタンスでフォームの設定コンテナを見つける

1. AEM Forms as a Cloud Service オーサーインスタンスで、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Edge Delivery Services 設定]**&#x200B;に移動します。
1. フォームの名前に一致するフォルダーを選択します。 例えば、フォームの名前が「contact-us」の場合は、フォルダー `forms/contact-us` を選択し、設定を選択して、設定を公開します。

   ![Edge Delivery Services 設定](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. 「**[!UICONTROL プロパティ]**」をクリックして、設定を確認します。\
   ![自動作成された設定](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   「Edge ホスト」オプションはそのままにしておくことができます。 フォームは、プレビュー（.page）環境とライブ（.live）環境の両方に公開されます。

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。 設定が保存されました。

#### 3. ユニバーサルエディターでフォームを作成

「**[!UICONTROL 作成]**」をクリックすると、フォームがオーサリング用のユニバーサルエディターで開きます。

1. コンテンツブラウザーを開き、**コンテンツツリー**&#x200B;の&#x200B;**[!UICONTROL アダプティブフォーム]**&#x200B;コンポーネントに移動します。

   ![コンテンツツリー](/help/edge/assets/content-tree.png){width=50%, align-center}

1. **[!UICONTROL 追加]**&#x200B;アイコンをクリックし、**アダプティブフォームコンポーネント**&#x200B;リストから目的のコンポーネントを追加します。

   ![コンポーネントを追加](/help/edge/assets/add-component.png){width=50%, align-center}

1. 追加されたアダプティブフォームコンポーネントを選択し、**[!UICONTROL プロパティ]**&#x200B;を使用して、そのプロパティを更新します。

   ![プロパティを開く](/help/edge/assets/component-properties.png){width=50%, align-center}

   以下のスクリーンショットは、ユニバーサルエディターで作成したシンプルな「お問い合わせ」フォームを示しています。

   ![お問い合わせフォーム](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. フォームを公開およびプレビュー

次に、ユニバーサルエディターの右上隅にある「**[!UICONTROL 公開]**」ボタンをクリックして、フォームを Edge Delivery Services に公開します。

![フォームを公開](/help/edge/assets/publish-form.png){width=50%, align-center}


Edge Delivery Services のフォームにアクセスする方法は、次のとおりです。

* **ステージングされたバージョン（テスト用）**：ステージングされたバージョンには、テスト目的でフォームの非公開の作業用バージョンが表示されます。 フォームを公開する前にプレビューするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「aemcrosswalk」で、アカウント「wkndform」の下にあり、「main」分岐と「お問い合わせ」フォームを使用している場合、ステージングされたバージョンの URL は次のようになります：
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **ライブバージョン（公開済みフォーム）**：ライブバージョンには、エンドユーザーがアクセスできるフォームの最新公開バージョンが表示されます。 フォームの公開済みライブバージョンにアクセスするには、次の URL 形式を使用します。

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例えば、プロジェクトのリポジトリの名前が「aemcrosswalk」で、アカウント「wkndform」の下にあり、「main」分岐と「お問い合わせ」フォームを使用している場合、ステージングされたバージョンの URL は次のようになります：
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

URL 構造は、ステージングされたバージョンとライブバージョンの両方で同じままです。 ただし、表示されるコンテンツはコンテキストに基づいて異なります。

![公開されたフォームを表示](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## トラブルシューティング

フォームの読み込みに問題がありますか？ 一般的な問題と修正方法を以下に示します。

* **フォーム URL**：フォームの URL の末尾に「.html」拡張子が含まれていないことを再確認します。 Edge Deliver Service では、この拡張機能は必要ありません。

* **AEM オーサー URL**：`fstab.yaml` ファイルにリストされている AEM オーサー URL が正しい形式であることを確認します。 これには、次の詳細を含める必要があります。

   * 正しい GitHub 所有者
   * 正しいリポジトリ名
   * Edge Delivery Services に使用している特定の分岐

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 関連トピック

{{see-more-forms-eds}}
