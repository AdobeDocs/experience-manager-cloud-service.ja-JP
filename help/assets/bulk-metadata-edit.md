---
title: でのメタデータの一括編集  [!DNL Assets View]
description: で使用できる複数のアセットの定義済みの標準メタデータフィールドセットを更新する方法を説明します Assets View&rbrack; 同時に。
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# [!DNL Assets View] でのメタデータの一括編集{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

[!DNL Assets View] の **[!DNL Bulk Metadata Edit]** 機能を使用すると、複数のアセットファイルに対する事前定義済みの標準メタデータフィールドセットを同時に編集できます。 複数のアセットを選択し、各アセットの標準メタデータを個別に更新するのではなく、事前定義済みの標準メタデータのセットを一度に一括更新します。 この機能により、大規模なアセットセット全体で一連の標準メタデータプロパティの効率、一貫性および精度が維持され、アセットの検索性と編成が向上します。

## アセットメタデータの一括編集 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

複数のアセットのメタデータを一度に一括編集するには、次の手順を実行します。

1. **[!DNL Assets View]** に移動し、**[!UICONTROL Assets]** をクリックします。
1. 特定のアセットを参照するか、検索バーのキーワードを使用して検索します。
1. アセットを選択し、上部のメニューから **[!UICONTROL 一括メタデータ編集]** をクリックします。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. [!UICONTROL &#x200B; メタデータを編集ページ &#x200B;] で、**[!UICONTROL プロパティ]** パネルの次のフィールドを編集します。
   * **[!UICONTROL ステータス &#x200B;]:** 選択したアセットのステータスを選択します。
   * **[!UICONTROL 有効期限 &#x200B;]:** アセットが有効でなくなる、または必要でなくなる日付を設定します。
   * **[!UICONTROL 作成者 &#x200B;]:** 作成者の名前を指定します。
   * **[!UICONTROL キーワード &#x200B;]:** アセットに関する高レベルの情報を提供する特定の用語やテキスト文字列を追加して、検索性を高めます。 キーワードを追加し、**Enter** または **return** キーを押して、リストに別のキーワードを追加します。
   * **[!UICONTROL タグ &#x200B;]:** ![ 一括メタデータ編集 ](/help/assets/assets/tags-icon.svg) をクリックして、使用可能なオプションからタグを選択します。 タグは、アセットに関するより具体的な情報を提供し、その検出性を向上させます。 選択したアセットに既に適用されているタグが、**[!UICONTROL プロパティ]** パネルに表示されます。 関連するタグが見つからない場合は、作成し、選択したアセットに割り当てます。 アセットへのタグの作成と割り当てについて詳しくは、[ でのタグの管理  [!DNL Assets view]](/help/assets/tagging-management-assets-view.md) を参照してください。
   * 「**[!UICONTROL 保存]**」をクリックして、選択したアセットに上記のメタデータの更新を適用します。 保存すると、**[!UICONTROL キーワード]** と **[!UICONTROL タグ]** が追加され、**[!UICONTROL ステータス]**、**[!UICONTROL 有効期限]** と **[!UICONTROL 作成者]** の更新された詳細が既存の詳細を上書きします。

     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >一度に 100 個のアセットのメタデータを編集できます。

アセットに適用されたメタデータのアップデートを確認するには、ア [!DNL asset details page] ットに移動し（アセットを選択して **[!UICONTROL 詳細]**）をクリックし、![ 一括メタデータ編集 ](/help/assets/assets/info-icon-solid-black.svg) をクリックして、**[!UICONTROL 情報]** パネルにアセットのメタデータを表示します。

>[!NOTE]
>
>**[!UICONTROL ステータス]**、**[!UICONTROL 有効期限]**、**[!UICONTROL オーサー]**、**[!UICONTROL キーワード]** および **[!UICONTROL タグ]** は、フォルダー固有のメタデータにかかわらず、一括メタデータ編集で使用できる標準メタデータプロパティです。 これらのメタデータプロパティは、アセットのフォルダーに適用されたメタデータフォームに含まれている場合にのみ  アセットの詳細  ページに表示されます。 これらの標準メタデータプロパティが [!UICONTROL &#x200B; アセットの詳細ページ &#x200B;] で見つからない場合は、アセットフォルダーのメタデータフォームを編集してそれらを含めます。 メタデータフォームを作成または編集してフォルダーに適用する方法については、[ でのメタデータ  [!DNL Assets View]](/help/assets/metadata-assets-view.md) を参照してください。
