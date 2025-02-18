---
title: SSL 証明書の概要
description: SSL 証明書のインストールおよび管理において Cloud Manager が提供するセルフサービスツールについて説明します。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a91b15836d0ca0308fbc860ec57aacda908f610d
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---


# SSL 証明書の概要{#introduction}

SSL（Secure Socket Layer）証明書のインストールおよび管理において Cloud Manager が提供するセルフサービスツールについて説明します。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="SSL 証明書の管理"
>abstract="Cloud Manager のセルフサービスツールで、SSL 証明書をインストールおよび管理し、ユーザーのためにサイトを保護する方法について説明します。Cloud Manager は、プラットフォーム TLS サービスを使用して、SSL 証明書と秘密鍵（顧客が所有し、サードパーティの証明機関から取得される鍵）を管理します。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書の表示、更新、および置換"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書のステータスの確認"

## SSL 証明書とは？ {#overview}

企業や組織は SSL（Secure Socket Layer）証明書を使用して自社の web サイトを保護し、顧客の信頼を確保します。SSL プロトコルを使用するには、web サーバーに SSL 証明書が必要です。

組織や企業などのエンティティが認証機関（CA）に証明書を要求すると、CA は検証プロセスを完了します。このプロセスは、ドメイン名制御の検証から、会社登録書やサブスクライバー契約書の収集まで多岐にわたります。エンティティの情報が検証されると、CA は CA の秘密鍵を使用して公開鍵に署名します。主要な認証機関はすべて web ブラウザーのルート証明書を持っているので、エンティティ証明書は&#x200B;*信頼チェーン*&#x200B;を介してリンクされ、web ブラウザーはそれを信頼済み証明書と認識します。

>[!IMPORTANT]
>
>Cloud Manager からは、SSL 証明書や秘密鍵は提供されません。これらの情報は、証明機関（信頼できるサードパーティの組織）から取得する必要があります。よく知られている証明機関には、*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*、*Verisign* などがあります。

## Cloud Manager を使用した証明書の管理 {#cloud-manager}

Cloud Manager には、SSL 証明書をインストールおよび管理するセルフサービスツールが用意されており、ユーザーのサイトセキュリティを確保します。Cloud Manager では、証明書を管理する 2 つのモデルをサポートしています。

| | モデル | 説明 |
| --- | --- | --- |
| A | **[アドビが管理する SSL 証明書（DV）](#adobe-managed)** | Cloud Manager を使用すると、ユーザーはアドビが提供する DV（ドメイン検証）証明書を設定して、ドメインをすばやく設定できます。 |
| B | **[顧客が管理する SSL 証明書（OV/EV）](#customer-managed)** | Cloud Manager は、プラットフォーム TLS（Transport Layer Security）サービスを提供し、所有する OV および EV SSL 証明書と、サードパーティの証明機関からの秘密鍵（*Let&#39;s Encrypt* など）を管理できます。 |

どちらのモデルも、証明書を管理する次の一般的な機能を提供します。

* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。

>[!IMPORTANT]
>
>[カスタムドメインを追加して環境に関連付けるには](/help/implementing/cloud-manager/custom-domain-names/introduction.md)、そのドメインを対象とする有効な SSL 証明書が必要です。

### アドビが管理する（DV）SSL 証明書 {#adobe-managed}

DV 証明書は、最も基本的なレベルの SSL 証明書で、多くの場合、テスト目的や、基本的な暗号化で web サイトを保護する目的で使用されます。DV 証明書は[実稼動プログラムとサンドボックスプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)の両方で利用できます。

DV 証明書を作成すると、その証明書を削除しない限り、アドビが 3 か月ごとに自動的に更新します。

### 顧客が管理する（OV/EV）SSL 証明書 {#customer-managed}

OV 証明書と EV 証明書は、CA で検証された情報を提供します。このような情報は、web サイト所有者、メール送信者、コードや PDF ドキュメントのデジタル署名者が信頼できるかどうかを評価するのに役立ちます。DV 証明書では、このような所有権の検証は許可されません。

また、OV と EV は、Cloud Manager の DV 証明書を通じてこれらの機能も提供します。

* 複数の環境で OV/EV 証明書を使用できます。つまり、1 度の追加で複数回使用できます。
* 通常、各 OV／EV 証明書には複数のドメインが含まれます。
* Cloud Manager は、ドメインのワイルドカード OV／EV 証明書を受け付けます。

>[!TIP]
>
>複数のカスタムドメインがある場合は、新しいドメインを追加するたびに証明書をアップロードする必要がないことがあります。その場合、複数のドメインを対象とする単一の証明書を取得するとメリットが得られます。

#### 顧客が管理する OV/EV SSL 証明書の要件 {#requirements}

顧客が管理する独自の SSL 証明書を追加する場合は、次の更新された要件を満たす必要があります。

* ドメイン検証（DV）証明書および自己署名証明書はサポートされていません。
* 証明書は、OV（組織検証）ポリシーまたは EV（拡張検証）ポリシーに準拠する必要があります。
* 証明書は、信頼された認証機関（CA）から発行されている X.509 TLS 証明書にする必要があります。
* サポートされている暗号化キーのタイプは次のとおりです。

   * RSA 2048 ビット、標準サポート。
現時点では、2048 ビットを超える RSA キー（3072 ビットまたは 4096 ビットの RSA キーなど）はサポートされていません。
   * 楕円曲線（EC）キー `prime256v1`（`secp256r1`）および `secp384r1`
   * 楕円曲線デジタル署名アルゴリズム（ECDSA）証明書。このような証明書は、パフォーマンス、セキュリティ、効率を向上させるために、RSA よりもアドビによって推奨されています。

* 検証に合格するには、証明書を正しく書式設定する必要があります。秘密鍵は、`PKCS#8` 形式にする必要があります。

>[!NOTE]
>組織が 3072 ビット RSA キーを使用したコンプライアンスを必要とする場合、アドビが推奨する代替方法は、ECDSA 証明書（`secp256r1` または `secp384r1`）を使用することです。


#### 証明書管理のベストプラクティス

* **重複する証明書の回避：**

   * 証明書の管理をスムーズに行うには、同じドメインに一致する重複する証明書のデプロイを回避します。例えば、ワイルドカード証明書（*.example.com）と特定の証明書（dev.example.com）を一緒に使用すると、混乱が生じる場合があります。
   * TLS レイヤーは、最も具体的で最近デプロイされた証明書を優先します。

  シナリオの例：

   * 「開発証明書」には `dev.example.com` が含まれ、`dev.example.com` のドメインマッピングとしてデプロイされます。
   * 「ステージ証明書」には `stage.example.com` が含まれ、`stage.example.com` のドメインマッピングとしてデプロイされます。
   * 「ステージ証明書」を「開発証明書」の&#x200B;*後*&#x200B;にデプロイ／更新した場合、`dev.example.com` のリクエストも処理されます。

     証明書の範囲が意図したドメインに慎重に設定されていることを確認します。

* **ワイルドカード証明書：**

  ワイルドカード証明書（例：`*.example.com`）はサポートされていますが、必要な場合にのみ使用する必要があります。重複が発生した場合は、より具体的な証明書が優先されます。例えば、特定の証明書は、ワイルドカード（`*.example.com`）の代わりに `dev.example.com` を提供します。

* **検証とトラブルシューティング：**
Cloud Manager を使用して証明書をインストールする前に、アドビでは `openssl` などのツールを使用して証明書の整合性をローカルで検証することをお勧めします。例：

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

#### 顧客が管理する証明書の形式 {#certificate-format}

SSL 証明書ファイルを Cloud Manager でインストールするには、SSL ファイルを PEM 形式にする必要があります。PEM 形式の一般的なファイル拡張子には `.pem,` があります。`crt`、`.cer`、`.cert` です。

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

## インストールする SSL 証明書の数の制限 {#limitations}

Cloud Manager では、常に最大 50 個のインストールされた証明書をサポートします。これらの証明書は、プログラム全体の 1 つ以上の環境に関連付けることができ、期限切れの証明書も含むことができます。

上限に達した場合は、証明書を確認し、期限切れの証明書の削除を検討します。または、1 つの証明書で複数のドメイン（最大 100 個の SAN）をカバーする可能性があるので、複数のドメインを同じ証明書にグループ化します。

## 詳細情報 {#learn-more}

必要な権限を持つユーザーは、Cloud Manager を使用してプログラムの SSL 証明書を管理できます。これらの機能の使用方法について詳しくは、次のドキュメントを参照してください。

* [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

