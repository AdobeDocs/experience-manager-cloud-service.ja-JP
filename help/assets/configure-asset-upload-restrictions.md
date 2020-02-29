---
title: アセットのアップロード制限の設定
description: Adobe Experience Manager（AEM）Assets の設定でユーザーがアップロードできるアセット（ファイル）のタイプを制限する方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# アセットのアップロード制限の設定 {#configuring-asset-upload-restrictions}

Adobe Experience Manager（AEM）Assets の設定で、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。この機能により、望ましくない形式や悪意のあるファイルがユーザーによってアップロードされないようにすることができます。The `Day CQ DAM Asset Upload Restriction` service enables you to control the type of files that users can upload. デフォルトでは、AEM Assets はすべての MIME タイプのアセットのアップロードを許可します。ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager webコンソールを開きます。 アクセス `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Asset Upload Restriction]** service in Edit mode. By default, the **Allow all MIME** option is selected, which allows users to upload files of all MIME types.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. アップロードを特定の MIME タイプのファイルのみに制限するには、「**[!UICONTROL すべての MIME を許可]**」オプションをオフにして、「**[!UICONTROL 許可されている Asset MIME (regex)]**」フィールドに許可する MIME タイプを正規表現で指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックし、キャンペーンを保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
