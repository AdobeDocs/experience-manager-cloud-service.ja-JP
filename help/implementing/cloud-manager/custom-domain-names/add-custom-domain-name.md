---
title: カスタムドメイン名の追加
description: Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 29%

---

# カスタムドメイン名の追加 {#adding-cdn}

Cloud Manager では、次の 2 つの場所からカスタムドメイン名を追加できます。

* [ドメイン設定ページから](#adding-cdn-settings)
* [環境ページから](#adding-cdn-environments)

>[!NOTE]
>
>ユーザーが **ビジネスオーナー** または **デプロイメントマネージャー** Cloud Manager でカスタムドメイン名を追加するための役割

## ドメイン設定ページからのカスタムドメイン名の追加 {#adding-cdn-settings}

次の手順に従って、 **ドメイン設定** ページ。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **環境** 画面から **概要** ページ。

1. クリック **ドメイン設定** をクリックします。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. をクリックします。 **ドメインを追加** 右上のボタンで **ドメイン名を追加** ダイアログ。

   ![ドメインを追加ダイアログ](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. カスタムドメイン名を **ドメイン名** フィールドに入力します。

   >[!NOTE]
   >
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. を選択します。 **環境** ドメイン名に関連付けられるサービスを持つユーザー。

1. 次のいずれかを選択します。 **公開** または **プレビュー** サービス。

1. を選択します。 **ドメイン SSL 証明書** 関連付けられているドメイン名をドロップダウンから選択し、 **続行**.

1. この **ドメイン名を追加** ダイアログボックスが表示され、ドメイン名の検証プロセスが表示されます。 表示される指示に従って、環境のドメイン所有権を証明します。「**作成**」をクリックします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。

ドキュメントを参照します。 [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 様々なステータスの詳細と、潜在的な問題に対処する方法を確認します。

>[!NOTE]
>
>DNS の伝達遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。ドキュメントを参照します。 [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) を参照してください。

>[!TIP]
>
>参照： [TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) TXT レコードの詳細を表示します。

## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

次の手順に従って、 **環境** ページ。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. に移動します。 **環境の詳細** ページを開きます。

   ![環境の詳細ページでのドメイン名の入力](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 以下を使用： **ドメイン名** カスタムドメイン名を送信するテーブル。

   1. カスタムドメイン名を入力します。
   1. この名前に関連付けられている SSL 証明書をドロップダウンリストから選択します。
   1. 「**+ 追加**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 選択した値を **ドメイン名を追加** ダイアログボックスで **続行**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >次を含めない `http://`, `https://`またはスペースでドメイン名にを入力する場合。

1. この **ドメイン名を追加** ダイアログボックスが表示され、ドメイン名の検証プロセスが表示されます。 表示される指示に従って、環境のドメイン所有権を証明します。「**作成**」をクリックします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。

ドキュメントを参照します。 [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 様々なステータスの詳細と、潜在的な問題に対処する方法を確認します。

>[!NOTE]
>
>DNS の伝達遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。ドキュメントを参照します。 [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) を参照してください。

>[!TIP]
>
>参照： [TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) TXT レコードの詳細を表示します。
