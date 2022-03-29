---
title: アセットのダウンロード
description: ' [!DNL Adobe Experience Manager Assets]  からアセットをダウンロードする方法とダウンロード機能を有効または無効にする方法について説明します。'
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: ddc79a163e328d560912550900242cc089df3958
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 87%

---

# [!DNL Adobe Experience Manager] からのアセットのダウンロード  {#download-assets-from-aem}

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。または、アセットへのリンクを含む電子メールを [!DNL Adobe Experience Manager Assets] から直接送信できます。ダウンロードされたアセットは、ZIP ファイルにバンドルされています。<!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

Adobe Experience Manager アセットをダウンロードするには、次のいずれかの方法を使用します。

<!-- * [Link Share](#link-share-download) -->

* [Adobe Experience Manager ユーザーインターフェイス](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)
* [デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#download-assets)

## [!DNL Experience Manager] インターフェイスを使用したアセットのダウンロード  {#download-assets}

非同期ダウンロードサービスは、大規模なアセットをシームレスにダウンロードするためのフレームワークとなります。100GB を超えるダウンロードアーカイブは、それぞれ最大 100GB の複数の zip アーカイブに分割されます。これらは個別にダウンロードできます。サイズの小さいファイルはユーザーインターフェイスからリアルタイムでダウンロードされます。[!DNL Experience Manager] は、オリジナルファイルをダウンロードした単一アセットのダウンロードをアーカイブしません。この機能により、ダウンロードを高速化できます。

デフォルトでは、[!DNL Experience Manager] はダウンロードワークフローの完了時に通知をトリガーします。ダウンロード通知が [[!DNL Experience Manager] インボックス](/help/sites-cloud/authoring/getting-started/inbox.md) に表示されます。

![インボックス通知](assets/inbox-notification-for-large-downloads.png)


### 大量のダウンロードに対する電子メール通知を有効にする {#enable-emails-for-large-downloads}

>[!NOTE]
>
>この機能は、プレリリースチャネルで使用できます。 お使いの環境でこの機能を有効にする方法については、 [プレリリースチャネルドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) を参照してください。

非同期ダウンロードは、次のいずれかの場合にトリガーされます。

* 10 個を超えるアセットがある場合
* ダウンロードサイズが 100 MB を超える場合
* ダウンロードの準備に 30 秒以上かかる場合

非同期ダウンロードがバックエンドで実行される間、ユーザーは引き続き調査をおこない、Experience Managerでさらに作業をおこなうことができます。 ダウンロードプロセスの完了時にユーザーに通知するには、あらかじめ用意されているメカニズムが必要です。 この目的を達成するために、管理者は SMTP サーバーを設定して電子メールサービスを設定できます。 詳しくは、 [メールサービスの設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

電子メールサービスを設定すると、管理者とユーザーは、ユーザーインターフェイスから電子メール通知をExperience Managerできます。

電子メール通知を有効にするには：

1. [!DNL Experience Manager Assets] にログインします。
1. 右上隅にあるユーザーアイコンをクリックしてから、「**[!UICONTROL 環境設定]**」をクリックします。ユーザーの環境設定 ウィンドウが開きます。
1. を選択します。 **[!UICONTROL アセットのダウンロードの電子メール通知]** チェックボックスをオンにして、 **[!UICONTROL 確定]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


アセットをダウンロードするには、次の手順に従います。

1. Adobe [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;をクリックします。
1. ダウンロードするアセットに移動します。フォルダーを選択するか、フォルダー内の 1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。

   ![ からアセットをダウンロードする際に使用できるオプション[!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. ダウンロードダイアログボックスで、目的のダウンロードオプションを選択します。

   | ダウンロードオプション | 説明 |
   |---|---|
   | **[!UICONTROL アセットごとに別のフォルダーを作成]** | このオプションを選択すると、ダウンロードした各アセット（アセットの親フォルダーの下にネストされた子フォルダー内のアセットを含む）が、ローカルコンピューター上の 1 つのフォルダーに含まれます。このオプションを&#x200B;*選択しない場合*、デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルコンピューターの 1 つのフォルダーにダウンロードされます。 |
   | **[!UICONTROL 電子メール]** | （ダウンロードへのリンクを含む）メール通知を別のユーザーに送信する場合は、このオプションを選択します。受信者ユーザーは `dam-users` グループのメンバーである必要があります。次の場所にある標準の電子メールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> デプロイメント時にカスタマイズしたテンプレートは、次の場所で利用できます。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL アセット]** | レンディションを含めずに、元の形式でアセットをダウンロードする場合に、このオプションを選択します。<br>オリジナルアセットにサブアセットがある場合は、サブアセットオプションを使用できます。 |
   | **[!UICONTROL レンディション]** | レンディションは、アセットのバイナリ表現です。アセットは、（アップロードされたファイルの）一次表現を持ちます。アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットによって異なります。 |
   | **[!UICONTROL スマート切り抜き]** | このオプションを選択すると、選択したアセットのすべてのスマート切り抜きレンディションが Adobe [!DNL Experience Manager] 内からダウンロードされます。スマート切り抜きレンディションを含む zip ファイルが作成され、ローカルコンピューターにダウンロードされます。 |
   | **[!UICONTROL 動的レンディション]** | 一連の代替レンディションをリアルタイムで生成するには、このオプションを選択します。また、このオプションを選択すると、動的に作成するレンディションを [画像プリセット](/help/assets/dynamic-media/image-presets.md) リストから選択します。<br>さらに、サイズ、測定単位、形式、カラースペース、解像度および、画像の反転用などのオプションの画像修飾子を選択できます。このオプションは、[!DNL Dynamic Media] を有効にしている場合にのみ使用できます。 |

1. ダイアログボックスで、「**[!UICONTROL ダウンロード]**」をクリックします。

   大量のダウンロードに対するメール通知が有効になっている場合は、アーカイブされた zip フォルダーのダウンロード URL を記載したメールがインボックスに表示されます。 メールからダウンロードリンクをクリックして、zip フォルダーをダウンロードします。

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   また、[!DNL Experience Manager] インボックスで通知を表示することもできます。

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## リンク共有を使用して共有されたアセットのダウンロード {#link-share-download}

リンクを使用したアセットの共有は、関心のあるユーザーが [!DNL Assets] にログインしなくてもアセットを利用できるようにするための便利な方法です。[リンク共有機能](/help/assets/share-assets.md#sharelink) を参照してください。

ユーザーが共有リンクからアセットをダウンロードする場合、[!DNL Assets] では、高速で途切れないダウンロードを可能にする非同期サービスを使用します。ダウンロードされるアセットは、バックグラウンドで、扱いやすいファイルサイズの ZIP アーカイブにまとめられてインボックスのキューに入れられます。非常に大きなダウンロードファイルの場合は、最大 100 GB の複数のファイルに分割されます。

[!UICONTROL ダウンロードインボックス] には、各アーカイブの処理ステータスが表示されます。処理が完了したら、インボックスからアーカイブをダウンロードできます。

![ダウンロードインボックス](assets/link-sharing-download-inbox.png)

## アセットダウンロードサーブレットの有効化 {#enable-asset-download-servlet}

Adobe [!DNL Experience Manager] のデフォルトサーブレットを使用すると、認証済みユーザーは、任意の大きさの同時ダウンロードリクエストを発行してアセットの ZIP ファイルを作成できます。ダウンロードの準備でパフォーマンスに影響が及ぶ場合や、サーバーやネットワークに過重な負荷がかかる場合があります。この機能で生じる可能性がある DoS に似たリスクを軽減するため、パブリッシュインスタンスに対して `AssetDownloadServlet` OSGi コンポーネントが無効になっています。オーサーインスタンスでダウンロード機能が必要ない場合は、オーサーインスタンスでサーブレットを無効にします。

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

ダウンロード機能が必要ない場合は、サーブレットを無効にして、DoS に似たリスクを回避します。オーサーおよびパブリッシュインスタンスの `Asset Download Servlet` を無効にするには、アセットダウンロードリクエストをすべてブロックするように Dispatcher 設定をアップデートします。[!DNL Experience Manager]サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. Dispatcher 設定を通じてアセットダウンロード要求をブロックするには、`dispatcher.any` 設定を編集し、[フィルターセクション](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#configuring)に新しいルールを追加します。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## ヒントと制限事項 {#tips-limitations}

* 空のフォルダーをダウンロードすると、 [!DNL Experience Manager] は、ZIP アーカイブの作成に関する成功メッセージを伝えますが、アーカイブは作成されません。

>[!MORELIKETHIS]
>
>* [DRM で保護されたアセットのダウンロード](drm.md)
>* [Windows／Mac OS デスクトップで Adobe Experience Manager デスクトップアプリケーションを使用したアセットのダウンロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)
>* [サポートされている Adobe Creative Cloud アプリ内から Adobe Asset Link を使用したアセットのダウンロード](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)

