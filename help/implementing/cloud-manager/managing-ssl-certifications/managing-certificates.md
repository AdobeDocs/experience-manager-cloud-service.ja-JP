---
title: SSL 証明書の管理
description: Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 51b9e7fd6fd51ee3565ff2c563e6d0c8a6283389
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 81%

---


# SSL 証明書の管理 {#managing-ssl-certificates}

Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。

## SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

Cloud Manager には、プログラムに対するすべての証明書のステータスの概要が表示されます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある「![ メニューアイコンを表示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)」をクリックして、サイドメニューを開きます。
1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

**SSL 証明書**&#x200B;ページには、SSL 証明書のステータスが表示されます。

| SSL 証明書のステータス | 説明 |
| --- | --- |
| グリーン | 証明書は現在の日付から 14 日以上有効です。 |
| オレンジ | 証明書の有効期限は14日以内です。<br> ・証明書を更新し、Cloud Manager ユーザーインターフェイスを介して置き換える計画があることを確認して、サイトへのアクセスや停止が発生する可能性を回避します。<br>・ Cloud Managerは、UIに定期的な通知を送信し、証明書の有効期限が差し迫っていることを通知します。 |
| レッド | SSL 証明書の有効期限が切れています。<br>詳しくは、[顧客が管理する期限切れの SSL 証明書の更新](#update-ssl-certificate)または [SSL 証明書の削除](#deleting-an-ssl-certificate)を参照してください。 |

## 顧客が管理する期限切れの SSL 証明書の更新 {#update-ssl-certificate}

顧客管理証明書の有効期限が切れると、期限切れの証明書で使用されているドメインは機能しなくなります。 証明書を更新すると、ドメインが引き続き正しく機能するようになります。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

>[!IMPORTANT]
>
>SSL 証明書を追加または更新する際は、新しい証明書を証明書チェーンに含めないでください。 含めると、アップロードが完了しません。

**顧客が管理する期限切れの SSL 証明書を更新するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。
1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。
1. 更新の対象となる、顧客が管理する期限切れの証明書の行で、右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、「**表示と更新**」をクリックします。

   ![顧客が管理する期限切れの SSL 証明書の更新](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. **SSL 証明書の表示と更新**&#x200B;ダイアログボックスで、次の操作を行います。

   * （オプション）「**証明書名**」フィールドに、新しい名前を入力します。
   * **証明書** フィールドに、新しい証明書の内容を貼り付けます。
   * 「**秘密鍵**」フィールドでは、証明書に変更を加えた場合にのみ、このフィールドを更新します。
   * 「**証明書チェーン**」フィールド（または信頼チェーン）に、証明書チェーンを貼り付けます。

1. 「**更新**」をクリックして変更を保存し、自動的に適用されるようにします。


>[!NOTE]
>
>2 つ以上の SAN 証明書が同じ SAN ドメインエントリをカバーし、そのうちの 1 つが更新されると、システムはそのドメインに対して更新された証明書をインストールします。
>
>詳しくは、[SSL 証明書問題のトラブルシューティング](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert)を参照してください。

## 顧客が管理する期限切れの SSL 証明書の置換 {#replace-ssl-certificate}

期限切れの顧客管理SSL証明書を置き換えるには、[期限切れのSSL証明書の更新](#update-ssl-certificate)に記載されている同じ手順に従います。

## アドビが管理する SSL 証明書の名前の変更（#rename-an-ssl-certificate）

SSL証明書の名前を変更する理由は次のとおりです。

* **組織の改善**：証明書の名前を変更すると、証明書の目的を明確にするのに役立ちます。例えば、目的の環境（ステージング、実稼動など）やドメインを識別できます。
* **混乱の回避**：複数の証明書を管理している場合、明確でわかりやすい名前を付けると、間違った証明書を間違ったドメインに適用するなどの誤りを防ぐのに役立ちます。
* **コンプライアンスと監査**：適切に名前が付けられた証明書は、セキュリティと監査の目的で追跡しやすくなります。

**アドビが管理する SSL 証明書の名前を変更するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

1. **SSL 証明書**&#x200B;ページで、名前を変更する&#x200B;**アドビが管理する** SSL 証明書の行の末尾にある、![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。

1. ドロップダウンメニューで、「**名前を変更**」をクリックします。

1. **DV 証明書の名前を変更**&#x200B;ダイアログボックスの「**証明書名**」テキストフィールドに、証明書の新しい名前を入力します。

1. 「**名前を変更**」をクリックします。


## SSL 証明書の削除 {#deleting-an-ssl-certificate}

アドビまたは顧客が管理する SSL 証明書を Cloud Manager から削除する操作は、元に戻せない恒久的な操作です。 ベストプラクティスとして、SSL ファイルをローカルに保存してから Cloud Manager で削除することをお勧めします。

>[!NOTE]
>
>アドビが管理する SSL 証明書のうち、1 つ以上のアクティブなドメインが関連付けられているものは削除できません。 SSL 証明書を削除する前に、関連付けられているアクティブなドメインをすべて削除する必要があります。 詳しくは、[ カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)を参照してください。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**SSL 証明書を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

1. SSL 証明書ページで、削除する証明書のテーブル行の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) 、「**削除**」の順にクリックします。

   **削除**&#x200B;に次の画像のような情報アイコンがある場合は、上記の注意を参照してください。

   ![情報アイコン付きの「削除」ボタン](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. **SSL 証明書を削除**&#x200B;ダイアログボックスで、「**削除**」をクリックして削除を確定します。

1. 削除された証明書のデプロイを解除するには、パイプラインを実行します。


## 既存の CDN 設定 {#pre-existing-cdn}

SSL 証明書の CDN 設定が既にある場合は、**SSL 証明書**&#x200B;ページに情報メッセージが表示されます。 これらの設定を UI を通じて追加し、Cloud Manager で表示および管理できるようにすることをお勧めします。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。 メッセージは1～2営業日以内に削除されます。

詳しくは、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

IP 許可リストまたはカスタムドメイン名に対応する既存の CDN 設定がある環境の **IP 許可リスト**&#x200B;ページと&#x200B;**環境**&#x200B;ページにも、同様のメッセージが表示されます。
