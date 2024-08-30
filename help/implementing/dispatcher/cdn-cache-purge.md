---
title: CDN キャッシュのパージ
description: API 呼び出しで使用できるパージ API トークンを設定して、Adobe CDN キャッシュからキャッシュされたオブジェクトを削除する方法を説明します。
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: 5b777171cb9246c2a0174985e060d7d1b6ed8591
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 96%

---

# CDN キャッシュのパージ {#cdn-purge-cache}

パージでは、Adobe CDN キャッシュからオブジェクトが削除されるので、その後のリクエストはキャッシュから提供されるのではなく、キャッシュミスとして接触チャネルに向かいます。
AEM as a Cloud Service を使用すると、API 呼び出しのパージで使用できる API トークンのパージを設定できます。Cloud Manager 設定パイプライン認証ディレクティブを使用してこのトークンを設定する方法については、[CDN 資格情報および認証の設定](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)を参照してください。

サポートされているパージには、次の 3 つのバリエーションがあります。

* [単一 URL パージ](#single-purge) - 一度に 1 つのリソースをパージします。
* [代理キーによるパージ](#surrogate-key-purge) - 複数のリソースを一度にパージします。
* [完全パージ](#full-purge) - すべてのリソースをパージします。

すべてのパージバリエーションで次の点は共通しています。

* HTTP メソッドは `PURGE` に設定する必要があります。
* パージリクエストの対象となる AEM サービスに関連付けられている任意のドメインを URL にすることができます。
* HTTP ヘッダーで `X-AEM-Purge-Key` を指定する必要があります。

>[!CAUTION]
>（特にハードフラグで）CDN キャッシュをパージすると、オリジンでのトラフィックが増加し、適切に実行しないと機能停止につながる場合があります。

パージキーの設定と CDN キャッシュパージの実行に焦点を当てた [ チュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) を参照してください。

## 単一 URL パージ {#single-purge}

次の手順で、一度に 1 つのリソースをパージできます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

上記の例に示すように、**オプション**&#x200B;で、キャッシュされたオブジェクトに対して CDN で&#x200B;**ハード**&#x200B;パージ（デフォルト）を実行するか&#x200B;**ソフト**&#x200B;パージを実行するかを指定できます。

デフォルトのハードパージでは、コンテンツがオリジンから取得されるまで、新しいリクエストはコンテンツには直ちにアクセスできなくなります。ソフトパージでは、コンテンツが古いとマークされますが、クライアントには引き続き提供されるので、コンテンツがオリジンから取得されるまで待つ必要はありません。

## 代理キーによるパージ {#surrogate-key-purge}

代理キーは、一連のコンテンツをパージするために使用する一意の ID です。応答に `Surrogate-Key` ヘッダーを追加し、コンテンツに適用されます。1 つ以上の代理キーをパージ API 呼び出しで参照できます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

複数の `Surrogate-Key` はスペースで区切ります。単一 URL パージと同様に、ハードパージかソフトパージのどちらかを設定できます。

## 完全パージ {#full-purge}

キャッシュされたすべてのリソースの完全パージは、次の手順で実行できます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

`X-AEM-Purge` ヘッダーには「all」値を含める必要があることに注意してください。

## Apache／Dispatcher レイヤーとのインタラクション {#apache-layer}

[コンテンツ配信フロー](/help/implementing/dispatcher/overview.md)で説明されているように、キャッシュの有効期限が切れている場合、CDN は Apache／Dispatcher レイヤーからコンテンツを取得します。つまり、CDN でリソースをパージする前に、コンテンツの新しいバージョンを Dispatcher でも確実に入手できるようにする必要があります。詳しくは、[Dispatcher キャッシュの無効化](/help/implementing/dispatcher/caching.md#disp)も参照してください。
