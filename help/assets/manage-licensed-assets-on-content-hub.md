---
title: コンテンツハブでのライセンス済みアセットの管理
description: アセットメタデータフォームへのライセンスフィールドの追加、アセットフォルダーへのライセンスメタデータプロパティの適用、使用するライセンスを持つアセットの承認について説明します。
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 91%

---

# コンテンツハブでのライセンス済みアセットの管理 {#manage-licensed-assets-on-content-hub}

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

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

管理者として、メタデータフォームを編集してアセットライセンスフィールドを含め、AEM オーサー環境のアセットプロパティに表示されるようにします。その後、アセットとそのライセンスを承認して、アセットのライセンスを付与し、コンテンツハブで使用できます。

次の手順を実行します。

1. メタデータフォームを編集して、ライセンスの詳細を含める新しいテキストフィールドを含めます。テキストフィールドを `dc:license` プロパティにマッピングします。メタデータフォームにフィールドを追加してプロパティを定義する方法について詳しくは、[メタデータフォームの設定](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。
   ![ZIP 抽出](/help/assets/assets/metadata-form-edit.png)
1. メタデータフォームをアセットフォルダーに適用して、手順 1 で組み込んだ設定を適用します。メタデータフォームをアセットフォルダーに割り当てる方法について詳しくは、[フォルダーへのメタデータフォームの割り当て](/help/assets/metadata-assets-view.md#metadata-forms)を参照してください。
1. [ライセンス済み PDF の承認](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. アセットを選択し、「**詳細**」をクリックしてそのプロパティを表示します。手順 1 で追加したライセンスフィールドに、手順 3 で承認済みまたは既に以前に承認済みのアセットライセンスの絶対パスを定義します。コンテンツハブの絶対パスは、`/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)` の標準パターンに従います。例：/content/dam/teamA/projects/documents/file1.pdf
   ![絶対パス](/help/assets/assets/absolute-path.png)
1. アセットを承認して、コンテンツハブで使用できるようにし、「**保存**」をクリックします。アセットの承認方法について詳しくは、[アセットステータスの設定](/help/assets/manage-organize-assets-view.md#set-asset-status)を参照してください。
