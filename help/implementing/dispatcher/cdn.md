---
title: AEM as a Cloud Service での CDN
description: AEM as a Cloud Service での CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
translation-type: tm+mt
source-git-commit: 3d0f58754aaff3a0c505f60a9c24b4712c2e4c30
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 64%

---

# AEM as a Cloud Service での CDN {#cdn}

AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。

AEM が管理する CDN は、ほとんどの顧客のパフォーマンスとセキュリティに関する要件を満たします。パブリッシュ層では、オプションとして、顧客は独自の CDN からそれらを参照することもできますが、その場合は自社で管理する必要があります。このオプションは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。

## AEM 管理による CDN {#aem-managed-cdn}

次の節に従って、Cloud Manager セルフサービス UI を使用し、AEM の標準搭載 CDN を使用してコンテンツ配信の準備を行います。

1. [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**トラフィックの制限**

デフォルトでは、AEM 管理による CDN セットアップの場合、すべてのパブリックトラフィックは、実稼動版と非実稼動版（開発およびステージング）環境の両方で、パブリッシュサービスに到達できます。特定の環境のパブリッシュサービスへのトラフィックを制限する場合（例えば、一定の IP アドレスでステージングを制限する場合）、Cloud Manager UI を使用して、セルフサービスでこの操作をおこなうことができます。

詳しくは、「[IP 許可リストの管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)」を参照してください。

>[!CAUTION]
>
>許可されている IP からの要求のみが AEM 管理による CDN で処理されます。AEMが管理するCDNに対して独自のCDNを指定する場合は、CDNのIPが許可リストに含まれていることを確認します。

## 顧客 CDN で AEM 管理 CDN を参照する {#point-to-point-CDN}

顧客が既存の CDN を使用する必要がある場合は、自社でその CDN を管理して AEM 管理による CDN を参照できます。ただし、次の条件を満たす必要があります。

* 顧客は、交換するのに手間がかかる既存 CDN を保有している。
* 顧客が自社で管理している。
* CDN を AEM as a Cloud Service と連携するように設定できる。設定手順を以下に示します。
* 関連する問題が発生する事態に備えて、エンジニアリング CDN エキスパートが待機している。
* 実稼動環境に移行する前に、負荷テストを実行し、成功している。

設定手順：

1. `X-Forwarded-Host` ヘッダーをドメイン名で設定します。例：`X-Forwarded-Host:example.com`
1. ホストヘッダーをオリジンドメインに設定します（AEM CDN の入口）。例：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`
1. SNI ヘッダーをオリジンに送信します。ホストヘッダーと同様に、SNIヘッダーは接触チャネルドメインである必要があります。
1. `X-Edge-Key`または`X-AEM-Edge-Key`を設定します（CDNが`X-Edge-*`を取り除く場合）。 この値はアドビから取得されます。
   * これは、AdobeCDNがリクエストのソースを検証し、`X-Forwarded-*`ヘッダーをAEMアプリケーションに渡すために必要です。 例えば、AEMは`X-Forwarded-Host`を使用してホストヘッダーを決定し、`X-Forwarded-For`を使用してクライアントIPを決定します。 したがって、`X-Forwarded-*`ヘッダの正確性を保証するのは、信頼できる呼び出し元（例：お客様管理のCDN）の責任になります（下記の注意を参照）。
   * 必要に応じて、`X-Edge-Key`が存在しない場合にAdobeCDNの入力へのアクセスをブロックできます。 AdobeCDNの入力に直接アクセスする必要がある場合（ブロックする場合）は、Adobeに通知してください。

ライブトラフィックを受け入れる前に、Adobeのカスタマーサポートに問い合わせて、エンドツーエンドのトラフィックルーティングが正しく機能していることを検証する必要があります。

>[!NOTE]
>
>独自のCDNを管理するお客様は、AEM CDN経由で送信されるヘッダーの整合性を確保する必要があります。 例えば、すべての`X-Forwarded-*`ヘッダーを消去し、既知の値と制御値に設定することをお勧めします。 例えば、`X-Forwarded-For`にはクライアントのIPアドレスを含め、`X-Forwarded-Host`にはサイトのホストを含める必要があります。

顧客 CDN から AEM 管理による CDN へのホップは効率的ですが、ホップの増加に伴い、パフォーマンスがわずかに低下する可能性があります。

このお客様のCDN設定は発行層でサポートされていますが、作成者層の前ではサポートされていません。

## 位置情報ヘッダー {#geo-headers}

AEMが管理するCDNは、次のコマンドを使用して各リクエストにヘッダーを追加します。

* 国コード: `x-aem-client-country`
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

この情報は、リクエストのオリジン（国）に基づいて別の URL にリダイレクトするなどの使用例に役立ちます。地域情報に依存するキャッシュ応答には、Varyヘッダーを使用します。 例えば、特定の国のランディングページにリダイレクトする場合は、常に`Vary: x-aem-client-country`を含める必要があります。 必要に応じて、`Cache-Control: private` を使用してキャッシュを防ぐことができます。「[キャッシュ](/help/implementing/dispatcher/caching.md#html-text)」も参照してください。
