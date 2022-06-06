---
title: SSL 証明書の追加
description: Cloud Manager のセルフサービスツールを使用して独自の SSL 証明書を追加する方法を説明します。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 2c87d5fb33b83ca77b97391e4b0baaf38f8dd026
workflow-type: ht
source-wordcount: '592'
ht-degree: 100%

---

# SSL 証明書の追加 {#adding-an-ssl-certificate}

Cloud Manager のセルフサービスツールを使用して独自の SSL 証明書を追加する方法を説明します。

>[!TIP]
>
>証明書のプロビジョニングには数日かかる場合があります。アドビでは、証明書を事前に適切にプロビジョニングすることをお勧めします。

## 証明書の形式 {#certificate-format}

SSL 証明書ファイルを Cloud Manager にインストールするには、SSL ファイルを PEM 形式にする必要があります。PEM 形式の一般的なファイル拡張子は次のとおりです `.pem,` .`crt`、`.cer`、`.cert` です。

次の `openssl` コマンドを使用して、PEM 以外の証明書を変換できます。

* PFX を PEM に変換

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* P7B を PEM に変換

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* DER を PEM に変換

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## 証明書の追加 {#adding-a-cert}

Cloud Manager を使用して証明書を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 画面左側のナビゲーションパネルで「**SSL 証明書**」をクリックします。既存の SSL 証明書の詳細を示す表がメイン画面に表示されます。

   ![SSL 証明書の追加](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. 「**SSL 証明書を追加**」をクリックすると、**SSL 証明書を追加**&#x200B;ダイアログボックスが開きます。

   * 「**証明書名**」に証明書の名前を入力します。
      * これは情報提供だけを目的とし、証明書を簡単に参照するのに役立つ任意の名前を指定できます。
   * **証明書**、**秘密鍵**、**証明書チェーン**&#x200B;の値をそれぞれのフィールドに貼り付けます。
      * 入力ボックスの右側にある貼り付けアイコンを使用できます。
      * 3 つのフィールドはすべて必須です。

   ![SSL 証明書を追加ダイアログ](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * 検出されたエラーが表示されます。
      * 証明書を保存する前に、すべてのエラーを解決する必要があります。
      * 一般的なエラーの対処方法の詳細については、[証明書エラー](#certificate-errors)の節を参照してください。


1. 「**保存**」をクリックして証明書を保存します。

保存すると、証明書が表の新しい行として表示されます。

![保存された SSL 証明書](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>Cloud Manager で SSL 証明書をインストールするには、ユーザーが&#x200B;**ビジネスオーナー**&#x200B;のメンバーまたは&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持っている必要があります。

## 証明書エラー {#certificate-errors}

証明書が正しくインストールされていないか、Cloud Manager の要件を満たしていない場合は、特定のエラーが発生する場合があります。

### 証明書ポリシー {#certificate-policy}

次のエラーが発生した場合は、証明書のポリシーを確認してください。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

通常、証明書ポリシーは埋め込み OID 値で識別されます。テキストに証明書を出力し、OID を検索すると、証明書のポリシーが表示されます。

次の例を参考にして、証明書の詳細をテキストとして出力できます。

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

テキスト内の OID パターンは、証明書のポリシータイプを定義します。

| パターン | ポリシー | Cloud Manager で受け入れ可能 |
|---|---|---|
| `2.23.140.1.1` | EV | はい |
| `2.23.140.1.2.2` | OV | はい |
| `2.23.140.1.2.1` | DV | いいえ |

証明書の出力テキストの OID パターンに対して `grep` を実行すると、証明書ポリシーを確認できます。

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### 正しい証明書の順序 {#correct-certificate-order}

証明書のデプロイに失敗する原因として最もよくあるのは、中間証明書またはチェーン証明書の順序が正しくないことです。

中間証明書ファイルの末尾は、ルート証明書またはルートに最も近い証明書である必要があります。これらは、`main/server` 証明書からルートへ降順である必要があります。

中間ファイルの順序は、次のコマンドを使用して決定できます。

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

秘密鍵と `main/server` 証明書が一致することは、次のコマンドを使用して確認できます。

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>これらの 2 つのコマンドの出力は、完全に同じである必要があります。`main/server` 証明書と一致する秘密鍵が見つからない場合は、新しい CSR を生成するか、更新された証明書を SSL ベンダーに要求して、証明書を再入力する必要があります。

### 証明書の有効期限 {#certificate-validity-dates}

Cloud Manager で想定している SSL 証明書の有効期間は現在の日付から少なくとも 90 日間です。証明書チェーンの有効期限を確認します。
