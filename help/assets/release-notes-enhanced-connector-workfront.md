---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のリリースノート'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f49ac67b7a90d638e266b9f7f5bf5ac9d7f78e3a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 52%

---

# [!DNL Workfront for Experience Manager enhanced connector] のリリースノート {#release-notes-enhanced-connector-workfront}

以下の節では、[!DNL Workfront for Experience Manager enhanced connector] の一般リリースノートの概要を説明します。

## リリース日 {#release-date}

の最新バージョン 1.9.2 のリリース日 [!DNL Workfront for Experience Manager enhanced connector] は 2022 年 8 月 3 日です。

## リリースのハイライト {#release-highlights}

の最新バージョン [!DNL Workfront for Experience Manager enhanced connector] には、次の機能強化とバグ修正が含まれています。

* この **[!UICONTROL ドキュメントをアップロード]** ワークフローステップで、ドキュメントをWorkfrontに添付できません。

* この **[!UICONTROL ドキュメントをアップロード]** ワークフローステップで、Workfrontのタスクと問題にドキュメントを添付できません。 ワークフローステップは、ドキュメントをプロジェクトに正常に添付します。

>[!IMPORTANT]
>
>Adobeが推奨する [最新バージョン 1.9.2 にアップグレード](../assets/update-workfront-enhanced-connector.md) の [!DNL Workfront for Experience Manager enhanced connector].

## 既知の問題 {#known-issues}

* AEM 6.4 でプロジェクトにリンクしたフォルダーを設定する際に、Experience Manager は「**[!UICONTROL sub-folders]**」フィールドと「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値を保存しません。設定を保存すると、「**[!UICONTROL sub-folders]**」フィールドの値が **[!UICONTROL undefined]** に、「**[!UICONTROL Create linked folder in projects with portfolio]**」フィールドの値が **[!UICONTROL Default Portfolio]** に、それぞれ自動的に更新されます。

* 従来の Workfront エクスペリエンスを使用している場合、「**[!UICONTROL 詳細]**」ドロップダウンリストで選択できる「**[!UICONTROL 送信先]**」オプションでは、Experience Manager 内のターゲット宛先を選択できません。「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストを使用する場合、「**[!UICONTROL 送信先]**」オプションは正常に機能します。新しい Workfront エクスペリエンスの「**[!UICONTROL 詳細]**」ドロップダウンリストと「**[!UICONTROL ドキュメントアクション]**」ドロップダウンリストでは、「**[!UICONTROL 送信先]**」オプションは正常に機能します。

## 以前のリリース {#previous-releases}

### 2022 年 7 月リリース {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] バージョン 1.9.1 には、次の更新が含まれています。

* Adobe IMSに移行されたインスタンスにWorkfront API キーを使用した、Experience ManagerとWorkfrontアプリケーション間の認証のサポートを追加しました。

* 外部のファイルまたはフォルダーをリンクすると、Workfrontアプリケーションに `SERVER_ERROR` エラーメッセージ。 エラーメッセージは、API キーの不一致が原因で未認証の例外を示しています。

* アセットに対してタスクを作成ワークフローを実行すると、ログメッセージに Null Pointer 例外が表示されます。

* 次を有効にした場合、 `Replace Spaces with DASH` 「Experience Managerの詳細設定」の「設定」オプションを使用すると、Workfrontでフォルダーが重複して作成されます。

### 2022 年 6 月リリース {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* リンクされたフォルダーを使用してアップロードする場合、または `Send To` WorkfrontでアセットをExperience Manageras a Cloud Serviceにアップロードするために使用できるアクション。アセットが破損し、Adobe Photoshopで開くことができない。

### 2022 年 3 月リリース {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* プロジェクトにリンクしているフォルダー設定が複数ある場合でも、Adobe Workfront と AEM Assets as a Cloud Service の間でリンクされたフォルダーを作成できるようになりました。

* イベント購読のページネーションがサポートされるようになりました。

* AEM 6.4.x がサポートされるようになりました。

* プロキシ環境がサポートされるようになりました。

* パートナーやお客様のご意見に基づいて、いくつかのバグを修正しました。

>[!MORELIKETHIS]
>
>* [ [!DNL Workfront for Experience Manager enhanced connector]  と Experience Manager 6.5 の統合](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=ja)
>* [ [!DNL Workfront for Experience Manager enhanced connector]  と Experience Manager 6.4 の統合](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=ja)

