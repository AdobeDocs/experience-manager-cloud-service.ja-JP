---
title: ページの作成
description: サイトコンソールを使用して、Web サイト用の新しいページを作成する方法を説明します。
source-git-commit: 0ba8faaa14d09d09fce5846bfff77287bfbd94c7
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 40%

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

1. ウィザードの最初の段階で、次のいずれかを実行できます。

   * 新しいページの作成に使用するテンプレートを選択し、「 」を選択します。 **次へ** をクリックして続行します。

   * 「**キャンセル**」を使用してプロセスを中止します。

   ![新しいページのテンプレートの選択](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. ウィザードの最後の段階で、次のいずれかを実行できます。

   * 3 つのタブを使用して、新しいページに割り当てる[ページプロパティ](/help/sites-cloud/authoring/sites-console/page-properties.md)を入力し、「**作成**」を選択してページを実際に作成します。

   * 「**戻る**」を使用してテンプレートの選択に戻ります。

   主なフィールドは次のとおりです。

   * **タイトル**：

      * ユーザーに表示される、必須のフィールドです。

   * **名前**：

      * これは URI の生成に使用されます。指定しない場合、名前はタイトルから派生します。
      * ページを作成するときにページの&#x200B;**名前**&#x200B;を指定すると、AEM では AEM と JCR によって課された[規則に基づいてページ名が検証](/help/implementing/developing/introduction/naming-conventions.md)されます。
      * 「**名前**」フィールドに&#x200B;**無効な文字は指定できません**。AEMで無効な文字が検出されると、フィールドがハイライト表示され、削除または置換が必要な文字を示す説明メッセージが表示されます。

   >[!TIP]
   >
   > [ページ命名規則](#page-naming-conventions)を参照してください。

   ページの作成に必要となる最小限の情報は、「**タイトル**」です。

   ![ページタイトルの指定](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. タップまたはクリック **作成** をクリックしてプロセスを完了し、新しいページを作成します。 確認ダイアログで、 **開く** ページを直ちに開くか、コンソールに戻ります (**完了**) をクリックします。 1 つを選択して、ページ作成プロセスを終了します。

   ![ページ作成の成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * 次を選択した場合： **開く**、 **Sites** コンソールは、次のいずれかの方法で、新しいページのテンプレートに基づく適切なエディターを開きます。
      * [ページエディター](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/authoring.md)

コンソールに戻ると、新しいページが表示されます。

![作成された新しいページ](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>同じ場所に既に存在する名前でページを作成した場合、AEMは、数字を付加して指定された名前のバリエーションを持つページを作成します。 例えば、 `beach` が既に存在する場合、新しいページは `beach1`.

>[!CAUTION]
>
>ページを作成した後は、以下の手順を実行しない限り、テンプレートを変更できません。 [新しいテンプレートでのローンチの作成](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)を呼び出すと、既存のコンテンツはすべて失われます。
