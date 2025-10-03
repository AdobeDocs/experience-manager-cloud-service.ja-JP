---
title: AEM as a Cloud Serviceのコンテキスト実験
description: 実験プラグインを使用して、サイトに実験機能を追加する方法を説明します。
feature: Administering
role: Admin
source-git-commit: 66ee08babae1f6640158260af051f8ad5f9bde85
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 0%

---

# AEM as a Cloud Serviceのコンテキスト実験 {#contextual-experimentation}

>[!NOTE]
>現在、コンテキスト実験機能は、ベータ版プログラムでのみ使用できます。 ベータ版プログラムへのアクセスについては、Adobe サポートまたは担当のアカウントマネージャーにお問い合わせください。

実験とは、パフォーマンスを向上させ、サイトをより効果的かつ合理化するために、サイトのデザイン、機能、コードをテストする手法です。 これを実現するには、コンテンツまたは機能を変更し、結果を以前のバージョンと比較し、測定可能な効果がある改善を選択します。

正しく完了すると、コンバージョン、エンゲージメント、訪問者エクスペリエンスを向上させる強力なパターンになります。 一般的に、この手法の採用を検討する際に避けるべき問題がいくつかあります。

* **少なすぎる**：ほとんどの企業は十分な実験を行っていませんが、行った場合、有意義な結果を得るには少なすぎるトラフィックを実験します。
* **速度が遅すぎる**：多くの実験フレームワークでは、サイトの速度が非常に低下し、レンダリングが遅いため、失われたトラフィックとバウンスを新しいコンバージョンで補うことはできません。
* **複雑すぎます**：新しい実験の設定に時間がかかりすぎる場合は、実行される実験の数が少なくなります。

Adobe Experience Managerで動作するサイトの場合は、開発者がサイトに実験機能を追加できる、「標準 **** 実験プラグイン」があります。 このアプローチは、他の実験フレームワークとは次の 3 つの点で異なります。

* 作成者が既に熟知しているツールを使用すると、テストを簡単に設定でき、別のログインは必要ありません。
* これはAEM配信システムに深く統合されており、サイトの速度を低下させず、コードおよびコンテンツの変更に対して回復力があります。
* シンプルなコンテンツ変更や、デザイン、機能、コードをカバーする実験をテストできます。

## 開始する前に {#before-start}

実験プラグインは [Edge Delivery Servicesのコンテキスト内で使用されるので ](/help/edge/overview.md)Github アカウント、SharePointやGoogle Drive などのコンテンツリポジトリおよび [2}AEM Sidekick} が必要です。 ](https://www.aem.live/docs/sidekick)[ はじめに – ユニバーサルエディター開発者チュートリアルページ ](https://www.aem.live/developer/tutorial) および [ はじめに – 開発者チュートリアル ](https://www.aem.live/developer/tutorial) も参照してください。

すべての設定が完了したら **このビデオをご覧ください**[ インスタント実験 ](https://business.adobe.com/products/experience-manager/sites/testing-optimization.html) と題して、実験プラグインの仕組みを示す短いデモを行います。

## よく使用される用語 {#frequently-used-terms}

ガイドの残りの部分に従って最初の実験を設定する前に、よく使用する用語をいくつか理解しておく必要があります。

* **コントロール**：実験を実行する前のエクスペリエンス。 すべての実験は、制御エクスペリエンスの向上をテストし実証しようとします。
* **チャレンジャー**：コントロールエクスペリエンスとは異なるエクスペリエンスで、それに対して、または同時に「テスト」されます。
* **バリアント**：コントロールとチャレンジャーは、すべて実験のバリアントです。
* **統計的有意性**：挑戦者がコントロールよりも本当に優れているかどうかを評価します。 統計的有意差を計算すると、運を除外し、実際の効果がある結果に集中することができます。

## 実験のバリエーションと一般的なワークフロー {#experiment-variants-workflow}

一般的に、実験を設定する場合、既存のページをコントロールページとして使用します。 次に、一部の訪問者のコントロールページを置き換えるチャレンジャーページを作成します。 挑戦者ページでは、コンテンツのバリエーション、ページレイアウト、call-to-action（CTA）など、様々なものをテストできます。 コントロールページにメタデータパラメーターを追加することで、これらの実験バリアントを設定できます（以下を参照）。

次に、[ 運用上のテレメトリサービス ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) がデータを収集します。例えば、コントロールページとチャレンジャーページの訪問者数が収集されます。 その後、このデータを使用して、サイトに必要な改善点を選択します。 確立された web サイトのデザイン言語を使用し、既存のブロック機能を使用する限り、実験バリアントを設定して、数分で実稼動環境に送信できます。

>[!NOTE]
>プラグインは、エンドユーザーの識別につながる可能性のあるエンドユーザーのデータを使用せず、保持もしないことに注意してください。 AEM as a Cloud Serviceの [ 運用上のテレメトリサービス ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) を使用するデフォルト設定を使用する場合、エンドユーザーのオプトインや Cookie の同意は必要ありません。

### 実験識別子 {#experiment-identifier}

開始する前に、トラッキングと分析を目的とした独自の識別子をすべての実験に指定する必要があります。 良い出発点は、実験の優れた一意の ID を見つけることです。これは「実験 ID」になります。 実験は、多くの場合、イシュートラッカーまたは管理システムで、イシュー ID に対して線形番号または相関しています。 実験 ID には多くの場合、プロジェクトのプレフィックス（`OPT-0134`、`EXP0004`、`CCX0076` など）を使用します。

### チャレンジャーページの作成 {#create-challenger-page}

慣例により、`/experiments/ folder` ールに小文字の実験 ID （例：/experiments/ccx0076/）を含むフォルダーを作成することをお勧めします。 チャレンジャーのバリエーションのページはすべて、このフォルダーにあります。 このフォルダーは、ローカルリポジトリ（SharePoint や Goggle Drive など）に作成します。

実験フォルダーは次のようになります。

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

フォルダーを作成したら、そのフォルダーにコントロールページのコピーを配置し、実験バリアントの一部としてテストするページに変更を適用します（上記のビデオを参照）。 例として、実験を実行する web サイトに次のページがあるとします。

![control-page](/help/sites-cloud/administering/assets/control-page.png)

`experiments/<experiment-id>` フォルダーに配置された挑戦者のコピーは次のようになります。

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

サイドキックを使用して、挑戦者ページのオーサリングが完了したら、挑戦者ページをプレビューして公開します。 公開されたチャレンジャーの URL は、次の節の実験の設定で使用されます。

### 実験の設定 {#configure-experiment}

チャレンジャーページの準備が整ったら、すぐにコントロールページに戻り、ページがテストに含まれていることを示すメタデータを追加する必要があります。

実験バリアントには、追加する必要があるメタデータ行が 2 つあります。

* **実験**：実験 ID を含みます。

* **実験のバリアント**：このページのすべての挑戦者の URL を含みます。複数の挑戦者がいる場合は改行で区切ります。

以下の例を参照してください。

![ メタデータページ ](/help/sites-cloud/administering/assets/metadata-page.png)

実験ごとに、トラフィックはすべてのバリアント（コントロールチャレンジャーとチャレンジャー）に分割され、自動的に偶数分布に設定されます。 したがって、1 人の挑戦者がいる場合、自動的に制御と挑戦者の間で 50/50 の均等な分割が行われます。 2 人の挑戦者がいる場合は、制御に割り当てられたトラフィックの 3 分の 1 が自動的に表示され、各挑戦者などが表示されます。

メタデータを設定することで、トラフィックの分割を上書きできます。 実験で使用されるメタデータをカスタマイズする方法について詳しくは、次の [ ページ ](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring) を参照してください。

### 実験のバリアントのプレビューとステージング {#preview-stage-experiment}

実験をプレビューしてステージングする準備が整ったら、左上のサイドキックから「プレビュー」をクリックします。 実験が実行されているページをプレビューする場合は常に、`.aem.page` のプレビュー環境に実験のオーバーレイが表示されます。 実験オーバーレイを使用すると、実験のバリエーションを切り替えることができ、トラフィックデータも提供できます。

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

各バリアントの効果を測定するためのデータ収集は、[AEM as a Cloud Serviceでの運用上のテレメトリサービス ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) に基づいています。

### 実験バリアントを実稼動環境に送信 {#production-experiment}

実験ページを選択し、サイドキックから「公開」をクリックして、コントロールと挑戦者バリアントの両方をライブにプッシュします。

### ユースケースの例 {#use-case-examples}

実験のバリアントのユースケースの例をいくつか以下に示します。 一般的に、基本的なワークフローは上記のワークフローと似ていますが、ユースケースごとに特定の変更（挑戦者ページの数やメタデータの変更など）が行われます。

#### 完全ページの実験 {#full-page}

完全なページ実験を使用して、同じページの 2 つのバリアントをテストします。 これは、コントロールと挑戦者ページを持つ a/b テストの完全なページバリアントです。 チャレンジャーバリアントの「オリジナル」コントロールページのコンテンツ全体を別のタイプのコンテンツに置き換えます。 デフォルトでは顧客トラフィックは均等に分割（50/50）されていますが、必要に応じてカスタム分割を作成できます。

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## その他の注意点 {#other-considerations}

コンテキスト実験を使用する際に考慮すべきその他の側面を以下に示します。

### コンバージョン {#conversion}

実験は、コンバージョンに対処するように設定されます（ページ上のクリック可能な要素を追跡します）。 すべての実験は、次の目的で定義する必要があります。

* 実験タイプ
* 実験が適用されるエクスペリエンスブロック
* 実験に含まれるバリアントの数
* 各バリアントの構成

### 実験バリアントのインデックスが作成されていないことを確認します {#experiment-not-indexed}

実験を実行する場合、通常は、サイトマップからバリアントを除外し、検索エンジンでインデックスが作成されないようにします。 これは、バリアントページが重複したコンテンツと見なされ、SEO に悪影響を与える可能性があるためです。

これを行うには、次の 2 つの方法のいずれかを使用します。

* `/experiments` のように、すべての実験を専用フォルダーに一元化する場合は、一括 `metadata.xlsx` シートに `/experiments/**` をパスとする行と、`noindex`、`nofollow` という値を持つロボット列が含まれていることを確認します。
* 実験のコントロールとバリアントの値を通常のコンテンツのままにする場合：各バリアントのページメタデータに、値 `noindex`、`nofollow` を指定してロボットのエントリを追加します。

## 開発者向けリソースとテクニカルリソース {#dev-resources}

Adobe Experience Managerは [ 運用上のテレメトリ ] （/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md

）、Adobe Experience Managerを利用したサイトで機能とパフォーマンスの問題を検出および修正するために不可欠なオペレーションデータを収集します。 運用上のテレメトリデータを使用して、パフォーマンスの問題を診断できます。 運用テレメトリでは、サンプリングを通じて訪問者のプライバシーを保持します（すべてのページビューのごく一部のみが監視されます）。

### プライバシー {#privacy-experimentation}

[AEM as a Cloud Serviceの運用上のテレメトリサービス ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) は、訪問者のプライバシーを保護し、データ収集を最小限に抑えるように設計されています。 つまり、Adobeは、お客様の個人情報や、お客様に遡って追跡できる情報の収集を試みません。 サイトオペレーターは、以下に収集したデータ項目を確認し、同意が必要かどうかを把握します。
AEM Operational Telemetry では、使用状況指標を収集するために、cookie や `localStorage`、`sessionStorage` など、クライアントサイドのステートや ID を使用しません。 データは、ピクセルや同様の手法ではなく、`Navigator.sendBeacon` 呼び出しを通じて透過的に送信されます。 サンプリングされたデータを取得する目的で、IP アドレス、ユーザーエージェント文字列、その他のデータを介したデバイスや個人の「フィンガープリント」は行われません。

運用上のテレメトリデータ収集に個人データを追加することは許可されておらず、また、運用上のテレメトリデータは、厳密に必要な範囲を超えるユースケースに使用することもできません。

### よくある質問 {#faq}

よくある質問のリストを以下に示します。

Q：実験のバリエーション間の分割率（例えば、コントロールで 10%、挑戦者で 90%）を調整することはできますか？

はい、分割率は [ メタデータ ](#configure-experiment) で設定できます。

Q：テキストと画像の両方を試すことはできますか？

はい、バリアントは完全に異なるページになる可能性があるので、レイアウトの変更をテストすることもできます。
