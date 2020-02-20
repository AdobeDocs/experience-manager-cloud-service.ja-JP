---
title: AEM からのアセットのダウンロード
description: AEM からアセットをダウンロードする方法とダウンロード機能を有効または無効にする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# AEM からのアセットのダウンロード {#download-assets-from-aem}

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。または、アセットへのリンクを含む電子メールを AEM Assets から直接送信できます。ダウンロードされたアセットは、ZIP ファイルにバンドルされています。書き出しジョブ用に圧縮する ZIP ファイルの最大サイズは 1 GB です。1 つの書き出しジョブに許可されるアセットの合計数は最大 500 個です。

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. アセットをダウンロードするためには、アセットのダウンロードを起動するワークフローを開始する権限が必要です。

To download assets, navigate to an asset, select the asset, and tap/click the **[!UICONTROL Download]** icon from the toolbar. 表示されるダイアログで、ダウンロードオプションを指定します。

画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

![AEM Assets図からアセットをダウンロードする際に使用できるオプ](assets/asset_download_dialog.png)*ション：AEM Assetsからアセットをダウンロードする際に使用できるオプション*

次に、書き出し／ダウンロードのオプションを示します。動的レンディションは Dynamic Media 特有の機能であり、選択したアセットに加えてレンディションもその場で生成できます。このオプションは、Dynamic Media を有効にしている場合のみ利用できます。

| 書き出しまたはダウンロードのオプション | 説明 |
|---|---|
| [!UICONTROL Assets] | レンディションを含めずに、元の形式でアセットをダウンロードする場合に選択します。 |
| [!UICONTROL レンディション] | レンディションは、アセットのバイナリ表現です。アセットは、（アップロードされたファイルの）一次表現を持ちます。アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットによって異なります。 |
| [!UICONTROL 動的レンディション] | 動的レンディションでは、他のレンディションをその場で生成します。このオプションを選択すると、画像プリセットリストから選択して、動的に作成するレンディションも選択します。 さらに、サイズ、測定単位、形式、カラースペース、解像度および画像の修飾子（例：画像の反転用）を選択できます。 |
| [!UICONTROL 電子メール] | ユーザーに電子メール通知が送信されます。次の場所にある標準の電子メールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> デプロイ時にカスタマイズするテンプレートは、次の場所に存在している必要があります。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> |
| [!UICONTROL アセットごとに別のフォルダーを作成] | フォルダー階層を保持したままアセットをダウンロードするには、このオプションを選択します。デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルシステムの1つのフォルダーにダウンロードされます。 |

アセットにレンディションがある場合は、レンディションオプションを使用できます。アセットにサブアセットが含まれている場合は、サブアセットオプションを使用できます。

ダウンロードするフォルダーを選択すると、そのフォルダーの下位のアセットの階層全体がダウンロードされます。ダウンロードする各アセット（親フォルダーの下にネストされている子フォルダーのアセットを含む）を個々のフォルダーに格納するには、「**[!UICONTROL アセットごとに別のフォルダーを作成]**」を選択します。

## Enable asset download servlet {#enable-asset-download-servlet}

AEM のデフォルトサーブレットを使用すると、認証されたユーザーは、表示可能なアセットの ZIP ファイルを作成するために任意のサイズの同時ダウンロード要求を発行することができますが、その結果、サーバーやネットワークに過剰な負荷をかけるおそれがあります。To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

例えば Asset Share Commons やポータルのような実装などを使用する場合に DAM からアセットをダウンロードできるようにするには、OSGi 設定を通じてサーブレットを手動で有効にします。日常的なダウンロードの要件に影響を与えない範囲で、許容ダウンロードサイズをできるだけ小さく設定することをお勧めします。この値を大きくすれば、パフォーマンスに影響を与える可能性があります。

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. ダウンロードの最大サイズ（バイト単位）を `asset.download.prezip.maxcontentsize` の値として設定します。以下のサンプルでは、ZIP ダウンロードの最大サイズを 100 KB を超えないように設定しています。

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. Dispatcher 設定を通じてアセットダウンロード要求をブロックするには、`dispatcher.any` 設定を編集し、[フィルターセクション](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)に新しいルールを追加します。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [DRM で保護されたアセットのダウンロード](drm.md)
>* [WinまたはMacデスクトップでAEMデスクトップアプリケーションを使用してアセットをダウンロードする](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [サポートされているAdobe Creative cloudアプリケーションから「Adobe Assets Link」を使用してアセットをダウンロードします](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

