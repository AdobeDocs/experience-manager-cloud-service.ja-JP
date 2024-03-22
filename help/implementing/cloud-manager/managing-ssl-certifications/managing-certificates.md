---
title: SSL 証明書の管理
description: Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 7143ea8d36e26aa1674608ff7bd8ba22e2030b3c
workflow-type: ht
source-wordcount: '644'
ht-degree: 100%

---


# SSL 証明書の管理 {#managing-ssl-certificates}

Cloud Manager を使用して SSL 証明書のステータスを確認する方法と、SSL 証明書を編集、置換、更新および削除する方法について説明します。

## SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL 証明書のステータスは、SSL 証明書ページから一目で確認できます。

* **緑** - このステータスは、証明書が現在の日付から 14 日以上有効であることを示します。

* **オレンジ** - このステータスは、証明書の有効期限が 14 日未満であることを示します。
   * サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager のユーザーインターフェイスで証明書を更新して置き換える計画を必ず立ててください。
   * 証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。

* **赤** - このステータスは、SSL 証明書の有効期限が切れたことを示します。

## SSL 証明書の更新 {#update-ssl-certificate}

証明書の有効期限が切れると、有効期限切れの証明書で使用されているドメインは機能しなくなります。次の手順で証明書を更新すると、お使いのドメインが引き続き希望どおりに動作します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)**&#x200B;画面でプログラムを選択します。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. **環境**&#x200B;画面から **SSL 証明書**&#x200B;画面に移動します。
1. プログラムに正常にインストールされた各 SSL 証明書の行が記載された表が表示されます。更新する証明書の行の右端にある省略記号ボタンをクリックし、「**表示と更新**」を選択します。
1. 証明書の詳細が表示され、更新することができます。
1. パイプラインを実行して、更新された証明書をデプロイします。

>[!NOTE]
>
>Cloud Manager で SSL 証明書を更新するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

## SSL 証明書の置換 {#replace-ssl-certificate}

SSL 証明書は、[SSL 証明書の更新](#update-ssl-certificate)の節で説明している手順と同じ手順に従って置き換えることができます。

## SSL 証明書の削除 {#deleting-an-ssl-certificate}

Cloud Manager からの証明書の削除は、元に戻すことができない恒久的な操作です。ベストプラクティスとして、SSL ファイルをローカルに保存してから Cloud Manager で削除することをお勧めします。

Cloud Manager では、1 つ以上のドメインが関連付けられている SSL 証明書を削除できません。SSL 証明書を削除する前に、関連付けられているドメインをすべて削除する必要があります。詳しくは、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)を参照してください。

SSL 証明書を削除するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. **環境**&#x200B;画面から **SSL 証明書**&#x200B;画面に移動します。
1. プログラムに正常にインストールされた各 SSL 証明書の行が記載された表が表示されます。削除する証明書の行の右端にある省略記号をクリックし、「**削除**」を選択します。
1. **SSL 証明書を削除**&#x200B;ダイアログで削除を確定します。
1. パイプラインを実行して、削除した証明書のデプロイを解除します。

>[!NOTE]
>
>Cloud Manager で SSL 証明書を削除するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つメンバーである必要があります。

## 既存の CDN 設定 {#pre-existing-cdn}

SSL 証明書用の既存の CDN 設定がある場合は、UI を通じてこれらの設定を追加して Cloud Manager で表示および設定できるようにすることを促す情報メッセージが **SSL 証明書**&#x200B;ページに表示されます。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

IP 許可リストまたはカスタムドメイン名に対応する既存の CDN 設定がある環境の **IP 許可リスト**&#x200B;ページと&#x200B;**環境**&#x200B;ページにも、同様のメッセージが表示されます。
