---
title: カスタム HTTP ヘッダー
description: コマースエンジンに送信されるカスタム HTTP ヘッダーと、CIF から既に送信されたヘッダーを設定する方法について説明します。
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: ht
source-wordcount: '284'
ht-degree: 100%

---

# カスタム HTTP ヘッダー {#custom-http-headers}

## 概要 {#overview}

バックエンドをより詳細に制御するために、CIF によって既に送信されたヘッダーに加えて、コマースエンジンに送信されるカスタム HTTP ヘッダーを設定できます。一般的な使用例としては、マルチストアの設定で、HTTP ヘッダーを使用してコマースバックエンドの応答を制御できます。

>[!NOTE]
>
>開発者は、GraphQL クライアント設定を使用して、カスタム HTTP ヘッダーをいつでも設定できます。
>

## 設定 {#configuration}

カスタム HTTP ヘッダーを設定するには、まず定義する必要があります。カスタム HTTP ヘッダーを定義するには、まず OSGi 設定を使用して `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` サービス設定に追加する必要があります。

HTTP ヘッダーの値は、プロジェクトのクラウドサービス設定ページで設定できます。

1. ツール／クラウドサービス／CIF 設定のクラウドサービス設定ページに移動します。
1. 既存の設定を開くか、設定を作成します。
1. 「詳細」タブに移動し、「カスタム HTTP ヘッダー」マルチフィールドを探します。定義済みのヘッダーを選択し、それらに値を割り当てることができます。

上記のクラウドサービス設定を使用するコンポーネントは、すべての GraphQL リクエストでこれらの HTTP ヘッダーを送信します。

## 制限 {#restrictions}

このサービスでは、標準のヘッダー名を含め、任意のヘッダー名を定義することができますが、設定することはできません。つまり、この機能を使用して標準の HTTP ヘッダーを上書きすることはできません。制限付きヘッダー名のリストは、[mdn web docs - HTTP ヘッダー](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers)にあります。これらに加えて、使用できないヘッダーが 2 つあります。

* 「Store」 - CIF で Adobe Commerce ストアを識別するために使用
* 「Preview-Version」 - CIF がステージングされた製品を取得するために使用
