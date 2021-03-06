---
title: リリースノート（） [!DNL Workfront for Experience Manager enhanced connector]
description: リリースノート（） [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: d763bacb0844a438ebea6ef206dfa184a49993fe
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---

# リリースノート（）[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下の節では、 [!DNL Workfront for Experience Manager enhanced connector].

## リリース日 {#release-date}

の最新バージョン 1.9.1 のリリース日 [!DNL Workfront for Experience Manager enhanced connector] は 2022 年 7 月 1 日です。

## 新機能ハイライト {#release-highlights}

の最新バージョン [!DNL Workfront for Experience Manager enhanced connector] には、次の機能強化とバグ修正が含まれています。

* Adobe IMSに移行されたインスタンスにWorkfront API キーを使用した、Experience ManagerとWorkfrontアプリケーション間の認証のサポートを追加しました。

* 外部のファイルまたはフォルダーをリンクすると、Workfrontアプリケーションに `SERVER_ERROR` エラーメッセージ。 エラーメッセージは、API キーの不一致が原因で未認証の例外を示しています。

* アセットに対してタスクを作成ワークフローを実行すると、ログメッセージに Null Pointer 例外が表示されます。

* 次を有効にした場合、 `Replace Spaces with DASH` 「Experience Managerの詳細設定」の「設定」オプションを使用すると、Workfrontでフォルダーが重複して作成されます。

>[!IMPORTANT]
>
>Adobeが推奨する [最新バージョン 1.9.1 にアップグレード](../assets/update-workfront-enhanced-connector.md) の [!DNL Workfront for Experience Manager enhanced connector].

## 既知の問題 {#known-issues}

* AEM 6.4 でプロジェクトにリンクされたフォルダーを設定する際に、Experience Managerは次の値を保存しません： **[!UICONTROL サブフォルダー]** および **[!UICONTROL ポートフォリオを含むプロジェクトでリンクされたフォルダーを作成する]** フィールド。 の値 **[!UICONTROL サブフォルダー]** フィールドの更新 **[!UICONTROL 未定義]** および **[!UICONTROL ポートフォリオを含むプロジェクトでリンクされたフォルダーを作成する]** フィールドの更新 **[!UICONTROL デフォルトのPortfolio]** は、設定を保存した後に自動的に追加されます。

* 従来のWorkfrontエクスペリエンスを使用している場合、 **[!UICONTROL 送信先]** オプションは **[!UICONTROL 詳細]** ドロップダウンリストでは、「Experience Manager」内でターゲットの宛先を選択できません。 この **[!UICONTROL 送信先]** オプションは **[!UICONTROL ドキュメントアクション]** ドロップダウンリスト。 この **[!UICONTROL 送信先]** オプションは、 **[!UICONTROL 詳細]** ドロップダウンリスト **[!UICONTROL ドキュメントアクション]** 新しいWorkfrontエクスペリエンスで使用できるドロップダウンリスト。

## 以前のリリース {#previous-releases}

### 2022 年 6 月リリース {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* リンクされたフォルダーを使用してアップロードする場合、または `Send To` WorkfrontでアセットをExperience Manageras a Cloud Serviceにアップロードするために使用できるアクション。アセットが破損し、Adobe Photoshopで開くことができない。

### 2022 年 3 月リリース {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] には、次の更新が含まれています。

* 複数のプロジェクトリンクフォルダー設定がある場合でも、Adobe WorkfrontとAEM Assetsas a Cloud Serviceの間にリンクされたフォルダーを作成できるようになりました。

* イベント購読のページネーションのサポートを追加しました。

* AEM 6.4.x のサポートを追加しました。

* プロキシ環境のサポートを追加しました。

* パートナーやお客様のご意見に基づいて、いくつかのバグを修正しました。

>[!MORELIKETHIS]
>
>* [統合 [!DNL Workfront for Experience Manager enhanced connector] Experience Manager6.5 の場合](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [統合 [!DNL Workfront for Experience Manager enhanced connector] Experience Manager6.4 の場合](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

