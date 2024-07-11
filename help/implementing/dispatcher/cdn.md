---
title: AEM as a Cloud Service での CDN
description: AEM の管理による CDN を使用する方法と、独自の CDN を AEM の管理による CDN にポイントする方法について説明します。
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 100%

---

# AEM as a Cloud Service での CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service での CDN"
>abstract="AEM as Cloud Service には、ビルトイン CDN が出荷時に搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。"

AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。

AEM の管理による CDN は、ほとんどのお客様のパフォーマンスとセキュリティに関する要件を満たします。 顧客は、オプションで、独自の CDN から公開層を参照することもできますが、その場合は自社で管理する必要があります。このシナリオは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM の管理による CDN  {#aem-managed-cdn}

Cloud Manager セルフサービス UI を使用して、AEM の標準搭載 CDN でコンテンツ配信の準備をするには、以下の節に従います。

1. [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**トラフィックの制限**

デフォルトでは、AEM の管理による CDN 設定の場合、実稼動環境と実稼動以外（開発およびステージング）の環境の両方で、すべてのパブリックトラフィックがパブリッシュサービスに到達できます。Cloud Manager ユーザーインターフェイスを使用して、特定の環境のパブリッシュサービスへのトラフィックを制限できます（IP アドレスの範囲でステージングを制限するなど）。

詳しくは、[IP 許可リストの管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)を参照してください。

>[!CAUTION]
>
>許可されている IP からのリクエストのみが、AEM の管理による CDN で処理されます。独自の CDN に AEM の管理による CDN を参照させる場合は、CDN の IP が許可リストに含まれていることを確認してください。

### CDN でのトラフィックの設定 {#cdn-configuring-cloud}

CDN トラフィックとフィルターを設定するルールは、設定ファイルで宣言し、[Cloud Manager の設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)を使用して CDN にデプロイできます。詳しくは、[CDN でのトラフィックの設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)および [WAF ルールを含むトラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)を参照してください。

### CDN エラーページの設定 {#cdn-error-pages}

CDN エラーページは、まれに AEM に到達できない場合にブラウザーに提供されるデフォルトのブランド化されていないページを上書きするように設定できます。詳しくは、[CDN エラーページの設定](/help/implementing/dispatcher/cdn-error-pages.md)を参照してください。

## 顧客 CDN で AEM の管理による CDN を参照する {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="顧客 CDN で AEM 管理 CDN を参照する"
>abstract="AEM as a Cloud Service は、顧客が既存の CDN を使用するためのオプションを提供しています。顧客は、オプションで、独自の CDN から公開層を参照することもできますが、その場合は自社で管理する必要があります。このシナリオは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。"

顧客が既存の CDN を使用する必要がある場合は、自社でその CDN を管理して AEM 管理による CDN を参照できます。ただし、次の条件を満たす必要があります。

* 顧客は、交換するのに手間がかかる既存 CDN を保有している。
* 顧客が自社で管理している。
* CDN を AEM as a Cloud Service と連携するように設定できる。設定手順を以下に示します。
* 関連する問題が発生する事態に備えて、エンジニアリング CDN エキスパートが待機している。
* 実稼動環境に移行する前に、負荷テストを実行し、成功している。

設定手順：

1. お使いの CDN が Adobe CDN のイングレスを元のドメインとして指すようにします。例：`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`
1. SNI をAdobe CDN の入力に設定する。
1. ホストヘッダーを接触チャネルドメインに設定します（例：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`）。
1. AEM がホストヘッダーを決定できるように、`X-Forwarded-Host` ヘッダーにドメイン名を設定します（例：`X-Forwarded-Host:example.com`）。
1. `X-AEM-Edge-Key` を設定します。この値はアドビから取得されます。

   * これは、Adobe CDN でリクエストのソースを検証し、`X-Forwarded-*` ヘッダーを AEM アプリケーションに渡すために必要です。例えば、`X-Forwarded-For` を使用してクライアント IP を決定します。したがって、`X-Forwarded-*` ヘッダーが正しいことを確認するのは、信頼できる呼び出し元（顧客が管理する CDN）の責任となります（以下のメモを参照）。
   * 必要に応じて、`X-AEM-Edge-Key` が存在しない場合に Adobe CDN の入口へのアクセスをブロックできます。Adobe CDN の入力に直接アクセスする必要がある場合（ブロックする場合）は、アドビにお知らせください。

主要な CDN ベンダーの設定例については、[CDN ベンダー設定のサンプル](#sample-configurations)の節を参照してください。

ライブトラフィックを受け入れる前に、アドビカスタマーサポートに問い合わせて、エンドツーエンドのトラフィックルーティングが正しく機能していることを検証してください。

`X-AEM-Edge-Key` を取得後、リクエストが正しくルーティングされているかどうかを、次のようにテストできます。

Linux® の場合：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

Windows の場合：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>なお、独自の CDN を使用する場合、Cloud Manager にドメインと証明書をインストールする必要はありません。Adobe CDN でのルーティングは、リクエスト `Host` ヘッダーで送信されるデフォルトのドメイン `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` を使用して行われます。リクエストの `Host` ヘッダーをカスタムドメイン名で上書きすると、リクエストが Adobe CDN によって誤ってルーティングされる可能性があります。


>[!NOTE]
>
>独自の CDN を管理している場合は、AEM CDN 経由で送信されるヘッダーの整合性を確保する必要があります。例えば、すべての `X-Forwarded-*` ヘッダーを消去し、既知の値と制御値に設定することをお勧めします。例えば、`X-Forwarded-For` にはクライアントの IP アドレスを含め、`X-Forwarded-Host` にはサイトのホストを含める必要があります。

>[!NOTE]
>
>サンドボックスプログラム環境では、顧客提供の CDN をサポートしていません。

顧客 CDN と AEM CDN の間の追加ホップは、キャッシュミスがあった場合にのみ必要になります。この記事で説明しているキャッシュ最適化戦略を使用すると、顧客 CDN を追加した場合でも、無視できるほどわずかな待ち時間しか発生しません。

この顧客 CDN 設定は、パブリッシュ層に対してサポートされていますが、オーサー層の前ではサポートされていません。

### CDN ベンダー設定のサンプル {#sample-configurations}

いくつかの主要な CDN ベンダーの設定例を以下に示します。

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## 位置情報ヘッダー {#geo-headers}

AEM の管理による CDN は、次のヘッダーを各リクエストに追加します。

* 国コード：`x-aem-client-country`
* 大陸コード：`x-aem-client-continent`

>[!NOTE]
>
>顧客の管理による CDN がある場合、これらのヘッダーは、実際のクライアントではなく、顧客の CDN プロキシサーバーの場所を反映します。したがって、顧客の管理による CDN の場合、位置情報ヘッダーは顧客の CDN で管理する必要があります。

国コードの値は、Alpha-2 コード（[ここ](https://ja.wikipedia.org/wiki/ISO_3166-1)で説明）です。

大陸コードの値は次のとおりです。

* AF - アフリカ
* AN - 南極大陸
* AS - アジア
* EU - ヨーロッパ
* NA - 北米
* OC - オセアニア
* SA - 中南米

この情報は、リクエストのオリジン（国）に基づいて別の URL にリダイレクトするなどの使用例に役立ちます。地理情報に依存するキャッシュ応答には、Vary ヘッダーを使用します。例えば、特定の国のランディングページにリダイレクトする場合は、常に `Vary: x-aem-client-country` を含める必要があります。必要に応じて、`Cache-Control: private` を使用してキャッシュを防ぐことができます。「[キャッシュ](/help/implementing/dispatcher/caching.md#html-text)」も参照してください。
