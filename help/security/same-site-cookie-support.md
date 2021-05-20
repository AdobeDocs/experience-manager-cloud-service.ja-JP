---
title: Adobe Experience Manager as aCloud Serviceと同じサイトcookieのサポート
description: Adobe Experience Manager as aCloud Serviceと同じサイトcookieのサポート
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Adobe Experience Manager as aCloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}と同じサイトcookieのサポート

バージョン80、Chromeおよびそれ以降のSafariでは、cookieセキュリティの新しいモデルが導入されました。 このモードは、`SameSite`と呼ばれる設定を通じて、サードパーティサイトに対するcookieの可用性に関するセキュリティ制御を導入するように設計されています。 詳しくは、この[記事](https://web.dev/samesite-cookies-explained/)を参照してください。

この設定のデフォルト値(`SameSite=Lax`)を使用すると、AEMインスタンスまたはサービス間での認証が機能しない場合があります。 これは、これらのサービスのドメインやURL構造が、このcookieポリシーの制約に該当しない可能性があるためです。

この問題を回避するには、ログイントークンのSameSite cookie属性を`None`に設定する必要があります。

これをおこなうには、次の手順に従います。

1. AEM SDK Quickstartのバージョンのローカルインストール
1. Webコンソール(`http://serveraddress:serverport/system/console/configMgr`)に移動します。
1. **AdobeGranite Token Authentication Handler**&#x200B;を探してクリックします。
1. 次の図に示すように、login-token cookie **の** SameSite属性を`None`に設定します
   ![サムサイト](/help/security/assets/samesite1.png)
1. 「保存」をクリックします。
1. [AEM SDK Quickstartを使用したOSGi設定の生成](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)で説明されている手順に従って、この特定の設定のJSON形式設定を生成します。
1. 「[Cloud Manager API形式でのプロパティの設定](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi」のドキュメントに記載されている手順に従って、設定を適用します。

この設定が更新され、ユーザーがログアウトして再度ログインすると、`login-token` Cookieの属性は`None`に設定され、クロスサイトリクエストに含められます。
