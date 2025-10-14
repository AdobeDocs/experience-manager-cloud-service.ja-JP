---
title: AEM ヘッドレスを使用したリファラーフィルターの設定
description: Adobe Experience Manager のリファラーフィルターを使用すると、サードパーティのホストからアクセスできます。ヘッドレスアプリケーションの GraphQL エンドポイントへのアクセスを有効にするには、リファラーフィルターの OSGi 設定が必要です。
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 56%

---

# リファラーフィルター {#referrer-filter}

Adobe Experience Manager のリファラーフィルターを使用すると、サードパーティのホストからアクセスできます。

HTTP POST 経由でヘッドレスアプリケーションの GraphQL エンドポイントにアクセスできるようにするには、リファラーフィルターの OSGi 設定が必要です。HTTP GET 経由で AEM にアクセスする AEM ヘッドレス永続クエリを使用する場合、リファラーフィルターの設定は必要ありません。

>[!WARNING]
> AEM のリファラーフィルターは OSGi 設定ファクトリではありません。つまり、AEM サービスで一度にアクティブになる設定は 1 つだけです。可能であれば、カスタムリファラーフィルター設定を追加しないでください。これにより、AEM のネイティブ設定が上書きされ、製品の機能が損なわれる可能性があります。

これを行うには、リファラーフィルターに次の適切な OSGi 設定を追加します。

* 信頼できる web サイトのホスト名（`allow.hosts` または `allow.hosts.regexp`）を指定する。
* この名前のホストに対するアクセスを許可する。

ファイル名は、`org.apache.sling.security.impl.ReferrerFilter.cfg.json`.のように指定する必要があります。

## 設定例 {#example-configuration}

例えば、リファラー `my.domain` を持つリクエストにアクセスを許可するには、次の操作を行います。

>[!CAUTION]
>
>これは、標準設定を上書きする基本的な例です。 製品のアップデートは、カスタマイズに常に適用されるようにする必要があります。

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

## データのセキュリティ {#data-security}

>[!CAUTION]
>
>これは、完全に次の点に対処するためにあなたの責任が残っている。

データのセキュリティを確実に維持するには、次の点を確認する必要があります。

* アクセスは信頼されたドメインに **のみ** 許可されています

* ワイルドカード [`*`] 構文が使用されています **使用されていません**。これにより、GraphQL エンドポイントへの認証済みアクセスが無効になり、世界中に公開されます

* 機密情報は決して公開されず **直接的にも間接的にも** 公開されません。

   * 例えば、すべての [GraphQL スキーマ &#x200B;](/help/headless/graphql-api/content-fragments.md#schema-generation) は次のとおりです。

      * **有効** になっているコンテンツフラグメントモデルから派生

     **and**

      * GraphQL エンドポイントを介して読み取り可能

     つまり、モデル定義のフィールド名として存在する情報を使用できるようになります。

機密データがどの手段でも利用できないことを確認する必要があるので、そのような詳細は慎重に検討する必要があります。
