---
title: SSL 証明書の管理
description: Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f12392075b71b219bf449f585f63561167ddada9
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 87%

---


# SSL 証明書の管理 {#managing-ssl-certificates}

Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。

## SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

Cloud Managerには、プログラムのすべての証明書のステータスの概要が表示されます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。
1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

**SSL 証明書** ページには、SSL 証明書のステータスが表示されます。

| SSL 証明書のステータス | 説明 |
| --- | --- |
| グリーン | 証明書は現在の日付から 14 日以上有効です。 |
| オレンジ | 証明書の有効期限は 14 日未満です。<br>• サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager のユーザーインターフェイスで証明書を更新して置き換える計画を必ず立ててください。<br>• 証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。 |
| レッド | SSL 証明書の有効期限が切れています。<br>詳しくは、[顧客が管理する期限切れの SSL 証明書の更新](#update-ssl-certificate)または [SSL 証明書の削除](#deleting-an-ssl-certificate)を参照してください。 |

## 顧客が管理する期限切れの SSL 証明書の更新 {#update-ssl-certificate}

顧客が管理する証明書の有効期限が切れると、有効期限切れの証明書で使用されているドメインは機能しなくなります。証明書を更新すると、お使いのドメインが引き続き希望どおりに動作します。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**顧客が管理する期限切れの SSL 証明書を更新するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。
1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。
1. 更新の対象となる、顧客が管理する期限切れの証明書の行で、右端にある省略記号ボタンをクリックして、「**表示と更新**」を選択します。

   ![顧客が管理する期限切れの SSL 証明書の更新](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. **SSL 証明書の表示と更新**&#x200B;ダイアログボックスで、次の操作を行います。

   * （オプション）「**証明書名**」フィールドに、新しい名前を入力します。
   * 「**証明書**」フィールドに、新しい証明書コンテンツキーを貼り付けます。
   * 「**秘密鍵**」フィールドでは、証明書に変更を加えた場合にのみ、このフィールドを更新します。
   * 「**証明書チェーン**」フィールド（または信頼チェーン）に、証明書チェーンを貼り付けます。

1. 「**更新**」をクリックして変更を保存し、自動的に適用されるようにします。


>[!NOTE]
>
>同じ SAN ドメイン・エントリーに対応する SAN 証明書が 2 つ以上ある場合、一方の証明書でそのドメインをカバーし、もう一方の証明書を更新すると、他方の証明書がドメインにインストールされます。
>
>詳しくは、[SSL 証明書の問題のトラブルシューティング ](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert) を参照してください。

## 顧客が管理する期限切れの SSL 証明書の置換 {#replace-ssl-certificate}

[期限切れの SSL 証明書の更新](#update-ssl-certificate)で説明したのと同じ手順に従って、顧客が管理する期限切れの SSL 証明書を置き換えます。

## アドビが管理する SSL 証明書の名前の変更（#rename-an-ssl-certificate）

SSL 証明書の名前を変更する必要がある理由を以下に示します。

* **組織の改善**：証明書の名前を変更すると、証明書の目的を明確にするのに役立ちます。例えば、目的の環境（ステージング、実稼動など）やドメインを識別できます。
* **混乱の回避**：複数の証明書を管理している場合、明確でわかりやすい名前を付けると、間違った証明書を間違ったドメインに適用するなどの誤りを防ぐのに役立ちます。
* **コンプライアンスと監査**：証明書に適切な名前が付けられていると、セキュリティや監査の目的での追跡が容易になります。

**アドビが管理する SSL 証明書の名前を変更するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

1. **SSL 証明書** ページで、**Adobe管理 ![SSL 証明書の名前を変更する行の最後にある** 詳細アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**名前を変更**」をクリックします。

1. **DV 証明書の名前を変更**&#x200B;ダイアログボックスの「**証明書名**」テキストフィールドに、証明書の新しい名前を入力します。

1. 「**名前を変更**」をクリックします。


## SSL 証明書の削除 {#deleting-an-ssl-certificate}

アドビまたは顧客が管理する SSL 証明書を Cloud Manager から削除する操作は、元に戻せない恒久的な操作です。ベストプラクティスとして、SSL ファイルをローカルに保存してから Cloud Manager で削除することをお勧めします。

>[!NOTE]
>
>アドビが管理する SSL 証明書のうち、1 つ以上のアクティブなドメインが関連付けられているものは削除できません。SSL 証明書を削除する前に、関連付けられているアクティブなドメインをすべて削除する必要があります。詳しくは、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)を参照してください。

このタスクを完了するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

**SSL 証明書を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、サイドメニューを表示します。

1. **サービス**&#x200B;見出しの下にある ![鍵がかかったアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) 「**SSL 証明書**」をクリックします。

1. SSL 証明書ページで、削除する証明書のテーブル行で、右端にある ![ その他のアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。

1. ドロップダウンメニューで、「**削除**」をクリックします。

   **削除** に情報アイコンが表示されている場合（下図を参照）、上記のメモを参照してください。

   ![情報アイコン付きの「削除」ボタン](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. **SSL 証明書を削除**&#x200B;ダイアログボックスで、「**削除**」をクリックして削除を確定します。

1. パイプラインを実行して、削除した証明書のデプロイを解除します。


## 既存の CDN 設定 {#pre-existing-cdn}

SSL 証明書の CDN 設定が既にある場合は、**SSL 証明書**&#x200B;ページに情報メッセージが表示されます。これらの設定を UI を通じて追加し、Cloud Manager で表示および管理できるようにすることをお勧めします。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

IP 許可リストまたはカスタムドメイン名に対応する既存の CDN 設定がある環境の **IP 許可リスト**&#x200B;ページと&#x200B;**環境**&#x200B;ページにも、同様のメッセージが表示されます。
