---
title: アセットのアップロード制限の設定
description: Adobe Experience Manager（AEM）Assets の設定でユーザーがアップロードできるアセット（ファイル）のタイプを制限する方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# アセットのアップロード制限の設定 {#configuring-asset-upload-restrictions}

Adobe Experience Manager（AEM）Assets の設定で、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。この機能により、望ましくない形式や悪意のあるファイルがユーザーによってアップロードされないようにすることができます。The `Day CQ DAM Asset Upload Restriction` service enables you to control the type of files that users can upload. デフォルトでは、AEM Assets はすべての MIME タイプのアセットのアップロードを許可します。ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager webコンソールを開きます。 アクセス `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Asset Upload Restriction]** service in Edit mode. By default, the **Allow all MIME** option is selected, which allows users to upload files of all MIME types.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL llow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click/tap **[!UICONTROL Save]** to save the changes. 許可されているMIMEタイプにMIME文字列を指定した場合、これらのフィールドで設定されているMIME文字列と一致しないMIMEタイプを持つアセットに対するアップロード操作は失敗します。

