---
title: アセット関係
description: 一部の共通属性を共有するデジタルアセットを関連付ける方法について説明します。また、アセット関係を使用して、デジタルアセット間にソースから派生した関係を作成します。
role: User
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 77dab2731f8d442bf999bf1614ef060944794574
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 59%

---

# アセット関係 {#related-assets}

[!DNL Adobe Experience Manager Assets] では、関連するアセット機能を使用して、組織のニーズに基づいて手動でアセットを関連付けることができます。例えば、ライセンスファイルを、類似するトピックのアセットや画像／ビデオに関連付けることができます。特定の共通属性を共有するアセットを関連付けることができます。また、この機能を使用して、アセット間にソースと派生の関係を作成することもできます。例えば、INDD ファイルから生成された PDF ファイルがある場合、その PDF ファイルをそのソース INDD ファイルに関連付けることができます。

この機能を使用すると、ベンダーや代理店と低解像度の PDF ファイルや JPG ファイルを共有し、高解像度の INDD ファイルは必要な場合のみ利用できるように柔軟に指定できます。

>[!NOTE]
>
>アセットに対する編集権限を持つユーザーのみが、アセットの関連付けと関連付け解除を行うことができます。

## アセットを関連付ける手順 {#steps-to-relate-assets}

1. [!DNL Experience Manager] のインターフェイスから、関連付けるアセットの **[!UICONTROL プロパティ]**&#x200B;ページを開きます。

   ![アセットのプロパティページを開きアセットを関連付ける](assets/asset-properties-relate-assets.png)

1. 選択したアセットに別のアセットを関連付けるには、「**[!UICONTROL アセットの関係]**![ アセットの関連付け ](assets/do-not-localize/link-relate.png) をクリックします。
1. 次のいずれかの操作を行います。

   * アセットのソースファイルを関連付けるには、リストから「**[!UICONTROL Sourceを追加]**」を選択します。 ソースとして関連付けることができるアセットは 1 つだけです。
   * 派生ファイルを関連付けるには、リストから「**[!UICONTROL 派生を追加]**」を選択します。 このカテゴリには複数のアセットを関連付けることができます。
   * アセット間に双方向関係を作成するには、リストから **[!UICONTROL その他を追加]** を選択します。 このカテゴリには複数のアセットを関連付けることができます。

1. **[!UICONTROL Assetsを選択]** 画面で、関連付けるアセットの場所に移動し、アセットを選択します。 Shift キーを押しながらクリックすることで、1 つのアセットを一度に選択することも、複数のアセットを選択することもできます。この場合、[Assets ビューでサポートされているファイル形式 ](/help/assets/supported-file-formats-assets-view.md) を使用できます。

   ![ 関連アセットを追加 ](assets/add-related-asset.png)

1. **[!UICONTROL 選択]** をクリックします。 手順 3 で選択した関係に応じて、関連アセットが「**[!UICONTROL アセット関係]**」セクションの適切なカテゴリの下に表示されます。 例えば、関連付けたアセットが現在のアセットのソースファイルの場合は、「**[!UICONTROL ソース]**」の下に表示されます。

   ![Assets関係の例 ](assets/asset-relations-example.png)

1. 各セクションのすべての関連アセットで使用できる **[!UICONTROL 関連付けを解除]**![ アセットの関連付けを解除 ](assets/do-not-localize/link-unrelate-icon.png)、（[!UICONTROL Source]、[!UICONTROL &#x200B; 派生 &#x200B;]、（その他 ）  をクリックして、アセットの関連付けを解除します。

## 関連アセットの翻訳 {#translating-related-assets}

関連アセット機能を使用してアセット間でソースと派生の関係を作成すると、翻訳ワークフローにも役立ちます。派生アセットで翻訳ワークフローを実行すると、[!DNL Experience Manager Assets] はソースファイルが参照するすべてのアセットを自動的に取得し、翻訳用に組み込みます。これにより、ソースアセットが参照するアセットが、ソースおよび派生アセットと共に翻訳されます。ソースファイルが別のアセットに関連付けられている場合、[!DNL Experience Manager Assets] は参照されているアセットを取得し、翻訳用に組み込みます。

[AEMのアセットの翻訳 ](/help/assets/translate-assets.md) を参照してください。

## 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [アセットのバージョンを表示](/help/assets/manage-organize-assets-view.md#view-versions)
>* [AEMでのアセットの翻訳 ](/help/assets/translate-assets.md)
>* [Assets ビューでサポートされるファイル形式 ](/help/assets/supported-file-formats-assets-view.md)。
