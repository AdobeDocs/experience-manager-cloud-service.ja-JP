---
title: GraphQLの永続クエリ — Dispatcher でのキャッシュの有効化
description: Dispatcher は、Adobe Experience Manager パブリッシュ環境の前にあるキャッシュとセキュリティのレイヤーです。AEMヘッドレスの永続クエリのキャッシュを有効にできます。
feature: Dispatcher, GraphQL API
source-git-commit: 0066bfba3a403791c6a35b1280ae04b576315566
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---


# GraphQLの永続クエリ — Dispatcher でのキャッシュの有効化 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Dispatcher でのキャッシュが有効な場合、 [CORS フィルター](/help/headless/deployment/cross-origin-resource-sharing.md) が不要なので、セクションを無視できます。

永続化されたクエリのキャッシュは、Dispatcher ではデフォルトで有効になっていません。 複数のオリジンで CORS（クロスオリジンリソース共有）を使用している場合、Dispatcher 設定を確認し、場合によっては更新する必要があるので、デフォルトを有効にすることはできません。

>[!NOTE]
>
>Dispatcher は `Vary` ヘッダー。
>
>他の CORS 関連ヘッダーのキャッシュは、Dispatcher で有効にすることができますが、CORS オリジンが複数ある場合は不十分な可能性があります。

>[!NOTE]
>
>Dispatcher に関する詳細なドキュメントについては、 [Dispatcher ガイド](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja).

## 永続クエリのキャッシュの有効化 {#enable-caching-persisted-queries}

永続化されたクエリのキャッシュを有効にするには、Dispatcher 変数を定義します `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. 変数を Dispatcher ファイルに追加します。 `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>を [キャッシュ可能なドキュメントに対する Dispatcher の要件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)を指定しない場合、Dispatcher はサフィックスを追加します `.json` をすべての永続化されたクエリ URL に追加し、結果をキャッシュできるようにします。
>
>このサフィックスは、永続化されたクエリのキャッシュが有効になると、書き換えルールによって追加されます。

## Dispatcher での CORS の設定 {#cors-configuration-in-dispatcher}

CORS リクエストを使用するお客様は、Dispatcher で CORS の設定を確認および更新する必要が生じる場合があります。

* The `Origin` ヘッダーは、Dispatcher を介してAEMパブリッシュに渡さないでください。
   * 次を確認します。 `clientheaders.any` ファイル。
* 代わりに、許可されたオリジンに対して、Dispatcher レベルで CORS リクエストを評価する必要があります。 また、この方法では、CORS 関連のヘッダーが、どの場合でも 1 か所で正しく設定されます。
   * このような設定は、 `vhost` ファイル。 次に設定例を示します。簡単にするために、CORS 関連の部分のみが提供されています。 特定の使用例に合わせて調整できます。

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
