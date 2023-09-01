---
title: コンテンツフラグメントの操作の概要
description: Adobe Experience Manager(AEM) のコンテンツフラグメントを使用して、ページに依存しないコンテンツのデザイン、作成、キュレーション、使用を可能にし、ヘッドレス配信やページオーサリングに最適な方法を説明します。
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 40%

---


# コンテンツフラグメントの操作の概要 {#overview-working-with-content-fragments}

Adobe Experience Manager(AEM) をas a Cloud Serviceしたコンテンツフラグメントを使用すると、デザイン、作成、キュレーション、および [ページに依存しないコンテンツを公開](/help/sites-cloud/authoring/fundamentals/content-fragments.md). 複数の場所や複数のチャネルで使用できるコンテンツを準備でき、ヘッドレス配信やページオーサリングに最適です。

>[!IMPORTANT]
>
>コンテンツフラグメントには次の 2 つのコンソールからアクセスできます。 **コンテンツフラグメント** および **Assets**.
>
>コンテンツフラグメントには 2 つのエディターも使用できます。 （両方のエディターは、両方のコンソールからアクセスできます）。
>
>この節では、 **コンテンツフラグメント** コンソールと *新規* コンテンツフラグメントエディター。 これらはヘッドレスコンテンツ配信用に開発されています（ただし、すべてのシナリオで使用できます）。
>
>詳しくは、次のセクションを参照してください。
>
>* の使用 **Assets** コンソール [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)
>* の使用 [*オリジナル* コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md),
>* using [ページオーサリング用のコンテンツフラグメント](/help/sites-cloud/authoring/fundamentals/content-fragments.md).


コンテンツフラグメントには、構造化されたコンテンツが含まれます。

* 各フラグメントは、 [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * コンテンツフラグメントモデルは、生成されるフラグメントの構造を定義します。
* すべてのフラグメントは、次の要素で構成されます。
   * **[メイン](#main-and-variations)**  — コアコンテンツを保持するフラグメントの不可欠な部分。常に存在し、削除できない
   * **[バリエーション](#main-and-variations)**  — 作成者が作成したコンテンツの順列（1 つ以上）
* 構造の範囲は次のとおりです。
   * 基本
      * 例えば、1 つの複数行テキストフィールドがあるとします。
      * ページオーサリングで使用する単純なコンテンツを用意するのに使用できます。
      * また、アプリケーションへのヘッドレス配信にも使用できます。
   * 複合
      * テキスト、数値、ブール値、日時など、様々なデータタイプの多くのフィールドの組み合わせ。
      * は、ページオーサリング用により構造化されたコンテンツを準備する場合や、アプリケーションへのヘッドレス配信に使用できます。
   * 入れ子
      * 使用可能な参照データ型を使用して、コンテンツをネストできます。
      * アプリケーションへのヘッドレス配信に使用される傾向があります。

コンテンツフラグメントは、AEMコアコンポーネントの Sling Model(JSON) 書き出し機能を使用して、JSON 形式で配信することもできます。 この形式の配信では次のことが可能です。

* コンポーネントを使用して、配信するフラグメントの要素を管理できます。
* 一括配信を許可します。複数の [コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja) （API 配信に使用されているページ）

通信チャネルの数は年々増加しています。通常、チャネルとは配信メカニズムのことであり、次のどちらも指します。

* 物理チャネル：例えば、デスクトップ、モバイルなど。
* 物理チャネルでの配信形式：デスクトップ用の「製品詳細ページ」や「製品カテゴリーページ」、モバイル用の「モバイル web」や「モバイルアプリ」など。

ただし、おそらく、 *正確* すべてのチャネルで同じコンテンツ — 特定のチャネルに応じてコンテンツを最適化する必要があります。

コンテンツフラグメントを使用すると、次のことが可能になります。

* 複数のチャネルでターゲットオーディエンスに効率よくリーチする方法を検討する。
* チャネルに依存しないエディトリアルコンテンツを作成、管理する。
* 多様なチャネル向けのコンテンツプールを構築する。
* 特定のチャネル向けにコンテンツのバリエーションをデザインする。
* アセットを挿入して画像をテキストに追加します。
* データの複雑さを反映して、ネストされたコンテンツを作成する。

その後、これらのコンテンツフラグメントを組み立てて、様々なチャネルをまたいでエクスペリエンスを提供できます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>* **コンテンツフラグメント**&#x200B;は、定義と構造を備えたエディトリアルコンテンツですが、視覚的なデザインやレイアウトは追加されていません。これらを使用して、テキスト、数値、日付などの構造化データにアクセスできます。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
>
>詳しくは、 [AEMのコンテンツフラグメントとエクスペリエンスフラグメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments).

以下のページでは、コンテンツフラグメントを作成、設定、管理、使用するためのタスクについて説明します。

* [インスタンスに対するコンテンツフラグメント機能を有効化します。](/help/sites-cloud/administering/content-fragments/setup.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)  — モデルの有効化、作成、定義
* [コンテンツフラグメントを作成する](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) （コンテンツフラグメントコンソールを使用）

フラグメントを作成した後は、次の操作を実行できます。

* [コンテンツフラグメントコンソールの使用](/help/sites-cloud/administering/content-fragments/managing.md)  — フラグメントにアクセス、公開（プレビューまたは実稼動用）し、参照する
* [コンテンツフラグメントエディターの使用](/help/sites-cloud/administering/content-fragments/authoring.md)  — フラグメントを編集、公開（プレビューまたは実稼動用）し、参照する
* [分析](/help/sites-cloud/administering/content-fragments/analysis.md)  エディターを使用したコンテンツフラグメントの構造
* [GraphQLを使用してフラグメントにアクセスし、アプリケーションにヘッドレスで配信](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [または、フラグメントをページオーサリングに使用します。](/help/sites-cloud/authoring/fundamentals/content-fragments.md)

>[!NOTE]
>
>これらのページは、以下と共に読み取ることができます。
>
>* [コンテンツフラグメントのカスタマイズと拡張](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [レンダリングコンポーネントのコンテンツフラグメントの設定](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)

## メインとバリエーション {#main-and-variations}

バリエーションは、AEMコンテンツフラグメントの重要な機能です。 これにより、 **メイン** 特定のチャネルやシナリオで使用するコンテンツ。ヘッドレスなコンテンツ配信やページオーサリングをより柔軟におこなえます。

* **メイン**

   * **メイン** はバリエーションとは異なり、すべてのバリエーションの基礎となります。
   * フラグメントの不可欠な構成要素

      * すべてのコンテンツフラグメントには、 **メイン**.
      * **メイン** は削除できません。

   * **メイン** は、フラグメントエディターの下にあります。 **[バリエーション](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >エディターで、 **Assets** コンソール **メイン** 次のラベルが付けられます： **マスター**.

* **バリエーション**

   * 編集目的に合わせたフラグメントテキストのレンディション。チャネルに関連付けることができますが必須ではありません。ローカルで臨時に変更する場合にも使用できます。
   * のコピーとして作成 **メイン**&#x200B;を編集する場合もありますが、その後、必要に応じて編集できます。多くの場合、バリエーション同士にはコンテンツの重複があります。
   * フラグメントのオーサリング中に、左のパネルから定義できます。
   * コンテンツコピーの分散を避けるために、フラグメントに格納されます。
   * バリエーションは、 [比較および同期済み](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) 次を使用 **メイン**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## コンテンツフラグメントとコンテンツサービス {#content-fragments-and-content-services}

AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

配信は、JSON エクスポーターを使用して JSON 形式で行われます。

AEM コンテンツフラグメントを使用して構造化コンテンツを記述し、管理できます。構造化コンテンツは、テキスト、数値データ、ブール値、日付と時刻など、様々なコンテンツタイプを含めることができるモデルを使用して定義します。

AEM コアコンポーネントの JSON 書き出し機能と共にこの構造化コンテンツを使用して、AEM コンテンツを AEM ページ以外のチャネルに配信できます。

>[!NOTE]
>
>AEM Sites as a Cloud Service 向けヘッドレス開発の概要については、[AEM Sites as a Cloud Service 向けヘッドレス開発](/help/headless/introduction.md)を参照してください。

>[!NOTE]
>
>AEM はフラグメントコンテンツの翻訳もサポートしています。詳しくは、「[アセットの翻訳](/help/assets/translate-assets.md)」を参照してください。

## コンテンツタイプ {#content-type}

コンテンツフラグメントとは、次のようなものです。

* **Sites** 機能。

* **Assets** として格納されます。

   * コンテンツフラグメント（とバリエーション）は、 [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * で作成および編集済み [コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/authoring.md).

* 次を使用したコンテンツ配信用にアクセス可能： [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md).

* 次の場所で使用可能： [コンテンツフラグメントコンポーネントを使用したページエディター](/help/sites-cloud/authoring/fundamentals/content-fragments.md) （参照コンポーネント）:

   * The [コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja) は、ページ作成者が使用できます。 これにより、必要なコンテンツフラグメントをHTMLまたは JSON 形式で参照し、配信できます。

コンテンツフラグメントは、次のようなコンテンツ構造です。

* レイアウトやデザインがありません（テキストフィールドではテキストの書式設定が可能です）。
* 配信メカニズム（ページやチャネルなど）に依存しません。
* 1 つ以上の[構成要素](#constituent-parts-of-a-content-fragment)を含みます。
* [画像を含めたり、関連付けたりする](#fragments-with-visual-assets)ことができます。

### ビジュアルアセットを含むフラグメント {#fragments-with-visual-assets}

作成者がより詳細にコンテンツを制御できるように、画像をコンテンツフラグメントに追加したり、コンテンツフラグメントと統合したりできます。

アセットとコンテンツフラグメントの組み合わせは、様々な方法で使用できます。それぞれに独自の利点があります。

* as a **コンテンツ参照**
* 内 **複数行テキスト** フィールド

### コンテンツフラグメントの構成要素 {#constituent-parts-of-a-content-fragment}

コンテンツフラグメントアセットは、次の部分（直接的または間接的）で構成されます。

* **フラグメントの要素**

   * 要素は、コンテンツを含むデータフィールドと相関関係にあります。
   * 次を使用する： [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) をクリックして、コンテンツフラグメントを作成します。 モデルで指定された要素（フィールド）は、フラグメントの構造を定義します。このような要素（フィールド）には様々なデータタイプがあります。

* **フラグメントの段落**

   * 個々のエンティティとして区切られたテキストのブロック（多くの場合は複数行）。

   * ページ作成中にコンテンツを制御できます。

* **フラグメントのメタデータ**

   * [アセットメタデータスキーマ](/help/assets/metadata-schemas.md)を使用します。
   * タグは、次のことを行うときに作成できます。

      * フラグメントを作成してオーサリングするとき。
      * または、後で、 [プロパティを表示または編集する](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) フラグメントエディターで

  >[!CAUTION]
  >
  >メタデータ処理プロファイルは、コンテンツフラグメントには適用されません。

  >[!CAUTION]
  >
  >コンテンツフラグメントモデルでは、多くの場合、 **タイトル** および **説明**. これら 2 つのフィールドが存在する場合、それらはユーザー定義のフィールドで、エディターのコンテンツ領域で更新できます。
  >
  >コンテンツフラグメントとそのバリエーションには、 **タイトル** および **説明**. これら 2 つのメタデータフィールドは、コンテンツフラグメントとバリエーションの不可欠な部分で、フラグメントの作成時に最初に定義されます。 これらは、エディターの「プロパティ/メタデータ」領域で更新できます。

* **[メイン](#main-and-variations)**
* **[バリエーション](#main-and-variations)**

### フラグメントを利用するための要件 {#required-by-fragments}

コンテンツフラグメントを作成するには、次が必要です。

* **コンテンツモデル**

   * ](/help/sites-cloud/administering/content-fragments/setup.md)設定ブラウザーを使用して有効化[されます。
   * [ツールを使用して作成](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)されます。
   * [フラグメントを作成](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments)するために必要です。
   * フラグメントの構造（タイトル、コンテンツ要素、タグ定義）を定義します。
   * コンテンツフラグメントモデルの定義にはタイトルと 1 つのデータ要素が必要です。その他すべてはオプションです。
   * モデルでは、デフォルトコンテンツを定義できます（該当する場合）。
   * 作成者は、フラグメントコンテンツのオーサリング時に定義された構造を変更できません。ただし、フラグメントエディターからモデルエディターを開くことはできます。
   * 依存コンテンツフラグメントの作成後にモデルに対して行った変更は、これらのコンテンツフラグメントに影響を与える可能性があります。

ヘッドレスコンテンツ配信にコンテンツフラグメントを使用するには、次も必要です。

* a [GraphQLクエリ](/help/headless/graphql-api/content-fragments.md) 必要な内容を要求する
* このコンテンツは、AEM向けの独自のSPAを開発する際に使用できます。詳しくは、次のドキュメントを参照してください。

   * [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [React の使用を開始する](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Angular の使用を開始する](/help/implementing/developing/hybrid/getting-started-angular.md)

コンテンツフラグメントをページオーサリングに使用するには、次のものも必要です。

* A **コンテンツフラグメントコンポーネント**

   * フラグメントを HTML 形式や JSON 形式で配信するのに役立ちます。
   * [ページ上でフラグメントを参照](/help/sites-cloud/authoring/fundamentals/content-fragments.md)するために必要です。
   * フラグメントのレイアウトと配信（チャネルなど）を担当します。
   * フラグメントは、レイアウトを定義し、一部またはすべての要素／バリエーションと関連するコンテンツを配信するために、1 つ以上の専用コンポーネントを必要とします。
   * 作成時にフラグメントをページにドラッグすると、必要なコンポーネントが自動的に関連付けられます。
   * 詳しくは、 [コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja).

## 使用例 {#example-usage}

フラグメントと、その要素およびバリエーションを一緒に使用して、複数のチャネルに対応した一貫性のあるコンテンツを作成できます。フラグメントをデザインする際は、何を使用し、どこで使用するかを考慮する必要があります。

### WKND サンプル {#wknd-sample}

The [WKND サイトと WKND 共有](/help/implementing/developing/introduction/develop-wknd-tutorial.md) AEM as a Cloud Serviceの学習に役立つサンプルが用意されています。

<!-- CHECK: which links can/should be used these days? -->

WKND プロジェクトには、次のものが含まれます。

* 次の URL で入手できるコンテンツフラグメントモデル：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：

   * `.../assets.html/content/dam/wknd/en`
