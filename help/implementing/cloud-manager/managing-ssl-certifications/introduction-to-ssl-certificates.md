---
title: SSL 証明書の概要
description: SSL 証明書をインストールおよび管理するためにCloud Managerが提供するセルフサービスツールについて説明します。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 075094f018ccf213cd8d1d69defdc390f0a90713
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 56%

---


# SSL 証明書の概要{#introduction}

SSL （Secure Socket Layer）証明書をインストールおよび管理するためにCloud Managerが提供するセルフサービスツールについて説明します。

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="SSL 証明書の管理"
>abstract="Cloud Manager で、サイトを保護するために、SSL 証明書をセルフサービスでインストールおよび管理する方法について説明します。Cloud Manager は、プラットフォーム TLS サービスを使用して、SSL 証明書と、サードパーティの証明機関から取得され、顧客が所有する秘密鍵を管理します。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書の表示、更新、および置換"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="SSL 証明書のステータスの確認"

## SSL 証明書とは {#overview}

企業や組織では、SSL （Secure Socket Layer）証明書を使用して web サイトを保護し、顧客の信頼を確保しています。 SSL プロトコルを使用するには、web サーバーに SSL 証明書が必要です。

組織や企業などのエンティティが認証機関（CA）に証明書を要求すると、CA は検証プロセスを完了します。このプロセスは、ドメイン名制御の検証から、会社登録書やサブスクライバー契約書の収集まで多岐にわたります。エンティティの情報が検証されると、CA は CA の秘密鍵を使用して公開鍵に署名します。主要な認証機関はすべて web ブラウザーのルート証明書を持っているので、エンティティ証明書は&#x200B;*信頼チェーン*&#x200B;を介してリンクされ、web ブラウザーはそれを信頼済み証明書と認識します。

>[!IMPORTANT]
>
>Cloud Manager からは、SSL 証明書や秘密鍵は提供されません。これらの部分は、信頼できるサードパーティの組織である証明機関から取得する必要があります。 よく知られている証明機関には、*DigiCert*、*Let&#39;s Encrypt*、*GlobalSign*、*Entrust*、*Verisign* などがあります。

## Cloud Managerでの証明書の管理 {#cloud-manager}

Cloud Managerには、SSL 証明書をインストールおよび管理するセルフサービスツールが用意されており、ユーザーのサイトセキュリティを確保できます。 Cloud Managerでは、証明書を管理する 2 つのモデルをサポートしています。

| | モデル | 説明 |
| --- | --- | --- |
| A | **[アドビが管理する証明書（DV）](#adobe-managed)** | Cloud Managerを使用すると、ドメインのクイックセットアップ用にAdobeから提供される DV （Domain Validation）証明書を設定できます。 |
| B | **[顧客が管理する証明書（OV／EV）](#customer-managed)** | Cloud Managerは、所有する OV および EV SSL 証明書と、サードパーティの認証機関からの秘密鍵（*Let’s Encrypt* を管理できる、プラットフォーム TLS （Transport Layer Security）サービスを提供しています。 |

どちらのモデルも、証明書を管理するための次の一般的な機能を提供します。

* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。

>[!IMPORTANT]
>
>[ カスタムドメインを追加して環境に関連付けるには ](/help/implementing/cloud-manager/custom-domain-names/introduction.md)、ドメインをカバーする有効な SSL 証明書が必要です。

### Adobe管理証明書 {#adobe-managed}

DV 証明書は、最も基本的なレベルの SSL 証明書で、多くの場合、テスト目的や、基本的な暗号化で web サイトを保護する目的で使用されます。DV 証明書は、[ 実稼動プログラムとサンドボックスプログラム ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) の両方で使用できます。

DV 証明書を作成すると、その証明書を削除しない限り、アドビが 3 か月ごとに自動的に更新します。

### 顧客管理の証明書 {#customer-managed}

OV 証明書と EV 証明書は、CA で検証された情報を提供します。このような情報は、web サイト所有者、メール送信者、コードや PDF ドキュメントのデジタル署名者が信頼できるかどうかを評価するのに役立ちます。DV 証明書では、このような所有権の検証は許可されません。

OV および EV は、Cloud Managerの DV 証明書に対してさらに、これらの機能を提供します。

* 複数の環境が 1 つの OV/EV 証明書を使用できます。
   * つまり、1 度の追加で複数回使用できます。
* 通常、各 OV/EV 証明書には複数のドメインが含まれます。
* Cloud Managerは、ドメインのワイルドカード OV/EV 証明書を受け付けます。

>[!TIP]
>
>複数のカスタムドメインがある場合、新しいドメインを追加するたびに証明書をアップロードしたくないことがあります。 その場合、複数のドメインに対応する単一の証明書を取得することで、メリットが得られる可能性があります。

>[!NOTE]
>
>インストールされている証明書が同じドメインに対応している場合は、より正確な証明書が適用されます。
>
>例えば、ドメインが `dev.adobe.com` で、`*.adobe.com` 用の証明書と `dev.adobe.com` 用の証明書が 1 つある場合、より具体的な証明書（`dev.adobe.com`）が使用されます。

#### 顧客管理証明書の要件 {#requirements}

独自の EV/OV 証明書をアップロードする場合は、次の要件を満たす必要があります。

* AEM as a Cloud Serviceでは、OV （Organization Validation）ポリシーまたは EV （Extended Validation）ポリシーに準拠する証明書を受け付けます。
   * Cloud Managerは独自の DV （Domain Validation）証明書のアップロードをサポートしていません。
* 証明書はすべて、2048 ビットの RSA 秘密鍵と一致する信頼できる証明機関の X.509 TLS 証明書である必要があります。
* 自己署名証明書は受け付けられません。

#### 顧客管理証明書の形式 {#certificate-format}

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

