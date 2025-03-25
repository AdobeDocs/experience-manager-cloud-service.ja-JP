---
title: Dynamic Media のベストプラクティス
description: 画像やビデオを操作する際の Dynamic Media のベストプラクティスと、Dynamic Media ビューアのベストプラクティスについて説明します。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '4049'
ht-degree: 98%

---

# Dynamic Media のベストプラクティス{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

{{see-also-dm}}

組織は、ユーザーと接点を持つためのチャネルやデバイスの急激な増加に直面しています。カスタマージャーニーは、実店舗、web、モバイル、ソーシャルメディア、メール、コマースに広がります。この需要を満たすために、Adobe Experience Manager（AEM）の Dynamic Media では、包括的なソリューションを提供します。このソリューションはアセット配信を最適化し、パーソナライゼーションを処理します。また、チャネルやデバイスをまたいで、高パフォーマンス、かつブランドに合わせた一貫性のあるエクスペリエンスを保証します。

Dynamic Media の主要な考え方の一部を次に示します。

* **単一ファイルアプローチ：** Dynamic Media では、1 つのプライマリソースファイルを保存し、すべてのサイズのバリエーションと視覚効果は配信時に動的に作成され、最適化されます。このアプローチにより、ストレージコストを節約し、ワークフローの複雑さを解消します。
* **真にグローバル：**&#x200B;コンテンツ配信時に適用されるスマートイメージングでは、画質を損なうことなく、画像サイズとページの重さを大幅に削減します。ネットワーク帯域幅とデバイスのピクセル比に合わせて最適化されます。
* **AI を活用：** AI 駆動機能のスマート切り抜きでは、画像とビデオの目的の箇所を自動で切り抜きます。手作業をなくし、企業での使用に合わせて効率的に拡張できます。
* **簡単なビデオ：**&#x200B;プライマリソースビデオを Dynamic Media にアップロードし、説明的なオーディオと共に複数の言語にアダプティブにストリーミングします。
* **エクスペリエンスビューアライブラリ：**&#x200B;画像やビデオのエクスペリエンスビューアをカスタマイズしてブランド化します。これらのビューアは、デジタルエクスペリエンスにシームレスに統合されます。
* **新しい形式のサポート：** Dynamic Media では、3D およびパノラマエクスペリエンスを配信できます。

[Dynamic Media ジャーニー](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1)を検討する際に、以下のベストプラクティスの統合リストを確認すると、その機能を最大限に活用するのに役立ちます。チャネルやデバイスをまたいでエクスペリエンスを最適化できるように、Dynamic Media のこれらのベストプラクティスを、具体的なコンテキストやプロジェクト要件に合わせて調整します。

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>この記事における Dynamic Media のベストプラクティスは、Dynamic Media の新しいテクノロジーが登場するにつれて、時間の経過と共に進化する可能性があります。以下の情報は、Dynamic Media の最新バージョンに関するものです。


## Dynamic Media へのアセットの取り込み

**ビジネスケース：** *大量のアセットを効率的に管理し、関連性が高い承認済みのコンテンツのみをエンドユーザーに配信します。*

大量のアセットの管理を効率的に合理化します。Dynamic Media の&#x200B;**選択的同期**&#x200B;および&#x200B;**選択的公開**&#x200B;機能を使用して、承認済みの適切なコンテンツのみがエンドユーザーに届くようにします。

* **選択的同期：**
Dynamic Media と同期するアセットを選択できるプロアクティブな機能。例えば、最終承認を受けたアセットを含むフォルダーのみを同期するように指定できます。このワークフローは、顧客への配信の準備が行われているアセットを管理するのに役立ちます。

* **選択的公開：**
アセットを同期した後に、選択的公開を使用すると、顧客に表示するアセットを制御できます。つまり、どの承認済みアセットがチャネルを通じて実際に配信されるかを管理できるので、顧客に関連性の高い最適なコンテンツのみを表示できます。

これらの 2 つのベストプラクティスは、リッチメディアコンテンツに対するコントロール、ガバナンス、生産性を向上させるのに役立ちます。

詳しくは、[Dynamic Media のフォルダーレベルでの選択的公開の設定](/help/assets/dynamic-media/selective-publishing.md)を参照してください。


## Dynamic Media ビューア

Dynamic Media ビューアのベストプラクティスは、AEM 上の Dynamic Media アセットのパフォーマンス、機能、ユーザーエクスペリエンスを最適化するために設計された重要なガイドラインです。これらのプラクティスにより、Dynamic Media のすべての機能を使用するように、アセットが適切に同期、公開、設定されます。

これらのベストプラクティスに従うことで、シームレスな統合、効率的なアセット管理、強化されたビューアのインタラクションを実現できます。アセットの同期、スマート切り抜きの使用、JavaScript ファイルの包含ガイドラインへの準拠はすべて重要なプラクティスです。これらのレコメンデーションは、様々なプラットフォームやデバイス間でのメディア配信の整合性と信頼性を維持するのに役立ちます。

* **ビューアアセットの同期：**
プレーヤーを使用する前に、すべてのビューアアセットが Dynamic Media と同期されます。

   * `/libs/dam/gui/content/s7dam/samplemanager/samplemanager` にあるサンプルマネージャーページにアクセスします。このページでは、標準のアイコン、CSS ファイル、プリセットなど、ビューアのアセットを再同期できます。
   * ビューアの問題が発生した場合は、[Dynamic Media ビューアのトラブルシューティング](/help/assets/dynamic-media/troubleshoot-dm.md#viewers)の記事を参照してください。

* **アセットの公開：**
配信ビューアでアセットを表示する前に、アセットが公開されます。
* **自動再生ビデオのミュート：**
ビデオの自動再生機能については、ブラウザーがボリュームによるビデオの再生を制限するので、ミュートされたビデオ設定を使用します。
* **スマート切り抜き：**
スマート切り抜き用の Image v3 コンポーネントを使用して、画像アセットのプレゼンテーションを強化します。
* **JavaScript ファイルの組み込み：**
ページには、プライマリビューアの JavaScript ファイルのみを組み込みます。ビューアのランタイムロジックによってダウンロードされる可能性のある追加の JavaScript ファイルを参照しないでください。具体的には、`/s7viewers` コンテキストパス（統合 SDK インクルードと呼ばれる）から HTML5 SDK `Utils.js` ライブラリに直接リンクしないでください。ビューアのロジックは、リリース間で変更される可能性がある `Utils.js` または類似のランタイムビューアライブラリの場所を管理します。アドビでは古いバージョンのセカンダリビューアをサーバー上に保持しないので、これらを直接参照すると、今後の更新でビューアの機能が損なわれる可能性があります。
* **埋め込みガイドライン：**
各ビューアに固有の埋め込みガイドラインについては、ドキュメントを参照してください。
詳しくは、[AEM Assets のビューア](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers)を参照してください。
* **SDK チュートリアルと例：**
SDK コンポーネント API について詳しくは、[ビューア SDK チュートリアル](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/library/c-tutorial)と [HTML5 SDK アプリケーションの例](https://s7d9.scene7.com/s7sdk/2024.5/docs/jsdoc/index.html)を参照してください。


## 配信用アセットの準備

### アセットの整理

**ビジネスケース：***アセットを効率的に整理してワークフローを合理化します。*

ワークフローを合理化してアセットを効率的に整理するには、次のベストプラクティスから 1 つ以上を使用してください。

* **アセットをフォルダーに整理：**
アセットを効率的に整理するには、コンピューター上でファイルを整理する際と同様に、アセットをフォルダーに分類する必要があります。これらのフォルダー内での適切な命名、サブフォルダーの構造化、ファイル管理は、アセット処理を効率的に行う上で重要です。体系的な命名規則とメタデータ手法を実装すると、デジタルアセットリポジトリのユーティリティを最大限に活用できます。
詳しくは、[フォルダー内のアセットの整理](/help/assets/organize-assets.md#organize-using-folders)を参照してください。
* **タグを使用したアセットの整理：**
アセットにタグを付けると、検索性、コレクションの作成、検索ランキングが向上します。Adobe Sensei の AI は、正確なタグ付けを行うために自己学習アルゴリズムを採用しており、迅速なアセット取得を可能にします。また、Adobe Sensei は、説明的な自動タグ付けを使用してアセット管理を簡素化し、カスタムタグを含む関連タグを認識してアセットに割り当てます。
詳しくは、[タグを使用したアセットの整理](/help/assets/organize-assets.md#use-tags-to-organize-assets)を参照してください。
* **アセットをコレクションとして整理：**
Dynamic Media を Experience Manager Assets と併用すると、ユーザー間でアセットコレクションを効率的に作成、編集、共有できます。静的なリストや動的な検索ベースのコンパイルなど、様々なコレクションタイプを設定できます。これらのコレクションタイプは、カスタマイズ可能なアクセス権と編集権を使用して、様々な場所で共有できます。
詳しくは、[アセットをコレクションとして整理](/help/assets/manage-collections.md)を参照してください。
* **プロファイルを使用したアセットの整理：**
処理プロファイルは、指定フォルダーでのアセット処理を自動化し、組織を効率化します。メタデータ、ファイル名およびフォルダー構造を標準化すると、デジタルアセットコレクションが拡大するにつれて、これらのプロファイルを一貫して正確に適用できます。
詳しくは、[プロファイルを使用したアセットの整理](/help/assets/organize-assets.md#organize-to-use-profiles)を参照してください。



### 画質の最適化

**ビジネスケース：***Dynamic Media から高品質の画像を取得します。*

画質を向上させるには、様々な要素を慎重に考慮する必要があります。このプロセスには時間がかかる場合があります。ただし、望ましい結果を得るのに役立つ、実証済みのプラクティスがいくつかあります。これらのベストプラクティスには、最適な画像サイズ設定、画像のシャープニング、使用に最適な画像形式を取得する方法が含まれています。

詳しくは、[画質最適化のベストプラクティス](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)を参照してください。

画質に対する考え方は人によって異なるため、ときには望ましい結果を得るために、実験に対する体系的なアプローチが必要となる場合があります。Adobe Experience Manager は、100 を超える Dynamic Media コマンドでこのプロセスを支援し、画像を強化します。

詳しくは、[Dynamic Media スナップショット](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)をご覧ください（3 分 17 秒）。

これらの様々なコマンドが画質に与える影響を評価するには、Dynamic Media に画像をアップロードし、指定した URL でツールのインターフェイスを使用して、試してみるコマンドを適用します。

試してみるには、[Dynamic Media Snapshot](https://snapshot.scene7.com/) を起動してください

### 画像に適用されるスタイルの標準化

**ビジネスケース：***画像アセットに適用されるスタイルと変換を効率的に標準化します。*

Dynamic Media で画像プリセットを定期的に使用すると、画像のサイズ、形式、プロパティを一貫して動的に調整できます。画像プリセットは、マクロと考えることができます。サイズ設定と書式設定のためのコマンドの名前付きセットです。例えば、サイトで様々なサイズと形式の製品画像が必要で、デスクトップとモバイルに特定の圧縮が必要な場合は、画像プリセットによってこのプロセスが効率的に自動化されます。

試してみるには、[アセットをレンダリングするための画像プリセットの作成の基本](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)を参照してください

### 画像やビデオのフォーカスとフレーミングの調整

**ビジネスケース：***画像やビデオの主な POI が、デバイス間でフォーカスされたままであることを確認します。*

スマート切り抜きは、アドビの AI および機械学習フレームワークである Adobe Sensei を使用して画像やビデオの切り抜きを自動化する Dynamic Media の機能です。画像やビデオ内の主なサブジェクトや POI をインテリジェントに検出し、フォーカスします。このインテリジェンスにより、デスクトップコンピューターやモバイルデバイスの様々な画面サイズ間で焦点位置が維持されます。

ベストプラクティスとしては、スマート切り抜きを使用して画像プロファイルを作成することをお勧めします。プロファイルでは、様々な画面サイズを定義し、Adobe Sensei に残りの処理を任せることで、画像やビデオが常に閲覧者のデバイスに合わせて最適化されるようにすることができます。

詳しくは、[AEM Assets Dynamic Media でのスマート切り抜きの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)（6 分 35 秒）と[ビデオに対する Dynamic Media スマート切り抜きの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video)（6 分 22 秒）をご覧ください。

### SEO ランキングの向上

**ビジネスケース：***Dynamic Media を設定して、SEO ランキングを向上させます。*

画像が全体的な SEO 戦略に効果的に貢献するように、次のレコメンデーションを定期的に使用します。

* **意味のある画像ファイル名：**
画像コンテンツを反映したわかりやすいファイル名を使用します。例：

   * `myCompany-Silver-Wrist-Watch` を使用します
   * `myCompany_Silver_Wrist_Watch` または `myCompanySilverWristWatch` を&#x200B;*回避*&#x200B;します

  これにより、検索エンジンが画像のコンテキストを理解し、SEO を向上させることができます。Google では、ファイル名でアンダースコアやスペースよりもハイフンが優先されます。また、ファイル名では単語の連結を回避します。
* **カスタムドメイン：**
会社名やブランド名を含むカスタムドメインを実装して、ブランドの認識と信頼を強化します。例：

   * `http://images.mycompany.com/is/image/companyname/` を使用します
   * `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982` を&#x200B;*回避*&#x200B;します

* **SEO に対応したフォルダー構造：**
インデックス作成を強化するには、`http://images.mycompany.com/is/image/companyname/` のように、会社名やブランドを含むフォルダー構造で画像を整理します。
* **Dynamic Media ルールセット：**
様々な要因に基づいて URL を条件付きで変換し、SEO とユーザーエクスペリエンスを強化する方法を学びます。
詳しくは、[ルールセットを使用した URL の変換](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)を参照してください。
* **スマートイメージングとスマート切り抜き：**
Dynamic Media のスマートイメージング機能とスマート切り抜き機能を使用して、最適化されたレスポンシブな画像を提供します。これにより、ページの読み込み時間が改善されるだけでなく、SEO ランキングにもプラスに貢献します。
詳しくは、[スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)を参照するか、[AEM Assets Dynamic Media でのスマート切り抜きの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)（6 分 35 秒）をご覧ください。

これらのベストプラクティスは、Google の画像 SEO のベストプラクティスとうまく一致しています。このようなプラクティスでは、適切な命名規則、構造化データ、最適化された画像配信を通じて、検索エンジンにコンテキストと明確さを提供する重要性が強調されます。

詳しくは、[Google の URL 構造のベストプラクティス](https://developers.google.com/search/docs/crawling-indexing/url-structure)と [Google 画像 SEO のベストプラクティス](https://developers.google.com/search/docs/appearance/google-images)を参照してください

### コマンドを使用した画像の動的な強化と視覚効果の作成

**ビジネスケース：***画像にリッチな視覚効果を適用します。*

Dynamic Media では、複数の静的アセットを必要とせずに、画像を強化し、視覚効果を動的に作成するための一連のコマンドを提供します。これらのプロセスの一部についての簡単な説明と、ガイドとなる例の一部を以下に示します。

#### ソース画像内の効果

| タスク | 実行内容 |
| --- | --- |
| **元の画像をアップロードして公開** | <ul><li> まず、元の画像を Dynamic Media にアップロードします。</li><li> その画像が公開されており、URL を通じてアクセスできることを確認します。</li><li> この例では、白い背景と時計のストック画像（「画像 X」と呼びます）が Dynamic Media にアップロードされます。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer)</li></ul> |
| **マスクを作成** | <ul><li> サブジェクト（効果を適用する領域）と背景（変更する領域）を定義するマスクを作成します。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)</li><li> マスクは通常、グレースケール画像で、白はサブジェクト、黒は背景を表します。Adobe Photoshop などのツールを使用してマスクを作成できます。<br>詳しくは、[Photoshop でのクイックマスクの作成と編集](https://helpx.adobe.com/jp/photoshop/using/create-temporary-quick-mask.html)を参照してください。</li><li> 「画像 X」について、強調するサブジェクトの輪郭を正確に描くマスクを作成します。例えば、ユーザー、オブジェクトなどです。</li></ul> |
| **Dynamic Media URL コマンドを効果に適用** | マスクを作成したら、URL コマンドを使用して光彩（外側）などの効果を適用したり、背景色を「画像 X」に変更したりします。次の 2 つの例があります。<ul><li> **光彩（外側）エフェクト：**<br>&#x200B;サブジェクトの境界に沿って光彩（外側）効果を追加するには、URL を次のように編集します。<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25)<br>この URL では、`op_blur`、`op_grow` および `opac` パラメーターによって光彩（外側）効果が作成されます。</li><li> **背景色の変更：**<br>&#x200B;背景色を変更するには、異なる背景色の値を持つ次の URL を使用します。<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0)<br>この例では、`color=255,255,0` によって背景色が黄色に設定されます。視覚効果を得るために、背景を特定の色に編集します。</li></ul> |

#### 画像の境界線の追加

Dynamic Media を使用すると、URL を通じて画像を直接操作できるので、動的なデジタルエクスペリエンスを作成するための強力なツールになります。一部の例を以下に示します。まず、次の元の画像の URL から始めましょう。[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel)。

| タスク | 実行内容 |
| --- | --- |
| **白い境界線** | 白い境界線を追加するには、次の URL を使用します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10)<br>この URL では、`extend=10,10,10,10` パラメーターによって、すべての辺の境界サイズが 10 ピクセルに指定されます。 |
| **白い境界線に沿ってぼかす** | 白い境界線に沿ってブラーエフェクトを追加するには、次のように URL を編集します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0)<br>この URL では、`effect=-1` パラメーターによって、ブラーエフェクトが適用され、`op_blur=60` によってぼかしの強度が制御されます。 |
| **外側の境界に沿ったドロップシャドウ効果** | 外側の境界に沿ってドロップシャドウ効果を追加するには、次の URL を使用します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0)<br>`$shadow$` パラメーターによってシャドウ効果が作成され、`color=0,0,0` によってシャドウの色が黒に設定されます。 |

目的の視覚効果を得るには、これらの URL を自由に試してください。

#### 画像オーバーレイの作成

既存の画像にロゴやアイコンを重ねて表示する場合は、Dynamic Media では URL コマンドを使用すると簡単に行うことができます。手順を詳しく見てみましょう。

| 手順 | 実行内容 |
| --- | --- |
| **ベース画像をアップロードして公開** | まず、ロゴやアイコンを重ねて表示するベース画像をアップロードして公開します。任意の画像をベースとして使用できます。<br>例えば、次にベース画像を示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)。 |
| **ロゴやアイコン画像をアップロードして公開** | 次に、ベース画像の上に重ねて表示する画像をアップロードして公開します。この画像は、オーバーレイするロゴやアイコンを含む透明な PNG にする必要があります。<br>次に、重ねて表示する透明効果のある星形オブジェクトの透明な PNG 画像を示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Dynamic Media URL を適用** | 次に、ベース画像とロゴやアイコン画像を組み合わせた Dynamic Media URL を作成します。URL コマンドを使用すると、この効果を得ることができます。<br>URL 構造は次のようになります。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png)<br>ここで、アセット<ul><li> `hotspotRetailBaseImage` は、ベース画像です。</li><li> `starxp` は、ロゴ／アイコンの画像です。</li><li> `layer=1` は、ロゴやアイコンをベース画像の上に重ねることを指定します。</li><li> `scale=1.25` は、ロゴ／アイコンのサイズを調整します。</li><li> `posN=0.33,-.25` は、ベース画像に対するロゴ／アイコンの位置を決定します。</li><li> `fmt=png` は、出力が PNG 形式になることを保証します。</li></ul> |

詳しくは、[src](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) を参照して、`src` コマンドおよびその他の Dynamic Media URL コマンドの詳細を確認してください。


#### プロモーションテキストのオーバーレイ

HTML と CSS を使用して画像にプロモーションテキストメッセージをオーバーレイする手順を以下に示します。

| 手順 | 実行内容 |
| --- | --- |
| **ベース画像をアップロードして公開** | まず、テキストを重ねて表示するベース画像をアップロードして公開します。任意の画像を使用できます。例えば、ベース画像のサンプルを次に示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Dynamic Media のテキスト演算子を適用** | Dynamic Media を使用すると、テキスト演算子を適用して、動的なテキストを画像に直接オーバーレイできます。次のサンプル URL は、この機能を示します。<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3333&amp;wid=600&amp;hei=600) |

#### 様々なユースケースに対応したサイズ変更と切り抜き

##### 画像のサイズ変更の基本

画像のサイズ変更には、画像のサイズ、解像度、ファイルサイズの変更が含まれます。考慮すべき重要なポイントは次のとおりです。

* **ピクセル構成：**
デジタル画像は、ピクセルと呼ばれる小さな点で構成されます。画像を作成する際には、特定の数のピクセルが含まれます。サイズ変更では、ピクセルを追加または削除して、画像のサイズ、解像度、ファイルサイズを変更します。
* **縦横比：**
歪みを防ぐには、縦横比（幅と高さの関係）を維持することが重要です。画像を拡大（アップスケーリング）する場合でも、縮小（ダウンスケーリング）する場合でも、縦横比を維持することで視覚的な一貫性が確保されます。
* **品質に関する考慮事項：**
サイズ変更は、画質に影響を与える場合があります。ピクセル化につながる可能性があるので、大幅なアップスケーリングは回避します。代わりに、より大きなサイズと解像度で画像を再現することを検討してください。画像が小さい場合は、適切なツールを使用して解像度を維持します。

##### 切り抜きとサイズ変更

切り抜きとサイズ変更は、サムネール、製品表示画像、バナーの作成など、様々なユースケースに合わせて画像を変換できる Dynamic Media の手法です。

* **切り抜き：**
画像の一部を削除して、構成とフレーミングを変更します。全体の寸法は変更しませんが、特定の領域に焦点を当てます。
* **サイズ変更：**
縦横比を維持しながら、画像全体の寸法、解像度、ファイルサイズを調整します。

次のリビングルームの画像を含むユースケースを見てみましょう。

* **元のリビングルームの画像：**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **サムネール（200 ピクセル x 200 ピクセル）：**
すばやく読み込んだり表示したりするのに適した小さいバージョンです。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop)
* **切り抜き付きサムネール（200 ピクセル x 200 ピクセル）：**
ソファ領域にフォーカスするために切り抜きました。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **製品表示画像（800 ピクセル x 600 ピクセル）：**
ソファを表示するために切り抜いてサイズ変更しました。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **バナー（1720 ピクセル x 820 ピクセル）：**
元の画像から派生し、部屋を強調しました。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop)

特定のニーズに合わせて、これらのバリエーションを自由に検討してください。
URL 内で使用できるコマンドについて詳しくは、[コマンドリファレンス](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference)を参照してください。

### GIF 画像の配信

**ビジネスケース：***Dynamic Media を使用して GIF をストリーミングする*

Dynamic Media を通じて GIF をアップロードおよび配信できます。アニメーション GIF をレンダリングするには、URL で `is/image` を `is/content` に置き換えます。例えば、`abc.gif` をアップロードした場合は、次を使用します。

* この URL パスは、GIF の静的ビューをレンダリングします。

  ```
  https://your.domain.com/is/image/yourfolder/abc
  ```

* この URL パスは、GIF のアニメーションビューをレンダリングします。

  ```
  https://your.domain.com/is/content/yourfolder/abc
  ```

>[!NOTE]
>
>URL パスで `is/content` を使用する際、画像変換コマンドはアセットに適用されません。

### Web サイトにビデオを公開する

**ビジネスケース：** *マーケティングサイトのビデオをすばやく公開します。*

* **ビデオプロファイルの選択：**
まず、Dynamic Media で適切なビデオプロファイルを選択する必要があります。AEM Assets のビデオプロファイルで利用可能な*アダプティブビデオエンコーディング*&#x200B;プロファイルを選択できます。これらの事前定義されたエンコーディング設定により、様々なデバイスや帯域幅の条件で再生できるようにビデオが最適化されます。または、独自のアダプティブビデオプロファイルを作成することもできます。
* **プロファイルの割り当て：**
選択したビデオプロファイルを、ビデオのアップロード先フォルダーに割り当てます。この手順により、アップロードプロセス中に正しいエンコーディング設定が適用されるようになります。
* **オリジナルビデオのアップロード：**
オリジナルビデオファイルをアップロードします。高画質のビデオであることを確認してください。ソースビデオが優れているほど、最終結果も良くなります。
* **プレビューと公開：**
ビデオをプレビューして、すべてが期待どおりに表示されることを確認します。満足な結果であれば、公開します。この手順により、オーディエンスがビデオにアクセスできるようになります。
* **リンクまたは埋め込み：**
公開後、次の 2 つのオプションがあります。

   * **直接リンク：**
指定された URL を使用して、ビデオに直接リンクします。マーケティングサイトで適切にハイパーリンクを設定します。
   * **ビデオを埋め込む：**
提供された埋め込みコードをコピーして、Web ページのHTMLでビデオを表示する場所に貼り付けます。 これにより、ビデオをサイトで直接再生できます。

詳しくは、「[ビデオ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video)」に移動します。

### 最適な品質とエンゲージメントのためのビデオ設定

**ビジネスケース：** *最高の品質とエンゲージメントを得るために、ビデオを設定します。*

ビデオの品質とエンゲージメントを最適なものにするには、次のベストプラクティス戦略を組み合わせて実装することを検討してください。

* **組み込みの HTML5 ビデオビューアの使用：**
Dynamic Media HTML5 ビデオビューアプリセットは、堅牢なビデオプレーヤーです。これらを使用すると、HTML5 ビデオの再生とモバイルデバイスに関連するよくある問題を回避できます。
これらのプリセットは、アダプティブビットレートストリーミング配信やデスクトップブラウザーの範囲制限などの課題に対処します。
詳しくは、[ベストプラクティス：HTML 5 ビデオビューアの使用](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer)を参照してください。

* **Dynamic Media ビデオプロファイルの使用：**
Dynamic Media のビデオプロファイルは、効率的なビデオ管理、一貫した画質およびアダプティブストリーミングに役立ちます。
詳しくは、[Dynamic Media ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)を参照してください。

* **ビデオエンコーディングのベストプラクティスに従う：**
エンコード時に過度のダウンスケーリングを行わずに、元のビデオ品質を維持するビデオエンコーディングプロファイルを適用します。
詳しくは、[ビデオエンコーディングのベストプラクティス](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos)を参照してください。

* **プログレッシブストリーミングの代わりにアダプティブストリーミングを採用：**
アダプティブストリーミングは、ビューアのインターネット接続速度とデバイス機能に基づいてビデオ品質を調整します。
HLS（HTTP ライブストリーミング）や DASH（`Dynamic Adaptive Streaming over HTTP`）などのプロトコルを使用して、最適な再生品質を実現します。
ビデオを線形に配信するプログレッシブストリーミングとは異なり、アダプティブストリーミングはバッファリングを最小限に抑え、シームレスな視聴エクスペリエンスを提供します。

### 多言語で利用できるようにビデオを国際化する

**ビジネスケース：***ビデオを多言語で利用できるように準備します。*

グローバルオーディエンスにリーチするには、多言語で利用できるようにビデオを国際化することが不可欠です。Dynamic Media には、この目標を達成するのに役立つ機能が用意されています。

* **ビデオのアップロード**
   * まず、ビデオエンコーディングプロファイルを作成します。Dynamic Media に付属している事前定義済みのアダプティブビデオエンコーディングプロファイルを使用することも、独自のカスタムプロファイルを作成することもできます。
   * ビデオ処理プロファイルを、プライマリソースビデオのアップロード先となる 1 つ以上のフォルダーに関連付けます。
   * プライマリソースビデオをこれらのフォルダーにアップロードします。Dynamic Media では、割り当てたビデオ処理プロファイルに基づいてエンコードします。
   * Dynamic Media では、最小解像度が 25 × 25 を超える短い形式のビデオ（最大長 30 分）が主にサポートされています。最大 15 GB のビデオファイルをアップロードできます。1

* **ビデオを管理：**
   * AEM 内でビデオアセットを整理、参照、検索します。
   * ビデオアセットをプレビューして公開します。
   * ソースビデオとそのエンコードされたレンディションを、関連するサムネールと共に表示します。
   * タイトル、説明、タグ 2 など、ビデオのプロパティを編集します。

* **ローカライゼーション：**
   * ターゲットとなる地域／言語ごとに、オーディオトラックとサブタイトルを作成します。
   * AEM インターフェイスからこれらのオーディオトラックとサブタイトルトラックをビデオに追加します。
   * ユーザーはビデオを再生する際に、オーディオとサブタイトルの優先言語を選択できます。

* **公開：**
   * Web コンテンツ管理（WCM）システムとして AEM を使用している場合は、web ページにビデオを直接追加できます。
   * サードパーティの WCM システムを使用している場合は、URL または埋め込みコードを使用して、web ページにビデオをリンクまたは埋め込むことができます。

詳しくは、[Dynamic Media でのビデオの複数キャプションおよびオーディオトラックのサポートについて ](/help/assets/dynamic-media/video.md#about-msma) を参照してください。


## 顧客へのアセットの送信

### 画像サイズの最適化とページの読み込み時間の最小化

**ビジネスケース：***任意のブラウザーまたは画面に合わせて画像のサイズを最適化し、ページの読み込み時間を短縮します。*

Dynamic Media スマートイメージングは、クライアントのブラウザー機能に基づいて画像の形式、サイズ、品質を自動的に最適化することで、画像配信のパフォーマンスを向上させる強力なツールです。

アドビでは、画像形式を手動で `webp` または `avif` に設定するのではなく、スマートイメージングの機能を使用することをお勧めします。理由は次のとおりです。

* **ブラウザーの互換性：**
スマートイメージングは、配信される画像形式がユーザーのブラウザーと互換性があることを保証します。
* **最適な圧縮：**
特定のブラウザー、ネットワーク条件、画面解像度に基づいて、圧縮に最適な形式を選択します。
* **最新の形式：**
`avif` はより優れた圧縮を提供する新しい形式ですが、まだすべてのブラウザーで一般的に広くサポートされているわけではありません。
* **ベストプラクティス：**
最適な web 最適化形式を保証するには、コマンド `fmt=webp` または `fmt=avif` を手動で使用するのではなく、スマートイメージングを信頼して形式を選択できます。

スマートイメージングを利用することで、各ユーザーのブラウジング環境に合わせて、画像を可能な限り効率的に配信できます。このアプローチにより、プロセスが簡素化され、画像の読み込み時間と全体的なユーザーエクスペリエンスの観点からパフォーマンスが向上します。

詳しくは、[スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)を参照してください。

### 顧客へのアセットの配信後

**ビジネスケース：***新しいコンテンツを公開した後や、既存のコンテンツを上書きした後、CDN に変更をすぐに反映するにはどうすればよいですか？*

CDN （コンテンツ配信ネットワーク）は、Dynamic Media アセットをキャッシュして、顧客にすばやく配信します。これらのアセットに更新を行った際は、変更を web サイトにすぐに反映することが重要です。CDN キャッシュをパージまたは無効にすることで、Dynamic Media によって配信されるアセットをすばやく更新できます。このアプローチにより、通常 10 時間に設定されている TTL（有効期間）の値に基づいてキャッシュの有効期限が切れるのを待つ必要がなくなります。特定のユースケースに応じて、CDN TTL（有効期間）設定を適宜更新できます。

詳しくは、[Dynamic Media を使用した CDN キャッシュの無効化](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)を参照してください。

