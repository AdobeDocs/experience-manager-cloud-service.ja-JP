---
title: アダプティブフォームの送信アクションの設定方法
description: アダプティブフォームには、複数の送信アクションが用意されています。送信アクションは、送信後のアダプティブフォームの処理方法を定義します。ビルトインの送信アクションを使用するか、独自のアクションを作成できます。
keywords: アダプティブフォームの送信アクションの選択方法, アダプティブフォームの SharePoint リストへの接続方法, アダプティブフォームの SharePoint ドキュメントライブラリへの接続方法, アダプティブフォームのフォームデータモデル（FDM）への接続方法
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 3f8950c3-9022-4e9f-b3ed-723245201e45
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 66%

---

# Edge Delivery Services Formsの送信アクション

| バージョン | 記事リンク |
|---------|-----------------------------|
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=ja) |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（コアコンポーネント） | [ここをクリックしてください](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service（Edge Delivery Services） | この記事 |

送信アクションは、データの保存、ワークフローのトリガー、サードパーティシステムとの統合など、ユーザーがフォームを送信したときの動作を定義します。 設定できる送信アクションの種類は、Edge Delivery Services Formsの作成に使用したオーサリング方法によって異なります。

Edge Delivery Services Formsは、[&#x200B; ユニバーサルエディター &#x200B;](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) または [&#x200B; ドキュメントベースのForms](/help/edge/docs/forms/overview.md) オーサリングを使用して作成し、それに応じて、異なる送信アクションを持つフォームを設定できます。

## ユニバーサルエディターで作成されたフォームの送信アクション

[ユニバーサルエディターで作成されたアダプティブフォーム](/help/edge/docs/forms/universal-editor/create-forms.md)では、次の送信アクションがサポートされています。

* [メールを送信](/help/forms/configure-submit-action-send-email.md)
* [Power Automate フローを起動](/help/forms/forms-microsoft-power-automate-integration.md)
* [SharePoint に送信](/help/forms/configure-submit-action-sharepoint.md)
* [Workfront Fusion を起動](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [フォームデータモデル（FDM）を使用して送信](/help/forms/integrate-adaptive-form-with-fdm.md)
* [Azure Blob Storage に送信](/help/forms/configure-submit-action-azure-blob-storage.md)
* [REST エンドポイントに送信](/help/forms/configure-submit-action-restpoint.md)
* [OneDrive に送信](/help/forms/configure-submit-action-onedrive.md)
* [AEM ワークフローを起動](/help/forms/configure-submit-action-workflow.md)
* [Marketo Engage に送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Adobe Experience Platform（AEP）に送信](/help/forms/aem-forms-aep-connector.md)
* [スプレッドシートに送信](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

**フォームプロパティを編集**&#x200B;拡張機能の「**送信**」タブを使用して、ユニバーサルエディターで作成されたフォームの送信アクションを設定できます。

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Manager で&#x200B;**フォームプロパティを編集**&#x200B;拡張機能を有効にします。
> * ユニバーサルエディターで拡張機能を有効または無効にする方法については、[Extension Manager 機能のハイライト](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)の記事を参照してください。

## ドキュメントベースのFormsの送信アクション

ドキュメントベースのFormsでは、スプレッドシートへの送信のみをサポートしています。 送信されたデータを受け取るスプレッドシートの設定方法については、[&#x200B; データの受け入れを開始するためのGoogle シートまたはMicrosoft Excel ファイルの設定 &#x200B;](/help/edge/docs/forms/submit-forms.md) 記事の手順を参照してください。

## 関連トピック {#see-also}

{{af-submit-action}}
