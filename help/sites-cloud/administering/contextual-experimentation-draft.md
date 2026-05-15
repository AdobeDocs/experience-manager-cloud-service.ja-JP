---
title: AEM as a Cloud Serviceのコンテキスト実験
description: 実験パネルを使用して、サイトに実験機能を追加する方法を説明します。
feature: Administering
role: Admin
source-git-commit: c948abf5391e61f01912f769b17e1ac0bd81a745
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 2%

---

# AEM as a Cloud Serviceのコンテキスト実験 {#contextual-experimentation}

テストとは、パフォーマンスを向上させ、サイトをより効果的かつ合理的にするために、サイトのデザイン、機能、コードをテストすることです。 これは、コンテンツや機能を変更し、結果を以前のバージョンと比較し、測定可能な効果をもたらす改善点を選ぶことで達成できます。

正しい方法で実施すれば、コンバージョン、エンゲージメント、訪問者の体験を向上させるための強力なパターンになります。 一般的に、この手法を採用する際には避けるべき問題がいくつかあります。

* **少なすぎます**：多くの企業は十分な実験を行っておらず、十分な実験を行うと、トラフィックが少なすぎて意味のある結果が得られません。
* **速度が遅すぎます**：多くの実験フレームワークにより、サイトの速度が非常に遅くなるため、潜在的な新しいコンバージョンでは、レンダリング速度が遅いため、失われたトラフィックとバウンスを補うことができません。
* **複雑すぎます**：新しい実験の設定に時間がかかりすぎると、実行される実験が少なくなります。

Adobe Experience Manager上で動作するサイトの場合、開発者は新しいテスト機能をサイトに追加できます。 このアプローチは、他の実験フレームワークと異なり、3つのことが挙げられます。

* 作成者が使い慣れたツールを使用してテストを容易に設定できるため、個別のログインは必要ありません。
* AEMの配信システムと深く統合されており、サイトの動作を遅らせることなく、コードやコンテンツの変更に対して柔軟に対応できます。
* シンプルなコンテンツの変更だけでなく、デザイン、機能、コードなどのテストも可能です。

## 実験パネル {#experimentation-rail}

実験パネルは、実験を設定するための主な方法です。 このファイルは、[Edge Delivery Services](/help/edge/overview.md) コンテキストまたは[ ユニバーサルエディター](/help/implementing/universal-editor/introduction.md)のいずれかでプロジェクトで使用できます。 そのため、Github アカウント、SharePointやGoogle Driveなどのコンテンツリポジトリ、および[AEM Sidekick](https://www.aem.live/docs/sidekick) プラグインも必要です。 ユニバーサルエディターを使用する場合は、[AEM as a Cloud Service環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)にもアクセスする必要があります。 [はじめに – ユニバーサルエディター開発者チュートリアルのページ ](https://www.aem.live/developer/tutorial)も参照してください。

>[!WARNING]
>実験機能を使用するには、実験エンジンが必要です。 以下の手順を実行する前に、エンジンが正しくインストールおよび更新されていることを確認してください。 詳しくは、次の[ インストールページ ](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation)を参照してください。

### Edge Delivery ServicesのAEM Sidekickを利用したテストの設定

Edge Delivery Services プロジェクト内の実験パネル機能にアクセスするには、[AEM Sidekick](https://www.aem.live/docs/sidekick) プラグインが必要です。 サイドキックを設定するには、次の手順に従います。

1. [AEM Sidekick拡張機能](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar)を追加し、ブラウザーにピン留めします。
1. プロジェクトページをプレビューモードで開きます。
1. AEM Sidekick バーで、設定アイコン ![設定](/help/sites-cloud/administering/assets/settings-1.png)をクリックし、**このプロジェクトを追加**&#x200B;を選択します。
1. 「実験」タブをクリックして、実験パネルを開きます。

### ユニバーサルエディターでの実験の設定

テストを設定する前に、ユニバーサルエディターでオーサリングするには、AEM Sitesをコンテンツソースとして使用する必要があることに留意してください。 必要に応じて、[AEM as a Content Source](https://www.aem.live/developer/ue-tutorial) ページで説明されているチュートリアルに従って、既存のプロジェクトをAEM Sites as a Content Sourceに変換できます。 ユニバーサルエディターでテストを設定する準備ができたら、次の手順に従います。

1. ユニバーサルエディターでプロジェクトを開き、**A/B** アイコン拡張機能を確認します。 アイコンが表示されない場合は、拡張機能マネージャーでこの機能を有効にしているかどうかを確認します。 有効になっていない場合は、有効にするか、アクセスをリクエストしてください。
   <!--1. Open your GitHub repository and check if the `plugins/experimention` folder exists. If not, you will need to set up the experimentation engine and MFE first (see the note above).-->
1. `fstab.yaml`設定をプロジェクト設定に指定し、AEM オーサーインスタンスにリンクします。 [ コードをコンテンツに接続](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)するも参照してください
1. AEM インスタンスを開き、プロジェクトの準備ができたら、ユニバーサルエディターで直接開きます。
1. 実験を実行するプロジェクトとインデックスページを開き、上部バーの&#x200B;**編集**&#x200B;をクリックします。
1. A/B アイコンをクリックして、実験の拡張機能を開きます。

>[!NOTE]
>プロジェクトの実験の設定で問題が発生した場合は、`aem-contextual-experimentation@adobe.com`にお問い合わせください。

>[!NOTE]
>実験エンジンの設定と設定方法について詳しくは、次の[ リポジトリ ](https://github.com/adobe/aem-experimentation/tree/v2-ui)のドキュメントセクションを参照してください。

## 実験のバリエーションと一般的なワークフロー {#experiment-variants-workflow}

ガイドの残りの部分に従って最初の実験を設定する前に、よく使用される用語をいくつか紹介します。

* **Control**：実験を実行する前のエクスペリエンス。 あらゆる実験において、制御体験に対する改善を検証および実証しようとします。
* **チャレンジャー**：コントロールのエクスペリエンスとは異なるエクスペリエンスで、そのエクスペリエンスに対してテストするか、そのエクスペリエンスと一緒にテストされます。
* **バリアント**: コントロールとチャレンジャーはすべて実験のバリアントです。
* **統計的有意性**：チャレンジャーがコントロールよりも優れているかどうかを評価します。 統計的有意性を計算することで、運を除外し、実際に効果がある結果に集中することができます。

一般的に、実験を設定する際には、既存のページをコントロールページとして使用します。 実験パネルを使用して、最初にコントロールページのコピーとなるチャレンジャーページを作成します。 チャレンジャーページでは、コンテンツのバリエーション、ページレイアウト、call-to-action（CTA）など、さまざまな要素をテストできます。 また、実験パネルの&#x200B;**バリエーションを生成**&#x200B;機能を使用して、AIで生成したバリエーションを使用することもできます。

それぞれの実験では、最初にトラフィックがcontrolとchallengerの間で50:50に分割されますが、必要に応じてトラフィックの分割方法を設定できます。 実験を有効にすると、Operational Telemetry サービスを介してデータが受信されます。

[運用テレメトリサービス ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)は、コントロールページとチャレンジャーページの訪問者数などのデータを収集します。 そのデータを使用して、サイトに必要な改善を選択します。 web サイトの確立されたデザイン言語の範囲内で、既存の機能を使用する限り、実験のバリエーションを設定して、わずか数分で本番環境に送信できます。

>[!NOTE]
>このプラグインは、特定につながる可能性のあるエンドユーザーデータを使用せず、保持していないことに注意してください。 AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)の[Operational Telemetry サービスを使用するデフォルト設定を使用する場合、エンドユーザーのオプトインもCookieの同意も必要ありません。

<!--### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. -->

### ユニバーサルエディターでの実験の作成

ユニバーサルエディターでテスト機能を使用するには、最初に上記の章で詳しく説明されているようにテスト用パネルを設定し、AEM Sitesをコンテンツソースとして使用する必要があります。 すべての設定が完了したら、次の手順に従います。

### ユニバーサルエディターでプロジェクトの編集を開始する

AEM インスタンスを開き、プロジェクトの準備ができたら、ユニバーサルエディターで直接開きます。 プロジェクトの準備が整っておらず、AEM Sitesがコンテンツソースとして設定されている場合は、提供されたテンプレートから新しいボイラープレートプロジェクトを作成します。 リポジトリまたはサンプルリポジトリをリンクして、[https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation)を操作できます。 [AEM Sites as a Content Sourceの設定](https://www.aem.live/developer/ue-tutorial) ページも参照してください。 プロジェクトの設定が完了したら、プロジェクトを開き、実験を実行するインデックスページを開き、上部のバーの「**編集**」をクリックします。

### A/B拡張機能の起動

**A/B** アイコンをクリックして、実験の拡張機能を開きます。 最初の使用時には、インターフェイスは空になります。 「**新規作成**」をクリックして、新しい実験を開始します。

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### 実験の詳細を設定

実験値の一部は、次のように事前に定義されています。

**実験タイプ**: A/B テスト （現在サポートされているタイプのみ）
**用に最適化**: コンバージョン （現在サポートされているタイプのみ）

また、実験の名前をより説明的な名前（例：`homepage-head-experiment`）に変更することもできます。

![実験の詳細](/help/sites-cloud/administering/assets/exp-values.png)

### バリエーションの追加と編集

続行する前に、上記の「チャレンジャー」と「バリアント」の概念を必ず理解してください。 「**新しい**&#x200B;を追加」をクリックして、チャレンジャーのバリアントを作成します。

* チャレンジャーページに移動します。最初は、コントロールのコピーに過ぎません。
* コンテキストに沿ってページを直接編集するか、**バリエーションを生成**&#x200B;をクリックしてAI支援を使用します。
* 変更を加えた後、拡張機能に戻って続行します。

![Control-variant](/help/sites-cloud/administering/assets/control-variant.png)

### 他のプロパティを定義してドラフトとして保存

実験パネルでは、開始日と終了日を設定できます（両方ともオプション）。 開始日が指定されていない場合、テストは公開後に開始されます。 終了日が指定されていない場合、テストは無期限に実行されます。 また、トラフィックの分割を調整することもできます。50対50の分割から始めることをお勧めします。

完了したら、**保存**&#x200B;をクリックします。これにより、テストがドラフトとして保存されます。 この実験はまだアクティブではありません。 **実験に戻る**&#x200B;をクリックして概要に戻るか、編集インターフェイスから実験をアクティブにできます。

![ドラフト](/help/sites-cloud/administering/assets/draft-save.png)

### 実験を有効にする

準備ができたら、**アクティベート**&#x200B;をクリックして実験を開始し、実験ページを公開します。 このテストは、運用上のテレメトリ（RUM）データの収集を開始します（詳細については、以下の章を参照してください）。

![アクティベート](/help/sites-cloud/administering/assets/activate.png)

### 監視とプロモーション

実験が統計的有意性に達したら、**プロモーション**&#x200B;をクリックして、目的のバリエーションを新しいコントロールにします。 統計的有意性に達しない場合でも、アクティベーション後は任意の時点で実験のバリエーションを宣伝できます。

### Edge Delivery ServicesのAEM Sidekickを利用したテストでは

AEM sidekickがインストールされている場合は、ユニバーサルエディターを使用せずに、Edge Delivery Serviceでプロジェクトに直接実験パネルを使用できます。 機能は基本的に上記のA/B テストと同じですが、テストを編集および設定するには&#x200B;**プレビュー** モードである必要があることに留意してください。 テストの設定が完了したら、**Activate**&#x200B;をクリックして、コントロールとチャレンジャーのバリアントの両方を公開し、テレメトリデータの収集を開始します。

<!-- ### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the “Experiment ID”. Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let’s assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

<!--- The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md). -->

<!--- ### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like. -->

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

コンテキスト実験を使用する際に考慮すべき側面を以下に示します。

### コンバージョン {#conversion}

実験は、コンバージョンに対応するように設定されています（ページ上のクリック可能な要素を追跡します）。 現在、ページごとに1つの実験でページレベルの実験をサポートしています。

<!--### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.-->

## 開発者および技術リソース {#dev-resources}

Adobe Experience Manager では[運用上のテレメトリ](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)を使用して、Adobe Experience Manager を利用したサイトで機能とパフォーマンスの問題を検出および修正するために必要な運用データのみを収集します。 運用テレメトリデータは、パフォーマンスの問題を診断するために使用できます。 運用上のテレメトリは、サンプリングを通じて訪問者のプライバシーを保護します（すべてのページビューの一部のみが監視されます）。

### プライバシー {#privacy-experimentation}

AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)の[Operational Telemetry サービスは、訪問者のプライバシーを保護し、データ収集を最小限に抑えるように設計されています。 Adobeは、お客様に関する個人情報やお客様に追跡可能な情報を収集しようとしません。 サイト運営者は、以下で収集したデータ項目を確認し、同意が必要かどうかを判断する必要があります。
AEM Operational Telemetryは、使用状況の指標を収集するために、Cookieや`localStorage`、`sessionStorage`などのクライアントサイドの状態やIDを使用しません。 データは、ピクセルや類似の手法ではなく、`Navigator.sendBeacon`呼び出しを通じて透過的に送信されます。 IP アドレス、ユーザーエージェント文字列、またはサンプリングされたデータをキャプチャする目的で使用されるデバイスまたは個人の「フィンガープリント」はありません。

個人データを運用上のテレメトリデータ収集に追加することは許可されておらず、運用上のテレメトリデータを厳密に必要なユースケースを超えるユースケースに使用することはできません。
