---
title: SSL証明書の追加 — SSL証明書の管理
description: SSL証明書の追加 — SSL証明書の管理
translation-type: tm+mt
source-git-commit: b6911f0b8674550713bd4ec1e34be5d0a14cc427
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# SSL証明書の追加{#adding-an-ssl-certificate}

>[!NOTE]
>AEMは、OV（組織の検証）またはEV（拡張検証）の証明書のみをCloud Serviceとして受け入れます。 DV（ドメイン検証）証明書は受け入れられません。

証明書のプロビジョニングには数日かかり、数か月前から証明書をプロビジョニングすることをお勧めします。 詳しくは、「SSL証明書の取得」を参照してください。

## 証明書の形式{#certificate-format}

SSLファイルをCloud Managerにインストールするには、PEM形式にする必要があります。 PEM形式の一般的なファイル拡張子は`.pem,`です。`crt`, `.cer`, および `.cert`.

次の手順に従って、SSLファイルの形式をPEMに変換します。

1. PFXをPEMに変換

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. P7BをPEMに変換

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. DERをPEMに変換

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## 証明書の追加{#adding-certificate}

>[!NOTE]
>* SSL証明書をCloud Managerにインストールするには、ユーザーがビジネス所有者またはDeployment Managerの役割を持っている必要があります。
>* Cloud Managerでは、証明書の有効期限が切れている場合でも、プログラム内の1つ以上の環境に関連付けることができるSSL証明書は、常に最大10個まで許可されます。 ただし、Cloud Manager UIでは、50個までのSSL証明書をプログラムにインストールできます。


証明書を追加するには、次の手順に従います。

1. Cloud Managerにログインします。
1. 概要ページから環境画面に移動します。
1. 左側のナビゲーションメニューから「SSL証明書」画面に移動します。 既存のSSL証明書の詳細を示す表がこの画面に表示されます。
1. **追加証明書**&#x200B;ボタンを選択して、ウィザードを起動します。
   1. 証明書の名前を指定します。 証明書を簡単に参照できる任意の名前を指定できます。
   1. 証明書、秘密鍵、およびチェーンの内容をそれぞれのフィールドに貼り付けます。 入力ボックスの右側にある貼り付けアイコンを使用します。

      >[!NOTE]
      >3つのフィールドはすべてオプションではなく、含める必要があります。
1. 証明書を送信すると、表内の新しい行として表示されます。


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

Cloud Managerでは、SSL証明書が今後90日以上有効になる予定です

証明書チェーンの有効性を確認します。
