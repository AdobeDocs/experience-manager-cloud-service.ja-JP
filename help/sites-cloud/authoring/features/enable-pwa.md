---
title: プログレッシブ web アプリケーション機能の有効化
description: AEM Sites では、コンテンツ作成者がコーディングの代わりにシンプルな設定で、任意のサイトに対してプログレッシブ web アプリケーション機能を有効にすることができます。
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1998'
ht-degree: 66%

---

# プログレッシブ web アプリケーション機能の有効化 {#enabling-pwa}

シンプルな設定で、コンテンツ作成者が AEM Sites で作成されたエクスペリエンスに対してプログレッシブ web アプリケーション（PWA）機能を有効化できるようになりました。

>[!CAUTION]
>
>これは高度な機能で、次を必要とします。
>
>* PWA に関する知識
>* サイトとコンテンツ構造に関する知識
>* キャッシュ方法の理解
>* 開発チームによるサポート
>
>この機能を使用する前に、Adobeは開発チームと話し合い、プロジェクトに最適な使用方法を定義することをお勧めします。

## はじめに {#introduction}

[プログレッシブ web アプリケーション（PWA）](https://developer.mozilla.org/ja-JP/docs/Web/Progressive_web_apps)を使用すると、AEM Sites のアプリケーションのような臨場感のあるエクスペリエンスを、ユーザーのコンピューターにローカルに保存し、オフラインでアクセスできるようになります。インターネット接続が切れた場合でも、外出中にサイトを閲覧できます。PWAを使用すると、ネットワークが失われたり不安定な場合でもシームレスなエクスペリエンスを実現できます。

サイトの記録を必要とする代わりに、コンテンツ作成者はPWAのプロパティを [ページのプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md) サイトの

* この設定は、保存または公開時に、トリガーに [マニフェストファイル](https://developer.mozilla.org/ja-JP/docs/Web/Manifest) および [サービスワーカー](https://developer.mozilla.org/ja-JP/docs/Web/API/Service_Worker_API) サイト上でPWA機能を有効にする
* Sling マッピングは、サービスワーカーがアプリケーションのルートから提供されるように維持され、アプリケーション内でオフライン機能を可能にするコンテンツのプロキシ化を有効にします。

PWA では、ユーザーはサイトのローカルコピーを保持するので、インターネットに接続していなくてもアプリケーションのような操作をおこなうことができます。

>[!NOTE]
>
>プログレッシブ web アプリケーションは発展中のテクノロジーであり、ローカルアプリケーションのインストールやその他の機能のサポート状況は[どのブラウザーを使用するかによって異なります。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary)

## 前提条件 {#prerequisites}

サイトで PWA 機能を使用するには、プロジェクト環境に必要な要件が 2 つあります。

1. [コアコンポーネント](#adjust-components)を使用してこの機能を利用する
1. [Dispatcher を調整する](#adjust-dispatcher) 必要なファイルを公開するルール

これらは、作成者が開発チームと連携する必要がある技術的な手順です。 これらの手順は、サイトごとに 1 回だけ必要です。

### コアコンポーネントの使用 {#adjust-components}

コアコンポーネントリリース 2.15.0 以降は、AEM Sites の PWA 機能を完全にサポートしています。AEMaaCS には常に最新バージョンのコアコンポーネントが含まれているので、標準搭載の PWA 機能を使用できます。AEMaaCS プロジェクトは、この要件を自動的に満たします。

>[!NOTE]
>
>アドビは、カスタムコンポーネントまたは[コアコンポーネントから拡張](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja)されていないコンポーネントで PWA 機能を使用することはお勧めしません。
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer adds the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer also adds the following link to the `customfooterlibs.html` file of your page component.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```
-->

### Dispatcher の調整 {#adjust-dispatcher}

PWA 機能は、`/content/<sitename>/manifest.webmanifest` ファイルを生成して使用します。デフォルトでは、 [Dispatcher](/help/implementing/dispatcher/overview.md) では、このようなファイルを公開しません。 これらのファイルを公開するには、デベロッパーはサイトプロジェクトに次の設定を追加する必要があります。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

プロジェクトに応じて、書き換えルールに様々なタイプの拡張機能を含めることができます。 `webmanifest` 拡張は、リクエストを非表示にして `/content/<projectName>` にリダイレクトするルールを導入した場合に、書き換え条件を含めるのに便利です。

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## サイトの PWA の有効化 {#enabling-pwa-for-your-site}

を使用 [前提条件](#prerequisites) を満たした場合、コンテンツ作成者はサイトへのPWA機能を簡単に有効にできます。 次に、その方法の概要を示します。個々のオプションについて詳しくは、の節を参照してください。 [詳細オプション。](#detailed-options)

1. AEM にログインします。
1. メインメニューから、「 」を選択します。 **ナビゲーション** > **Sites**.
1. サイトプロジェクトを選択し、「 」を選択します。 [**プロパティ**](/help/sites-cloud/authoring/fundamentals/page-properties.md) または、ホットキーを使用します。 `p`.
1. 「**プログレッシブ Web アプリケーション**」タブを選択し、該当するプロパティを設定します。少なくとも、次の操作が必要です。
   1. 「**PWA を有効にする**」オプションを選択します。
   1. **スタートアップ URL** を定義します。

      ![PWA を有効にする](../assets/pwa-enable.png)

   1. 512x512 の png アイコンを DAM にアップロードし、それをアプリケーションのアイコンとして参照します。

      ![PWA アイコンの定義](../assets/pwa-icon.png)

   1. サービスワーカーがオフラインにするパスを構成します。 一般的なパスは次のとおりです。
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * サードパーティのフォント参照
      * `/etc/clientlibs/<sitename>`

      ![PWA のオフラインパスの定義](../assets/pwa-offline.png)

1. 「**保存して閉じる**」を選択します。

これでサイトが構成され、[ローカルアプリケーションとしてインストールできます。](#using-pwa-enabled-site)

## PWA 対応サイトの使用 {#using-pwa-enabled-site}

これで、[PWA をサポートするようにサイトを設定できたので、](#enabling-pwa-for-your-site)体験してみてください。

1. のサイトにアクセスする [サポートされているブラウザ](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Tutorials/js13kGames/Installable_PWAs#summary).
1. ブラウザーのアドレスバーに、サイトがローカルアプリとしてインストールできることを示す新しいアイコンが表示されます。
   * ブラウザーによってアイコンは異なり、ローカルアプリケーションとしてインストールできることを示す通知（バナーやダイアログボックスなど）が表示される場合もあります。
1. AEM Desktop App をインストールします。
1. アプリがデバイスのホーム画面にインストールされます。
1. アプリケーションを開いてしばらく作業して、ページがオフラインで使用できることを確認してください。

## 詳細なオプション {#detailed-options}

次の節では、[PWA 用にサイトを設定](#enabling-pwa-for-your-site)する際に使用できるオプションの詳細を説明します。

### インストール可能なエクスペリエンスの設定 {#configure-installable-experience}

これらの設定を使用すると、訪問者のホーム画面にインストールでき、オフラインで使用できるようにすることで、サイトをネイティブアプリのように動作させることができます。

* **「Enable」PWA**  — これは、サイトのPWAを有効にする主な切り替えです。
* **スタートアップ URL**  — これは [優先開始 URL](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/start_url) ユーザーがローカルにインストールされたアプリを読み込むと、デスクトップアプリケーションが開きます。
   * これは、コンテンツ構造内の任意のパスにすることができます。
   * ルートにする必要はなく、多くの場合アプリケーションの開始ページにします。
   * この URL が相対 URL の場合、マニフェスト URL がベース URL として使用され、解決されます。
   * 空のままにすると、アプリがインストールされた Web ページのアドレスが使用されます。
   * 値を設定することをお勧めします。
* **表示モード** - PWA 対応のアプリケーションは、引き続きブラウザーを介して配信される AEM サイトです。[これらの表示オプション](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/display)は、ブラウザーを非表示にする方法や、ローカルデバイス上のユーザーに表示する方法を定義します。
   * **スタンドアロン**  — ブラウザーはユーザーに対して非表示になり、ネイティブアプリのように表示されます。 これがデフォルト値です。
      * このオプションを使用する場合、アプリケーションのナビゲーションは、ブラウザーのナビゲーションコントロールを使用することなく、サイトのページ上のリンクやコンポーネントを使用してコンテンツ全体でナビゲーション可能でなければなりません。
   * **ブラウザー** - ブラウザーは、サイトの訪問時に通常通り表示されます。
   * **最小限の UI** - ネイティブアプリケーションと同様に、ブラウザーはほとんど非表示ですが、基本的なナビゲーションコントロールが表示されます。
   * **全画面表示**  — ブラウザーは、ネイティブアプリと同様に非表示になりますが、フルスクリーンモードでレンダリングされます。
      * このオプションを使用する場合、アプリケーションのナビゲーションは、ブラウザーのナビゲーションコントロールを使用することなく、サイトのページ上のリンクやコンポーネントを使用してコンテンツ全体でナビゲーション可能でなければなりません。
* **画面の向き**  — ローカルアプリケーションは、PWAが [デバイスの向き](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/orientation).
   * **任意** - アプリケーションはユーザーのデバイスの向きに合わせて調整されます。これがデフォルト値です。
   * **縦置き** - ユーザーのデバイスの向きに関係なく、アプリケーションが強制的に縦置きレイアウトで開きます。
   * **横置き** - ユーザーのデバイスの向きに関係なく、アプリケーションが強制的に横置きレイアウトで開きます。
* **テーマの色** - ローカルユーザーのオペレーティングシステムがネイティブの UI ツールバーとナビゲーションコントロールを表示する方法に影響する[アプリケーションの色](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/theme_color)を定義します。ブラウザーによっては、他のアプリケーションプレゼンテーション要素に影響を与える場合があります。
   * カラーウェルポップアップを使用して、色を選択します。
   * 色は、16 進数または RGB 値で定義することもできます。
* **背景色** - アプリの読み込み時に表示される、[アプリの背景色](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/background_color)を定義します。
   * カラーウェルポップアップを使用して、色を選択します。
   * 色は、16 進数または RGB 値で定義することもできます。
   * 特定のブラウザーでは、アプリケーション名、背景色、アイコンから[自動的にスプラッシュスクリーンが作成されます](https://developer.mozilla.org/ja-JP/docs/Web/Manifest#Splash_screens)。
* **アイコン** - ユーザーのデバイス上に表示される、アプリケーションを表す[アイコン](https://developer.mozilla.org/ja-JP/docs/Web/Manifest/icons)を定義します。
   * アイコンは、サイズが 512x512 ピクセルの png ファイルである必要があります。
   * アイコンは [DAM に保存](/help/assets/overview.md)する必要があります。

### キャッシュ管理（詳細） {#offline-configuration}

これらの設定により、このサイトの一部はオフラインで使用できるようになり、訪問者のデバイスでローカルに使用できるようになります。Web アプリケーションのキャッシュを制御してネットワークリクエストを最適化し、オフラインエクスペリエンスをサポートできます。

* **コンテンツ更新のキャッシュ方法と頻度** - この設定は、PWA のキャッシュモデルを定義します。
   * **中程度** - [この設定](https://web.dev/stale-while-revalidate/)は、大半のサイトで使用されます。これがデフォルト値です。
      * この設定を使用すると、ユーザーが最初に閲覧したコンテンツをキャッシュから読み込み、ユーザーがそのコンテンツを利用している間は、キャッシュ内の残りのコンテンツを再検証します。
   * **頻繁**  — オークション会社など、迅速にアップデートを実施する必要があるサイトの場合は、このケースが該当します。
      * この設定を使用すると、アプリは最初にネットワークを介して最新のコンテンツを探し、使用できない場合はローカルキャッシュにフォールバックします。
   * **まれ** - これは、リファレンスページなど、ほとんど静的なサイトの場合に使用します。
      * この設定では、アプリは最初にキャッシュ内のコンテンツを探し、コンテンツが使用できない場合はネットワークにフォールバックして取得します。
* **ファイルの事前キャッシュ** - AEM でホストされるこれらのファイルは、サービスワーカーのインストール時および使用前に、ローカルブラウザーのキャッシュに保存されます。これにより、オフライン時に Web アプリが完全に機能するようになります。
* **パスの包含** - 定義されたパスに対するネットワーク要求が捕捉され、設定された&#x200B;**キャッシュ方法とコンテンツ更新の頻度**&#x200B;に従ってキャッシュされたコンテンツが返されます。
* **キャッシュの除外**  — これらのファイルは、以下の設定に関係なくキャッシュされません。 **ファイルのプリキャッシュ** および **パスを含む**.

>[!TIP]
>
>デベロッパーチームは、オフライン設定の設定方法に関する貴重な情報を得られる可能性が高くなります。

## 制限と Recommendations {#limitations-recommendations}

AEM Sites では PWA 機能の一部が利用できます。これらには、いくつかの顕著な制限があります。

* ユーザーがアプリケーションを使用していない場合、ページは自動的に同期または更新されません。

Adobeを実装する場合は、次のこともお勧めします。PWA

### 事前キャッシュするリソースの数を最小限に抑える。 {#minimize-precache}

アドビでは、事前キャッシュするページ数を制限するよう勧めています。

* ライブラリを埋め込むことで、プリキャッシュ時に管理するエントリ数を減らすことができます。
* 事前キャッシュする画像のバリエーション数を制限します。

### プロジェクトスクリプトとスタイルシートを安定化した後にPWAを有効にします。 {#pwa-stabilized}

クライアントライブラリにはキャッシュセレクタが追加され、`lc-<checksumHash>-lc` のようなパターンで配信されます。ライブラリを構成するファイル（および依存関係）の 1 つが変更されるたびに、このセレクターが変更されます。 サービスワーカーが事前にキャッシュするクライアントライブラリを一覧表示し、新しいバージョンを参照する場合は、手動でエントリを取得して更新します。そのため、Adobeでは、プロジェクトスクリプトとスタイルシートが安定した状態になった後で、サイトをPWAに設定することをお勧めします。

### 画像バリエーションの数を最小限に抑える。 {#minimize-variations}

AEM コアコンポーネントの画像コンポーネントは、取得に最適な、フロントエンドのレンディションを 1 つ決定します。このメカニズムには、そのリソースの最終変更時刻に対応するタイムスタンプも含まれます。このメカニズムにより、PWA の事前キャッシュの設定が複雑になります。

プリキャッシュを設定する場合、ユーザーは取得可能なすべてのパスのバリエーションをリストする必要があります。 これらのバリエーションは、画質や幅などのパラメーターで構成されます。これらのバリエーションの数を、最大 3 つ（小、中、大）に減らすことをお勧めします。 これは、 [画像コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=ja).

慎重に設定しないと、メモリとネットワークの消費が PWA のパフォーマンスに大きな影響を与える可能性があります。また、50 個の画像をプリキャッシュし、1 画像あたり 3 つの幅を持つ場合、サイトを維持するユーザーは、ページプロパティの「PWAプリキャッシュ」セクションで最大 150 個のエントリのリストを維持する必要があります。

また、アドビでは、プロジェクトでの画像の使用が安定してから、サイトを PWA に設定することを勧めています。
