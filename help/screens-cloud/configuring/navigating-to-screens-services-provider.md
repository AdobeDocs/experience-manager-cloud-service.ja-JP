---
title: Screens サービスプロバイダーへの移動
description: ここでは、Screens サービスプロバイダーへの移動方法について説明します。
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: ea374f6e521d3b94d1d38af5c8f6780275ae2cb4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 63%

---

# Screens サービスプロバイダーへの移動 {#setup-screens-services-provider}

## はじめに {#introduction}

**Screens サービスプロバイダー**&#x200B;を使用すると、チャネルにコンテンツが追加された後で、コンテンツ作成者、開発者、および管理者がコンテンツ再生用のディスプレイとプレーヤーを管理できます。ユーザーは、AEM Cloud Service へのアクセス権が付与されたら、Screens サービスプロバイダーにログインできるようになります。

ここでは、Screens サービスプロバイダーの設定方法について説明します。


## 目的 {#objective}

次の節では、Screens サービスプロバイダーの設定およびセットアップ方法について説明します。

## Screens サービスプロバイダーの設定手順 {#screens-services-provider}

Screens サービスプロバイダーを設定するには、次の手順に従います。

1. [ここ](https://experience.adobe.com/screens)から Screens サービスプロバイダーに移動します。

   >[!CAUTION]
   >複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認してください。組織を変更するには、画面の右上隅にある組織名をクリックし、アクセスする必要がある組織を選択します。

1. 「プロジェクト」（左上隅）の横にある歯車アイコンをクリックします。

   ![画像](/help/screens-cloud/assets/configure/configure-screens0.png)

1. 設定を編集ダイアログボックスに、次の詳細を入力します。
   * **公開 URL** - AEM の公開 URL（例：`https://publish-p12345-e12345.adobeaemcloud.com`）
   * **オーサー URL** - AEM のオーサー URL（例：`https://author-p12345-e12345.adobeaemcloud.com`）

   >[!NOTE]
   >Screens サービスプロバイダーで AEM を設定する前に、少なくとも 1 つ の AEM 画面チャネルを必ず作成して公開します。チャネルを作成するには、コンテンツプロバイダーの /screens.html に移動します。

   ![画像](/help/screens-cloud/assets/configure/configure-screens4.png)

1. 「**保存**」をクリックして、Screens コンテンツプロバイダーに接続します。

1. Cloud Managerの IPAEM機能により信頼できる IP アドレスのみにアクセスを許可するように許可リストに加える パブリッシュインスタンスを設定した場合、次に示すように、設定ダイアログでキー値を持つヘッダーを設定する必要があります。
許可リストへの登録が必要な IP は、設定ファイルに移動し、Cloud Manager設定から [ 適用解除 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list) する必要もあります。

   ![ 画像 ](/help/screens-cloud/assets/configure/configure-screens20.png)
AEM CDN 設定でも同じキーを設定する必要があります。  ヘッダー値を直接 GITHub に配置せず、[ 秘密参照 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets) を使用することをお勧めします。
[CDN 設定 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf) のサンプルを以下に示します。
kind: &quot;CDN&quot;
バージョン : &quot;1&quot;
メタデータ：
envTypes:[&quot;dev&quot;、&quot;stage&quot;、&quot;prod&quot;]
データ：
trafficFilter:
ルール：
 – 名前：&quot;block-request-from-not-allowed-ips&quot;
日時：
allOf:
- reqProperty: clientIp
notIn: [&quot;101.41.112.0/24&quot;]
- reqProperty：層
次に等しい：公開
アクション : ブロック
 – 名前：「allow-requests-with-header」
日時：
allOf:
- reqProperty：層
次に等しい：公開
- reqProperty: path
次に等しい：/screens/channels.json
許可リストに加える - reqHeader: x-screens-key
次に等しい：${\
   {CDN_HEADER_KEY}
アクション :
タイプ：許可

1. 左側のナビゲーションバーから「**チャネル**」を選択し、「**コンテンツプロバイダーで開く**」をクリックします。

   ![画像](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Screens コンテンツプロバイダーが別のタブで開き、コンテンツを作成できるようになります。

   ![画像](/help/screens-cloud/assets/configure/configure-screens2.png)





## 次の手順 {#whats-next}

Screens サービスプロバイダーのセットアップ方法を習得したら、[Screens コンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=ja#screens-content-provider)に移動して詳細を確認してください。
