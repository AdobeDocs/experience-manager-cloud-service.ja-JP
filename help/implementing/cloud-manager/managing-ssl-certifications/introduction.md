---
title: SSL 証明書の管理の概要
description: Cloud Manager が、SSL 証明書をインストールするセルフサービスツールを提供する方法について説明します。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 100%

---


# SSL 証明書の管理の概要{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="SSL 証明書の管理"
>abstract="Cloud Manager で、サイトを保護するために、SSL 証明書をセルフサービスでインストールおよび管理する方法について説明します。Cloud Manager は、プラットフォーム TLS サービスを使用して、SSL 証明書と、サードパーティの証明機関から取得され、顧客が所有する秘密鍵を管理します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=ja" text="SSL 証明書の表示、更新、置換"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=ja" text="SSL 証明書のステータスの確認"

Cloud Manager は、SSL 証明書をインストールおよび管理するセルフサービスツールを用意しているので、ユーザーのためにサイトを保護できます。Cloud Manager は、プラットフォーム TLS サービスを使用して、顧客が所有し、Let&#39;s Encrypt などのサードパーティ証明機関から取得した SSL 証明書と秘密鍵を管理します。

## 証明書の概要 {#certificates}

企業は SSL 証明書を使用して自社の web サイトを保護し、顧客の信頼を確保します。SSL プロトコルを使用するには、web サーバーで SSL 証明書を使用する必要があります。

事業体が CA に証明書を要求すると、CA は検証プロセスを完了します。これは、ドメイン名制御の検証から、会社登録書や加入者契約書の収集まで多岐にわたります。事業体の情報が検証されると、CA は CA の秘密鍵を使用して公開鍵に署名します。主要な認証機関はすべて web ブラウザーのルート証明書を持っているので、エンティティ証明書は&#x200B;*信頼のチェーン*&#x200B;を介してリンクされ、web ブラウザーはそれを信頼済み証明書と認識します。

>[!IMPORTANT]
>
>Cloud Manager からは、SSL 証明書や秘密鍵は提供されません。これらは、証明機関（CA）から取得する必要があります。

## Cloud Manager SSL 管理機能 {#features}

Cloud Manager では、次の顧客向け SSL 証明書の使用オプションをサポートしています。

* 1 つの SSL 証明書は複数の環境で使用できます。つまり、1 度の追加で複数回使用できます。
* 各 Cloud Manager 環境は、複数の証明書を使用できます。
* 秘密鍵は、複数の SSL 証明書を発行する場合があります。
* 通常、各証明書には複数のドメインが含まれます。
* プラットフォーム TLS サービスは、終了に使用された SSL 証明書と、そのドメインをホストする CDN サービスに基づいて、リクエストを顧客の CDN サービスにルーティングします。
* AEM as a Cloud Service は、ドメインのワイルドカード SSL 証明書を受け入れます。

## レコメンデーション {#recommendations}

AEM as a Cloud Service は、セキュリティで保護された `https` サイトのみをサポートしています。

* 複数のカスタムドメインを持つ顧客の場合、ドメインを追加するたびに証明書をアップロードしたくはありません。
* 複数のドメインを持つ 1 つの証明書を取得することで、そのような顧客はメリットが得られます。

## 要件 {#requirements}

* AEM as a Cloud Service では、OV（組織検証）ポリシーまたは EV（拡張検証）ポリシーに準拠する証明書のみを受け付けます。
* 証明書はすべて、2048 ビットの RSA 秘密鍵と一致する信頼できる証明機関（CA）の X.509 TLS 証明書である必要があります。
* DV（ドメイン検証）ポリシーは受け付けられません。
* 自己署名証明書は受け付けられません。

OV 証明書と EV 証明書は、CA で検証された追加の情報をユーザーに提供します。ユーザーは、この情報を使用して、web サイトの所有者、メールの送信者、実行可能なコードや PDF ドキュメントのデジタル署名者の信頼性を判断できます。DV 証明書では、このような所有権の検証は許可されません。

## 制限事項 {#limitations}

Cloud Manager では、いつでも最大 50 個の SSL 証明書をインストールできます。これらは、プログラム全体の 1 つ以上の環境に関連付けることができ、期限切れの証明書も含むことができます。

上限に達した場合は、証明書を確認して、以下を検討します。

* 期限切れの証明書を削除します。
* 1 つの証明書が複数のドメイン（最大 100 個の SAN）をカバーする可能性があるので、同じ証明書内の複数のドメインをグループ化します。

## 詳細情報 {#learn-more}

必要な権限を持つユーザーは、Cloud Manager を使用してプログラムの SSL 証明書を管理できます。これらの機能の使用方法について詳しくは、次のドキュメントを参照してください。

* [SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [SSL 証明書の表示、更新、置換](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [SSL 証明書の削除](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
