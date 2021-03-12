---
title: Cloud Serviceと同じサイトでのAdobe Experience Managerのcookieサポート
description: Cloud Serviceと同じサイトでのAdobe Experience Managerのcookieサポート
translation-type: tm+mt
source-git-commit: 4f25aa54bd40644912e0e430a81f1a17d545e3f8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Cloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}と同じサイトでのAdobe Experience Managerのcookieサポート

バージョン80以降、Chromeおよびそれ以降のSafariでは、cookieセキュリティの新しいモデルが導入されました。 このモードは、`SameSite`と呼ばれる設定を通じて、サードパーティサイトにcookieの利用に関するセキュリティ制御を導入するように設計されています。 詳しくは、[記事](https://web.dev/samesite-cookies-explained/)を参照してください。

この設定のデフォルト値(`SameSite=Lax`)は、AEMインスタンスまたはサービス間の認証が機能しない原因になる場合があります。 これは、これらのサービスのドメインやURL構造が、このcookieポリシーの制約に該当しない可能性があるからです。

この問題を回避するには、ログイントークンのSameSite cookieを`None`に設定する必要があります。

これを行うには、次の手順に従います。

1. AEM SDK Quickstartのバージョンをローカルにインストールする
1. `http://serveraddress:serverport/system/console/configMgr`のWebコンソールに移動
1. **AdobeGranite Token Authentication Handler**&#x200B;を検索してクリックします。
1. 次の図に示すように、login-token cookie **の** SameSite属性を`None`に設定します
   ![サメサイト](/help/security/assets/samesite1.png)
1. 「保存」をクリックします。
1. AEM SDK Quickstart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)を使用したOSGi設定の生成で説明されている手順に従って、この特定の設定のJSON形式の設定を生成します。[
1. [Cloud Manager API Format for Setting Properties](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGiドキュメントの手順に従って設定を適用します。

この設定が更新され、ユーザーがログアウトしてから再度ログインすると、`login-token` cookieには`None`属性が設定され、クロスサイトリクエストに含められます。