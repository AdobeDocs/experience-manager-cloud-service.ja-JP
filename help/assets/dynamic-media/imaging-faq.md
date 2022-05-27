---
title: スマートイメージング
description: Adobe Sensei AI を活用したスマートイメージングが、各ユーザー固有の閲覧特性を適用して、ユーザーのエクスペリエンスに最適化された適切な画像を自動的に提供することで、パフォーマンスとエンゲージメントの向上を実現している仕組みを説明します。
feature: Asset Management,Renditions
role: User
mini-toc-levels: 3
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 263808980a9542b1a333c59e68e59122cf43025d
workflow-type: tm+mt
source-wordcount: '3525'
ht-degree: 47%

---

# スマートイメージング {#smart-imaging}

## スマートイメージングとは  {#what-is-smart-imaging}

スマートイメージングテクノロジーは、Adobe Sensei AI 機能を使用し、既存の「画像プリセット」と連携して動作します。クライアントのブラウザー機能に基づいて画像形式、サイズ、および画質を自動的に最適化し、画像配信のパフォーマンスを向上させます。

さて、AVIF と WebP の両方のサポートに付属している、改善されたスマートイメージングで、LCP(Largest Contentful Paint) のためのより優れたGoogle Core Web Vital スコアを取得します。

>[!IMPORTANT]
>
>スマートイメージングを使用するには、Adobe Experience Manager - Dynamic Media にバンドルされている標準搭載の CDN（コンテンツ配信ネットワーク）を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。

スマートイメージングをAdobeのクラス最高のプレミアム CDN（コンテンツ配信ネットワーク）サービスと完全に統合することで、パフォーマンスを大幅にアップさせることができます。 このサービスは、サーバー、ネットワーク、およびピアリングポイント間の最適なインターネットルートを見つけます。インターネットのデフォルトのルートを使用する代わりに、待ち時間が最も短く、パケット損失率が最も低いルートを見つけます。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| 画像 （URL） | サムネール | サイズ（JPEG） | スマートイメージングを使用したサイズ (WebP) | スマートイメージングを使用したサイズ (AVIF) | WebP による削減率 | AVIF による%削減 |
|---|---|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [画像 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

上記と同様に、Adobeでも、より大きなサンプルセットを持つテストを実行しました。 AVIF は WebP に対して 20 %の追加サイズ削減を提供し、JPEGに対して 27 %の削減を提供した。 すべて同じ視覚品質です。 AVIF は、JPEGに比べ、平均で最大 41%のサイズ削減を実現しました。

WebP と AVIF を PNG と比較すると、WebP で 84%のサイズ縮小、AVIF で 87%のサイズ縮小が実現します。 また、WebP 形式と AVIF 形式の両方が透明な画像と複数の画像アニメーションをサポートするので、透明な PNG ファイルやGIFファイルの代わりに適しています。

関連トピック [次世代画像形式による画像の最適化（WebP および AVIF）](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 最新のスマートイメージングの主要なメリットとは  {#what-are-the-key-benefits-of-smart-imaging}

スマートイメージングは、使用中のクライアントブラウザー、デバイスの表示、ネットワーク条件に基づいて画像ファイルサイズを自動的に最適化することで、より優れた画像配信パフォーマンスを提供します。 ページの読み込み時間の大部分は画像によって構成されるので、パフォーマンスの向上は、ビジネス KPI（コンバージョン率の高さ、サイトでの滞在時間の短さ、サイトの直帰率の低さなど）に大きな影響を与えます。

最新のスマートイメージングの最新の主なメリットには、次のようなものがあります。

* 次世代の AVIF 形式をサポートするようになりました。
* PNG から WebP、AVIF への変換で可逆変換がサポートされるようになりました。 PNG は可逆形式なので、以前に配信された WebP および AVIF は可逆形式でした。
* ブラウザー形式の変換 (`bfc`)
* デバイスのピクセル比 (`dpr`)
* ネットワーク帯域幅 (`network`)

### ブラウザー形式の変換 (bfc) について {#bfc}

次を追加してブラウザフォーマット変換を有効にする `bfc=on` を画像 URL に自動的に変換すると、JPEGと PNG が可逆 AVIF、可逆 WebP、可逆 JPEGXR、可逆JPEG2000（異なるブラウザー向け）に変換されます。 これらの形式をサポートしていないブラウザーでは、スマートイメージングは引き続きJPEGまたは PNG を提供します。 形式と共に、新しい形式の品質はスマートイメージングによって再計算されます。

スマートイメージングは、 `bfc=off` を画像の URL に追加します。

関連トピック [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) (Dynamic Media Image Serving and Rendering API の )

### デバイスのピクセル比 (dpr) の最適化について {#dpr}

Device Pixel Ratio(DPR)（CSS ピクセル比とも呼ばれます）は、デバイスの物理ピクセルと論理ピクセルとの関係です。 特に、Retina 画面の出現に伴い、最新のモバイルデバイスのピクセル解像度が急速に増加しています。

デバイスのピクセル比の最適化を有効にすると、画像が画面のネイティブ解像度でレンダリングされ、画面が鮮明に表示されます。

現在、ディスプレイのピクセル密度は Akamai CDN ヘッダー値から得られます。

| 画像の URL で許可されている値 | 説明 |
|---|---|
| `dpr=off` | 個々の画像 URL レベルで DPR の最適化をオフにします。 |
| `dpr=on,dprValue` | スマートイメージングで検出された DPR 値を、カスタム値（クライアント側のロジックまたはその他の手段で検出された値）でオーバーライドします。`dprValue` に指定可能な値は、0 より大きい任意の数です。 |

>[!NOTE]
>
>* 全社レベルの DPR 設定がオフの場合でも、`dpr=on,dprValue` を使用できます。
>* DPR の最適化により、結果の画像が Dynamic Media の MaxPix 設定より大きくなる場合、画像の縦横比を維持することで MaxPix の幅が常に認識されます。-->


| 要求された画像サイズ | デバイスのピクセル比 (dpr) 値 | 配信される画像サイズ |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

[画像を操作する場合](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images)および[スマート切り抜きを操作する場合](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)も参照してください。

### ネットワーク帯域幅の最適化について {#network}

「ネットワーク帯域幅」をオンにすると、提供される画質が、実際のネットワーク帯域幅に基づいて自動的に調整されます。ネットワーク帯域幅が不十分な場合、既にオンになっている場合でも、DPR(Device Pixel Ratio) 最適化は自動的にオフになります。

必要に応じて、画像の URL に `network=off` を付けて、個々の画像レベルでネットワーク帯域幅の最適化をオプトアウトできます。

| 画像の URL で使用できる値 | 説明 |
|---|---|
| `network=off` | 個々の画像 URL レベルでネットワーク帯域幅の最適化をオフにします。 |

DPR とネットワーク帯域幅の値は、バンドルされた CDN のクライアント側の検出値に基づいています。これらの値は不正確な場合があります。例えば、iPhone5 と DPR=2、iPhone12 と `dpr=3`、両方表示 `dpr=2`. 高解像度デバイスの場合は、送信 `dpr=2` 送信するよりも効果が高い `dpr=1`. ただし、この不正確さを克服する最善の方法は、クライアント側の DPR を使用して 100%の正確な値を得ることです。 また、起動された任意のデバイス (Appleか他のデバイスかに関わらず ) で機能します。 詳しくは、 [クライアント側デバイスのピクセル比でのスマートイメージングの使用](/help/assets/dynamic-media/client-side-dpr.md).

### スマートイメージングのその他の主なメリット

* 最新のスマートイメージングを使用する Web ページの Google SEO ランキングを改善しました。
* 最適化されたコンテンツをすぐに提供（実行時）
* Adobe Sensei テクノロジーを使用して、イメージリクエストで指定された品質（`qlt`）に従って変換します。
* TTL（Time To Live）独立。以前は、スマートイメージングを機能させるには、最小 TTL 値 12 時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされていて、キャッシュを無効にする 2 つの手順がありました。最新のスマートイメージングでは、派生画像のみがキャッシュされ、1 ステップのキャッシュ無効化プロセスが可能です。
* ルールセットでカスタムヘッダーを使用しているユーザーは、以前のバージョンのスマートイメージングとは異なってこれらのヘッダーがブロックされないので、最新のスマートイメージングのメリットが得られます。例えば、「[画像応答へのカスタム接触チャネル値の追加 | Dynamic Media Classic](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)」で推奨される「Timing Allow Header」、「X-Robot」などは、最新のスマートイメージングによるメリットを享受できます。

## スマートイメージングにはライセンス費用がかかりますか？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

いいえ。スマートイメージングは、既存のライセンスに含まれています。この規則は、Dynamic Media Classic または Experience Manager Dynamic Media（オンプレミス、AMS、および Experience Manager as a Cloud Service）に当てはまります。

>[!NOTE]
>
>Dynamic Media - ハイブリッドのユーザーはスマートイメージングを使用できません。

## スマートイメージングはどのように機能しますか？ {#how-does-smart-imaging-work}

消費者が画像を要求すると、スマートイメージングはユーザーの特性を確認し、使用中のブラウザーに基づいて適切な画像形式に変換します。 これらの形式変換は、視覚的忠実性を低下させない方法で行われます。スマートイメージングは、次のような方法で、ブラウザーの機能に基づいて、自動的に画像を別の形式に変換します。

* ブラウザーがこの形式をサポートしている場合、AVIF に自動的に変換
* AVIF 変換が有益でなかった場合、またはブラウザーが AVIF をサポートしていない場合は、WebP に自動的に変換します
* Safari が WebP をサポートしていない場合は、JPEG2000 に自動的に変換
* IE 9 以降で JPEGXR に自動的に変換するか、Edge が WebP をサポートしていない場合\
   |画像形式 |サポートされているブラウザー | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | |JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 上記形式をサポートしていないブラウザーの場合は、元々要求された画像形式が提供されます。

元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

## どんな画像形式がサポートされていますか？  {#what-image-formats-are-supported}

スマートイメージングでは次の画像形式がサポートされています。

* JPEG
* PNG

JPEG画像ファイル形式の場合、新しい形式の品質はスマートイメージングによって再計算されます。

PNG などの透明性をサポートする画像ファイル形式の場合、可逆性の高い AVIF および WebP を提供するようにスマートイメージングを設定できます。 可逆形式変換の場合、スマートイメージングは画像の URL に記載されている画質を使用します。非可逆形式変換の場合は、Dynamic Mediaの会社アカウントで設定されている画質を使用します。

## スマートイメージングは、使用中の既存の画像プリセットとどのように連携しますか？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

スマートイメージングは既存の画像プリセットと連携し、すべての画像設定を監視します。 変更は、画像形式、画質設定、またはその両方です。 形式変換の場合、スマートイメージングは画像プリセットの設定で定義されているとおりの完全な視覚的忠実性を維持しますが、ファイルサイズは小さくなります。

例えば、JPEGフォーマット、サイズ 500 x 500、画質=85、アンシャープマスク=0.1,1,5 を使用して画像プリセットが定義されているとします。 スマートイメージングがJPEGが Chrome ブラウザー上にあることを検出すると、画像は WebP 形式に変換され、サイズは 500 x 500、アンシャープマスク= 0.1,1,5(WebP) の画質で、可能な限り 85 の画質に一致します。 その WebP 変換のフットプリントがJPEGと比較され、2 つのうち小さい方が返されます。

## スマートイメージングを使用する場合、URL の変更や、画像プリセットの変更、サイトへの新しいコードのデプロイなどは必要ですか？  {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

いいえ。スマートイメージングは既存の画像 URL や画像プリセットとシームレスに連携します。また、スマートイメージングでは、ユーザーのブラウザーを検出するために Web サイトにコードを追加する必要はありません。 これらの機能はすべて自動的に処理されます。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## スマートイメージングは HTTPS で機能しますか？HTTP/2 ではどうですか？  {#does-smart-imaging-working-with-https-how-about-http}

スマートイメージングは、HTTP または HTTPS で配信された画像に対して機能します。また、HTTP/2 上でも機能します。

## スマートイメージングを使用するための資格を私は満たしていますか？ {#am-i-eligible-to-use-smart-imaging}

スマートイメージングを使用するには、貴社の Dynamic Media Classic アカウントまたは Dynamic Media on Experience Manager アカウントが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン（例えば、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` など）ではなく、専用ドメイン（例えば、`images.company.com` または `mycompany.scene7.com`）を使用してください。

ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用ドメインを使用している場合は、独自のカスタムドメインに移動するようにリクエストできます。サポートケースを送信する際には、この移行リクエストを実行してください。

最初のカスタムドメインは、Dynamic Media ライセンスを使用する場合、追加費用はかかりません。

## 自分のアカウントでスマートイメージングを有効にするには、どうすればいいですか？  {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

スマートイメージングを使用するリクエストを開始します。自動的には有効になりません。

以下の説明に従って、サポートケースを作成します。 サポートケースでは、アカウントで有効にする次のスマートイメージング機能（1 つ以上）を指定してください。

* WebP
* AVIF
* DPR とネットワーク帯域幅の最適化
* PNG から可逆 AVIF または非可逆 WebP

WebP で既にスマートイメージングを有効にしているが、上記のような他の新機能を希望する場合は、サポートケースを作成する必要があります。

**お使いのアカウントでスマートイメージングを有効にするサポートケースを作成するには、次の手順を実行します。**

1. [Admin Consoleを使用して、新しいサポートケースの作成を開始します](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html).
1. サポートケースには、次の情報を記入してください。

   * 主要連絡先の氏名、電子メールアドレス、電話番号。

   * アカウントで有効にする次のスマートイメージング機能（1 つ以上）の一覧を示します。
      * WebP
      * AVIF
      * DPR とネットワーク帯域幅の最適化
      * PNG から可逆 AVIF または非可逆 WebP
   * スマートイメージングを有効にするすべてのドメイン（`images.company.com` や `mycompany.scene7.com`）。

      ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

      **[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。

   * `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

      ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社情報アカウントまたはアカウントにログインします。

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

## 自分のアカウントでスマートイメージングが有効になるのはいつ頃ですか？  {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

リクエストはカスタマーサポートに到着した順序で、待ちリストに従って処理されます。

>[!NOTE]
>
>リードタイムが長くなる場合がありますが、それは、スマートイメージングを有効化するためには、アドビによるキャッシュのクリアが必要になるからです。そのため、処理できる移行の数は、常にほんの数件です。

## スマートイメージングを使用するための切り替えに際しては、どんなリスクがありますか？  {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

顧客の Web ページを表示するリスクはありません。ただし、スマートイメージングにトランジションすると、CDN キャッシュがクリアされます。この操作では、Dynamic Media Classic や Dynamic Media on Experience Manager の新しい構成に移行します。

最初の切り替え中、キャッシュが再構築されるまでの間は、アドビの起点サーバーにあるキャッシュされていない画像が直接ヒットします。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。大半のお客様の場合、CDN のキャッシュが完全に再構築されるまでに要する時間は 1～2 日です。

## スマートイメージングが想定どおりに機能しているかどうかを確認するには、どうすればいいですか？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. アカウントにスマートイメージングが設定されたら、ブラウザーで、Dynamic Media Classic または Adobe Experience Manager - Dynamic Media の画像の URL を読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示]**／**[!UICONTROL デベロッパー]**／**[!UICONTROL デベロッパーツール]**&#x200B;に移動して、デベロッパーパネルを開きます。または、別のブラウザーのデベロッパーツールを使用します。

1. デベロッパーツールを開いたときにキャッシュが無効化されるようにします。

   * Windows® では、デベロッパーツールパネルの設定に移動してから、「**[!UICONTROL キャッシュを無効にする（devtools が開いている間）]**」チェックボックスを選択します。
   * macOS では、デベロッパーパネルの「**[!UICONTROL ネットワーク]**」タブで、「**[!UICONTROL キャッシュを無効にする]**」を選択します。

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome 上で PNG 画像が動的に WebP に変換されているのを示しています。ドメインで AVIF が有効になっている場合は、コンテンツタイプに AVIF が表示されることを期待できます。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
>
>すべての画像が変換されるわけではありません。スマートイメージングは、変換がパフォーマンスを向上させる可能性があるかどうかを判断します。予期されるパフォーマンスゲインがない場合や、形式が JPEG や PNG でない場合、画像は変換されません。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## パフォーマンスの向上を把握する方法 スマートイメージングのメリットを知る方法はありますか？ {#benefits}

スマートイメージングヘッダーは、スマートイメージングのメリットを決定します。 スマートイメージングが有効な場合、画像を要求した後、 **[!UICONTROL 応答ヘッダー]** 見出し、 `-X-Adobe-Smart-Imaging` 次のハイライトされた例に示すように、

![スマートイメージングヘッダー](/help/assets/dynamic-media/assets/smartimagingheader.png)

このヘッダーは次の内容を示します。

* スマートイメージングは、会社で機能しています。
* 正の値は、変換が成功したことを意味します。 この場合、新しい WebP イメージが返されます。
* 負の値は、変換処理が成功しなかったことを示します。 この場合、元の要求された画像が返されます ( 指定されていない場合は、デフォルトのJPEG)。
* 正の値は、要求された画像と新しい画像のバイト数の違いを示します。 上記の例では、保存されるバイトはです。 `75048` 1 つの画像の場合は約 75 KB です。
* 負の値は、要求された画像が新しい画像より小さいことを意味します。 負のサイズの差が表示されますが、提供される画像は元の要求された画像のみです。

>[!NOTE]
>
>**X-Adobe — スマートイメージング= -1 （WebP を配信中）**
>
>値が `X-Adobe-Smart-Imaging` が —1 で WebP はまだ配信中です。これは、スマートイメージングが機能しているが、古いキャッシュが原因でサイズのメリットが計算されなかったことを意味します。 以下を使用できます。 `cache=update` （1 回のみ）を画像の URL に追加して、この問題を修正します。
>修飾子の使用例を次に示します。
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>キャッシュ全体を無効にするには、サポートケースを作成する必要があります。

## スマートイメージングで AVIF の最適化を無効にするにはどうすればよいですか？{#disable-avif}

デフォルトで WebP の提供に戻す場合は、同じサポートケースを作成します。 通常どおり、パラメーター `bfc=off` を画像の URL に追加します。 ただし、スマートイメージングの URL 修飾子で WebP または AVIF を選択することはできません。 この機能は、会社のアカウントレベルで維持されます。

## 要求に対してスマートイメージングをオフにできますか？ {#turning-off-smart-imaging}

はい。次のいずれかの修飾子を追加して、スマートイメージングをオフにできます。

* `bfc=off` をオフにして、ブラウザフォーマット変換をオフにします。 関連トピック [ブラウザー形式の変換](#bfc).
* `dpr=off` をオフにして、 Device Pixel Ratio をオフにします。 関連トピック [デバイスのピクセル比](#dpr).
* `network=off` ネットワーク帯域幅をオフにする。 関連トピック [ネットワーク帯域幅](#network).

## どの「チューニング」が使用できますか。定義できる設定やビヘイビアーはありますか。 {#tuning-settings}

スマートイメージングには、有効または無効にできる 3 つのオプションがあります。

* [ブラウザー形式の変換](#bfc)
* [デバイスのピクセル比](#dpr)
* [ネットワーク帯域幅](#network)

## Chrome Web ブラウザーで fmt=tif の URL をお持ちです。 ただし、要求が ImageServer エラーで失敗します。 使用する理由 {#fmt-tif}

お使いのアカウントでスマートイメージングが有効になっていない場合、このエラーは発生しません。 スマートイメージングは、JPEG形式または PNG 形式でのみ機能します。

このエラーを回避するには、次のいずれかを実行します。

* JPEG、PNG、または
* 次を使用しない `fmt` 修飾子、または
* スマートイメージングで定義されているブラウザー設定の形式を使用します。 例えば、Chrome Web ブラウザー用の WebP を使用できます。

## 画像の URL からTIFF画像をダウンロードしたい。 どうやって？ {#download-tif}

追加 `fmt=tif` および `bfc=off` を画像の URL パスに追加します。

## スマートイメージングは画像形式のみを管理しますか？または、最適な結果を得るために画質設定も管理しますか？

スマートイメージングは、形式と画質の両方を使用します。 画像の URL で要求された場合、残りのパラメーターは同じままです。

## スマートイメージングが画質設定を管理する場合、設定できる最小値と最大値はありますか？ つまり 60 以上 80 以下の品質？ {#quality-setting}

現在、そのようなプロビジョニングはありません。

## スマートイメージングは画質の割合の出力設定を自動的に調整しますか？それとも、手動で調整した設定で、すべての画像に適用されますか？ どの範囲で？ {#percent-quality}

スマートイメージングは、画質の割合を自動的に調整します。 この品質の割合は、Adobeで開発された機械学習アルゴリズムを使用して決定されます。 この割合は、範囲に固有ではありません。

## スマートイメージングでは、サポートまたは無視される画像サービングコマンドはどれですか？ {#support-ignore}

無視されるコマンドは次のとおりです。 `fmt` および `qlt`. 残りのコマンドはすべてサポートされています。

## スマートイメージングに置き換えられるのはJPEG画像のみですか？ WebP や PNG などを要求した場合はどうなりますか？ {#replace-request}

この機能は、JPEGと PNG でのみ機能します。

## JPEG画像が WebP ではなく Chrome に返されることがあるのはなぜですか。 {#jpeg-returned}

スマートイメージングは、変換が有益かどうかを判断します。新しい画像を返すのは、変換のみが有益です。

## デバイスのピクセル比 (dpr) 機能が複合画像で期待どおりに動作しないのはなぜですか？ {#composite-images}

合成イメージに含まれるレイヤーが多すぎると、位置修飾子の使用中に dpr 機能に影響が及ぶ場合があります。 この問題は既知で、スマートイメージングの今後のリリースで修正される予定です。 他のスマートイメージング機能が期待どおりに動作しない場合は、問題を報告するサポートケースを作成できます。

## スマートイメージング PNG が可逆 WebP/AVIF に変換されるのはなぜですか？ {#convert-to-lossless}

PNG は可逆形式なので、以前の WebP および AVIF の配信は可逆形式なので、予想よりも大きなサイズになりました。 スマートイメージングで可逆変換がサポートされるようになりました。 修飾子を使用できます `cache=update` （1 回のみ）をイメージリクエストに含めて、この問題を修正します。 この修飾子の使用例を次に示します。

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

キャッシュ全体を無効にするには、そのような作業をリクエストするサポートケースを作成する必要があります。

## スマートイメージングで PNG を使用して可逆変換を続行するにはどうすればよいですか？ {#continue-using}

スマートイメージングで、品質レベルに基づく非可逆変換がサポートされるようになりました。 ロスレス変換を引き続き使用するには、会社の設定に基づいて設定された 100 品質を使用するか、画像の URL を使用してを使用します。 `qlt=100` パスに含まれています。



























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
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) -->
>