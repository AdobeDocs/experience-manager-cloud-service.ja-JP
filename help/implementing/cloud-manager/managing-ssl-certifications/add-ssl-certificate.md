---
title: SSL 証明書の追加 - SSL 証明書の管理
description: SSL 証明書の追加 - SSL 証明書の管理
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 3b4a9d7c04a5f4feecad0f34c27a894c187152e7
workflow-type: ht
source-wordcount: '578'
ht-degree: 100%

---

# SSL 証明書の追加 {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as a Cloud Service では、OV（組織検証）証明書または EV（拡張検証）証明書のみを受け付けます。DV（ドメイン検証）証明書は受け付けられません。さらに、証明書はすべて、2048 ビットの RSA 秘密鍵と一致する信頼できる証明機関（CA）の X.509 TLS 証明書にする必要があります。AEM as a Cloud Service は、ドメインのワイルドカード SSL 証明書を受け付けます。

証明書のプロビジョニングには数日かかるので、数か月前からでも証明書をプロビジョニングすることをお勧めします。詳しくは、「[SSL 証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)」を参照してください。

## 証明書の形式 {#certificate-format}

SSL ファイルを Cloud Manager にインストールするには、SSL ファイルを PEM 形式にする必要があります。PEM 形式の一般的なファイル拡張子は `.pem,`、`crt`、`.cer`、`.cert` です。

SSL ファイルの形式を PEM に変換するには、次の手順に従います。

* PFX を PEM に変換

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* P7B を PEM に変換

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* DER を PEM に変換

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 重要な検討事項 {#important-considerations}

* Cloud Manager で SSL 証明書をインストールするには、ユーザーがビジネスオーナーまたはデプロイメントマネージャーの役割を持っている必要があります。

* Cloud Manager では、1 つ以上の環境に関連付けることができる SSL 証明書は、証明書の有効期限が切れている場合でも、プログラム全体で常に最大 10 個まで許可されます。ただし、Cloud Manager UI では、最大 50 個までの SSL 証明書をプログラムにインストールできます。通常、証明書は複数のドメイン（最大 100 個の SAN）に対応できるので、この制限内に収まるように、複数のドメインを同じ証明書でグループ化することを検討してください。


## 証明書の追加 {#adding-a-cert}

証明書を追加するには、次の手順に従います。

1. Cloud Manager にログインします。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. 画面左側のナビゲーションメニューで「**SSL 証明書**」をクリックします。既存の SSL 証明書の詳細を示す表がこの画面に表示されます。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 「**SSL 証明書を追加**」をクリックすると、**SSL 証明書を追加**&#x200B;ダイアログボックスが開きます。

   * 「**証明書名**」に証明書の名前を入力します。証明書を簡単に参照できる名前であれば何でもかまいません。
   * **証明書**、**秘密鍵**、**証明書チェーン**&#x200B;をそれぞれのフィールドに貼り付けます。入力ボックスの右側にある貼り付けアイコンを使用します。これら 3 つのフィールドはすべてオプションではなく、必須です。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >検出されたエラーが表示されます。証明書を保存する前に、すべてのエラーを解決する必要があります。一般的なエラーの対処方法の詳細については、「[証明書エラー](#certificate-errors)」を参照してください。

1. 「**保存**」をクリックして、証明書を送信します。証明書が表に新しい行として表示されます。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 証明書エラー {#certificate-errors}

### 正しい証明書の順序 {#correct-certificate-order}

証明書のデプロイに失敗する原因として最もよくあるのは、中間証明書またはチェーン証明書の順序が正しくないことです。特に、中間証明書ファイルは、ルート証明書またはルートに最も近い証明書で終わり、`main/server` 証明書からルートへの降順である必要があります。

中間ファイルの順序は、次のコマンドを使用して決定できます。

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

秘密鍵と `main/server` 証明書が一致することは、次のコマンドを使用して確認できます。

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>これらの 2 つのコマンドの出力は、完全に同じである必要があります。`main/server` 証明書と一致する秘密鍵が見つからない場合は、新しい CSR を生成するか、更新された証明書を SSL ベンダーに要求して、証明書を再入力する必要があります。

### 証明書の有効期限 {#certificate-validity-dates}

Cloud Manager で想定している SSL 証明書の有効期間は少なくとも 90 日間です。証明書チェーンの有効期限を確認します。
