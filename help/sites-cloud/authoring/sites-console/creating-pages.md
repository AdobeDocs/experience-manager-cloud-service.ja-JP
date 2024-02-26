---
title: ページの作成
description: サイトコンソールを使用して、Web サイト用の新しいページを作成する方法を説明します。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 84%

---


# ページの作成 {#creating-pages}

を使用して Web サイトの新しいページを作成する方法を説明します。 **Sites** コンソール。

>[!TIP]
>
>新しいページの作成を開始する前に、 [AEMでのページの整理方法。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## アクセス権限 {#access-privileges}

ページを作成するための適切なアクセス権と権限がアカウントに必要です。

問題が発生した場合は、システム管理者にお問い合わせください。

## 新しいページの作成 {#creating-a-new-page}

すべてのページが事前に作成されていない限り、コンテンツの作成を開始するには、まずページを作成する必要があります。

1. 開く [の **Sites** コンソール。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 新しいページを作成する場所に移動します。
1. ツールバーの「**作成**」を使用してドロップダウンセレクターを開き、リストから「**ページ**」を選択します。

   ![ページの作成](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. ウィザードの最初のステージで、次のいずれかを実行できます。

   * 新しいページの作成に使用するテンプレートを選択し、「**次へ**」を選択して続行します。

   * 「**キャンセル**」を使用してプロセスを中止します。

   ![新しいページのテンプレートの選択](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. ウィザードの最後のステージで、次のいずれかを実行できます。

   * 3 つのタブを使用して、新しいページに割り当てる[ページプロパティ](/help/sites-cloud/authoring/sites-console/page-properties.md)を入力し、「**作成**」を選択してページを実際に作成します。

   * 「**戻る**」を使用してテンプレートの選択に戻ります。

   主なフィールドは次のとおりです。

   * **タイトル**：

      * ユーザーに表示される、必須のフィールドです。

   * **名前**：

      * これは URI の生成に使用されます。指定しない場合、名前はタイトルから派生します。
      * ページを作成するときにページの&#x200B;**名前**&#x200B;を指定すると、AEM では AEM と JCR によって課された[規則に基づいてページ名が検証](/help/implementing/developing/introduction/naming-conventions.md)されます。
      * 「**名前**」フィールドに&#x200B;**無効な文字は指定できません**。AEM で無効な文字が検出されると、そのフィールドは強調表示され、対象の文字を削除または置換する必要があることを示す説明メッセージが表示されます。

   >[!TIP]
   >
   > [ページ命名規則](#page-naming-conventions)を参照してください。

   ページの作成に必要となる最小限の情報は、「**タイトル**」です。

   ![ページタイトルの指定](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 「**作成**」を使用してプロセスを完了し、新しいページを作成します。ページをすぐに「**開く**」かコンソールに戻る（「**完了**」する）かを確認するダイアログが表示されます。

   ![ページ作成の成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >ページの作成先に同名のページが既に存在する場合は、その名前のバリエーションが数字を付加して自動的に生成されます。例えば、`beach` が既に存在する場合、新しいページは `beach1` になります。

1. コンソールに戻ると、新しいページが表示されます。

   ![作成された新しいページ](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>作成済みのページのテンプレートは変更できません。ただし、[新しいテンプレートでローンチを作成](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)する場合を除きます。ただしその場合、既存のコンテンツはすべて失われます。
