---
title: アセットの関連付け
description: 一部の共通属性を共有するデジタルアセットを関連付ける方法について説明します。また、アセットの関連付けを使用して、デジタルアセット間にソースから派生した関係を作成します。
role: User
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
exl-id: 89149283-bbf2-40d3-9a4c-5b27ff5f944e
source-git-commit: 41ac6c5c18d1acb094f1107bd4a477df058ea55a
workflow-type: ht
source-wordcount: '532'
ht-degree: 100%

---

# アセットの関連付け {#related-assets}

[!DNL Adobe Experience Manager Assets] では、関連するアセット機能を使用して、組織のニーズに基づいて手動でアセットを関連付けることができます。例えば、ライセンスファイルを、類似するトピックのアセットや画像／ビデオに関連付けることができます。特定の共通属性を共有するアセットを関連付けることができます。また、この機能を使用して、アセット間にソースと派生の関係を作成することもできます。例えば、INDD ファイルから生成された PDF ファイルがある場合、その PDF ファイルをそのソース INDD ファイルに関連付けることができます。

この機能を使用すると、ベンダーや代理店と低解像度の PDF ファイルや JPG ファイルを共有し、高解像度の INDD ファイルは必要な場合のみ利用できるように柔軟に指定できます。

>[!NOTE]
>
>アセットに対する編集権限を持つユーザーのみが、アセットの関連付けと関連付け解除を行うことができます。

## アセットを関連付ける手順 {#steps-to-relate-assets}

1. [!DNL Experience Manager] のインターフェイスから、関連付けるアセットの **[!UICONTROL プロパティ]**&#x200B;ページを開きます。

   ![アセットのプロパティページを開きアセットを関連付ける](assets/asset-properties-relate-assets.png)

1. 選択したアセットに別のアセットを関連付けるには、「**[!UICONTROL アセットの関連付け]**」![アセットの関連付け](assets/do-not-localize/link-relate.png)アイコンをクリックします。
1. 次のいずれかの操作を行います。

   * アセットのソースファイルを関連付けるには、リストから「**[!UICONTROL ソースを追加]**」を選択します。ソースとして関連付けることができるアセットは 1 つだけです。
   * 派生ファイルを関連付けるには、リストから「**[!UICONTROL 派生を追加]**」を選択します。このカテゴリには複数のアセットを関連付けることができます。
   * アセット間に双方向の関係を作成するには、リストから「**[!UICONTROL その他を追加]**」を選択します。このカテゴリには複数のアセットを関連付けることができます。

1. **[!UICONTROL アセットを選択]**&#x200B;画面から、関連付けを行うアセットの場所に移動して、選択します。アセットを 1 つずつ選択することもできますが、Shift キーを押しながらクリックして複数のアセットを選択することもできます。この場合、[アセットビューでサポートされているファイル形式](/help/assets/supported-file-formats-assets-view.md)を使用できます。

   ![関連アセットを追加](assets/add-related-asset.png)

1. 「**[!UICONTROL 選択]**」をクリックします。手順 3 で選択した関係に応じて、関連付けられたアセットが「**[!UICONTROL アセットの関連付け]**」セクションの適切なカテゴリに表示されます。例えば、関連付けたアセットが現在のアセットのソースファイルの場合は、「**[!UICONTROL ソース]**」の下に表示されます。

   ![アセットの関連付けの例](assets/asset-relations-example.png)

1. 各セクション（[!UICONTROL ソース]、[!UICONTROL 派生]、[!UICONTROL その他]）で関連付けられているすべてのアセットで使用できる「**[!UICONTROL 関連付けを解除]**」![アセットの関連付けを解除](assets/do-not-localize/link-unrelate-icon.png)をクリックすると、アセットの関連付けを解除できます。

## 関連アセットの翻訳 {#translating-related-assets}

関連アセット機能を使用してアセット間でソースと派生の関係を作成すると、翻訳ワークフローにも役立ちます。派生アセットで翻訳ワークフローを実行すると、[!DNL Experience Manager Assets] はソースファイルが参照するすべてのアセットを自動的に取得し、翻訳用に組み込みます。これにより、ソースアセットが参照するアセットが、ソースおよび派生アセットと共に翻訳されます。ソースファイルが別のアセットに関連付けられている場合、[!DNL Experience Manager Assets] は参照されているアセットを取得し、翻訳用に組み込みます。

[AEM でのアセットの翻訳](/help/assets/translate-assets.md)を参照してください。

## 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる

>[!MORELIKETHIS]
>
>* [アセットのバージョンを表示](/help/assets/manage-organize-assets-view.md#view-versions)
>* [AEM でのアセットの翻訳](/help/assets/translate-assets.md)
>* [アセットビューでサポートされているファイル形式](/help/assets/supported-file-formats-assets-view.md)。
