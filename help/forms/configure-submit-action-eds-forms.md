---
title: アダプティブフォームの送信アクションの設定方法
description: アダプティブフォームには、複数の送信アクションが用意されています。送信アクションは、送信後のアダプティブフォームの処理方法を定義します。ビルトインの送信アクションを使用するか、独自のアクションを作成できます。
keywords: アダプティブフォームの送信アクションを選択する方法、アダプティブフォームを sharepoint リストに接続する方法、アダプティブフォームを sharepoint ドキュメントライブラリに接続する方法、アダプティブフォームをフォームデータモデル（FDM）に接続する方法
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 22%

---


# Edge Delivery Services Formsの送信アクション

| バージョン | 記事リンク |
|---------|-----------------------------|
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（コアコンポーネント） | [ここをクリックしてください](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service（Edge Delivery Services） | この記事 |

送信アクションは、データの保存、ワークフローのトリガー、サードパーティシステムとの統合など、ユーザーがフォームを送信したときの動作を定義します。 設定できる送信アクションの種類は、Edge Delivery Services Formsの作成に使用したオーサリング方法によって異なります。

Edge Delivery Services Formsは、[ ユニバーサルエディター ](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) または [ ドキュメントベースのForms](/help/edge/docs/forms/overview.md) オーサリングを使用して作成し、それに応じて、異なる送信アクションを持つフォームを設定できます。

## ユニバーサルエディターで作成されたFormsの送信アクション

[ ユニバーサルエディターで作成されたアダプティブForms](/help/edge/docs/forms/universal-editor/create-forms.md) では、次の送信アクションがサポートされています。

* [メールを送信](/help/forms/configure-submit-action-send-email.md)
* [Power Automate フローを起動](/help/forms/forms-microsoft-power-automate-integration.md)
* [SharePoint に送信](/help/forms/configure-submit-action-sharepoint.md)
* [Workfront Fusion の呼び出し](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [フォームデータモデル（FDM）を使用して送信](/help/forms/using-form-data-model.md)
* [Azure Blob Storage への送信](/help/forms/configure-submit-action-azure-blob-storage.md)
* [REST エンドポイントへの送信](/help/forms/configure-submit-action-restpoint.md)
* [OneDrive に送信](/help/forms/configure-submit-action-onedrive.md)
* [AEM ワークフローを起動](/help/forms/configure-submit-action-workflow.md)
* [Marketo Engage に送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Adobe Experience Platform（AEP）への送信](/help/forms/aem-forms-aep-connector.md)
* [スプレッドシートに送信](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

ユニバーサルエディターで作成されたフォームの送信アクションは、「**フォームプロパティを編集** 拡張機能の「**送信**」タブを使用して設定できます。

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
> * ユニバーサルエディターで拡張機能を有効または無効にする方法については [](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト } の記事を参照してください。

## ドキュメントベースのFormsの送信アクション

ドキュメントベースのFormsでは、スプレッドシートへの送信のみをサポートしています。 送信されたデータを受け取るスプレッドシートの設定方法については、[ データの受け入れを開始するためのGoogle シートまたはMicrosoft Excel ファイルの設定 ](/help/edge/docs/forms/submit-forms.md) 記事の手順を参照してください。

## 関連トピック {#see-also}

{{af-submit-action}}

