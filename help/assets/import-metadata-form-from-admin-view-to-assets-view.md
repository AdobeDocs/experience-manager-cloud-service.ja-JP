---
title: メタデータフォ  [!DNL Admin View]  ムの読み込み先  [!DNL Assets View]
description: この記事では、 [!DNL Assets View] の場所で使用可能なメタデータフォームを読み込む方法  [!DNL Admin View]  ついて説明します。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 5c279f4a02f0d981e1ab9a0f32f60f76fb1418dd
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 8%

---

# [!DNL Admin View] メタデータフォームの [!DNL Assets View] への読み込み {#import-admin-view-metadata-forms-to-assets-view}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
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

[!DNL Adobe Experience Manager Assets] では、メタデータフォームとそのフォルダーの関連付けを [!DNL Admin View] から [!DNL Assets View] に読み込むことができます。

## 開始する前に{#prerequisites-for-importing-metadata-forms-to-assets-view}

メタデータフォームとそのフォルダーの関連付けを [!DNL Admin View] から [!DNL Assets View] に読み込むための管理者権限があることを確認します。

## メタデータフォームの [!DNL Assets View] への読み込み{#import-metadata-forms-to-assets-view}

管理者は、次の手順を実行して、[!DNL Admin View] で使用可能なメタデータフォームを [!DNL Assets View] に読み込みます。

1. [!DNL Assets View] ホームページに移動し、**[!UICONTROL 設定]** の **[!UICONTROL メタデータForms]** をクリックして **[!UICONTROL メタデータForms]** ページを開き、[!DNL Assets View] で使用可能なメタデータフォームのリストを表示します。

   ![ メタデータフォームページ ](/help/assets/assets/metadata-forms-page.png)

1. 「**[!UICONTROL インポート]**」を選択すると、処理メッセージが表示されます（例：*2 つのメタデータフォームを処理中…お待ちください。*）を選択します。 処理が完了すると、**[!UICONTROL メタデータフォームの読み込み]** テーブルが表示され、[!DNL Admin View] で使用可能なメタデータフォームのリストが含まれます。 テーブルの行には、メタデータフォーム名（「**[!UICONTROL 名前]**」の下）、そのフォームに関連付けられたフォルダー（「**[!UICONTROL フォルダーの関連付け]**」の下）、フォームを読み込む前にプレビュー ![ プレビュー ](/help/assets/assets/Preview.svg) するオプションが含まれます。

   ![ メタデータFormsの読み込みページ ](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > **[!UICONTROL メタデータのインポートForms]** で、フォーム名の横にあるテーブル **[!UICONTROL 複製]** ラベルは、フォームが [!DNL Assets View] 内のフォルダーに既に適用されていることを示します。 重複したフォームを読み込むと、フォルダーに適用されている既存のフォームが上書きされます。 この上書きを回避するには、フォームを読み込む前に名前を変更します。 フォーム名をクリックして名前を変更します。

1. （[!UICONTROL &#x200B; フォルダー関連付け &#x200B;] の下にある）フォルダー名の横の ![ フォルダーを選択 ](/help/assets/assets/x.svg)」をクリックして、フォームとのフォルダーの関連付けを削除します。
1. ![ フォルダーを選択 ](/help/assets/assets/add-to-folder.svg) をクリックして、対応するメタデータフォームを割り当てるフォルダーを選択します。
1. 赤い円をクリックすると、インポートから除外されたサポートされていないメタデータコンポーネントまたはフォーム内のマッピングに関する詳細が表示されます。

   ![ メタデータFormsの読み込みページ ](/help/assets/assets/unsupported-import-elements.png)

1. テーブル内の 1 つ以上のフォームを選択し、**[!UICONTROL 読み込みの開始]** をクリックして、メタデータフォームとそれに関連するフォルダーを [!DNL Assets View] に読み込みます。 処理メッセージが表示されます（例：3 つのメタデータフォームの *読み込み。 お待ちください。*）。読み込みが完了すると、フォームが正常に読み込まれたことを示す成功メッセージが表示され、（[!DNL Assets View] の） **[!UICONTROL メタデータForms]** ページには、最近読み込まれたフォームと、[!DNL Assets View] で使用可能な既存のフォームの両方が表示されます。 このページでは、次の操作を実行できます。

   * 列見出しをクリックして、[!UICONTROL &#x200B; 名前 &#x200B;]、[!UICONTROL &#x200B; 変更済み &#x200B;]、または [!UICONTROL &#x200B; 作成者 &#x200B;] でテーブルを並べ替えます。
   * 読み込んだフォームを選択し、「**[!UICONTROL フォルダーから削除]**」をクリックしてフォルダーパスのフォルダー名を確認し、フォルダーが正しく移植されていることを確認します。

     ![ メタデータフォームページの確認 ](/help/assets/assets/confirm-ported-folder.png)
   * 読み込んだフォームを選択し、**[!UICONTROL 編集]** をクリックして、メタデータフォームのサポート対象のすべての設定を表示します。 メタデータフォーム、そのコンポーネントおよびフィールドについて詳しくは、[ メタデータFormsの設定 ](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/metadata#metadata-forms) を参照してください。

   ![ メタデータフォームページの確認 ](/help/assets/assets/verify-metadata-forms-page.png)

## 読み込んだメタデータフォームの確認{#Verify-the-imported-metadata-forms}

メタデータフォームを [!DNL Admin View] から [!DNL Assets View] に読み込んだ後、次の手順に従って読み込みを検証します。

1. 読み込んだメタデータフォームに関連付けられている任意のフォルダーに移動します。
1. [ アセットの詳細ページに移動し ](/help/assets/navigate-assets-view.md#preview-assets) サポートされているメタデータコンポーネント、コンポーネントフィールド、フィールド値が [!DNL Admin View] から同期されていることを確認します。 メタデータコンポーネント、コンポーネントフィールド、フィールド値について詳しくは、[Assets Essentials のメタデータ ](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/metadata) の記事を参照してください。

   >[!NOTE]
   >
   > [[!DNL Assets View]  詳細ページ ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms) または [[!DNL Admin View]  プロパティページ ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/administer/metadata-schemas) では、メタデータプロパティの値の変更は、2 つのインターフェイス間で自動的に同期されます。 ただし、フィールドの追加や削除、その他の変更など、フォームの構造の変更は同期されません。
