---
title: ' [!DNL Admin View]  から  [!DNL Assets View] へのメタデータフォームの読み込み'
description: この記事では、 [!DNL Admin View]  から  [!DNL Assets View] へのメタデータフォームの読み込み方法について説明します
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '547'
ht-degree: 100%

---

# [!DNL Admin View] から [!DNL Assets View] へのメタデータフォームの読み込み {#import-metadata-forms-from-admin-view-to-assets-view}

[!DNL Adobe Experience Manager Assets] を使用すると、メタデータフォームとそのフォルダーの関連付けを [!DNL Admin View] から [!DNL Assets View] に読み込むことができます。

## 始める前に{#prerequisites-for-importing-metadata-forms-to-assets-view}

メタデータフォームとそのフォルダーの関連付けを [!DNL Admin View] から [!DNL Assets View] に読み込むための管理者権限があることを確認します。

## [!DNL Assets View] へのメタデータフォームの読み込み{#import-metadata-forms-to-assets-view}

管理者として次の手順を実行し、[!DNL Admin View] で使用可能なメタデータフォームを [!DNL Assets View] に読み込みます。

1. [!DNL Assets View] ホームページに移動し、**[!UICONTROL 設定]**&#x200B;の下にある「**[!UICONTROL メタデータフォーム]**」をクリックして、[!DNL Assets View] で使用できるメタデータフォームのリストを表示する&#x200B;**[!UICONTROL メタデータフォーム]**&#x200B;ページを開きます。

   ![メタデータフォームページ](/help/assets/assets/metadata-forms-page.png)

1. 「**[!UICONTROL 読み込み]**」を選択すると、読み込みの処理中に処理メッセージが表示されます（例：*2 つのメタデータフォームを処理中... お待ちください*）。処理が完了すると、**[!UICONTROL メタデータフォームを読み込み]**&#x200B;テーブルが表示され、[!DNL Admin View] で使用できるメタデータフォームのリストが表示されます。テーブル行には、メタデータフォーム名（**[!UICONTROL 名前の下]**）、そのフォームに関連付けられたフォルダー（**[!UICONTROL フォルダーの関連付け]**&#x200B;の下）、フォームを読み込む前にプレビュー ![プレビュー](/help/assets/assets/Preview.svg) するオプションが含まれます。

   ![メタデータを読み込みページ](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > **[!UICONTROL メタデータフォームを読み込み]**&#x200B;テーブルで、フォーム名の横にある&#x200B;**[!UICONTROL 重複]**&#x200B;ラベルは、そのフォームが既に [!DNL Assets View] 内のフォルダーに適用されていることを示します。重複したフォームを読み込むと、フォルダーに適用されている既存のフォームが上書きされます。この上書きを回避するには、読み込む前にフォームの名前を変更します。名前を変更するには、フォーム名をクリックします。

1. フォルダー名の横にある ![フォルダーを選択](/help/assets/assets/x.svg)（[!UICONTROL フォルダーの関連付け]の下）をクリックして、フォームとのフォルダーの関連付けを削除します。
1. ![フォルダーを選択](/help/assets/assets/add-to-folder.svg) をクリックしてフォルダーを選択し、対応するメタデータフォームを割り当てます。
1. 赤い円をクリックして、読み込みから除外されるフォーム内のサポートされていないメタデータコンポーネントまたはマッピングの詳細を表示します。

   ![メタデータフォームを読み込みページ](/help/assets/assets/unsupported-import-elements.png)

1. テーブル内の 1 つ以上のフォームを選択し、「**[!UICONTROL 読み込みを開始]**」をクリックして、メタデータフォームとその関連付けられたフォルダーを [!DNL Assets View] に読み込みます。処理メッセージが表示されます（例：*3 つのメタデータフォームを読み込み中。お待ちください*）。読み込みが完了すると、フォームが正常に読み込まれたことを確認する成功メッセージが表示され、（[!DNL Assets View] の）**[!UICONTROL メタデータフォーム]**&#x200B;ページに、最近読み込まれたフォームと [!DNL Assets View] で使用可能な既存のフォームの両方が表示されます。このページでは、次の操作を実行できます。

   * 列ヘッダーをクリックして、テーブルを[!UICONTROL 名前]、[!UICONTROL 更新日時]または[!UICONTROL 作成者]で並べ替えます。
   * 読み込んだフォームを選択し、「**[!UICONTROL フォルダーから削除]**」をクリックして、フォルダーパス内のフォルダー名を確認し、フォルダーが正しく移植されていることを確認します。
     ![メタデータフォームを確認ページ](/help/assets/assets/confirm-ported-folder.png)
   * 読み込んだフォームを選択し、「**[!UICONTROL 編集]**」をクリックして、メタデータフォームでサポートされているすべての設定を表示します。メタデータフォーム、そのコンポーネントおよびフィールドについて詳しくは、[メタデータフォームの設定](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/metadata#metadata-forms)を参照してください。

   ![メタデータフォームを確認ページ](/help/assets/assets/verify-metadata-forms-page.png)

## 読み込んだメタデータフォームの確認{#Verify-the-imported-metadata-forms}

メタデータフォームを [!DNL Admin View] から [!DNL Assets View] に読み込んだ後、次の手順に従って読み込みを確認します。

1. 読み込んだメタデータフォームの関連フォルダーのいずれかに移動します。
1. [アセットの詳細ページ](/help/assets/navigate-assets-view.md#preview-assets)に移動し、サポートされているメタデータコンポーネント、コンポーネントフィールドおよびフィールド値が [!DNL Admin View] から同期されていることを確認します。メタデータコンポーネント、コンポーネントフィールドおよびフィールド値について詳しくは、[Assets Essentials のメタデータ](https://experienceleague.adobe.com/ja/docs/experience-manager-assets-essentials/help/metadata)の記事を参照してください。

   >[!NOTE]
   >
   > [[!DNL Assets View]  の詳細ページ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms)または [[!DNL Admin View]  のプロパティページ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/administer/metadata-schemas)では、メタデータプロパティ値の変更が 2 つのインターフェイス間で自動的に同期されます。ただし、フィールドの追加や削除、その他の変更など、フォームの構造的な変更は同期されません。
