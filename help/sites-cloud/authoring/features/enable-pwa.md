---
title: プログレッシブWebアプリ機能を有効にする
description: AEM Sitesでは、コンテンツ作成者がコーディングの代わりにシンプルな設定で、任意のサイトに対してプログレッシブwebアプリケーション機能を有効にすることができます。
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 071eefa3b6f5e9636ace612e968b6a9627c98550
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 2%

---


# プログレッシブWeb App機能を有効にする{#enabling-pwa}

シンプルな設定で、コンテンツ作成者がAEM Sitesで作成されたエクスペリエンスに対してプログレッシブWebアプリ(PWA)機能を有効にできるようになりました。

>[!CAUTION]
>
>これは、次の高度な機能を必要とします。
>
>* PWAに関する知識
>* サイトとコンテンツ構造に関する知識
>* キャッシュ方法の理解
>* 開発チームによるサポート

>
>
この機能を使用する前に、開発チームに相談して、プロジェクトに最適な方法を定義することをお勧めします。

## 概要 {#introduction}

[プログレッシブWebアプリ(PWA)を](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) 使用すると、AEMサイトのアプリのような体感的なエクスペリエンスを、ユーザーのコンピューターにローカルに保存し、オフラインでアクセスできるようになります。ユーザーは、インターネット接続が切れた場合でも、外出中にサイトを閲覧できます。 PWAを使用すると、ネットワークが失われたり不安定な状態になった場合でも、シームレスなエクスペリエンスを実現できます。

コンテンツ作成者は、サイトの再コーディングを必要とする代わりに、サイトの[ページプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md)の追加タブとしてPWAプロパティを設定できます。

* 保存または公開時に、この設定では、サイト上のPWA機能を有効にする[マニフェストファイル](https://developer.mozilla.org/en-US/docs/Web/Manifest)と[サービスワーカー](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)を書き出すイベントハンドラーをトリガーします。
* マニフェストおよびサービスワーカーは、サイトに適用される[コンテキスト対応構成](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html)に保存されます。 また、アプリ内でオフライン機能を許可するコンテンツのプロキシを有効にするため、サービスワーカーがアプリケーションのルートから提供されるように、Slingマッピングも管理されます。

PWAの場合、ユーザーはサイトのローカルコピーを持ち、インターネットに接続していなくてもアプリのような操作を行うことができます。

>[!NOTE]
>
>プログレッシブWebアプリは進化するテクノロジーであり、ローカルアプリのインストールやその他の機能のサポートをサポートします。[どのブラウザーを使用するかによって異なります。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 前提条件 {#prerequisites}

サイトでPWA機能を使用するには、プロジェクト環境に2つの要件があります。

1. [コンポーネントを調整して、この機能を有効に](#adjust-components) します。
1. [ディスパッチルールを調整して、必要な](#adjust-dispatcher) ファイルを公開します。

これらは、作成者が開発チームと連携する必要がある技術的な手順です。 これらの手順は、サイトごとに1回だけ必要です。

### コンポーネントの調整{#adjust-components}

コンポーネントには、PWA機能をサポートする[マニフェストファイル](https://developer.mozilla.org/en-US/docs/Web/Manifest)と[サービスワーカー](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)を含める必要があります。

これを行うには、開発者はページコンポーネントの`customheaderlibs.html`ファイルに次のリンクを追加する必要があります。

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

また、開発者は、次のリンクをページコンポーネントの`customfooterlibs.html`ファイルに追加する必要があります。

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

>[!NOTE]
>
>[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)の今後のバージョンでは、これらの機能が自動的に含まれる予定です。 ただし、コアコンポーネントの代わりにカスタムコンポーネントを使用する場合は、これらの調整が必要になります。

### ディスパッチャーの調整{#adjust-dispatcher}

PWA機能は、`/content/<sitename>/manifest.webmanifest`ファイルを生成して使用します。 デフォルトでは、[ディスパッチャー](/help/implementing/dispatcher/overview.md)はこのようなファイルを公開しません。 これらのファイルを公開するには、開発者はサイトプロジェクトに次の設定を追加する必要があります。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>[AEMプロジェクトのアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing)の今後のバージョンでは、この設定が含まれる予定です。

## サイトのPWAを有効にする{#enabling-pwa-for-your-site}

[前提条件](#prerequisites)が満たされたので、コンテンツ作成者はサイトへのPWA機能を有効にするのが非常に簡単です。 次に、その方法の基本的な概要を示します。 個々のオプションの詳細は[詳細なオプション](#detailed-options)セクションに説明されています。

1. AEMにログインします。
1. メインメニューで、**ナビゲーション** -> **サイト**&#x200B;をタップまたはクリックします。
1. サイトプロジェクトを選択し、「[**プロパティ**](/help/sites-cloud/authoring/fundamentals/page-properties.md)」をタップまたはクリックするか、ホットキー`p`を使用します。
1. 「**プログレッシブWebアプリ**」タブを選択し、該当するプロパティを設定します。 少なくとも、次のことが必要です。
   1. 「**PWAを有効にする**」を選択します。
   1. **スタートアップURL**&#x200B;を定義します。

      ![PWA を有効にする](../assets/pwa-enable.png)

   1. 512 x 512のpngアイコンをDAMにアップロードし、それをアプリのアイコンとして参照します。

      ![定義PWAアイコン](../assets/pwa-icon.png)

   1. サービスワーカーがオフラインにするパスを構成します。 一般的なパスは次のとおりです。
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任意のサードパーティフォントの参照
      * `/etc/clientlibs/<sitename>`

      ![PWAのオフラインパスの定義](../assets/pwa-offline.png)


1. 「**保存して閉じる**」をタップまたはクリックします。

これでサイトが構成され、[ローカルアプリとしてインストールできます。](#using-pwa-enabled-site)

## PWA対応サイトの使用{#using-pwa-enabled-site}

これで、[PWAをサポートするようにサイトを設定できたので、](#enabling-pwa-for-your-site)体験してみてください。

1. [サポートされているブラウザーでサイトにアクセスします。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. ブラウザーのアドレスバーに`+`アイコンが表示され、サイトがローカルアプリとしてインストールできることが示されます。
   * ブラウザーによっては、ローカルアプリケーションとしてインストールできることを示す通知（バナーやダイアログボックスなど）が表示される場合もあります。
1. AEM Desktop App をインストールします。
1. アプリケーションがデバイスのホーム画面にインストールされます。
1. アプリを開き、少し参照して、ページがオフラインで使用できることを確認します。

## 詳細なオプション{#detailed-options}

次の節では、[PWA用にサイトを設定する際に使用できるオプションの詳細を説明します。](#enabling-pwa-for-your-site)

### インストール可能なエクスペリエンスを構成{#configure-installable-experience}

これらの設定により、訪問者のホーム画面にインストールでき、オフラインで使用できるようにすることで、サイトをネイティブアプリと同じように動作させることができます。

* **PWAを有効にする**  — これは、サイトのPWAを有効にするためのメイントグルです。
* **起動URL**  — これは、ユーザーがローカルにインストールしたアプリを読み込むときに開く、 [推奨される開始](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) URLです。
   * これは、コンテンツ構造内の任意のパスにすることができます。
   * これは、ルートにする必要はなく、多くの場合アプリの専用のようこそページです。
   * このURLが相対URLの場合、マニフェストURLがベースURLとして使用され、解決されます。
   * 空白のままにすると、Webアプリケーションのインストール元のWebページのアドレスが使用されます。
   * 値を設定することをお勧めします。
* **表示モード** -PWA対応のアプリは、引き続きブラウザーを介して配信されるAEMサイトです。[これらの表示](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) オプションは、ブラウザーを非表示にする方法や、ローカルデバイス上のユーザーに表示する方法を定義します。
   * **スタンドアロン**  — ブラウザーはユーザーに完全に隠され、ネイティブアプリケーションのように表示されます。これがデフォルト値です。
      * このオプションを使用する場合、アプリのナビゲーションは、サイトのページ上のリンクとコンポーネントを使用してコンテンツ全体を通じて、ブラウザーのナビゲーションコントロールを使用せずに可能でなければなりません。
   * **ブラウザー**  — ブラウザーは、サイトの訪問時に通常通りに表示されます。
   * **最小限のUI**  — ブラウザーは、ネイティブアプリと同様、ほとんど非表示ですが、基本的なナビゲーションコントロールが表示されます。
   * **フルスクリーン**  — ブラウザーはネイティブアプリケーションと同様に完全に非表示になりますが、フルスクリーンモードでレンダリングされます。
      * このオプションを使用する場合、アプリのナビゲーションは、サイトのページ上のリンクとコンポーネントを使用してコンテンツ全体を通じて、ブラウザーのナビゲーションコントロールを使用せずに可能でなければなりません。
* **画面の向き**  — ローカルアプリケーションとして、PWAは [デバイスの向きを処理する方法を知っている必要があります。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **任意**  — アプリはユーザーのデバイスの向きに合わせて調整されます。これがデフォルト値です。
   * **縦置き**  — ユーザーのデバイスの向きに関係なく、アプリが強制的に縦置きレイアウトで開きます。
   * **横置き**  — ユーザーのデバイスの向きに関係なく、アプリが強制的に横置きレイアウトで開きます。
* **テーマの色**  — ローカルユーザーのオペレーティングシステムがネイティブのUIツールバーとナビゲーションコントロールを表示する方法に影響する [アプリの](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 色を定義します。ブラウザーによっては、他のアプリプレゼンテーション要素に影響を与える場合があります。
   * カラーウェルポップアップを使用して、色を選択します。
   * 色は、16進数またはRGB値で定義することもできます。
* **背景色**  — アプリの読み込み時に表示され [る、アプリの](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 背景色を定義します。
   * カラーウェルポップアップを使用して、色を選択します。
   * 色は、16進数またはRGB値で定義することもできます。
   * 特定のブラウザー[では、アプリ名、背景色、アイコンから自動的にスプラッシュスクリーン](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)が作成されます。
* **アイコン**  — ユーザー [のデバイス上](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) にあるアプリを表すアイコンを定義します。
   * アイコンは、サイズが512 x 512ピクセルのpngファイルである必要があります。
   * アイコンはDAMに[保存されている必要があります。](/help/assets/overview.md)

### キャッシュ管理（詳細） {#offline-configuration}

これらの設定により、このサイトの一部はオフラインで使用でき、訪問者のデバイス上でローカルに使用できます。 これにより、Webアプリのキャッシュを制御して、ネットワークリクエストを最適化し、オフラインエクスペリエンスをサポートします。

* **コンテンツ更新のキャッシュ方法と頻度**  — この設定は、PWAのキャッシュモデルを定義します。
   * **そこそ** - [この](https://web.dev/stale-while-revalidate/) 設定は、ほとんどのサイトで使用されます。これがデフォルト値です。
      * この設定を使用すると、ユーザーが最初に閲覧したコンテンツがキャッシュから読み込まれ、ユーザーがそのコンテンツを消費している間は、キャッシュ内の残りのコンテンツが再検証されます。
   * **頻繁に**  — これは、オークション会社など、更新を非常に速く必要とするサイトの場合です。
      * この設定を使用すると、アプリは最初にネットワーク経由で最新のコンテンツを探し、使用できない場合はローカルキャッシュに戻ります。
   * **めったに**  — これは、リファレンスページなど、ほとんど静的なサイトの場合に該当します。
      * この設定を使用すると、アプリは最初にキャッシュ内のコンテンツを探し、利用できない場合はネットワークにフォールバックして取得します。
* **ファイルの事前キャッシュ** - AEMでホストされているこれらのファイルは、サービスワーカーのインストール時および使用前に、ローカルブラウザーのキャッシュに保存されます。これにより、オフライン時にWebアプリケーションが完全に機能することが保証されます。
* **パスの包含**  — 定義されたパスに対するネットワーク要求は傍受され、キャッシュされたコンテンツは、設定された **キャッシュ方法とコンテンツ更新の頻度に従って返されます**。
* **キャッシュの除外**  — これらのファイルは、「 **ファイルのキャッシュ前および** パスの挿入」の設定に関係なくキャッシュされません ****。

>[!TIP]
>
>開発者チームは、オフライン設定の設定方法に関する貴重な情報を得られる可能性が高くなります。

## 制限事項 {#limitations}

AEM Sitesでは、PWA機能の一部が利用できるわけではありません。 これらには、いくつかの顕著な制限があります。

* ユーザーは、少なくとも1回ページを参照してから、オフラインでキャッシュする必要があります。
* ユーザーがアプリを使用していない場合、ページは自動的に同期または更新されません。
