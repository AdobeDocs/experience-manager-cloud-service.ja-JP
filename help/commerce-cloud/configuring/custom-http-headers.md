---
title: カスタムHTTPヘッダー
description: カスタムHTTPヘッダーの設定
source-git-commit: 81d6c50635813fa106f58b61c5e88560422adc65
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# カスタムHTTPヘッダー {#custom-http-headers}

## 概要 {#overview}

作成者は、バックエンドをより詳細に制御するために、CIFによって既に送信されたヘッダーと共に、コマースエンジンに送信されるカスタムHTTPヘッダーを設定できます。 一般的な使用例としては、マルチストアの設定が含まれ、HTTPヘッダーを使用してコマースバックエンドの応答を制御できます。

>[!NOTE]
>
>開発者は、GraphQLクライアント設定を使用して、常にカスタムHTTPヘッダーを設定できます。


## 設定 {#configuration}

カスタムHTTPヘッダーを設定するには、まずヘッダーを定義する必要があります。 カスタムHTTPヘッダーは、まずOSGi設定を使用して`com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl`サービス設定に追加することで定義する必要があります。

HTTPヘッダーの値は、プロジェクトのCloud Service設定ページで設定できます。

1. ツール/Cloud Service/Cloud Services/CIF設定のページに移動します。
1. 既存の設定を開くか、新しい設定を作成します
1. 「詳細」タブに移動し、「カスタムHTTPヘッダー」複数フィールドを探します。 定義済みのヘッダーを選択し、それらに値を割り当てることができます。

上記のクラウドサービス設定を使用するコンポーネントは、GraphQL要求ごとにこれらのHTTPヘッダーを送信します。

## 制限 {#restrictions}

サービスでは、標準のヘッダー名を含む任意のヘッダー名を定義できますが、設定には使用できません。 つまり、この機能を使用して標準のHTTPヘッダーを上書きすることはできません。 制限されたヘッダー名のリストは、[ここ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)にあります。 これらに加えて、使用できないヘッダーがさらに2つあります。

* 「Store」 - CIFでMagentoストアを識別するために使用
* 「プレビューバージョン」 - CIFがステージングされた製品を取得するために使用
