---
title: アセット、フォルダー、コレクションをリンクとして共有
description: ここでは、Adobe Experience Manager Assets 内のアセット、フォルダー、コレクションをハイパーリンクとして共有する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# アセットリンク共有の設定 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

ユーザーと共有するアセットの URL を生成するには、リンク共有ダイアログを使用します。`/var/dam/share` の場所への管理者特権または読み取り権限を持つユーザーが、共有されたリンクを表示することができます。リンクによるアセットの共有は、外部の関係者が AEM Assets にログインすることなくリソースを利用するための便利な方法です。

>[!NOTE]
>
>AEM オーサーインスタンスから外部エンティティへのリンクを共有する場合は、`GET` リクエストに対する次の URL のみ公開するようにします。AEM オーサーインスタンスの安全性を確保するために、その他の URL はブロックします。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Day CQ Mail Service の設定 {#configmailservice}

アセットをリンクとして共有するには、まず、電子メールサービスを設定します。

1. AEM のロゴをクリックまたはタップし、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。
1. サービスのリストから、**[!UICONTROL Day CQ Mail Service]** を探します。
1. サービスの横に表示されている&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをクリックして、**Day CQ Mail Service** のパラメーターを次のように設定します。

   * SMTP server host name：電子メールサーバーのホスト名
   * SMTP server port：電子メールサーバーのポート
   * SMTP user：メールサーバーのユーザー名
   * SMTP password：電子メールサーバーのパスワード

1. 「**Save**」をクリックまたはタップします。

## 最大データサイズの設定 {#maxdatasize}

リンク共有機能を使用して共有されているリンクからアセットをダウンロードすると、AEM は、リポジトリのアセットの階層を圧縮して、ZIP ファイルにしてアセットを返します。ただし、ZIP ファイルとして圧縮できるデータ量に制限がないと、膨大なデータが圧縮の対象となり、JVM のメモリ不足エラーの原因となります。この状況による潜在的な DoS 攻撃からシステムを保護するには、Configuration Manager で Day CQ DAM Adhoc Asset Share Proxy Servlet の「**Max Content Size (uncompressed)**」パラメーターを使用して、最大サイズを設定します。アセットの未圧縮時のサイズが設定値を超えていると、アセットのダウンロード要求は拒否されます。デフォルト値は 100 MB です。

1. AEM のロゴをクリックまたはタップし、**ツール**／**運営**／**Web コンソール**&#x200B;に移動します。
1. Web コンソールで、「**Day CQ DAM Adhoc Asset Share Proxy Servlet**」設定を見つけます。
1. 「**Day CQ DAM Adhoc Asset Share Proxy Servlet**」設定を編集モードで開き、「**Max Content Size (uncompressed)**」パラメーターの値を変更します。
1. 変更内容を保存します。

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
