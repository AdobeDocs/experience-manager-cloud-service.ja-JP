---
title: AEM Headless を使用した Referrer Filter の設定
description: Adobe Experience Managerのリファラーフィルターを使用すると、サードパーティのホストからアクセスできます。 ヘッドレスアプリケーションの GraphQL エンドポイントへのアクセスを有効にするには、リファラーフィルターの OSGi 設定が必要です。
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# リファラーフィルター {#referrer-filter}

Adobe Experience Managerのリファラーフィルターを使用すると、サードパーティのホストからアクセスできます。 ヘッドレスアプリケーションの GraphQL エンドポイントへのアクセスを有効にするには、リファラーフィルターの OSGi 設定が必要です。

これは、リファラーフィルターに次の適切な OSGi 設定を追加することでおこなわれます。

* 信頼できる Web サイトのホスト名（`allow.hosts` または `allow.hosts.regexp`）を指定する。
* この名前のホストに対するアクセスを許可する。

ファイルの名前は次のように指定する必要があります。 `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

例えば、リファラー `my.domain` を持つリクエストにアクセスを許可するには、次の操作を行います。

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>以下は顧客の責任で行う必要があります。
>
>* 信頼できるドメインにのみアクセスを許可する
>* 機密情報が公開されていないことを確認する
>* ワイルドカードの [*] 構文を使用しない。これを使用すると、GraphQL エンドポイントへの認証済みアクセスが無効になり、エンドポイントが世界中に公開されることになります。


>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL [スキーマ](#schema-generation)は、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。
