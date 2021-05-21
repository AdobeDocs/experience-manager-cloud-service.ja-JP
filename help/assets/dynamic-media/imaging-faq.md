---
title: スマートイメージング
description: 「スマートイメージングが各ユーザーに固有の表示特性を適用して、エクスペリエンスに最適化された適切な画像を自動的に提供する方法を学び、パフォーマンスとエンゲージメントを向上させます。」
feature: アセット管理，レンディション
role: Business Practitioner
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 77%

---

# スマートイメージング {#smart-imaging}

## スマートイメージングとは {#what-is-smart-imaging}

スマートイメージングテクノロジーは、Adobe Sensei AI 機能を使用し、既存の「画像プリセット」と連携して動作します。クライアントのブラウザー機能に基づいて画像形式、サイズ、および画質を自動的に最適化し、画像配信のパフォーマンスを向上させます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Mediaにバンドルされている標準搭載のCDN（コンテンツ配信ネットワーク）を使用する必要があります。 この機能では、その他のカスタム CDN はサポートされません。

また、スマートイメージングをアドビのクラス最高のプレミアム CDN（ココンテンツ配信ネットワーク）サービスと完全に統合することで、パフォーマンスを大幅にアップさせることもできます。このサービスは、サーバー、ネットワーク、およびピアリングポイント間の最適なインターネットルートを見つけます。インターネット上のデフォルトのルートを使用する代わりに、待ち時間が最も短く、パケット損失率が最も低いルートを見つけます。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| 画像 <br>（URL） | サムネール | サイズ<br>（JPEG） | サイズ（WebP）<br>（スマートイメージングを使用） | 削減 % |
|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [画像 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均 = 51% |

上記と同様に、アドビでもライブ顧客サイトの 7,009 件の URL でテストを実施しました。JPEG 用のファイルサイズの最適化は、平均で 38%も向上しました。WebP 形式の PNG の場合、ファイルサイズの最適化を平均で 31%向上させることができました。このような最適化は、スマートイメージングの機能によって可能となります。

## 最新のスマートイメージングの主要なメリットとは {#what-are-the-key-benefits-of-smart-imaging}

画像は、ページの読み込み時間の大部分を占めます。したがって、パフォーマンスの向上は、コンバージョン率の増加、サイトでの滞在時間、サイトの直帰率の低下に大きな影響を与える可能性があります。

最新バージョンのスマートイメージングの機能強化：

* 最新のスマートイメージングを利用したWebページのGoogle SEOランキングを改善しました。
* 最適化されたコンテンツをすぐに提供（実行時）
* Adobe Senseiテクノロジーを使用して、イメージリクエストで指定された品質(`qlt`)に従って変換します。
* スマートイメージングは、`bfc` URLパラメーターを使用してオフにできます。
* TTL（Time To Live）独立。以前は、スマートイメージングを機能させるには、最小 TTL 値 12 時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされていて、キャッシュを無効にする 2 つの手順がありました。最新のスマートイメージングでは、派生画像のみがキャッシュされ、1 ステップのキャッシュ無効化プロセスが可能です。
* ルールセットでカスタムヘッダーを使用するお客様は、以前のバージョンのスマートイメージングとは異なり、これらのヘッダーがブロックされないので、最新のスマートイメージングのメリットが得られます。 例えば、[画像応答へのカスタムヘッダー値の追加|Dynamic Media Classic](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)で推奨される「タイミング許可原点」、「X-Robot」。

## スマートイメージングにはライセンス費用がかかりますか？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

いいえ。スマートイメージングは、既存のライセンスに含まれています。この規則は、Dynamic Media Classic または Experience ManagerDynamic Media（オンプレミス、AMS、および Experience Manager as a Cloud Service）に当てはまります。

>[!NOTE]
>
>スマートイメージングは、Dynamic Media — ハイブリッドのお客様はご利用いただけません。

## スマートイメージングはどのように機能しますか？ {#how-does-smart-imaging-work}

消費者から画像が要求されると、スマートイメージングはユーザーの特性を確認し、使用中のブラウザーに基づいて適切な画像形式に変換します。 これらの形式変換は、視覚的忠実性を低下させない方法でおこなわれます。スマートイメージングは、次のような方法で、ブラウザーの機能に基づいて、自動的に画像を別の形式に変換します。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 次のブラウザー用に WebP に自動的に変換：
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari（iOS、macOS、iPadOSをまたぐ）、WebPをサポートするブラウザーとOSバージョンが提供されました。
   * Android™
   * Opera
* 以下のレガシーブラウザーでのサポート：

   | ブラウザー | ブラウザー／OS のバージョン | 形式 |
   | --- | --- | --- |
   | Safari | iOS/iPad 14.0またはmacOS BigSurより前 | JPEG2000 |
   | Edge | 18より前 | JPEGXR |
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

## スマートイメージングは、使用中の既存の画像プリセットとどのように連携しますか？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

スマートイメージングは、既存の「画像プリセット」と連携して動作します。要求されたファイル形式がJPEGまたはPNGの場合、画質(`qlt`)と形式(`fmt`)を除くすべての画像設定を監視します。 形式変換の場合、画像プリセットの設定で定義されているとおりの完全な視覚的忠実性が維持されますが、ファイルサイズは小さくなります。元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## スマートイメージングを使用する場合、URL の変更や、画像プリセットの変更、サイトへの新しいコードのデプロイなどは必要ですか？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

既存のカスタムドメインで設定する場合、スマートイメージングは既存の画像 URL や画像プリセットとシームレスに連携します。また、スマートイメージングでは、ユーザーのブラウザーを検出するために Web サイトにコードを追加する必要はありません。すべて自動的に処理されます。

スマートイメージングを使用するために新しいカスタムドメインを設定する必要がある場合は、このカスタムドメインを反映するように URL を更新する必要があります。

スマートイメージングの前提条件を理解するには、[スマートイメージングを使用する資格はありますか？](#am-i-eligible-to-use-smart-imaging)を参照してください。

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## スマートイメージングは HTTPS で機能しますか？HTTP/2 ではどうですか？ {#does-smart-imaging-working-with-https-how-about-http}

スマートイメージングは、HTTP または HTTPS で配信された画像に対して機能します。また、HTTP/2 上でも機能します。

## スマートイメージングを使用するための資格を私は満たしていますか？ {#am-i-eligible-to-use-smart-imaging}

スマートイメージングを使用するには、貴社の Dynamic Media Classic アカウントまたは Dynamic Media on Experience Manager アカウントが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン（例えば、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` など）ではなく、専用ドメイン（例えば、`images.company.com` または `mycompany.scene7.com`）を使用してください。

ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社のアカウントにログインします。

**[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をタップします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用ドメインを使用している場合は、独自のカスタムドメインに移動するようにリクエストできます。技術サポートチケットを送信したら、このトランジションリクエストを作成します。

最初のカスタムドメインは、Dynamic Media ライセンスを使用する場合、追加費用はかかりません。

## 自分のアカウントでスマートイメージングを有効にするには、どうすればいいですか？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

スマートイメージングを使用するためのリクエストを開始する必要があります。自動的には有効になりません。

1. [「 」Admin Consoleを使用して、サポートケースを作成します](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。
1. サポートケースには、次の情報を記入してください。

   1. 主要連絡先の氏名、電子メールアドレス、電話番号。
   1. スマートイメージングを有効にする全ドメイン（`images.company.com` や `mycompany.scene7.com`）。

      ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。
   1. 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。
   1. `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

      ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社のアカウントにログインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media Classic ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。
   1. HTTP/2 で動作させるかどうかを指定します。

1. Adobe のサポートでは、要求が送信された順序に基づいて、スマートイメージングカスタマー待ちリストに貴社を追加します。
1. 要求を処理する準備が整った時点で、テクニカルサポートから連絡を差し上げ、調整と日取り設定をおこないます。
1. **オプション**：アドビが実稼働環境にスマートイメージングをプッシュする前に、この新機能をステージングでテストするためのオプションがあります。
1. 完了後、サポートから通知があります。
1. スマートイメージングのパフォーマンス向上を最大限にするため、アドビでは、有効期間（TTL）を 24 時間以上に設定することを推奨しています。TTL によって定義されるのは、アセットが CDN によってキャッシュされる期間です。この設定を変更するには、次の手順を実行します。

   1. Dynamic Media Classic を使用している場合は、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。「**[!UICONTROL 初期設定のクライアントキャッシュの有効期限]**」の値を 24 以上に設定します。
   1. Dynamic Media を使用する場合は、[次の手順](config-dm.md)に従います。「**[!UICONTROL 有効期限]**」の値を 24 時間以上に設定します。

## 自分のアカウントでスマートイメージングが有効になるのはいつ頃ですか？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

リクエストは、カスタマーケアが受け取った順序で、待機リストに従って処理されます。

>[!NOTE]
>
>リードタイムは長くなる場合があります。これは、スマートイメージングを有効にする際に、キャッシュのAdobeクリアが必要になるからです。 そのため、処理できる移行の数は、常にほんの数件です。

## スマートイメージングを使用するための切り替えに際しては、どんなリスクがありますか？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

顧客の Web ページを表示するリスクはありません。ただし、スマートイメージングにトランジションすると、CDN キャッシュがクリアされます。この操作では、Dynamic Media Classic や Dynamic Media on Experience Manager の新しい構成に移行します。

最初の切り替え中、キャッシュが再構築されるまでの間は、アドビの起点サーバーにあるキャッシュされていない画像が直接ヒットします。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。大半のお客様の場合、CDN のキャッシュが完全に再構築されるまでに要する時間は 1～2 日です。

## スマートイメージングが想定どおりに機能しているかどうかを確認するには、どうすればいいですか？ {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. アカウントにスマートイメージングが設定されたら、ブラウザーで、Dynamic Media ClassicまたはAdobe Experience Manager - Dynamic Media画像のURLを読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示／デベロッパー／デベロッパーツール]**&#x200B;をクリックしてデベロッパーパネルを開きます。または、別のブラウザーのデベロッパーツールを使用します。

1. デベロッパーツールを開いたときにキャッシュが無効化されるようにします。

   * Windows®で、デベロッパーツールパネルの「設定」に移動し、「**[!UICONTROL キャッシュを無効にする（devtoolsが開いている間）]**」チェックボックスをオンにします。
   * macOSのデベロッパーペインの「**[!UICONTROL Network]**」タブで、「**[!UICONTROL disable cache]**」を選択します。

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome 上で PNG 画像が動的に WebP に変換されているのを示しています。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
>
>すべての画像が変換されるわけではありません。スマートイメージングは、変換がパフォーマンスを向上させる可能性があるかどうかを判断します。 予期されるパフォーマンスゲインがない場合や、形式が JPEG や PNG でない場合、画像は変換されません。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 要求に対してスマートイメージングをオフにできますか？ {#turning-off-smart-imaging}

はい。URL に `bfc=off` 修飾子を追加して、スマートイメージングをオフにできます。

## どの「チューニング」が使用できますか。定義できる設定やビヘイビアーはありますか。(#tuning-settings)

現在、オプションでスマートイメージングを有効または無効にできます。他のチューニングは使用できません。

## スマートイメージングが画質設定を管理する場合、設定できる最小値と最大値はありますか。例えば、「60 以上」や「80 以下」というクォリティを設定できますか。(#minimum-maximum)

現在のスマートイメージングには、このようなプロビジョニング機能はありません。

## 場合によっては、WebP 画像ではなく JPEG 画像が Chrome に返されます。その変更がおこなわれる理由はなぜですか。(#jpeg-webp)

スマートイメージングは、変換が有益かどうかを判断します。変換結果のファイルサイズが同等の画質で小さくなる場合にのみ、新しい画像が返されます。
