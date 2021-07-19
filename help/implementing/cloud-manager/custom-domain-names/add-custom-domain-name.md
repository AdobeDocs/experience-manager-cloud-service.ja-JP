---
title: カスタムドメイン名の追加
description: カスタムドメイン名の追加
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 94%

---

# カスタムドメイン名の追加 {#adding-cdn}

Cloud Manager でカスタムドメイン名を追加するには、ユーザーがビジネスオーナーまたはデプロイメントマネージャーでなければなりません。

## 重要な検討事項 {#important-considerations}

* カスタムドメイン名を追加する前に、カスタムドメイン名を含んだ有効な SSL 証明書をプログラムにインストールする必要があります。詳しくは、[SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

* 現在実行中のパイプラインが環境に接続されている間は、その環境にドメイン名を追加することはできません。

* 一度に追加できるドメイン名は 1 つだけです。ただし、ドメインにワイルドカードを含めることはできません。オーサー側のカスタムドメインはサポートされていません。

* AEM as a Cloud Service は、ワイルドカードドメインをサポートしていません。

* 各 Cloud Manager 環境は、1 つの環境につき最大 500 個のカスタムドメインをホストできます。

* 同じドメイン名を複数の環境で使用することはできません。

## ドメイン設定ページからのカスタムドメイン名の追加 {#adding-cdn-settings}

ドメイン設定ページからカスタムドメイン名を追加するには、次の手順に従います。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションメニューで「**ドメイン設定**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 「**ドメインを追加**」ボタンをクリックして、**ドメイン名を追加**&#x200B;ダイアログボックスを開きます。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 「**ドメイン名**」にカスタムドメイン名を入力します。

   >[!NOTE]
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. そのドメイン名と関連付けられるパブリッシュサービスを持つ&#x200B;**環境**&#x200B;を選択します。

1. 「**パブリッシュ**」または「**プレビュー**」としてサービスを選択します。

   >[!NOTE]
   >パブリッシュサービスとプレビューサービスの両方で、Cloud Managerのサイトプログラムでカスタムドメイン名がサポートされるようになりました。 各 Cloud Manager 環境は、1 つの環境につき最大 250 個のカスタムドメインをホストできます。Preview Serviceの詳細については、「[Preview Service](/help/implementing/cloud-manager/manage-environments.md#preview-service)」を参照してください。

1. ドロップダウンから&#x200B;**ドメイン SSL 証明書**&#x200B;を選択し、「**続行**」をクリックします。

1. **ドメイン名を追加**&#x200B;ダイアログボックスが表示されます。環境のドメイン名検証画面が開きます。詳しくは、[TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。

   表示される指示に従って、環境のドメイン所有権を証明します。

1. 「**作成**」をクリックします。
1. CDN デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。様々なステータスとその対処方法について詳しくは、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

   >[!NOTE]
   >DNS 伝達の遅延により、DNS 配達確認が認識されるまでに最大で数時間かかる場合があります。Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、「ドメイン名のステータスの確認」を参照してください。

## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

1. 対象となる環境の環境詳細ページに移動します。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. ドメイン名テーブルの上部にある入力フィールドを使用して、カスタムドメイン名を送信し、ドロップダウンリストから SSL 証明書を選択します。「**+ 追加**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **ドメイン名を追加**&#x200B;ダイアログボックスのフィールドを確認し、「**続行**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. 環境のドメイン名検証画面が表示されます。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   詳しくは、[ドメインの検証](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。表示される指示に従って、環境のドメイン所有権を証明します。

1. 「**作成**」をクリックします。

1. カスタムドメイン名デプロイメントの場合は、有効な SSL 証明書が必要で、TXT 検証に成功している必要があります。これは、ステータス&#x200B;**検証済みかつデプロイ済み**&#x200B;のステータスで示されます。

これで、カスタムドメイン名がテスト用に準備され、`CNAME` がそれを指すようになります。様々なステータスとその対処方法について詳しくは、[ドメイン名のステータス](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

>[!NOTE]
>DNS 伝達の遅延により、DNS 配達確認が認識されるまでに最大で数時間かかる場合があります。Cloud Manager が所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。詳しくは、「ドメイン名のステータスの確認」を参照してください。
