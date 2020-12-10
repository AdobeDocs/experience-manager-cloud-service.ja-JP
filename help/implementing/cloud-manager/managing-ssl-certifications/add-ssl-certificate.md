---
title: SSL証明書の追加 — SSL証明書の管理
description: SSL証明書の追加 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: 1e7855661220f69038edf35d4c45b7d45b5c6bce
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# SSL証明書の追加{#adding-an-ssl-certificate}

>[!NOTE]
>AEMは、OV（組織の検証）またはEV（拡張検証）の証明書のみをCloud Serviceとして受け入れます。 DV（ドメイン検証）証明書は受け入れられません。 また、証明書は、信頼できる証明機関(CA)のX.509 TLS証明書で、一致する2048ビットRSA秘密鍵が含まれている必要があります。

証明書のプロビジョニングには数日かかり、数か月前から証明書をプロビジョニングすることをお勧めします。 詳しくは、[SSL証明書の取得](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)を参照してください。

## 証明書の形式{#certificate-format}

SSLファイルをCloud Managerにインストールするには、PEM形式にする必要があります。 PEM形式の一般的なファイル拡張子は`.pem,`です。`crt`, `.cer`, および `.cert`.

次の手順に従って、SSLファイルの形式をPEMに変換します。

* PFXをPEMに変換

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* P7BをPEMに変換

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* DERをPEMに変換

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 重要な検討事項 {#important-considerations}

* SSL証明書をCloud Managerにインストールするには、ユーザーがビジネス所有者またはDeployment Managerの役割を持っている必要があります。

* Cloud Managerでは、証明書の有効期限が切れている場合でも、プログラム内の1つ以上の環境に関連付けることができるSSL証明書は、常に最大10個まで許可されます。 ただし、Cloud Manager UIでは、50個までのSSL証明書をプログラムにインストールできます。

## 証明書の追加{#adding-a-cert}

証明書を追加するには、次の手順に従います。

1. Cloud Managerにログインします。
1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。
1. 画面左側のナビゲーションメニューで「**SSL Certificates**」をクリックします。 既存のSSL証明書の詳細を示す表がこの画面に表示されます。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. **追加SSL証明書**&#x200B;をクリックして、**追加SSL証明書**&#x200B;ダイアログボックスを開きます。

   * 「**証明書名**」に証明書の名前を入力します。 証明書を簡単に参照できる任意の名前を指定できます。
   * **証明書**、**秘密鍵**、**証明書チェーン**をそれぞれのフィールドに貼り付けます。 入力ボックスの右側にある貼り付けアイコンを使用します。
3つのフィールドはすべてオプションではなく、含める必要があります。

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >検出されたエラーが表示されます。 証明書を保存する前に、すべてのエラーを解決する必要があります。 一般的なエラーの対処方法の詳細については、[証明書のエラー](#certificate-errors)を参照してください。

1. 「**保存**」をクリックして、証明書を送信します。 テーブルに新しい行として表示されます。

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## 証明書エラー{#certificate-errors}

### 正しい証明書の順序{#correct-certificate-order}

証明書のデプロイメントが失敗する最も一般的な理由は、中間証明書またはチェーン証明書の順序が正しくないことです。 特に、中間証明書ファイルは、ルート証明書またはルートに最も近い証明書で終わり、`main/server`証明書からルートに降順である必要があります。

次のコマンドを使用して、中間ファイルの順序を決定できます。

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

次のコマンドを使用して、秘密鍵と`main/server`証明書が一致することを確認できます。

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>これらの2つのコマンドの出力は、完全に同じである必要があります。 `main/server`証明書と一致する秘密鍵が見つからない場合は、新しいCSRを生成し、SSLベンダーから更新された証明書を要求して、証明書のキーを再設定する必要があります。

### 証明書の有効期限{#certificate-validity-dates}

Cloud Managerでは、SSL証明書が今後90日以上有効になる予定です。 証明書チェーンの有効性を確認する必要があります。
