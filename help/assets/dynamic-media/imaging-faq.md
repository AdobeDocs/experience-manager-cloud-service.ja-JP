---
title: スマートイメージング
description: Adobe Sensei AI を活用したスマートイメージングが、各ユーザー固有の閲覧特性を適用して、ユーザーのエクスペリエンスに最適化された適切な画像を自動的に提供することで、パフォーマンスとエンゲージメントの向上を実現している仕組みを説明します。
contentOwner: Rick Brough
feature: Asset Management,Renditions,Best Practices
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 22de8ac77af27114099de2f6b4349232524cb94f
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 99%

---

# スマートイメージング {#smart-imaging}

## スマートイメージングについて{#about-smart-imaging}

スマートイメージングテクノロジーは、Adobe Sensei AI 機能を使用し、既存の「画像プリセット」と連携して動作します。クライアントのブラウザー機能に基づいて画像形式、サイズ、および画質を自動的に最適化し、画像配信のパフォーマンスを向上させます。

また、AVIF と WebP の両方のサポートに伴うスマートイメージングの改善により、LCP（Largest Contentful Paint）の Google Core Web Vital スコアが改善されました。

>[!IMPORTANT]
>
>スマートイメージングを使用するには、Adobe Experience Manager - Dynamic Media にバンドルされている標準搭載の CDN（コンテンツ配信ネットワーク）を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。

>[!TIP]
>
>Dynamic Media の&#x200B;[_スナップショット_](https://snapshot.scene7.com/)を使用して、Dynamic Media の画像修飾子とスマートイメージングのメリットを体験してみましょう。
>
> スナップショットは、最適化された動的な画像配信における Dynamic Media のパワーをわかりやすく伝えるために作られた、視覚的なデモツールです。テスト画像や Dynamic Media の URL を試して、様々な Dynamic Media 画像修飾子の出力を視覚的に観察し、次の項目に対するスマートイメージング最適化を確認します。
>
>* ファイルサイズ（WebP および AVIF 配信を使用）
>* ネットワーク帯域幅
>* DPR（デバイスのピクセル比）
>
>スナップショットの使用がどれほど簡単かを知るには、[スナップショットのトレーニングビデオ](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=ja)（3 分 17 秒）を再生してください。

スマートイメージングを、クラス最高のプレミアム CDN（コンテンツ配信ネットワーク）サービスと完全に統合することで、パフォーマンスを大幅にアップさせることができます。このサービスは、サーバー、ネットワーク、およびピアリングポイント間の最適なインターネットルートを見つけます。インターネットのデフォルトのルートを使用する代わりに、待ち時間が最も短く、パケット損失率が最も低いルートを見つけます。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| 画像（URL） | サムネール | サイズ（JPEG） | サイズ（WebP）（スマートイメージングを使用） | サイズ（AVIF）（スマートイメージングを使用） | WebP による削減率 | AVIF による削減率 |
|---|---|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89％ | 37.79％ |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01％ | 72.57％ |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47％ | 60.58％ |
| [画像 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25％ | 51.85％ |

上記と同様に、アドビでも、より大きなサンプルセットを使用してテストを実行しました。AVIF 形式は WebP よりもサイズ削減率が 20％向上しました（WebP では JPEG に対して 27％の削減を実現）。視覚的な品質はすべて同じです。全体的に見て、AVIF は JPEG よりも最大で平均 41％のサイズ削減を実現しています。

WebP および AVIF を PNG と比較すると、サイズ削減は WebP で 84％、AVIF で 87％となっています。また、WebP 形式も AVIF 形式も透明度と複数の画像アニメーションをサポートしているので、透明 PNG および GIF ファイルの代わりに使用できます。

[次世代の画像形式 WebP および AVIF による画像の最適化](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)も参照してください。

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**スマートイメージングのメリット**

スマートイメージングは、使用しているクライアントブラウザー、デバイスのディスプレイおよびネットワーク状況に応じて画像ファイルサイズを自動的に最適化することで、より優れた画像配信パフォーマンスを実現します。画像はページの読み込み時間のほとんどを占めるので、こうしたパフォーマンス向上はビジネス KPI（より高いコンバージョン率、より長いサイト滞在時間、より低いサイトバウンス率など）に大きな影響を及ぼす可能性があります。

最新のスマートイメージングの主要なメリットには、次のものがあります。

* 次世代の AVIF 形式をサポートするようになりました。
* PNG から WebP および AVIF への変換で非可逆変換がサポートされるようになりました。PNG は可逆形式なので、以前配信されていた WebP および AVIF は可逆形式でした。
* [ブラウザーフォーマット変換](#bfc)
* [デバイスピクセル比](#dpr)
* [ネットワーク帯域幅](#bandwidth)

### ブラウザーフォーマット変換について {#bfc}

画像 URL に `bfc=on` を追加してブラウザーフォーマット変換を有効にすると、異なるブラウザー向けに JPEG と PNG が非可逆 AVIF、非可逆 WebP、非可逆 JPEGXR、非可逆 JPEG2000 に自動的に変換されます。これらの形式をサポートしていないブラウザーでは、スマートイメージングは引き続き JPEG または PNG を提供します。形式と共に、新しい形式の画質がスマートイメージングによって再計算されます。

画像の URL に `bfc=off` を追加することで、スマートイメージングをオフにすることもできます。

Dynamic Media 画像サービングおよび画像レンダリング API の [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=ja) も参照してください。

### デバイスピクセル比の最適化について {#dpr}

デバイスピクセル比（DPR）は、CSS ピクセル比とも呼ばれ、デバイスの物理ピクセルと論理ピクセルの関係を表します。特に、Retina 画面の出現に伴い、最新のモバイルデバイスのピクセル解像度が急速に増加しています。

デバイスピクセル比の最適化を有効にすると、画像が画面のネイティブ解像度でレンダリングされるので、画面が鮮明に見えます。

現在、ディスプレイのピクセル密度は Akamai CDN ヘッダー値から得られます。

| 画像の URL で使用できる値 | 説明 |
|---|---|
| `dpr=off` | 個々の画像 URL レベルで DPR の最適化をオフにします。 |
| `dpr=on,dprValue` | スマートイメージングで検出された DPR 値を、カスタム値（クライアント側のロジックまたはその他の手段で検出された値）でオーバーライドします。`dprValue` に指定可能な値は、0 より大きい任意の数です。 |

>[!NOTE]
>
>* 全社レベルの DPR 設定がオフの場合でも、`dpr=on,dprValue` を使用できます。
>* DPR の最適化により、結果の画像が Dynamic Media の MaxPix 設定より大きくなる場合、画像の縦横比を維持することで MaxPix の幅が常に認識されます。-->

| 要求された画像サイズ | デバイスピクセル比（dpr）の値 | 配信される画像サイズ |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

[画像を操作する場合](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images)および[スマート切り抜きを操作する場合](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)も参照してください。

### ネットワーク帯域幅の最適化について {#bandwidth}

「ネットワーク帯域幅」をオンにすると、提供される画質が、実際のネットワーク帯域幅に基づいて自動的に調整されます。ネットワーク帯域幅が不十分な場合は、DPR（デバイスピクセル比）の最適化がオンになっていても、自動的にオフになります。

必要に応じて、画像の URL に `network=off` を付けて、個々の画像レベルでネットワーク帯域幅の最適化をオプトアウトできます。

| 画像の URL で使用できる値 | 説明 |
|---|---|
| `network=off` | 個々の画像 URL レベルでネットワーク帯域幅の最適化をオフにします。 |

DPR とネットワーク帯域幅の値は、バンドルされた CDN のクライアント側の検出値に基づいています。これらの値は不正確な場合があります。例えば、dpr=2 の iPhone5 と `dpr=3` の iPhone12 では、どちらも `dpr=2` と表示されます。それでも、高解像度デバイスの場合は、`dpr=1` を送信するより `dpr=2` を送信する方が適切です。この不正確さを克服する最善の方法は、クライアントサイドの DPR を使用して 100％正確な値を指定することです。また、これは、Apple か他のデバイスかに関わらず、発売された任意のデバイスで機能します。[クライアントサイドのデバイスピクセル比（DPR）を使用したスマートイメージングについて](/help/assets/dynamic-media/client-side-dpr.md)を参照してください。

**スマートイメージングのその他の主要なメリット**

* 最新のスマートイメージングを使用する Web ページの Google SEO ランキングを改善しました。
* 最適化されたコンテンツをすぐに提供（実行時）
* Adobe Sensei テクノロジーを使用して、イメージリクエストで指定された品質（`qlt`）に従って変換します。
* TTL（Time To Live）独立。以前は、スマートイメージングを機能させるには、最小 TTL 値 12 時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされていて、キャッシュを無効にする 2 つの手順がありました。最新のスマートイメージングでは、派生画像のみがキャッシュされ、1 ステップのキャッシュ無効化プロセスが可能です。
* ルールセットでカスタムヘッダーを使用しているユーザーは、以前のバージョンのスマートイメージングとは異なってこれらのヘッダーがブロックされないので、最新のスマートイメージングのメリットが得られます。例えば、「[画像応答へのカスタム接触チャネル値の追加 | Dynamic Media Classic](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)」で推奨される「Timing Allow Header」、「X-Robot」などは、最新のスマートイメージングによるメリットを享受できます。

## スマートイメージングの仕組み{#how-smart-imaging-works}

画像が消費者から要求されると、スマートイメージングがそのユーザーの特性を確認し、使用中のブラウザーに基づいて適切な画像形式に変換します。これらの形式変換は、視覚的忠実性を低下させない方法で行われます。スマートイメージングは、次のような方法で、ブラウザーの機能に基づいて、自動的に画像を別の形式に変換します。

* ブラウザーが AVIF 形式をサポートしている場合は、自動的に AVIF に変換します
* AVIF 変換がうまくいかなかった場合やブラウザーが AVIF をサポートしていない場合は、自動的に WebP に変換します
* Safari で WebP がサポートされていない場合は、自動的に JPEG2000 に変換します
* IE 9 以降については、または Edge で WebP がサポートされていない場合は、自動的に JPEGXR に変換します

  | 画像の形式 | サポートされているブラウザー |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* 上記形式をサポートしていないブラウザーの場合は、元々要求された画像形式が提供されます。

元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

## スマートイメージングでの画像形式のサポート{#image-format-support}

スマートイメージングでは次の画像形式がサポートされています。

* JPEG
* PNG

JPEG 画像ファイル形式の場合、新しい形式の画質がスマートイメージングによって再計算されます。

透明度をサポートしている PNG などの画像ファイル形式の場合は、非可逆の AVIF および WebP を配信するようにスマートイメージングを設定できます。スマートイメージングでは、非可逆の形式変換の場合、画像の URL で指定されている画質を使用します。それ以外の場合は、Dynamic Media の会社アカウントで設定されている画質を使用します。

## スマートイメージングでの画像サービングコマンドのサポート{#imaging-serving-command-support}

画像サービングコマンド `fmt` および `qlt` はサポートされていません。残りのコマンドはすべてサポートされます。

## スマートイメージングに関するよくある質問（FAQ）{#smart-imaging-faq}

+++**スマートイメージングにはライセンス費用がかかりますか？**

いいえ。スマートイメージングは、既存のライセンスに含まれています。この規則は、Dynamic Media Classic または Experience Manager Dynamic Media（オンプレミス、AMS、および Experience Manager as a Cloud Service）に当てはまります。

>[!IMPORTANT]
>
>Dynamic Media - ハイブリッドのユーザーはスマートイメージングを使用できません。

+++

+++**要求に対してスマートイメージングをオフにできますか？**

はい。次のいずれかの修飾子を追加して、スマートイメージングをオフにできます。

* `bfc=off`：ブラウザーフォーマット変換をオフにします。[ブラウザーフォーマット変換](#bfc)も参照してください。
* `dpr=off`：デバイスピクセル比の最適化をオフにします。[デバイスピクセル比](#dpr)も参照してください。
* `network=off`：ネットワーク帯域幅の最適化をオフにします。[ネットワーク帯域幅](#network)も参照してください。

+++

+++**スマートイメージングを「調整」できますか？**

はい。スマートイメージングには、有効または無効にできるオプションが次の 3 つあります。

* [ブラウザーフォーマット変換](#bfc)
* [デバイスピクセル比](#dpr)
* [ネットワーク帯域幅](#network)

+++

+++**スマートイメージングは既存の画像プリセットと連動しますか？**

はい。スマートイメージングは既存の画像プリセットと連携し、すべての画像設定に従います。変更されるのは、画像形式、画質設定またはその両方です。形式変換の場合、スマートイメージングは画像プリセットの設定で定義されているとおりの完全な視覚的忠実性を維持しますが、ファイルサイズは小さくなります。

例えば、JPEG 形式、サイズ 500 x 500、画質=85、アンシャープマスク=0.1,1,5 と定義された画像プリセットがあるとします。ユーザーが Chrome ブラウザーを使用していることをスマートイメージングが検出すると、画像は WebP 形式（サイズ 500 x 500）に変換されます。また、アンシャープマスク=0.1,1,5 は、JPEG の画質=85 にできるだけ一致する WebP の画質で適用されます。その WebP 変換のフットプリントが JPEG と比較され、2 つのうち小さい方が返されます。

+++

+++**URL や画像プリセットの変更またはサイトへの新しいコードのデプロイなどは必要ですか？**

いいえ。スマートイメージングは既存の画像 URL や画像プリセットとシームレスに連携します。さらに、スマートイメージングでは、ユーザーのブラウザーを検出するために web サイトにコードを追加する必要はありません。これらの機能はすべて自動的に処理されます。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++

+++**スマートイメージングは HTTPS で機能しますか？HTTP/2 ではどうですか？**

いずれの質問も、回答は「はい」です。スマートイメージングは、HTTP または HTTPS で配信された画像に対して機能します。また、HTTP/2 上でも機能します。

+++

+++**スマートイメージングを使用するための資格を私は満たしていますか？**

場合によって異なります。スマートイメージングを使用するには、貴社の Dynamic Media Classic アカウントまたは Dynamic Media on Experience Manager アカウントが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン（例えば、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` など）ではなく、専用ドメイン（例えば、`images.company.com` または `mycompany.scene7.com`）を使用してください。

ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用ドメインを使用している場合は、独自のカスタムドメインに移動するようにリクエストできます。このトランジションリクエストは、サポートケースを送信する際に行います。

最初のカスタムドメインは、Dynamic Media ライセンスを使用する場合、追加費用はかかりません。

+++

+++**自分のアカウントでスマートイメージングを有効できますか？**

いいえ。スマートイメージングを使用するためのリクエストを開始する必要があります。自動的には有効になりません。

以下の説明に従って、サポートケースを作成します。サポートケースでは、次のスマートイメージング機能のうち、どれ（1 つ以上）をアカウントで有効にするかを指定してください。

* WebP
* AVIF
* DPR とネットワーク帯域幅の最適化
* PNG から非可逆 AVIF または非可逆 WebP への変換

スマートイメージングが WebP で既に有効になっていても、上記のような他の新しい機能を希望する場合は、サポートケースを作成する必要があります。

**アカウントでスマートイメージングを有効にするためのサポートケースを作成するには：**

1. [Admin Console を使用して、新しいサポートケースの作成を開始します](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)。
1. サポートケースには、次の情報を記入してください。

   * 主要連絡先の氏名、メールアドレス、電話番号。

   * 次のスマートイメージング機能のうち、どれ（1 つ以上）をアカウントで有効にするかを指定します。
      * WebP
      * AVIF
      * DPR とネットワーク帯域幅の最適化
      * PNG から非可逆 AVIF または非可逆 WebP への変換

   * スマートイメージングを有効にするすべてのドメイン（`images.company.com` や `mycompany.scene7.com`）。

     ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

     **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。

     「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。

   * `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

     ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

     **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。

     「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media Classic ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

   * HTTP/2 で動作させるかどうかを指定します。

1. アドビカスタマーサポートでは、要求が送信された順序に基づいて、スマートイメージングカスタマー待ちリストに貴社を追加します。
1. リクエストを処理する準備が整った時点で、カスタマーサポートから連絡を差し上げ、調整と日取り設定を行います。
1. **オプション**：アドビが実稼働環境にスマートイメージングをプッシュする前に、この新機能をステージングでテストするためのオプションがあります。
1. 完了後、カスタマーサポートから通知があります。
1. スマートイメージングのパフォーマンス向上を最大限にするため、アドビでは、有効期間（TTL）を 24 時間以上に設定することを推奨しています。TTL によって定義されるのは、アセットが CDN によってキャッシュされる期間です。この設定を変更するには、次の手順を実行します。

   1. Dynamic Media Classic を使用している場合は、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 公開設定]**／**[!UICONTROL Image Server]** に移動します。「**[!UICONTROL 初期設定のクライアントキャッシュの有効期限]**」の値を 24 以上に設定します。
   1. Dynamic Media を使用する場合は、[次の手順](config-dm.md)に従います。「**[!UICONTROL 有効期限]**」の値を 24 時間以上に設定します。

+++

+++**自分のアカウントでスマートイメージングはいつ有効になりますか？**

リクエストはカスタマーサポートに到着した順序で、待ちリストに従って処理されます。

>[!NOTE]
>
>リードタイムが長くなる場合がありますが、それは、スマートイメージングを有効化するためには、アドビによるキャッシュのクリアが必要になるからです。そのため、処理できる移行の数は、常にほんの数件です。

+++

+++**スマートイメージングの使用に関してリスクはありますか？**

顧客の Web ページを表示するリスクはありません。ただし、スマートイメージングにトランジションすると、CDN キャッシュがクリアされます。この操作では、Dynamic Media Classic や Dynamic Media on Experience Manager の新しい構成に移行します。

最初の切り替え中、キャッシュが再構築されるまでの間は、アドビの起点サーバーにあるキャッシュされていない画像が直接ヒットします。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。ほとんどのお客様の場合、キャッシュは CDN で 1〜2 日以内に完全に再構築されます。

+++

+++**スマートイメージングが機能するかどうかを確認できますか？**

はい。次の操作を実行できます。

1. アカウントにスマートイメージングが設定されたら、ブラウザーで、Dynamic Media Classic または Adobe Experience Manager - Dynamic Media の画像の URL を読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示]**／**[!UICONTROL デベロッパー]**／**[!UICONTROL デベロッパーツール]**&#x200B;に移動して、デベロッパーパネルを開きます。または、別のブラウザーのデベロッパーツールを使用します。

1. デベロッパーツールを開いたときにキャッシュが無効化されるようにします。

   * Windows® では、デベロッパーツールパネルの設定に移動してから、「**[!UICONTROL キャッシュを無効にする（devtools が開いている間）]**」チェックボックスを選択します。
   * macOS では、デベロッパーパネルの「**[!UICONTROL ネットワーク]**」タブで、「**[!UICONTROL キャッシュを無効にする]**」を選択します。

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome 上で PNG 画像が動的に WebP に変換されているのを示しています。ドメインで AVIF が有効になっている場合は、コンテンツタイプに AVIF が表示されることも期待できます。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
>
>すべての画像が変換されるわけではありません。スマートイメージングは、変換がパフォーマンスを向上させる可能性があるかどうかを判断します。予期されるパフォーマンスゲインがない場合や、形式が JPEG や PNG でない場合、画像は変換されません。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

+++

+++**スマートイメージングのメリットを知る方法はありますか？**

はい。スマートイメージングのメリットはスマートイメージングヘッダーで決まります。スマートイメージングが有効な場合は、画像を要求すると、**[!UICONTROL 応答ヘッダー]**&#x200B;の見出し下に `-X-Adobe-Smart-Imaging` が表示されます（下の例のハイライト表示された部分を参照）。

![スマートイメージングヘッダー](/help/assets/dynamic-media/assets/smartimagingheader.png)

このヘッダーは次のことを示しています。

* スマートイメージングは会社向けに機能しています。
* 正の値は、変換が成功したことを意味します。この場合、新しい WebP 画像が返されます。
* 負の値は、変換が成功しなかったことを意味します。この場合、要求されたオリジナル画像が返されます（指定されていない場合は、デフォルトの JPEG）。
* 正の値は、要求された画像と新しい画像のバイト数の違いを示します。上記の例では、保存されたバイト数は 1 つの画像について `75048`（約 75 KB）です。
* 負の値は、要求された画像が新しい画像より小さいことを意味します。負のサイズの差が表示されますが、提供される画像は要求されたオリジナル画像のみです。

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 で WebP を配信中**
>
>`X-Adobe-Smart-Imaging` の値が -1 で WebP がまだ配信中の場合は、スマートイメージングは機能しているものの、古いキャッシュが原因でサイズのメリットが計算されなかったことを意味します。画像の URL で `cache=update` を（1 回だけ）使用して、この問題を修正できます。
>この修飾子の使用例を次に示します。
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>キャッシュ全体を無効にするには、サポートケースを作成する必要があります。

+++

+++**スマートイメージングで AVIF の最適化を無効にできますか？**

はい。WebP をデフォルトで提供する状態に戻す場合は、同様にサポートケースを作成します。通常どおり、画像の URL に `bfc=off` パラメーターを追加して、スマートイメージングをオフにできます。ただし、スマートイメージングの URL 修飾子で WebP または AVIF を選択することはできません。この機能は、会社アカウントレベルで維持管理されています。

+++

+++**Chrome web ブラウザーで fmt=tif の URL を使用している場合、リクエストが失敗するのはなぜですか？**

アカウントでスマートイメージングが有効になっていない場合、このエラーは発生しません。スマートイメージングは、JPEG 形式または PNG 形式でのみ機能します。

このエラーを回避するには、次のいずれかを行います。

* JPEG または PNG を指定する
* `fmt` 修飾子をまったく使用しない
* スマートイメージングで定義されているブラウザー優先設定形式を使用する。例えば、Chrome web ブラウザーには WebP を使用できます。

+++

+++**画像の URL から TIFF 画像をダウンロードできますか？**

はい。`fmt=tif` と `bfc=off` を画像の URL パスに追加します。

+++

+++**スマートイメージングは画像形式と画質の設定を管理しますか？**

はい。スマートイメージングでは、形式と画質の両方を使用します。画像の URL で要求された場合、残りのパラメーターは同じままです。

+++

+++**最低品質と最大品質の設定を指定できますか？**

いいえ。現在、そのようなプロビジョニングはありません。

+++

+++**スマートイメージングは画質の出力設定のパーセントを調整しますか？**

はい。スマートイメージングでは、画質（％単位）を自動的に調整します。この画質（％単位）は、アドビで開発された機械学習アルゴリズムを使用して決定されます。このパーセントは、範囲固有のものではありません。

+++

+++**スマートイメージングで置換の対象となるのは JPEG および PNG 画像のみですか？**

はい。この機能は、JPEG と PNG でのみ機能します。

+++

+++**WebP ではなく JPEG 画像が Chrome に返されることがあるのはなぜですか？**

スマートイメージングは、変換が有益かどうかを判断します。変換が有益な場合にのみ、新しい画像を返します。

+++

+++**合成画像でデバイスピクセル比（dpr）機能が動作しないのはなぜですか？**

合成画像に含まれるレイヤーが多すぎると、位置修飾子の使用中に dpr 機能に影響が及ぶ場合があります。この問題は既知で、スマートイメージングの今後のリリースで修正される予定です。他のスマートイメージング機能が期待どおりに動作しない場合は、サポートケースを作成して問題を報告することができます。

+++

+++**スマートイメージングで PNG が可逆圧縮 WebP／AVIF に変換されるのはなぜですか？**

PNG は可逆形式なので、以前配信されていた WebP および AVIF は可逆形式でした。その結果、予想よりも大きいサイズになりました。スマートイメージングでは、非可逆変換をサポートするようになりました。画像リクエストで修飾子 `cache=update` を（1 回だけ）使用して、この問題を修正できます。この修飾子の使用例を次に示します。

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

キャッシュ全体を無効にするには、サポートケースを作成して、その作業を依頼する必要があります。

+++

+++**スマートイメージングで PNG の可逆変換を引き続き使用できますか？**

はい。スマートイメージングでは、画質レベルに応じた非可逆変換をサポートするようになりまし。可逆変換を引き続き使用するには、会社の設定を通じて、または画像の URL パスで `qlt=100` を使用して、100％の画質を設定します。

+++



























<!-- ## If Smart Imaging manages the quality settings, are there minimums and maximums I can set? For example, is it possible to set "no lower than 60" and "no greater than 80 quality"? {#minimum-maximum}

There is no such provisioning ability in the current Smart Imaging. -->

<!-- ## Sometimes a JPEG image is returned to Chrome instead of a WebP image. Why does that change happen? {#jpeg-webp}

Smart Imaging determines if the conversion is beneficial or not. It returns the new image only if the conversion results in a smaller file size with comparable quality.

How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) 
-->
