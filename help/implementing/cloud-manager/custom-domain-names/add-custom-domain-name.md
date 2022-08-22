---
title: カスタムドメイン名の追加
description: Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 100%

---

# カスタムドメイン名の追加 {#adding-cdn}

Cloud Manager では、次の 2 つの場所からカスタムドメイン名を追加できます。

* [ドメイン設定ページから](#adding-cdn-settings)
* [環境ページから](#adding-cdn-environments)

>[!NOTE]
>
>Cloud Manager でカスタムドメイン名を追加するには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持っている必要があります

## ドメイン設定ページからのカスタムドメイン名の追加 {#adding-cdn-settings}

**ドメイン設定**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」をクリックします。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 右上の「**ドメインを追加**」ボタンをクリックして、**ドメイン名を追加**&#x200B;ダイアログを開きます。

   ![ドメインを追加ダイアログ](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 「**ドメイン名**」フィールドにカスタムドメイン名を入力します。

   >[!NOTE]
   >
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. そのドメイン名と関連付けられるサービスを持つ&#x200B;**環境**&#x200B;を選択します。

1. **公開**&#x200B;サービスまたは&#x200B;**プレビュー**&#x200B;サービスのいずれかを選択します。

1. ドロップダウンから、ドメイン名と関連付けられている「**ドメイン SSL 証明書**」を選択し、「**続行**」を選択します。

1. **ドメイン名を追加**&#x200B;ダイアログボックスが表示され、ドメイン名の検証プロセスが表示されます。表示される指示に従って、環境のドメイン所有権を証明します。「**作成**」をクリックします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。

様々なステータスと起こりうる問題への対処方法について詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントを参照してください。

>[!NOTE]
>
>DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントを参照してください。

>[!TIP]
>
>TXT レコードについて詳しくは、[TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。

## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

**環境**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 対象となる環境の、**環境の詳細**&#x200B;ページに移動します。

   ![環境の詳細ページでのドメイン名の入力](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. **ドメイン名**&#x200B;テーブルを使用してカスタムドメイン名を送信します。

   1. カスタムドメイン名を入力します。
   1. この名前に関連付けられている SSL 証明書をドロップダウンリストから選択します。
   1. 「**+ 追加**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **ドメイン名を追加**&#x200B;ダイアログボックスで選択した値を確認し、「**続行**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. **ドメイン名を追加**&#x200B;ダイアログボックスが表示され、ドメイン名の検証プロセスが表示されます。表示される指示に従って、環境のドメイン所有権を証明します。「**作成**」をクリックします。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。

様々なステータスと起こりうる問題への対処方法について詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントを参照してください。

>[!NOTE]
>
>DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。
>
>Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)ドキュメントを参照してください。

>[!TIP]
>
>TXT レコードについて詳しくは、[TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。
