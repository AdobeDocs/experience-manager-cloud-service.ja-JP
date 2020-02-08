---
title: アセット、フォルダー、コレクションをリンクとして共有
description: この記事では、Experience Manager Assets内のアセット、フォルダーおよびコレクションをハイパーリンクとして共有する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# アセットリンクの共有の設定 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. リンクを使用したアセットの共有は、AEM Assetsに最初にログインしなくても、外部のユーザーがリソースを利用できるようにする便利な方法です。

>[!NOTE]
>
>AEM作成者インスタンスから外部エンティティへのリンクを共有する場合は、リクエストに対して次のURLのみを公開するようにし `GET` ます。 他のURLをブロックして、AEM作成者インスタンスが安全であることを確認します。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Day CQ Mail Service の設定 {#configmailservice}

アセットをリンクとして共有する前に、電子メールサービスを設定します。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

1. 「**Save**」をクリックまたはタップします。

## 最大データサイズの設定 {#maxdatasize}

リンク共有機能を使用して共有されているリンクからアセットをダウンロードすると、AEM は、リポジトリのアセットの階層を圧縮して、ZIP ファイルにしてアセットを返します。ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。To secure the system from a potential denial of service attack due to this situation, configure the maximum size using the **Max Content Size (uncompressed)** parameter for Day CQ DAM Adhoc Asset Share Proxy Servlet in Configuration Manager. アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. AEM のロゴをクリックまたはタップし、**ツール**／**運営**／**Web コンソール**&#x200B;に移動します。
1. From the web console, locate the **Day CQ DAM Adhoc Asset Share Proxy Servlet** configuration.
1. Open the **Day CQ DAM Adhoc Asset Share Proxy Servlet** configuration in edit mode, and modify the value of the **Max Content Size (uncompressed)** parameter.
1. 変更内容を保存します。

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
