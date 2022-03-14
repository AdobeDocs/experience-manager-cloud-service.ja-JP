---
title: AEMヘッドレスを使用したクロスオリジンリソース共有 (CORS) 設定
description: Adobe Experience Managerのクロスオリジンリソース共有 (CORS) を使用すると、ヘッドレス Web アプリケーションでAEMへのクライアント側の呼び出しをおこなうことができます。 GraphQL エンドポイントへのアクセスを有効にするには、CORS 設定が必要です。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 28%

---

# クロスオリジンリソース共有 (CORS) 設定

>[!NOTE]
>
>AEM での CORS リソース共有ポリシーについて詳しくは、[クロスオリジンリソース共有（CORS）について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja#understand-cross-origin-resource-sharing-(cors))を参照してください。

GraphQL エンドポイントにアクセスするには、CORS ポリシーを設定し、 [Cloud Manager を使用してAEMにデプロイ](/help/implementing/cloud-manager/deploy-code.md). それには、目的のエンドポイントに適した OSGi CORS 設定ファイルを追加します。複数の CORS 設定を作成し、異なる環境にデプロイできます。 例については、 [WKND 参照サイト](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

CORS 設定では、信頼できる Web サイトのオリジンを指定する必要があります `alloworigin` または `alloworiginregexp` アクセス権を付与する必要がある

設定ファイルの名前は次のように指定する必要があります。 `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` 場所 `appname` は、アプリケーションの名前を反映します。

例えば、GraphQL エンドポイントへのアクセスを許可するには、次のようにします。 `/content/cq:graphql/wknd/endpoint` および永続クエリエンドポイント `https://my.domain` 以下を使用できます。

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

エンドポイントのバニティーパスを設定した場合は、`allowedpaths` でも使用できます。
