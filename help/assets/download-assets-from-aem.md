---
title: AEM からのアセットのダウンロード
description: AEM からアセットをダウンロードする方法とダウンロード機能を有効または無効にする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12575cd2f046d3a382786811dd28fec8df3be8bd
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 56%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。Alternatively, you can send emails with links to assets directly from [!DNL Adobe Experience Manager Assets]. ダウンロードされたアセットは、ZIP ファイルにバンドルされています。書き出しジョブ用に圧縮する ZIP ファイルの最大サイズは 1 GB です。書き出しジョブあたり、最大で500個のアセットの合計を指定できます。

>[!NOTE]
>
>電子メールの受信者は、電子メールメッセージに含まれる ZIP ダウンロードリンクにアクセスするためには、`dam-users` グループのメンバーである必要があります。アセットをダウンロードするためには、アセットのダウンロードを起動するワークフローを開始する権限が必要です。

画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

**アセットをダウンロードするには**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Navigation]** (Compass icon).
1. On the Navigation page, tap **[!UICONTROL Assets > Files]**.
1. ダウンロードするアセットを含むフォルダーに移動します。
1. フォルダーを選択するか、フォルダー内の1つ以上のアセットを選択します。
1. On the toolbar, tap **[!UICONTROL Download]**.

   ![Experience Managerアセットからアセットをダウンロードする場合に使用できるオプション](/help/assets/assets/asset-download1.png)

   *ダウンロードダイアログボックスのオプション*

1. ダウンロードダイアログボックスで、目的のダウンロードオプションを選択します。

   | ダウンロードオプション | 説明 |
   |---|---|
   | **[!UICONTROL アセットごとに別のフォルダーを作成]** | このオプションを選択すると、ダウンロードした各アセット（アセットの親フォルダーの下にネストされた子フォルダー内のアセットを含む）が、ローカルコンピューター上の1つのフォルダーに含まれます。 このオプションを *選択しない場合* 、デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルコンピューターの1つのフォルダーにダウンロードされます。 |
   | **[!UICONTROL 電子メール]** | 受信者に電子メール通知を送信する場合は、このオプションを選択します。 次の場所にある標準の電子メールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> 展開時にカスタマイズしたテンプレートは、次の場所で利用できます。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL アセット]** | レンディションなしで元の形式でアセットをダウンロードする場合は、このオプションを選択します。<br>元のアセットにサブアセットが含まれている場合は、「サブアセット」オプションを使用できます。 |
   | **[!UICONTROL レンディション]** | レンディションは、アセットのバイナリ表現です。アセットは、（アップロードされたファイルの）一次表現を持ちます。アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットによって異なります。 |
   | **[!UICONTROL スマート切り抜き]** | このオプションを選択すると、選択したアセットのすべてのスマートトリミングレンディションがAEM内からダウンロードされます。 スマート切り抜きレンディションを含むzipファイルが作成され、ローカルコンピューターにダウンロードされます。 |
   | **[!UICONTROL 動的レンディション]** | 一連の代替レンディションをリアルタイムで生成するには、このオプションを選択します。 When you select this option, you also select the renditions that you want to create dynamically by selecting from the [Image Preset](/help/assets/dynamic-media/image-presets.md) list. <br>また、測定のサイズと単位、形式、カラースペース、解像度、および画像の反転などのオプションの画像修飾子を選択できます。 このオプションは、有効にしている場合にのみ使用でき [!DNL Dynamic Media] ます。 |

1. ダイアログボックスで、「 **[!UICONTROL ダウンロード]**」をタップします。


## アセットダウンロードサーブレットの有効化 {#enable-asset-download-servlet}

AEM のデフォルトサーブレットを使用すると、認証されたユーザーは、表示可能なアセットの ZIP ファイルを作成するために任意のサイズの同時ダウンロード要求を発行することができますが、その結果、サーバーやネットワークに過剰な負荷をかけるおそれがあります。この機能で生じる可能性がある DoS リスクを軽減するために、パブリッシュインスタンスに対しては、`AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。

例えば Asset Share Commons やポータルのような実装などを使用する場合に DAM からアセットをダウンロードできるようにするには、OSGi 設定を通じてサーブレットを手動で有効にします。日常的なダウンロードの要件に影響を与えない範囲で、許容ダウンロードサイズをできるだけ小さく設定することをお勧めします。この値を大きくすれば、パフォーマンスに影響を与える可能性があります。

1. 次のように、パブリッシュ実行モードを対象とする命名規則（`config.publish`）でフォルダーを作成します。

   `/apps/<your-app-name>/config.publish`

1. config フォルダーに、`nt:file` タイプのファイル `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` を新しく作成します。
1. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` に以下を入力します。ダウンロードの最大サイズ（バイト単位）を `asset.download.prezip.maxcontentsize` の値として設定します。以下のサンプルでは、ZIP ダウンロードの最大サイズを 100 KB を超えないように設定しています。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## アセットダウンロードサーブレットの無効化 {#disable-asset-download-servlet}

AEM パブリッシュインスタンスの `Asset Download Servlet` を無効にするには、アセットダウンロード要求をすべてブロックするように Dispatcher 設定を更新します。サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. Dispatcher 設定を通じてアセットダウンロード要求をブロックするには、`dispatcher.any` 設定を編集し、[フィルターセクション](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)に新しいルールを追加します。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [DRM で保護されたアセットのダウンロード](drm.md)
>* [Windows または Mac OS デスクトップで AEM デスクトップアプリケーションを使用したアセットのダウンロード](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)
>* [サポートされている Adobe Creative Cloud アプリ内から Adobe Asset Link を使用したアセットのダウンロード](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)

