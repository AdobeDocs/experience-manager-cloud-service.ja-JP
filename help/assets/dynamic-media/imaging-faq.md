---
title: スマートイメージング
description: スマートイメージングでは、各ユーザーに固有の閲覧特性を利用して、ユーザーのエクスペリエンス用に最適化された適切な画像を自動的に提供することで、より良いパフォーマンスとエンゲージメントをもたらします。
translation-type: tm+mt
source-git-commit: e4d75f8bb783df57705bcaa6483bcb0ac6ec7ead
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 79%

---


# スマートイメージング {#smart-imaging}

## スマートイメージングとは {#what-is-smart-imaging}

スマートイメージングテクノロジーは、Adobe Senesi AI の機能を活用して、既存の「画像プリセット」と連携してクライアントのブラウザーの機能に基づいて、画像形式、サイズ、画質を自動的に最適化し、配信パフォーマンスを向上します。

スマートイメージングをアドビのクラス最高のプレミアム CDN サービスと完全に統合することで、パフォーマンスを大幅にアップさせることもできます。このサービスが、サーバー、ネットワークおよびピアリングポイント間を結ぶ、最適なインターネットルートを見つけます。最適なインターネットルートとは、待ち時間が最小限であったり、インターネット上のデフォルトルートよりもパケット損失率が低かったりするルートです。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| 画像 <br>（URL） | サムネール | サイズ<br>（JPEG） | サイズ（WebP）<br>（スマートイメージングを使用） | % 削減 |
|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [画像 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均 = 51% |

上記と同様に、アドビでも 7009 個の URL を含むテストを実施し、スマートイメージングの機能により、JPEG 用のファイルサイズの平均最適化を 38%、WebP 形式の PNG 用のファイルサイズの最適化を 31%達成しました。

## 最新のスマートイメージングの主要なメリットとは {#what-are-the-key-benefits-of-smart-imaging}

ページのロード時間の大部分は画像のロード時間なので、画像配信パフォーマンスの向上は、ビジネス上の KPI（より高いコンバージョン率、より長いサイト滞在時間、より低いサイト直帰率）に多大な影響を与えます。

最新バージョンのスマートイメージングの機能強化：

* 最適化されたコンテンツをすぐに提供（実行時）
* Adobe Sensei テクノロジーを使用して、イメージリクエストで指定された品質（qlt）に従って変換します。
* スマートイメージングは、「bfc」 URL パラメータを使用してオフにできます。
* TTL（Time To Live）独立。以前は、スマートイメージングを機能させるには、最小 TTL 値 12 時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされていて、キャッシュを無効にする 2 つの手順がありました。最新のスマートイメージングでは、派生画像のみがキャッシュされ、1 ステップのキャッシュ無効化プロセスが可能です。
* ルールセットにカスタムヘッダーを使用する顧客（例：[画像応答へのカスタムヘッダーの追加 ｜ Dynamic Media Classic](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html) で提案されている「Timing Allow Origin」、「X-Robot」）は、以前のバージョンのスマートイメージングとは異なり、ヘッダーがブロックされないため、最新のスマートイメージングを活用できます。

## スマートイメージングにはライセンス費用がかかりますか？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

いいえ。スマートイメージングは、Dynamic Media Classic（Scene7）または AEM Dynamic Media（オンプレミス、AMS、AEM as a Cloud Service）の既存のライセンスに含まれています。

>[!NOTE]
>
>スマートイメージングは、Dynamic Media – ハイブリッドの顧客はご利用いただけません。


## スマートイメージングはどのように機能しますか？ {#how-does-smart-imaging-work}

ユーザーから画像が要求された場合、ユーザーの特性を確認し、使用中のブラウザーに基づいて適切な画像形式に変換します。 これらの形式の変換は、表示の忠実度を低下させない方法で行われます。 スマートイメージングは、次の方法で、ブラウザの機能に基づいて画像を異なる形式に自動的に変換します。

* 次のブラウザー用にWebPに自動的に変換：
   * Chrome
   * Firefox 以降
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14のみ（iOS 14.0以降およびmacOS BigSur以降）
   * Android
   * Opera
* レガシーブラウザーでの次のサポート：

   | ブラウザー | ブラウザー/OSのバージョン | 形式 |
   | --- | --- | --- |
   | Safari | iOS 14.0以前 | JPEG2000 |
   | Edge | 十八以前 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 上記形式をサポートしていないブラウザーの場合は、元々要求された画像形式が提供されます。

元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

## どんな画像形式がサポートされていますか？ {#what-image-formats-are-supported}

スマートイメージングでは次の画像形式がサポートされています。
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## スマートイメージングは、使用中の既存の画像プリセットとどのように連携しますか？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

スマートイメージングは既存の「画像プリセット」と連携し、要求されたファイル形式が JPEG または PNG の場合は、画質（qlt）および形式（fmt）を除くすべての画像設定を監視します。形式変換の場合、画像プリセットの設定で定義されているとおりの完全な視覚的忠実性が維持されますが、ファイルサイズは小さくなります。元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## スマートイメージングを使用する場合、URL の変更や、画像プリセットの変更、サイトへの新しいコードのデプロイなどは必要ですか？{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

スマートイメージングは、既存のカスタムドメインでスマートイメージングを設定する場合、既存の画像URLや画像プリセットとシームレスに連携します。 また、スマートイメージングでは、ユーザーのブラウザーを検出するために Web サイトにコードを追加する必要はありません。これらはすべて自動的に処理されます。

スマートイメージングを使用するために新しいカスタムドメインを設定する必要がある場合は、このカスタムドメインを反映するようにURLを更新する必要があります。

また、スマートイメージングの前提条件を理解するには、[スマートイメージングを使用するための資格を私は満たしていますか？](#am-i-eligible-to-use-smart-imaging)を参照してください。

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## スマートイメージングは HTTPS で機能しますか？HTTP/2 ではどうですか？{#does-smart-imaging-working-with-https-how-about-http}

スマートイメージングは、HTTP または HTTPS で配信された画像に対して機能します。また、HTTP/2 上でも機能します。

## スマートイメージングを使用するための資格を私は満たしていますか？ {#am-i-eligible-to-use-smart-imaging}

スマートイメージングを使用するには、貴社の Dynamic Media Classic アカウントまたは Dynamic Media on AEM アカウントが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン（例えば、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` など）ではなく、専用ドメイン（例えば、`images.company.com` または `mycompany.scene7.com`）を使用してください。

 自社のドメインを調べるには、会社のアカウントにログインします。

**[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をタップします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用ドメインを使用している場合は、この切り替えの一部として、テクニカルサポートチケットを送信するときに、独自のカスタムドメインへの移行を要求できます。

最初のカスタムドメインは、Dynamic Media ライセンスを使用する場合、追加費用はかかりません。

## 自分のアカウントでスマートイメージングを有効にするには、どうすればいいですか？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

スマートイメージングを使用するためのリクエストを開始する必要があります。自動的には有効になりません。

1. [Admin Consoleを使用して、サポートケースを作成します。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. サポートケースに次の情報を入力します。

   1. 主要連絡先の氏名、電子メールアドレス、電話番号。
   1. スマートイメージングを有効にする全ドメイン（`images.company.com` や `mycompany.scene7.com`）。

       自社のドメインを調べるには、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。
   1. 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。
   1. `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

       自社のドメインを調べるには、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media Classic ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。
   1. HTTP/2 上で機能させる必要もある場合は、その旨を記載します。

1. テクニカルサポートでは、要求が送信された順序に基づいて、スマートイメージングカスタマー待ちリストに貴社を追加します。
1. 要求を処理する準備が整った時点で、テクニカルサポートから連絡を差し上げ、調整と日取り設定をおこないます。
1. **オプション**：アドビが実稼働環境にスマートイメージングをプッシュする前に、この新機能をステージングでテストするためのオプションがあります。
1. 完了後、サポートから通知があります。
1. スマートイメージングのパフォーマンス向上を最大限にするため、アドビでは、有効期間（TTL）を 24 時間以上に設定することを推奨しています。TTL によって定義されるのは、アセットが CDN によってキャッシュされる期間です。この設定を変更するには、次の手順を実行します。

   1. Dynamic Media Classic を使用している場合は、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。「**[!UICONTROL 初期設定のクライアントキャッシュの有効期限]**」の値を 24 以上に設定します。
   1. Dynamic Media を使用する場合は、[次の手順](config-dm.md)に従います。「**[!UICONTROL 有効期限]**」の値を 24 時間以上に設定します。

## 自分のアカウントでスマートイメージングが有効になるのはいつ頃ですか？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

リクエストは、テクニカルサポートに到着した順序で、待ちリストに従って処理されます。

>[!NOTE]
リードタイムが長くなる場合がありますが、それは、スマートイメージングを有効化するためには、アドビによるキャッシュのクリアが必要になるからです。そのため、処理できる移行の数は、常にほんの数件です。

## スマートイメージングを使用するための切り替えに際しては、どんなリスクがありますか？{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

顧客の Web ページを表示するリスクはありません。ですが、スマートイメージングへの切り替えには、Dynamic Media Classic または Dynamic Media on AEM の新規構成への移行が伴うので、スマートイメージングに切り替えると、CDN のキャッシュが消去されることを認識する必要があります。

最初の切り替え中、キャッシュが再構築されるまでの間は、アドビの起点サーバーにあるキャッシュされない画像が直接ヒットします。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。ほとんどのお客様につきましては、CDN のキャッシュが完全に再構築されるまでに要する時間は 1～2 日です。

## スマートイメージングが想定どおりに機能しているかどうかを確認するには、どうすればいいですか？ {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. アカウントにスマートイメージングが設定されたら、ブラウザーで、Dynamic Media Classic（Scene7）／Dynamic Media の画像の URL を読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示／デベロッパー／デベロッパーツール]**&#x200B;をクリックしてデベロッパーパネルを開きます。または、別のブラウザーのデベロッパーツールを使用します。

1. デベロッパーツールを開いたときにキャッシュが無効化されるようにします。

   * Windows - デベロッパーツールパネルの「Settings」に移動してから、「**[!UICONTROL Disable cache (while devtools is open)]**」チェックボックスを選択します。
   * Mac - デベロッパーパネルの「**[!UICONTROL Network]**」タブで、「**[!UICONTROL disable cache]**」を選択します。

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome 上で PNG 画像が動的に WebP に変換されているのを示しています。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
すべての画像が変換されるわけではありません。スマートイメージングは、パフォーマンスを向上させるために変換が必要かどうかを判別します。予期されるパフォーマンスゲインがない場合や、形式が JPEG や PNG でない場合、画像は変換されません。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## パフォーマンスの向上を知る方法 スマート・イメージングのメリットをメモする方法はありますか。 {#performance-gain}

**スマートイメージング・ヘッダーについて**

Smart Imagingのヘッダ値は、キャッシュ以外の要求が現在の時点で処理される場合にのみ機能します。 これは、現在のキャッシュの互換性を維持するために行われ、キャッシュを介して画像が提供される場合に計算を行う必要がなくなります。

スマートイメージングヘッダーを使用するには、リクエストに`cache=off`修飾子を追加する必要があります。 ダイナミックメディア画像サービング[](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-cache.html) /レンダリングAPIのキャッシュを参照してください。

使用例 `cache=off` （説明用のみ）:

`https://domain.scene7.com/is/image/companyName/imageName?cache=off` 

このようなリクエストを使用した後、「応答ヘッダー」セクションにヘッダーが表示され `-x-adobe-smart-imaging` ます。 次のスクリーンショットを参照してください(ハイライト表示されて `-x-adobe-smart-imaging` います)。

![スマートイメージング・ヘッダ](/help/assets/assets-dm/smart-imaging-header2.png) 

このヘッダー値は、次のことを示します。

* スマートイメージングが会社で動作しています。
* 正の値(>=0)は、変換が成功したことを示します。 この場合、新しい画像（ここではwebP）が返されます。
* 負の値(&lt;0)は、変換が成功しなかったことを示します。 この場合、元の要求された画像が返されます（指定しない場合は、デフォルトでJPEGが返されます）。
* この値は、要求された画像と新しい画像のバイト数の差を示します。 この場合、保存されるバイト数は75048で、1つのイメージの場合は約75 KBです。 
   * 負の値は、要求された画像が新しい画像より小さかったことを示します。 負のサイズの差は表示されますが、提供される画像は元の要求された画像のみです

**スマートイメージングヘッダーを使用するタイミング**

スマートイメージング応答ヘッダーは、デバッグ目的で有効にするか、またはスマートイメージングの利点のみを強調表示します。 を通常のシナリオ`cache=off`で使用すると、読み込み時間に大きな影響を与えます。

## 要求に対してスマートイメージングをオフにできますか？ {#turning-off-smart-imaging}

はい。URL に `bfc=off` 修飾子を追加して、スマートイメージングをオフにできます。

## どの「チューニング」が使用できますか。定義できる設定やビヘイビアーはありますか。(#tuning-settings)

現在、オプションでスマートイメージングを有効または無効にできます。他のチューニングは使用できません。

## スマートイメージングが画質設定を管理する場合、設定できる最小値と最大値はありますか。例えば、「60 以上」や「80 以下」というクォリティを設定できますか。(#minimum-maximum)

現在のスマートイメージングには、このようなプロビジョニング機能はありません。

## 場合によっては、WebP 画像ではなく JPEG 画像が Chrome に返されます。なぜそのようなことが起こるのですか？(#jpeg-webp)

スマートイメージングは、変換が有益かどうかを判断します。変換結果のファイルサイズが同等の画質で小さくなる場合にのみ、新しい画像が返されます。
