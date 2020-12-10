---
title: カスタムドメイン名の追加
description: カスタムドメイン名の追加
translation-type: tm+mt
source-git-commit: 27e96d66d93f2fa0e67e607c75f37efda17a13b7
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# カスタムドメイン名の追加{#adding-cdn}

Cloud Managerでカスタムドメイン名を追加するには、ユーザーがビジネス所有者またはデプロイメントマネージャーである必要があります。

## 重要な検討事項 {#important-considerations}

* カスタムドメイン名を追加する前に、カスタムドメイン名を含む有効なSSL証明書をプログラムにインストールする必要があります。 詳しくは、[SSL証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)を参照してください。

* 一度に追加できるドメイン名は1つだけです。 ただし、ワイルドカードをドメイン名として追加することはできます。例えば`*.wknd.com`を追加すると、複数のサブドメインを1つのTXTレコードでホストできます。

* 各Cloud Manager環境は、1つの環境につき最大100個のカスタムドメインをホストできます。

* 同じドメイン名を複数の環境で使用することはできません。

## ドメイン設定ページからのカスタムドメイン名の追加{#adding-cdn-settings}

次の手順に従って、ドメイン設定ページからカスタムドメイン名を追加します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 画面左側のナビゲーションメニューで[**ドメイン設定**]をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 「**追加ドメイン**」ボタンをクリックして、**ドメイン名**&#x200B;追加ダイアログボックスを開きます。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. 「**ドメイン名**」にカスタムドメイン名を入力します。

   >[!NOTE]
   >ドメインに入力する際は、`http://`、`https://`、またはスペースを含めないでください。

1. 発行サービスをドメイン名に関連付ける&#x200B;**環境**&#x200B;を選択します。

1. ドロップダウンから「**Domain SSL Certificate**」を選択し、「**Continue**」を選択します。

1. **追加[ドメイン** 名]ダイアログボックスが表示されます。[環境名の検証]画面が開きます。 詳しくは、[TXTレコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。
表示される手順に従って、環境のドメイン所有権を証明します。

1. 「**作成**」をクリックします。
1. CDNデプロイメントには、有効なSSL証明書が必要で、TXT検証に成功している必要があります。 これは、ステータス&#x200B;**検証済みで展開済み**で示されます。
様々なステータスと対処方法の詳細については、[カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

   >[!NOTE]
   >DNSの伝達が遅延するため、DNS配達確認が認識するのに最大で数時間かかる場合があります。 Cloud Managerは、所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。 詳細は、「ドメイン名のステータスの確認」を参照してください。

## 環境ページからのカスタムドメイン名の追加{#adding-cdn-environments}

1. 目標環境の「環境詳細」ページにナビゲートします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 「Domain Names」テーブルの上部にある入力フィールドを使用してカスタムドメイン名を送信し、ドロップダウンリストからSSL証明書を選択します。 **+追加**&#x200B;をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 「**追加ドメイン名**」ダイアログボックスのフィールドを確認し、「**継続**」をクリックします。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >ドメインに入力する際は、`http://`、`https://`、スペースを含めないでください。

1. 「Domain Name Verification for your環境」画面が表示されます。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   詳しくは、[ドメインの検証](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)を参照してください。 表示される手順に従って、環境のドメイン所有権を証明します。

1. 「**作成**」をクリックします。

1. カスタムドメイン名の展開には、有効なSSL証明書が必要で、TXT検証に成功している必要があります。 これは、ステータス&#x200B;**検証済みで展開済み**&#x200B;で示されます。

この時点で、カスタムドメイン名はテスト用に準備され、`CNAME`がそれを指し示します。 様々なステータスと対処方法の詳細については、[ドメイン名のステータス](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)を参照してください。

>[!NOTE]
>DNSの伝達が遅延するため、DNS配達確認が認識するのに最大で数時間かかる場合があります。 Cloud Managerは、所有権を検証し、ドメイン設定テーブルに表示されるステータスを更新します。 詳しくは、「ドメイン名のステータスを確認する」を参照してください。
