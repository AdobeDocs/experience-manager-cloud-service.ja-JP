---
title: AEM as a Cloud Service での CDN
description: AEM as a Cloud Service での CDN
translation-type: tm+mt
source-git-commit: 8ca8944d37c1a10782597ec30c16b0151b5cd717
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 68%

---


# AEM as a Cloud Service での CDN {#cdn}

AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。

AEM が管理する CDN は、ほとんどの顧客のパフォーマンスとセキュリティに関する要件を満たします。パブリッシュ層では、オプションとして、顧客は独自の CDN からそれらを参照することもできますが、その場合は自社で管理する必要があります。このオプションは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。

## AEM 管理による CDN {#aem-managed-cdn}

次の節に従って、Cloud ManagerセルフサービスUIを使用し、Adobeの追加設定不要なCDNを使用してコンテンツ配信の準備を行います。

1. [SSL証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**トラフィックの制限**

デフォルトでは、アドビが管理する CDN のセットアップの場合、すべてのパブリックトラフィックは、実稼動版と非実稼動版（開発およびステージング）環境の両方で、パブリッシュサービスに到達できます。特定の環境の発行サービスへのトラフィックを制限する場合（例えば、一定のIPアドレスでステージングを制限する場合）、Cloud Manager UIを使用して、セルフサービスでこの操作を行うことができます。

詳しくは、[IP許可リストの管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)を参照してください。

## 顧客 CDN で AEM 管理 CDN を参照する {#point-to-point-CDN}

顧客が既存の CDN を使用する必要がある場合は、自社でその CDN を管理してアドビの管理対象 CDN を参照できます。ただし、次の条件を満たす必要があります。

* 顧客は、交換するのに手間がかかる既存 CDN を保有している。
* 顧客が自社で管理している。
* CDN を AEM as a Cloud Service と連携するように設定できる。設定手順を以下に示します。
* 関連する問題が発生する事態に備えて、エンジニアリング CDN エキスパートが待機している。
* 実稼動環境に移行する前に、負荷テストを実行し、成功している。

設定手順：

1. `X-Forwarded-Host` ヘッダーをドメイン名で設定します。
1. ホストヘッダーを接触チャネルドメインに設定します（アドビの CDN の入口）。この値はアドビから取得されます。
1. SNI ヘッダーを接触チャネルに送信します。ホストヘッダーと同様に、sni ヘッダーはドメイン接触チャネルです。
1. トラフィックを AEM サーバーに正しくルーティングするために必要な `X-Edge-Key` を設定します。この値はアドビから取得されます。

ライブトラフィックを受け入れる前に、アドビカスタマーサポートに問い合わせて、エンドツーエンドのトラフィックルーティングが正しく機能していることを検証する必要があります。

顧客 CDN からアドビが管理する CDN へのホップは効率的ですが、ホップの増加に伴い、パフォーマンスがわずかに低下する可能性があります。

この顧客 CDN 設定は、パブリッシュ層に対してサポートされていますが、オーサー層の前ではサポートされていません。

## 位置情報ヘッダー{#geo-headers}

Adobeが管理するCDNは、次の内容を含む各リクエストにヘッダーを追加します。

* 国コード：`x-aem-client-country`
* 大陸コード：`x-aem-client-continent`

国コードの値は、Alpha-2コード（[ここ](https://en.wikipedia.org/wiki/ISO_3166-1)で説明）です。

大陸コードの値は次のとおりです。

* AFアフリカ
* 南極大陸
* ASアジア
* EUヨーロッパ
* 北米
* オクセアニア
* 南アメリカ南部

この情報は、リクエストの接触チャネル（国）に基づいて別のURLにリダイレクトするなどの使用例に役立ちます。 ただし、この使用例ではリダイレクトは様々なのでキャッシュしないでください。 必要に応じて、`Cache-Control: private`を使用してキャッシュを防ぐことができます。 [キャッシュ](/help/implementing/dispatcher/caching.md#html-text)も参照してください。
