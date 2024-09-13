---
title: AEM as a Cloud Service での CDN
description: AEM の管理による CDN を使用する方法と、独自の CDN を AEM の管理による CDN にポイントする方法について説明します。
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 62%

---


# AEM as a Cloud Service での CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service での CDN"
>abstract="AEM as Cloud Service の出荷時には、組み込みの CDN が搭載されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。"

AEM as a Cloud Serviceには統合 CDN が付属しており、ユーザーのブラウザーに近いエッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を短縮するように設計されています。 この完全に管理された CDN は、AEM アプリケーションのパフォーマンス向けに最適化されています。

AEMの管理による CDN は、ほとんどのお客様のパフォーマンスとセキュリティのニーズを満たします。 パブリッシュ層の場合、お客様は、自身の CDN を介してトラフィックをルーティングすることを選択できますが、その場合は自身で管理する必要があります。 このオプションはケースバイケースで使用できます。特に、置き換えるのが困難な CDN プロバイダーと既存のレガシー統合がある場合に便利です。

Edge Delivery Services層への公開を検討しているお客様は、Adobeが管理する CDN を利用できます。 [Adobe管理の CDN](#aem-managed-cdn) を参照してください。<!-- CQDOC-21758, 5b -->


<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## アドビが管理する CDN {#aem-managed-cdn}

<!-- CQDOC-21758, 5a -->

Cloud Manager セルフサービス UI を使用して、AEMの組み込み CDN を使用したコンテンツ配信の準備を行う場合は、Adobeが管理する CDN 機能を利用できます。 この機能を使用すると、DV （ドメイン検証）証明書や EV/OV （拡張/組織検証）証明書などの SSL 証明書の設定およびインストールなど、セルフサービス CDN 管理を処理できます。 これらの方法について詳しくは、次を参照してください。

* [Cloud ManagerのEdge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)
* [カスタムドメイン名の概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
* [SSL 証明書の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
* [CDN 設定の追加](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)

**トラフィックの制限**

デフォルトでは、AEM の管理による CDN 設定の場合、実稼動環境と実稼動以外（開発およびステージング）の環境の両方で、すべてのパブリックトラフィックがパブリッシュサービスに到達できます。Cloud Manager ユーザーインターフェイスを使用して、特定の環境のパブリッシュサービスへのトラフィックを制限できます（IP アドレスの範囲でステージングを制限するなど）。

詳しくは、[IP 許可リストの管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)を参照してください。

>[!CAUTION]
>
>AEMの管理による CDN は、許可された IP からのみリクエストを配信します。 AEMの管理による CDN に対して独自の CDN を指定する場合は、CDN の IP が IP許可リストに含まれていることを確認します。

### CDN でのトラフィックの設定 {#cdn-configuring-cloud}

CDN でのトラフィックは、次のような様々な方法で設定できます。

* [トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)（オプションでライセンス可能な高度な WAF ルールを含む）による悪意のあるトラフィックのブロック
* [リクエストと応答](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)の特性の変更
* 301/302 [クライアントサイドのリダイレクト](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)の適用
* AEM 以外のバックエンドへのリクエストをリバースプロキシするための[接触チャネルセレクター](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)の宣言

Git の YAML ファイルを使用して、これらの機能を設定します。 また、Cloud Manager [Config パイプライン ](/help/implementing/dispatcher/cdn-configuring-traffic.md) を使用してデプロイします。

### CDN エラーページの設定 {#cdn-error-pages}

デフォルトのブランドのないページを置き換えるように、CDN エラーページを設定できます。 このカスタムページは、AEMが利用できないというまれな場合に表示されます。 詳しくは、[CDN エラーページの設定](/help/implementing/dispatcher/cdn-error-pages.md)を参照してください。

### CDN でキャッシュされたコンテンツをパージ {#purge-cdn}

HTTP キャッシュ制御ヘッダーを使用した TTL の設定は、コンテンツ配信のパフォーマンスとコンテンツの鮮度のバランスを取る効果的なアプローチです。ただし、更新されたコンテンツを直ちに提供することが重要なシナリオでは、CDN キャッシュを直接パージすると便利な場合があります。

[パージ API トークンの設定](/help/implementing/dispatcher/cdn-credentials-authentication.md/#purge-API-token)と[キャッシュされた CDN コンテンツのパージ](/help/implementing/dispatcher/cdn-cache-purge.md)を参照してください。

### CDN での基本認証 {#basic-auth}

ビジネス関係者がコンテンツのレビューを行うなどの簡単な認証ユースケースの場合は、ユーザー名とパスワードを必要とする基本認証ダイアログを表示して、コンテンツを保護します。[詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md)を確認し、早期導入プログラムに参加してください。

## お客様が管理する CDN がAEMが管理する CDN を指す {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="顧客 CDN で AEM 管理 CDN を参照する"
>abstract="AEM as a Cloud Service は、顧客が既存の CDN を使用するためのオプションを提供しています。顧客は、オプションで、独自の CDN から公開層を参照することもできますが、その場合は自社で管理する必要があります。このシナリオは、放棄が困難な CDN ベンダーとのレガシー統合を保有する顧客など（ただし、これに限定されない）、特定の前提条件を満たしていることに基づき、ケースバイケースで使用できます。"

お客様が既存の CDN を使用する必要がある場合は、自社でその CDN を管理してAEM管理による CDN を参照できます。ただし、次の条件を満たす必要があります。

* 顧客は、交換が必要な既存の CDN を持っている必要があります。
* 顧客が管理する必要があります。
* CDN をAEM as a Cloud Serviceと連携するように設定できる。設定手順を以下に示します。
* 関連する問題が発生する事態に備えて、エンジニアリング CDN エキスパートが待機している。
* お客様は、実稼動環境に移行する前に、負荷テストを実行して正常に合格する必要があります。

設定手順：

1. お使いの CDN が Adobe CDN のイングレスを元のドメインとして指すようにします。例：`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`
1. SNI をAdobe CDN の入力に設定する。
1. ホストヘッダーを接触チャネルドメインに設定します（例：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`）。
1. AEM がホストヘッダーを決定できるように、`X-Forwarded-Host` ヘッダーにドメイン名を設定します（例：`X-Forwarded-Host:example.com`）。
1. `X-AEM-Edge-Key` を設定します。[ この記事 ](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value) で説明しているように、Cloud Manager設定パイプラインを使用して値を設定する必要があります。

   * これは、Adobe CDN でリクエストのソースを検証し、`X-Forwarded-*` ヘッダーを AEM アプリケーションに渡すために必要です。例えば、`X-Forwarded-For` を使用してクライアント IP を決定します。したがって、`X-Forwarded-*` ヘッダーが正しいことを確認するのは、信頼できる呼び出し元（顧客が管理する CDN）の責任となります（以下のメモを参照）。
   * 必要に応じて、`X-AEM-Edge-Key` が存在しない場合に Adobe CDN の入口へのアクセスをブロックできます。Adobe CDN の入力に直接アクセスする必要がある場合（ブロックする場合）は、アドビにお知らせください。

主要な CDN ベンダーの設定例については、[CDN ベンダー設定のサンプル](#sample-configurations)の節を参照してください。

ライブトラフィックを受け入れる前に、アドビカスタマーサポートに問い合わせて、エンドツーエンドのトラフィックルーティングが正しく機能していることを検証してください。

`X-AEM-Edge-Key` を設定後、リクエストが正しくルーティングされているかどうかを、次のようにテストできます。

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
>なお、独自の CDN を使用する場合、Cloud Manager にドメインと証明書をインストールする必要はありません。Adobe CDN でのルーティングは、リクエスト `Host` ヘッダーで送信されるデフォルトのドメイン `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` を使用して行われます。 リクエスト `Host` ヘッダーをカスタムドメイン名で上書きすると、Adobe CDN 経由でリクエストが正しくルーティングされない可能性があります。

>[!NOTE]
>
>独自の CDN を管理している場合は、AEM CDN 経由で送信されるヘッダーの整合性を確保する必要があります。例えば、すべての `X-Forwarded-*` ヘッダーを消去し、既知の値と制御値に設定することをお勧めします。例えば、`X-Forwarded-For` にはクライアントの IP アドレスを含め、`X-Forwarded-Host` にはサイトのホストを含める必要があります。

>[!NOTE]
>
>サンドボックスプログラム環境は、顧客が提供した CDN をサポートしていません。

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

### 一般的なエラー {#common-errors}

提供されるサンプル設定は、必要なベース設定を示しています。 ただし、お客様の設定には、AEM as a Cloud Serviceがトラフィックに対応するために必要なヘッダーを削除、編集、再配置する、その他の影響を受けるルールが存在する場合があります。 顧客管理 CDN を AEM as a Cloud Service を指すように設定する際に発生する一般的なエラーを以下に示します。

**パブリッシュサービスエンドポイントへのリダイレクト**

リクエストが 403 forbidden 応答を受け取った場合、リクエストに必要なヘッダーの一部が欠落していることを意味します。よくある原因は、CDN が apex と `www` ドメインの両方のトラフィックを管理しているものの、`www` ドメインに適したヘッダーを追加していないことです。この問題は、AEM as a Cloud Service CDN ログを確認し、必要なリクエストヘッダーを確認することで、トリアージすることができます。

**リダイレクト ループが多すぎます**

ページで「リダイレクトが多すぎます」ループが発生すると、ページを強制的にページ自体に戻すリダイレクトに一致する一部のリクエストヘッダーが CDN に追加されます。例：

* CDN ルールは、apex ドメインまたは www ドメインのいずれかに一致するように作成され、apex ドメインの X-Forwarded-Host ヘッダーのみが追加されます。
* apex ドメインのリクエストはこの CDN ルールに一致し、apex ドメインを X-Forwarded-Host ヘッダーとして追加します。
* リダイレクトが apex ドメイン（例：^example.com）のホストヘッダーと明示的に一致する接触チャネルにリクエストが送信されます。
* 書き換えルールがトリガーされ、apex ドメインのリクエストが www サブドメインを含む https に書き換えられます。
* その後、このリダイレクトは顧客のエッジに送信され、CDN ルールが再度トリガーされ、www サブドメインではなく apex ドメインの X-Forwarded-Host ヘッダーが再度追加されます。その後、リクエストが失敗するまでプロセスが再度開始されます。

この問題を解決するには、SSL リダイレクト戦略、CDN ルール、リダイレクトおよび書き換えルールの組み合わせを評価します。

## 位置情報ヘッダー {#geo-headers}

AEM が管理する CDN は、次の情報を含む各リクエストにヘッダーを追加します。

* 国コード：`x-aem-client-country`
* 大陸コード：`x-aem-client-continent`

>[!NOTE]
>
>顧客の管理による CDN がある場合、これらのヘッダーは、実際のクライアントではなく、顧客の CDN プロキシサーバーの場所を反映します。 顧客が管理する CDN を使用する場合は、独自の CDN を通じて位置情報ヘッダーを管理する必要があります。

国コードの値は、[ISO 3166-1](https://ja.wikipedia.org/wiki/ISO_3166-1) で説明されている Alpha-2 コードです。

大陸コードの値は次のとおりです。

* AF - アフリカ
* AN - 南極大陸
* AS - アジア
* EU - ヨーロッパ
* NA - 北米
* OC - オセアニア
* SA - 中南米

この情報は、リクエストの生成国に基づいて別の URL にリダイレクトする場合に役立ちます。 地理情報に依存するキャッシュ応答には、Vary ヘッダーを使用します。例えば、特定の国のランディングページにリダイレクトする場合は、常に `Vary: x-aem-client-country` を含める必要があります。必要に応じて、`Cache-Control: private` を使用してキャッシュを防ぐことができます。「[キャッシュ](/help/implementing/dispatcher/caching.md#html-text)」も参照してください。
