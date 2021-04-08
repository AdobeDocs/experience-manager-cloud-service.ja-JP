---
title: スマートイメージング
description: 「各ユーザー独自の表示特性を適用して、エクスペリエンスに最適化された適切な画像を自動的に提供することで、パフォーマンスとエンゲージメントを向上させるスマートイメージングについて説明します。」
feature: アセット管理，レンディション
topic: 業務担当者
role: Business Practitioner
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
translation-type: tm+mt
source-git-commit: 4f2aa7d444d46aef959abc953e7a943f00cbb0c1
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 46%

---

# スマートイメージング {#smart-imaging}

## スマートイメージングとは {#what-is-smart-imaging}

スマートイメージングテクノロジは、Adobe SenseiAI機能を適用し、既存の「画像プリセット」と連携して動作します。 クライアントのブラウザー機能に基づいて画像形式、サイズ、および画質を自動的に最適化し、画像配信のパフォーマンスを向上させます。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience ManagerDynamic Mediaに付属の標準搭載のCDN(コンテンツ配信ネットワーク)を使用する必要があります。 この機能では、その他のカスタムCDNはサポートされません。

また、スマートイメージングは、Adobeのクラス最高のプレミアムCDN(コンテンツ配信ネットワーク)サービスと完全に統合され、パフォーマンスの向上をももたらします。 このサービスは、サーバー、ネットワーク、およびピアリングポイント間の最適なインターネットルートを見つけます。 インターネット上のデフォルトのルートを使用する代わりに、待ち時間が最も短く、パケット損失率が最も低いルートを見つけます。

次の画像アセットの例は、追加されたスマートイメージングの最適化を示しています。

| 画像 <br>（URL） | サムネール | サイズ<br>（JPEG） | サイズ（WebP）<br>（スマートイメージングを使用） | 削減 % |
|---|---|---|---|---|
| [画像 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [画像 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [画像 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [画像 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均 = 51% |

上記と同様に、Adobeでも7,009個のURLを含むテストを実施しました。 JPEG用のファイルサイズの最適化は、平均で38%も向上しました。 WebP形式のPNGの場合、ファイルサイズの最適化を平均で31%向上させることができました。 このような最適化は、スマートイメージングの機能があるので可能です。

## 最新のスマートイメージングの主要なメリットとは {#what-are-the-key-benefits-of-smart-imaging}

画像は、ページの読み込み時間の大部分を占めます。 したがって、パフォーマンスの向上は、コンバージョン率の増加、サイトでの滞在時間、サイトの直帰率の低下に大きな影響を与える可能性があります。

最新バージョンのスマートイメージングの機能強化：

* 最新のスマートイメージングを使用するWebページのGoogle SEOランキングを改善しました。
* 最適化されたコンテンツをすぐに（実行時に）提供します。
* Adobe Senseiテクノロジを使用して、イメージリクエストで指定された画質(`qlt`)に従って変換します。
* スマートイメージングは、`bfc` URLパラメータを使用してオフにできます。
* TTL（Time To Live）独立。以前は、スマートイメージングを機能させるには、最小 TTL 値 12 時間が必要でした。
* 以前は、元の画像と派生画像の両方がキャッシュされており、キャッシュを無効にする2つの手順が必要でした。 最新のスマートイメージングでは、派生物のみがキャッシュされ、1ステップのキャッシュ無効化プロセスが可能です。
* ルールセットでカスタムヘッダーを使用するお客様は、以前のバージョンのSmart Imagingとは異なり、最新のスマートイメージングを利用できます。これらのヘッダーはブロックされないためです。 例えば、[画像応答へのカスタム接触チャネル値の追加|Dynamic Mediaクラシック](https://helpx.adobe.com/jp/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)で推奨される「Timing Allow Header」、「X-Robot」などです。

## スマートイメージングにはライセンス費用がかかりますか？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

いいえ。スマートイメージングは、既存のライセンスに含まれています。 この規則は、Dynamic MediaクラシックまたはExperience ManagerDynamic Media(Cloud Serviceとしてのオンプレム、AMS、Experience Manager)に当てはまります。

>[!NOTE]
>
>スマートイメージングは、Dynamic Media — ハイブリッドのお客様はご利用いただけません。

## スマートイメージングはどのように機能しますか？ {#how-does-smart-imaging-work}

消費者から画像が要求されると、スマートイメージングはユーザの特性をチェックし、使用中のブラウザに基づいて適切な画像形式に変換する。 これらの形式変換は、視覚的忠実性を低下させない方法でおこなわれます。スマートイメージングは、次のような方法で、ブラウザーの機能に基づいて、自動的に画像を別の形式に変換します。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 次のブラウザー用に WebP に自動的に変換：
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari(iOS、macOS、iPadOS)で、WebPのブラウザーとOSバージョンのサポートが提供されている
   * Android™
   * Opera
* 以下のレガシーブラウザーでのサポート：

   | ブラウザー | ブラウザー／OS のバージョン | 形式 |
   | --- | --- | --- |
   | Safari | iOS/iPad 14.0以前またはmacOS BigSur | JPEG2000 |
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

## スマートイメージングは、既に使用されている既存の画像プリセットとどのように連携しますか？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

スマートイメージングは、既存の「画像プリセット」と連携します。 要求されたファイル形式がJPEGまたはPNGの場合は、画質(`qlt`)および形式(`fmt`)を除くすべての画像設定が監視されます。 形式変換の場合、スマートイメージングは、画像プリセットの設定によって定義されたとおりに完全な視覚的な再現性を維持しますが、ファイルサイズは小さくなります。 元の画像サイズがスマートイメージングの生成するサイズより小さい場合は、元の画像が提供されます。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## スマートイメージングのために、URLや画像プリセットを変更するか、サイトに新しいコードを導入する必要がありますか。{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

既存のカスタムドメインで設定する場合、スマートイメージングは既存の画像 URL や画像プリセットとシームレスに連携します。また、スマートイメージングでは、ユーザーのブラウザーを検出するために Web サイトにコードを追加する必要はありません。すべて自動的に処理されます。

スマートイメージングを使用するように新しいカスタムドメインを設定する場合は、このカスタムドメインを反映するようにURLを更新する必要があります。

スマートイメージングの前提条件を理解するには、[スマートイメージングを使用する資格があるか](#am-i-eligible-to-use-smart-imaging)を参照してください。

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## スマートイメージングは HTTPS で機能しますか？HTTP/2 ではどうですか？ {#does-smart-imaging-working-with-https-how-about-http}

スマートイメージングは、HTTP または HTTPS で配信された画像に対して機能します。また、HTTP/2 上でも機能します。

## スマートイメージングを使用するための資格を私は満たしていますか？ {#am-i-eligible-to-use-smart-imaging}

スマートイメージングを使用するには、会社のDynamic MediaクラシックまたはExperience ManagerアカウントのDynamic Mediaが次の要件を満たしている必要があります。

* ライセンスの一部としてアドビによってバンドルされている CDN（コンテンツ配信ネットワーク）を使用している。
* 汎用ドメイン（例えば、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` など）ではなく、専用ドメイン（例えば、`images.company.com` または `mycompany.scene7.com`）を使用してください。

ドメインを探すには、[Dynamic Mediaクラシックデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社アカウントにサインインします。

**[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をタップします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在汎用ドメインを使用している場合は、独自のカスタムドメインに移動するようにリクエストできます。 テクニカルサポートチケットを送信したら、このトランジションリクエストを作成します。

最初のカスタムドメインは、Dynamic Media ライセンスを使用する場合、追加費用はかかりません。

## 自分のアカウントでスマートイメージングを有効にするには、どうすればいいですか？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

お客様は、スマートイメージングを使用する要求を開始します。自動的には有効になりません。

1. [Admin Console を使用して、サポートケースを作成します。](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. サポートケースには、以下の情報を記入してください。

   1. 主要連絡先の氏名、電子メールアドレス、電話番号。
   1. スマートイメージングを有効にする全ドメイン（`images.company.com` や `mycompany.scene7.com`）。

      ドメインを探すには、[Dynamic Mediaクラシックデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社アカウントにサインインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。
   1. 直接的な関係で管理されているのではなく、アドビを通じて CDN を使用していることを確認します。
   1. `s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用ドメインではなく、`images.company.com` や `mycompany.scene7.com` などの専用ドメインを使用していることを確認します。

      ドメインを探すには、[Dynamic Mediaクラシックデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社アカウントにサインインします。

      **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。

      「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media Classic ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。
   1. HTTP/2で動作させるかどうかを指定します。

1. Adobeカスタマーケアにより、要求が送信された順序に基づいて、スマートイメージングのカスタマー待機リストに追加されます。
1. Adobeがリクエストを処理する準備が整ったら、ターゲット日を調整して設定するよう、カスタマーケアから連絡があります。
1. **オプション**:オプションで、Adobeが新機能を実稼動環境にプッシュする前に、ステージングでスマートイメージングをテストできます。
1. カスタマーケアの完了後、お知らせします。
1. スマートイメージングのパフォーマンス向上を最大限にするため、アドビでは、有効期間（TTL）を 24 時間以上に設定することを推奨しています。TTL によって定義されるのは、アセットが CDN によってキャッシュされる期間です。この設定を変更するには、次の手順を実行します。

   1. Dynamic Media Classic を使用している場合は、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。「**[!UICONTROL 初期設定のクライアントキャッシュの有効期限]**」の値を 24 以上に設定します。
   1. Dynamic Media を使用する場合は、[次の手順](config-dm.md)に従います。「**[!UICONTROL 有効期限]**」の値を 24 時間以上に設定します。

## 自分のアカウントでスマートイメージングが有効になるのはいつ頃ですか？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

リクエストは、待機リストに従って、カスタマーケアが受け取った順に処理されます。

>[!NOTE]
>
>スマートイメージングを有効にすると、Adobeがキャッシュをクリアするので、リードタイムが長くなる場合があります。 そのため、処理できる移行の数は、常にほんの数件です。

## スマートイメージングを使用するための切り替えに際しては、どんなリスクがありますか？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

顧客の Web ページを表示するリスクはありません。ただし、スマートイメージングにトランジションすると、CDNキャッシュがクリアされます。 この手順では、Experience Manager上でDynamic MediaクラシックやDynamic Mediaの新しい構成に移行します。

最初のトランジション中、キャッシュされていない画像は、キャッシュが再び再構築されるまで、Adobeの接触チャネルサーバーに直接ヒットします。 したがって、Adobeは、接触チャネルから要求を取り込む際に許容可能なパフォーマンスを維持できるよう、いくつかのトランジションを一度に処理する予定です。 ほとんどのお客様は、1 ～ 2日以内にCDNでキャッシュを完全に再構築できます。

## スマートイメージングが想定どおりに機能しているかどうかを確認するには、どうすればいいですか？ {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. スマートイメージングを使用してアカウントを設定したら、ブラウザーにDynamic MediaクラシックまたはAdobe Experience Manager-Dynamic MediaイメージURLを読み込みます。
1. Chrome ブラウザーで&#x200B;**[!UICONTROL 表示／デベロッパー／デベロッパーツール]**&#x200B;をクリックしてデベロッパーパネルを開きます。または、別のブラウザーのデベロッパーツールを使用します。

1. 開発者ツールを開いている場合は、キャッシュが無効になっていることを確認します。

   * Windows®では、Developer Toolペインの設定に移動し、**[!UICONTROL 「（devtoolsが開いている間は）キャッシュを無効にする」]**&#x200B;チェックボックスをオンにします。
   * macOSの場合は、開発者ペインの「**[!UICONTROL ネットワーク]**」タブで、**[!UICONTROL キャッシュを無効にする]**&#x200B;を選択します。

1. コンテンツタイプが適切な形式に変換されるのを監視します。次のスクリーンショットは、Chrome 上で PNG 画像が動的に WebP に変換されているのを示しています。
1. このテストを、様々なブラウザーやユーザー条件で繰り返します。

>[!NOTE]
>
>すべての画像が変換されるわけではありません。スマートイメージングは、変換によってパフォーマンスが向上するかどうかを決定します。 予期されるパフォーマンスゲインがない場合や、形式がJPEGやPNGでない場合、画像が変換されないことがあります。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 要求に対してスマートイメージングをオフにできますか？ {#turning-off-smart-imaging}

はい。URL に `bfc=off` 修飾子を追加して、スマートイメージングをオフにできます。

## どの「チューニング」が使用できますか。定義できる設定やビヘイビアーはありますか。(#tuning-settings)

現在、オプションでスマートイメージングを有効または無効にできます。他のチューニングは使用できません。

## スマートイメージングが画質設定を管理する場合、設定できる最小値と最大値はありますか。 例えば、「60 以上」や「80 以下」というクォリティを設定できますか。(#minimum-maximum)

現在のスマートイメージングには、このようなプロビジョニング機能はありません。

## WebP画像ではなくJPEG画像がChromeに返されることがあります。 なぜ変化が起こるのでしょう？ (#jpeg-webp)

スマートイメージングは、変換が有益かどうかを判断します。変換結果のファイルサイズが同等の画質で小さくなる場合にのみ、新しい画像が返されます。
