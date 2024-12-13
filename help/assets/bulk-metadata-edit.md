---
title: Assets ビューでのメタデータの一括編集
description: Assets ビューで使用可能な複数のアセットのメタデータを同時に編集する方法を説明します。
source-git-commit: 5778d0dac141174c1b950625057f920af0301a8b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Assets ビューでのメタデータの一括編集{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

Assets ビュー UI 内の **一括メタデータ編集** を使用すると、複数のアセットファイルのメタデータを同時に変更できます。 各アセットのメタデータを個別に編集する代わりに、一度に大きなアセットグループに変更を適用することができます。 この機能により、大規模なアセットのセット全体でメタデータプロパティの効率、一貫性および精度が向上し、アセットの検索性と編成が向上します。

## アセットメタデータの一括編集 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

複数のアセットのメタデータを一度に一括編集するには、次の手順を実行します。

1. Assets ビューで、**Assets** をクリックします。
1. アセットを参照するか、検索バーに関連するキーワードを入力して特定のアセットを検索します。
1. 複数のアセットを選択し、上部のメニューから **一括メタデータ編集** をクリックします。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit.png)
1. メタデータを編集ページで、**プロパティ** パネルの次のフィールドを編集します。
   * **ステータス：** 選択したアセットの使いやすさを定義するためのステータスを選択します。
   * **有効期限：** アセットが有効でなくなる日付または必要でなくなる日付を設定します。
   * **作成者：** 作成者の名前を指定します。
   * **キーワード：** アセットに関する高レベルの情報を提供する用語やテキスト文字列を追加して、検索性を高めます。 キーワードを追加し、Enter キーまたはリターンキーを押して、リストに別のキーワードを追加します。
     <!-- * **Tags:** Click ![tags icon](/help/assets/assets/tags-icon.svg) to select tags from the available options. Tags provide more specific information about the assets and enhances their discoverability. Tags already applied to the selected assets are only displayed in the **Properties** panel. If you cannot find the relevant tags, create the tags and assign them to the selected assets. See [Manage tags in Assets view](/help/assets/tagging-management-assets-view.md) for details.-->
   * 「**保存**」をクリックしてキーワードを追加し、ステータス、有効期限、作成者の既存の詳細を上書きで <!-- Tags while--> ます。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties1.png)

     >[!NOTE]
     >
     >一度に 100 個のアセットのメタデータを編集できます。

アセットに適用されたメタデータの変更を確認するには、アセットの詳細ページに移動し（アセットを選択して **詳細**）、「![](/help/assets/assets/info-icon-solid-black.svg)」をクリックして、**情報** パネルでアセットのメタデータを表示します。

>[!NOTE]
>
>ステータス、有効期限、オーサーおよびキーワードの <!-- and Tags--> は、フォルダー固有のメタデータに関係なく、一括メタデータ編集に使用できる標準のメタデータプロパティです。 これらのメタデータプロパティは、アセットのフォルダーに適用されるメタデータフォームに含まれる場合にのみ、アセットの詳細ページに表示されます。  アセットの詳細ページにこれらのメタデータプロパティが表示されない場合は、アセットフォルダーのメタデータフォームを編集してそれらを含めます。 メタデータフォームを作成または編集してフォルダーに適用する方法については、[Assets ビューのメタデータ ](/help/assets/metadata-assets-view.md) を参照してください。


