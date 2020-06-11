---
title: AEMでのクラウドサービスとしてのキャッシュ
description: 'AEMでのクラウドサービスとしてのキャッシュ '
translation-type: tm+mt
source-git-commit: 18c2f70acd33c83a0d98ccb658d3e9be18b34c8b
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 85%

---


# 概要 {#intro}

トラフィックは、CDNを経由してApache Webサーバーレイヤーに渡されます。このレイヤーは、ディスパッチャーを含むモジュールをサポートします。 パフォーマンスを向上させるために、ディスパッチャーは主にキャッシュとして使用され、発行ノードで処理を制限します。
ルールをディスパッチャーの設定に適用して、デフォルトのキャッシュ有効期限の設定を変更し、CDNでのキャッシュを可能にします。 Note that dispatcher also respects the resulting cache expiration headers if `enableTTL` is enabled in the dispatcher configuration, implying that it will refresh specific content even outside of content being republished.

また、このページでは、ディスパッチャーキャッシュの無効化の方法、およびクライアント側ライブラリに関するブラウザーレベルでのキャッシュの動作についても説明します。

## キャッシュ {#caching}

### HTML/Text {#html-text}

* デフォルトでは、Apache レイヤーによって生成されるキャッシュ制御ヘッダーに基づいて、ブラウザーによって 5 分間キャッシュされます。CDN はこの値も順守します。
* AEM as a Cloud Service の SDK Dispatcher ツールを使用して、`global.vars` の `EXPIRATION_TIME` 変数を定義することにより、すべての HTML/Text コンテンツに対して上書きできます。
* 次の apache mod_headers ディレクティブを使用して、より詳細なレベルで上書きできます。

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

`src/conf.dispatcher.d/cache` の下のファイルに次のルール（デフォルト設定）があることを確認する必要があります。

```
/0000
{ /glob "*" /type "allow" }
```

* 特定のコンテンツがキャッシュされないようにするには、Cache-Controlヘッダーを「private」に設定します。 例えば、次の例では、&quot;myfolder&quot;という名前のディレクトリ下のhtmlコンテンツがキャッシュされないようにします。

```
<LocationMatch "\/myfolder\/.*\.(html)$">.  // replace with the right regex
    Header set Cache-Control “private”
</LocationMatch>
```

* [dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)を含む他のメソッドでは、値は上書きされません。

### クライアントサイドライブラリ（js、css） {#client-side-libraries}

* AEM のクライアントサイドライブラリフレームワークを使用すると、変更が新しいファイルとして一意のパスで表示されるので、JavaScript と CSS コードは、ブラウザーで無期限にキャッシュできるように生成されます。つまり、クライアントライブラリを参照する HTML は必要に応じて作成されるので、顧客は公開時に新しいコンテンツを体験できます。「immutable」値を考慮しない古いブラウザーでは、cache-control は「immutable」または 30 日に設定されます。
* 詳しくは、[クライアントサイドライブラリとバージョンの整合性](#content-consistency)を参照してください。

### BLOB ストレージに格納されるほど大きい画像とコンテンツ {#images}

* デフォルトではキャッシュされません。
* 次の Apache `mod_headers` ディレクティブを使用して、より詳細なレベルに設定できます。

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

src/conf.dispatcher.d/cache の下のファイルに、次のルール（デフォルト設定）があることを確認する必要があります。

```
/0000
{ /glob "*" /type "allow" }
```

キャッシュせずに非公開にするアセットが、LocationMatch ディレクティブフィルターの一部ではないことを確認します。

* [dispatcher-ttl AEM ACS Commons プロジェクト](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)を含む他のメソッドでは、値は上書きされません。

### ノードストア内の他のコンテンツファイルタイプ {#other-content}

* デフォルトのキャッシュなし
* HTML／Text ファイルタイプに使用する `EXPIRATION_TIME` 変数はデフォルトに設定できません
* キャッシュの有効期限は、HTML/Text の節で説明したのと同じ LocationMatch 方法で、適切な正規表現を指定することで設定できます

## ディスパッチャーキャッシュの無効化 {#disp}

一般に、ディスパッチャーキャッシュを無効にする必要はありません。 代わりに、コンテンツが再公開される際にディスパッチャーがキャッシュを更新し、CDNがキャッシュの有効期限のヘッダーを考慮する必要があります。

### アクティベーション／非アクティベーション中の Dispatcher キャッシュの無効化 {#cache-activation-deactivation}

以前のバージョンの AEM と同様に、ページの公開または非公開では、Dispatcher のキャッシュからコンテンツがクリアされます。キャッシュに問題があると疑われる場合は、該当するページを再度公開する必要があります。

パブリッシュインスタンスは、オーサーから新しいバージョンのページまたはアセットを受け取ると、フラッシュエージェントを使用して Dispatcher 上の適切なパスを無効にします。更新されたパスは、親と共に、Dispatcher キャッシュから削除されます（削除されるレベルは [statfilelevel](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level) で設定できます）。

### 明示的な Dispatcher キャッシュの無効化 {#explicit-invalidation}

一般に、Dispatcher 内のコンテンツを手動で無効にする必要はありませんが、以下に説明するように、必要に応じて無効にすることができます。

AEM as a Cloud Service 以前は、Dispatcher キャッシュを無効にする方法が 2 通りありました。

1. パブリッシュ Dispatcher のフラッシュエージェントを指定して、レプリケーションエージェントを呼び出す
2. `invalidate.cache` API を直接呼び出す（例：`POST /dispatcher/invalidate.cache`）

Dispatcher の `invalidate.cache` API アプローチは、特定の Dispatcher ノードのみを指すので、今後サポートされなくなります。AEM as a Cloud Service は、個々のノードレベルではなくサービスレベルで動作するので、[AEM からのキャッシュページの無効化](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/configuring/page-invalidate.translate.html)ページで説明されている無効化手順は、AEM as a Cloud Service では無効になります。代わりに、レプリケーションフラッシュエージェントを使用する必要があります。タグの割り当ては、レプリケーション API を使用しておこなえます。レプリケーション API ドキュメントは[ここ](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html)からご利用ください。また、キャッシュをフラッシュする例については、[API 使用例](https://helpx.adobe.com/jp/experience-manager/using/aem64_replication_api.html)および、特に、使用可能なあらゆるエージェントに対して ACTIVATE タイプのレプリケーションアクションを発行する `CustomStep` の例を参照してください。フラッシュエージェントエンドポイントは設定できませんが、フラッシュエージェントを実行するパブリッシュサービスと一致する Dispatcher を指すように事前設定されています。フラッシュエージェントは、通常、OSGi のエージェントまたはイベントによってトリガーされます。

次に図で示します。

![CDN](assets/cdnd.png "CDN")

Dispatcher キャッシュがクリアされない問題が発生した場合は、[カスタマーサポート](https://helpx.adobe.com/support.ec.html)にお問い合わせください。必要に応じて Dispatcher キャッシュをフラッシュします。

アドビが管理する CDN は TTL に従うので、フラッシュする必要はありません。問題の疑いがある場合は、[カスタマーサポート](https://helpx.adobe.com/support.ec.html)にお問い合わせください。必要に応じてアドビが管理する CDN キャッシュをフラッシュします。

## クライアントサイドライブラリとバージョンの整合性 {#content-consistency}

ページは、HTML、JavaScript、CSS、画像で構成されます。JS ライブラリ間の依存関係を考慮して、クライアントサイドライブラリ（clientlibs）フレームワークを活用し、JavaScript および CSS リソースを HTML ページに読み込むことをお勧めします。

clientlibs フレームワークは、自動バージョン管理を提供します。つまり、開発者はソース管理で JS ライブラリに対する変更をチェックインでき、最新バージョンは、顧客がリリースをプッシュしたときに利用可能になります。この機能がないと、開発者は新しいバージョンのライブラリを参照して HTML を手動で変更する必要があります。同じライブラリを共有する HTML テンプレートが多い場合は特に負担がかかります。

新しいバージョンのライブラリが実稼動環境にリリースされると、参照する HTML ページは、更新されたライブラリバージョンへの新しいリンクで更新されます。特定の HTML ページのブラウザーキャッシュの有効期限が切れると、（AEM から）更新されたページが新しいバージョンのライブラリを参照することが保証されるので、古いライブラリがブラウザーキャッシュから読み込まれる心配はありません。更新された HTML ページには、最新のライブラリバージョンがすべて含まれます。

このメカニズムはシリアル化されたハッシュで、クライアントライブラリリンクに追加され、ブラウザーが CSS／JS をキャッシュするための一意のバージョン付き URL を確保します。シリアル化されたハッシュは、クライアントライブラリの内容が変更された場合にのみ更新されます。つまり、新しいデプロイメントでも、関係ない更新（クライアントライブラリの基になる CSS／JS の変更はなし）が発生した場合、参照は同じままになるので、ブラウザーのキャッシュの中断が少なくなります。

### クライアントサイドライブラリの Longcache バージョンの有効化 - AEM as a Cloud Service の SDK クイックスタート {#enabling-longcache}

HTML ページにインクルードされるデフォルトの clientlib は、次の例のようになります。

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

厳密な clientlib のバージョン管理が有効な場合、クライアントライブラリに長期ハッシュキーがセレクターとして追加されます。その結果、clientlib の参照は次のようになります。

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

厳密な clientlib のバージョン管理は、すべての AEM as a Cloud Service 環境で、デフォルトで有効になっています。

ローカル SDK クイックスタートで厳密な clientlib のバージョン管理を有効にするには、次の操作を実行します。

1. OSGi Configuration manager `<host>/system/console/configMgr` へ移動する。
1. Adobe Granite HTML Library Manager の OSGi Config を探します。
   * 「厳密なバージョン管理」チェックボックスをオンにして有効にします。
   * 「長期クライアントサイドキャッシュキー」というラベルの付いたフィールドに、値「/.*;hash」を入力します。
1. 変更内容を保存します。AEM as a Cloud Service は、開発、ステージ、実稼動環境でこの設定を自動的に有効にするので、この設定をソース管理に保存する必要はありません。
1. クライアントライブラリのコンテンツが変更されるたびに、新しいハッシュキーが生成され、HTML 参照が更新されます。
