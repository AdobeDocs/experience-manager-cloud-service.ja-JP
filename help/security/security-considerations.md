---
title: AEMのas a Cloud Service的セキュリティに関する考慮事項
description: AEM as a Cloud Serviceを使用する際のセキュリティに関する重要な考慮事項について説明します
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# AEMのas a Cloud Service的セキュリティに関する考慮事項 {#security-considerations}

## AEM Trust Store {#aem-trust-store}

非対称の暗号化操作をサポートするために、AEMは証明書をコンテンツリポジトリ内のグローバルトラストストアに保存します。 コンテンツは公開され、デフォルトでは、パブリッシャーインスタンス上の全員が匿名でアクセスできます。

### トラストストアの特性 {#truststore-characteristics}

* トラストストアは、以下にあります。 `/etc/truststore` は、Java キーストアファイル、キーストアのパスワード、リポジトリのメタデータで構成されます。 含まれる証明書はデフォルトで API を通じてすべてのユーザーがアクセスできる場合でも、パスワードとキーストア自体は技術的な理由により暗号化されます
* 標準では、証明書は HTTPS および SAML のサポートにのみ使用され、最初にストアを手動で作成する必要があります
* お客様は、 [keystore API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* トラストストアは、UI( **ツール** - **セキュリティ** - **トラストストア** または、 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*、以下に示すように。

  ![Trust Store の管理](/help/security/assets/global-trust-store-modified.png)

* trust-store へのアクセスは、使用事例に応じて、リポジトリのアクセス制御によってさらに制限されます。

>[!NOTE]
>
>Adobeでは、Trust Store にデフォルトのアクセス制御を使用することをお勧めします。つまり、公開されたままアクセスできます。 最も安全な設定の場合は、全員に対して deny jcr:all のポリシーを使用できます。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
