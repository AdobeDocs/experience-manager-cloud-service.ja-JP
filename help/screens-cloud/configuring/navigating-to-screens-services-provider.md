---
title: Screens サービスプロバイダーへの移動
description: ここでは、Screens サービスプロバイダーへの移動方法について説明します。
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: 5452a02ed20d70c09728b3e34f248c7d37fc4668
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 87%

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

1. Cloud Managerの IPAEM機能により信頼できる IP アドレスのみにアクセスを許可するように許可リストに加える パブリッシュインスタンスを設定している場合、次に示すように、設定ダイアログでキー値を持つヘッダーを設定する必要があります。
また、許可リストに登録する必要がある IP も設定ファイルに移動する必要があり、Cloud Manager 設定から[適用解除](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list)する必要があります。

   ![画像](/help/screens-cloud/assets/configure/configure-screens20b.png)
AEM CDN 設定で同じキーを設定する必要があります。ヘッダー値を GitHub に直接入れず、[秘密鍵参照](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets)を使用することをお勧めします。
[CDN 設定 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf) のサンプルを以下に示します。

   ```kind: "CDN"
       version: "1"
       metadata:
         envTypes: ["dev", "stage", "prod"]
       data:
         trafficFilters:
           rules:
             - name: "block-request-from-not-allowed-ips"
               when:
                 allOf:
                   - reqProperty: clientIp
                     notIn: ["101.41.112.0/24"]
                    reqProperty: tier
                     equals: publish
               action: block
             - name: "allow-requests-with-header"
               when:
                 allOf:
                   - reqProperty: tier
                     equals: publish
                   - reqProperty: path
                     equals: /screens/channels.json
                   - reqHeader: x-screens-allowlist-key
                     equals: $\
       {CDN_HEADER_KEY}
               action:
                 type: allow
   ```

1. 左側のナビゲーションバーから「**チャネル**」を選択し、「**コンテンツプロバイダーで開く**」をクリックします。

   ![画像](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Screens コンテンツプロバイダーが別のタブで開き、コンテンツを作成できるようになります。

   ![画像](/help/screens-cloud/assets/configure/configure-screens2.png)





## 次の手順 {#whats-next}

Screens サービスプロバイダーのセットアップ方法を習得したら、[Screens コンテンツプロバイダーの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=ja#screens-content-provider)に移動して詳細を確認してください。
