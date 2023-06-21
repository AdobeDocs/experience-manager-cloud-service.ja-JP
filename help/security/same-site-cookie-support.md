---
title: Adobe Experience Manager as a Cloud Service に対する Same Site Cookie の のサポート
description: Adobe Experience Manager as a Cloud Service に対する Same Site Cookie の のサポート
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 85%

---

# Adobe Experience Manager as a Cloud Service に対する Same Site Cookie の のサポート {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

バージョン 80 以降、Chrome およびそれ以降の Safari では、cookie セキュリティの新しいモデルが導入されました。このモードは、`SameSite` と呼ばれる設定を通じて、cookie の利用に関するセキュリティ制御をサードパーティサイトに導入するように設計されています。詳しくは、こちらの[記事](https://web.dev/samesite-cookies-explained/)を参照してください。

この設定のデフォルト値（`SameSite=Lax`）により、AEM インスタンスまたはサービス間の認証が機能しないことがあります。これは、これらのサービスのドメインや URL 構造が、この cookie ポリシーの制約に該当しない可能性があるためです。

この問題を回避するには、SameSite cookie 属性を `None` ログイントークン用。

>[!CAUTION]
>
>`SameSite=None` の設定は、セキュアプロトコル（HTTPS）の場合にのみ適用されます。
>
>セキュアプロトコルでない（HTTP）場合、この設定は無視され、サーバーは次の WARN メッセージを表示します。
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

次の手順に従って、設定を追加できます。

1. AEM SDK クイックスタートのバージョンをローカルにインストールする
1. Web コンソール（`http://serveraddress:serverport/system/console/configMgr`）にアクセスします。
1. **Adobe Granite Token Authentication Handler** を検索してクリックします。
1. 次の図に示すように、**login-token cookie の SameSite 属性**&#x200B;を `None` に設定します。
   ![samesite](/help/security/assets/samesite1.png)
1. 「保存」をクリックします。
1. ](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)AEM SDK クイックスタートを使用した OSGi 設定の生成[で説明されている手順に従って、この特定の設定の JSON 形式の設定を生成します。
1. [プロパティ設定用の Cloud Manager API 形式](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGiドキュメントの手順に従って設定を適用します。

この設定が更新され、ユーザーがログオフし、再度ログオンした後、 `login-token` cookie に `None` 属性セットに含まれ、クロスサイトリクエストに含まれます。
