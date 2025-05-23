---
title: Dynamic Media ジャーニー（第 1 部）
description: Dynamic Media ジャーニーでは、Dynamic Media の基本的な仕組み、Dynamic Media で可能なこと、仕事や顧客にもたらす価値について説明します。
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3615'
ht-degree: 100%

---

# Dynamic Media ジャーニー：基本知識（第 1 部） {#dm-journey-part1}

{{see-also-dm}}

Dynamic Media ジャーニーへようこそ。

このジャーニーでは、Dynamic Media の基本的な仕組み、Dynamic Media で可能なこと、仕事や顧客にもたらす価値について説明します。

**_前提条件_**

* 画像およびビデオ形式の基本的な理解
* HTML と CSS の基本的な理解
* Adobe Illustrator、Adobe Photoshop、Adobe XD などのデザインツールの基本的な理解
* Experience Manager 上の Dynamic Media へのアクセスは役に立ちますが、必須ではありません

**_学習内容_**

_第 1 部_

* Dynamic Media の概要と機能
* Dynamic Media のユースケース
* Dynamic Media システムでのアセットのフロー

_第 2 部_

* Dynamic Media URL の分解と Dynamic Media のコンテンツ配信方法
* アセットをレンダリングするための画像プリセットの作成の基本
* 画像セット、スピンセット、混在メディアセット

**_対象読者_**
このジャーニーの最適な読者は、Experience Manager 上の Dynamic Media を初めて使用する以下のユーザーです。

* 管理者
* ビジネスアナリスト
* コンテンツアーキテクト
* コンテンツ作成者
* デザイナー
* 開発者
* マーケター
* 製品管理者／所有者

>[!TIP]
>
>最良の結果を得るには、デスクトップコンピューターでこの Dynamic Media ジャーニーを表示して読むことをお勧めします。

## Dynamic Media の概要と機能 {#dm-journey-a}

Dynamic Media は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するのに役立ちます。また、ズーム、360 度スピン、ビデオなどのインタラクティブな視聴エクスペリエンスの作成と提供にも役立ちます。アセットは、web サイト、モバイルサイトおよびソーシャルサイトでの利用に合わせて動的に拡大縮小されます。Dynamic Media では、画像、ビデオ、3D などの一連のプライマリソースアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルな CDN（コンテンツ配信ネットワーク）経由で、リッチコンテンツの複数のバリエーションをリアルタイムで生成および配信します。

Dynamic Media は、デジタルアセット管理ソリューション Adobe Experience Manager Assets のワークフローを取り込むことで、デジタルキャンペーン管理プロセスを簡易化し効率化します。

### 無限の可能性を持つ 1 つのファイル

Dynamic Media について理解するための主なポイントの 1 つは、_無限の可能性を持つ 1 つのプライマリアセットファイル_&#x200B;という概念です。

この概念をより深く理解するために、画像やビデオなどの単一アセットの従来の操作方法を考えてみましょう。通常は、1 つのプライマリアセットを作成します。次に、そのアセットのバージョンを、アセットが使用されるエクスペリエンスごと、必要なデバイスごと、web ページごとに手動で作成します。時間が経つと、1 つのアセットが 20、30、またはそれ以上のバージョンに増え、バージョン履歴も残らなくなります。保有している画像やビデオごとに、この操作を行うことを想像してみてください。アセットバージョンは、あっと言う間に圧倒的な数に増えて維持管理と更新が困難になります。ストレージコストの増加は言うまでもありません。

一方、Dynamic Media は他のシステムとは基本的に異なり、単一のプライマリアセットや RL 呼び出しから&#x200B;_動的に_&#x200B;メディアを配信します。Dynamic Media の URL パスには、顧客の画面にアセットを配信する際に、アドビのパブリッシュサーバーに表示方法を指示する命令が含まれています。例えば、同一のプライマリアセットを使用して、サイズ、形式、解像度、線幅、カラー、切り抜き、ズームビューなどのエフェクトを変更しながら無数のレンディションで即座に配信することができます。

この独自の配信方法では、サイズや帯域幅に関係なく、一貫した品質のエクスペリエンスを任意の画面に確実に配信できます。また、フルサイズのビデオが、画面に応じて最適化され、アダプティブにストリーミングされるので、一貫性のある高品質なユーザーエクスペリエンスが保証されます。

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media は、同じプライマリ画像を異なるメディアに異なるサイズと形式で配信します](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media は、サイズや帯域幅に関係なく、一貫性のある高品質なエクスペリエンスをあらゆる画面に確実に提供します。_

以下では、この「無限の可能性を持つ 1 つのプライマリアセットファイル」という概念が重要な理由を詳しく説明します。

### コンテンツ配信ネットワーク

画像アセットまたはビデオアセットは、運用開始の準備が整ったら、Dynamic Media バックボーンである最上位層の強力な配信ネットワークによってサポートされます。このネットワークでは、毎日、世界中の何百ものクライアントに配信しています。アセットは、Akamai によりホストされているコンテンツ配信ネットワーク（CDN）で配布されます。CDN は、透過的に連携してコンテンツ、特に大容量のリッチメディアコンテンツをエンドユーザーに配信する、ネットワーク接続されたコンピュータサービスのシステムです。

CDN システムでは、web コンテンツはインターネット上の web キャッシュに保存されます。その後、web キャッシュからエンドユーザーに配信されるので、配信が高速化されます。ユーザーが初めて web ページをダウンロードしたときに、表示されるアセットは CDN キャッシュに配信されます。これらはサーバーに保存されるので、同じ領域のユーザーが次回その web ページにアクセスしたときは、キャッシュされた同じコンテンツがより高速に配信されます。コンテンツはエンドユーザーに近い場所に配置されるので、より高速に配信されます。CDN を使用すると、web ページの表示が高速化される一方、どのインスタンスでもコンテンツが中央のサーバーからではなくキャッシュネットワークから配信されるので、中央サーバーの帯域幅の需要は減少します。この最適化されたフローの結果、ユーザーエクスペリエンスが向上し、売上の増加につながります。

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

これまで、CDN は、毎月 3.5 ペタバイトのトラフィックを顧客に配信してきました。このシステムは 1 日に 520 億個のアセットを配信できます。これは、_毎秒_ 864,000 個の画像およびビデオが顧客に正常に配信されることに相当します。

### スマートイメージング

Dynamic Media はすでに優れた働きをしています。これには、CDNを利用したアセットの最適化や、各アセットのモバイルやデスクトップシステムでの迅速な読込みが含まれます。これを実現するために、Dynamic Media では、画像の品質を定義するために画像プリセットが使用されています。また、送信する画像のタイプや鮮明さなど、エクスペリエンスやページの様々な要素も定義されます。

さらに、Dynamic Media には、画像プリセット以外にさらに価値を付加するために、_スマートイメージング_&#x200B;も用意されています。

スマートイメージングは、顧客のブラウザー機能に応じて画像の形式とファイルサイズを自動的に最適化することで、画像アセット配信のパフォーマンスをさらに向上させます。既存の画像プリセット（画像プリセットについては、このジャーニーの第 2 部で説明します）と連携し、配信時にインテリジェンスを使用します。

このインテリジェンスにより、ブラウザーとネットワーク接続速度に応じて、画像ファイルのサイズがさらに縮小されます。画像アセットはページの読み込み時間のほとんどを占めるので、このパフォーマンス向上は次のような主要ビジネス指標に大きな影響を及ぼす可能性があります。

* コンバージョンの向上
* サイトでの滞在時間
* サイトバウンス率の低下

スマートイメージングを使用すると、既存の画像プリセット設定やエンドユーザーの特定の特性に応じて、全体として 22～47％のパフォーマンス向上を期待できます。その一方で、元の画質はそのまま維持することができます。

![スマートイメージング](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_スマートイメージングは、顧客のブラウザー機能とネットワーク速度に応じて画像の形式とファイルサイズを自動的に最適化します。_

スマートイメージングを使用するには Dynamic Media のテクニカルサポートとの連携が必要なので、スマートイメージングはデフォルトではオンになっていません。また、スマートイメージングを有効にするには、CDN キャッシュを一度完全にクリアする必要があります。その後、キャッシュには、時間の経過と共にデータがまた保存されていきます。スマートイメージングの使用に関心がある場合は、テクニカルサポートチケットを送ることで、アドビと協力してスマートイメージングを有効にすることができます。次に、スマートイメージングを試すことができる URL パラメーターがテクニカルサポートから提供されます。どの web ページや画像でも試すことができるので、実際のパフォーマンスやメリットを確認できます。その後、サイト全体に対してスマートイメージングを有効にすることができます。

### アダプティブビデオセット

あるページやメインページにビデオがある場合、顧客がそのコンテンツに関わる時間やページに留まる時間が長くなる傾向がありますが、これは基本的に良いことです。これは、アドビが実施した分析を通じて明らかになっています。ただし、ビデオは扱いが複雑になりがちです。1 つには、多くの場合、プライマリファイルが大きくなります。表示しているデバイスや帯域幅に関係なくエクスペリエンスがスムーズに実行されるようにビデオをサイズ設定し、配信する方法を決定するのは簡単ではありません。

この問題を解決するために、Dynamic Media では&#x200B;_アダプティブビデオセット_&#x200B;を作成できるようになっています。

アダプティブビデオセットは、同じビデオを様々なビットレートおよび形式でエンコードしたバージョンをグループ化したものです。

まずオリジナルのプライマリビデオをシステムにアップロードします。Dynamic Media は、そのビデオを複数のビデオに自動的にサイジングつまり&#x200B;_トランスコード_&#x200B;します。次に、使用するビデオ画面、画質および形式を配信時にインテリジェントに決定し、携帯電話、タブレット、デスクトップコンピューターなどにビデオを配信します。

例えば、iOS モバイルデバイスでは、4G、5G、Wi-Fi などの帯域幅が検出されます。次に、アダプティブビデオセット内の様々なビデオのビットレートの中から、適切なエンコード済みビデオが自動的に選択されます。ビデオは、モバイルデバイス、タブレット、デスクトップコンピューターにストリーミングされます。

さらに、ネットワークの状態が変化した場合は、ビデオ画質が自動で動的に切り替わります。また、デスクトップが全画面表示モードに切り替わった場合、アダプティブビデオセットがより高い解像度を使用するように応答するので、ユーザーの視聴エクスペリエンスが向上します。

アダプティブビデオセットを使用すると、Dynamic Media ビデオを複数の画面やデバイスで再生するユーザーが、スムーズに高画質再生を行えます。これにより、ビデオの扱いの複雑さが解消されます。

## Dynamic Media のユースケース {#dm-journey-b}

次に、肯定的な顧客エンゲージメント、ロイヤルティ、コンバージョン、ROI 向上を推進するために、Dynamic Media が役に立つ可能性がある一般的なユースケースについて、問題と解決策を説明します。

### ユースケース：プライマリファイルアプローチ

Dynamic Media の最も重要なユースケースの 1 つは、最も明白なユースケースの 1 つでもあります。つまり、配信されるページやエクスペリエンスを軽量化し、画像やビデオなどのコンテンツのサイズを小さくします。

以下に示すのは、典型的なエクスペリエンスまたは web ページです。ページの約 90％は、画像やビデオなどのリッチメディアで構成されています。一般に、これらははるかに重いファイルになります。

![コンテンツページの重さ](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_典型的な web ページのコンテンツページの重さ。_

残りの 10％はHTML、CSS コードおよび特定のタグです。そのページの 90％の重さを最適化しようとする場合、Dynamic Media がその作業に役立ちます。先ほど、_無限の可能性を持つ 1 つのプライマリアセットファイル_&#x200B;という概念について説明しました。このアプローチは、ページ全体の重さを軽減するうえで重要です。1 つのプライマリアセットを製品詳細ページ、サムネールページ、買い物かごおよび検索グリッドで使用できるので、時間を大幅に節約できます。また、エクスペリエンス間の一貫性も保てます。

![プライマリファイルアプローチ](/help/assets/dynamic-media/assets/dm-onefile.png)
_watch は 1 つのプライマリアセットファイルですが、その場で作成された複数のレンディション（コピーではなく）があります。_

1 つのファイルに関して Dynamic Media で解決している問題と、そのアプローチに対する解決策のいくつかを詳しく見てみましょう。

| **問題** | **Dynamic Media の解決策** |
|---|---|
| アセットごとに作成と保存が必要。 | 1 つの画像ファイルを使用し、必要なレンディションを配信時に自動的に作成します。 |
| ストレージコストが高い。 | アセットの複数のコピーを作成して保存する必要がなくなります。 |
| 管理の連鎖を維持するのが難しい。 | デバイスに最適化された一貫性のあるエクスペリエンスの配信を保証します。 |
| バージョン履歴がない。 | |
| デバイス間でブランドエクスペリエンスの一貫性がない。 | |
| 重複したアセット作成により不要なコストが発生する。 | |

1 つのファイルについて考えると、エクスペリエンスの種類ごとにアセットを作成することになります。例えば、出発点となる画像が 1 つあって、その画像の 20 個、30 個、40 個のバリエーションを作成する必要があるとすると、最終的にそれらを保存し、そのストレージの費用を支払う必要があります。

この場合、必ず適切な画像が使用されるようにする必要があるので、ブランド間の一貫性を保つことに影響が及ぶ可能性があります。また、画像が見つからない場合は、元に戻って、それらのアセットを複製する必要があります。

Dynamic Media では、出発点となる 1 つの画像から画像のバリエーションをその場で作成できます。そのため、グラフィックデザイナーやフォトスタジオと何度もやり取りして追加コンテンツを作成する必要がなく、プライマリアセットでクリエイティブの作業を行うことができます。そして、それはお金と時間の節約になります。

1 ファイルアプローチでは、1 つのプライマリファイルを使用します。次に、配信時または顧客による閲覧時に、サイトやプロパティおよびエクスペリエンスで必要なバージョンまたはレンディションを作成します。この効率化により、アセットに必要なストレージの量を大幅に削減し、ワークフロー全体の複雑さを軽減できます。また、Dynamic Media の配信システムを使用すると、あらゆる画像とビデオの最適化、迅速な読み込み、あらゆる画面やデバイスでの整った表示が保証されます。

### ユースケース：ビデオ

Dynamic Media で解決されるもう 1 つのユースケースはビデオです。ビデオは複雑です。管理も困難です。ビデオファイルは、ファイルサイズが原因で、保存や移動に難点があります。

| **問題** | **Dynamic Media の解決策** |
|---|---|
| 様々なデバイス向けに最適化されたビデオの管理と配信が困難。 | すべてのデバイスに合わせて自動的にサイズ調整される 1 つのビデオを使用します。 |
| ユーザーの使用可能な帯域幅が原因で、ビデオが停止したり低画質で再生されたりする。 | 使用可能な帯域幅を自動検出し、画質を調整して高い忠実性とスムーズな再生を確保する HTML プレーヤーでビデオを再生します。 |
| デバイスを問わず良好な表示と再生を確保するためにビデオのすべてのバージョンを手動で作成するのは実現不可能で時間がかかる。 | ワークフローを簡素化して、何時間もの煩雑なトランスコーディング作業をなくします。 |
| | より価値の高い作業のために時間を空けます。 |

顧客は、次のような問題を解決したいと考えて Dynamic Media にたどり着きます。

「_弊社のビジネスにはビデオがあり、ビデオ部門で多額の費用をかけて制作しましたが、ページへの掲載や配信には躊躇しました。その理由は、テストした結果、ビデオの品質が保証されない、あるいは本当に再生できるかどうかもわからないからでした。そして、最終的に、それがビジネスのブランドやコンバージョンの役割に潜在的に影響を及ぼす可能性があります。_」

Dynamic Media の解決策は、1 つのプライマリビデオファイルを基に、Dynamic Media のトランスコーディングプロセスを通じてあらゆるサイズのファイルを作成できるようにすることです。次に、それを Dynamic Media のインテリジェントビデオプレーヤーとペアリングします。このワークフローにより、ビデオをメインのランディングページで使用しているか、カテゴリページや製品詳細ページで使用しているかに関わらず、全体でビデオの一貫性が保たれ、高画質で配信されるようになります。

検討すべきその他のユースケースを以下に示します。

### ユースケース：唯一の信頼できる情報源

| **問題** | **Dynamic Media の解決策** |
|---|---|
| デジタルアセットが組織のあちこちに分散し、複数の異なるチームやビジネスユニットにサイロ化されている。 | すべてのデジタルアセットを一元的に保存および管理します。 |
| チームメンバーがローカルバージョンをダウンロードおよび作成する。 | チームメンバーは、1 つのプライマリファイルを使用して、様々な画面サイズやデバイスで必要なすべてのバージョンを作成&#x200B;_および_&#x200B;配信します。 |
| エクスペリエンスやデバイスごとに「使い捨て」のアセットが作成される。 | 使い捨てのアセットをなくし、それらの作成にかかる時間とコストを節約します。 |

### ユースケース：AI を活用したリッチメディア向けスマート切り抜き

| **問題** | **Dynamic Media の解決策** |
|---|---|
| 画像やビデオを手作業で制作、測定、カットして、重要な部分を強調したり、あらゆる画面サイズやデバイスで適切に表示できるようにするには、時間と労力がかかる。 | Dynamic Media の Adobe Sensei AI 機能の 1 つであるスマート切り抜きを使用して、どのような画像やビデオでも重要な部分を自動的に検出し、切り抜いて維持管理します。 |
| 本来ならインパクトの大きいエクスペリエンスの作成に費やすことができる時間が浪費される。 | 画面のサイズに関係なく、目的の部分をキャプチャします。 |
| エクスペリエンスやデバイスごとに「使い捨て」のアセットが作成される。 | 煩雑な手作業をなくし、あらゆるデバイスや画面で整って見える高画質かつ高速読み込み可能な画像やビデオを配信します。 |

### ユースケース：インタラクティブメディアのオーサリング

| **問題** | **Dynamic Media の解決策** |
|---|---|
| カスタマーエクスペリエンスが平凡で静的なので、エンゲージメント、ロイヤリティの醸成、コンバージョンの促進につながらない。 | 技術に詳しくないユーザーでも、ホットスポット、カルーセル、スピンセットなどのインタラクティブ要素を簡単かつシームレスに追加して、より動的で魅力的なエクスペリエンスを実現できます。 |
| デジタルアセットから得られる投資回収率（ROI）が低く、カスタマーエクスペリエンスがパッとしない。 | リッチメディアエクスペリエンスからコンバージョンと投資回収率を促進します。 |

## Dynamic Media システムでのアセットのフロー {#dm-journey-c}

Dynamic Media の典型的なワークフローを下図に示します。

![Dynamic Media ワークフロー](/help/assets/dynamic-media/assets/dm-workflow.png)
_Dynamic Media システム内でのアセットのフロー。_

最終的にはプライマリアセットを作成することを主な目標に、作成フェーズから始めます。プライマリアセットは、写真撮影やビデオベンダーから入手することもできますし、自分で作成したオーディオファイルでも構いません。Adobe InDesign、Adobe Photoshop、Adobe Illustrator といったアドビの Creative Suite アプリケーションを、コンテンツの作成に役立てることができます。

作成フェーズが完了したら、アセットを Dynamic Media にアップロードすることで、アセットをオーサリングソリューションに配置します。Dynamic Media 内で、サイト上の様々な web ページに適した画像プリセットおよびビューアを準備します。

最終的には、web、印刷、メール、デスクトップ、モバイルデバイスで使用できるように、コンテンツをすべて最適化して Dynamic Media サーバーに公開します。

### Dynamic Media へのアセットのアップロード

プライマリアセットの作成が完了したら、プライマリアセットを Dynamic Media にアップロードします。アップロードするファイルの種類やファイルの形式およびサイズは、Dynamic Media にとって重要な属性です。1 ファイルアプローチのサポートから最大限の価値を確実に引き出す必要があるのは、アップロード時です。

例えば、以下の腕時計の画像は 4560 x 3020 ピクセルです。そのサイズの画像を使用することはない場合でも、アップロードはできます。画像が大きいほど、Dynamic Media で配信できる画質は、サムネールレンディションに至るまで良くなります。注意：既存画像の解像度を&#x200B;_下げる_&#x200B;ことは簡単です。しかし、画像の解像度を&#x200B;_上げよう_&#x200B;としても、満足できない結果になる可能性が高いものになります。

![Dynamic Media へのアップロードにお勧めの形式](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_アセットのアップロードに関する考慮事項。_

可逆圧縮形式でアセットをアップロードすることをお勧めします。一般に、JPEG は避けた方がよいでしょう。JPEG で配信する場合や JPEG で保存を繰り返すと、時間が経つにつれて画質が低下するからです。使用可能な可逆圧縮形式の最も高い解像度の画像から始めます。その形式は通常、TIFF または PNG ファイルです。

カラースペースに関しては、デジタルチャネルや web ビューを検討する場合、通常は RGB（赤、緑、青）を考えます。

CMYK で配信しようとは思わないでしょう。その理由さえわからないでしょう。その理由は、カラースペースは印刷物の配信に使用されることが最も多いからです。ただし、Dynamic Media ではどちらのカラースペースでも配信できます。

倉庫型の卸売店など、今でも印刷を行っている顧客は多数存在します。また、毎週チラシを印刷することが多い食料品店もあります。このような顧客は、画像を両方のカラースペースで準備する必要があります。そのためには、従来、RGB 形式と CMYK 形式の 2 種類の画像が必要でした。しかし、現在は、CMYK アセットを直接 Dynamic Media にアップロードすれば、画像プリセットまたはカラープロファイルを通じて RGB アセットを自動的に配信することができます。ファイルの複数のバージョンを作成する必要がないので、_無限の可能性を持つ 1 つのプライマリアセットファイル_&#x200B;の概念が保たれます。

<!-- **The Value of Renditioning??? or Demo portion** -->

### アセットの公開とプレビュー

アセットを Dynamic Media にアップロードしたら、Dynamic Media でアセットを選択して、「**[!UICONTROL 公開]**」または「**[!UICONTROL クイック公開]**」をクリックして、アセットを&#x200B;_公開_&#x200B;することをお勧めします。アセットをエクスペリエンスで使用する場合は、アセットを公開する必要があります。アセットを公開すると、Dynamic Media で生成される URL をコピーして web ページで使用するか、web ページにコードを埋め込むことで、アセットを web ページに組み込むことができます。

アセットを手動で公開する以外にも、アップロード時にユーザーの操作なしでアセットが即座に公開されるように、Dynamic Media を設定することもできます。

アップロード後に、Dynamic Media でアセットのレンディションをプレビューするには、いくつかの方法があります。レンディションのプレビューは、顧客に表示される内容を把握するうえで役に立ちます。一般的なプレビュー方法としては、アセットを選択したあと、_画像プリセット_&#x200B;を選択してアセットのレンディションを表示します（下図を参照）。

![「Large」画像プリセットに基づくアセットのレンディションのプレビュー](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_選択した「Large」画像プリセットに基づくアセットのレンディションのプレビュー。「URL」ボタンをクリックしました。結果の URL パスには「Large」画像プリセット名が含まれており、このパスを web ページで使用できます。_

上記の URL は実際のものです。[試してみる](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}。

アセットをプレビューするもう 1 つの方法は、画像アセットを選択したあと、_ビューア_&#x200B;プリセットを選択することです（下図を参照）。

![ZoomVertical_light ビューアプリセットに基づくアセットのプレビュー](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_選択した「ZoomVertical_light」ビューアプリセットに基づくアセットのプレビュー。画像上でマウスポインター（「`+`」）を移動してズームインしました。「URL」ボタンと「埋め込み」ボタンに注目してください。_

上記の レンディション は実際のものです。[試してみる](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target="_blank"}。

## オプション - 詳細情報

このジャーニーの第 1 部では、様々な Dynamic Media トピックの基本を説明しました。ここで学んだ内容についてさらに詳しく知るには、以下の資料を参照してください。または、ジャーニーの第 2 部に進んでください。[この Dynamic Media ジャーニーの次のステップ](#whats-next)を参照してください。

<!--
_Dynamic Media Help topics_

* [Work with Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [About Smart Imaging](/help/assets/dynamic-media/imaging-faq.md)
* [How to create Adaptive Video Sets](/help/assets/dynamic-media/video.md)
* [Best practices for optimizing the quality of your images](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [How to upload assets](/help/assets/add-assets.md#upload-assets)
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to deliver Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [How to publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Work with Selective Publish in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md) -->

_Dynamic Media チュートリアル_

* [Experience Manager Assets での Dynamic Media の使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=pt-BR)
* [Adobe Experience Manager コンテンツライブラリ](https://experienceleague.adobe.com/ja?lang=ja#recommended/solutions/experience-manager)（_Dynamic Media_ で検索）

_Dynamic Media ビューア_

* 各ビューアの[ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)

## この Dynamic Media ジャーニーの次のステップ {#whats-next}

このジャーニーの第 2 部では、Dynamic Media URL を詳しく調べ、アセット配信時の動作について理解を深めます。また、アセットをレンダリングするための画像プリセットの作成に関する基本事項を詳しく説明し、画像セット、スピンセットおよび混在メディアセットとそれらの作成方法についても説明します。

[Dynamic Media ジャーニー：基本知識（第 2 部）](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d)に移動します。

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->