---
title: 送信レビュー担当者とフォームの関連付け
seo-title: Associating submission reviewers with a form
description: ' [!DNL AEM Forms] のフォームへ送信レビュー担当者を関連付ける方法を説明します。関連付けられたレビュー担当者は、送信されたフォームをフォームポータル経由でレビューします。'
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 100%

---


# 送信レビュー担当者とフォームの関連付け {#associating-submission-reviewers-with-a-form}

フォーム作成時に、フォームポータル経由で送信されたフォームのレビューおよびフィードバックを行うユーザーを指定できます。組織はフィードバックを収集し、送信済みフォームに対して再作業を行うことができます。

[!DNL AEM Forms] では、レビュー担当者グループをフォームに関連付けることができます。フォームのレビューグループに追加されたユーザーは、フォームの送信を確認し、フィードバックを提供します。

フォームに割り当てられたレビュー担当者グループは指定されたフォームのみをレビューできます。

## 前提条件 {#prerequisite}

### メタデータスキーマエディターを使用してアダプティブフォームの送信レビュー担当者グループのプロパティを有効化 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

レビュー担当者グループをフォームに関連付けるには、アダプティブフォームのメタデータスキーマを編集します。デフォルトでは、送信されたフォームにレビュー担当者グループを追加できません。

メタデータスキーマを編集するには、以下の手順に従います。

1. オーサーモードで、Experience Manager の **ツール**／**アセット**／**メタデータスキーマ** をクリックします。
1. スキーマフォームページで、「**フォーム**／**AEM で作成されたフォーム**」に移動します。

   ページの URL は以下のとおりです。

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 「**アダプティブフォーム**」を選択し、「**編集**」をクリックします。
1. 「フォームの編集」ページで、「**詳細**」をクリックします。
1. 「詳細」タブで、ビルドフォームで使用可能な「**1 行テキスト**」コンポーネントをドラッグ＆ドロップします。
1. 追加されたテキストコンポーネントを選択し、その設定を確認します。

   「設定」の下の「プロパティにマップ」フィールドに `./jcr:content/metadata/form-submission-reviewer-group` と入力します。

   アダプティブフォームの詳細属性の送信レビュー担当者グループフィールドが、フィールドラベルで指定した名前で有効化されます。

## 送信レビュー担当者とフォームの関連付け {#associating-submission-reviewers-with-a-form-1}

アダプティブフォームに送信レビュー担当者を関連付けるには、レビュー担当者グループを作成し、そこにユーザーを追加します。フォームの詳細属性内のフォーム送信レビュー担当者のフィールドに、作成したレビュー担当者グループを追加します。ユーザーグループを使用することで、アダプティブフォームごとに異なる送信レビュー担当者のグループを関連付けることができます。この機能によって、権限のないユーザーによる送信レビューを避けることができます。

以下の手順を行う前に、「[必要条件](adding-reviewers-form.md#prerequisite)」を参照してください。

グループを作成し、メンバーを追加するには、**ツール**／**操作**／**セキュリティ**／**グループ**&#x200B;に移動します。詳しくは、「[ユーザー管理およびサービス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ja)」を参照してください。作成したグループが、あらかじめ用意されているユーザーグループ **forms-submission-reviewers** のメンバーとして追加されていることを確認してください。このユーザーグループは、[!DNL AEM Forms] に付属しており、ユーザーは送信レビュー担当者として追加されます。

ユーザーグループをアダプティブフォームに関連付けるには、以下の手順に従います。

1. 作成者モードで、**フォーム**／**フォームとドキュメント**&#x200B;に移動します。
1. **選択**オプションを使用してアダプティブフォームを選択し、「**プロパティを表示**」をクリックします。
1. フォームのプロパティウィンドウで「**編集**」をクリックし、「**詳細**」をクリックします。
1. 送信レビュー担当者グループのフィールドにグループを入力し、「**完了**」をクリックします。

   送信レビュー担当者グループのフィールドには、アダプティブフォームのメタデータスキーマの編集で指定した名前が表示されます。

>[!NOTE]
>
>リモートでの [!DNL AEM Forms] の導入においてユーザーとフォームの可用性を確認するには、ユーザーとフォームを複製してください。
>
>リモートで、すべてのユーザーがレビュー担当のメンバーとして複製されていることを確認してください。

