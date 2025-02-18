---
title: ページの作成
description: Sites コンソールを使用して web サイトの新しいページを作成する方法について説明します。
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '477'
ht-degree: 100%

---


# ページの作成 {#creating-pages}

**Sites** コンソールを使用して web サイトの新しいページを作成する方法について説明します。

>[!TIP]
>
>新しいページの作成を開始する前に、[AEM でページを整理する方法](/help/sites-cloud/authoring/sites-console/organizing-pages.md)について理解を深めます。

## アクセス権 {#access-privileges}

ページを作成するには、アカウントに適切なアクセス権と権限が必要です。

問題が発生した場合は、システム管理者にお問い合わせください。

## 新しいページの作成 {#creating-a-new-page}

すべてのページが事前に作成されていない限り、コンテンツの作成を開始するには、まずページを作成する必要があります。

1. [**Sites** コンソール](/help/sites-cloud/authoring/sites-console/introduction.md)を開きます。
1. 新しいページを作成する場所に移動します。
1. ツールバーの「**作成**」を使用してドロップダウンセレクターを開き、リストから「**ページ**」を選択します。

   ![ページの作成](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. ウィザードの最初のステージで、次のいずれかを実行できます。

   * 新しいページの作成に使用するテンプレートを選択し、「**次へ**」を選択して続行するか、「**キャンセル**」を選択してプロセスを中止します。
   * テンプレートは、[ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)と[ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/templates.md)の両方でサポートされています。

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

1. 「**作成**」をタップまたはクリックしてプロセスを完了し、新しいページを作成します。ページをすぐに「**開く**」かコンソールに戻る（「**完了**」する）かを確認するダイアログが表示されます。1 つを選択して、ページ作成プロセスを終了します。

   ![ページ作成の成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * 「**開く**」を選択すると、**Sites** コンソールは、新しいページのテンプレートに基づいて、次のいずれかの適切なエディターを開きます。
      * [ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)

コンソールに戻ると、新しいページが表示されます。

![作成された新しいページ](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>同じ場所に既に存在する名前を使用してページを作成する場合、AEM では、番号を付加して、指定された名前のバリエーションを使用してページを作成します。例えば、`beach` が既に存在する場合、新しいページは `beach1` になります。

>[!CAUTION]
>
>ページを作成したら、そのテンプレートは変更できません。ただし、[新しいテンプレートでローンチを作成](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)する場合を除きます。その場合、既存のコンテンツはすべて失われます。
