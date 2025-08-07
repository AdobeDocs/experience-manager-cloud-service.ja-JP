---
title: アダプティブフォームの送信アクションの設定方法
description: アダプティブフォームには、複数の送信アクションが用意されています。送信アクションは、送信後のアダプティブフォームの処理方法を定義します。ビルトインの送信アクションを使用するか、独自のアクションを作成できます。
keywords: アダプティブフォームの送信アクションを選択する方法、アダプティブフォームを sharepoint リストに接続する方法、アダプティブフォームを sharepoint ドキュメントライブラリに接続する方法、アダプティブフォームをフォームデータモデル（FDM）に接続する方法
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: d221959bbf19a874ec65eb414c4c49811df291ca
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 50%

---

# アダプティブフォーム送信アクション

| バージョン | 記事リンク |
|---------|-----------------------------|
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=ja) |
| AEM as a Cloud Service（基盤コンポーネント） | [ここをクリックしてください](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service（コアコンポーネント） | [ここをクリックしてください](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service（Edge Delivery Services） | この記事 |

## 概要

フォーム送信は、ユーザージャーニーでの重要な最終ステップです。ここで収集されたデータが処理され、アクションが実行されます。このドキュメントでは、ユニバーサルエディターでのアダプティブフォームの送信アクションの設定と管理に関する包括的なガイドを提供します。

### 学習内容

このドキュメントの終わりまでに、次の方法を理解できます。

- フォームに対して様々なタイプの送信アクションを設定
- 外部システムとの統合のために REST エンドポイント送信を設定
- フォームへの応答に対するメール送信を設定
- 特定のビジネスニーズに合わせてカスタム送信アクションを実装
- 送信時のフォーム検証とエラーシナリオを処理

### ターゲットオーディエンス

このガイドは、以下の読者を対象に設計されています。

- 送信ロジックを実装する&#x200B;**フォーム開発者**
- フォームをバックエンドシステムに接続する&#x200B;**システムインテグレーター**
- フォームワークフローを定義する&#x200B;**ビジネスアナリスト**
- フォーム送信プロセスを設計する&#x200B;**テクニカルアーキテクト**

## ユニバーサルエディターで作成されたFormsの送信アクション

[ ユニバーサルエディターで作成されたアダプティブForms](/help/edge/docs/forms/universal-editor/create-forms.md) では、次の送信アクションがサポートされています。

- [メールを送信](/help/forms/configure-submit-action-send-email.md)
- [Power Automate フローを起動](/help/forms/forms-microsoft-power-automate-integration.md)
- [SharePoint に送信](/help/forms/configure-submit-action-sharepoint.md)
- [Workfront Fusion の呼び出し](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [フォームデータモデル（FDM）を使用して送信](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Azure Blob Storage への送信](/help/forms/configure-submit-action-azure-blob-storage.md)
- [REST エンドポイントへの送信](/help/forms/configure-submit-action-restpoint.md)
- [OneDrive に送信](/help/forms/configure-submit-action-onedrive.md)
- [AEM ワークフローを起動](/help/forms/configure-submit-action-workflow.md)
- [Marketo Engage に送信](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Adobe Experience Platform（AEP）への送信](/help/forms/aem-forms-aep-connector.md)
- [スプレッドシートに送信](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

ユニバーサルエディターで作成されたフォームの送信アクションは、「**フォームプロパティを編集** 拡張機能の「**送信**」タブを使用して設定できます。

**ユニバーサルエディターで作成したFormsの送信アクションを設定する方法？**
ユニバーサルエディターで作成されたフォームの送信アクションは、「**フォームプロパティを編集** 拡張機能の「**送信**」タブを使用して設定できます。

![ フォームプロパティアイコン ](/help/forms/assets/ue-form-properties-icon.png)

![ ユニバーサルエディターフォームのプロパティ ](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - ユニバーサルエディターインターフェイスに **フォームプロパティを編集** アイコンが表示されない場合は、Extension Managerで **フォームプロパティを編集** 拡張機能を有効にします。
> - ユニバーサルエディターで拡張機能を有効または無効にする方法については [&#128279;](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)Extension Manager機能のハイライト &rbrace; の記事を参照してください。



