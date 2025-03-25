---
title: セレクターを操作する
description: Dynamic Media でインタラクティブ画像、インタラクティブビデオ、カルーセルバナーのアセットを選択する方法について説明します。
contentOwner: Rick Brough
feature: Selectors,Interactive Images,Interactive Videos,Carousel Banners
role: User
exl-id: a6f366ab-41b8-4909-b815-e6c4b938bf77
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 100%

---

# Dynamic Media でセレクターを操作する {#working-with-selectors}

インタラクティブ画像、インタラクティブビデオ、カルーセルバナーを操作するときは、アセットを選択し、ホットスポットや画像マップのリンク先となるサイトや商品を選択します。画像セット、スピンセット、マルチメディアセットを操作するときは、アセットセレクターでアセットも選択します。

ここでは、商品、サイト、アセットのセレクターの使用方法について説明し、セレクターでの参照、フィルター処理、ソートの機能についても説明します。

セレクターを使用するのは、カルーセルセットを作成し、ホットスポットと画像マップを追加し、インタラクティブビデオとインタラクティブ画像を作成するときです。

例えば、このカルーセルバナーでは、ホットスポットまたは画像マップをクイックビューページにリンクする場合に、製品セレクターを使用します。ホットスポットまたは画像マップをハイパーリンクにリンクする場合は、サイトセレクターを使用します。スライドを作成する際には、アセットセレクターを使用します。

![chlimage_1-520](assets/chlimage_1-520.png)

ホットスポットまたは画像マップのリンク先を（手動で入力せずに）選択するときに、セレクターを使用します。サイトセレクターを使用できるのは [!DNL Adobe Experience Manager Sites] の顧客のみです。商品セレクターには [!DNL Experience Manager Commerce] も必要です。

## Dynamic Media で商品を選択する {#selecting-products}

商品セレクターを使用して商品を選択するのは、ホットスポットまたは画像マップで商品カタログの特定の商品のクイックビューを提供しようとするときです。

1. カルーセルセット、インタラクティブ画像、インタラクティブビデオのいずれかに移動し、「**[!UICONTROL アクション]**」タブ（ホットスポットまたは画像マップを定義した場合のみ使用可能）を選択します。

   製品セレクターは、「**[!UICONTROL アクションタイプ]**」領域にあります。

   ![chlimage_1-521](assets/chlimage_1-521.png)

1. **[!UICONTROL 商品セレクター]**&#x200B;アイコン（虫眼鏡）を選択し、カタログで商品に移動します。

   ![chlimage_1-522](assets/chlimage_1-522.png)

   「**[!UICONTROL フィルター]**」をタップして、キーワードを入力したりタグを選択したりすると、キーワードまたはタグでフィルター処理することもできます。

   ![chlimage_1-523](assets/chlimage_1-523.png)

   「**[!UICONTROL 参照]**」をタップして別のフォルダーに移動することで、[!DNL Experience Manager] が商品データを参照する場所を変更できます。

   ![chlimage_1-524](assets/chlimage_1-524.png)

   「**[!UICONTROL ソート順]**」を選択して、[!DNL Experience Manager] で新しい順に表示するか古い順に表示するかを変更します。

   ![chlimage_1-525](assets/chlimage_1-525.png)

   「**[!UICONTROL 表示形式]**」を選択して、商品の表示形式（**[!UICONTROL リスト表示]**&#x200B;または&#x200B;**[!UICONTROL カード表示]**）を変更します。

   ![chlimage_1-526](assets/chlimage_1-526.png)

1. 商品が選択されると、商品のサムネールと名前がフィールドに設定されます。

   ![chlimage_1-527](assets/chlimage_1-527.png)

1. **[!UICONTROL プレビュー]**&#x200B;モードでは、ホットスポットか画像マップを選択して、クイックビューの表示内容を確認できます。

   ![chlimage_1-528](assets/chlimage_1-528.png)

## Dynamic Media でサイトを選択する {#selecting-sites}

サイトセレクターを使用して Web ページを選択するのは、ホットスポットまたは画像マップを、[!DNL Experience Manager] Sites で管理される Web ページにリンクしようとするときです。

1. カルーセルセット、インタラクティブ画像、インタラクティブビデオのいずれかに移動し、「**[!UICONTROL アクション]**」タブ（ホットスポットまたは画像マップを定義した場合のみ使用可能）を選択します。

   サイトセレクターは、「**[!UICONTROL アクションタイプ]**」領域にあります。

   ![chlimage_1-529](assets/chlimage_1-529.png)

1. **[!UICONTROL サイトセレクター]**&#x200B;アイコン（フォルダーと虫眼鏡）を選択し、ホットスポットまたは画像マップのリンク先となる [!DNL Experience Manager] サイト内のページに移動します。

   ![chlimage_1-530](assets/chlimage_1-530.png)

1. サイトが選択されると、そのパスがフィールドに設定されます。

   ![chlimage_1-531](assets/chlimage_1-531.png)

1. **[!UICONTROL プレビュー]**&#x200B;モードでは、ホットスポットまたは画像マップを選択すると、指定した [!DNL Experience Manager] サイトページに移動します。

## Dynamic Media でアセットを選択する {#selecting-assets}

このセレクターで、カルーセルバナー、インタラクティブビデオ、画像セット、混在メディアセット、スピンセットで使用する画像を選択します。インタラクティブビデオでは、「**[!UICONTROL コンテンツ]**」タブの「**[!UICONTROL アセットを選択]**」を選択すると、アセットセレクターを使用できます。カルーセルセットでは、スライドを作成するときにアセットセレクターを使用できます。画像セット、混在メディアセット、スピンセットでは、画像セット、混在メディアセット、スピンセットをそれぞれ作成するときに、アセットセレクターを使用できます。

詳しくは、[アセットピッカー](/help/assets/search-assets.md#asset-selector)を参照してください。

1. カルーセルセットに移動して、新しいスライドを作成します。または、インタラクティブビデオに移動して、「**[!UICONTROL コンテンツ]**」タブでアセットを選択します。あるいは、混在メディアセット、画像セット、スピンセットのいずれかを作成します。
1. **[!UICONTROL アセットセレクター]**&#x200B;アイコン（フォルダーと虫眼鏡）を選択し、アセットに移動します。

   ![chlimage_1-532](assets/chlimage_1-532.png)

   「**[!UICONTROL フィルター]**」をタップして、キーワードを入力したり条件を追加したりして、キーワードまたはタグでフィルター処理します。

   ![chlimage_1-533](assets/chlimage_1-533.png)

   [!DNL Experience Manager]「**[!UICONTROL パス]**」フィールドで別のフォルダーに移動して、 がアセットを参照する場所を変更できます。

   コレクション内のアセットのみを検索するには、「**[!UICONTROL コレクション]**」を選択します。

   ![chlimage_1-534](assets/chlimage_1-534.png)

   「**[!UICONTROL 表示形式]**」を選択して、商品の表示形式（**[!UICONTROL リスト表示]**、**[!UICONTROL 列表示]**、**[!UICONTROL カード表示]**&#x200B;のいずれか）を変更します。

   ![chlimage_1-535](assets/chlimage_1-535.png)

1. アセットを選択するには、チェックマークを選択します。アセットが表示されます。

   ![chlimage_1-536](assets/chlimage_1-536.png)
-->
