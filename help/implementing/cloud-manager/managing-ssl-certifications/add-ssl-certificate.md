---
title: SSL証明書の追加 — SSL証明書の管理
description: SSL証明書の追加 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# SSL証明書の追加 {#adding-an-ssl-certificate}

>[!NOTE]
>証明書のプロビジョニングには数日かかり、数か月前から証明書をプロビジョニングすることをお勧めします。 SSL証明書の取得方法に移動して詳細を確認してください。INSERT LINK

## 証明書の形式 {#certificate-format}

SSLファイルをCloud Managerにインストールするには、PEM形式にする必要があります。 PEM形式内の一般的なファイル拡張子は、.pem、.crt、.cer、.certです。

次の手順に従って、SSLファイルの形式をPEMに変換します。

1. PFXをPEMに変換

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. P7BをPEMに変換

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. DERをPEMに変換

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 証明書の追加 {#adding-certificate}

>[!NOTE]
>* SSL証明書をCloud Managerにインストールするには、ユーザーがビジネス所有者またはDeployment Managerの役割を持っている必要があります。
>* Cloud Managerでは、証明書の有効期限が切れている場合でも、プログラム内の1つ以上の環境に関連付けることができるSSL証明書を、いつでも5つまで許可します。 ただし、Cloud Manager UIでは、50個までのSSL証明書をプログラムにインストールできます。


1. Cloud Managerにログインします。
1. 概要ページから環境画面に移動します。
1. 左側のナビゲーションメニューから「SSL証明書」画面に移動します。 既存のSSL証明書の詳細を示す表がこの画面に表示されます。INSERT IMAGE
1. ウィザードを起動するには、 **証明書** ボタンを選択します。
1. 証明書の名前を入力します。 証明書を簡単に参照できる任意の名前を指定できます。
1. 証明書、秘密鍵、およびチェーンの内容をそれぞれのフィールドに貼り付けます。 入力ボックスの右側にある貼り付けアイコンを使用します。
1. 「**保存**」を選択します。

   >[!NOTE]
   >検出されたエラーが表示されます。 証明書を保存する前に、すべてのエラーを解決する必要があります。 一般的なエラーの対処方法の詳細については、「証明書のINSERT LINKエラー」を参照してください。

   証明書を送信すると、表内の新しい行として表示されます。

## 証明書エラー {#certificate-errors}

### 証明書の正しい順序 {#correct-certificate-order}

証明書のデプロイメントが失敗する最も一般的な理由は、中間証明書またはチェーン証明書の順序が正しくないことです。 特に、中間証明書ファイルは、ルート証明書またはルートに最も近い証明書で終わり、証明書からルートに降順である必要があり `main/server` ます。

次のコマンドを使用して、中間ファイルの順序を決定できます。

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

次のコマンドを使用して、秘密鍵と `main/server` 証明書が一致することを確認できます。

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>これらの2つのコマンドの出力は、完全に同じである必要があります。 証明書に一致する秘密鍵が見つからない場合は、新しいCSRを生成し、SSLベンダーから更新された証明書を要求して、証明書を再キーする必要があります。 `main/server`

### 証明書の有効期限 {#certificate-validity-dates}

Cloud Managerでは、SSL証明書が今後90日以上有効になる予定です

証明書チェーンの有効性を確認します。
