---
title: AEM as a Cloud Service のセキュリティに関する考慮事項
description: AEM as a Cloud Service を使用する際のセキュリティに関する重要な考慮事項について説明します。
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 100%

---

# AEM as a Cloud Service のセキュリティに関する考慮事項 {#security-considerations}

## AEM トラストストア {#aem-trust-store}

非対称の暗号化操作をサポートするために、AEM は証明書をコンテンツリポジトリ内のグローバルトラストストアに保存します。そのコンテンツは公開され、デフォルトでは、パブリッシャーインスタンス上の全員が匿名でアクセスできます。

### トラストストアの特性 {#truststore-characteristics}

* トラストストアは、`/etc/truststore` の下にあり、Java™ キーストアファイル、キーストアパスワード、リポジトリメタデータで構成されます。含まれる証明書にはデフォルトで API を通じてすべてのユーザーがアクセスできる場合でも、技術的な理由によりパスワードとキーストアは両方とも暗号化されます
* 標準では、証明書は HTTPS および SAML のサポートにのみ使用され、最初にストアを手動で作成する必要があります
* お客様は、[キーストア API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-) を通じて独自のコードでこれを使用できます。
* トラストストアは、UI（**ツール** - **セキュリティ** - **トラストストア**）を通じて管理するか、以下に示すように *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`* にアクセスして管理できます。

  ![トラストストアの管理](/help/security/assets/global-trust-store-modified.png)

* トラストストアへのアクセスは、使用事例に応じて、リポジトリのアクセス制御によってさらに制限されます。

>[!NOTE]
>
>アドビでは、Trust Store に対してデフォルトのアクセス制御を使用する（引き続きパブリックアクセス可能にする）ことをお勧めします。最も安全な設定を実現するには、全員に対して deny `jcr:all` のポリシーを使用できます。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=ja#anonymous-permission-hardening-package).
-->
