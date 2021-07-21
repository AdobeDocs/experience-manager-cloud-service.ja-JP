---
title: Dynamic Media ViewersとAdobe AnalyticsおよびExperience Platformタグの統合
description: Experience PlatformタグおよびDynamic Mediaビューア5.13のDynamic Mediaビューア拡張機能について説明します。Adobe Analyticsおよびプラットフォームタグのお客様は、Experience Platformタグ設定でDynamic Mediaビューア固有のイベントとデータを使用できます。
feature: アセットレポート
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: 13dbce0d8ad25fec47460a41c5ea3e355a4dd486
workflow-type: tm+mt
source-wordcount: '6681'
ht-degree: 58%

---

# Dynamic Media ViewersとAdobe AnalyticsおよびExperience Platformタグの統合 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Adobe AnalyticsおよびExperience PlatformタグとのDynamic Media Viewersの統合とは {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

*Dynamic Media* ViewerExtension for Experience Tags and Dynamic Media Viewers 5.13を使用すると、Adobe AnalyticsおよびExperience Platformタグのお客様は、Experience Platformタグ設定でDynamic Mediaビューア固有のイベントとデータを使用できます。

この統合により、Adobe Analytics を使用して、Web サイト上での Dynamic Media ビューアの使用状況を追跡できます。同時に、Adobeやサードパーティ製のその他のExperience Platformタグ拡張機能を持つビューアによって公開されたイベントやデータを使用できます。

Adobe拡張機能またはサードパーティ拡張機能について詳しくは、『Experience Platformタグユーザーガイド』の「[Adobe拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html)」を参照してください。

**このトピックは、** サイト管理者、Adobe Experience Manager プログラムでのデベロッパー、および運用担当者を対象としています。

### 統合の制限 {#limitations-of-the-integration}

* Dynamic MediaビューアのExperience Platformタグ統合は、Experience Manager作成者ノードでは機能しません。 公開されるまで、WCM ページからのトラッキングを表示することはできません。
* Dynamic MediaビューアのExperience Platformタグ統合は、「ポップアップ」操作モードではサポートされていません。このモードでは、ビューアのURLは、アセットの詳細ページの「URL」ボタンを使用して取得されます。
* Experience Platformタグの統合は、（`config2=`パラメーターを介して）従来のビューアAnalytics統合とは同時に使用することはできません。
* ビデオトラッキングのサポートは、[トラッキングの概要](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html?lang=ja#player-events)で説明されているように、コア再生トラッキングのみに制限されます。具体的には、QoS、広告、チャプター／セグメント、エラーのトラッキングはサポートされていません。
* データ要素のストレージデュレーション設定は、*Dynamic Media ビューア*&#x200B;拡張機能を使用したデータ要素ではサポートされません。ストレージデュレーションは **[!UICONTROL None]** に設定する必要があります。

### 統合の事例 {#use-cases-for-the-integration}

Experience Platformタグとの統合の主な使用例は、Experience ManagerアセットとExperience Managerサイトの両方を使用するお客様です。 このようなシナリオでは、Experience ManagerオーサーノードとExperience Platformタグの間の標準的な統合を設定し、Sitesインスタンスを「Experience Platformタグ」プロパティに関連付けることができます。 その後、Site ページに追加された Dynamic Media WCM コンポーネントは、ビューアのデータとイベントを追跡します。

[Experience ManagerサイトでのDynamic Mediaビューアの追跡](#tracking-dynamic-media-viewers-in-aem-sites)を参照してください。

統合の 2 番目の事例は、Experience Manager Assets のみ、または Dynamic Media Classic を使用する顧客です。その場合、ビューアの埋め込みコードを取得して、Web サイトページに追加します。次に、Experience PlatformタグからExperience Platformタグライブラリ実稼動用URLを取得し、Webページのコードに手動で追加します。

[埋め込みコード](#tracking-dynamic-media-viewers-using-embed-code)を使用したDynamic Mediaビューアの追跡を参照してください。

## 統合でのデータとイベントのトラッキングの仕組み {#how-data-and-event-tracking-works-in-the-integration}

この統合では、*Adobe Analytics* と *Adobe Analytics for Audio and Video* という、2 種類の独立したタイプの Dynamic Media ビューアのトラッキングを利用します。

### Adobe Analytics を使用したトラッキングについて   {#about-tracking-using-adobe-analytics}

Adobe Analytics を使用すると、エンドユーザーが Web サイト上で Dynamic Media ビューアとやり取りしたときに実行したアクションを追跡できます。また、Adobe Analytics では、ビューア固有のデータも追跡できます。例えば、ビューの読み込みイベントを、アセット名や、発生したズーム操作、ビデオ再生操作などと共に追跡して記録できます。

Experience Platformタグでは、*データ要素*&#x200B;と&#x200B;*ルール*&#x200B;の概念が連携して、Adobe Analyticsトラッキングを有効にします。

#### データタグのデータ要素についてExperience Platform {#about-data-elements-in-adobe-launch}

Experience Platformタグ内のデータ要素は、名前の付いたプロパティです。このプロパティの値は、静的に定義されるか、Webページの状態やDynamic Mediaビューアのデータに基づいて動的に計算されます。

データ要素の定義で使用できるオプションは、Experience Platformタグプロパティにインストールされる拡張機能のリストによって異なります。 「コア」拡張機能はプレインストールされており、どのような設定でもすぐに使用できます。この「コア」拡張機能を使用すると、cookie、JavaScript コード、クエリ文字列、その他多くのソースから取得した値を持つデータ要素を定義できます。

Adobe Analytics でトラッキングをおこなう場合は、[拡張機能のインストールとセットアップ](#installing-and-setup-of-extensions)で説明されているように、他にいくつか拡張機能をインストールする必要があります。Dynamic Media ビューア拡張機能には、Dynamic Viewer イベントの引数である値のデータ要素を定義する機能が追加されています。例えば、ビューアのタイプや、読み込み時にビューアから報告されるアセット名、エンドユーザーがズームしたときに報告されるズームレベルなどを参照できます。

Dynamic Media ビューア拡張機能は、データ要素の値を自動的に最新の状態に保ちます。

定義したデータ要素は、データ要素ピッカーウィジェットを使用して、他のExperience PlatformタグUIで使用できます。 特に、Dynamic Media ビューアのトラッキングを目的として定義されたデータ要素は、ルール内の Adobe Analytics 拡張機能の変数設定アクションで参照されます（以下を参照）。

『タグユーザガイド』の「[データ要素](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html)」を参照してください。

#### タグタグのルールについてExperience Platform {#about-rules-in-adobe-launch}

Experience Platformタグのルールは、ルールを構成する次の3つの領域を定義する非依存型の設定です。*イベント*、*条件*、*アクション*:

* *イベント* (if)は、Experience Platformタグにルールをトリガーするタイミングを伝えます。
* *条件* (if)は、Experience Platformタグに、ルールのトリガー時に許可または禁止する他の制限を通知します。
* *アクション* (then)は、Experience Platformタグに、ルールがトリガーされた場合の処理を伝えます。

「イベント、条件、アクション」セクションで使用できるオプションは、Experience Platformタグプロパティにインストールされている拡張機能によって異なります。 *コア*&#x200B;拡張機能はプレインストールされており、どのような設定でもすぐに使用できます。この拡張機能では、イベントについては、フォーカスの変更、キーの押下、フォームの送信といった、基本的なブラウザーレベルのアクションなどのオプションがいくつか用意されています。また、条件についても、cookie の値、ブラウザータイプなどのオプションが用意されています。アクションについては、カスタムコードオプションのみ使用できます。

Adobe Analytics でトラッキングをおこなう場合は、[拡張機能のインストールとセットアップ](#installing-and-setup-of-extensions)で説明されているように、他にいくつか拡張機能をインストールする必要があります。具体的には以下のとおりです。

* Dynamic Media ビューア拡張機能は、サポートされるイベントのリストを、ビューアの読み込み、アセットの入れ替え、ズームイン、ビデオ再生など、Dynamic Media ビューアに固有のイベントに拡張します。
* Adobe Analytics 拡張機能は、サポートされるアクションのリストを拡張し、データをトラッキングサーバーに送信するために必要な、*変数設定*&#x200B;と&#x200B;*ビーコン送信*&#x200B;という 2 つのアクションが用意されています。

Dynamic Media ビューアを追跡するには、次のいずれかを使用できます。

* Dynamic Media ビューア拡張機能、コア拡張機能またはその他の拡張機能からのイベント。
* ルール定義の条件。または、条件領域を空のままにすることもできます。

アクションセクションでは、*変数設定*&#x200B;アクションが必要です。このアクションは、Adobe Analytics にデータを使用してトラッキング変数を設定する方法を知らせます。同時に、*変数設定*&#x200B;アクションは、トラッキングサーバーに何も送信しません。

*変数設定*&#x200B;アクションに続けて、*ビーコン送信*&#x200B;アクションを使用する必要があります。*ビーコン送信*&#x200B;アクションは、実際に Analytics トラッキングサーバーにデータを送信します。*変数設定*&#x200B;と&#x200B;*ビーコン送信*&#x200B;アクションは、いずれも Adobe Analytics 拡張機能から得られます。

『Experience Platformタグユーザガイド』の「[ルール](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html)」を参照してください。

#### サンプル設定 {#sample-configuration}

以下のタグタグ内のサンプルExperience Platformで、ビューアの読み込み時にアセット名を追跡する方法を示します。

1. 「**[!UICONTROL データ要素]**」タブで、Dynamic Media ビューア拡張機能から `LOAD` イベントの `asset` パラメーターを参照するデータ要素 `AssetName` を定義します。

   ![image2019-11](assets/image2019-11.png)

1. 「**[!UICONTROL ルール]**」タブで、ルール *TrackAssetOnLoad* を定義します。

   このルールでは、「**[!UICONTROL イベント]**」フィールドは、Dynamic Media ビューア拡張機能の **[!UICONTROL LOAD]** イベントを使用します。

   ![image2019-22](assets/image2019-22.png)

1. アクション設定には、Adobe Analytics 拡張機能の 2 つのアクションタイプがあります。

   *変数設定*&#x200B;は、選択した分析変数を `AssetName` データ要素の値にマップします。

   *ビーコン送信*&#x200B;は、Adobe Analytics にトラッキング情報を送信します。

   ![image2019-3](assets/image2019-3.png)

1. ルール設定結果は次のようになります。

   ![image2019-4](assets/image2019-4.png)

### Adobe Analytics for Audio and Video について {#about-adobe-analytics-for-audio-and-video}

Experience Cloud アカウントが Adobe Analytics for Audio and Video を使用するよう登録されている場合、*Dynamic Media ビューア*&#x200B;拡張機能の設定でビデオのトラッキングを有効にするだけで十分です。ビデオ指標が Adobe Analytics で使用できるようになります。ビデオトラッキングは、Adobe Media Analytics for Audio and Video 拡張機能の有無に依存します。

詳しくは、[拡張機能のインストールとセットアップ](#installing-and-setup-of-extensions)を参照してください。

現在、ビデオトラッキングのサポートは、[トラッキングの概要](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html#player-events)で説明されているように、「コア再生」トラッキングのみに制限されます。具体的には、QoS、広告、チャプター／セグメント、エラーのトラッキングはサポートされていません。

## Dynamic Media Viewers拡張機能の使用 {#using-the-dynamic-media-viewers-extension}

[統合の使用例](#use-cases-for-the-integration)で説明したように、Experience Managerサイトで新しいExperience Platformタグ統合を使用し、埋め込みコードを使用してDynamic Mediaビューアを追跡できます。

### Experience ManagerサイトでのDynamic Mediaビューアの追跡 {#tracking-dynamic-media-viewers-in-aem-sites}

Experience ManagerサイトでDynamic Mediaビューアを追跡するには、 [すべての統合ピースの設定](#configuring-all-the-integration-pieces)の節に示す手順をすべて実行する必要があります。 特に、IMS設定とタグクラウド設定をExperience Platformする必要があります。

適切な設定に従い、Dynamic Media でサポートされる WCM コンポーネントを使用して Sites ページに追加した Dynamic Media ビューアは、Adobe Analytics、Adobe Analytics for Video、またはその両方のデータを自動的に追跡します。

[Adobeサイトを使用したページへのDynamic Media Assetsの追加](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)を参照してください。

### 埋め込みコードを使用したDynamic Mediaビューアの追跡 {#tracking-dynamic-media-viewers-using-embed-code}

Experience Managerサイトを使用しない、またはDynamic MediaビューアをExperience Managerサイト以外のWebページに埋め込む、またはその両方をお使いのお客様は、Experience Platformタグ統合を引き続き使用できます。

[Adobe Analytics](#configuring-adobe-analytics-for-the-integration)の設定および[Experience Platformタグ](#configuring-adobe-launch-for-the-integration)の設定の手順を実行します。 ただし、Experience Manager 関連の設定手順は不要です。

適切な設定を行ったら、Dynamic Mediaビューアを使用してWebページにExperience Platformタグのサポートを追加できます。

Experience Platformタグライブラリの埋め込みコードの使用方法について詳しくは、 [Experience Platformタグの埋め込みコードの追加](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=ja#configure-launch)を参照してください。

Dynamic MediaExperience Managerの埋め込みコード機能の使用方法について詳しくは、[Webページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/dynamic-media/embed-code.md)を参照してください。

**埋め込みコードを使用してDynamic Mediaビューアを追跡するには：**

1. Dynamic Media ビューアを埋め込む Web ページを準備します。
1. 最初にExperience Platformタグにログインして、Experience Platformタグライブラリの埋め込みコードを取得します([Experience Platformタグの設定](#configuring-adobe-launch-for-the-integration)を参照)。
1. **[!UICONTROL プロパティ]**&#x200B;を選択し、「**[!UICONTROL 環境]**」タブを選択します。
1. Web ページの環境に関連する環境レベルを取得します。次に、「****&#x200B;をインストール」列で、ボックスのアイコンを選択します。
1. **[!UICONTROL Web Install Instructionsダイアログボ]** ックスで、Experience Platformタグライブラリの埋め込みコード全体と、それを囲むタグをコピー `<script/>` します。

## Dynamic Media ビューア拡張機能リファレンスガイド {#reference-guide-for-the-dynamic-media-viewers-extension}

### Dynamic Media ビューアの設定について {#about-the-dynamic-media-viewers-configuration}

次の条件を満たす場合、Dynamic Media Viewer拡張機能はExperience Platformタグライブラリと自動的に統合されます。

* Experience Platformタグライブラリのグローバルオブジェクト(`_satellite`)がページに存在します。
* Dynamic Media ビューア拡張機能の `_dmviewers_v001()` 関数が、`_satellite` で定義されている。

* `config2=` ビューアパラメーターが指定されていない。つまり、ビューアが従来の Analytics 統合を使用していない。

また、ビューアの設定で`launch=0`パラメーターを指定して、ビューアでExperience Platformタグの統合を明示的に無効にするオプションもあります。 このパラメーターのデフォルト値は `1` です。

### Dynamic Media Viewers拡張機能の設定 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media ビューア拡張機能の唯一の設定オプションは、**[!UICONTROL Adobe Media Analytics for Audio and Video を有効にする]**&#x200B;です。

このオプションを選択する（有効にする）と、Adobe Media Analytics for Audio and Video 拡張機能がインストールおよび設定され、ビデオ再生指標は Adobe Analytics for Audio and Video ソリューションに送信されます。このオプションを無効にすると、ビデオトラッキングがオフになります。

Adobe Media Analytics for Audio and Video 拡張機能をインストール&#x200B;*せずに*&#x200B;このオプションを有効にしても、このオプションは無効です。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Dynamic Media ビューア拡張機能のデータ要素について {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media ビューア拡張機能で提供されるデータ要素タイプは、「**[!UICONTROL データ要素タイプ]**」ドロップダウンリストの&#x200B;**[!UICONTROL ビューアイベント]**&#x200B;のみです。

選択すると、データ要素エディターは、次の 2 つのフィールドを含むフォームをレンダリングします。

* **[!UICONTROL DM ビューアイベントデータタイプ]** - 引数を持つ Dynamic Media ビューア拡張機能でサポートされるすべてのビューアイベントと、特別な **[!UICONTROL COMMON]** 項目を識別するドロップダウンリスト。**[!UICONTROL COMMON]** 項目は、ビューアから送信されるすべてのタイプのイベントに共通するイベントパラメーターのリストを表します。
* **[!UICONTROL トラッキングパラメーター-]** - 選択した Dynamic Media ビューアイベントの引数。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

各ビューアタイプでサポートされるイベントのリストについては、 [Dynamic Mediaビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html?lang=ja)を参照してください。特定のビューアセクションに移動し、「 Adobe Analyticsトラッキングのサポート」サブセクションを選択します。 現在、Dynamic Media ビューアリファレンスガイドでは、イベントの引数について説明していません。

次に、Dynamic Media ビューアの&#x200B;*データ要素*&#x200B;のライフサイクルを考えてみましょう。このようなデータ要素の値は、対応する Dynamic Media ビューアイベントがページで発生した後に設定されます。例えば、データ要素が **[!UICONTROL LOAD]** イベントとその「asset」引数を指しているとします。このようなデータ要素の値は、ビューアが初めて LOAD イベントを実行した後に有効なデータを受け取ります。データ要素が **[!UICONTROL ZOOM]** イベントとその「scale」引数を指している場合、このようなデータ要素の値は、ビューアが初めて **[!UICONTROL ZOOM]** イベントを送信するまで空のままです。

同様に、ビューアがページ上の対応するイベントを送信すると、データ要素の値は自動的に更新されます。値の更新は、特定のイベントがルール設定で指定されていない場合でもおこなわれます。例えば、ZOOM イベントの「scale」パラメーターにデータ要素 **[!UICONTROL ZoomScale]** が定義されているとします。ただし、ルール設定に存在する唯一のルールは、**[!UICONTROL LOAD]** イベントによってトリガーされます。**[!UICONTROL ZoomScale]** の値は、ユーザーがビューア内でズームを実行するたびに更新されます。

Dynamic Media ビューアは Web ページ上で一意の識別子を持ちます。データ要素は、値自体と、値が入力されたビューアを追跡します。例えば、同じページに複数のビューアがあり、**[!UICONTROL LOAD]** イベントとその「asset」引数を指す **[!UICONTROL AssetName]** データ要素があるとします。**[!UICONTROL AssetName]** データ要素は、ページに読み込まれた各ビューアに関連付けられたアセット名のコレクションを保持します。

データ要素から返される正確な値は、コンテキストによって異なります。Dynamic Media ビューアイベントによってトリガーされたルール内でデータ要素が要求された場合、ルールを開始したビューアに対してデータ要素の値が返されます。また、データ要素は、他のイベントタグ拡張機能からイベントによってトリガーされたルール内でExperience Platformされます。 この時点で、データ要素の値は、このデータ要素を最後に更新したビューアから取得されます。

**次の設定例を考えてみましょう**。

* 2 つの Dynamic Media ズームビューアを持つ Web ページ：*viewer1* および *viewer2*。

* **[!UICONTROL ZoomScale]** データ要素は、**[!UICONTROL ZOOM]** イベントとその「scale」引数を指します。
* **[!UICONTROL TrackPan]** ルールには、次の情報が含まれます。

   * Dynamic Media ビューアの **[!UICONTROL PAN]** イベントをトリガーとして使用。
   * **[!UICONTROL ZoomScale]** データ要素の値を Adobe Analytics に送信。

* **[!UICONTROL TrackKey]** ルールには、次の情報が含まれます。

   * CoreExperience Platformタグ拡張のkey pressイベントをトリガーとして使用します。
   * **[!UICONTROL ZoomScale]** データ要素の値を Adobe Analytics に送信。

ここで、エンドユーザーが 2 つのビューアで Web ページを読み込んだとします。*viewer1* では 50％の拡大率でズームインし、次に、*viewer2* では 25％の拡大率でズームインします。*viewer1* では、画像がパンされ、最後にキーボードのキーが押されます。

エンドユーザーのアクティビティによって、Adobe Analytics に対して次の 2 つのトラッキングコールが実行されます。

* 最初の呼び出しは、ユーザーが *viewer1* でパンしたときに **[!UICONTROL TrackPan]** ルールがトリガーされることから発生します。この呼び出しでは、ルールが *viewer1* によってトリガーされたことをデータ要素が認識し、対応するスケール値が取得されるので、**[!UICONTROL ZoomScale]** データ要素の値として 50％が送信されます。
* 2 回目の呼び出しは、ユーザーがキーボードのキーを押したときに **[!UICONTROL TrackKey]** ルールがトリガーされるので発生します。ルールをトリガーしたのがビューアでなかったので、この呼び出しでは **[!UICONTROL ZoomScale]** データ要素の値として 25％が送信されます。このようにして、データ要素は最新の値を返します。

上記のサンプル設定は、データ要素の値の寿命にも影響します。Dynamic Media Viewerで管理されるデータ要素の値は、ビューア自体がWebページに配置された後でも、Experience Platformタグライブラリコードに保存されます。 つまり、Dynamic Media 以外のビューアの拡張によってトリガーされるルールがあり、そのようなデータ要素を参照する場合、データ要素は最後に認識された値を返します。これには、ビューアが Web ページに存在しなくなった場合も含みます。

いずれの場合も、Dynamic Mediaビューアによって駆動されるデータ要素の値は、ローカルストレージやサーバーには保存されません。代わりに、クライアント側のタグライブラリにのみExperience Platformされます。 Web ページがリロードされると、このようなデータ要素の値は消去されます。

一般に、データ要素エディターでは、[ストレージ期間の選択](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html?lang=en#create-a-data-element)がサポートされます。ただし、Dynamic Media ビューア拡張機能を使用するデータ要素では、ストレージ期間「**[!UICONTROL なし]**」オプションのみがサポートされます。その他の値はユーザーインターフェイスで設定可能ですが、この場合、データ要素の動作は定義されていません。拡張機能は、データ要素の値を独自に管理します。データ要素は、ビューアのライフサイクル全体でビューアのイベント引数の値を維持します。

### Dynamic Media ビューア拡張機能のルールについて {#about-rules-in-the-dynamic-media-viewers-extension}

ルールエディターで、イベントエディターの新しい設定オプションが追加されます。また、エディターには、事前に設定されたデータ要素を使用する代わりに、アクションエディターでイベントパラメーターを手動で参照する簡略オプションも用意されています。

#### イベントエディターについて {#about-the-events-editor}

Dynamic Media ビューア拡張機能によって、イベントエディターで&#x200B;**[!UICONTROL ビューアイベント]**&#x200B;と呼ばれる&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;が追加されます。

選択すると、イベントエディターによって「**[!UICONTROL Dynamic Media ビューアイベント]**」ドロップダウンがレンダリングされ、Dynamic Media ビューアでサポートされる使用可能なイベントがすべて表示されます。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### アクションエディターについて {#about-the-actions-editor}

Dynamic Media ビューア拡張機能を使用すると、Dynamic Media ビューアのイベントパラメーターを使用して、Adobe Analytics 拡張機能の変数設定エディターで分析変数にマッピングできます。

最も簡単な方法は、次の 2 つの手順を実行することです。

* まず、1 つ以上のデータ要素を定義します。各データ要素は、Dynamic Media ビューアイベントのパラメーターを表します。
* 最後に、 Adobe Analytics拡張機能の変数設定エディターで、データ要素ピッカーアイコン（3つの積み重ねディスク）を選択してデータ要素を選択ダイアログボックスを開き、そこからデータ要素を選択します。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

ただし、別の方法を使用して、データ要素の作成をスキップすることは可能です。引数は、Dynamic Media ビューアイベントから直接参照できます。Analytics 変数の割り当ての「**[!UICONTROL 値]**」入力フィールドに、イベント引数の完全修飾名を入力します。パーセント記号（%）で囲んでください。例：

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

データ要素を使用する場合と、直接イベント引数の参照を使用する場合では、重要な違いがあることに注意してください。データ要素の場合、「変数を設定」トリガーがどのイベントに属していてもかまいません。ルールをトリガーするイベントは、動的ビューアとは関係ない場合があります（Core拡張機能からWebページを選択する場合など）。 ただし、直接引数参照を使用する場合は、ルールをトリガーするイベントが、参照するイベント引数に対応していることを確認することが重要です。

例えば、`%event.detail.dm.LOAD.asset%` の参照は、ルールが Dynamic Media ビューア拡張機能の **[!UICONTROL LOAD]** イベントによってトリガーされる場合、正しいアセット名を返します。ただし、他のイベントの場合は空の値を返します。

次の表に、Dynamic Media ビューアイベントと、サポートされている引数を示します。

<table>
 <tbody>
  <tr>
   <td>ビューアのイベント名</td>
   <td>引数の参照</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## すべての統合ピースの設定 {#configuring-all-the-integration-pieces}

**始める前に**

アドビでは、この節の前にドキュメントを十分に見直し、統合について完全に理解することをお勧めします。

ここでは、Dynamic Media ビューアを Adobe Analytics および Adobe Analytics for Audio and video と統合するために必要な設定手順について説明します。Dynamic Mediaビューア拡張機能は、Experience Platformタグで他の目的で使用する可能性がありますが、このドキュメントでは扱いません。

次のアドビ製品を使用して統合を設定します。

* Adobe Analytics - トラッキング変数とレポートを設定します。
* Experience Platformタグ — ビューアトラッキングを有効にするプロパティ、1つ以上のルールおよび1つ以上のデータ要素を定義するために使用します。

また、この統合ソリューションを Experience Manager Sites で使用する場合は、次の設定をおこなう必要があります。

* Adobe I/Oコンソール — 統合はタグタグ用にExperience Platformされます。
* Experience Manager作成者ノード — IMS設定およびExperience Platformタグクラウド設定

設定の一環として、Adobe AnalyticsタグとExperience Platformタグが既に有効になっているAdobe Experience Cloudの会社にアクセスできることを確認してください。

## 統合のためのAdobe Analyticsの設定 {#configuring-adobe-analytics-for-the-integration}

Adobe Analytics を設定した後、統合のために次の設定がおこなわれます。

* レポートスイートが配置され、選択される。
* Analytics 変数がトラッキングデータを受け取るために使用可能になる。
* Adobe Analytics 内で収集されたデータを表示するレポートが使用可能になる。

[Analytics 導入ガイド](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)も参照してください。

**統合のために Adobe Analytics を設定するには**：

1. まず、Experience Cloud [ホームページ](https://experience.adobe.com/#/home)から Adobe Analytics にアクセスします。メニューバーで、ページの右上隅付近にあるソリューションアイコン（3 x 3のドットテーブル）を選択し、「**[!UICONTROL Analytics]**」を選択します。

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   次に、レポートスイートを選択します。

### レポートスイートの選択 {#selecting-a-report-suite}

1. Adobe Analytics ページの右上隅近くの「**[!UICONTROL レポートの検索]**」フィールドの右側にあるドロップダウンリストから、適切なレポートスイートを選択します。複数のレポートスイートが使用可能で、どれを使用するか不明な場合は、Adobe Analytics 管理者が使用するレポートスイートを選択するのに役立ちます。

   下の図では、ユーザーが *DynamicMediaViewersExtensionDoc* という名前のレポートスイートを作成し、ドロップダウンリストから選択しています。レポートスイート名は一例です。最終的に選択するレポートスイート名は、ユーザーが決定できます。

   使用できるレポートスイートがない場合は、設定を続行する前に、ユーザーまたは Adobe Analytics 管理者がレポートスイートを作成する必要があります。

   [レポートとレポートスイート](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html?lang=ja#manage-report-suites)および[レポートスイートの作成](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=ja#manage-report-suites)を参照してください。

   Adobe Analyticsでは、**[!UICONTROL 管理者]** / **[!UICONTROL レポートスイート]**&#x200B;でレポートスイートを管理します。

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   次に、Adobe Analytics 変数を設定します。

### Adobe Analytics変数の設定 {#setting-up-adobe-analytics-variables}

1. Web ページ上の Dynamic Media ビューアの動作を追跡するために使用する、1 つ以上の Adobe Analytics 変数を指定します。

   Adobe Analytics でサポートされている任意のタイプの変数を使用できます。変数のタイプ（カスタムトラフィック [prop] や、コンバージョン [eVar] など）は、Adobe Analytics 実装の具体的なニーズに応じて決めます。

   [prop と eVar の概要](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=ja#vars)を参照してください。

   このドキュメントでは、カスタムトラフィック（prop）変数のみを使用します。これは、Web ページでアクションが発生した場合、数分以内に Analytics のレポートで使用できるようになるためです。

   新しいカスタムトラフィック変数を有効にするには、Adobe Analyticsのツールバーで、**[!UICONTROL 管理者]** / **[!UICONTROL レポートスイート]**&#x200B;に移動します。

1. **[!UICONTROL Report Suite Manager]**&#x200B;ページで正しいレポートを選択し、ツールバーで&#x200B;**[!UICONTROL 設定を編集]** / **[!UICONTROL トラフィック]** / **[!UICONTROL トラフィック変数]**&#x200B;に移動します。
1. 未使用の変数を選択し、わかりやすい名前を付け（**[!UICONTROL ビューアアセット（prop 30）]**）、「有効」列のコンボボックスを「有効」に変更します。

   次のスクリーンショットは、ビューアが使用するアセット名を追跡するためのカスタムトラフィック変数（**[!UICONTROL prop30]**）の例です。

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. 変数リストの下部で、「**[!UICONTROL 保存]**」を選択します。

### レポートの設定 {#setting-up-a-report}

1. 一般に、Adobe Analytics でのレポートの設定は、特定のプロジェクトのニーズに左右されます。したがって、詳細なレポート設定は、この統合の範囲外です。

   ただし、**[Adobe Analytics変数](#setting-up-adobe-analytics-variables)**&#x200B;のセットアップでカスタムトラフィック変数を設定すると、カスタムトラフィックレポートがAdobe Analyticsで自動的に使用可能になることがわかります。

   例えば、**[!UICONTROL ビューアアセット(prop 30)]**&#x200B;変数のレポートは、**[!UICONTROL カスタムトラフィック]**/**[!UICONTROL カスタムトラフィック21-30]**/**[!UICONTROL ビューアアセット(prop 30)]**&#x200B;のレポートメニューから使用できます。

   **[!UICONTROL ビューアアセット（prop 30）]**&#x200B;を作成した直後にこのレポートを表示すると、データが表示されません。これは、統合のこの時点で予想されることです。

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## 統合のExperience Platformタグの設定 {#configuring-adobe-launch-for-the-integration}

Experience Platformタグを設定した後、統合に対して次の設定がおこなわれます。

* すべての設定をまとめるための新しいプロパティの作成。
* 拡張機能のインストールとセットアップ。プロパティにインストールされたすべての拡張機能のクライアント側コードは、1 つのライブラリにまとめられる。このライブラリは後で Web ページで使用されます。
* データ要素とルールの設定。この設定は、Dynamic Media ビューアから取得するデータ、トラッキングロジックをトリガーするタイミング、Adobe Analytics でビューアのデータを送信する場所を定義するものです。
* ライブラリの公開。

**統合のExperience Platformタグを設定するには：**

1. まず、Experience Cloud[ホームページ](https://experience.adobe.com/#/home)からExperience Platformタグにアクセスします。 メニューバーで、ページの右上隅付近にあるソリューションアイコン（3 x 3のドットテーブル）を選択し、「**[!UICONTROL タグ]**」を選択します。

   [Experience Platformタグを直接開くこともできます](https://launch.adobe.com/)。

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### タグでのプロパティのExperience Platform {#creating-a-property-in-adobe-launch}

Experience Platformタグのプロパティは、すべての設定をまとめた名前付き設定です。 構成設定のライブラリが様々な環境レベル（開発、ステージングおよび実稼動）で生成され、公開されます。

[タグプロパティ](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-mobile-android-apps-with-launch/configure-launch/launch-create-a-property.html?lang=ja#configure-launch)の作成も参照してください。

**タグタグでプロパティをExperience Platformするには：**

1. 「Experience Platformタグ」で、「**[!UICONTROL 新しいプロパティ]**」を選択します。
1. **[!UICONTROL プロパティを作成]**&#x200B;ダイアログボックスの「**[!UICONTROL 名前]**」フィールドに、Web サイトのタイトルなど、わかりやすい名前を入力します。例：`DynamicMediaViewersProp.`
1. 「**[!UICONTROL ドメイン]**」フィールドに、Web サイトのドメインを入力します。
1. 使用したい拡張機能（この場合は *Dynamic Media ビューア*）がまだリリースされていない場合に備えて、「**[!UICONTROL 詳細オプション]**」ドロップダウンで、**[!UICONTROL 拡張機能の開発用に設定（後で変更できません）]**&#x200B;を有効にします。

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 「**[!UICONTROL 保存]**」を選択します。

   新しく作成されたプロパティを選択し、「*拡張機能のインストールと設定*」に進みます。

### 拡張機能のインストールとセットアップ {#installing-and-setup-of-extensions}

Experience Platformタグで使用可能な拡張機能は、すべて&#x200B;**[!UICONTROL 拡張機能]** > **[!UICONTROL カタログ]**&#x200B;の下に一覧表示されます。

拡張機能をインストールするには、「****&#x200B;をインストール」を選択します。 必要に応じて、1回限りの拡張設定を実行し、「**[!UICONTROL 保存]**」を選択します。

必要に応じて、次の拡張機能をインストールし、設定する必要があります。

* （必須）*Experience Cloud ID サービス*&#x200B;拡張機能

追加の設定は必要ありません。提案されたあらゆる値を受け入れます。完了したら、必ず「**[!UICONTROL 保存]**」を選択します。

[Experience CloudIDサービス拡張](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html)を参照してください。

* （必須）*Adobe Analytics*&#x200B;拡張機能

この拡張機能を設定するには、Adobe Analyticsの&#x200B;**[!UICONTROL 管理者]** / **[!UICONTROL レポートスイート]**&#x200B;の下にある、**[!UICONTROL レポートスイートID]**&#x200B;列ヘッダーにあるレポートスイートIDが必要です。

（以下のスクリーンショットでは、デモ目的のために、**[!UICONTROL DynamicMediaViewersExtensionDoc]** レポートスイートのレポートスイート ID を使用しています。この ID は、以前の[レポートスイートの選択](#selecting-a-report-suite)で作成および使用されていました）

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

拡張機能のインストールページで、「**[!UICONTROL 開発レポートスイート]**」フィールド、「**[!UICONTROL ステージングレポートスイート]**」フィールド、「**[!UICONTROL 実稼動レポートスイート]**」フィールドに、レポートスイート ID を入力します。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*ビデオトラッキングを使用する予定の場合のみ、次の項目を設定します。*

**[!UICONTROL 拡張機能のインストール]**&#x200B;ページで、「**[!UICONTROL 一般]**」を展開し、「トラッキングサーバー」を指定します。トラッキングサーバーはテンプレート `<trackingNamespace>.sc.omtrdc.net` に従います。`<trackingNamespace>` は、プロビジョニング電子メールで取得した情報です。

「**[!UICONTROL 保存]**」を選択します。

詳しくは、[Adobe Analytics 拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)を参照してください。

* （オプション。ビデオトラッキングが必要な場合のみ必須）*Adobe Media Analytics for Audio and Video* 拡張機能

「トラッキングサーバー」フィールドに入力します。*Adobe Media Analytics for Audio and Video* 拡張機能のトラッキングサーバーは、Adobe Analytics で使用されるトラッキングサーバーとは異なります。これはテンプレート `<trackingNamespace>.hb.omtrdc.net` に従います。`<trackingNamespace>` は、プロビジョニング電子メールの情報です。

その他のフィールドはオプションです。

[Analytics for Audio and Video拡張機能](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)を参照してください。

* （必須）*Dynamic Media ビューア*&#x200B;拡張機能

**[!UICONTROL Adobe Analytics for Video を有効にする]**&#x200B;を選択して、ビデオハートビートトラッキングを有効（オン）にします。

このドキュメントの記述時点で、*Dynamic Mediaビューア*&#x200B;拡張機能は、開発用にExperience Platformタグプロパティが作成されている場合にのみ使用できます。

[Experience Platformタグ](#creating-a-property-in-adobe-launch)でプロパティを作成するを参照してください。

拡張機能のインストールと設定が完了すると、少なくとも次の 5 つの拡張機能（ビデオをトラッキングしていない場合は 4 つ）が拡張機能／インストール領域に表示されます。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### データ要素とルールの設定 {#setting-up-data-elements-and-rules}

Experience Platformタグで、Dynamic Mediaビューアの追跡に必要なデータ要素とルールを作成します。

Experience Platformタグを使用したトラッキングの概要については、[統合でのデータとイベントのトラッキングの仕組み](#how-data-and-event-tracking-works-in-the-integration)を参照してください。

ビューアの読み込み時にExperience Platform名を追跡する方法を示すアセットタグのサンプル設定については、 [サンプル設定](#sample-configuration)を参照してください。

拡張機能の機能について詳しくは、 [Dynamic Mediaビューア拡張機能の設定](#configuring-the-dynamic-media-viewers-extension)を参照してください。

### ライブラリの公開 {#publishing-a-library}

Experience Platformタグの設定（プロパティ、拡張機能、ルール、データ要素の設定を含む）を変更するには、*公開*&#x200B;する必要があります。 Experience Platformタグでの公開は、プロパティ設定の「公開」タブから実行します。

Experience Platformタグには、複数の開発環境、1つのステージング環境、1つの実稼動環境を含めることができます。 デフォルトでは、Experience ManagerのExperience Platformタグクラウド設定は、Experience Managerオーサーノードをプラットフォームタグのステージ環境に指定します。 Experience Managerの公開ノードが、タグの実稼動環境を指している。 これは、デフォルトのExperience Manager設定では、Experience Platformタグライブラリをステージング環境に公開する必要があることを意味します。 これにより、ライブラリを Experience Manager オーサーで使用できるようになります。その後、実稼動環境に公開することで、Experience Manager のパブリッシュで使用できるようになります。

タグ環境について詳しくは、[Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html)を参照してください。

ライブラリの公開には、次の 2 つの手順を実行します。

* 必要な変更（新しい変更や更新）をすべてライブラリに含めて、新しいライブラリを追加して構築。
* 様々な環境レベルを通じてライブラリを移動（開発からステージングおよび実稼動へ）。

#### 新しいライブラリの追加とビルド {#adding-and-building-a-new-library}

1. 初めて「公開」タブをExperience Platformタグで開くと、ライブラリリストは空になります。

   左側の列で、「**[!UICONTROL 新しいライブラリを追加]**」を選択します。

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 新しいライブラリを作成ページの「**[!UICONTROL 名前]**」フィールドに、新しいライブラリのわかりやすい名前を入力します。例：

   *DynamicMediaViewersLib*

   「環境」ドロップダウンリストから、環境レベルを選択します。最初は、選択できるのは開発レベルのみです。ページの左下近くにある「**[!UICONTROL 変更されたすべてのリソースを追加]**」を選択します。

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. ページの右上隅付近にある「**[!UICONTROL 開発用に保存してビルド]**」を選択します。

   数分でライブラリが作成され、使用できる状態になります。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >次回Experience Platformタグの設定を変更する際に、**[!UICONTROL プロパティ]**&#x200B;設定の下の「**[!UICONTROL 公開]**」タブに移動し、以前に作成したライブラリを選択します。
   >
   >
   >ライブラリの公開画面で、「**[!UICONTROL 変更されたすべてのリソースを追加]**」を選択し、「**[!UICONTROL 開発用に保存してビルド]**」を選択します。

#### 環境レベルでのライブラリの上への移動 {#moving-a-library-up-through-environment-levels}

1. 新しいライブラリが追加されると、そのライブラリはまず開発環境に表れます。これをステージング環境レベル（「送信済み」列に対応）に移動するには、ライブラリのドロップダウンメニューから「**[!UICONTROL 承認用に送信]**」を選択します。

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 確認ダイアログボックスで、「**[!UICONTROL 送信]**」を選択します。

   ライブラリが「送信済み」列に移動したら、ライブラリのドロップダウンメニューから、「**[!UICONTROL ステージング用にビルド]**」を選択します。

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. ステージング環境から実稼動環境（「発行済み」列）にライブラリを移動するには、同様のプロセスに従います。

   まず、ドロップダウンメニューから「**[!UICONTROL 公開の承認]**」を選択します。

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. ドロップダウンメニューから、「**[!UICONTROL ビルドして実稼動環境に公開]**」を選択します。

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Experience Platformタグでの公開プロセスについて詳しくは、[公開](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)を参照してください。

## 統合のためのAdobe Experience Managerの設定 {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

前提条件：

* Experience Manager は、オーサーインスタンスとパブリッシュインスタンスの両方を実行します。
* Experience Manager オーサーノードは Dynamic Media で設定されます。<!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM コンポーネントは Experience Manager Sites で有効になっています。

Experience Manager 設定は、次の 2 つの主な手順で構成されます。

* Experience Manager IMS の設定。
* Experience Platformタグクラウドの設定

### Experience ManagerIMSの設定 {#configuring-aem-ims}

1. Experience Managerオーサーで、ツールアイコン（ハンマー）を選択し、**[!UICONTROL セキュリティ]** /**[!UICONTROL AdobeIMS設定]**&#x200B;に移動します。

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. AdobeIMC設定ページの左上隅付近で、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL AdobeIMSテクニカルアカウント設定]**&#x200B;ページの「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで、「**[!UICONTROL Experience Platformデータ収集]**」を選択します。
1. 「**[!UICONTROL 新しい証明書を作成]**」を有効にし、テキストフィールドに証明書に意味のある値を入力します。例えば、*AdobeLaunchIMSCert* と入力します。「**[!UICONTROL 証明書を作成]**」を選択します。

   次の情報メッセージが表示されます。

   *有効なアクセストークンを取得するには、新しい証明書の公開鍵を Adobe I/O のテクニカルアカウントに追加する必要があります*

   [情報]ダイアログボックスを閉じるには、[**[!UICONTROL OK]**]を選択します。

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 「 **[!UICONTROL 公開鍵をダウンロード]** 」を選択して、公開鍵ファイル(`*.crt`)をローカルシステムにダウンロードします。

   >[!NOTE]
   >
   >この時点で、******&#x200B;を開いたまま&#x200B;**[!UICONTROL AdobeIMSテクニカルアカウント設定]**&#x200B;ページを開きます。***ページを閉じない***&#x200B;で、***閉じない***&#x200B;で「**[!UICONTROL 次へ]**」を選択します。 このページには、手順の後半で戻ってきます。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 新しいブラウザータブで、[Adobe I/O コンソール](https://console.adobe.io/integrations)に移動します。

1. **[!UICONTROL Adobe I/Oコンソールの統合]**&#x200B;ページの右上隅付近で、「**[!UICONTROL 新しい統合]**」を選択します。
1. **[!UICONTROL 新しい統合を作成]**&#x200B;ダイアログボックスで、「**[!UICONTROL API]**&#x200B;にアクセス」ラジオボタンが選択されていることを確認し、「**[!UICONTROL 続行]**」を選択します。

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 2つ目の&#x200B;**[!UICONTROL 新しい統合を作成]**&#x200B;ページで、「**[!UICONTROL Experience PlatformタグAPI]**」ラジオボタンを有効（オン）にします。 ページの右下隅にある「**[!UICONTROL 続行]**」を選択します。

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. **[!UICONTROL 統合の新規作成]**&#x200B;の 3 ページ目で、次の操作をおこないます。

   * 「**[!UICONTROL 名前]**」フィールドにわかりやすい名前を入力します。例えば、*DynamicMediaViewersIO* と入力します。

   * 「**[!UICONTROL 説明]**」フィールドに、統合の説明を入力します。

   * 「**[!UICONTROL 公開鍵証明書]**」領域に、この手順で以前にダウンロードした公開鍵ファイル（`*.crt`）をアップロードします。

   * 「Experience PlatformタグAPI ]**の役割を選択」の見出しの下で、「**[!UICONTROL &#x200B;管理者&#x200B;]**」を選択します。**[!UICONTROL 

   * 「**[!UICONTROL Experience PlatformタグAPI]**&#x200B;用の1つ以上の製品プロファイルを選択」の見出しの下で、「**[!UICONTROL Tags - &lt;your_company_name>]**」という名前の製品プロファイルを選択します。

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 「**[!UICONTROL 統合を作成]**」を選択します。
1. **[!UICONTROL 作成された統合]**&#x200B;ページで、「**[!UICONTROL 統合の詳細を続行]**」を選択します。

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 次のような統合の詳細ページが表示されます。

   >[!NOTE]
   >
   >***この統合の詳細ページは開いたままにします***。「**[!UICONTROL 概要]**」タブと「**[!UICONTROL JWT]**」タブの様々な情報がすぐに必要になります。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   _統合の詳細ページ_

1. 前に開いておいた **[!UICONTROL Adobe IMS テクニカルアカウント設定]**&#x200B;ページに戻ります。ページの右上隅にある「**[!UICONTROL 次へ]**」を選択して、**[!UICONTROL AdobeIMSテクニカルアカウント設定]**&#x200B;ウィンドウで&#x200B;**[!UICONTROL アカウント]**&#x200B;ページを開きます。

   (前にページを閉じた場合は、Experience Manager作成者に戻り、**[!UICONTROL ツール]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL AdobeIMS設定]**&#x200B;に移動します。 「**[!UICONTROL 作成]**」を選択します。「**[!UICONTROL クラウドソリューション]**」ドロップダウンリストで、「**[!UICONTROL Experience Platformタグ]**」を選択します。 「**[!UICONTROL 証明書]**」ドロップダウンリストで、以前に作成した証明書の名前を選択します。

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   _Adobe IMS テクニカルアカウント設定 - 証明書ページ_

1. **[!UICONTROL アカウント]**&#x200B;ページには 5 つのフィールドがあり、前の手順の統合詳細ページの情報を使って入力する必要があります。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   _Adobe IMS テクニカルアカウント設定 - アカウントページ_

1. **[!UICONTROL アカウント]**&#x200B;ページで以下のフィールドに入力します。

   * **[!UICONTROL タイトル]** - 説明的なアカウントのタイトルを入力します。
   * **[!UICONTROL 認証サーバー]** - 以前に開いた統合の詳細ページに戻ります。「**[!UICONTROL JWT]**」タブを選択します。 次に示すように、サーバー名（パスなし）をコピーします。

（サーバー名の例は説明用です）   **[!UICONTROL アカウント]**ページに戻り、その名前を各フィールドに貼り付けます。
例：`https://ims-na1.adobelogin.com/`（サーバー名の例は説明用です）。

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   _統合の詳細ページ - 「JWT」タブ_

1. **[!UICONTROL API キー]** - 統合の詳細ページに戻ります。「**[!UICONTROL 概要]**」タブを選択し、「**[!UICONTROL APIキー（クライアントID）]**」フィールドの右側にある「**[!UICONTROL コピー]**」を選択します。

   **[!UICONTROL アカウント]**&#x200B;ページに戻り、キーを各フィールドに貼り付けます。

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   _統合の詳細ページ_

1. **[!UICONTROL クライアントシークレット]** - 統合の詳細ページに戻ります。「**[!UICONTROL 概要]**」タブで、「**[!UICONTROL クライアントシークレットを取得]**」を選択します。 「**[!UICONTROL クライアントシークレット]**」フィールドの右側で、「**[!UICONTROL コピー]**」を選択します。

   **[!UICONTROL アカウント]**&#x200B;ページに戻り、キーを各フィールドに貼り付けます。

1. **[!UICONTROL ペイロード]** - 統合の詳細ページに戻ります。「**[!UICONTROL JWT]**」タブの「JWT ペイロード」フィールドで、JSON オブジェクトコード全体をコピーします。

   **[!UICONTROL アカウント]**&#x200B;ページに戻り、コードを各フィールドに貼り付けます。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   _統合の詳細ページ - 「JWT」タブ_

   すべてのフィールドに値が入力されたアカウントページは、次のようになります。

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. **[!UICONTROL アカウント]**&#x200B;ページの右上隅近くにある「**[!UICONTROL 作成]**」を選択します。

   Experience Manager IMS が設定され、**[!UICONTROL Adobe IMS 設定]**&#x200B;に新しい IMS アカウントが表示されます。

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 統合用のExperience Platformタグクラウドの設定 {#configuring-adobe-launch-cloud-for-the-integration}

1. Experience Manager作成者の左上隅付近にあるツールアイコン（ハンマー）を選択し、**[!UICONTROL Cloud Services]** / **[!UICONTROL Experience Platformタグ設定]**&#x200B;に移動します。

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. **[!UICONTROL Experience Platformタグ設定]**&#x200B;ページの左側のパネルで、Experience Platformタグ設定を適用するExperience Managerサイトを選択します。

   サンプル目的でのみ、以下のスクリーンショットで&#x200B;**`We.Retail`**&#x200B;サイトが選択されています。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. ページの左上隅付近にある「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL Experience Platformタグ設定を作成]**&#x200B;ウィンドウの&#x200B;**[!UICONTROL 一般]**&#x200B;ページ（1/3ページ）で、次のフィールドに入力します。

   * **[!UICONTROL タイトル]** - 説明的な設定のタイトルを入力します。例： `We.Retail Tags cloud configuration`

   * **[!UICONTROL 関連するAdobeのIMS設定]**  -Experience ManagerのIMSの設定で作成したIMS設定を [選択します](#configuring-aem-ims)。

   * **[!UICONTROL 会社]** - 「**[!UICONTROL 会社]**」ドロップダウンリストから、Experience Cloud の会社を選択します。リストが自動的に入力されます。

   * **[!UICONTROL プロパティ]**  - 「プロパティ」ドロップダウンリストから、以前に作成したExperience Platformタグプロパティを選択します。リストが自動的に入力されます。
   すべてのフィールドに入力すると、**[!UICONTROL 一般]**&#x200B;ページは次のようになります。

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 左上隅付近で、「**[!UICONTROL 次へ]**」を選択します。
1. **[!UICONTROL Experience Platformタグ設定を作成]**&#x200B;ウィンドウの&#x200B;**[!UICONTROL ステージング]**&#x200B;ページ（2/3ページ）で、次のフィールドに入力します。

   「**[!UICONTROL Experience PlatformURI]**(Uniform Resource Identifier)」フィールドで、ライブラリタグライブラリのステージングバージョンの場所を確認します。 Experience Manager によってこのフィールドに自動的に入力されます。

   説明のために、この手順では、Experience PlatformCDNにデプロイされるAdobeタグライブラリを使用します。

   >[!NOTE]
   >
   >自動入力されたライブラリ URI（Uniform Resource Identifier）の形式に誤りがないか確認します。必要に応じて、URI がプロトコル相対 URI を表すように修正します。つまり、ダブルスラッシュから始まります。
   >
   >
   >例：`//assets.adobetm.com/launch-xxxx`

   **[!UICONTROL ステージング]**&#x200B;ページは次のようになります。「**[!UICONTROL アーカイブ]**」オプションと「**[!UICONTROL ライブラリを非同期にロード]**」オプションは設定されて&#x200B;***いません***。

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 右上隅付近にある「**[!UICONTROL 次へ]**」を選択します。
1. **[!UICONTROL Experience Platformタグ設定を作成]**&#x200B;ウィンドウの&#x200B;**[!UICONTROL 実稼動]**&#x200B;ページ（3/3ページ）で、必要に応じて、前の&#x200B;**[!UICONTROL ステージング]**&#x200B;ページでおこなったのと同様に、自動入力された実稼動URIを修正します。
1. 右上隅付近にある「**[!UICONTROL 作成]**」を選択します。

   これで、新しいExperience Platformタグクラウド設定が作成され、Webサイトの横に表示されます。

1. 新しいExperience Platformタグクラウド設定を選択します（設定タイトルを選択すると、設定タイトルの左側にチェックマークが表示されます）。 ツールバーで、「**[!UICONTROL 公開]**」を選択します。

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

現在、Experience Manager作成者は、Dynamic MediaビューアとExperience Platformタグの統合をサポートしていません。

ただし、Experience Manager パブリッシュノードではサポートされています。Experience Platformタグクラウド設定のデフォルト設定を使用して、Experience Manager公開は、Experience Platformタグの実稼動環境を使用します。 そのため、テスト中は毎回、Experience Platformタグライブラリの更新を開発環境から実稼動環境にプッシュする必要があります。

この制限は回避することは可能です。上記のExperience Platform公開用のExperience Platformタグクラウド設定で、Experience Managerタグライブラリの開発URLまたはステージングURLを指定します。 これにより、Experience Managerパブリッシュノードは、開発またはステージングバージョンのExperience Platformタグライブラリを使用します。

Experience Platformタグクラウドの設定について詳しくは、[Experience PlatformタグとExperience Managerの統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=ja#integrations)を参照してください。
