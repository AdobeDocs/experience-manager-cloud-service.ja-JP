---
title: ' [!DNL Assets View] でのメタデータを一括編集'
description: '[DNL! Assets View] で使用できる複数のアセットの定義済み標準メタデータフィールドセットを同時に更新する方法を説明します。'
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '450'
ht-degree: 100%

---

# [!DNL Assets View] でのメタデータを一括編集{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

[!DNL Assets View] の **[!DNL Bulk Metadata Edit]** 機能を使用すると、複数のアセットファイルに対する事前定義済みの標準メタデータフィールドセットを同時に編集できます。複数のアセットを選択し、各アセットの標準メタデータを個別に更新するのではなく、事前定義済みの標準メタデータのセットを一度に一括更新します。この機能により、大規模なアセットセット全体で標準メタデータプロパティセットの効率、一貫性および精度が維持され、アセットの検索性と整理が向上します。

## アセットメタデータを一括編集 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

複数のアセットメタデータを一度に一括編集するには、次の手順を実行します。

1. **[!DNL Assets View]** に移動して「**[!UICONTROL アセット]**」をクリックします。
1. 特定のアセットを参照するか、検索バーのキーワードを使用して検索します。
1. アセットを選択し、上部のメニューから「**[!UICONTROL メタデータを一括編集]**」をクリックします。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. [!UICONTROL メタデータを編集ページ]で、**[!UICONTROL プロパティ]**&#x200B;パネルの次のフィールドを編集します。
   * **[!UICONTROL ステータス]：**&#x200B;選択したアセットのステータスを選択します。
   * **[!UICONTROL 有効期限日]：**&#x200B;アセットが有効でなくなる、または必要でなくなる日付を設定します。
   * **[!UICONTROL 作成者]：**&#x200B;作成者の名前を指定します。
   * **[!UICONTROL キーワード]：**&#x200B;アセットに関する概要情報を提供する特定の用語またはテキスト文字列を追加して、検索性を高めます。キーワードを追加し、**Enter** キーまたは **return** キーを押して、リストに別のキーワードを追加します。
   * **[!UICONTROL タグ]：**「![メタデータを一括編集](/help/assets/assets/tags-icon.svg)」をクリックして、使用可能なオプションからタグを選択します。タグによりアセットに関するより具体的な情報が得られ、検出性が向上します。選択したアセットに既に適用されているタグが、**[!UICONTROL プロパティ]**&#x200B;パネルに表示されます。関連するタグが見つからない場合は、作成し、選択したアセットに割り当てます。アセットへのタグの作成と割り当てについて詳しくは、[ [!DNL Assets view]](/help/assets/tagging-management-assets-view.md) でのタグの管理を参照してください。
   * 「**[!UICONTROL 保存]**」をクリックして、選択したアセットに上記のメタデータの更新を適用します。保存すると、**[!UICONTROL キーワード]**&#x200B;と&#x200B;**[!UICONTROL タグ]**&#x200B;が追加され、**[!UICONTROL ステータス]**、**[!UICONTROL 有効期限日]**、**[!UICONTROL 作成者]**の更新された詳細が既存の詳細を上書きします。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >一度に 100 個のアセットのメタデータを編集できます。

アセットに適用されたメタデータの更新内容を確認するには、[!DNL asset details page]（アセットを選択して&#x200B;**[!UICONTROL 詳細]**&#x200B;をクリック）に移動し、「![メタデータを一括編集](/help/assets/assets/info-icon-solid-black.svg)」をクリックして、**[!UICONTROL 情報]**&#x200B;パネルにアセットのメタデータを表示します。

>[!NOTE]
>
>**[!UICONTROL ステータス]**、**[!UICONTROL 有効期限日]**、**[!UICONTROL 作成者]**、**[!UICONTROL キーワード]**&#x200B;および&#x200B;**[!UICONTROL タグ]**&#x200B;は、フォルダー固有のメタデータにかかわらず、メタデータを一括編集で使用できる標準メタデータプロパティです。これらのメタデータプロパティは、アセットのフォルダーに適用されたメタデータフォームに含まれている場合にのみ、]アセットの詳細[!UICONTROL ページに表示されます。これらの標準メタデータプロパティが[!UICONTROL アセットの詳細ページ]で見つからない場合は、アセットフォルダーのメタデータフォームを編集してそれらを含めます。メタデータフォームを作成または編集してフォルダーに適用する方法については、[ [!DNL Assets View]](/help/assets/metadata-assets-view.md) でのメタデータを参照してください。
