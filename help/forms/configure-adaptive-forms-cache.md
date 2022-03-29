---
title: アダプティブフォームのキャッシュの設定
seo-title: Configure Adaptive Forms cache
description: 'アダプティブフォームのキャッシュは、アダプティブフォームおよびアダプティブドキュメント向けに設計されています。これは、クライアントサイドのアダプティブフォームまたはドキュメントのレンダリングの時間を短縮する目的で、アダプティブフォームとアダプティブドキュメントをキャッシュします。 '
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 100%

---


# アダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、遅延を削減して I／O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、クライアントサイドのアダプティブフォームのレンダリングの時間を短縮します。特にアダプティブフォーム向けに設計されています。

## オーサーおよびパブリッシュインスタンスでのアダプティブフォームのキャッシュの設定 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。
1. [!UICONTROL 設定値を編集]ダイアログで、AEM [!DNL Forms] サーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を「**[!UICONTROL アダプティブフォームの数]**」フィールドに指定します。デフォルト値は 100 です。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

   ![アダプティブフォームの HTML キャッシュの設定ダイアログ](assets/cache-configuration-edit.png)

1. 「**[!UICONTROL 保存]**」をクリックして、設定を保存します。

環境は、アダプティブフォームと関連アセットのキャッシュを使用するように設定されています。


## （オプション）Dispatcher でのアダプティブフォームのキャッシュの設定 {#configure-the-cache}

パフォーマンスをさらに向上させるために、Dispatcher でアダプティブフォームのキャッシュを設定することもできます。

### 前提条件 {#pre-requisites}

* [クライアントでのデータの結合または事前入力](prepopulate-adaptive-form-fields.md#prefill-at-client)オプションを有効にします。これは、事前入力されたフォームの各インスタンスの一意のデータを結合するのに役立ちます。
* [すべてのパブリッシュインスタンスに対してフラッシュエージェントを有効にします](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=ja#invalidating-dispatcher-cache-from-a-publishing-instance)。これにより、アダプティブフォームのキャッシュパフォーマンスが向上します。フラッシュエージェントのデフォルト URL は `http://[server]:[port]]/etc/replication/agents.publish/flush.html` です。

### Dispatcher 上でアダプティブフォームをキャッシュする際の考慮事項 {#considerations}

* アダプティブフォームのキャッシュを使用する場合、AEM [!DNL Dispatcher] を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。
* 拡張子のない URL はキャッシュされません。例えば、パターン `/content/forms/[folder-structure]/[form-name].html` の URL はキャッシュされ、パターン `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content` の URL は無視されます。したがって、キャッシュのメリットを活用するには、拡張子が付いた URL を使用します。
* ローカライズされたアダプティブフォームの考慮事項：
   * `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>` の代わりに `http://host:port/content/forms/af/<afName>.<locale>.html` の URL 形式を使用して、アダプティブフォームのローカライズ版をリクエストします。
   * `http://host:port/content/forms/af/<adaptivefName>.html` 形式の URL に対するブラウザーロケール<!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->の使用を無効にします。
   * URL 形式 `http://host:port/content/forms/af/<adaptivefName>.html` を使用し、設定マネージャーで「**[!UICONTROL ブラウザーロケールを使用]**」が無効になっている場合、アダプティブフォームの非ローカライズ版が提供されます。非ローカライズ言語とは、アダプティブフォームの開発時に使用される言語です。ブラウザーに設定されているロケール（ブラウザーロケール）は考慮されず、アダプティブフォームの非ローカライズ版が提供されます。
   * URL 形式 `http://host:port/content/forms/af/<adaptivefName>.html` を使用し、設定マネージャーで「**[!UICONTROL ブラウザーロケールを使用]**」が有効になっている場合、アダプティブフォームのローカライズ版が提供されます（利用可能な場合）。ローカライズされたアダプティブフォームの言語は、ブラウザーに設定されたロケール（ブラウザーロケール）に基づきます。これは、[アダプティブフォームの最初のインスタンスのみがキャッシュされる]原因になる可能性があります。インスタンスで問題が発生しないようにするには、[トラブルシューティング](#only-first-insatnce-of-adptive-forms-is-cached)を参照してください。

### Dispatcher でのキャッシュの有効化

Dispatcher 上のアダプティブフォームのキャッシュを有効にして設定するには、以下の手順を実行します。

1. 環境の各パブリッシュインスタンスに対して以下の URL を開き、レプリケーションエージェントを設定します。
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [dispatcher.any ファイルに以下を追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#automatically-invalidating-cached-files)。

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   上記を追加すると、以下のようになります。

   * アダプティブフォームは、更新されたバージョンのフォームが公開されなくなるまで、キャッシュ内に残ります。

   * アダプティブフォームで参照されている新しいバージョンのリソースが公開されると、影響を受けたアダプティブフォームは自動的に無効になります。参照されるリソースの自動無効化には、いくつかの例外があります。例外の回避策については、 [トラブルシューティング](#troubleshooting) の節を参照してください。
1. [以下のルール dispatcher.any またはカスタムルールファイルを追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#specifying-the-documents-to-cache)。キャッシュをサポートしない URL は除外されます。例えば、インタラクティブ通信などです。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [「URL パラメーターを無視」リストに以下のパラメーターを追加します](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#ignoring-url-parameters)。

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

AEM 環境は、アダプティブフォームをキャッシュするように設定されています。すべてのタイプのアダプティブフォームをキャッシュします。キャッシュされたページを配信する前に、ページのユーザーアクセス権限を確認する必要がある場合は、[セキュリティで保護されたコンテンツのキャッシュ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ja)を参照してください。

## トラブルシューティング {#troubleshooting}

### 画像やビデオを含むアダプティブフォームの一部が、Dispatcher キャッシュから自動的に無効化されない {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

アセットブラウザーで画像やビデオを選択してアダプティブフォームに追加し、これらの画像およびビデオをアセットエディターで編集する場合、このような画像を含むアダプティブフォームが、Dispatcher キャッシュから自動的に無効になりません。

#### 解決策 {#Solution1}

画像とビデオを公開した後、これらのアセットを参照するアダプティブフォームを明示的に非公開にしてから公開します。

### コンテンツフラグメントまたはエクスペリエンスフラグメントを含む一部のアダプティブフォームが、Dispatcher キャッシュから自動的に無効化されない {#content-or-experience-fragment-not-auto-invalidated}

#### 問題 {#issue2}

コンテンツフラグメントやエクスペリエンスフラグメントをアダプティブフォームに追加し、これらのアセットを個別に編集して公開する場合、このようなアセットを含むアダプティブフォームは、Dispatcher キャッシュから自動的に無効になりません。

#### 解決策 {#Solution2}

更新されたコンテンツフラグメントまたはエクスペリエンスフラグメントを公開した後、これらのアセットを使用するアダプティブフォームを明示的に非公開にしてから公開します。

### アダプティブフォームの最初のインスタンスのみがキャッシュされる {#only-first-insatnce-of-adptive-forms-is-cached}

#### 問題 {#issue3}

アダプティブフォーム URL にローカライゼーション情報がなく、設定マネージャーの「**[!UICONTROL ブラウザーロケールを使用]**」が有効になっている場合、アダプティブフォームのローカライズ版が提供され、アダプティブフォームの最初のインスタンスのみがキャッシュされて後続のすべてのユーザーに配信されます。

#### 解決策 {#Solution3}

問題を解決するには、以下の手順を実行します。

1. conf.d/httpd-dispatcher.conf または実行時に読み込むように設定されたその他の設定ファイルを開きます。

1. 次のコードをファイルに追加して保存します。これはサンプルコードです。環境に合わせて変更してください。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
