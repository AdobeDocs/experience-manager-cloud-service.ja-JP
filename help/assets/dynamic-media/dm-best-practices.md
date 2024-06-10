---
title: Dynamic Mediaのベストプラクティス
description: 画像とビデオの操作に関しては、Dynamic Mediaのベストプラクティスについて説明します。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Video,Renditions, Configuration, Asset Management, Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
source-git-commit: e8594310a4d169995c4463c98140ac1c93350675
workflow-type: tm+mt
source-wordcount: '3574'
ht-degree: 0%

---

# Dynamic Mediaのベストプラクティスについて{#about-dm-best-practices}

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

組織は、ユーザーとのエンゲージメントのためのチャネルとデバイスの急拡大に直面しています。 カスタマージャーニーは、物理的な店舗、web、モバイル、ソーシャルメディア、電子メール、コマースにわたります。 この需要を満たすために、Dynamic Media on Adobe Experience Manager（AEM）は包括的なソリューションを提供します。 アセット配信を最適化し、パーソナライゼーションを処理し、チャネルやデバイスをまたいで、一貫性があり、パフォーマンスが高く、ブランドに合わせたエクスペリエンスを保証します。

Dynamic Mediaの主要な教義の一部を次に示します。

* **単一ファイル・アプローチ：** Dynamic Mediaでは、1 つのプライマリソースファイルを保存すると、すべてのサイズのバリエーションと視覚効果が配信時に動的に作成および最適化されます。 このアプローチにより、ストレージコストが削減され、ワークフローの複雑さが解消されます。
* **真にグローバル：** コンテンツ配信時に適用されるスマートイメージングは、画質を損なうことなく、画像サイズとページの重さを大幅に削減します。 ネットワーク帯域幅とデバイスのピクセル比に最適化されています。
* **AI を活用：** AI 駆動機能の 1 つであるスマート切り抜きは、画像およびビデオの POI 切り抜きを自動化します。 手作業をなくし、企業での使用に合わせて効率的に拡張できます。
* **簡単なビデオ：** プライマリソースビデオをDynamic Mediaにアップロードし、説明的なオーディオを使用して、複数の言語に適応的にストリーミングします。
* **Experience viewer ライブラリ：** 画像およびビデオのブランドエクスペリエンスビューアをでカスタマイズします。 これらのビューアは、デジタルエクスペリエンスにシームレスに統合されます。
* **新しい形式のサポート：** Dynamic Mediaでは、3D およびパノラマエクスペリエンスを配信できます。

を参照する際 [Dynamic Mediaジャーニー](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1)の機能を最大限に活用するには、以下のベストプラクティスの一覧を確認してください。 チャネルやデバイスをまたいでエクスペリエンスを最適化できるように、Dynamic Mediaのこれらのベストプラクティスを具体的なコンテキストやプロジェクト要件に合わせて調整します。

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>この記事のDynamic Mediaのベストプラクティスは、Dynamic Mediaの新しいテクノロジーが登場するにつれて、時間の経過と共に進化する可能性があります。 以下の情報は、Dynamic Mediaの最新バージョンに関するものです。


## Dynamic Mediaへのアセットの取り込み

**ビジネス ケース：** *大量のアセットを効率的に管理し、関連性が高く承認されたコンテンツのみをエンドユーザーに配信します。*

大量のアセットの管理を効率的に効率化します。 Dynamic Mediaを使用して、適切で承認済みのコンテンツのみがエンドユーザーに届くようにします。 **選択的同期** および **選択的公開** 機能。

* **選択的同期：**
Dynamic Mediaと同期するアセットを選択できるプロアクティブな機能。 例えば、最終承認を受けたアセットを含むフォルダーのみを同期するように指定できます。 このワークフローは、顧客への配信の準備をするアセットを管理するのに役立ちます。

* **選択的公開：**
アセットを同期した後に、選択的公開を使用すると、顧客に表示するアセットを制御できます。 つまり、どの承認済みアセットがチャネルを通じて実際に配信されるかを管理できるので、顧客に最適で関連性の高いコンテンツのみを表示できます。

これらの 2 つのベストプラクティスは、リッチメディアコンテンツに対するコントロール、ガバナンス、生産性の向上を実現するのに役立ちます。

詳細情報 に移動 [Dynamic Mediaのフォルダーレベルでの選択的公開の設定](/help/assets/dynamic-media/selective-publishing.md).


## 配信するアセットの準備

### アセットの整理

**ビジネス ケース：** *アセットを効率的に整理してワークフローを効率化します。*

ワークフローを効率化する効率的なアセット編成のために、次の 1 つ以上のベストプラクティスを使用します。

* **アセットをフォルダーに整理します。**
アセットを整理するには、コンピューター上のファイル編成と同様に、アセットをフォルダーに分類する必要があります。 これらのフォルダー内での適切な命名、サブフォルダーの構造化、ファイル管理は、アセット処理を効率的に行うために重要です。 体系的な命名規則とメタデータ手法を実装することで、デジタルアセットリポジトリのユーティリティを最大限に活用できます。
詳細情報 に移動 [フォルダー内のアセットの整理](/help/assets/organize-assets.md#organize-using-folders).
* **タグを使用したアセットの整理：**
アセットにタグを付けると、検索性、コレクションの作成および検索ランキングが向上します。 Adobe Senseiの AI は、正確なタグ付けのために自己学習アルゴリズムを採用しており、迅速なアセット取得を可能にします。 また、Adobe Senseiは、カスタムタグを含む関連するタグを認識してアセットに割り当てるため、説明を備えた自動タグ付けでアセット管理をシンプル化できます。
詳細情報 に移動 [タグを使用したアセットの整理](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **アセットをコレクションとして整理する：**
Dynamic MediaをExperience Manager Assetsと併用すると、アセットコレクションを効率的に作成、編集およびユーザー間で共有できます。 静的なリストや動的な検索ベースのコンパイルなど、様々なコレクションタイプを設定できます。 これらのコレクションタイプは、カスタマイズ可能なアクセス権と編集権を使用して、様々な場所で共有できます。
詳細情報 に移動 [アセットをコレクションとして整理する](/help/assets/manage-collections.md).
* **プロファイルを使用したアセットの整理：**
処理プロファイルは、指定フォルダーでのアセット処理を自動化し、組織を効率化します。 メタデータ、ファイル名およびフォルダー構造を標準化すると、デジタルアセットコレクションの拡大に合わせて、これらのプロファイルを一貫した正確に適用できます。
詳細情報 に移動 [プロファイルを使用したアセットの整理](/help/assets/organize-assets.md#organize-to-use-profiles).

### 画像の画質の最適化

**ビジネス ケース：** *Dynamic Mediaから高品質の画像を取得します。*

画質の向上には、さまざまな要素への配慮が必要です。 時間がかかるプロセスになる場合があります。 ただし、望ましい結果を得るのに役立つ、実証済みのプラクティスがいくつかあります。 これらのベストプラクティスには、最適な画像サイズ設定、画像のシャープニング、使用に最適な画像形式を取得する方法が含まれています。

詳細情報 に移動 [画像品質の最適化のベストプラクティス](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

画質に対する考え方は人によって異なるため、ときには望ましい結果を得るために、実験に対する体系的なアプローチが必要となります。 Adobe Experience Managerは、100 を超えるDynamic Media コマンドでこのプロセスを支援し、画像を強化します。

詳細情報 ウォッチ [Dynamic Media Snapshot](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) （3 分、17 秒）。

これらの様々なコマンドが画質に与える影響を評価するには、画像をDynamic Mediaにアップロードし、指定された URL でツールのインターフェイスを使用して、試したいコマンドを適用します。

試してみる？ ローンチ [Dynamic Media Snapshot](https://snapshot.scene7.com/)

### 画像に適用されるスタイルを標準化

**ビジネス ケース：** *画像アセットに適用するスタイルと変換を効率的に標準化します。*

Dynamic Mediaで画像プリセットを定期的に使用すると、画像のサイズ、形式、プロパティを一貫性のある動的な方法で調整できます。 画像プリセットは、マクロと考えることができます。サイズ変更と書式設定を行う名前付きのコマンドセットです。 例えば、デスクトップとモバイル用に特定の圧縮を使用して、様々なサイズと形式の製品画像がサイトで必要な場合は、画像プリセットによってこのプロセスが効率的に自動化されます。

試してみる？ に移動 [アセットをレンダリングするための画像プリセットの作成の基本](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### 画像やビデオのフォーカスとフレーミングの調整

**ビジネス ケース：** *画像やビデオの主要な目標点が、デバイス間で確実にフォーカスされるようにします。*

スマート切り抜きは、Dynamic Mediaの機能で、Adobeの AI および機械学習フレームワークであるAdobe Senseiを使用して、画像やビデオの切り抜きを自動化します。 画像やビデオの主要な被写体や注目点をインテリジェントに検出し、フォーカスします。 このインテリジェンスにより、デスクトップコンピューターやモバイルデバイスの様々な画面サイズで焦点が維持されます。

ベストプラクティスは、スマート切り抜きを使用して画像プロファイルを作成することです。 プロファイルでは、様々な画面サイズを定義し、残りの作業はAdobe Senseiに任せることで、画像やビデオを常にビューアのデバイスに最適化することができます。

詳細情報 ウォッチ [AEM Assets Dynamic Mediaでのスマート切り抜きの使用](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) （6 分 35 秒）および [ビデオに対するDynamic Media スマート切り抜きの使用](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) （6 分、22 秒）。

### SEO ランキングの向上

**ビジネス ケース：** *Dynamic Mediaを設定して、SEO ランキングを向上させます。*

画像が SEO 戦略全体に効果的に貢献するように、次の推奨事項を定期的に使用します。

* **意味のある画像ファイル名：**
画像の内容を反映したわかりやすいファイル名を使用します。 次に例を示します。
   * `myCompany-Silver-Wrist-Watch` を使用します
   * *回避する* `myCompany_Silver_Wrist_Watch` または `myCompanySilverWristWatch`

  これにより、検索エンジンが画像のコンテキストを理解し、SEO を向上させることができます。 Googleでは、ファイル名でアンダースコアやスペースよりもハイフンが優先されます。 また、ファイル名では単語を連結しないでください。
* **カスタムドメイン :**
会社またはブランド名を含むカスタムドメインを実装して、ブランドの認識と信頼を強化します。 次に例を示します。

   * `http://images.mycompany.com/is/image/companyname/` を使用します
   * *回避する* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`
* **SEO 対応のフォルダー構造：**
以下のようなインデックス作成を強化するために、会社名やブランドを含んだフォルダー構造で画像を整理します `http://images.mycompany.com/is/image/companyname/`.
* **Dynamic Media ルールセット：**
様々な要因に基づいて URL を条件付きで変換し、SEO とユーザーエクスペリエンスを強化する方法を説明します。
詳細情報 に移動 [ルールセットを使用した URL の変換](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **スマートイメージングとスマート切り抜き：**
Dynamic Mediaのスマートイメージング機能とスマート切り抜き機能を使用して、最適化されたレスポンシブな画像を提供します。 これにより、ページの読み込み時間が改善されるだけでなく、SEO ランキングにもプラスに貢献します。
詳細情報 に移動 [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md)、またはウォッチ [AEM Assets Dynamic Mediaでのスマート切り抜きの使用](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) （6 分、35 秒）。

これらのベストプラクティスは、Googleの画像 SEO のベストプラクティスとうまく一致していることを覚えておいてください。 このようなプラクティスでは、適切な命名規則、構造化データ、最適化された画像配信を通じて、コンテキストと明確さを検索エンジンに提供する重要性が強調されます。

詳細情報 に移動 [Googleの URL 構造のベストプラクティス](https://developers.google.com/search/docs/crawling-indexing/url-structure) および [Google画像 SEO のベストプラクティス](https://developers.google.com/search/docs/appearance/google-images)


### コマンドを使用してイメージをダイナミックに拡張し、視覚効果を作成する

**ビジネス ケース：** *画像にリッチな視覚効果を適用します。*

Dynamic Mediaには、画像を拡張し、視覚的な効果を動的に作成するための一連のコマンドが用意されています。静的なアセットを複数用意する必要はありません。 これらのプロセスの一部を簡単に説明し、例を示します。

#### ソース画像内のエフェクト

| タスク | 対処方法 |
| --- | --- |
| **元の画像をアップロードして公開する** | ・まず、元の画像をDynamic Mediaにアップロードします。<br>・ コンテンツが公開され、URL からアクセスできることを確認します。<br>・この例では、背景が白い時計のストック画像（「画像 X」と呼びましょう）がDynamic Mediaにアップロードされています。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer) |
| **マスクの作成** | ・件名（効果を適用する領域）と背景（変更する領域）を定義するマスクを作成します。<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer_maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer_maskps)<br>・通常、マスクはグレースケール画像です。白は被写体、黒は背景を表します。 Adobe Photoshopなどのツールを使用してマスクを作成できます。<br>詳細情報 に移動 [Photoshopでのクイックマスクの作成と編集](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).<br>・「画像 X」には、強調したい被写体を的確に輪郭を描いたマスクを作成。 例えば、人物、オブジェクトなど。 |
| **Dynamic Media URL コマンドを効果に適用する** | マスクを設定したら、URL コマンドを使用して、ドロップシャドウなどの効果を適用したり、背景色を「画像 X」に変更したりします。 次の 2 つの例があります。<br><br> ・ **ドロップシャドウ効果：**<br>&#x200B;件名の境界線に沿ってドロップシャドウ効果を追加するには、次のように URL を編集します。<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer_maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer_maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25)<br>この URL では、 `$shadow$` パラメーターはシャドウ効果を作成し、 `color=0,0,0` 影の色を黒に設定します。<br>・ **背景色の変更：**<br>&#x200B;背景色を変更するには、次のように異なる背景色の値を指定して URL を使用します。<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer_maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer_maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0)<br> この例では、 `color=255,255,0` 背景色を黄色に設定します。 視覚的な効果を得るために、背景を特定の色に編集します。 |

#### 画像の境界線の追加

Dynamic Mediaでは、URL を使用して画像を直接操作できるので、動的なデジタルエクスペリエンスを作成するための強力なツールになります。 以下に例を示します。 まず、次の元の画像 URL から見てみましょう。 [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| タスク | 対処方法 |
| --- | --- |
| **白い境界線** | 白い境界線を追加するには、次の URL を使用します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10)<br>この URL では、 `extend=10,10,10,10` パラメーターは、すべての辺の境界線のサイズを 10 ピクセルに指定します。 |
| **白い境界線に沿ってぼかします** | 白い境界線に沿ってブラー効果を追加するには、次のように URL を編集します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0)<br>この URL では、 `effect=-1` パラメータはブラー効果を適用し、 `op_blur=60` ブラーの強度を制御します。 |
| **外側の境界に沿ったドロップシャドウ効果** | 外側の境界に沿ってドロップシャドウ効果を追加するには、次の URL を使用します。<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g10.scene7.com/is/image/genaibeta/AdobeStock_754660022?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0)<br>この `$shadow$` パラメーターはシャドウ効果を作成し、 `color=0,0,0` 影の色を黒に設定します。 |

これらの URL を自由に試して、目的の視覚効果を実現してください。

#### 画像オーバーレイの作成

既存の画像にロゴやアイコンを重ねたい場合は、Dynamic Mediaの URL コマンドを使用すると簡単に行うことができます。 手順を分解しましょう。

| 手順 | 対処方法 |
| --- | --- |
| **ベース画像をアップロードして公開する** | まず、ロゴまたはアイコンを重ね合わせるベース画像をアップロードして公開します。 任意の画像をベースとして使用できます。<br>例えば、次にベース画像を示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **ロゴまたはアイコン画像をアップロードして公開する** | 次に、ベース画像にスーパーインポーズする画像をアップロードして公開します。 この画像は、オーバーレイするロゴまたはアイコンを含む透明 PNG である必要があります。<br>次に、重ね合わせる透明効果を持つ星オブジェクトの透明 PNG 画像を示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Dynamic Media URL を適用** | 次に、ベース画像とロゴまたはアイコン画像を組み合わせたDynamic Media URL を作成します。 URL コマンドを使用すると、この効果を実現できます。<br>URL 構造は次のようになります。<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png)<br>ここで、<br>・ `hotspotRetailBaseImage` はベース画像です。<br>・ `starxp` はロゴ / アイコンの画像です。<br>・ `layer=1` ロゴまたはアイコンを基本画像の上に重ねて表示するように指定します。<br>・ `scale=1.25` ロゴ/アイコンのサイズを調整します。<br>・ `posN=0.33,-.25` ロゴ/アイコンの基本画像を基準とした位置を決定します。<br>・ `fmt=png` 出力が PNG 形式であることを確認します。 |

詳細情報 に移動 [src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) の詳細 `src` コマンドおよびその他のDynamic Media URL コマンド。


#### プロモーションテキストのオーバーレイ

HTMLと CSS を使用してプロモーションテキストメッセージを画像にオーバーレイする手順を以下に示します。

| 手順 | 対処方法 |
| --- | --- |
| **ベース画像をアップロードして公開する** | まず、テキストを重ね合わせるベース画像をアップロードして公開します。 任意の画像を使用できます。 例えば、ベース画像のサンプルを次に示します。<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Dynamic Mediaのテキスト演算子の適用** | Dynamic Mediaを使用すると、テキスト演算子を適用して、画像に直接ダイナミックテキストをオーバーレイできます。 次のサンプル URL は、この機能を示しています。<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fontbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fontbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF333&amp;wid=600&amp;hei=600) |

#### 様々なユースケースでのサイズ変更と切り抜き

##### 画像のサイズ変更の基本事項

画像のサイズ変更には、画像のサイズ、解像度およびファイルサイズの変更が含まれます。 考慮すべき重要なポイントを次に示します。

* **ピクセル構成：**
デジタル画像は、ピクセルと呼ばれる小さな点で構成されています。 画像を作成すると、特定のピクセル数になります。 サイズを変更するには、ピクセルを追加または減算して、画像のサイズ、解像度およびファイルサイズを変更します。
* **縦横比：**
歪みを防ぐには、縦横比（幅と高さの関係）を維持することが重要です。 画像を拡大する場合（アップスケーリング）でも縮小する場合（ダウンスケーリング）でも、縦横比を維持することで視覚的な一貫性を確保できます。
* **品質に関する考慮事項**
サイズ変更は、画質に影響を与える場合があります。 ピクセル化につながる可能性があるので、大幅なアップスケーリングは避けます。 代わりに、より大きなサイズと解像度で画像を再現することを検討してください。 画像が小さい場合は、適切なツールを使用して解像度を維持します。

##### 切り抜きとサイズ変更

切り抜きとサイズ変更は、Dynamic Mediaのテクニックで、サムネール、商品ディスプレイ画像、バナーなどを作成する場合でも、様々なユースケースに合わせて画像を変換できます。

* **切り抜き：**
画像の一部を削除して、構成とフレームを変更します。 全体の寸法は変更されませんが、特定の領域に焦点を当てます。
* **サイズ変更：**
縦横比を維持しながら、画像全体の寸法、解像度、ファイルサイズを調整します。

次のリビングルームの画像を含むユースケースを見てみましょう。

* **リビングのオリジナル画像：**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **サムネール （200 ピクセル x 200 ピクセル）:**
すばやく読み込んだり表示したりするのに適した小さいバージョン。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop)
* **切り抜き付きサムネール（200 ピクセル x 200 ピクセル）:**
ソファエリアに焦点を当てるために切り抜きました。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **製品表示画像（800 ピクセル x 600 ピクセル）:**
ソファを表示するために切り抜いてサイズ変更しました。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **バナー（1720 ピクセル x 820 ピクセル）:**
元の画像から派生し、部屋を強調します。
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop)

具体的なニーズに合わせて、これらのバリエーションを自由に調べることができます。
URL 内で使用できるコマンドについて詳しくは、 に移動 [コマンドリファレンス](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### Web サイトのビデオを公開する

**ビジネス ケース：** *マーケティングサイトのビデオをすばやく公開します。*

* **ビデオプロファイルを選択します。**
まず、Dynamic Mediaで適切なビデオプロファイルを選択する必要があります。 を選択できます *アダプティブビデオエンコーディング* プロファイルは、AEM Assetsの「ビデオプロファイル」で使用できます。 これらの事前定義されたエンコーディング設定により、様々なデバイスや帯域幅の条件で再生できるようにビデオが最適化されます。 または、独自のアダプティブビデオプロファイルを作成することもできます。
* **プロファイルを割り当てます。**
選択したビデオプロファイルを、ビデオのアップロード先フォルダーに割り当てます。 この手順により、アップロードプロセス中に正しいエンコーディング設定が適用されるようになります。
* **オリジナルビデオをアップロードします。**
元のビデオファイルをアップロードします。 高画質のビデオであることを確認してください。 ソースビデオが良いほど、最終結果も良くなります。
* **プレビューと公開：**
ビデオをプレビューして、すべてが期待どおりに表示されることを確認します。 満足したら、公開します。 この手順により、オーディエンスがビデオにアクセスできるようになります。
* **リンクまたは埋め込み：**
公開後、次の 2 つのオプションがあります。
   * **直接リンク：**
指定された URL を使用して、ビデオに直接リンクします。 マーケティングサイトで適切にハイパーリンクを設定します。
   * **ビデオを埋め込みます。**
提供された埋め込みコードをコピーして、Web ページのビデオを表示するHTMLーに貼り付けます。 これにより、ビデオをサイトで直接再生できます。

詳細情報 に移動 [ビデオ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### 最適な品質とエンゲージメントのためのビデオの設定

**ビジネス ケース：** *最高の品質とエンゲージメントを得るために、ビデオを設定します。*

ビデオの品質とエンゲージメントを最適なものにするには、次のベストプラクティス戦略を組み合わせて実装することを検討してください。

* **組み込みのHTML5 ビデオビューアを使用します。**
Dynamic Media HTML5 ビデオビューアプリセットは、堅牢なビデオプレーヤーです。 これらを使用すると、HTML5 ビデオの再生とモバイルデバイスに関連するよくある問題を回避できます。
これらのプリセットは、アダプティブビットレートストリーミング配信やデスクトップブラウザーの限られたリーチなどの課題に対処します。
詳細情報 に移動 [ベストプラクティス：HTML 5 ビデオビューアの使用](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **Dynamic Media ビデオプロファイルを使用します。**
Dynamic Mediaのビデオプロファイルは、効率的なビデオ管理、一貫した画質およびアダプティブストリーミングに役立ちます。
詳細情報 に移動 [Dynamic Media ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md).

* **ビデオエンコーディングのベストプラクティスに従います。**
エンコード時に過度のダウンスケーリングを行わずに元のビデオ品質を維持するビデオエンコーディングプロファイルを適用します。
詳細情報 に移動 [ビデオエンコーディングのベストプラクティス](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **プログレッシブストリーミングの代わりにアダプティブストリーミングを採用する：**
アダプティブストリーミングは、ビューアのインターネット接続速度とデバイス機能に基づいてビデオ品質を調整します。
HLS （HTTP ライブストリーミング）や DASH （`Dynamic Adaptive Streaming over HTTP`）を選択して、最適な再生品質を確保します。
ビデオを線形に配信するプログレッシブストリーミングとは異なり、アダプティブストリーミングはバッファリングを最小限に抑え、シームレスな視聴エクスペリエンスを提供します。

* **アカウントで DASH を有効にする（HTTP でのデジタルアダプティブストリーミング）:**
DASH は、アダプティブストリーミングを使用してビデオコンテンツを動的に提供します。
DASH を有効にするには、環境のサポートチケットを作成します。
詳細情報 に移動 [Dynamic Media アカウントで DASH を有効にする](/help/assets/dynamic-media/video.md#enable-dash).

### 多言語消費のためのビデオの国際化

**ビジネス ケース：** *ビデオを多言語消費に対応させます。*

多言語消費のためのビデオの国際化は、グローバルオーディエンスにリーチするために不可欠です。 Dynamic Mediaには、この目標を達成するのに役立つ機能が用意されています。

* **ビデオをアップロードします。**
   * まず、ビデオエンコーディングプロファイルを作成します。 Dynamic Mediaに付属している事前定義済みのアダプティブビデオエンコーディングプロファイルを使用するか、独自のカスタムプロファイルを作成できます。
   * プライマリソースビデオをアップロードする 1 つ以上のフォルダーにビデオ処理プロファイルを関連付けます。
   * これらのフォルダーにプライマリソースビデオをアップロードします。 Dynamic Mediaは、割り当てられたビデオ処理プロファイルに基づいてそれらをエンコードします。
   * Dynamic Mediaは主に、最小解像度が 25 × 25 を超える短時間（最大 30 分）のビデオをサポートします。 15GB までの動画ファイルをアップロードできます 1.

* **ビデオを管理：**
   * AEM内のビデオアセットを整理、参照および検索します。
   * ビデオアセットのプレビューと公開。
   * ソースビデオとそのエンコードされたレンディションを、関連するサムネールと共に表示します。
   * タイトル、説明、タグ 2 など、ビデオのプロパティを編集します。

* **ローカライゼーション：**
   * ターゲットの地域/言語ごとに、オーディオトラックとサブタイトルを作成します。
   * AEM インターフェイスからこれらのオーディオトラックとサブタイトルトラックをビデオに追加します。
   * ユーザーがビデオを再生する際に、オーディオとサブタイトルで優先言語を選択できます。

* **公開中：**
   * AEMを Web コンテンツ管理（WCM）システムとして使用している場合は、web ページにビデオを直接追加できます。
   * サードパーティの WCM システムを使用している場合は、URL または埋め込みコードを使用して、web ページにビデオをリンクまたは埋め込むことができます。

詳細情報 に移動 [Dynamic Mediaでのビデオの複数キャプションおよびオーディオトラックのサポートについて](/help/assets/dynamic-media/video.md#about-msma) または時計 [ビデオへの複数のキャプションとオーディオトラックの追加](https://delivery-p106302-e1008131.adobeaemcloud.com/adobe/assets/urn:aaid:aem:daf9a222-9f7f-4333-b167-98cb4c63a1f8/play) （1 分、41 秒）。


## 顧客へのアセットの配信

### 画像サイズを最適化し、ページの読み込み時間を最小限に抑える

**ビジネス ケース：** *ブラウザーまたは画面の画像のサイズを最適化し、ページの読み込み時間を短縮します。*

Dynamic Media スマートイメージングは、クライアントのブラウザーの機能に応じて画像の形式、サイズ、画質を自動的に最適化することで、画像配信のパフォーマンスを向上させる強力なツールです。

Adobeでは、画像フォーマットを手動でに設定するのではなく、スマートイメージングの機能を使用することをお勧めします。 `webp` または `avif`. 理由は次のとおりです。

* **ブラウザーの互換性：**
スマートイメージングは、配信される画像形式がユーザーのブラウザーと互換性があることを保証します。
* **最適な圧縮：**
特定のブラウザー、ネットワーク条件、画面の解像度に基づいて、圧縮に最適な形式を選択します。
* **最新の形式：**
While `avif` は、より高い圧縮を提供する新しい形式です。まだ、すべてのブラウザーで広くサポートされているわけではありません。
* **ベストプラクティス：**
Web に最適な形式を保証するには、コマンドを手動で使用するのではなく、スマートイメージングを信頼して形式を選択します `fmt=webp` または `fmt=avif`.

スマートイメージングを利用すると、各ユーザーの閲覧環境に合わせて、可能な限り効率的に画像を配信できます。 このアプローチにより、プロセスが簡素化され、画像の読み込み時間と全体的なユーザーエクスペリエンスの観点からパフォーマンスが向上します。

詳細情報 に移動 [スマートイメージング](/help/assets/dynamic-media/imaging-faq.md).

