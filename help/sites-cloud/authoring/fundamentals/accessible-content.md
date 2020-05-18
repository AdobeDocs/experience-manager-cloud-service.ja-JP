---
title: クラウドサービスとしてのAdobe Experience Manager向けアクセシブルコンテンツの作成（WCAG 2.1準拠）
description: 障碍のあるユーザーが Web コンテンツにアクセスして利用できるようにします。
translation-type: tm+mt
source-git-commit: 0f1ef5ab6ebc929ced669e47c8737d7401d5ea35
workflow-type: tm+mt
source-wordcount: '13935'
ht-degree: 48%

---


# アクセス可能なコンテンツ（WCAG 2.1 適合）の作成 {#creating-accessible-content-wcag-conformance}

World Wide Wec Consortium(WCAG)の [作業グループによって作成された](https://www.w3.org/TR/WCAG/)Webコンテンツアクセシビリティガイドライン(WCAG)2.1 [](https://www.w3.org/Consortium/アクティビティ#Accessibility_Guidelines_Working_Group)は、障害を持つユーザーが利用しやすく、使用しやすいように、一連の技術に依存しないガイドラインと成功基準で構成されています。

入門として、コンソーシアムは一連のセクションとサポートドキュメントを提供します。

* [WCAG 2.1の新機能](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [WCAG 2.1 に準拠する方法](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2.1 の理解](https://www.w3.org/WAI/WCAG21/Understanding/)
* [WCAG 2.1 の各種テクニック](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAGドキュメント](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

さらに、次を参照してください。
* Our [Quick Guide to WCAG 2.1](/help/onboarding/accessibility/quick-guide-wcag.md).
* アドビのソリューション用の [アクセシビリティ準拠レポート](https://www.adobe.com/accessibility/compliance.html)。

<!-- 
>* [Configuring the Rich Text Editor for producing accessible conten](/help/sites-administering/rte-accessible-content.md)
-->

ガイドラインは、次の3つの準拠レベルに従って評価されます。 レベルA（最下位）、レベルAA、レベルAA（最高）。 各レベルの簡単な定義を次に示します。

* **レベル A：**&#x200B;サイトのアクセシビリティ基本的な最小レベルに達します。このレベルに達するには、レベル A の達成基準をすべて満たしている必要があります。
* **レベルAA:** これは、基本的なレベルのアクセシビリティに到達し、ほとんどの状況でほとんどのテクノロジーを使用しているほとんどの人がアクセスできるように、注力すべき理想的なレベルのアクセシビリティです。 このレベルに達するには、レベル A とレベル AA の達成基準をすべて満たしている必要があります。
* **レベル AAA：**&#x200B;きわめて高いレベルのアクセシビリティが確保されているサイトです。このレベルに達するには、レベル A、レベル AA、レベル AAA の達成基準をすべて満たしている必要があります。

サイトを作成する際は、サイトの全体的なレベルを特定する必要があります。

The following section presents [layers of the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) with related success criteria for Level A and Level AA [conformance levels](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1).

>[!NOTE]
>
>このドキュメントでは、次の表記を使用しています。
>
>* The [short names for the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* The [numbering used in the WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) to aid cross-referencing with the WCAG website.


## 原則 1：知覚可能 {#principle-perceivable}

[原則 1: 知覚可能 - 情報およびユーザーインターフェイスコンポーネントは、ユーザーが知覚できる方法でユーザーに提示可能でなければならない。](https://www.w3.org/TR/WCAG/#perceivable)

### 代替テキスト（1.1）{#text-alternatives}

[ガイドライン 1.1 代替テキスト：すべてのテキスト以外のコンテンツには、拡大印刷、点字、音声、シンボル、平易な言葉などのユーザーが必要とする形式に変換できるように、代替テキストを提供すること。](https://www.w3.org/TR/WCAG/#text-alternatives)

### テキスト以外のコンテンツ（1.1.1） {#non-text-content}

* 達成基準 1.1.1
* レベル A
* テキスト以外のコンテンツ：ユーザーに提示されるすべてのテキスト以外のコンテンツには、同等の目的を果たす代替テキストが提供されます。ただし、次の場合は除きます。

#### 目的 - テキスト以外のコンテンツ（1.1.1）{#purpose-non-text-content}

Web ページ上の情報はテキスト以外の様々な形式（写真、ビデオ、アニメーション、チャート、グラフなど）で指定できます。視覚に障碍のあるユーザーは、テキスト以外のコンテンツを見ることができませんが、スクリーンリーダーによる読み上げや、触覚で感知可能な点字表示デバイスを使用すれば、テキストコンテンツにアクセスできます。そのため、グラフィカルな形式にコンテンツの代替テキストを指定することにより、グラフィカルなコンテンツを見ることができないユーザーも、そのコンテンツが提供するものと同等の情報にアクセスできます。

もう 1 つのメリットとして、代替テキストを使用すると、検索エンジンのテクノロジーによってテキスト以外のコンテンツのインデックスを作成できます。

#### 達成方法 - テキスト以外のコンテンツ（1.1.1） {#how-to-meet-non-text-content}

静的なグラフィックの場合、そのグラフィックと同等の代替テキストを指定することが基本的な要件です。これは、 **代替テキスト** フィールドで実行できます。 例えば、コアコンポーネント **[画像](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/image.html)**。

>[!NOTE]
>
>標準搭載のコアコンポーネント( **[カルーセルなど](https://docs.adobe.com/content/help/jp/experience-manager-core-components/using/components/carousel.html)**)には、個々の画像に代替テキスト記述を追加する**代替テキスト&#x200B;**フィールドを提供しないものもありますが、コンポーネント全体に「**Label ****[(](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** Accessibility)」フィールド(AccessibilityTab)があります。
>
>AEM インスタンスにこれらのバージョンを実装する場合は、作成者がコンテンツに追加できるように、開発チームは `alt` 属性をサポートするようにこれらのコンポーネントを設定する必要があります（「追加の HTML 要素および属性のサポートの追加」を参照）。

<!--
>Some out-of-the-box Core Components, such as **[Carousel](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)** do not provide an **Alternative Text** field for adding alternate text descriptions to individual images, though there is the **Label** field (**[Accessibility](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** tab) for the entire component. 
>
>When implementing versions of these for your AEM instance, your development team will need to configure such components to support the `alt` attribute so that authors can add it to the content (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

AEM では、デフォルトで入力される「**代替テキスト**」フィールドが必要です。If the image is purely decorative and alternative text would be unnecessary, the **Image is decorative** option can be checked.

#### 適切な代替テキストの作成 {#creating-good-text-alternatives}

テキスト以外のコンテンツには様々な形式があるので、代替テキストの値は、Web ページにおけるグラフィックの役割に応じて異なります。従う必要のある一般的な手法を次に示します。

* 代替テキストは、簡潔でありながら、テキスト以外のコンテンツによって提供されている情報の要点を明確にとらえる必要があります。
* 過剰に長い説明（100 文字超など）は避けてください。代替テキストに詳細を追加する必要がある場合は、次のようにします。
   * 代替テキストで短い説明を提示する
   * 同じページの別の場所、または別の Web ページに長い説明を表示し、画像をリンクにするか、画像の横にテキストリンクを配置することで、この別の説明にリンクを設定する
* 代替テキストでは、同じページ上のすぐ近くにテキスト形式で提示されているコンテンツをレプリケートしないでください。多くの画像は、ページのテキストで既に取り上げられている項目の説明なので、詳細な代替テキストが既に存在している場合があります。
* テキスト以外のコンテンツが別のページまたはドキュメントへのリンクであり、同じリンクを形成しているテキストが他にない場合、画像の代替テキストは、画像を説明するものではなく、リンク先を示すものにする必要があります。
* テキスト以外のコンテンツがボタン要素に含まれていて、同じボタンを形成するテキストがない場合、画像の代替テキストは、画像を説明するものではなく、ボタンの機能を示すものにする必要があります。
* 画像に空の（ヌルの）代替テキストを割り当てるのは、問題ありませんが、画像に代替テキストを必要としない（例えば、純粋に装飾的なグラフィック）場合や、ページのテキストに同等のテキストが既に存在する場合に限ります。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

代替テキストを必要とするテキスト以外のコンテンツには、以下のようなタイプがあります。

* 説明写真：人や物や場所の画像です。ページ内の写真の役割を考えることが重要です。通常は、支援テクノロジーが要素のタイプ( `graphic` や `image`)を発表する際に、画像コンテンツについて説明することをお勧めします。 代替テキストの説明を使用する際 `screenshot` や使用する際の明確さ `illustration` を高めることができますが、状況に応じて異なります。 一貫性は大きな要因です。オーサリングチーム全体に対して決定を行い、この決定をユーザーエクスペリエンス全体に適用する必要があります。
* アイコン：特定の情報を伝える小さい絵文字です。ページおよびサイト全体で一貫して使用する必要があります。1 つのページまたはサイト上の同じアイコンにはすべて、短く簡潔な同じ代替テキストを含める必要があります。ただし、そうすることにより、隣接するテキストと不要な重複が発生する場合を除きます。
* チャートとグラフ：通常は数値データを表します。よって、代替テキストを提供する 1 つのオプションとしては、チャートまたはグラフィックで示されている主なトレンドの簡単な概要を含めることがあります。必要に応じて、「**詳細**」画像プロパティタブの「**説明**」フィールドを使用して、詳細な説明をテキストで提供します。さらに、ページまたはサイトの別の場所で、ソースデータを表形式で提供することもできます。
* マップ、図、フローチャート： 空間データを提供するグラフィック（例えば、オブジェクト間やプロセス間の関係の説明をサポートする）の場合は、主要なメッセージがテキスト形式で提供され、このテキスト情報が各関連データポイントの近くに配置されていることを確認します。 地図の場合、完全に同等なテキストを提供することは困難な場合が多いものの、特定の場所への行き方を見つける手段として地図が提供されている場合は、地図画像の代替テキストで「*X の地図*」と簡単に示し、ページ内の別の場所または&#x200B;**画像**&#x200B;コンポーネントの「**詳細**」タブの「**説明**」フィールドで、目的の場所への道案内を提供します。
* CAPTCHA：CAPTCHA は、*Completely Automated Public Turing test to tell Computers and Humans Apart*（コンピューターと人間を区別するための、完全に自動化された公開チューリングテスト）の略です。Web ページで人間と不正ソフトウェアを区別するために使用されるセキュリティチェックですが、アクセシビリティの障害となる可能性があります。これらの画像をユーザーが見て説明することにより、セキュリティテストに合格します。この画像の代替テキストを提供することは明らかに不可能なので、代わりに代替のグラフィック以外のソリューションを検討する必要があります。W3C では、いくつかの提案をおこなっています。例えば、以下の方法にはそれぞれメリットとデメリットがあるとされています。
   * 論理パズル
   * 画像の代わりに音声出力を使用
   * アカウントおよびスパムフィルターの使用制限
* 背景画像：HTML ではなくカスケーディングスタイルシート（CSS）を使用します。つまり、代替テキスト値の指定は不可能ということです。したがって、背景画像では重要なテキスト情報を提供しないでください。提供する場合は、同じ情報をページのテキストでも提供する必要があります。ただし、画像を表示できないときに代替の背景を表示することは重要です。

>[!NOTE]
>
>背景と手前のテキストの間には適度なコントラストが必要です。これについて詳しくは、[コントラスト（最低限）（1.4.3）](#contrast-minimum)を参照してください。

#### 詳細情報 - テキスト以外のコンテンツ（1.1.1） {#more-information-non-text-content}

* [達成基準 1.1.1 について](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [達成基準 1.1.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [W3C：CAPTCHA の説明と代替機能](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 時間依存メディア（1.2） {#time-based-media}

[ガイドライン 1.2 時間依存メディア：時間依存メディアには代替コンテンツを提供すること。](https://www.w3.org/TR/WCAG/#time-based-media)

This deals with web content that is *time-based*. This covers content that the user can play (such as video, audio, and animated content) and may be prerecorded or a live stream.

### Audio-only and Video-only (Prerecorded) (1.2.1) {#audio-only-and-video-only-prerecorded}

* 達成基準 1.2.1
* レベル A
* 音声のみおよび映像のみ（収録済み）：事前に収録済みの音声のみおよび映像のみのメディアには、以下が該当します。ただし、音声または映像がテキストの代替であり、その旨の明確なラベルが付けられている場合を除きます。
   * 収録済みの音声のみ：時間依存メディアの代替コンテンツが提供されており、収録済みの音声のみのコンテンツと同等の情報を提示している。
   * 収録済みの映像のみ：時間依存メディアの代替コンテンツまたは音声トラックが提供されており、収録済みの映像のみのコンテンツと同等の情報を提示している。

#### Purpose - Audio-only and Video-only (Prerecorded) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

次のようなユーザーに、アクセシビリティの問題が発生します。

* 視覚障碍のあるユーザー（音声がまったくない場合や、映像またはアニメーションの内容が音声で十分に伝えられていない場合）
* 音声を聞くことのできない、聴覚障碍のあるユーザー
* 音声を聞くことはできるが、内容を理解できないユーザー（理解できない言語が使用されている場合など）

映像または音声は、Adobe Flash など特定のメディア形式のコンテンツ再生をサポートしていないブラウザーやデバイスを使用しているユーザーも使用できない場合があります。

この情報を別の形式（テキストや、音声なしの映像に音声を付けるなど）で提供すると、元のコンテンツにアクセスできないユーザーがアクセス可能になります。

#### How to Meet - Audio-only and Video-only (Prerecorded) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* コンテンツがビデオのない録音済みのオーディオ（ポッドキャストなど）の場合：
   * 音声コンテンツの字幕のリンクをコンテンツの直前または直後に提示します。字幕は、話の内容と、話されていない重要な内容のすべてに相当するテキストを含む HTML ページとし、話者を明記し、状況説明、声の表情、その他の重要な音声の説明を含める必要があります。
* コンテンツがアニメーションの場合、またはオーディオのない事前に記録されたビデオの場合：
   * 映像で提供されている情報に相当するテキスト説明のリンクをコンテンツの直前または直後に提示します。
   * または、MP3 など一般的に使用されている音声形式で、相当する音声解説のリンクを提示します。

>[!NOTE]
>
>同じWebページ上に既に別の形式で存在するコンテンツの代替としてオーディオまたはビデオコンテンツを提供する場合は、別の代替オプションを追加する必要がない場合があります。
>
>WCAG 1.2.1に [ついて詳しくは、ガイドライン](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)「WCAG 1.2.1について」を参照してください。

AEM Webページへのマルチメディアの挿入は、画像の挿入と似ています。 ただし、マルチメディアコンテンツには静止画像より多くの機能が含まれているので、マルチメディアの再生方法を制御するために、様々な設定やオプションがあります。

>[!NOTE]
>
>情報提供のためのコンテンツでマルチメディアを使用する場合は、代替のリンクも作成する必要があります。例えば、字幕を含めるには、字幕を表示するための HTML ページを作成してから、音声コンテンツの横または下にリンクを追加します。

#### More Information - Audio-only and Video-only (Prerecorded) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [達成基準 1.2.1 について](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [達成基準 1.2.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### キャプション（事前記録）(1.2.2) {#captions-prerecorded}

* 達成基準 1.2.2
* レベル A
* キャプション（収録済み）：同期されたメディアに含まれるすべての収録済み音声コンテンツに対してキャプションが提供されます。ただし、そのメディアがテキストの代替メディアであり、その旨の明確なラベルが付けられている場合を除きます。

#### 目的 — キャプション（事前記録）(1.2.2) {#purpose-captions-prerecorded}

耳が聞こえない人や耳が聞こえにくい人は、オーディオコンテンツにアクセスできないか、非常に難しくなります。 キャプションは、音声オーディオと音声が読み上げられないオーディオのテキストで、ビデオの適切な時間に画面に表示されます。 オーディオが聞こえない人に、何が起きているのかを理解することができます。

#### How to Meet - Captions (Prerecorded) (1.2.2) {#how-to-meet-captions-prerecorded}

キャプションは、次のいずれかの状態に設定できます。

* 開く： ビデオ再生時に常に表示
* クローズド：ユーザーがキャプションのオン、オフを切り替え可能

可能な場合は、クローズドキャプションを使用して、キャプションの表示、非表示をユーザーが選択できるようにしてください。

クローズドキャプションの場合、ビデオファイルと一緒に適切な形式( [SMIL](https://www.w3.org/AudioVideo/)など)で同期キャプションファイルを作成して提供する必要があります(方法の詳細はこのガイドの範囲外ですが、 [詳細情報 — キャプション（事前記録）(1.2.2)のチュートリアルへのリンクを用意しました](#more-information-captions-prerecorded)。 ビデオプレーヤーでキャプション機能を有効にして、そのビデオでキャプションが使用できることをユーザーに知らせるために、メモを提供するか、キャプション機能を有効にします。

オープンキャプションを使用する必要がある場合は、映像トラック内にテキストを埋め込みます。これをおこなうには、映像にタイトルをオーバーレイできるビデオ編集アプリケーションを使用します。

#### More Information - Captions (Prerecorded) (1.2.2) {#more-information-captions-prerecorded}

* [達成基準 1.2.2 について](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [達成基準 1.2.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audio Description or Media Alternative (Prerecorded) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 達成基準 1.2.3
* レベル A
* 音声解説または代替メディア（収録済み）：収録済みの映像コンテンツの時間依存メディアまたは音声解説の代わりとなるものが、同期されたメディアに対して提供されている。ただし、そのメディアがテキストの代替メディアであり、その旨の明確なラベルが付けられている場合を除きます。

#### Purpose - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

映像やアニメーションの情報が視覚的にのみ提供されている場合や、内容を視覚的に理解するのに十分な情報が音声で提供されていない場合は、視覚障碍のあるユーザーにアクセシビリティの問題が発生します。

#### How to Meet - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

この達成基準を満たすために採用できる方法は 2 つあり、どちらを使用してもかまいません。

1. 映像コンテンツに音声解説を追加します。これをおこなうには、次の 3 つのうちいずれかの方法を使用します。
   * 既存のボイスの休止部分で、既存の音声トラックでは提示されていないシーンの変化に関する情報を提供します。
   * 元の音声を含み、さらにシーンの変化に関する追加の音声情報も含む新しい追加のオプション音声トラックを提供します。
      * これにより、ユーザーは既存の音声トラック（**&#x200B;音声解説を含まない）と新しい音声トラック（**&#x200B;音声解説を含む）を切り替えることができます。
      * これにより、追加の説明が不要なユーザーの混乱を防ぐことができます。
   * 音声解説を拡張できるように、2 つ目のバージョンの映像コンテンツを作成します。これにより、適切な時点で音声と映像を一時的に休止して既存のボイスの合間に詳細な音声解説を提供することに関連する困難な作業を軽減できます。その結果、アクションが再開される前に、より長い音声解説を指定できます。前の例と同様に、追加の説明が不要なユーザーの混乱を防ぐために、この方法はオプションの追加音声トラックとして提供することをお勧めします。
1. 映像またはアニメーションの音声および視覚要素をテキストで適切に表現した字幕を提供します。これには、適切な場合は、発言者の指示、設定の説明、視覚的に表示されるイベントや情報、および音声式が含まれます。 長さによって、字幕は映像やアニメーションと同じページに配置するか、別のページに配置できます。後者を選んだ場合は、映像またはアニメーションのすぐ近くに字幕へのリンクを提示してください。

音声解説付きの映像の詳細な作成方法は、このガイドの範囲外です。映像および音声解説の作成には長時間を要する可能性がありますが、他のアドビ製品が役に立つ場合があります。

#### More Information - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [達成基準 1.2.3 について](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [達成基準 1.2.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### キャプション（ライブ）（1.2.4）    {#captions-live}

* 達成基準 1.2.4
* レベル AA
* キャプション（ライブ）：同期されたメディアに含まれるすべてのライブ音声コンテンツに対してキャプションが提供されている。

#### 目的 - キャプション（ライブ）（1.2.4） {#purpose-captions-live}

This success criterion is identical to [Captions (Prerecorded)](#captions-prerecorded) in that it addresses accessibility barriers experienced by people who are deaf or hearing-impaired, except that this success criterion deals with live presentations such as webcasts.

#### 達成方法 - キャプション（ライブ）（1.2.4）{#how-to-meet-captions-live}

Follow the guidance provided for [Captions (Prerecorded)](#captions-prerecorded) above. However, due to the live nature of the media, caption provision has to be created as quickly as possible and in response to what is happening. Therefore, you should consider using real time captioning or speech-to-text tools.

詳細な手順説明はこのドキュメントの範囲外ですが、次のリソースで役に立つ情報が提供されています。

* [WebAIM：Real Time Captioning](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputingプロジェクト（ワシントン大学）: 音声認識を使用してキャプションを自動的に生成できますか？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### More Information - Captions (Live) (1.2.4) {#more-information-captions-live}

* [達成基準 1.2.4 について](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [達成基準 1.2.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### オーディオの説明（事前に記録済み）(1.2.5)  {#audio-description-prerecorded}

* 達成基準 1.2.5
* レベル AA
* 音声解説（収録済み）：同期されたメディアに含まれるすべての収録済み映像コンテンツに対して音声解説が提供されている。

#### Purpose - Audio Description (Prerecorded) (1.2.5) {#purpose-audio-description-prerecorded}

This success criterion is identical to [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded), except that authors must provide a much more detailed audio description to conform to Level AA.

#### How to Meet - Audio Description (Prerecorded) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Follow the guidance provided for [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded).

#### More Information - Audio Description (Prerecorded) (1.2.5) {#more-information-audio-description-prerecorded}

* [達成基準 1.2.5 について](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [達成基準 1.2.5 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 適応可能（1.3） {#adaptable}

[ガイドライン 1.3 適応可能：情報および構造を損なうことなく、様々な方法（例えば、よりシンプルなレイアウト）で提供できるようにコンテンツを制作している。](https://www.w3.org/TR/WCAG/#adaptable)

このガイドラインは、次のようなユーザーのサポートに必要な要件に対応しています。

* は、そのコンテンツのデフォルト表示で作成者が提示した情報（複数列のレイアウトや、色や画像を多く使用するページなど）にアクセスできない場合があります。

* は、オーディオ専用、または大きなテキストや高いコントラストなどの代替の視覚表示を使用する場合があります。

### 情報および関係性（1.3.1）    {#info-and-relationships}

* 達成基準 1.3.1
* レベル A
* 情報および関係性：プレゼンテーションを通して伝えられる情報、構造および関係性を、プログラムによって特定できる、またはテキスト形式で利用できる。

#### 目的 - 情報および関係性（1.3.1） {#purpose-info-and-relationships}

障害を持つユーザーが使用する多くの支援テクノロジーは、コンテンツを効果的に表示または *理解するために構造情報に依存しています* 。 この構造情報は、ページ見出し、テーブル行、列見出し、リストタイプの形式をとることができます。 例えば、スクリーンリーダーを使用して、ページ内の見出しから見出しに移動できます。 ただし、ページコンテンツの構造が基になるHTMLではなく、視覚的なスタイルでのみ表示される場合、支援テクノロジーでは構造情報が利用できず、読みやすさが制限されます。

この成功基準は、HTMLや他のコーディング手法を使用してプログラム的に構造情報を提供し、ブラウザや支援テクノロジーがその情報にアクセスして活用できるようにするために存在します。

#### How to Meet - Info and Relationships (1.3.1) {#how-to-meet-info-and-relationships}

AEMでは、適切なHTML要素を使用して、意味的に意味のあるWebコンテンツを簡単に作成できます。 RTE（テキストコンポーネント）でページコンテンツを開き、**段落書式**&#x200B;メニュー（段落記号）を使用して、適切な構造要素（段落、見出しなど）を指定します。

必要に応じて、次の要素を使用して、Webページの構造が適切であることを確認できます。

* **見出し：** RTEのアクセシビリティ機能を有効にしている限り、AEMオファー3レベルのページ見出しが有効になっています。 これらを使用して、コンテンツのセクションおよびサブセクションを識別できます。「見出し 1」は最上位の見出し、「見出し 3」は最下位の見出しです。システム管理者の設定により、使用可能な見出しレベルを増やすこともできます。

* **リスト**: HTMLを使用して、次の3種類のリストを指定できます。
   * `<ul>` 要素は、順序なし（箇条書き）リスト&#x200B;**&#x200B;に使用します。個々のリスト項目は、`<li>` 要素を使用して識別されます。RTE では、**箇条書き**&#x200B;アイコンを使用します。
   * `<ol>` 要素は、番号付きリスト&#x200B;**&#x200B;に使用します。個々のリスト項目は、`<li>` 要素を使用して識別されます。RTE では、「**番号付きリスト**」アイコンを使用します。
   既存のコンテンツを特定のリストタイプに変更する場合は、該当するテキストをハイライト表示して、適切なリストタイプを選択します。前述した段落テキストの入力方法を示す例と同様に、適切なリスト要素が HTML に自動的に追加されます。

   全画面表示モードでは、個別の&#x200B;**箇条書きリスト**&#x200B;および&#x200B;**番号付きリスト**&#x200B;アイコンが表示されます。全画面表示モード以外の場合、1 つの&#x200B;**リスト**&#x200B;アイコンから 2 つのオプションを使用できます。

* **テーブル**: データの表は、HTMLの表要素を使用して識別する必要があります。
   * 1 つの `<table>` 要素
   * テーブルの行ごとに 1 つの `<tr>` 要素
   * 行および列の見出しごとに 1 つの `<th>` 要素
   * データセルごとに 1 つの `<td>` 要素
   さらに、アクセス可能なテーブルでは、次の要素および属性も使用します。

   * `<caption>` 要素は、テーブルの表示可能なキャプションを提供する際に使用します。キャプションは、デフォルトではテーブルの上に中央配置で表示されますが、CSS を使用して適切に配置できます。キャプションはプログラムによってテーブルに関連付けられるので、コンテンツを紹介する際に役立ちます。
   * `<summary>` 要素は、目の見えるユーザーに見えているものの概要を提示することで、視覚障碍のあるユーザーがテーブル内の情報をより簡単に理解できるように支援します。これは、複雑な、型どおりでないテーブルレイアウトが使用されている場合に特に便利です（この属性はブラウザーには表示されません。支援テクノロジーに読み上げられるだけです）。
   * `<th>` 要素の `scope` 属性は、セルが特定の行のヘッダーを表すか、特定の列のヘッダーを表すかを示すために使用します。同様の方法として、データセルが 1 つ以上のヘッダーに関連付けられている複雑なテーブルで、header 属性と id 属性を使用することがあります。
   >[!NOTE]
   >
   >デフォルトでは、これらの要素や属性を直接は使用することはできませんが、システム管理者が&#x200B;**テーブルのプロパティ**&#x200B;ダイアログボックスでこれらの値のサポートを追加することは可能です（「追加の HTML 要素および属性のサポートの追加」を参照）。

   <!-- removed link syntax for ExL - Bob Bringhurst
  >By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see Adding Support for Additional HTML Elements and Attributes /help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).
  -->

   「**テーブルのプロパティ**」タブを選択できる&#x200B;**テーブル**&#x200B;ダイアログを開くには、次のようにします。

   * 適切な&#x200B;**キャプション**&#x200B;を定義します。
   * 理想としては、「**幅**」、「**高さ**」、「**ボーダー**」、「**セル内の余白**」、「**セルの間隔**」のデフォルト値をすべて削除します。これらのプロパティはグローバルスタイルシートで設定できるからです。
   次に、**セルのプロパティ**&#x200B;を使用して、セルがデータセルかヘッダーセルかを選択できます。

* **強調**: 強調を示すには、 `<strong>` または `<em>` 要素を使用します。 段落内のテキストをハイライト表示するために見出しを使用しないでください。
   * 強調するテキストをハイライト表示します。
   * 「**B**」アイコン（`<strong>`に対応）または「**I**」アイコン（`<em>` に対応）を、**プロパティ**&#x200B;パネルでクリックします（HTML が選択されていることを確認してください）。

      >[!NOTE]
      >
      >AEM の標準的なインストールに含まれる RTE は、次のように設定されています。
      >
      >* `<b>` の代わりに `<strong>` を使用
      >* `<i>` の代わりに `<em>` を使用
      >
      >それぞれ実質的には同じですが、好ましいのは、意味的に正しい HTML である `<strong>` と `<em>` です。開発チームがプロジェクトインスタンスを作成する際に、`<strong>` と `<em>` ではなく `<b>` と `<i>` を使用するように RTE を設定できます。


* **複雑なデータテーブル**：レベルが 2 つ以上あるヘッダーを含む複雑なテーブルがある場合など、場合によっては、基本的なテーブルのプロパティでは必要な構造情報を十分に指定できないことがあります。このような複雑なテーブルでは、**header** 属性と **id** 属性を使用して、ヘッダーとその関連セルの間に直接の関係を作成する必要があります。

   >[!NOTE]
   >
   >id 属性は、標準のインストールでは使用できません。RTE で HTML ルールとシリアライザーを設定することによって有効にできます。

   例えば、以下に示すテーブルでは、支援テクノロジーユーザーのためのプログラムによる関連付けを作成するために、header と id が照合されています。

   ```xml
     <table>
       <tr>
         <th rowspan="2" id="h">Homework</th>
         <th colspan="3" id="e">Exams</th>
         <th colspan="3" id="p">Projects</th>
       </tr>
       <tr>
         <th id="e1" headers="e">1</th>
         <th id="e2" headers="e">2</th>
         <th id="ef" headers="e">Final</th>
         <th id="p1" headers="p">1</th>
         <th id="p2" headers="p">2</th>
         <th id="pf" headers="p">Final</th>
       </tr>
       <tr>
         <td headers="h">15%</td>
         <td headers="e e1">15%</td>
         <td headers="e e2">15%</td>
         <td headers="e ef">20%</td>
         <td headers="p p1">10%</td>
         <td headers="p p2">10%</td>
         <td headers="p pf">15%</td>
       </tr>
     </table>
   ```

   AEM でこれを実現するには、ソース編集モードを使用してマークアップを直接追加する必要があります。

   >[!NOTE]
   >
   >この機能は、標準インストールでは、すぐには使用できません。RTE、HTML ルールおよびシリアライザーを設定する必要があります。

#### 詳細情報 - 情報および関係性（1.3.1）{#more-information-info-and-relationships}

* [達成基準 1.3.1 について](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [達成基準 1.3.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 意味のあるシーケンス(1.3.2)  {#meaningful-sequence}

* 達成基準 1.3.2
* レベル A
* 意味のあるシーケンス： コンテンツが提示される順序がその意味に影響を与える場合、正しい読み取り順序をプログラム的に決定することができる。

#### 目的 — 意味のあるシーケンス(1.3.2) {#purpose-meaningful-sequence}

この成功条件の目的は、ユーザーエージェントが意味を理解するために必要な読み取り順序を維持しながら、コンテンツの代替表示を可能にすることです。 意味を持つコンテンツの少なくとも1つのシーケンスをプログラムで判断できることが重要です。 この成功基準を満たさないコンテンツは、支援テクノロジーがコンテンツを誤った順序で読み取った場合や、代替スタイルシートやその他の書式変更が適用された場合、ユーザーを混乱させたり、方向を狂わせたりする可能性があります。

#### ミーティング方法 — 意味のあるシーケンス(1.3.2) {#how-to-meet-meaningful-sequence}

「成功条件の [満たし方」のガイドラインに従います。 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### 詳細情報 — 意味のあるシーケンス(1.3.2) {#more-information-meaningful-sequence}

* [達成基準 1.3.2 について](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [達成基準 1.3.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感覚的な特徴（1.3.3）    {#sensory-characteristics}

* 達成基準 1.3.3
* レベル A
* 感覚的な特徴：コンテンツを理解および操作するために提供されている指示が、形状、サイズ、視覚的な場所、方向、音声など、コンポーネントの感覚的な特徴のみに依存していない。

#### 目的 - 感覚的な特徴（1.3.3） {#purpose-sensory-characteristics}

デザイナーは、情報を表示する際に、色、形状、テキストスタイル、またはコンテンツの絶対位置や相対位置など、視覚的なデザイン機能に重点を置いています。 これらは情報を伝える際に非常に強力なデザインテクニックになります（認知機能に関するニーズを持つ目の見えるユーザに対しては全体的なアクセシビリティを向上できます）が、視覚や視覚に障害を持つ人は、位置、色、形状などの属性を視覚的に識別する必要がある情報にアクセスできません。

同様に、話し手が男性か女性かなど、異なる音声を区別する必要のある情報を音声コンテンツの代替テキストに反映しないと、聴覚障碍のあるユーザーにアクセシビリティの問題が発生します。

>[!NOTE]
>
>色の代替に関連する要件について詳しくは、[色の使用](#use-of-color)を参照してください。

#### 達成方法 - 感覚的な特徴（1.3.3） {#how-to-meet-sensory-characteristics}

ページコンテンツの視覚的な特徴に依存する情報が、代替形式でも提示されていることを確認してください。

* 視覚的な位置に依存して情報を提供しないでください。例えば、追加情報にアクセスするためにページの右側にあるメニューをユーザーに示す場合は、「右側のメニュー」**&#x200B;とは言わずに、見出しを使用するなどしてメニューに名前を付けて、テキストではその名前で説明します。
* 情報を伝える唯一の方法として、テキストのスタイル設定（太字や斜体など）に依存しないでください。

>[!NOTE]
>
>視覚的でないコンテキストで意味を持つことが理解される場合は、説明的な用語を使用してかまいません。例えば、「上記」**&#x200B;や「下記」**&#x200B;という表現を使用することは、通常は許容されます。それぞれ、コンテンツの特定の項目の前後にあるコンテンツを示すからです。これは、コンテンツを声に出して読み上げる場合でも意味をなします。

#### 詳細情報 - 感覚的な特徴（1.3.3）{#more-information-sensory-characteristics}

* [達成基準 1.3.3 について](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [達成基準 1.3.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 判別可能（1.4） {#distinguishable}

[ガイドライン 1.4 判別可能：コンテンツを、利用者にとって見やすく、聞きやすいものにします。これには、前景と背景を区別することも含む。](https://www.w3.org/TR/WCAG/#distinguishable)

### 色の使用（1.4.1）    {#use-of-color}

* 達成基準 1.4.1
* レベル A
* 色の使用：色が、情報を伝達したり、アクションを示したり、応答を促したり、視覚的要素を区別したりするための唯一の視覚的方法として使用されていない。

>[!NOTE]
>
>この達成基準では、色覚を具体的に扱います。その他の知覚については、[適応可能（1.3）](#adaptable)で、色やその他の視覚的表現のコーディングを含めて説明しています。

#### 目的 - 色の使用（1.4.1） {#purpose-use-of-color}

色は、Web ページの美しさを強調するうえで間違いなく効果的な方法であり、情報を伝達するうえでも便利です。ただし、全盲から色覚異常まで、様々な視覚障碍があり、特定の色を区別できない人もいます。このため、情報を提供するうえで、色分けは信頼性の低い方法となります。

例えば、赤と緑の色覚異常のある人は、緑の影と赤の影を区別できません。両方の色が第三の色（茶色など）に見える場合があり、その場合は赤、緑、茶色を区別できません。

また、テキストのみのブラウザーやモノクロの表示デバイスを使用している場合や、ページの白黒印刷を見る場合も、色を知覚できません。

さらに考慮する必要があるのは、インターフェイス要素（タブ、トグルボタンなど）の *選択状態です* 。この状態は、色だけでなく視覚的な表示以外にも、何らかの形で伝達する必要があります。 このような要素では、特定の感覚に依存しない包括的なユーザーエクスペリエンスを作成する場合、パターン、図形、およびプログラム情報をさらに使用すると便利です。

#### How to Meet - Use of Color (1.4.1) {#how-to-meet-use-of-color}

色を使用して情報を伝達する場合は、色を見なくても情報が利用できることを確認してください。

例えば、色によって提供されている情報を、テキストでも明示的に提供します。

色を情報提供のキューとして使用する場合は、スタイル（太字、斜体など）やフォントの変更など、追加の視覚的キューを指定する必要があります。これは、視覚障碍を持つ人や色覚障碍を持つ人が情報を特定するのに役立ちます。ただし、ページをまったく見ることのできない人には役に立たないので、全面的に依存することはできません。したがって、この情報を目の見えないユーザーに伝えるには、隠しテキストを提供したり、 [Accessible Rich Internet Applications(ARIA)Suite of Web標準などのプログラム的なソリューションを使用したりすると便利です](https://www.w3.org/WAI/standards-guidelines/aria/)。

#### 詳細情報 - 色の使用（1.4.1）{#more-information-use-of-color}

* [達成基準 1.4.1 について](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [達成基準 1.4.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### オーディオコントロール(1.4.2)  {#audio-control}

* 達成基準 1.4.2
* レベル A
* オーディオコントロール： Webページ上の任意のオーディオが3秒以上自動的に再生される場合は、オーディオを一時停止または停止するメカニズムか、システム全体のボリュームレベルとは別にオーディオのボリュームを制御するメカニズムを使用できます。

#### 目的 — オーディオコントロール(1.4.2) {#purpose-audio-control}

スクリーンリーディングソフトウェアを使用している人は、同時に他のオーディオが再生されている場合、音声出力を聞き取るのが難しい場合があります。 この問題は、スクリーンリーダーの音声出力が、（現在のほとんどの場合と同様に）ソフトウェアベースで、サウンドと同じボリュームコントロールを介して制御される場合に悪化します。 また、認知障害を持つ人や神経異性の人は、音に対する感受性を持つ場合もあります。 オーディオコンテンツのボリュームレベルを変更できない場合もあります。

したがって、ユーザが背景音をオフにできることが重要です。

>[!NOTE]
>
>ボリュームの制御は、ボリュームをゼロにすることを含む。

#### 対応方法 — オーディオコントロール(1.4.2) {#how-to-meet-audio-control}

「成功条件の [満たし方」1.4.2のガイドラインに従い](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)ます。

#### 詳細情報 — オーディオコントロール(1.4.2) {#more-information-audio-control}

* [達成基準 1.4.2 について](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [達成基準 1.4.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contrast (Minimum) (1.4.3) {#contrast-minimum}

* 達成基準 1.4.3
* レベル AA
* コントラスト（最低限）：テキストおよびテキストの画像を視覚的に表現したものが、4.5:1 以上のコントラスト比を持つ。ただし、次の場合を除く。
   * 大きいテキスト：大型のテキストおよび大型のテキストの画像の最低コントラスト比は 3:1 です。
   * Incidental: Text or images of text that are part of an inactive user interface component, that are [pure decoration](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), that are not visible to anyone, or that are part of a picture that contains significant other visual content, have no contrast requirement.
   * ロゴタイプ：ロゴまたはブランド名の一部であるテキストには、最低コントラストの要件はありません。
   >[!NOTE]
   >
   >詳しくは、「テキスト以外のコントラスト [について](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html) 」を参照して、テキスト以外の要素（アイコン、インターフェイス要素など）に関する追加の要件を確実に理解してください。

#### Purpose - Contrast (Minimum) (1.4.3) {#purpose-contrast-minimum}

特定の視覚障碍のあるユーザーは、特定の低コントラストの色のペアを区別できない場合があります。次のいずれかの場合に、このようなユーザーにアクセシビリティの問題が発生することがあります。

* テキストと背景色のコントラストが不十分な場合。
* テキストの色分け（リンクテキストとリンク以外のテキストなど）が、情報を区別するうえで重要な場合。

>[!NOTE]
>
>純粋に装飾目的で使用されるテキストは、この達成基準から除外されます。

#### 達成方法 - コントラスト（最低限）（1.4.3） {#how-to-meet-contrast-minimum}

テキストと背景色のコントラストが十分であることを確認します。コントラスト比は、問題のテキストのサイズとスタイルによって異なります。

* テキストのサイズが 18 ポイント（太字の場合は 14 ポイント）未満の場合、テキストまたはテキストの画像と背景の間のコントラスト比は 4.5:1 以上である必要があります。
* テキストのサイズが 18 ポイント（太字の場合は 14 ポイント）以上の場合、コントラスト比は 3:1 である必要があります。
* 背景が模様入りの場合は、テキスト周辺の背景に陰影を付けて、4.5:1 または 3:1 の比率を維持する必要があります。

>[!NOTE]
>
>同等のPT/PX/EMサイズがフォントでレンダリングされる方法が異なる場合があることに注意してください。
>
>Webコンテンツ用の適切なフォントとサイズを選択する際は、判断力に優れ、読みやすさと操作性の面で誤りを含めることをお勧めします。

>[!NOTE]
>
>次のサイトは、他のユニットへのコンバージョンに役立ちます。
>
>* [ピクセルからEmカルキュレータ — オムニ](https://www.omnicalculator.com/conversion/px-to-em)
>* [フォントサイズの変換： pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com: PXからEMへの変換により、単純化](http://pxtoem.com)


コントラスト比を確認するには、[Paciello Group の Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) や [WebAIM の Color Contrast Checker](https://www.webaim.org/resources/contrastchecker/) などの色コントラストツールを使用してください。これらのツールを使用すると、色のペアを確認し、コントラストの問題を報告できます。

また、ページの外観の指定にそれほど関心がない場合は、背景や前面のテキストの色を指定しないことを選択できます。その場合、テキストや背景の色はユーザーのブラウザーによって決まるので、コントラストの確認は不要です。

推奨されるコントラストレベルを満たすことができない場合は、代替の、同等のページ（色のコントラストに関する問題がないページ）へのリンクを提供するか、ユーザーが自身の要件に合わせてページの配色のコントラストを調整できるようにする必要があります。

#### 詳細情報 - コントラスト（最低限）（1.4.3） {#more-information-contrast-minimum}

* [達成基準 1.4.3 について](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [達成基準 1.4.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### テキストのサイズ変更(1.4.4)  {#resize-text}

* 達成基準 1.4.4
* レベル A
* テキストのサイズ変更： テキストのキャプションと画像を除き、テキストは200%まで支援技術を必要とせず、コンテンツや機能を失うことなくサイズ変更できます。

#### 目的 — テキストのサイズ変更(1.4.4) {#purpose-resize-text}

この成功条件は、テキストベースのコントロール(ASCIIなどのデータ形式に残るテキスト文字 [と表示可能なテキスト文字])を含む視覚的にレンダリングされたテキストを、拡大鏡などの支援技術を使用せずに、正常に拡大・縮小できるようにする目的です。 Webページのすべてのコンテンツを拡大・縮小するメリットがある場合もありますが、テキストは非常に重要です。

#### 出会い方 — テキストのサイズ変更(1.4.4) {#how-to-meet-resize-text}

コンテンツ作成者は、成功条件1.4.4 [の満たし](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 方のガイドラインに従うだけでなく、ページデザインやフォントサイズ（レスポンシブWebデザインなど）で流動的で柔軟な幅と高さを使用して、読者がテキストのサイズを変更できるように促すことができます。

#### 詳細情報 — テキストのサイズ変更(1.4.4) {#more-information-resize-text}

* [達成基準 1.4.4 について](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [達成基準 1.4.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Images of Text (1.4.5) {#images-of-text}

* 達成基準 1.4.5
* レベル AA
* 文字画像：使用しているテクノロジーで視覚的表現を実現できる場合に、文字画像ではなくテキストを使用して情報を伝達している。ただし、次の場合を除く。
   * カスタマイズ可能：テキストの画像を、ユーザーの要件に合わせて視覚的にカスタマイズできる場合
   * 必須：テキストの特定の表現が、伝達する情報にとって不可欠な場合

>[!NOTE]
>
>ロゴタイプ（ロゴまたはブランド名の一部であるテキスト）は必須と見なされます。

#### 目的 - 文字画像（1.4.5） {#purpose-images-of-text}

文字画像は、多くの場合、ロゴタイプなど特定のスタイルのテキストが好まれる場合や、テキストが別のソース（紙のドキュメントのスキャンなど）から生成された場合に使用されます。ただし、HTML で表現され、CSS を使用してスタイル設定されているテキストと比較して、文字画像は柔軟性に欠けており、視覚障碍のあるユーザーや読解が困難なユーザーにとって必要となるサイズや外観の変更ができません。

#### 達成方法 - 文字画像（1.4.5） {#how-to-meet-images-of-text}

文字画像を使用する必要がある場合は、CSS を使用して、文字画像を同等の HTML テキストに置き換え、テキストをカスタマイズ可能にします。これをおこなう方法の例は、[C30：CSS を用いて、テキストを画像化された文字に置き換え、変換するユーザーインターフェイスコントロールを提供する](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30)を参照してください。

#### 詳細情報 - 文字画像（1.4.5）{#more-information-images-of-text}

* [達成基準 1.4.5 について](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [達成基準 1.4.5 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 原則 2：操作可能 {#principle-operable}

[原則 2：操作可能 - ユーザーインターフェイスコンポーネントおよびナビゲーションは操作可能でなければならない。](https://www.w3.org/TR/WCAG/#operable)

### キーボードアクセス可能(2.1) {#keyboard-accessible}

[Guideline 2.1 Keyboard Accessible: すべての機能をキーボードから使用できるようにします。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

これは、ユーザーがキーボードを使用してすべての機能にアクセスできるようにするための取り組みです。

### キーボード(2.1.1)  {#keyboard}

* 達成基準 2.1.1
* レベル A
* キーボード： コンテンツのすべての機能は、個々のキー操作に特定のタイミングを必要とせずに、キーボードインターフェイスを介して操作できます。ただし、基になる機能は、ユーザーの移動のパスに依存し、エンドポイントに依存する入力を必要とします。

#### 目的 — キーボード(2.1.1) {#purpose-keyboard}

この成功基準の目的は、可能な限り、キーボードまたはキーボードインターフェイスを使用してコンテンツを確実に操作できるようにすることです（代替キーボードを使用できるようにします）。 コンテンツをキーボードや代替キーボードで操作できる場合は、視覚を持たない人（目の調整を必要とするマウスなどのデバイスを使用できない人）や、代替キーボードやキーボードエミュレーターの役割を持つ入力デバイスを使用できます。 キーボードエミュレータには、音声入力ソフトウェア、SIP/PUFソフトウェア、画面キーボード、スキャンソフトウェア、および様々な支援技術や代替キーボードが含まれます。 視覚の低い人は、ポインタの追跡に苦労し、キーボードから制御できれば、ソフトウェアの使い方がずっと簡単になる（あるいは可能な限り）かもしれません。

#### 会う方法 — キーボード(2.1.1) {#how-to-meet-keyboard}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)。

#### 詳細情報 — キーボード(2.1.1) {#more-information-keyboard}

* [達成基準 2.1.1 について](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [達成基準 2.1.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### キーボードトラップなし(2.1.2)  {#no-keyboard-trap}

* 達成基準 2.1.2
* レベル A
* No Keyboard Trap: キーボードインターフェイスを使用してキーボードフォーカスをページのコンポーネントに移動できる場合は、キーボードインターフェイスのみを使用してフォーカスをそのコンポーネントから移動でき、変更されていない矢印キーやTabキーなどの標準的な出口方法が必要な場合は、移動方法を通知します。

#### 目的 — キーボードトラップなし(2.1.2) {#purpose-no-keyboard-trap}

この成功条件の目的は、コンテンツがWebページ上のコンテンツのサブセクション内に ** キーボードフォーカスをトラップしないようにすることです。 これは、複数の形式がページ内で組み合わされ、プラグインや埋め込みアプリケーションを使用してレンダリングされる場合に発生する一般的な問題です。

Webページの機能によって、コンテンツのサブセクション（モーダルダイアログなど）にフォーカスが制限される場合があります。 そのような場合は、ユーザーがコンテンツのサブセクションを終了できる方法を提供する必要があります（例えば、ESCキーでモーダルダイアログを閉じるか、閉じるボタンでモーダルダイアログを閉じます）。

#### 会う方法 — キーボードトラップなし(2.1.2) {#how-to-meet-no-keyboard-trap}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)。

#### 詳細情報 — キーボードトラップなし(2.1.2) {#more-information-no-keyboard-trap}

* [達成基準 2.1.2 について](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [達成基準 2.1.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 十分な時間(2.2) {#enough-time}

[ガイドライン2.2十分な時間： ユーザーがコンテンツを読み、使用するのに十分な時間を提供します。](https://www.w3.org/TR/WCAG/#enough-time)

これは、ユーザーが読んで行動を起こすのに十分な時間を確保することを目的としています。

### 調整可能なタイミング(2.2.1)  {#timing-adjustable}

* 達成基準 2.2.1
* レベル A
* キーボード： ユーザーがコンテンツを読み、使用するのに十分な時間を提供します。

#### 目的 — 調整可能なタイミング(2.2.1) {#purpose-timing-adjustable}

この成功基準の目的は、障害を持つユーザーに、可能な限りWebコンテンツを利用する適切な時間を与えることです。 視覚障害、低視覚障害、手指障害、認知機能の制限など障害を持つユーザーは、コンテンツを読むのに時間がかかる場合や、オンラインフォームの入力などの機能を実行するのに時間がかかる場合があります。 Web関数が時間に依存する場合は、時間制限が発生する前に必要な操作を行うのが難しい場合があります。 これにより、サービスにアクセスできなくなる場合があります。 時間に依存しない機能をデザインすると、障害を持つ人がこれらの機能を完了するのに役立ちます。 時間制限の無効化、時間制限のカスタマイズ、時間制限の発生前のリクエストを行うオプションを提供すると、タスクの完了に予想以上の時間を要するユーザーに役立ちます。 これらのオプションは、ユーザーにとって最も役に立つ順に表示されます。 時間制限を無効にする方が、時間制限の長さをカスタマイズするよりも効果的です。時間制限が発生するまでに、より多くの時間を要求する方が効果的です。

#### 対応方法 — タイミング調整可能(2.2.1) {#how-to-meet-timing-adjustable}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)。

#### 詳細情報 — 調整可能なタイミング(2.2.1) {#more-information-timing-adjustable}

* [達成基準 2.2.1 について](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [達成基準 2.2.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 一時停止、停止、非表示（2.2.2）    {#pause-stop-hide}

* 達成基準 2.2.2
* レベル A
* 一時停止、停止、非表示：情報の移動、点滅、スクロールまたは自動更新について、以下が該当する。
   * 移動、点滅、スクロール：情報の移動、点滅またはスクロールのうち、（a）自動的に開始し、（b）5 秒を超えて継続し、（c）他のコンテンツと並列で提示されるものに関しては、移動、点滅またはスクロールが必須のアクティビティの一部である場合を除き、ユーザーが情報を一時停止、停止または非表示にするメカニズムがある。
   * 自動更新：情報の自動更新のうち、（a）自動的に開始し、（b）他のコンテンツと並列で提示されるものに関しては、自動更新が必須のアクティビティの一部である場合を除き、ユーザーが情報を一時停止、停止または非表示にするか、更新の頻度を制御するメカニズムがある。

注意点は次のとおりです。

1. コンテンツの明滅や閃光に関連する要件については、発作の防止：発作を引き起こすようなコンテンツを設計しないこと（2.3）を参照してください。
1. この達成基準を満たさないコンテンツがある場合は、ユーザーがページ全体を使用できない場合があるので、Web ページ上のすべてのコンテンツ（他の達成基準を満たすために使用されているかどうかにかかわらず）が、この達成基準を満たす必要があります。[「Conformance Requirements」の「5. Non-Interference」](https://www.w3.org/TR/WCAG20/#cc5)を参照してください。
1. ソフトウェアによって定期的に更新されるコンテンツや、ユーザーエージェントにストリーミングされるコンテンツでは、一時停止してから再開されるまでの間に生成または受信された情報を保持したり停止したりする必要はありません。これは技術的に不可能な場合があり、多くの場合に誤解を招く可能性があるからです。
1. プリロード段階または同様の状況の一環として発生するアニメーションがある場合に、すべてのユーザーに対してその段階中はインタラクションが発生できず、進捗を示さないことによってユーザーが混乱したり、コンテンツがフリーズまたは破損していると考える可能性がある場合は、そのアニメーションを必須と見なすことができます。

#### 目的 - 一時停止、停止、非表示（2.2.2） {#purpose-pause-stop-hide}

移動するコンテンツが気をそらすか、物理的に負担が大きくなる場合があり、ページの他の部分に集中するのが困難な場合があります。 また、テキストの移動に遅れを取らないユーザーには、このようなコンテンツが読みにくくなる場合があります。

#### How to Meet - Pause, Stop, Hide (2.2.2) {#how-to-meet-pause-stop-hide}

移動、閃光、点滅の性質を持つコンテンツを含む Web ページを作成する際には、コンテンツの性質に応じて、次のうち 1 つ以上の提案事項を適用できます。

* ユーザーの読む時間を十分にするために、コンテンツのスクロールを一時停止する方法を提供します。例えば、ニュースティッカー、自動更新されたテキスト、自動進行する画像カルーセルなどです。
* 点滅するコンテンツが、5 秒後に点滅を停止するようにします。
* ブラウザーで無効にできるコンテンツの移動や点滅を表示するには、適切なテクノロジーを使用します。 例えば、Graphics Interchange Format(GIF)やAnimated Portable Network Graphics(APNG)ファイルなどです。
* Webページ上のフォームコントロールを提供して、ページ上で移動するコンテンツや明滅するコンテンツをすべて無効にすることができます。
* 上記のいずれかが不可能な場合は、すべてのコンテンツを含むページへのリンクを提供します。ただし、移動したり点滅したりすることはありません。

#### More information - Pause, Stop, Hide (2.2.2) {#more-information-pause-stop-hide}

* [達成基準 2.2.2 について](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [達成基準 2.2.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 発作と物理的反応(2.3) {#seizures-and-physcial-reactions}

[ガイドライン2.3発作： 発作や肉体的反応を引き起こすことがわかっているコンテンツをデザインしないでください。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Three Flashes or Below Threshold (2.3.1) {#three-flashes-or-below-threshold}

* 達成基準 2.3.1
* レベル A
* 3 回の閃光、またはしきい値以下：1 秒間の閃光回数が 3 回を超えるものが Web ページに含まれていない。または、閃光が一般閃光しきい値および赤色閃光しきい値を下回っている。

>[!NOTE]
>
>この達成基準を満たさないコンテンツがある場合は、ユーザーがページ全体を使用できない場合があるので、Web ページ上のすべてのコンテンツ（他の達成基準を満たすために使用されているかどうかにかかわらず）が、この達成基準を満たす必要があります。[「Conformance Requirements」の「5. Non-Interference」](https://www.w3.org/TR/WCAG/#cc5)を参照してください。

#### 目的 - 3 回の閃光、またはしきい値以下（2.3.1）{#purpose-three-flashes-or-below-threshold}

場合によっては、コンテンツが放つ閃光によって光過敏性発作が発生する可能性があります。この達成基準を満たすと、そのようなユーザーが閃光を放つコンテンツの心配をせずにすべてのコンテンツにアクセスし、体験できます。

#### 達成方法 - 3 回の閃光、またはしきい値以下（2.3.1） {#how-to-meet-three-flashes-or-below-threshold}

次の技法が適用されていることを確認する必要があります。

* コンポーネントの 1 秒間の閃光回数が 3 回以下であることを確認します。
* 上記の条件を満たすことができない場合は、画面上のピクセル単位の小さい安全な領域&#x200B;**&#x200B;内に、閃光コンテンツを表示します。この領域は、「[G176: Keeping the flashing area small enough](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)」で説明している複雑な数式を使用して計算されるので、この技法を使用するのは、閃光コンテンツが絶対に&#x200B;**&#x200B;必要な場合のみにする必要があります。

#### 詳細情報 - 3 回の閃光、またはしきい値以下（2.3.1）{#more-information-three-flashes-or-below-threshold}

* [達成基準 2.3.1 について](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [達成基準 2.3.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### ナビゲーション可能(2.4) {#navigable}

[Guideline 2.4 Navigable: ユーザーのナビゲーション、コンテンツの検索、位置の特定に役立つ方法を提供します。](https://www.w3.org/TR/WCAG/#navigable)

これは、ユーザーがコンテンツを簡単にナビゲートできるようにするための取り組みです。

### ブロックをバイパス(2.4.1)  {#bypass-blocks}

* 達成基準 2.4.1
* レベル A
* ブロックをバイパス： メカニズムは、複数のウェブページで繰り返されるコンテンツのブロックを回避するために使用できます。

#### 目的 — バイパスブロック(2.4.1) {#purpose-bypass-blocks}

この成功条件の目的は、コンテンツ間を順番に移動する訪問者が、Webページのプライマリコンテンツにより直接アクセスできるようにすることです。 Webページやアプリには、他のページや画面に表示されるコンテンツが含まれる場合が多くあります。 コンテンツの繰り返しブロックの例としては、ナビゲーションリンク、ヘッダーグラフィック、メニュー、広告フレームなどがありますが、これらに限定されません。 個々の単語、フレーズ、単一のリンクなどの小さな繰り返しセクションは、この規定の目的ではブロックとは見なされません。

#### 満たす方法 — ブロックをバイパス(2.4.1) {#how-to-meet-bypass-blocks}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)。

#### 詳細情報 — ブロックのバイパス(2.4.1) {#more-information-bypass-blocks}

* [達成基準 2.4.1 について](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [達成基準 2.4.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### ページタイトル（2.4.2）    {#page-titled}

* 達成基準 2.4.2
* レベル A
* ページタイトル： Web ページが、トピックまたは目的を説明するタイトルを持つ。

#### 目的 - ページタイトル（2.4.2） {#purpose-page-titled}

この達成基準を満たすと、特定の障碍があるかどうかにかかわらず誰でも、ページ全体を読まずに Web ページの内容を短時間で識別できます。これは、ブラウザーのタブで複数の Web ページを開いている場合に特に便利です。ページタイトルがタブに表示されるので、簡単に見つけることができるからです。

#### 達成方法 - ページタイトル（2.4.2） {#how-to-meet-page-titled}

AEMで新しいHTMLページを作成する場合、ページタイトルを指定できます。 ページのコンテンツと目的、特に一意の要素をタイトルに適切に記述し、訪問者がそのコンテンツが実際にニーズに関連しているかどうかをすばやく特定できるようにします。

ページを編集する際に、ページタイトルを編集することもできます（**ページ情報**／**プロパティ**&#x200B;からアクセス可能）。

#### 詳細情報 - ページタイトル（2.4.2）{#more-information-page-titled}

* [達成基準 2.4.2 について](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [達成基準 2.4.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### フォーカス順序(2.4.3)  {#focus-order}

* 達成基準 2.4.3
* レベル A
* フォーカスの順序： Webページを順次ナビゲーションでき、ナビゲーションシーケンスが意味や操作に影響を与える場合、フォーカス可能なコンポーネントは、意味や操作性を保持する順序でフォーカスを受け取ります。

#### 目的 — フォーカス順序(2.4.3) {#purpose-focus-order}

この成功条件の目的は、ユーザーがコンテンツを順番に移動する際に、コンテンツの意味に合った順序で情報が表示され、キーボードから操作できるようにすることです。 これにより、ユーザーがコンテンツの一貫した精神モデルを作成できるので、混乱が軽減されます。 コンテンツ内の論理的な関係を反映した異なる順序が存在する場合があります。 例えば、複数のフィールドやステップで構成されるオンラインフォームのコンポーネント間を移動すると、コンテンツ内の論理的な関係が反映されます。

#### 達成方法 — フォーカス順序(2.4.3) {#how-to-meet-focus-order}

「成功基準の [満たし方」のガイドラインに従い](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)ます。

#### 詳細情報 — フォーカス順序(2.4.3) {#more-information-focus-order}

* [達成基準 2.4.3 について](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [達成基準 2.4.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### リンクの目的（コンテキスト内）（2.4.4）    {#link-purpose-in-context}

* 達成基準 2.4.4
* レベル A
* リンクの目的（コンテキスト内）：各リンクの目的が、リンクテキストのみから、またはリンクテキストとプログラムで特定したリンクコンテキストから特定できる。ただし、リンクの目的が一般的にユーザーにとってあいまいな場合を除く。

#### 目的 - リンクの目的（コンテキスト内）（2.4.4） {#purpose-link-purpose-in-context}

障害に関係なく、適切なリンクテキストを介したリンクの向きを明確に示すことが、すべてのユーザーにとって重要です。 これは、ユーザーが実際にリンクをたどるかどうかを判断するのに役立ちます。 目が見えるユーザにとって、意味のあるリンクテキストはページ上に複数のリンクがある場合（特にページがテキスト中心の場合）に非常に役立ちます。意味のあるリンクテキストは、ターゲットページの機能を明確に示します。 単一のページですべてのリンクのリストを生成できる支援技術を使用するユーザーは、リンクのテキストが一意で情報のある場合に、リンクのテキストをコンテキスト外でより簡単に理解できます。 ただし、認識機能に障害を持つ視覚障害を持つ人は、リンクがリンクがどこに移動するのかを正確に説明するのに十分な情報を提供しないと、混乱する場合があります。

#### How to Meet - Link Purpose (In Context) (2.4.4) {#how-to-meet-link-purpose-in-context}

何よりも、リンクの目的がリンクのテキスト内で明確に説明されていることを確認してください。

* 悪い例：
   * テキスト：2010 年秋の夜間クラスについて詳しくは、ここをクリックしてください。
   * 理由：リンク先が不明瞭で、あいまいに示されています。
* 良い例：
   * テキスト：2010 年秋の夜間クラス - 詳細。
   * 理由：テキストとリンク要素の位置をわずかに調整することにより、リンクテキストを改善できます。

リンクは複数ページにわたって一貫した表現にする必要があります。ナビゲーションバーの場合は特にそうです。例えば、特定のページへのリンクの名前を、あるページで「**パブリケーション**」とする場合は、一貫性を保つために、他のページでもそのテキストを使用します。

記述時点では、ページに表示される類似のリンクが宛先に関する一意の情報を提供するように、タイトル属性の使用に関する問題がいくつかあります（例えば、「詳細を表示」は様々な宛先を指す場合が多い）。

* title属性に含まれるテキストは、通常、マウスユーザーのツールチップポップアップとしてのみ使用でき、キーボードやモバイルユーザーは常にアクセスできません。
* スクリーンリーダーでタイトル属性を読み上げることができますが、この機能はデフォルトでは有効になっていない場合があり、タイトル属性が存在することにユーザーが気づかない可能性があります。
* タイトルテキストの外観の変更が難しいので、ユーザーによっては読むことが困難または不可能な場合があります。

タイトル属性を使用してリンクにコンテキストを追加することはできますが、制限事項に注意し、また、適切なリンクテキストの代替としては使用しないでください。

リンクが画像で構成されている場合は、画像の代替テキストでリンク先を説明してください。例えば、本棚の画像をある人物のパブリケーションへのリンクとして設定している場合は、代替テキストを「**John Smith のパブリケーション**」のようにします。「**本棚**」とはしないでください。

また、画像要素に加えて、リンクの目的を説明するテキストがリンクアンカーに含まれている（画像と並んでテキストが表示されている）場合は、空の alt 属性を使用して画像を表します。

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>上記のスニペットは図です。**画像**&#x200B;コンポーネントを使用することをお勧めします。

追加のコンテキストを必要とせずに、リンクの目的を識別するリンクテキストを提供することをお勧めしますが、これは常に可能とは限りません。 コンテキストのないリンクは、次の場合に使用できます。HTML の例は、[達成基準 2.4.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)を参照してください。

* リンクテキストが、密接に関連するリンクのリストの一部であり、リンクを含むリスト項目で十分なコンテンツが提供されている場合。
* リンクの目的が、前の&#x200B;**（後ろではない）段落テキストから明確に識別できる場合。
* リンクがデータテーブル内に含まれているので、関連する見出しから目的を明確に識別できる場合。
* リンクのリストが一連の見出し内に含まれており、見出し自体で適切なコンテキストが提供される場合。
* リンクのリストがネストされたリンク内に含まれており、ネストされたリンクの上の親リスト項目で適切なコンテキストが提供される場合。

1 つのページ上に複数のリンクがある場合（各リンクで提供される指示が複雑だが必要な詳細である場合）は、代替バージョンの Web ページを提供することが妥当と言えます。代替バージョンは、まったく同じコンテンツを表示する一方で、リンクテキストはそれほど詳細ではないものを用意します。

また、スクリプトを使用して、リンク自体では最低限のテキストを使用し、ページの上部に向かって配置されている適切なコントロールをアクティベートするとリンクテキストが展開&#x200B;**&#x200B;され、詳細が表示されるように指定することもできます。同様に、CSS を使用して、目の見えるユーザーに対しては完全なリンクを非表示&#x200B;**&#x200B;にし、スクリーンリーダーユーザーに対しては引き続き完全に画面に出力する方法があります。これはこのドキュメントの範囲外ですが、これをおこなう方法について詳しくは、[詳細情報 - リンクの目的（コンテキスト内）（2.4.4）](#more-information-link-purpose-in-context)を参照してください。

#### 詳細情報 - リンクの目的（コンテキスト内）（2.4.4）{#more-information-link-purpose-in-context}

* [達成基準 2.4.4 について](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [達成基準 2.4.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 複数の方法(2.4.5)  {#multiple-ways}

* 達成基準 2.4.5
* レベル AA
* 複数の方法： 一連のウェブページ内でウェブページを見つける方法は複数あります。ただし、プロセスの結果がウェブページである場合やステップインの場合を除きます。

#### 目的 — 複数の方法(2.4.5) {#purpose-multiple-ways}

この成功基準の目的は、ユーザーがニーズに最も合った方法でコンテンツを見つけられるようにすることです。 ユーザは、使い方が簡単か、分かりやすい方法を見つけることができます。

小さなサイトでも、ユーザーは方向付けの手段を何らかの形で提供する必要があります。 3 ～ 4ページのページサイトで、すべてのページがホームページからリンクされている場合、ホームページ上のリンクがサイトマップとしても機能するホームページとの間にリンクを提供するだけで十分です。

#### 対応方法 — 複数の方法(2.4.5) {#how-to-meet-multiple-ways}

「成功条件の [満たし方」のガイドラインに従ってください(2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways))。

#### 詳細情報 — 複数の方法(2.4.5) {#more-information-multiple-ways}

* [達成基準 2.4.5 について](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [達成基準 2.4.5 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 見出しとラベル(2.4.6)  {#headings-and-labels}

* 達成基準 2.4.6
* レベル AA
* 見出しとラベル： 見出しとラベルは、トピックや目的を表します。

#### 目的 — 見出しとラベル(2.4.6) {#purpose-headings-and-labels}

この成功基準の目的は、ユーザがWebページに含まれる情報とその情報の編成方法を理解できるようにすることです。 見出しが明確で説明的な場合、ユーザーは検索しやすい情報を見つけ、コンテンツの異なる部分の関係をより簡単に理解できます。 説明的なラベルは、ユーザーがコンテンツ内の特定のコンポーネントを識別するのに役立ちます。

#### 会合方法 — 見出しとラベル(2.4.6) {#how-to-meet-headings-and-labels}

「成功基準の [満たし方」のガイドラインに従ってください](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)。

#### 詳細 — 見出しとラベル(2.4.6) {#more-information-headings-and-labels}

* [達成基準 2.4.6 について](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [達成基準 2.4.6 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### フォーカスを表示(2.4.7)  {#focus-visible}

* 達成基準 2.4.7
* レベル AA
* 表示フォーカス： キーボード操作可能なユーザインターフェイスは、キーボードフォーカスインジケータが表示される動作モードを有する。

#### 目的 — フォーカスを表示(2.4.7) {#purpose-focus-visible}

この成功基準の目的は、キーボードのフォーカスがある要素を人が知るのに役立ちます。

複数の要素の中で、キーボードフォーカスがある要素を知ることは可能である必要があります。 画面に操作可能なキーボードコントロールが1つしかない場合、ビジュアルデザインには、操作可能なキーボードアイテムが1つだけ表示されるので、成功基準が満たされます。

成功基準に「操作のモード」と表示される場合、これはフォーカスインジケーターが常に表示されるとは限らないプラットフォームを考慮するためです。 ほとんどの場合、操作のモードが1つだけなので、この成功条件が適用されます。

#### 会う方法 — フォーカス表示(2.4.7) {#how-to-meet-focus-visible}

「成功基準の [満たし方」のガイドラインに従ってください](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)。

#### 詳細情報 — フォーカス表示(2.4.7) {#more-information-focus-visible}

* [達成基準 2.4.7 について](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [達成基準 2.4.7 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 原則 3：理解可能 {#principle-understandable}

[原則 3：理解可能 - 情報およびユーザーインターフェイスの操作は理解可能でなければならない。](https://www.w3.org/TR/WCAG/#understandable)

### テキストのコンテンツを読みやすく理解可能にする（3.1） {#make-text-content-readable-and-understandable}

[ガイドライン 3.1 読みやすさ：テキストのコンテンツを読みやすく理解可能にすること。](https://www.w3.org/TR/WCAG/#readable)

### ページの言語（3.1.1） {#language-of-page}

* 達成基準 3.1.1
* レベル A
* ページの言語：各 Web ページのデフォルトの自然言語がどの言語であるか、プログラムによる特定ができる。

#### 目的 - ページの言語（3.1.1） {#purpose-language-of-page}

この達成基準の目的は、テキストおよびその他の言語コンテンツが正確にレンダリングされることを確認することです。スクリーンリーダーユーザーにとっては、これによってコンテンツが正しく発音され、一方で視覚的なブラウザーでは特定の言語セットが正確に表示されます。

#### 達成方法 - ページの言語（3.1.1） {#how-to-meet-language-of-page}

この達成基準を満たすために、ページ上部の `lang` 要素内で `<html>` 属性を使用して、Web ページのデフォルト言語を識別できます。次に例を示します。

* If a page is written in English, the `<html>` element should read:
   `<html lang = “en”>`

* 一方、スペイン語でレンダリングされるページは、次の標準を採用する必要があります。
   `<html lang = “es”>`

In AEM, the default language of your page is set when creating the page, but may also be changed when editing [Page Properties](/help/sites-cloud/authoring/fundamentals/page-properties.md).

>[!NOTE]
>
>AEMは、ルート言語のバリエーションに対してさらに微調整を行います。 例えば、アメリカン英語 — en-us、英語 — en-gb、カナダ英語 — en-caのように入力します。 この詳細レベルは支援テクノロジーにとって不必要なことが多くありますが、ページコンテンツの地域的なバリエーションに使用することもできます。

#### 詳細情報 - ページの言語（3.1.1）{#more-information-language-of-page}

* [達成基準 3.1.1 について](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [達成基準 3.1.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* コードは ISO 639-1 に基づいています。各言語の詳細なコードリストについては、[W3 Schools サイト](https://www.w3schools.com/tags/ref_language_codes.asp)を参照してください。

### 一部分の言語（3.1.2）    {#language-of-parts}

* 達成基準 3.1.2
* レベル AA
* 一部分の言語：コンテンツの一節ごと、フレーズごとの人間言語はプログラムによって決定できます。ただし、固有名詞、技術用語、不明な言語の単語、周囲のテキストに特有の表現の一部となっている単語やフレーズなどを除きます。

#### 目的 - 一部分の言語（3.1.2） {#purpose-language-of-parts}

この達成基準の目的は、[ページの言語](#language-of-page)の達成基準と類似していますが、単一のページに複数言語のコンテンツ（引用や一般的でない外来語）が含まれる Web ページに適用される点が異なります。

この達成基準を適用するページでは、以下のことが可能です。

* 点字切り替えソフトウェアで、アクセント記号付きの文字を挿入。
* スクリーンリーダーは、特殊文字を含む単語や、ページレベルで識別されたデフォルト言語ではない単語を発音します。
* Google 翻訳などの翻訳ツールを使用して、コンテンツを別の言語に翻訳。

#### 達成方法 - 一部分の言語（3.1.2） {#how-to-meet-language-of-parts}

`lang` 属性を使用して、コンテンツの言語の変更を識別できます。例えば、ドイツ語（ISO 639-1 コード “de”）の引用は、次のように表示できます。

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>blockquote は、標準のインスタンスではサポートされていません。この機能をサポートするためのカスタムコンポーネントを開発できます。

同様に、`span` 要素を次のように使用した場合は、一般的でない外来語やフレーズをブラウザーで正しくレンダリングできます。

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>様々な言語の名前や都市名を含める場合や、デフォルトの言語で一般的になった外来語やフレーズ（英語の *schadenfreude* など）を使用する場合は、この達成基準に従う必要はありません。

span 要素を適切な言語で追加するには、RTE のソース編集モードで、上記の内容になるように HTML マークアップを手動で編集します。または、システム管理者が `lang` 属性を RTE に含めることもできます（「追加の HTML 要素および属性のサポートの追加」を参照）。
<!--
To add the span element, with an appropriate language, you can manually edit your HTML markup in the source edit mode of the RTE so that it reads as above. Alternatively the `lang` attribute can be included in the RTE by a system administrator (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

#### 詳細情報 - 一部分の言語（3.1.2）{#more-information-language-of-parts}

* [達成基準 3.1.2 について](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [達成基準 3.1.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 予測可能(3.2) {#predictable}

[ガイドライン3.2予測可能： Webページを予測可能な方法で表示および操作できるようにします。](https://www.w3.org/TR/WCAG/#predictable)

これは、Webページの外観と動作に一貫性を持たせることに関するものです。

### フォーカス(3.2.1)  {#on-focus}

* 達成基準 3.2.1
* レベル A
* フォーカス時： ユーザインターフェイスコンポーネントがフォーカスを受け取った場合、コンテキストの変更は開始されません。

#### 目的 — フォーカス時(3.2.1) {#purpose-on-focus}

この成功基準の目的は、訪問者がドキュメント内を移動する際に、機能が予測可能であることを保証することです。 フォーカスを受け取ったときにイベントをトリガーできるコンポーネントは、コンテキストを変更してはなりません。 コンポーネントがフォーカスを受け取った場合のコンテキストの変更例を次に示します。

* コンポーネントがフォーカスを受けると自動的に送信されるフォーム；
* コンポーネントがフォーカスを受けると起動する新しいウィンドウ。
* フォーカスが他のコンポーネントに変更された場合、そのコンポーネントはフォーカスを受け取ります。

キーボード（タブキーからコントロールに移動）またはマウス（テキストフィールドのクリックなど）を介して、フォーカスをコントロールに移動できます。 コントロールの上にマウスを移動しても、スクリプティングによってこの動作が実装されていない限り、フォーカスは移動しません。 一部の種類のコントロールでは、コントロールをクリックすると、そのコントロール（ボタンなど）もアクティブになり、コンテキストの変更が開始される場合があります。

#### 会う方法 — 焦点を合わせる(3.2.1) {#how-to-meet-on-focus}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)。

#### 詳細情報 — フォーカス時(3.2.1) {#more-information-on-focus}

* [達成基準 3.2.1 について](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [達成基準 3.2.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 入力時(3.2.2)  {#on-input}

* 達成基準 3.2.2
* レベル A
* 入力時： ユーザインターフェイスコンポーネントの設定を変更しても、コンポーネントを使用する前にユーザに動作について通知されていない限り、コンテキストは自動的に変更されません。

#### 目的 — 入力時(3.2.2) {#purpose-on-input}

この成功基準の目的は、データの入力やフォームコントロールの選択を確実に予測可能な結果にすることです。 ユーザインターフェイスコンポーネントの設定を変更すると、ユーザが操作しなくなったときにコントロールの一部の側面が変更されます。 したがって、チェックボックスをオンにしたり、テキストフィールドにテキストを入力したり、リストコントロールで選択したオプションを変更したりすると、設定は変わりますが、リンクやボタンはアクティブになりません。 コンテキストの変更は、変更を容易に認識できないユーザや、変更によって容易に気を散らすユーザを混乱させる可能性があります。 コンテキストの変更は、ユーザーのアクションに応じてそのような変更が行われることが明らかな場合にのみ適切です。

#### 会う方法 — 入力時(3.2.2) {#how-to-meet-on-input}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#on-input)。

#### 詳細情報 — 入力時(3.2.2) {#more-information-on-input}

* [達成基準 3.2.2 について](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [達成基準 3.2.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一貫したナビゲーション(3.2.3)  {#consistent-navigation}

* 達成基準 3.2.3
* レベル AA
* 一貫したナビゲーション： 一連のウェブページ内の複数のウェブページで繰り返されるナビゲーションメカニズムは、ユーザが変更を開始しない限り、繰り返されるたびに同じ相対順で発生します。

#### 目的 — 一貫したナビゲーション(3.2.3) {#purpose-consistent-navigation}

この成功基準の目的は、一連のWebページ内で繰り返しコンテンツを操作し、特定の情報や機能を複数回見つける必要があるユーザーに対して、一貫した表示とレイアウトの使用を促すことです。 視覚が低く、画面の表示比率を使用して画面の一部を一度に表示する場合は、視覚的なキューやページの境界を使用して繰り返しコンテンツをすばやく見つけます。 繰り返しコンテンツを同じ順序で表示することは、デザイン内の空間メモリや視覚的キューを使用して繰り返しコンテンツを見つける視覚的ユーザにとっても重要です。

この節で「同じ順序」というフレーズを使用することで、サブナビゲーションメニューを使用できないこと、またはセカンダリナビゲーションやページ構造のブロックを使用できないことを意味するわけではありません。 代わりに、この成功基準は、Webページ上で繰り返し使用されるコンテンツを操作するユーザーの支援として、探しているコンテンツの場所を予測し、再度目に触れたときにその場所をより迅速に見つけることを目的としています。

ユーザは、アダプティブユーザエージェントを使用するか、環境設定を設定して、ユーザにとって最も役立つ方法で情報が表示されるようにすることで、順序の変更を開始できます。

#### 達成方法 — 一貫したナビゲーション(3.2.3) {#how-to-meet-consistent-navigation}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)。

#### 詳細情報 — 一貫したナビゲーション(3.2.3) {#more-information-consistent-navigation}

* [達成基準 3.2.3 について](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [達成基準 3.2.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一貫性のある識別(3.2.4)  {#consistent-identification}

* 達成基準 3.2.4
* レベル A
* Consistent Identification: 一連のWebページ内で同じ機能を持つコンポーネントは、一貫して識別されます。

#### 目的 — 一貫した識別(3.2.4) {#purpose-consistent-identification}

この成功条件の目的は、一連のWebページ内で繰り返し表示される機能コンポーネントを一貫して識別することです。 ウェブサイトの操作時にスクリーンリーダーを使用するユーザが使用する戦略は、ウェブページごとに表示される機能に対する知識を大きく活用することです。 同一の関数が異なるウェブページ上に異なるラベル（あるいは、一般的にはアクセス可能な名前が異なる）を持つ場合、そのサイトは非常に使いにくくなります。 また、認識機能の制限を持つ人に対しては、混乱を招き、認識機能の負荷が高まる可能性があります。 したがって、一貫したラベル付けが役立ちます。

この一貫性は、テキストの代替オプションにも及びます。 アイコンやその他のテキスト以外の項目が同じ機能を持つ場合は、代替テキストも一貫性を持つ必要があります。

Webページ上に2つのコンポーネントがあり、両方のコンポーネントがWebページのセット内の別のページ上のコンポーネントと同じ機能を持つ場合は、3つすべてのコンポーネントの一貫性が維持される必要があります。 したがって、同じページ上の2つは一貫性を持ちます。

1つのWebページ内で一貫性を保つことが望ましく、ベストプラクティスですが、3.2.4は、セット内の複数のページで何かが繰り返されるWebページのセット内の一貫性のみに対応します。

#### 会議の方法 — 一貫した識別(3.2.4) {#how-to-meet-consistent-identification}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)。

#### 詳細情報 — 一貫性のある識別(3.2.4) {#more-information-consistent-identification}

* [達成基準 3.2.4 について](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [達成基準 3.2.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 入力支援(3.3) {#input-assistance}

[ガイドライン 3.3 入力支援：利用者の間違いを防ぎ、修正を支援すること。](https://www.w3.org/TR/WCAG/#input-assistance)

### エラー識別(3.3.1)  {#error-identification}

* 達成基準 3.3.1
* レベル A
* エラーID: 入力エラーが自動的に検出されると、エラーのある項目が識別され、そのエラーがユーザーにテキストで説明されます。

#### 目的 — エラー識別(3.3.1) {#purpose-error-identification}

この成功基準の目的は、エラーが発生したことをユーザーが確実に認識し、何が悪いかを判断できるようにすることです。 エラーメッセージは、できる限り具体的に記述する必要があります。 フォームの送信に失敗した場合は、フォームを再表示し、エラーのあるフィールドを示すのは、エラーの発生を認識するのに十分ではありません。 例えば、スクリーンリーダーを使用するユーザーは、いずれかのインジケーターが表示されるまでエラーがあったことを知りません。 エラーインジケーターを検出する前に、ページが単に機能していないと考えて、フォームを完全に破棄する可能性があります。 WCAG 2.0の定義によると、「入力エラー」は受け入れられないユーザーから提供される情報です。 これには以下が含まれます。

webページで必要とされるがユーザーによって省略された情報、またはユーザーが提供するが、必要なデータ形式または許可されている値に該当しない情報。
次に例を示します。

* 州、都道府県、地域などに適切な省略形を入力できない。 field;
* ユーザーが、有効な状態ではない状態の省略形を入力した。
* ユーザーが存在しない郵便番号を入力した。
* ユーザーが2年後に生年月日を入力した場合
* ユーザーは、数字しか受け入れない電話番号フィールドに英字や丸括弧を入力する。
* ユーザーが前回の入札または最小入札増分を下回る入札を入力した。

#### 満たす方法 — エラー識別(3.3.1) {#how-to-meet-error-identification}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)。

#### 詳細情報 — エラー識別(3.3.1) {#more-information-error-identification}

* [達成基準 3.3.1 について](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [達成基準 3.3.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Labels or Instructions (3.3.2) {#labels-or-instructions}

* 達成基準 3.3.2
* レベル A
* ラベルまたは説明：コンテンツにユーザー入力が必要な場合に、ラベルまたは説明が提供されている。

#### 目的 - ラベルまたは説明（3.3.2） {#purpose-labels-or-instructions}

フォームへの入力を支援する説明を提供することは、インターフェイスを使いやすくするための基本です。これをおこなうことは、視覚や認知の障碍のあるユーザーに特に役立ちます。この説明がないと、フォームのレイアウトや、フォームの特定のフィールドで提供されているデータの種類を理解することが困難になるからです。

##### Forms

In the AEM WKND demo project a default label is added when you add a form component, such as a **Text Field**, to the page. このデフォルトのタイトルはコンポーネントのタイプによって異なります。そのフィールドの編集ダイアログの「**タイトルとテキスト**」タブに、独自のタイトルを追加できます。各フォームコンポーネントに関連付けられているデータをユーザーが理解できるようなラベルを指定することが重要です。

この「**タイトル**」フィールドは、支援テクノロジーで使用できるラベルを提供するので、フィールド要素用に使用する必要があります。フィールドの横のテキストにラベルを書き込むだけでは不十分です。

一部のフォームコンポーネントでは、「**タイトルを非表示にする**」チェックボックスを使用してラベルを非表示にすることもできます。この方法で非表示にしたラベルは、支援テクノロジーでは引き続き使用できますが、画面には表示されません。状況によっては、この方法で十分ですが、通常は、可能な限り目に見えるラベルを含めることをお勧めします。画面の非常に狭い部分（フィールド 1 つずつ）を見ていて、ラベルによってフィールドを正確に識別できることを必要としているユーザーがいる可能性もあるからです。

###### 画像ボタン {#image-buttons}

Where image buttons are used (for example, the **Image Button** component of the WKND project) the **Title** field in the **Title and Text** tab of the edit dialog actually provides the alt text for the image, rather than the label. 以下の例では、`Submit` というテキストを持つ画像に、`Submit` という代替テキストが、編集ダイアログの「**タイトル**」フィールドを使用して追加されています。

###### フォームフィールドのグループ {#groups-of-form-fields}

In the WKND project, where there is a group of related controls, such as **Radio Group**, a title may be needed for the group, as well as individual controls. AEMでラジオボタンのセットを追加する場合、「**タイトル**」フィールドにはこのグループタイトルが表示されますが、個々のタイトルはラジオボタン（**項目**）の作成時に指定されます。

ただし、グループタイトルとラジオボタン自体との間には、プログラム的な関連付けはありません。テンプレートエディターでは、必要な `fieldset` タグと `legend` タグでタイトルを囲んで、この関連付けを作成する必要があります。この処理は、ページのソースコードを編集することによってのみ可能です。また、システム管理者がこれらの要素のサポートを追加して、**フィールドのプロパティ**&#x200B;ダイアログに表示させることもできます（「追加の HTML 要素および属性のサポートの追加」を参照）。

<!--
However, there is no programmatic association between the group title and the radio buttons themselves. Template editors would need to wrap the title in the necessary `fieldset` and `legend` tags to create this association and this can only be done by editing the page source code. Alternatively, a system administrator can add support for these elements so that they appear in the **Field Properties** dialog (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

###### フォームに関するその他の考慮事項 {#additional-considerations-for-forms}

データを特定の形式で入力する必要がある場合は、ラベルテキストでそのことを明確に示します。例えば、日付を `DD-MM-YYYY` という形式で入力する場合は、ラベルの一部としてこのことを具体的に示します。つまり、スクリーンリーダーユーザーがフィールドに遭遇したとき、形式に関する追加情報も含めて、ラベルが自動的に読み上げられるということです。

入力が必須のフォームフィールドがある場合は、「必須」という単語をラベルの一部として使用して、このことを明確に示します。AEM では、必須のフィールドにはアスタリスクが追加されますが、「`required`」（必須）という単語をラベル自体に含めることが理想的です（編集ダイアログの「**タイトル**」フィールドを使用）。

ラベルの配置も、適切なフィールドを見つけるうえで役立つので重要です。このことは、複雑なフォームの場合に特に重要です。次の規則に従います。

* チェックボックスまたはラジオボタン：ラベルをフィールドのすぐ右に配置します。
* その他すべてのフォームコンポーネント（テキストボックス、コンボボックスなど）：ラベルをフィールドのすぐ上またはすぐ左に配置します。

機能がごく限られている簡単なフォームでは、「`Submit`」ボタンに適切にラベルを付けると、隣のフィールド（「`Search`」など）のラベルとしての役割を果たすことができます。これは、ラベルテキストのスペースを見つけることが困難な可能性のある場合に便利です。

#### 詳細情報 - ラベルまたは説明（3.3.2） {#more-information-labels-or-instructions}

* [達成基準 3.3.2 について](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [達成基準 3.3.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### エラーの提案(3.3.3)  {#error-suggestion}

* 達成基準 3.3.3
* レベル AA
* キーボード： 入力エラーが自動的に検出され、修正候補がわかる場合は、コンテンツのセキュリティや目的を危険にさらさない限り、修正候補がユーザーに提供されます。

#### 目的 — エラーの提案(3.3.3) {#purpose-error-suggestion}

この成功基準の目的は、入力エラーの修正に必要な適切な提案がユーザーに確実に届くようにすることです。 WCAG 2.0の「入力エラー」の定義では、これは「ユーザーが提供する情報で、受け入れられないもの」であると言っています。 受け付けられない情報の例としては、ユーザーが必要とするが省略する情報や、ユーザーが提供するが、必要なデータ形式または許容される値に該当しない情報などがあります。

成功基準3.3.1はエラーの通知を提供します。 しかし、認識の限界を持つ人は、誤りの修正方法を理解するのが難しい場合があります。 視覚に障害を持つユーザーは、エラーの修正方法を正確に理解できない場合があります。 フォームの送信に失敗した場合、エラーの発生を認識しているにもかかわらず、エラーの修正方法が不明である可能性があるので、ユーザーはフォームを放棄する可能性があります。

コンテンツ作成者がエラーの説明を提供したり、ユーザーエージェントが技術に固有の、プログラム的に決定された情報に基づいてエラーの説明を提供したりできます。

#### 満たす方法 — エラー提案(3.3.3) {#how-to-meet-error-suggestion}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)。

#### 詳細情報 — エラーの提案(3.3.3) {#more-information-error-suggestion}

* [達成基準 3.3.3 について](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [達成基準 3.3.3 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### エラー防止（法律、財務、データ） (3.3.4)  {#error-prevention-legal-financial-data}

* 達成基準 3.3.4
* レベル AA
* エラー防止（法律、財務、データ）: ユーザーに関する法的コミットメントや財務トランザクションの発生、データストレージシステムのユーザー制御可能なデータの変更や削除、またはユーザーテスト応答の送信を引き起こすWebページについては、次のうち少なくとも1つが真です。

   * ReversibleSubmissionsは元に戻すことができます。
   * ユーザーが入力したCheckedDataに入力エラーがないかどうかがチェックされ、ユーザーに修正の機会が与えられます。
   * 確認済み送信の最終処理を行う前に、情報の確認、確認および修正を行うメカニズムを利用できます。

#### 目的 — エラー防止（法的、財務、データ）(3.3.4) {#purpose-error-prevention-legal-financial-data}

この成功基準の目的は、障害を持つユーザーが、元に戻せない操作を実行する際に、誤りが原因で重大な結果が生じるのを回避できるよう支援することです。 例えば、返金不能な航空券を購入したり、証券会社の口座で株式を購入するように注文を送信したりすると、深刻な影響を受ける金融取引となります。 航空便の日に誤りを犯した場合は、交換できない間違った日のチケットがユーザーに送られる可能性があります。 購入する株式の数を間違えた場合は、意図した数よりも多くの株式を購入することになる。 どちらのエラーも、すぐに行われ、後で変更することができないトランザクションを伴うので、非常にコストがかかります。 同様に、データベースに保存されたデータを誤って変更または削除し、後でアクセスする必要が生じた場合、例えば旅行サービスのWebサイトに保存されている旅行プロファイル全体を誤って修正または削除すると、回復不能なエラーとなります。 「ユーザー制御可能」なデータの変更または削除を参照する場合、意図はファイルやレコードの削除など、データの大量損失を防ぐことです。 各保存コマンドの確認、またはドキュメント、レコード、その他のデータの単純な作成や編集は必要ありません。

障害を持つユーザーは、間違いを犯す可能性が高くなる場合があります。 読書障害を持つ人は数字や文字を転用したり、運動障害を持つ人は誤ってキーを押したりする場合があります。 アクションを取り消す機能を提供すると、ユーザーは重大な結果を招く可能性のある誤りを修正できます。 情報の確認と修正を行う機能を提供すると、ユーザーは重大な影響を及ぼす行動を取る前に、誤りを検出する機会を得ることができます。

ユーザ制御可能なデータは、意図的な行動によってユーザが変更および/または削除できるユーザ視認可能なデータである。 このようなデータを制御するユーザーの例としては、ユーザーのアカウントの電話番号と住所を更新したり、Webサイトから過去の請求書のレコードを削除したりします。 インターネットログや検索エンジンの監視データなど、ユーザーが直接表示したりやり取りしたりできないデータは参照しません。

#### 対応方法 — エラー防止（法律、財務、データ）(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

「成功条件の [満たし方」のガイドラインに従います](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)。

#### 詳細情報 — エラー防止（法律、財務、データ） (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [達成基準 3.3.4 について](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [達成基準 3.3.4 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原則4: 堅牢 {#principle-robust}

[原則4: 堅牢 — コンテンツは、支援テクノロジーを含む様々なユーザーエージェントによって解釈できる堅牢性が必要です。](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[ガイドライン4.1の互換性： 支援テクノロジーを含む、現在および将来のユーザーエージェントとの互換性を最大化します。](https://www.w3.org/TR/WCAG/#compatible)

支援テクノロジーを含む、現在および将来のユーザーエージェントとの互換性を最大化します。

### 解析(4.1.1)  {#parsing}

* 達成基準 4.1.1
* レベル A
* 解析中： マークアップ言語を使用して実装したコンテンツでは、要素に完全な開始タグと終了タグが付けられ、要素はその仕様に従ってネストされ、重複属性は含まれず、IDは一意です。ただし、指定によって機能が許可される場合は異なります。

#### 目的 — 解析(4.1.1) {#purpose-parsing}

この成功基準の目的は、支援テクノロジーを含むユーザーエージェントがコンテンツを正確に解釈および解析できるようにすることです。 コンテンツをデータ構造に解析できない場合、異なるユーザーエージェントがそのコンテンツを異なる方法で表示したり、完全に解析できない場合があります。 一部のユーザーエージェントは、コード化が不完全なコンテンツをレンダリングする際に、「修復テクニック」を使用します。

修復技術はユーザーエージェントによって異なるので、ユーザーエージェントの正式な文法で定義された規則に従ってコンテンツが作成されない限り、コンテンツが正確にデータ構造に解析される、または補助技術などの特殊なユーザーエージェントが正しくレンダリングされるとは想定できません。 マークアップ言語では、要素と属性の構文のエラーと、正しくネストされた開始/終了タグの提供に失敗すると、エラーが発生し、ユーザーエージェントがコンテンツを確実に解析できなくなります。 したがって、成功基準では、正式な文法規則の規則のみを使用して内容を解析できる必要があります。

#### 満たす方法 — 解析(4.1.1) {#how-to-meet-parsing}

「成功条件の [満たし方」のガイドラインに従います。 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### 詳細 — 解析(4.1.1) {#more-information-parsing}

* [達成基準 4.1.1 について](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [達成基準 4.1.1 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名前、役割、値(4.1.2)  {#name-role-value}

* 達成基準 4.1.2
* レベル A
* 名前、役割、値： すべてのユーザーインターフェイスコンポーネント（以下を含む） フォーム要素、リンク、スクリプトによって生成されるコンポーネントを参照)、名前と役割をプログラムによって決定できます。 ユーザーが設定できる状態、プロパティ、および値は、プログラムによって設定できます。 および、これらの項目に対する変更の通知は、支援テクノロジーを含むユーザーエージェントが利用できます。

#### 目的 — 名前、役割、値(4.1.2) {#purpose-ame-role-value}

この成功基準の目的は、支援テクノロジー(AT)がコンテンツ内のユーザーインターフェイスコントロールのステータスに関する情報を収集、アクティブ化（設定）し、最新の状態に保つことです。

アクセシブルなテクノロジーの標準的なコントロールを使用する場合、このプロセスは簡単です。 仕様に従ってユーザーインターフェイス要素が使用されると、この規定の条件が満たされます。 （以下の成功基準4.1.2の例を参照）。

ただし、カスタムコントロールを作成した場合、または（コードまたはスクリプト内の）インターフェイス要素が通常とは異なる役割や機能を持つようにプログラムされている場合は、補助テクノロジーに重要な情報を提供し、補助テクノロジーで制御できるよう追加の対策を講じる必要があります。

ユーザインターフェイスコントロールの特に重要な状態は、フォーカスがあるかどうかです。 コントロールのフォーカス状態をプログラム的に判定し、フォーカスの変更に関する通知をユーザエージェントや支援技術に送る。 ユーザーインターフェイスコントロール状態のその他の例としては、チェックボックスやラジオボタンが選択されているかどうか、または折りたたみ可能なツリーやリストノードが展開されているか折りたたまれているかどうかなどがあります。

#### 会う方法 — 名前、役割、値(4.1.2) {#how-to-meet-ame-role-value}

「成功条件の [満たし方」のガイドラインに従います。 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### 詳細情報 — 名前、役割、値(4.1.2) {#more-information-ame-role-value}

* [達成基準 4.1.2 について](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [達成基準 4.1.2 の達成方法](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
