---
title: AEM as a Cloud Serviceのコンテキスト実験
description: 実験プラグインを使用して、サイトに実験機能を追加する方法を説明します。
feature: Administering
role: Admin
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
exl-id: 420f8d5e-27f9-4081-b174-b2d7752779f7
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# AEM as a Cloud Serviceのコンテキスト実験 {#contextual-experimentation}

>[!NOTE]
>現在、コンテキスト実験機能はベータプログラムを通じてのみ使用できます。 ベータプログラムへのアクセスについては、Adobe サポートまたはアカウントマネージャーにお問い合わせください。

テストとは、パフォーマンスを向上させ、サイトをより効果的かつ合理的にするために、サイトのデザイン、機能、コードをテストすることです。 これは、コンテンツや機能を変更し、結果を以前のバージョンと比較し、測定可能な効果をもたらす改善点を選ぶことで達成できます。

正しく行われれば、コンバージョン、エンゲージメント、訪問者エクスペリエンスを向上させるための強力なパターンになります。 一般的に、この手法を採用する際には避けるべき問題がいくつかあります。

* **少なすぎます**：多くの企業は十分な実験を行っておらず、十分な実験を行うと、トラフィックが少なすぎて意味のある結果が得られません。
* **速度が遅すぎます**：多くの実験フレームワークにより、サイトの速度が非常に遅くなるため、潜在的な新しいコンバージョンでは、レンダリング速度が遅いため、失われたトラフィックとバウンスを補うことができません。
* **複雑すぎます**：新しい実験の設定に時間がかかりすぎると、実行される実験が少なくなります。

Adobe Experience Manager上で動作しているサイトの場合、開発者がサイトに実験機能を追加できる「すぐに使用できる」実験プラグイン **があります。**&#x200B;このアプローチは、他の実験フレームワークと異なり、3つのことが挙げられます。

* 作成者が使い慣れたツールを使用してテストを容易に設定できるため、個別のログインは必要ありません。
* AEMの配信システムと深く統合されており、サイトの動作を遅らせることなく、コードやコンテンツの変更に対して柔軟に対応できます。
* シンプルなコンテンツの変更だけでなく、デザイン、機能、コードなどのテストも可能です。

## 開始する前に {#before-start}

実験プラグインは[Edge Delivery Services](/help/edge/overview.md)のコンテキスト内で使用されるため、Github アカウント、SharePointやGoogle Driveなどのコンテンツリポジトリ、および[AEM Sidekick](https://www.aem.live/docs/sidekick)が必要になります。 [はじめに – ユニバーサルエディター開発者チュートリアルのページ &#x200B;](https://www.aem.live/developer/tutorial)および[はじめに – 開発者チュートリアル &#x200B;](https://www.aem.live/developer/tutorial)も参照してください。

すべての設定が完了したら、**実験プラグインがどのように機能するかについての簡単なデモを、** インスタント実験[と題したこのビデオ &#x200B;](https://business.adobe.com/products/experience-manager/sites/testing-optimization.html)をご覧ください。

## よく使う用語 {#frequently-used-terms}

このガイドの残りの部分に従って最初の実験を設定する前に、よく使用される用語がいくつかあります。

* **Control**：実験を実行する前のエクスペリエンス。 あらゆる実験において、制御体験に対する改善を検証および実証しようとします。
* **チャレンジャー**：コントロールのエクスペリエンスとは異なり、そのエクスペリエンスに対して、または一緒に「テスト」されるエクスペリエンス。
* **バリアント**: コントロールとチャレンジャーはすべて実験のバリアントです。
* **統計的有意性**：チャレンジャーがコントロールよりも優れているかどうかを評価します。 統計的有意性を計算することで、運を除外し、実際に効果がある結果に集中することができます。

## 実験のバリエーションと一般的なワークフロー {#experiment-variants-workflow}

一般的に、実験を設定する際には、既存のページをコントロールページとして使用します。 その後、チャレンジャーページを作成し、訪問者の一部を対象としたコントロールページに置き換えます。 チャレンジャーページでは、コンテンツのバリエーション、ページレイアウト、call-to-action（CTA）など、さまざまな要素をテストできます。 これらの実験バリエーションは、コントロールページでメタデータパラメーターを追加することで設定できます（以下を参照）。

次に、[運用上のテレメトリ サービス &#x200B;](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)は、コントロール ページの訪問者数とチャレンジャーページの訪問者数などのデータを収集します。 そのデータを使用して、サイトに必要な改善を選択します。 web サイトの確立されたデザイン言語の範囲内で、既存のブロック機能を使用すれば、実験のバリエーションを設定し、わずか数分で本番環境に送信できます。

>[!NOTE]
>このプラグインは、特定につながる可能性のあるエンドユーザーデータを使用せず、保持していないことに注意してください。 AEM as a Cloud Service[の](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)Operational Telemetry サービスを使用するデフォルト設定を使用する場合、エンドユーザーのオプトインもCookieの同意も必要ありません。

### 実験Id {#experiment-identifier}

開始する前に、トラッキングと分析の目的で、すべての実験に独自の識別子が必要です。 良い出発点は、「実験ID」となる、実験に適した一意の識別子を考え出すことです。 実験は、多くの場合、問題トラッカーまたは管理システムで問題IDに関連付けられ、線形的に番号が付けられます。 実験IDでは、プロジェクトの接頭辞が頻繁に使用されます（例：`OPT-0134`、`EXP0004`、または`CCX0076`）。

### チャレンジャーページの構築 {#create-challenger-page}

慣例として、`/experiments/ folder`に小文字の実験IDを含むフォルダーを作成することをお勧めします（例：/experiments/ccx0076/）。 チャレンジャーのバリエーションのすべてのページは、このフォルダーにあります。 このフォルダーは、ローカルリポジトリー（SharepointやGoggle Driveなど）に作成します。

A/B テスト用フォルダは次のようになります。

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

フォルダーを作成したら、コントロールページのコピーをそのフォルダーに入れ、テスト用のバリエーションの一部としてテストしたいページに変更を適用します（上記のビデオを参照）。 例として、実験を実行するweb サイトに次のページがあるとします。

![control-page](/help/sites-cloud/administering/assets/control-page.png)

`experiments/<experiment-id>` フォルダーに配置されたチャレンジャーのコピーは、次のようになります。

![&#x200B; チャレンジャーページ &#x200B;](/help/sites-cloud/administering/assets/challenger-page.png)

Sidekickを使用して、チャレンジャーページをプレビューし、公開します。また、チャレンジャーページのオーサリングが完了したら、公開します。 公開されたチャレンジャーのURLは、次のセクション（実験の設定）で使用されます。

### 実験の設定 {#configure-experiment}

チャレンジャーページの準備が整ったら、コントロールページに戻り、ページがテストの一部であることを示すメタデータを追加する必要があります。

実験のバリエーションに追加する必要があるメタデータ行が2つあります。

* **実験**：実験IDが含まれています。

* **実験バリアント**：複数のチャレンジャーがある場合は、改行で区切ったこのページのすべてのチャレンジャーのURLを含みます。

次の例を参照してください。

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

各実験では、トラフィックはすべてのバリエーション（コントロールとチャレンジャー）に分割され、自動的に均等な分布に設定されます。 そのため、チャレンジャーが1人いる場合、コントロールとチャレンジャーの間には自動的に50/50の分割が行われます。 2人のチャレンジャーがいる場合、コントロールに割り当てられたトラフィックの3分の1と、各チャレンジャーなどが自動的に表示されます。

メタデータを設定することで、分割されたトラフィックを上書きできます。 実験で使用するメタデータをカスタマイズする方法について詳しくは、次の[&#x200B; ページ &#x200B;](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring)を参照してください。

### 実験のバリエーションのプレビューとステージング {#preview-stage-experiment}

テストのプレビューとステージングの準備ができたら、左上のサイドキックから「プレビュー」をクリックします。 実行中の実験を含むページをプレビューする場合は、常に`.aem.page` プレビュー環境に実験オーバーレイが表示されます。 実験オーバーレイでは、実験のバリエーションを切り替えることができ、トラフィックデータも提供されます。

<!--
- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.
-->

各バリエーションの有効性を測定するためのデータ収集は、AEM as a Cloud Serviceの[Operational Telemetry サービス &#x200B;](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)に基づいています。

### 実験バリアントを実稼動環境に送信する {#production-experiment}

実験ページを選択し、サイドキックから「公開」をクリックして、コントロールとチャレンジャーバリアントの両方を公開します。

### ユースケースの例 {#use-case-examples}

以下に、実験のバリエーションの使用例をいくつか示します。 一般的に、基本的なワークフローは上記のワークフローと類似しており、ユースケースごとに特定の変更（チャレンジャーページの数やメタデータの変更など）が行われます。

#### フルページ実験 {#full-page}

ページ全体の検証では、同じページの2つのバリエーションを比較します。 これは、a/b テストのフルページ版で、コントロールページとチャレンジャーページがあります。 チャレンジャーのバリエーションの「オリジナル」コントロールページのコンテンツ全体を別のタイプのコンテンツに置き換えます。 デフォルトでは、顧客トラフィックは均等に（50対50）分割されますが、必要に応じてカスタム分割を作成できます。

<!--
The metadata on the control page should look like this:

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

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.
-->

## その他の注意点 {#other-considerations}

コンテキスト実験を使用する際に考慮すべきその他の側面を以下に示します。

### コンバージョン {#conversion}

実験は、コンバージョンに対応するように設定されています（ページ上のクリック可能な要素を追跡します）。 すべての実験は以下のために定義されなければならない：

* 実験タイプ
* 実験が適用されるエクスペリエンスブロック
* 実験に含まれるバリエーションの数
* 各バリエーションの構成は

### 実験のバリアントがインデックス付けされていないことを確認する {#experiment-not-indexed}

実験を行う場合は、通常、サイトマップからバリエーションを除外し、検索エンジンによってインデックス付けされないようにすることがベストプラクティスです。 これは、バリアントページが重複したコンテンツと見なされ、SEOに悪影響を与える可能性があるためです。

これは、次の2つの方法のいずれかを使用して行うことができます。

* `/experiments`のように、すべての実験を専用フォルダーに一元管理する場合は、バルク `metadata.xlsx` シートにパスとして`/experiments/**`を持つ行と、値が`noindex`、`nofollow`のロボット列が含まれていることを確認します。
* 実験コントロールと通常のコンテンツのバリエーションを維持する場合：各バリエーションのページメタデータにrobots エントリを追加し、値を`noindex`、`nofollow`にします。

## 開発者および技術リソース {#dev-resources}

Adobe Experience Managerは[運用上のテレメトリ ] （/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md）を使用しています

）を使用して、Adobe Experience Managerを搭載したサイトで機能とパフォーマンスの問題を発見して修正するために厳密に必要な操作データを収集します。 運用テレメトリデータは、パフォーマンスの問題を診断するために使用できます。 運用上のテレメトリは、サンプリングを通じて訪問者のプライバシーを保護します（すべてのページビューの一部のみが監視されます）。

### プライバシー {#privacy-experimentation}

AEM as a Cloud Service[の](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)Operational Telemetry サービスは、訪問者のプライバシーを保護し、データ収集を最小限に抑えるように設計されています。 Adobeは、お客様に関する個人情報やお客様に追跡可能な情報を収集しようとしません。 サイト運営者は、以下で収集したデータ項目を確認し、同意が必要かどうかを判断する必要があります。
AEM Operational Telemetryは、使用状況の指標を収集するために、Cookieや`localStorage`、`sessionStorage`などのクライアントサイドの状態やIDを使用しません。 データは、ピクセルや類似の手法ではなく、`Navigator.sendBeacon`呼び出しを通じて透過的に送信されます。 IP アドレス、ユーザーエージェント文字列、またはサンプリングされたデータをキャプチャする目的で使用されるデバイスまたは個人の「フィンガープリント」はありません。

個人データを運用上のテレメトリデータ収集に追加することは許可されておらず、運用上のテレメトリデータを厳密に必要なユースケースを超えるユースケースに使用することはできません。

### よくある質問 {#faq}

よくある質問のリストを以下に示します。

Q：自分の実験のバリエーションの分割率（例えば、コントロールで10%、チャレンジャーで90%）を調整できますか？

はい。分割率は[&#x200B; メタデータ &#x200B;](#configure-experiment)を使用して設定できます。

Q: テキストと画像の両方をテストできますか？

はい、バリエーションはまったく異なるページになる可能性があるので、レイアウトの変更をテストすることもできます。
