---
title: SSL 証明書の概要
description: Cloud Manager が、SSL 証明書をインストールするセルフサービスツールを提供する方法について説明します。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: ht
source-wordcount: '765'
ht-degree: 100%

---


# SSL 証明書の概要{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="SSL 証明書の管理"
>abstract="Cloud Manager で、サイトを保護するために、SSL 証明書をセルフサービスでインストールおよび管理する方法について説明します。Cloud Manager は、プラットフォーム TLS サービスを使用して、SSL 証明書と、サードパーティの証明機関から取得され、顧客が所有する秘密鍵を管理します。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書の表示、更新、および置換"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書のステータスの確認"


Cloud Manager には、SSL（Secure Socket Layer）証明書をインストールおよび管理するセルフサービスツールが用意されており、ユーザーのサイトセキュリティを確保できます。次の 2 つのユースケースがサポートされています。

<!-- CQDOC-21758, #1 -->

| | ユースケース | 説明 |
| --- | --- | --- |
| 1 | **アドビが管理する証明書（DV）** | Cloud Manager を使用すると、アドビから取得した DV（ドメイン検証）証明書を使用して、ドメインをすばやくセットアップできます。DV 証明書は、最も基本的なレベルの SSL 証明書で、多くの場合、テスト目的や、基本的な暗号化で web サイトを保護する目的で使用されます。DV 証明書は[実稼動プログラムとサンドボックスプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)の両方で利用できます。DV 証明書を作成すると、その証明書を削除しない限り、アドビが 3 か月ごとに自動的に更新します。 |
| 2 | **顧客が管理する証明書（OV／EV）** | Cloud Manager は、プラットフォーム TLS（Transport Layer Security）サービスを使用して、顧客が所有する SSL 証明書と、サードパーティの証明機関からの秘密鍵（*Let’s Encrypt* など）を管理します。 |

>[!NOTE]
>
>顧客が DV（ドメイン検証）証明書をアップロードすることは許可されていません。


## SSL 証明書の概要 {#certificates}

企業や組織は SSL 証明書を使用して自社の web サイトを保護し、顧客の信頼を確保します。SSL プロトコルを使用するには、web サーバーで SSL 証明書を使用する必要があります。

組織や企業などのエンティティが認証機関（CA）に証明書を要求すると、CA は検証プロセスを完了します。このプロセスは、ドメイン名制御の検証から、会社登録書やサブスクライバー契約書の収集まで多岐にわたります。エンティティの情報が検証されると、CA は CA の秘密鍵を使用して公開鍵に署名します。主要な認証機関はすべて web ブラウザーのルート証明書を持っているので、エンティティ証明書は&#x200B;*信頼チェーン*&#x200B;を介してリンクされ、web ブラウザーはそれを信頼済み証明書と認識します。

>[!IMPORTANT]
>
>Cloud Manager からは、SSL 証明書や秘密鍵は提供されません。これらの情報は、証明機関（信頼できるサードパーティの組織）から取得する必要があります。よく知られている証明機関には、*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*、*Verisign* などがあります。

Cloud Manager では、次の顧客向け SSL 証明書の使用オプションをサポートしています。

* 複数の環境で SSL 証明書を使用できます。つまり、1 度の追加で複数回使用できます。
* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* 通常、各証明書には複数のドメインが含まれます。
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。
* AEM as a Cloud Service は、ドメインのワイルドカード SSL 証明書を受け入れます。

AEM as a Cloud Service は、セキュリティで保護された `https` サイトのみをサポートしています。複数のカスタムドメインを持つ顧客の場合、ドメインを追加するたびに証明書をアップロードする必要はありません。このような顧客は、複数のドメインに対応した 1 つの証明書を取得することでメリットが得られます。

## SSL 証明書の要件 {#requirements}

* AEM as a Cloud Service では、OV（組織検証）、EV（拡張検証）、DV（ドメイン検証）ポリシーに準拠する証明書を受け付けます。<!-- CQDOC-21758, #2 -->
* 証明書はすべて、2048 ビットの RSA 秘密鍵と一致する信頼できる証明機関の X.509 TLS 証明書である必要があります。
* 自己署名証明書は受け付けられません。

OV 証明書と EV 証明書は、CA で検証された情報を提供します。このような情報は、web サイト所有者、メール送信者、コードや PDF ドキュメントのデジタル署名者が信頼できるかどうかを評価するのに役立ちます。DV 証明書では、このような所有権の検証は許可されません。

### 顧客が管理する SSL 証明書形式 {#certificate-format}

<!-- CQDOC-21758, #3 -->

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

Cloud Manager では、常に最大 50 個の SSL 証明書をインストールできます。これらの証明書は、プログラム全体の 1 つ以上の環境に関連付けることができ、期限切れの証明書も含むことができます。

上限に達した場合は、証明書を確認し、期限切れの証明書の削除を検討します。または、1 つの証明書で複数のドメイン（最大 100 個の SAN）をカバーする可能性があるので、複数のドメインを同じ証明書にグループ化します。

## 詳細情報 {#learn-more}

必要な権限を持つユーザーは、Cloud Manager を使用してプログラムの SSL 証明書を管理できます。これらの機能の使用方法について詳しくは、次のドキュメントを参照してください。

* [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

