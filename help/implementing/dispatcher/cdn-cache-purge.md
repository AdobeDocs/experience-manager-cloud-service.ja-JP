---
title: CDN キャッシュのパージ
description: API 呼び出しで使用できるパージ API トークンを設定して、Adobe CDN キャッシュからキャッシュされたオブジェクトを削除する方法を説明します。
feature: CDN Cache
source-git-commit: bd8f534642848a656e5e54c425049c95cdb413f7
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# CDN キャッシュのパージ {#cdn-purge-cache}

>[!NOTE]
>この機能はまだ一般提供されていません。早期導入プログラムに参加するには、次のメールを送信します `aemcs-cdn-config-adopter@adobe.com`.

パージでは、Adobe CDN キャッシュからオブジェクトが削除されるので、今後のリクエストはキャッシュから提供されるのではなく、キャッシュミスとしてオリジンに進みます。
AEMas a Cloud Serviceを使用すると、API 呼び出しで使用できるパージ API トークンを設定できます。 を読み取る [CDN 資格情報と認証の設定に関する記事](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) cloud Manager 設定パイプライン認証ディレクティブを使用してこのトークンを設定する方法を説明します。

サポートされているパージのバリエーションは 3 つあります。

* [単一 URL のパージ](#single-purge)  – 一度に 1 つのリソースをパージします。
* [代理キーによるパージ](#surrogate-key-purge)  – 複数のリソースを一度にパージします。
* [完全パージ](#full-purge)  – すべてのリソースをパージします。

すべてのパージのバリエーションで共有されるのは次のとおりです。

* この HTTP メソッドはに設定する必要があります。 `PURGE`.
* URL には、パージリクエストの対象となるAEM サービスに関連付けられた任意のドメインを指定できます。
* この `X-AEM-Purge-Key` http ヘッダーで指定する必要があります。

>[!CAUTION]
>CDN キャッシュをパージすると（特にハードフラグの場合）、オリジンでのトラフィックが増加し、適切に実行しないと停止が発生する可能性があります。

## 単一 URL のパージ {#single-purge}

次の手順で、一度に 1 つのリソースをパージできます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

上記の例に示すように、次のことができます **任意選択** cdn で以下を実行する必要があるかどうかを指定 **ハード** パージ（デフォルト）または **ソフト** キャッシュされたオブジェクトでパージします。

デフォルトのハードパージでは、コンテンツが元の場所から取得されるまで、新しいリクエストに対してコンテンツは直ちにアクセスできなくなります。 ソフトパージは、コンテンツを古いとマークしますが、クライアントには引き続き提供されるので、コンテンツが接触チャネルから取得されるまで待つ必要はありません。

## 代理キーパージ {#surrogate-key-purge}

サロゲートキーは、一連のコンテンツをパージするために使用する一意の ID です。 タグをコンテンツに適用するには、 `Surrogate-Key` 応答のヘッダー。 1 つ以上のサロゲートキーをパージ API 呼び出しで参照できます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

この `Surrogate-Key`（s）はスペースで区切ります。 単一の URL パージと同様に、ハードパージまたはソフトパージのいずれかを設定できます。

## 完全パージ {#full-purge}

次の手順で、キャッシュされたすべてのリソースの完全なパージを実行できます。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

次のことに注意してください `X-AEM-Purge` ヘッダーには「all」値を含める必要があります。

## Apache/Dispatcher レイヤーとのインタラクション {#apache-layer}

で説明されているように [コンテンツ配信フローに関する記事](/help/implementing/dispatcher/overview.md)キャッシュの有効期限が切れている場合、CDN は Apache/Dispatcher レイヤーからコンテンツを取得します。 つまり、CDN でリソースをパージする前に、コンテンツの新しいバージョンを Dispatcher でも使用できるようにする必要があります。 詳しくは、次も参照してください [Dispatcher キャッシュの無効化](/help/implementing/dispatcher/caching.md#disp).
