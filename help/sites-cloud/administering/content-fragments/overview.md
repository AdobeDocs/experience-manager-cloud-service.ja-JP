---
title: コンテンツフラグメントの操作の概要
description: Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントを使用して、ヘッドレス配信やページオーサリングに最適な構造化コンテンツを作成および使用できる方法について説明します。
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 2daddd852f4cfcbcd6b1d4aea9cd96e045c93ca0
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 97%

---

# コンテンツフラグメントの操作の概要 {#overview-working-with-content-fragments}

>[!IMPORTANT]
>
>早期導入プログラムを通じて、コンテンツフラグメントおよびコンテンツフラグメントモデルの様々な機能を利用できます。
>
>ステータスを確認し、興味がある場合に適用する方法について詳しくは、[リリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントを使用すると、ページに依存しないコンテンツを設計、作成、キュレーション、公開できます。複数の場所、複数のチャネル上で使用可能なコンテンツを用意でき、[ヘッドレス配信](/help/headless/what-is-headless.md)や[ページオーサリング](/help/sites-cloud/authoring/fragments/content-fragments.md)に理想的です。

>[!IMPORTANT]
>
>コンテンツフラグメントには、**コンテンツフラグメント**&#x200B;と **Assets** の 2 つのコンソールからアクセスできます。
>
>また、コンテンツフラグメントをオーサリングするエディターは 2 つあります。基本機能は同じですが、いくつか違いがあります。両方のエディターは、両方のコンソールからアクセスできます。
>
>この節では、**コンテンツフラグメント**&#x200B;コンソールと&#x200B;*新しい*&#x200B;コンテンツフラグメントエディターについて説明します。これらはヘッドレスコンテンツ配信用に開発されています（ただし、すべてのシナリオで使用できます）。
>
>詳しくは、次のセクションを参照してください。
>
>* [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md)のための **Assets** コンソールの使用
>* [*元の*&#x200B;コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)の使用
>* [ページオーサリング用のコンテンツフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)の使用


コンテンツフラグメントには、構造化されたコンテンツが含まれます。

* 各フラグメントは、[コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)に基づいています。
   * コンテンツフラグメントモデルは、生成されるフラグメントの構造を定義します。
* すべてのフラグメントは、次の要素で構成されます。
   * **[メイン](#main-and-variations)** - コアコンテンツを保持するフラグメントの不可欠な部分であり、常に存在し、削除できません
   * **[バリエーション](#main-and-variations)** - オーサーが作成したコンテンツの 1 つまたは複数の配列
* 構造の範囲は次のとおりです。
   * 基本
      * 例えば、1 つの複数行テキストフィールドです。
      * ページオーサリングで使用する単純なコンテンツを用意するのに使用できます。
      * また、アプリケーションへのヘッドレス配信にも使用できます。
   * 複合
      * テキスト、数値、ブーリアン、日時などの様々なデータ型のフィールドを多数組み合わせたもの。
      * ページオーサリング用のより構造化されたコンテンツを用意するためや、アプリケーションにヘッドレス配信するために使用できます。
   * 入れ子
      * 使用可能な参照データ型を使用して、コンテンツをネストできます。
      * アプリケーションへのヘッドレス配信に使用される傾向があります。

コンテンツフラグメントは、AEM コアコンポーネントの Sling モデル（JSON）書き出し機能を使用して、JSON 形式で配信することもできます。この形式の配信では次のことが可能です。

* コンポーネントを使用して、配信するフラグメントの要素を管理できます。
* API 配信に使用されるページで複数の[コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)を追加して、一括配信できます。

通信チャネルの数は年々増加しています。通常、チャネルとは配信メカニズムのことであり、次のどちらも指します。

* 物理チャネル：例えば、デスクトップ、モバイルなど。
* 物理チャネルでの配信形式：デスクトップ用の「製品詳細ページ」や「製品カテゴリーページ」、モバイル用の「モバイル web」や「モバイルアプリ」など。

ただし、すべてのチャネルでの&#x200B;*まったく*&#x200B;同じコンテンツの使用はお勧めしません。特定のチャネルに合わせてコンテンツを最適化する必要があります。

コンテンツフラグメントを使用すると、次のことが可能になります。

* 複数のチャネルでターゲットオーディエンスに効率よくリーチする方法を検討する。
* チャネルに依存しないエディトリアルコンテンツを作成、管理する。
* 多様なチャネル向けのコンテンツプールを構築する。
* 特定のチャネル向けにコンテンツのバリエーションをデザインする。
* アセットを挿入することでテキストに画像を追加します。
* データの複雑さを反映して、ネストされたコンテンツを作成します。

さらにこうしたコンテンツフラグメントを集めて組み立てることで、多様なチャネルにエクスペリエンスを提供できます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>* **コンテンツフラグメント**&#x200B;は、定義と構造を備えたエディトリアルコンテンツですが、視覚的なデザインやレイアウトは追加されていません。テキスト、数値、日付などの構造化データにアクセスするために使用できます。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
>
>詳しくは、[AEM のコンテンツフラグメントとエクスペリエンスフラグメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments)を参照してください。

このページおよび次のページでは、コンテンツフラグメントを作成、設定、維持管理および使用するためのタスクについて説明します。

* [お使いのインスタンスでコンテンツフラグメント機能を有効にする](/help/sites-cloud/administering/content-fragments/setup.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) - モデルを有効化、作成および定義します。
* [コンテンツフラグメントを作成](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)（コンテンツフラグメントコンソールを使用）

フラグメントが作成されたら、次の操作を実行できます。

* [ コンテンツフラグメントコンソールの使用 ](/help/sites-cloud/administering/content-fragments/managing.md) – 次の操作を行います。
   * フラグメントへのアクセス、公開（プレビューまたは実稼動用）、参照
* [ コンテンツフラグメントエディターの使用 ](/help/sites-cloud/administering/content-fragments/authoring.md) – 次の操作を行います。
   * フラグメントを編集、公開（プレビューまたは実稼動用）、参照します。
   * コメントを使用した他の作成者との共同作業
* [分析](/help/sites-cloud/administering/content-fragments/analysis.md)  エディターを使用したコンテンツフラグメントの構造
* [GraphQL を使用してフラグメントにアクセスし、アプリケーションへのヘッドレス配信を実現します](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)。
* [または、フラグメントをページオーサリングに使用します。](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>これらのページと併せて、次のページも参照してください。
>
>* [コンテンツフラグメントのカスタマイズと拡張](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [レンダリングコンポーネントのコンテンツフラグメントの設定](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-cloud/authoring/fragments/content-fragments.md)
>* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md) も利用できます。


## メインとバリエーション {#main-and-variations}

バリエーションは、AEM のコンテンツフラグメントの重要な機能です。これにより、特定のチャネルやシナリオで使用する&#x200B;**メイン**&#x200B;コンテンツのコピーを作成および編集でき、ヘッドレスコンテンツ配信やページオーサリングをより柔軟に行うことができます。

* **メイン**

   * **メイン**&#x200B;はバリエーションそのものではありませんが、すべてのバリエーションの基礎となります。
   * フラグメントの不可欠な構成要素

      * どのコンテンツフラグメントにも&#x200B;**メイン**&#x200B;のインスタンスが 1 つあります。
      * **メイン**&#x200B;は削除できません。

   * **メイン**&#x200B;には、フラグメントエディターの「**[バリエーション](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**」の下でアクセスできます。

  >[!NOTE]
  >
  >**Assets** コンソールから利用できるエディターでは、**メイン**&#x200B;は&#x200B;**マスター**&#x200B;としてラベル付けされています。

* **バリエーション**

   * 編集目的に合わせたフラグメントテキストのレンディション。チャネルに関連付けることができますが必須ではありません。ローカルで臨時に変更する場合にも使用できます。
   * **メイン**&#x200B;のコピーとして作成しますが、その後、必要に応じて編集できます。多くの場合、バリエーション同士にはコンテンツの重複があります。
   * フラグメントのオーサリング中に、左のパネルから定義できます。
   * コンテンツコピーの分散を避けるために、フラグメントに格納されます。
   * バリエーションは、**メイン**&#x200B;と[比較および同期](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text)できます。
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

   * コンテンツフラグメント（とバリエーション）は、[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)で作成および管理できます。
   * [コンテンツフラグメントエディター](/help/sites-cloud/administering/content-fragments/authoring.md)でオーサリングおよび編集されます。

* [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) を使用したコンテンツ配信用にアクセスできます。

* [コンテンツフラグメントコンポーネント（参照コンポーネント）を使用することで、ページエディター内で](/help/sites-cloud/authoring/fragments/content-fragments.md)使用できます。

   * [コンテンツフラグメントのコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)は、ページの作成者が使用できます。作成者は、コンテンツフラグメントコンポーネントを使用して、必要なコンテンツフラグメントを HTML または JSON 形式で参照し、配信できます。

コンテンツフラグメントは、次のようなコンテンツ構造です。

* レイアウトやデザインを伴いません（テキストフィールドに対してテキストの書式設定が可能です）。
* 配信メカニズム（ページやチャネルなど）に依存しません。
* 1 つ以上の[構成要素](#constituent-parts-of-a-content-fragment)を含みます。
* [画像を含めたり、関連付けたりする](#fragments-with-visual-assets)ことができます。

### ビジュアルアセットを含むフラグメント {#fragments-with-visual-assets}

作成者がより柔軟にコンテンツをコントロールできるように、画像をコンテンツフラグメントに追加したり、コンテンツフラグメントと統合したりできます。

コンテンツフラグメントアセットは、（直接的または間接的に）次の構成要素からなります。

* **コンテンツ参照**&#x200B;として
* **複数行テキスト**&#x200B;フィールド内に

### コンテンツフラグメントの構成要素 {#constituent-parts-of-a-content-fragment}

コンテンツフラグメントアセットは、（直接的または間接的に）次の構成要素からなります。

* **フラグメントの要素**

   * 要素は、コンテンツを含むデータフィールドと相関関係にあります。
   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)を使用して、コンテンツフラグメントを作成します。モデルで指定された要素（フィールド）は、フラグメントの構造を定義します。このような要素（フィールド）には様々なデータタイプがあります。

* **フラグメントの段落**

   * 個々のエンティティとして区切られたテキストのブロック（多くの場合は複数行）。

   * ページ作成中にコンテンツを制御できます。

* **フラグメントのメタデータ**

   * [アセットメタデータスキーマ](/help/assets/metadata-schemas.md)を使用します。
   * タグは、次のことを行うときに作成できます。

      * フラグメントを作成してオーサリングするとき。
      * または後で、フラグメントエディターで[プロパティを表示または編集する](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags)場合。

  >[!CAUTION]
  >
  >メタデータ処理プロファイルは、コンテンツフラグメントには適用されません。

  >[!CAUTION]
  >
  >コンテンツフラグメントモデルでは、多くの場合、**タイトル**&#x200B;および&#x200B;**説明**&#x200B;の名前が付けられたデータフィールドを定義できます。これらの 2 つのフィールドが存在する場合、それらはユーザー定義のフィールドであり、エディターのコンテンツ領域で更新できます。
  >
  >コンテンツフラグメントとそのバリエーションには、**タイトル**&#x200B;および&#x200B;**説明**&#x200B;と呼ばれるメタデータ（プロパティ）フィールドもあります。これらの 2 つのメタデータフィールドは、コンテンツフラグメントとバリエーションの不可欠な部分で、フラグメントの作成時に最初に定義されます。これらは、エディターのプロパティ／メタデータ領域で更新できます。

* **[メイン](#main-and-variations)**
* **[バリエーション](#main-and-variations)**

### フラグメントを利用するための要件 {#required-by-fragments}

コンテンツフラグメントを作成するには、次が必要です。

* **コンテンツモデル**

   * ](/help/sites-cloud/administering/content-fragments/setup.md)設定ブラウザーを使用して有効化[されます。
   * [ツールを使用して作成](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)されます。
   * [フラグメントを作成](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments)するために必要です。
   * フラグメントの構造（タイトル、コンテンツ要素、タグ定義）を定義します。
   * コンテンツフラグメントモデル定義にはタイトルと 1 つのデータ要素が必要です。その他すべてはオプションです。
   * モデルでは、デフォルトコンテンツを定義できます（該当する場合）。
   * オーサーは、フラグメントコンテンツのオーサリング時に定義された構造を変更できません。ただし、フラグメントエディターからモデルエディターを開くことはできます。
   * 依存コンテンツフラグメントの作成後にモデルに対して行った変更は、これらのコンテンツフラグメントに影響を与える可能性があります。

コンテンツフラグメントをヘッドレスコンテンツ配信に使用するには、次のものも必要です。

* 必要なコンテンツをリクエストするための [GraphQL クエリ](/help/headless/graphql-api/content-fragments.md)
* このコンテンツは、AEM 向けの独自の SPA を開発する際に使用できます。詳しくは、次のドキュメントを参照してください。

   * [SPA WKND チュートリアル](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [React の使用を開始する](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Angular の使用を開始する](/help/implementing/developing/hybrid/getting-started-angular.md)

コンテンツフラグメントをページオーサリングに使用するには、次のものも必要です。

* **コンテンツフラグメントコンポーネント**

   * フラグメントを HTML 形式や JSON 形式で配信するのに役立ちます。
   * [ページ上でフラグメントを参照](/help/sites-cloud/authoring/fragments/content-fragments.md)するために必要です。
   * フラグメントのレイアウトと配信（チャネルなど）に対応します。
   * フラグメントは、レイアウトを定義し、一部またはすべての要素／バリエーションと関連するコンテンツを配信するために、1 つ以上の専用コンポーネントを必要とします。
   * 作成時にフラグメントをページにドラッグすると、必須コンポーネントが自動的に関連付けられます。
   * [コンテンツフラグメントのコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)を参照してください。

## 使用例 {#example-usage}

フラグメントと、その要素およびバリエーションを一緒に使用すると、複数のチャネルに対応した一貫性のあるコンテンツを作成できます。フラグメントを設計するときは、何をどこで使用するかを考慮する必要があります。

### WKND のサンプル {#wknd-sample}

AEM as a Cloud Service について学ぶのに役立つ [WKND サイトと WKND 共有](/help/implementing/developing/introduction/develop-wknd-tutorial.md)サンプルが用意されています。

<!-- CHECK: which links can/should be used these days? -->

WKND プロジェクトには、次のものが含まれます。

* 次の URL で入手できるコンテンツフラグメントモデル：

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：

   * `.../assets.html/content/dam/wknd/en`
