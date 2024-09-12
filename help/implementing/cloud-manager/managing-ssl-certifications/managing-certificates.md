---
title: SSL 証明書の管理
description: Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 18%

---


# SSL 証明書の管理 {#managing-ssl-certificates}

Cloud Managerを使用して、顧客管理およびAdobe管理の SSL 証明書のステータスを確認する方法と削除方法について説明します。 顧客が管理する証明書の場合は、それらを編集および更新（置換）することもできます。

## SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL 証明書のステータスは、「**SSL 証明書** ページから一目で確認できます。

| SSL 証明書のステータス | 説明 |
| --- | --- |
| グリーン | 証明書は現在の日付から 14 日以上有効です。 |
| オレンジ | 証明書の有効期限は 14 日以内です。<br>・証明書を更新し、Cloud Manager ユーザーインターフェイスを介して証明書を置き換えて、サイトへのアクセスやサイトの停止を回避する計画があることを確認します。<br>・ Cloud Managerは、証明書の有効期限が間もなく切れることを通知する通常の通知を UI に送信します。 |
| レッド | SSL 証明書の有効期限が切れています。<br>[ 期限切れの顧客管理 SSL 証明書の更新 ](#update-ssl-certificate) または [SSL 証明書の削除 ](#deleting-an-ssl-certificate) を参照してください。 |

## 期限切れの顧客管理 SSL 証明書の更新 {#update-ssl-certificate}

顧客管理証明書の有効期限が切れると、有効期限切れの証明書で使用されているドメインは機能しなくなります。 証明書を更新することで、ドメインが引き続き希望どおりに動作します。

このタスクを完了するには、ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** の役割のメンバーである必要があります。

**期限切れの顧客管理 SSL 証明書を更新するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。
1. **概要**&#x200B;ページから、**環境**&#x200B;画面に移動します。
1. **環境** 画面から **SSL 証明書** 画面に移動します。
1. 更新する期限切れの顧客管理証明書の行で、右端にある省略記号ボタンをクリックし、「**表示と更新**」を選択します。

   ![ 期限切れの顧客管理 SSL 証明書の更新 ](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. **SSL 証明書の表示と更新** ダイアログボックスで、次の操作を行います。

   * （オプション）「**証明書名**」フィールドに、新しい名前を入力します。
   * 「**証明書**」フィールドに、新しい証明書コンテンツキーを貼り付けます。
   * 「**秘密鍵**」フィールドで、証明書に変更を加えた場合にのみ、このフィールドを更新します。
   * 「**証明書チェーン**」フィールド（または信頼チェーン）に、証明書チェーンを貼り付けます。

1. 「**更新**」をクリックして変更を保存し、自動的に適用します。

## 期限切れの顧客管理 SSL 証明書の置換 {#replace-ssl-certificate}

[ 期限切れの SSL 証明書の更新 ](#update-ssl-certificate) で説明したのと同じ手順に従って、期限切れの顧客管理 SSL 証明書を置き換えます。

## SSL 証明書の削除 {#deleting-an-ssl-certificate}

Cloud ManagerからAdobe管理または顧客管理の SSL 証明書を削除する操作は、元に戻すことができない恒久的な操作です。 Adobe ベストプラクティスとして、SSL ファイルをローカルに保存してからCloud Managerで削除することをお勧めします。

>[!NOTE]
>
>1 つ以上のアクティブなドメインが関連付けられているAdobe管理 SSL 証明書は削除できません。 SSL 証明書を削除する前に、関連付けられているすべてのアクティブなドメインを削除する必要があります。 詳しくは、[ カスタムドメイン名の管理 ](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) を参照してください。

このタスクを完了するには、ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** の役割のメンバーである必要があります。

**SSL 証明書を削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. **概要**&#x200B;ページから、**環境**&#x200B;画面に移動します。
1. **環境** 画面から **SSL 証明書** 画面に移動します。
1. 削除する証明書の行で、右端にある省略記号ボタンをクリックし、「**削除**」を選択します。
次の画像に示すように、「削除」ボタンに情報アイコンが表示されている場合は、上記のメモを参照してください。

   ![ 情報アイコン付きの削除ボタン ](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. **SSL 証明書を削除** ダイアログボックスで、**削除** をクリックして削除を確定します。
1. パイプラインを実行して、削除した証明書のデプロイを解除します。

## 既存の CDN 設定 {#pre-existing-cdn}

SSL 証明書用の CDN 設定が既にある場合は、**SSL 証明書** ページに情報メッセージが表示されます。 これらの設定を UI を通じて追加し、Cloud Managerで表示および管理できるようにすることをお勧めします。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。 メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは、[SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。

IP 許可リストまたはカスタムドメイン名に対応する既存の CDN 設定がある環境の **IP 許可リスト**&#x200B;ページと&#x200B;**環境**&#x200B;ページにも、同様のメッセージが表示されます。
