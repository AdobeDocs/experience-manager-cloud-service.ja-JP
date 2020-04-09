---
title: WCAG 2.1のクイックガイド
seo-title: WCAG 2.1のクイックガイド
translation-type: tm+mt
source-git-commit: 11f0509334ebe4456612789fd415a3099687dc64

---


# A Quick Guide to WCAG 2.1{#quick-guide-to-wcag}

クラウドサービスとしてのAdobe Experience Manager(AEM)は、Webコンテンツのアクセシビリティガイドラインへの準拠を最大限に高めるように開発されました。

[Web Content Accessibility Guidelines バージョン 2.1（WCAG）](https://www.w3.org/TR/WCAG/)は、[World Wide Web Consortium（W3C）](https://www.w3.org/)が [Web Accessibility Initiative（WAI）](https://www.w3.org/WAI/)の下で開発した一連のガイドラインであり、国際的に認知されています。

WCAG 2.1 は、障碍のあるユーザーが Web コンテンツにアクセスして利用できるようにするための、テクノロジーから独立した一連のガイドラインおよび達成基準で構成されます。これらのガイドラインでは、Web コンテンツの作成者、デザイナー、開発者を対象として、視覚障碍、難聴、学習障碍、加齢に伴う制限をはじめとする障碍の種類に関係なく、できるだけ多くの人ができるだけ容易にアクセスできるようなリソースを作成するようアドバイスしています。

例えば、HTML の `alt` 属性を使用して画像（またはその他のテキスト以外のコンテンツ）を説明すると、視覚障碍または弱視の人にとって大きな助けとなります。The textual description in the `alt` attribute can either be converted into speech output or transmitted to electronic refreshable braille displays.

また、WCAG 2.1 は、状況的問題&#x200B;**&#x200B;を抱える人などにも恩恵があります。ブラウズテクノロジー、ネットワーク接続速度、ブラウズ環境などの環境が原因で、障碍を抱える人と同じような障壁に直面することもあります。

Adobe Experience Manager を使用すると、コンテンツ作成者や Web サイトの所有者は、関連する WCAG 2.1 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

したがって、WCAG 2.1 の目的とガイドラインの構造を理解することは、Web アクセシビリティについて理解したり、ガイドラインを参考にアクセスしやすい Web コンテンツを作成したりするうえで重要です。

WCAG 2.1 の目的は次のようなガイドラインを提供することです。

* **テクノロジーに非依存：**&#x200B;言い換えると、これらのガイドラインは、HTML に限らず、様々な Web コンテンツ形式に適用できます。つまり、WCAG 2.1 では、PDF、Flash、JavaScript、およびその他の最新／将来の Web テクノロジーによって生成または提供されるコンテンツをカバーしています。<!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* **テスト可能：**&#x200B;各ガイドラインは、客観的にテストできるように記述されており、アクセシビリティの専門家グループによるガイドライン準拠の同意が得られやすくなっています。アクセシビリティガイドラインの課題の 1 つは、技術的にテスト可能なものもあれば、ガイドラインに正しく準拠しているかどうかの判断が人間に委ねられる場合もあることです。<!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* 優先度の高 **いコンテキスト実装をサポート：**
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

これらの目的は、WCAG 2.1 の構造に大きく影響しています。

>[!NOTE]
>
>考えられるあらゆる障碍、またはあらゆるタイプの人を考慮に入れた Web サイトを作成することは不可能です。WCAG 2.1 の目的は、Web 作成者が、特定の条件下かつ妥当な範囲内で可能な限り容易にアクセスできるサイトを作成できるようにすることです。

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## 構造 {#structure}

WCAG 2.1 は、アクセスしやすい Web コンテンツの作成の概念を徐々に詳細に紹介するように構造化されています。この点から、WCAG 2.1 は非常に複雑な連結ドキュメントセットであるという印象を受けますが、詳細情報を 1 つの非常に大きなドキュメントでまとめて提供するのではなく、作成者が必要とするときに（徐々に）提供することを目的としています。

WCAG 2.1は、アクセシブルなデザインの4つの主要な原則で構成されています。略語 **POURと呼ばれる場合もあります**。 これらは次のとおりです。

1. **知覚可能**：ユーザーが該当する Web コンテンツを感じ取ることが可能か。
1. **操作可能**：ユーザーがナビゲートしたり、データを入力したり、Web コンテンツと対話したりすることが可能か。
1. **理解可能**：ユーザーが提示された Web コンテンツを処理および理解することが可能か。
1. **堅牢**：従来のブラウズ環境と新興のブラウズ環境の両方を含め、様々なブラウズ環境で Web コンテンツを意図したとおりに利用できるか。

詳しくは、
* 各&#x200B;**原則**&#x200B;は 1 つ以上の&#x200B;**ガイドライン**&#x200B;で構成されます。

* ガイドラインは、肯定的表現（Do this...）または否定的表現（Do not do this...）の指示として記載されています。
* ガイドラインには 1.1 ～ 4.1 の番号が割り振られ、先頭番号は親原則に対応しています。
* 各ガイドラインは 1 つ以上の&#x200B;**達成基準**&#x200B;で構成されます。
* 達成基準は、特定の Web ページに対して `True` または `False` のいずれかの表現で記述されています。
* 達成基準には、二者択一の選択肢が含まれているか、例外、つまり達成基準を満たす必要がない状況が示されています。
* 達成基準には、親ガイドラインおよび親原則に従って、1.1.1 ～ 4.1.1 の番号が割り振られています。また、容易に参照できるように、基準の意図を要約した簡易名が割り当てられています。例えば、達成基準 1.1.1 は非テキストコンテンツです。
* Success criteria include a list of related **techniques** (described in more detail below).

## サポートリソース {#supporting-resources}

WCAG 2.1 のコアコンポーネントである原則、ガイドライン、および達成基準とは別に、一連のサポートドキュメントが用意されています。これらの中には、ガイドラインの各側面に準拠する方法を具体的にアドバイスするものもあれば、様々な能力を持つ Web 作成者、デザイナー、および開発者が WCAG 2.1 を理解し、できるだけ効果的に使用するのに役立つ一般的な参考資料もあります。

WCAG 2.1 は不変のドキュメントであり、変更されることはありませんが、これらのサポートリソースのほとんどは動的なドキュメントであり、今後、新興テクノロジーが登場したり、Web アクセシビリティの達成方法について新たな例が見つかったりした場合、内容が改訂および追加されていきます。

### WCAG 2.1 リソース {#wcag-resources}

このリストは、完全なものではなく、利用可能なリソースの紹介を提供しています。
* [WCAG関連のすべてのドキュメント](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [様々なドキュメント](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Webコンテンツアクセシビリティガイドライン(WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [WCAG 2.1の新機能](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [WCAG 2.1を満たす方法に関するクイックリファレンスガイド](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2よくある質問](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### WCAG 2.1の新機能 {#what-is-new}

[WCAG 2.1の新機能は](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) 、WCAGと2.0およびWCAG 2.1の差に関する貴重な情報を提供します。

[WCAG 2.0および2.1は](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) 、関係の状況をさらに明確にします。

### WCAG 2.1 の各種テクニック {#techniques-for-wcag}

WCAG 2.1 の各種テクニックを「[Techniques for WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)」ページで参照できます。

これらの&#x200B;**テクニック**&#x200B;は、WCAG 2.1 階層の達成基準の下位レベルを構成するものです。これらは、WAI により、規範としてではなく、参考情報として分類されています。つまり、リソースを WCAG 2.1 に準拠させる際に、特定のテクニックに必ずしも従う必要はありません。

テクニックは達成基準よりも具体的に説明されており、通常、特定のテクノロジーやコンテンツタイプ（HTML やビデオなど）、状況（e コマースや e ラーニングアプリケーションなど）について言及されています。テクニックは、特定のガイドラインや達成基準に準拠するための実証済みの方法の例と考えることができ、特定のコンテキストで作業する作成者や開発者にとって役立ちます。

テクニックには次の場所からアクセスします。

* コレクション別（一般的な手法、またはHTML、CSS、クライアントサイドのスクリプティングなど特定の技術や形式に関する手法）、または
* 関連する達成基準から。テクニックは複数の達成基準に適用することができます。

各テクニックには、そのコレクションに関連する一意の番号が割り振られています。例えば、ARIA テクニックの 1 つは「*Technique ARIA2: Identifying required fields with the &quot;required&quot; property*」です。

テクニックは、「十分」（Sufficient）、「参考」（Advisory）、または「失敗」（Failure）に分類されます。

* 十分なテクニック&#x200B;**&#x200B;は、従うと、特定の達成基準を十分に満たすことができます。
* 参考テクニック&#x200B;**&#x200B;は、従うと、アクセシビリティにプラスの影響を与えますが、それだけでは特定の達成基準を満たすのに十分ではない可能性があります。
* 失敗テクニック&#x200B;**&#x200B;は、達成基準を満たすことができない特定の例を示すものです。

テクニックの詳細には、説明、適用可能性、例、さらに具体的な情報を示すリソース、テクニックを正しく適用できているかをテストする方法の詳細が含まれています。

テクニックのリストは完全なものではなく、Web テクノロジーの開発、デザインアプローチ、研究結果を反映した新しい例を追加する形で WAI により定期的に更新されています。したがって、テクニックのリストを定期的にチェックして、新たな追加がないか確認することをお勧めします。

### WCAG 2.1 の理解 {#understanding-wcag}

ここでは、特定のガイドラインや達成基準の目的を十分に理解するのに役立つアドバイスを記載した一連のドキュメントが紹介されています。[概要をダウンロードするとともに、リンクをたどってさらに詳細な情報を参照する](https://www.w3.org/WAI/WCAG21/Understanding/)ことができます。

個々のガイドラインおよび達成基準にも、次の情報を示す「理解」ページがそれぞれ個別に用意されています。

* ガイドラインの意図
* 特定の達成基準
* 参考テクニック（ガイドラインの要件を満たす際に参考になるものの、特定の達成基準に当てはまるわけではないもの）

個々の達成基準にも、次の情報を示す「理解」ページがそれぞれ個別に用意されています。

* 達成基準の意図
* 達成基準を満たす方法の一般的な例
* 達成基準を満たす方法を示す関連リソース（W3C 以外）
* 手法と失敗：成功基準を満たす方法の具体的で詳細な例（以下で詳しく説明）
* 主要用語 — 成功基準を理解する上で重要な用語集。

「[Understanding Success Criterion 1.1.1 (&quot;Non-text content&quot;)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content)」に例が紹介されています。

### WCAG 2.1 に準拠する方法 {#how-to-meet-wcag}

「[How To Meet WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)」ページには、ガイドラインに準拠するための方法を示す節があります。この節では、WCAG が別の形式で示されており、読者個人の関心や環境に合わせてガイドラインの内容を絞り込むことができます。読者は、カスケードスタイルシートやスクリプティングなどの特定の Web コンテンツテクノロジーを指定したり、特定の優先順位を指定したりすることによって、目的の達成基準テクニックをフィルタリングして表示できます。

フィルタリングを使用しなかった場合、すべての達成基準がガイドライン別にグループ化されて表示されます。達成基準ごとに次のものが用意されています。

* 達成基準のテキスト
* 対応する「理解」ドキュメントへのリンク
* 関連する十分なテクニックのリスト（各テクニックの詳細へのリンクあり）
* 関連する参考テクニックのリスト（各テクニックの詳細へのリンクあり、存在する場合）
* 関連する失敗のリスト（各失敗の詳細へのリンクあり）
