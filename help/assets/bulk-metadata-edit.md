---
title: アセットビューでの一括メタデータ編集
description: Assets ビューで同時に使用できる複数アセットの事前定義済みの標準メタデータフィールドセットを更新する方法を説明します。
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# アセットビューでの一括メタデータ編集{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

Assets ビュー内の **メタデータ一括編集** 機能を使用すると、複数のアセットファイルに対して、事前に定義された一連の標準メタデータフィールドを同時に編集できます。 複数のアセットを選択し、各アセットの標準メタデータを個別に更新するのではなく、事前定義済みの標準メタデータのセットを一度に一括更新します。 この機能により、大規模なアセットのセット全体で標準メタデータプロパティの効率、一貫性および精度が向上し、アセットの検索性と編成性が向上します。

## アセットメタデータの一括編集 {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

複数のアセットのメタデータを一度に一括編集するには、次の手順を実行します。

1. Assets ビューで、**Assets** をクリックします。
1. 特定のアセットを参照するか、検索バーのキーワードを使用して検索します。
1. アセットを選択し、上部のメニューから **一括メタデータ編集** をクリックします。
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. メタデータを編集ページで、**プロパティ** パネルの次のフィールドを編集します。
   * **ステータス：** 選択したアセットのステータスを選択します。
   * **有効期限：** アセットが有効でなくなる日付または必要でなくなる日付を設定します。
   * **作成者：** 作成者の名前を指定します。
   * **キーワード：** アセットに関する高レベルの情報を提供する特定の用語やテキスト文字列を追加して、アセットの検出性を高めます。 キーワードを追加し、Enter キーまたはリターンキーを押して、リストに別のキーワードを追加します。
   * **タグ：** ![ タグアイコン ](/help/assets/assets/tags-icon.svg) をクリックして、使用可能なオプションからタグを選択します。 タグは、アセットに関するより具体的な情報を提供し、その検出性を向上させます。 選択したアセットに既に適用されているタグが、**プロパティ** パネルに表示されます。 関連するタグが見つからない場合は、作成し、選択したアセットに割り当てます。 アセットへのタグの作成と割り当てについて詳しくは、[Assets ビューでのタグの管理 ](/help/assets/tagging-management-assets-view.md) を参照してください。
   * 「**保存**」をクリックして、選択したアセットに上記のメタデータの更新を適用します。 保存すると、キーワードとタグが付加され、ステータス、有効期限、作成者の更新された詳細が既存の詳細より優先されます。
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >一度に 100 個のアセットのメタデータを編集できます。

アセットに適用されたメタデータのアップデートを確認するには、アセットの詳細ページに移動し（アセットを選択して **詳細**）をクリックし、「![](/help/assets/assets/info-icon-solid-black.svg)」をクリックして **情報** パネルでアセットのメタデータを表示します。

>[!NOTE]
>
>**ステータス**、**有効期限**、**オーサー**、**キーワード** および **タグ** は、フォルダー固有のメタデータにかかわらず、一括メタデータ編集で使用できる標準メタデータプロパティです。 これらのメタデータプロパティは、アセットのフォルダーに適用されるメタデータフォームに含まれる場合にのみ、アセットの詳細ページに表示されます。 アセットの詳細ページにこれらの標準メタデータプロパティが見つからない場合は、アセットフォルダーのメタデータフォームを編集してそれらを含めます。 メタデータフォームを作成または編集してフォルダーに適用する方法については、[Assets ビューのメタデータ ](/help/assets/metadata-assets-view.md) を参照してください。
