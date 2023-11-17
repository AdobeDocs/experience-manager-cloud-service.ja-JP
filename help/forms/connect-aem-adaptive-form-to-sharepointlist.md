---
title: AEMアダプティブフォームをMicrosoft&reg; SharePointリストに接続する方法
description: アダプティブフォームをMicrosoft&reg; SharePointリストに接続します。 Microsoft&reg; SharePointリストを設定し、設定を使用してフォームデータモデルを作成する方法を説明します。 さらに、FDM をアダプティブフォームに統合する方法も説明します。
role: User, Developer
keywords: AEMアダプティブフォームをMicrosoft SharePointリストに接続し、アダプティブフォームをMicrosoft SharePointリストに接続し、AEMアダプティブフォームをMicrosoft SharePointリストに統合し、アダプティブフォームをMicrosoftリストに統合し、アダプティブフォームからSharePointリストにデータを送信しAEMます。
hide: true
hidefromToC: true
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 5%

---


# アダプティブフォームのMicrosoft® SharePointリストへの接続

<span class="preview"> これはプレリリース機能で、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

**Microsoft® SharePoint**:Microsoft® SharePointは、すべてのチーム、部門、部門に動的で効率的なチームサイトを提供することで、コラボレーションを可能にします。 任意の Web ブラウザー (Microsoft® Edge、Internet Explorer、Chrome、Firefox など ) を使用して、任意のデバイスから情報を保存、整理、共有、アクセスするために使用されます。 の 2 つの主要な構成要素 **Microsoft® SharePoint** は次のとおりです。

* **Microsoft® SharePoint Document Library**:Microsoft® SharePointドキュメントライブラリには、ファイルとフォルダーのリストと、そのキー情報（最終変更日やファイルの所有者など）が表示されます。 この機能により、ファイルの整理とナビゲーションが容易になります。
の統合方法の手順については、 **Microsoft® SharePoint Document Library** アダプティブフォームを使用する場合、 [アダプティブフォーム送信アクション](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) 記事。

* **Microsoft® SharePoint List**:Microsoft® SharePointリストはデータの集まりです。 様々なタイプのデータに列を追加し、データを効果的に表示するビューを作成できます。 リストのグループ化、フィルタリング、並べ替え、書式設定を簡単におこなえます。

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## アダプティブフォームをMicrosoft® SharePointリストに接続するための前提条件 {#prerequisites}

アダプティブフォームをMicrosoft® SharePointリストに接続する前に、次の手順を実行します。

1. [Microsoftの設定](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [Microsoftを使用してフォームデータモデルを作成する](/help/forms/create-form-data-models.md)
1. [データを取得して送信するためのフォームデータモデルの設定](/help/forms/work-with-form-data-model.md#configure-services)
1. [アダプティブフォームを作成](/help/forms/creating-adaptive-form-core-components.md)

次の操作が可能になりました。

* [Connect Microsoft](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [Connect Microsoft](#connect-sharepoint-list-workflow)

## アダプティブフォームのMicrosoft® SharePointリストへの接続 {#connect-af-sharepoint-list}

Microsoft® SharePointリストをアダプティブフォームに統合するには [フォームデータモデルを使用するためのアダプティブフォームの設定](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

フォームデータモデルを使用するようアダプティブフォームを設定すると、次のことが可能になります。

* [フォームデータモデルを使用した送信アクションの設定](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [フォームデータモデルを呼び出すためのルールエディターの設定](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## Microsoft® SharePointリストをAEMワークフローに接続 {#connect-sharepoint-list-workflow}

Microsoft® SharePointリストをAEMワークフローに統合するには：

1. [フォームデータモデルを呼び出すためのワークフローを作成する](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=ja#extending-aem)

   <!--
    To create a workflow with the editor:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [AEM Workflow を呼び出すための送信アクションの設定](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


方法を学ぶ [AEM Workflow を使用](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) アダプティブフォーム内のコンテンツの共同作業、管理、処理を行う。

## ベストプラクティス {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft&reg; SharePoint List rather than Microsoft&reg; SharePoint Document Library. -->
* Microsoft® SharePointリストでは、次の列タイプはサポートされていません。
   * 画像列
   * メタデータ列
   * ユーザー列
   * 外部データ列

## 関連トピック {#see-also}

* [コアコンポーネントベースのアダプティブフォームの作成](/help/forms/creating-adaptive-form-core-components.md)
* [データソースの設定](/help/forms/configuring-submit-actions.md)
* [フォームデータモデルの作成](/help/forms/create-form-data-models.md)
* [Forms中心のAEM Workflows — ステップリファレンスを使用して、ビジネスプロセスを自動化します。](/help/forms/aem-forms-workflow-step-reference.md)
* [アダプティブフォーム用のカスタム送信アクションの作成](/help/forms/custom-submit-action-form.md)
* [アダプティブフォームを作成するかAEM Sitesページに追加する](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [アダプティブフォームをAEM Sitesページに埋め込む](/help/forms/embed-adaptive-form-aem-sites.md)
* [アダプティブフォームのテーマを作成、使用、カスタマイズする](/help/forms/using-themes-in-core-components.md)







