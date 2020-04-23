---
title: スマートイメージング
description: スマートイメージングでは、各ユーザーに固有の閲覧特性を利用して、ユーザーのエクスペリエンス用に最適化された適切な画像を自動的に提供することで、より良いパフォーマンスとエンゲージメントをもたらします。
translation-type: tm+mt
source-git-commit: a934f28f74f0ff9ae68d7507290851dc5ca907e5

---


# スマートイメージング {#smart-imaging}

## What is &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

スマートイメージングテクノロジーは、Adobe Sensei AIの機能を活用し、既存の「画像プリセット」と連携して、クライアントのブラウザーの機能に基づいて画像形式、サイズ、画質を自動的に最適化し、画像配信のパフォーマンスを向上します。

また、スマートイメージングは、アドビのクラス最高のプレミアムCDNサービスと完全に統合され、パフォーマンスが向上するという利点もあります。 このサービスが、サーバー、ネットワークおよびピアリングポイント間を結ぶ、最適なインターネットルートを見つけます。最適なインターネットルートとは、待ち時間が最小限であったり、インターネット上のデフォルトルートよりもパケット損失率が低かったりするルートです。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| Image<br>(URL) | サムネール | サイズ<br> (JPEG) | サイズ(WebP)<br> （スマートイメージングを使用） | %削減 |
|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [画像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

上記と同様に、アドビでは、7,009 URLのテストも実施し、スマートイメージングの機能により、JPEGのファイルサイズ最適化を平均で38%、WebP形式のPNGのファイルサイズ最適化を31%向上させました。

## What are the key benefits of the latest Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

画像はページの読み込み時間の大部分を占めるので、パフォーマンスの向上は、コンバージョン率、サイトでの滞在時間、サイトの直帰率の低下など、ビジネスKPIに大きな影響を与える可能性があります。

最新バージョンのスマートイメージングの機能強化：

* 最適化されたコンテンツを即座に（実行時に）提供します。
* Adobe Sensei技術を使用して、イメージリクエストで指定された品質(qlt)に従って変換します。
* スマートイメージングは、「bfc」 URLパラメータを使用してオフにできます。
* TTL(Time To Live)非依存。 以前は、スマートイメージングを機能させるには、最小TTL値の12時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされ、キャッシュを無効にする2つの手順が必要でした。 最新のスマートイメージングでは、派生物のみがキャッシュされ、1ステップのキャッシュ無効化プロセスが可能です。
* ルールセットでカスタム接触チャネルを使用するお客様(例： [Adding a custom header value to image responses|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html))は、以前のバージョンのスマートイメージングとは異なり、ブロックされないので、最新のスマートイメージングを利用できます。

## スマートイメージングにはライセンス費用がかかりますか？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

いいえ。スマートイメージングは、Dynamic Media Classic(Scene7)またはAEM Dynamic Media(On Prem、AMS、AEM as a Cloud Service)の既存のライセンスに含まれています。

>[!NOTE]
>
>スマートイメージングは、ダイナミックメディア — ハイブリッドのお客様はご利用いただけません。


## スマートイメージングはどのように機能しますか？ {#how-does-smart-imaging-work}

スマートイメージングは、Adobe Senseiを使用して、ブラウザの機能に基づいて、最も最適な形式、サイズ、画質に画像を自動的に変換します。

* Chrome、Firefox、Microsoft Edge、Android、Operaなどのブラウザー用のWebPに自動的に変換します。
* Safariなどのブラウザーでは、JPEG2000に自動的に変換されます。
* Internet Explorer 9以降などのブラウザーでは、自動的にJPEGに変換されます。
* これらの形式をサポートしていないブラウザーでは、最初に要求された画像形式が提供されます。

元の画像のサイズがスマートイメージングの生成サイズより小さい場合は、元の画像が提供されます。

## What image formats are supported? {#what-image-formats-are-supported}

スマートイメージングでは、次の画像形式がサポートされています。
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## How does Smart Imaging work with our existing image presets that are already in use? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

スマートイメージングは既存の「画像プリセット」と連携し、要求されたファイル形式がJPEGまたはPNGの場合、画質(qlt)と形式(fmt)を除くすべての画像設定を監視します。 形式変換の場合、画像プリセットの設定で定義されているとおりの完全な視覚的忠実性が維持されますが、ファイルサイズは小さくなります。元の画像のサイズがスマートイメージングの生成サイズより小さい場合は、元の画像が提供されます。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Will I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

いいえ。スマートイメージングは、既存の画像URLや画像プリセットとシームレスに連携します。 また、スマートイメージングでは、ユーザのブラウザを検出するためにWebサイトにコードを追加する必要はありません。 これらはすべて自動的に処理されます。

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

Also, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) スマートイメージングの前提条件を理解する。

## スマートマージングはHTTPSで機能しますか？ How about HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

スマートイメージングは、HTTPまたはHTTPS経由で配信される画像と連動します。 また、HTTP/2でも機能します。

## スマートイメージングを使用するための資格を私は満たしていますか？ {#am-i-eligible-to-use-smart-imaging}

スマートイメージングを使用するには、会社のAEMアカウント上のダイナミックメディアクラシックまたはダイナミックメディアが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン(、、、など `images.company.com` )ではな `mycompany.scene7.com`く、専用ドメイン(例えば、ま `s7d1.scene7.com`たは `s7d2.scene7.com`)を使用し `s7d13.scene7.com`ます。

 自社のドメインを調べるには、会社のアカウントにログインします。

**[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をタップします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用トランジションを使用している場合は、テクニカルサポートチケットを送信する際に、このドメインの一部として独自のカスタムドメインに移動するように要求できます。

最初のカスタムドメインは、ダイナミックメディアライセンスを使用する場合に追加費用はかかりません。

## What is the process for enabling Smart Imaging for my account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

スマートイメージングを使用するためのリクエストを開始する必要があります。自動的には有効になりません。

1. Initiate a Technical Support request (email: `s7support@adobe.com`).
1. サポートリクエストには、以下の情報を記入してください。

   1. 主要連絡先の氏名、電子メールアドレス、電話番号。
   1. All domains to be enabled for smart imaging (that is, `images.company.com` or `mycompany.scene7.com`).

       自社のドメインを調べるには、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。
   1. 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。
   1. `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

       自社のドメインを調べるには、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media Classic ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。
   1. HTTP/2でも動作させる必要があるかどうかを示します。

1. テクニカルサポートは、要求が送信された順序に基づいて、スマートイメージングの顧客待機リストにユーザーを追加します。
1. 要求を処理する準備が整った時点で、テクニカルサポートから連絡を差し上げ、調整と日取り設定をおこないます。
1. **オプション**:アドビが新機能を実稼働環境にプッシュする前に、ステージングでスマートイメージングをテストするオプションがあります。
1. 完了後、サポートから通知があります。
1. スマートイメージングのパフォーマンス向上を最大限に高めるため、Adobeでは、Time To Live(TTL)を24時間以上に設定することをお勧めします。 TTL によって定義されるのは、アセットが CDN によってキャッシュされる期間です。この設定を変更するには、次の手順を実行します。

   1. Dynamic Media Classic を使用している場合は、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。「**[!UICONTROL 初期設定のクライアントキャッシュの有効期限]**」の値を 24 以上に設定します。
   1. ダイナミックメディアを使用する場合は、次の手 [順に従いま](config-dm.md)す。 Set the **[!UICONTROL Expiration]** value 24 hours or longer.

## When can I expect my account to be enabled with Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

リクエストは、テクニカルサポートに到着した順序で、待ちリストに従って処理されます。

>[!NOTE]
スマートイメージングを有効にすると、アドビがキャッシュをクリアするので、リードタイムが長くなる可能性があります。 そのため、処理できる移行の数は、常にほんの数件です。

## What are the risks with switching over to use Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

顧客のWebページが表示されるリスクはありません。 ただし、AEM上のDynamic Media Classicまたはダイナミックメディアの新しい設定に移行するので、スマートイメージングのトランジションによってCDNのキャッシュがクリアされることに注意してください。

最初の切り替え中、キャッシュが再構築されるまでの間は、アドビの起点サーバーにあるキャッシュされない画像が直接ヒットします。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。ほとんどのお客様につきましては、CDN のキャッシュが完全に再構築されるまでに要する時間は 1～2 日です。

## スマートイメージングが想定どおりに機能しているかどうかを確認するには、どうすればいいですか？ {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. アカウントにスマートイメージングを設定したら、ブラウザにDynamic Media Classic(Scene7)/ダイナミックメディア画像のURLを読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示／デベロッパー／デベロッパーツール]**&#x200B;をクリックしてデベロッパーパネルを開きます。または、任意のブラウザー開発者ツールを選択します。

1. デベロッパーツールを開いたときにキャッシュが無効化されるようにします。

   * On Windows – navigate to settings in the developer tool pane, then select **[!UICONTROL Disable cache (while devtools is open)]** checkbox.
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome上のWebPに動的に変換されるPNG画像を示しています。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
すべての画像が変換されるわけではありません。スマートイメージングは、パフォーマンスを向上させるために変換が必要かどうかを判断します。 場合によっては、期待されるパフォーマンスの向上がない場合や、形式がJPEGやPNGでない場合、画像は変換されません。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 要求に対してスマートイメージングをオフにできますか？ {#turning-off-smart-imaging}

はい。URLに修飾子を追加することで、スマートイメージングをオ `bfc=off` フにできます。

## どのような「チューニング」を利用できますか。 定義できる設定や動作はありますか。 (#tuning-settings)

現在、オプションでスマートイメージングを有効または無効にできます。 他のチューニングは使用できません。

## スマートイメージングが画質設定を管理する場合、設定できる最小値と最大値はありますか。 例えば、「60以下」と「80以下」の画質を設定できますか。 (#minimum-maximum)

現在のスマートイメージングには、このようなプロビジョニング機能はありません。

## 場合によっては、WebP画像ではなくJPEG画像がChromeに返されます。 なぜそうなるの？ (#jpeg-webp)

スマートイメージングは、変換が有益かどうかを判断します。 変換結果のファイルサイズが小さく、画質も同等の場合にのみ、新しい画像が返されます。
