---
title: AEM as a Cloud Service での CDN
description: AEM as a Cloud Service での CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 92b8a54f585e25db807914601ea5b3c07da681fc
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 98%

---

# AEM as a Cloud Service での CDN {#cdn}


>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service での CDN"
>abstract="AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。"

AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。

AEM が管理する CDN は、ほとんどの顧客のパフォーマンスとセキュリティに関する要件を満たします。パブリッシュ層では、オプションとして、顧客は独自の CDN からそれらを参照することもできますが、その場合は自社で管理する必要があります。このオプションは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。

## AEM 管理による CDN  {#aem-managed-cdn}

次のセクションの説明に従って、Cloud Manager セルフサービス UI を使用し、AEM の標準搭載 CDN を使用してコンテンツ配信の準備を行います。

1. [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**トラフィックの制限**

デフォルトでは、AEM 管理による CDN セットアップの場合、すべてのパブリックトラフィックは、実稼動版と非実稼動版（開発およびステージング）環境の両方で、パブリッシュサービスに到達できます。特定の環境のパブリッシュサービスへのトラフィックを制限する場合（例えば、一定の IP アドレスでステージングを制限する場合）、Cloud Manager UI を使用して、セルフサービスでこの操作を行うことができます。

詳しくは、「[IP 許可リストの管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)」を参照してください。

>[!CAUTION]
>
>許可されている IP からの要求のみが AEM 管理による CDN で処理されます。AEM 管理による CDN に対して独自の CDN を指定する場合は、CDN の IP が許可リストに含まれていることを確認します。

## 顧客 CDN で AEM 管理 CDN を参照する {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="顧客 CDN で AEM 管理 CDN を参照する"
>abstract="AEM as a Cloud Service は、顧客が既存の CDN を使用するためのオプションを提供しています。パブリッシュ層では、オプションとして、顧客は独自の CDN からそれらを参照することもできますが、その場合は自社で管理する必要があります。このオプションは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。"

顧客が既存の CDN を使用する必要がある場合は、自社でその CDN を管理して AEM 管理による CDN を参照できます。ただし、次の条件を満たす必要があります。

* 顧客は、交換するのに手間がかかる既存 CDN を保有している。
* 顧客が自社で管理している。
* CDN を AEM as a Cloud Service と連携するように設定できる。設定手順を以下に示します。
* 関連する問題が発生する事態に備えて、エンジニアリング CDN エキスパートが待機している。
* 実稼動環境に移行する前に、負荷テストを実行し、成功している。

設定手順：

1. CDN が Adobe CDN の入口を接触チャネルドメインとして指すようにします（例：`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`）。
1. また、SNI も Adobe CDN の入口に設定する必要があります。
1. ホストヘッダーを接触チャネルドメインに設定します（例：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`）。
1. AEM がホストヘッダーを決定できるように、`X-Forwarded-Host` ヘッダーにドメイン名を設定します（例：`X-Forwarded-Host:example.com`）。
1. `X-AEM-Edge-Key` を設定します。この値はアドビから取得されます。
   * これは、Adobe CDN でリクエストのソースを検証し、`X-Forwarded-*` ヘッダーを AEM アプリケーションに渡すために必要です。例えば、`X-Forwarded-For` を使用してクライアント IP を決定します。したがって、`X-Forwarded-*` ヘッダーが正しいことを確認するのは、信頼できる呼び出し元（顧客が管理する CDN）の責任となります（以下のメモを参照）。
   * 必要に応じて、`X-AEM-Edge-Key` が存在しない場合に Adobe CDN の入口へのアクセスをブロックできます。Adobe CDNの入力に直接アクセスする必要がある場合（ブロックする場合）は、アドビにお知らせください。

ライブトラフィックを受け入れる前に、アドビカスタマーサポートに問い合わせて、エンドツーエンドのトラフィックルーティングが正しく機能していることを検証する必要があります。

取得後 `X-AEM-Edge-Key`に値を入力する場合は、次のようにリクエストが正しくルーティングされているかをテストできます。

```
https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H 'X-Forwarded-Host: example.com' -H 'X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>'
```

なお、独自の CDN を使用する場合、Cloud Manager にドメインと証明書をインストールする必要はありません。Adobe CDN のルーティングは、デフォルトドメイン `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` を使用して行われます。

>[!NOTE]
>
>独自の CDN を管理している場合は、AEM CDN 経由で送信されるヘッダーの整合性を確保する必要があります。例えば、すべての `X-Forwarded-*` ヘッダーを消去し、既知の値と制御値に設定することをお勧めします。例えば、`X-Forwarded-For` にはクライアントの IP アドレスを含め、`X-Forwarded-Host` にはサイトのホストを含める必要があります。

>[!NOTE]
>
>サンドボックスプログラム環境では、顧客提供の CDN をサポートしていません。

顧客 CDN から AEM 管理による CDN へのホップは効率的ですが、ホップの増加に伴い、パフォーマンスがわずかに低下する可能性があります。

この顧客 CDN 設定は、パブリッシュ層に対してサポートされていますが、オーサー層の前ではサポートされていません。

## 位置情報ヘッダー {#geo-headers}

AEM が管理する CDN は、次の情報を含む各リクエストにヘッダーを追加します。

* 国コード：`x-aem-client-country`
* 大陸コード：`x-aem-client-continent`

国コードの値は、Alpha-2 コード（[ここ](https://ja.wikipedia.org/wiki/ISO_3166-1)で説明）です。

大陸コードの値は次のとおりです。

* AF - アフリカ
* AN - 南極大陸
* AS - アジア
* EU - ヨーロッパ
* NA - 北米
* OC - オセアニア
* SA - 中南米

この情報は、リクエストのオリジン（国）に基づいて別の URL にリダイレクトするなどの使用例に役立ちます。地域情報に依存するキャッシュ応答には、Vary ヘッダーを使用します。例えば、特定の国のランディングページにリダイレクトする場合は、常に `Vary: x-aem-client-country` を含める必要があります。必要に応じて、`Cache-Control: private` を使用してキャッシュを防ぐことができます。「[キャッシュ](/help/implementing/dispatcher/caching.md#html-text)」も参照してください。
