---
title: AEM ヘッドレスを使用したクロスオリジンリソース共有（CORS）設定
description: Adobe Experience Manager のクロスオリジンリソース共有（CORS）を使用すると、ヘッドレス web アプリケーションで AEM へのクライアント側の呼び出しを行うことができます。GraphQL エンドポイントへのアクセスを有効にするには、CORS 設定が必要です。
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '208'
ht-degree: 100%

---

# クロスオリジンリソース共有（CORS）設定

>[!NOTE]
>
>AEM での CORS リソース共有ポリシーについて詳しくは、[クロスオリジンリソース共有（CORS）について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja#understand-cross-origin-resource-sharing-(cors))を参照してください。

GraphQL エンドポイントにアクセスするには、CORS ポリシーを設定し、[Cloud Manager を使用して AEM にデプロイ](/help/implementing/cloud-manager/deploy-code.md)された AEM プロジェクトに追加する必要があります。それには、目的のエンドポイントに適した OSGi CORS 設定ファイルを追加します。複数の CORS 設定を作成し、異なる環境にデプロイできます。例については、[WKND 参照サイト](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)をご確認ください。

CORS 設定では、アクセスを許可する必要がある信頼できる web サイトオリジン `alloworigin` または `alloworiginregexp` を指定する必要があります。

設定ファイルの名前は、`com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` のように指定する必要があります。`appname` は、アプリケーションの名前を反映します。

例えば、`https://my.domain` の GraphQL エンドポイント `/content/cq:graphql/wknd/endpoint` と永続クエリのエンドポイントへのアクセスを許可するには、以下を使用します。

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
