---
title: ' [!DNL Assets] 内ファイルのチェックインとチェックアウト'
description: 編集のためにアセットをチェックアウトし、変更が完了した後にアセットをチェックインする方法について説明します。
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 89%

---

# [!DNL Experience Manager] DAM 内ファイルのチェックイン、チェックアウト  {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] では、編集のためにアセットをチェックアウトし、変更終了後にアセットをチェックインすることができます。アセットをチェックアウトした後は、その人だけがアセットを編集、注釈、公開、移動、削除できるようになります。アセットのチェックアウトでアセットにロックがかかることになります。アセットが [!DNL Assets] にチェックインされるまで、他のユーザーはそのアセットではどんな作業も行えません。ただし、ロックされたアセットのメタデータは変更することができます。

アセットをチェックイン／チェックアウトするには、アセットへの書き込み権限が必要です。

この機能は、複数のユーザーがチーム間でワークフローの編集で共同作業する場合に、作成者が加えた変更が他のユーザーによって上書きされるのを防ぐのに役立ちます。

## アセットのチェックアウト {#checking-out-assets}

1. [!DNL Assets] ユーザーインターフェイスでチェックアウトするアセットを選択します。チェックアウトしたいアセットは複数選択することもできます。

1. ツールバーの「**[!UICONTROL チェックアウト]**」をクリックします。「**[!UICONTROL チェックアウト]**」オプションが「**[!UICONTROL チェックイン]**」に変わります。
チェックアウトしたアセットを他のユーザーが編集できるかを確認するには、別のユーザーとしてログインします。チェックアウトしたアセットのサムネールに、![チェックアウトロックアイコン](assets/do-not-localize/checkout_lock.png)が表示されます。

   ![カード表示のチェックアウトアイコン](assets/checkout-icon-card-view.png)

   アセットを選択します。アセットを編集、注釈、公開、削除するためのオプションはツールバーに表示されません。

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   ロックされたアセットのメタデータを編集するには、「**[!UICONTROL プロパティを表示]**」をクリックします。

1. 「**[!UICONTROL 編集]**」をクリックして、アセットを編集モードで開きます。

1. アセットを編集して、変更内容を保存します。例えば、画像を切り抜いて保存します。アセットに注釈を付けたり公開したりすることもできます。

1. [!DNL Assets] インターフェイスで編集したアセットを選択し、ツールバーの「**[!UICONTROL チェックイン]**」をクリックします。変更されたアセットは [!DNL Assets] にチェックインされ、他のユーザーが編集できるようになります。

## 強制チェックイン {#forced-check-in}

管理者は他のユーザーがチェックアウトしたアセットをチェックインできます。

1. 管理者として [!DNL Assets] にログインします。
1. [!DNL Assets] ユーザーインターフェイスで他のユーザーにチェックアウトされているアセットを 1 つ以上選択します。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. ツールバーの「**[!UICONTROL ロックを解除]**」をクリックします。アセットはチェックインされ、他のユーザーが編集できるようになります。

## ベストプラクティスと制限事項 {#tips-limitations}

* チェックアウトされたアセットファイルを含む&#x200B;*フォルダー*&#x200B;を削除できます。フォルダーを削除する前に、ユーザーがチェックアウトしているデジタルアセットがないことを確認します。

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットの検索](search-assets.md)
* [Connected Assets](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットのダウンロード](download-assets-from-aem.md)
* [メタデータの管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションの管理](manage-collections.md)
* [一括メタデータ読み込み](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#how-app-works2)でのチェックインとチェックアウトについて
>* [チェックインとチェックアウトについて説明するビデオチュートリアル [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html?lang=ja)

