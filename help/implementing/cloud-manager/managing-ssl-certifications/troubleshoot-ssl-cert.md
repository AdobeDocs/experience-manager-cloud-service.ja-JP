---
title: SSL 証明書エラーのトラブルシューティング
description: 一般的な原因を特定して SSL 証明書エラーのトラブルシューティングを行い、安全な接続を維持する方法を説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9ffec422ec4b5a45962f07142c49a466e8892754
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 83%

---


# SSL 証明書エラーのトラブルシューティング {#certificate-errors}

証明書が正しくインストールされていないか、Cloud Managerの要件を満たしていない場合は、特定のエラーが発生する場合があります。

+++**正しい証明書の順序**

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

+++

+++**クライアント証明書の削除**

証明書を追加する際に、次のようなエラーが表示される場合があります。

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

クライアント証明書が証明書チェーンに含まれた可能性があります。チェーンにクライアント証明書が含まれていないことを確認し、もう一度試してください。

+++

+++**証明書ポリシー**

次のエラーが発生した場合は、証明書のポリシーを確認してください。

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

埋め込まれている OID 値は通常、証明書ポリシーを識別します。テキストに証明書を出力し、OID を検索すると、証明書のポリシーが表示されます。

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

+++

+++**証明書の有効期限**

Cloud Manager で想定している SSL 証明書の有効期間は現在の日付から少なくとも 90 日間です。証明書チェーンの有効期限を確認します。

+++