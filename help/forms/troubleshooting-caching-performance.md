---
title: 'キャッシュパフォーマンスのトラブルシューティング  '
seo-title: Troubleshooting caching performance
description: 'キャッシュパフォーマンスのトラブルシューティング  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 100%

---

# キャッシュパフォーマンス {#caching-performance}

Cloud Service 環境でアダプティブフォームキャッシュを設定または使用する際に、次のような問題が発生する場合があります。

## 画像やビデオを含むアダプティブフォームの一部が、Dispatcher キャッシュから自動的に無効化されない {#images-videos-not-invalidated}

アダプティブフォームには、アセットブラウザーから画像やビデオを選択して追加できます。画像を Assets エディターで編集しても、その画像を含むアダプティブフォームのキャッシュ済みバージョンは無効になりません。アダプティブフォームに古い画像が引き続き表示されます。

この問題を解決するには、画像やビデオを公開した後、これらのアセットを参照するアダプティブフォームの公開を明示的に非公開にして公開します。

## コンテンツフラグメントまたはエクスペリエンスフラグメントを含む一部のアダプティブフォームが、Dispatcher キャッシュから自動的に無効化されない {#content-fragments-experience-fragments-not-invalidated}

アダプティブフォームには、コンテンツフラグメントまたはエクスペリエンスフラグメントを追加できます。これらのフラグメントが個別に編集および公開される場合、そのフラグメントが含まれるアダプティブフォームのキャッシュ済みバージョンは無効になりません。アダプティブフォームに古いフラグメントが引き続き表示されます。

この問題を解決するには、更新されたコンテンツフラグメントまたはエクスペリエンスフラグメントを公開した後、これらのアセットを使用するアダプティブフォームを明示的に非公開にして公開します。

## アダプティブフォームの最初のインスタンスのみがキャッシュされる {#only-first-instance-cached}

アダプティブフォーム URL にローカライゼーション情報が含まれておらず、設定マネージャーの「ブラウザーのロケールを使用する」オプションが有効な場合、ローカライズバージョンのアダプティブフォームが提供され、最初のリクエスト（ブラウザーロケールのリクエスト）に基づいてアダプティブフォームのインスタンスがキャッシュされ、以降の各ユーザーに配信されます。

問題を解決するには、以下の手順を実行します。

1. Experience Manager プロジェクトを開きます。
1. `dispatcher/scr/conf.d/rewrites/rewrite.rules` を開いて編集します。
1. 実行時に読み込むように設定された `conf.d/httpd-dispatcher.conf` またはその他の設定ファイルを開きます。
1. 次のコードをファイルに追加して保存します。これはサンプルコードです。環境に合わせて変更してください。

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN キャッシュが 300 秒後に動作を停止する {#cdn-caching-stops-working-after-300-seconds}

CDN キャッシュは 300 秒後に動作を停止し、CDN 上のキャッシュに対するすべてのリクエストは Dispatcher にリダイレクトされます。

この問題を解決するには、年齢ヘッダーを 0 に設定します。

1. `src\conf.d\available_vhosts` にファイルを作成します。

1. 次のようにファイルに追加して、年齢ヘッダーを設定します。

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. ファイルを保存して閉じます。
1. `src\conf.d\enabled_vhosts\default.vhost` へのソフトリンクを新しいファイルを指すように変更します。
