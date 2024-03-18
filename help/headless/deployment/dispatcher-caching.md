---
title: GraphQL の永続クエリ - Dispatcher でのキャッシュの有効化
description: Dispatcher は、Adobe Experience Manager パブリッシュ環境の前にあるキャッシュとセキュリティのレイヤーです。AEM ヘッドレスの永続クエリのキャッシュを有効にできます。
feature: Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
source-git-commit: 6bcbef1695b291c36e19e70db203a114a7e40e67
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 90%

---

# GraphQL の永続クエリ - Dispatcher でのキャッシュの有効化 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Dispatcher でのキャッシュが有効な場合、[CORS フィルター](/help/headless/deployment/cross-origin-resource-sharing.md)が不要なので、セクションを無視できます。

永続化されたクエリのキャッシュは、Dispatcher ではデフォルトで有効になっていません。複数のオリジンで CORS（クロスオリジンリソース共有）を使用している場合、Dispatcher 設定を確認し、場合によっては更新する必要があるので、デフォルトで有効にすることはできません。

>[!NOTE]
>
>Dispatcher では `Vary` ヘッダーはキャッシュされません。
>
>他の CORS 関連ヘッダーのキャッシュは、Dispatcher で有効にすることができますが、CORS オリジンが複数ある場合は不十分な可能性があります。

>[!NOTE]
>
>Dispatcher に関する詳細なドキュメントについては、[Dispatcher ガイド](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

## 永続クエリのキャッシュを有効にする {#enable-caching-persisted-queries}

永続クエリーのキャッシュを有効にするには、Dispatcher 変数 `CACHE_GRAPHQL_PERSISTED_QUERIES` を定義します。

1. 変数を Dispatcher ファイル `global.vars` に追加します。

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>`Define CACHE_GRAPHQL_PERSISTED_QUERIES` を使用して永続化されたクエリに対して Dispatcher のキャッシュを有効にする場合、`ETag` ヘッダーが Dispatcher によって応答に追加されます。
>
>個人を成し遂げるには `ETag` キャッシュされた永続クエリ ( *各* 一意の応答 ) `FileETag Digest` dispatcher 設定の仮想ホスト設定で設定を使用する必要があります（まだ存在しない場合）。
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>[キャッシュ可能なドキュメントに対する Dispatcher の要件](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html?lang=ja#how-does-the-dispatcher-return-documents%3F)に適合するために、Dispatcher はすべての永続クエリ URL に接尾辞 `.json` を追加し、結果をキャッシュできるようにします。
>
>この接尾辞は、永続クエリのキャッシュが有効になると、書き換えルールによって追加されます。

## Dispatcher での CORS の設定 {#cors-configuration-in-dispatcher}

CORS リクエストを使用するお客様は、Dispatcher で CORS の設定を確認および更新する必要が生じる場合があります。

* `Origin` ヘッダーは、Dispatcher を介して AEM パブリッシュに渡さないでください。
   * `clientheaders.any` ファイルを確認します。
* 代わりに、許可されたオリジンに対して、Dispatcher レベルで CORS リクエストを評価する必要があります。また、この方法では、CORS 関連のヘッダーが、どの場合でも 1 か所で正しく設定されます。
   * このような設定は `vhost` ファイルに追加されます。次に設定例を示します。簡単にするために、CORS 関連の部分のみが提供されています。特定のユースケースに合わせて調整してください。

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
