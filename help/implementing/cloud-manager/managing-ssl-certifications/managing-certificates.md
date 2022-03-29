---
title: SSL 証明書の管理
description: Cloud Manager を使用して SSL 証明書のステータスを確認する方法、および SSL 証明書の編集、置換、更新、削除の方法について説明します。
source-git-commit: 95539851590456b6b5ecbfeb0df8fc7bc7dde74b
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 30%

---


# SSL 証明書の管理 {#managing-ssl-certificates}

Cloud Manager を使用して SSL 証明書のステータスを確認する方法、および SSL 証明書の編集、置換、更新、削除の方法について説明します。

## SSL 証明書のステータスの確認 {#checking-status-an-ssl-certificate}

SSL 証明書のステータスは、SSL 証明書ページから一目で確認できます。

* **緑**  — このステータスは、証明書が現在の日付から 60 日以上有効であることを示します。

* **オレンジ**  — このステータスは、証明書の有効期限が 60 日未満であることを示します。
   * サイトへの不正アクセスやサイトの停止を回避するために、Cloud Manager UI で証明書を更新して置き換える計画を必ず立ててください。
   * 証明書の有効期限が間もなく切れることを警告する通知が Cloud Manager の UI に定期的に表示されます。

* **赤**  — このステータスは、SSL 証明書の有効期限が切れたことを示します。

## 既存の CDN 設定 {#pre-existing-cdn}

SSL 証明書用の既存の CDN 設定がある場合、 **SSL 証明書** UI を使用してこれらの設定を追加し、Cloud Manager で表示して設定できるようにすることを促すページ

UI を使用して既存のすべての環境設定を移行すると、メッセージは消えます。 メッセージが表示されなくなるまでに 1 ～ 2 営業日かかる場合があります。

ドキュメントを参照してください [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) を参照してください。

同様のメッセージが **IP許可リスト** そして **環境** IP ドメインまたはカスタムドメイン名用の既存の CDN 設定を持つ許可リスト向けのページ。

## SSL 証明書の更新 {#update-ssl-certificate}

証明書の有効期限が切れると、有効期限切れの証明書で使用されているドメインは機能しなくなります。次の手順で証明書を更新すると、ドメインが引き続き希望どおりに動作します。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. に移動します。 **環境** 画面から **概要** ページ。
1. 次に移動： **SSL 証明書** 画面から **環境** 画面
1. プログラムに正常にインストールされた各 SSL 証明書の行が記載された表が表示されます。更新する証明書の行の右端にある省略記号ボタンをクリックし、「 」を選択します。 **表示と更新**.
1. 証明書の詳細が表示され、更新できます。

>[!NOTE]
>
>ユーザーは、 **ビジネスオーナー** または **デプロイメントマネージャー** ロールを使用して、Cloud Manager で SSL 証明書を更新する必要があります。

## SSL 証明書の置換 {#replace-ssl-certificate}

SSL 証明書は、の節で説明している手順と同じ手順に従って置き換えることができます [SSL 証明書の更新。](#update-ssl-certificate)

## SSL 証明書の削除 {#deleting-an-ssl-certificate}

Cloud Manager からの証明書の削除は、取り消すことができない永続的な操作です。 ベストプラクティスとして、Adobeでは、SSL ファイルをローカルに保存してから、Cloud Manager で削除することをお勧めします。

Cloud Manager では、1 つ以上のドメインが関連付けられている SSL 証明書を削除できません。SSL 証明書を削除する前に、関連付けられているドメインをすべて削除する必要があります。ドキュメントを参照してください [カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) を参照してください。

SSL 証明書を削除するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. に移動します。 **環境** 画面から **概要** ページ。
1. 次に移動： **SSL 証明書** 画面から **環境** 画面
1. プログラムに正常にインストールされた各 SSL 証明書の行が記載された表が表示されます。削除する証明書の行の右端にある省略記号ボタンをクリックし、「 」を選択します。 **削除**.
1. 削除を **SSL 証明書を削除** ダイアログ。

>[!NOTE]
>
>ユーザーは、 **ビジネスオーナー** または **デプロイメントマネージャー** ロールを使用して、Cloud Manager で SSL 証明書を削除する必要があります。