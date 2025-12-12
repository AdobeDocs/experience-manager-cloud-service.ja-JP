---
title: コンテンツフラグメントの操作（Assets - コンテンツフラグメント）
description: Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントで、ページオーサリングやヘッドレス配信に最適な、コンテンツをデザイン、作成、キュレーションおよび使用する方法を説明します。
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: 2449bc380268ed42b6c8d23ae4a4fecaf1736889
workflow-type: tm+mt
source-wordcount: '2576'
ht-degree: 87%

---

# コンテンツフラグメントの使用方法 {#working-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントを使用すると、[ページに依存しないコンテンツの設計、作成、キュレーション、公開](/help/sites-cloud/authoring/fragments/content-fragments.md)が可能になります。ヘッドレ配信に最適とされる複数の場所、複数のチャネル上で使用可能なコンテンツを用意できるようになります。また、[マルチサイト管理と併用してコンテンツを再利用](#reusing-content-fragments-with-msm)することもできます。

コンテンツフラグメントには、構造化コンテンツが含まれます。

* 作成されるフラグメントの構造を事前定義する[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)に基づいています。
* 構造の範囲は次のとおりです。
   * 基本
      * 例えば、1 つの複数行テキストフィールドなどです。
      * ページオーサリングで使用する単純なコンテンツを用意するのに使用できます。
   * 複合
      * テキスト、数値、ブーリアン、日時などの様々なデータタイプのフィールドを多数組み合わせたもの。
      * ページオーサリング用のより構造化コンテンツを用意するためまたはアプリケーションに配信するために使用できます。
   * 入れ子
      * 使用可能な参照データ型を使用して、コンテンツをネストできます。
      * アプリケーションへの配信に使用される傾向があります。

コンテンツフラグメントは、AEM コアコンポーネントの Sling モデル（JSON）書き出し機能を使用して、JSON 形式で配信することもできます。この形式の配信では次のことが可能です。

* コンポーネントを使用して、配信するフラグメントの要素を管理できます。
* API 配信に使用されるページで複数のコンテンツフラグメントコアコンポーネントを追加して、一括配信できます。

>[!NOTE]
>
>コンテンツフラグメントは Sites 機能ですが、**Assets** として保存されます。
>
>コンテンツフラグメントとコンテンツフラグメントモデルは、主に&#x200B;**[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**&#x200B;コンソールで管理されるようになりましたが、コンテンツフラグメントは **Assets** コンソールから、コンテンツフラグメントモデルは **Tools** コンソールから引き続き管理できます。この節では、**Assets** コンソールと **Tools** コンソールでの管理について説明します。
>
>コンテンツフラグメントをオーサリングするエディターは 2 つあります。基本機能は同じですが、いくつか違いがあります。この節では、**Assets** コンソールから主にアクセスされるエディターについて説明します。（主に&#x200B;**コンテンツフラグメント**&#x200B;コンソールからアクセスされる）新しいエディターについて詳しくは、Sites のドキュメントの[コンテンツフラグメント - オーサリング](/help/sites-cloud/administering/content-fragments/authoring.md)を参照してください。どちらのエディターも、上部のツールバーに切替スイッチを使用して、他のエディターに素早くアクセスできます。

このページおよび次のページでは、コンテンツフラグメントを作成、設定、維持管理および使用するためのタスクについて説明します。

* [お使いのインスタンスでコンテンツフラグメント機能を有効にする](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md) - モデルを有効化、作成および定義します。
* [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md) - コンテンツフラグメントを作成し、編集、公開、参照します。
* [バリエーション - フラグメントコンテンツのオーサリング](/help/assets/content-fragments/content-fragments-variations.md) - フラグメントコンテンツをオーサリングし、マスターのバリエーションを作成します。
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - フラグメントに Markdown 構文を使用します。
* [関連コンテンツの使用](/help/assets/content-fragments/content-fragments-assoc-content.md) - 関連コンテンツを追加します。
* [メタデータ - フラグメントのプロパティ](/help/assets/content-fragments/content-fragments-metadata.md) - フラグメントのプロパティを表示および編集します。
* [コンテンツフラグメントと GraphQL を併用すると、アプリケーション用コンテンツを配信](/help/assets/content-fragments/content-fragments-graphql.md)できます。その一助として、[JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。
* [MSM を使用したコンテンツフラグメントの再利用](#reusing-content-fragments-with-msm)

>[!NOTE]
>
>これらのページと併せて、次のページも参照してください。
>
>* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-cloud/authoring/fragments/content-fragments.md)
>* [コンテンツフラグメントのカスタマイズと拡張](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [レンダリングコンポーネントのコンテンツフラグメントの設定](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [コンテンツフラグメントおよびコンテンツフラグメントモデルの OpenAPI](/help/headless/content-fragment-openapis.md)

通信チャネルの数は年々増加しています。通常、チャネルとは配信メカニズムのことであり、次のどちらも指します。

* 物理チャネル：例えば、デスクトップ、モバイルなど。
* 物理チャネルでの配信形式：デスクトップ用の「製品詳細ページ」や「製品カテゴリーページ」、モバイル用の「モバイル web」や「モバイルアプリ」など。

しかし、すべてのチャネルでまったく同じコンテンツを使用することはお勧めしません。特定のチャネルに合わせてコンテンツを最適化する必要があります。

コンテンツフラグメントを使用すると、次のことが可能になります。

* 複数のチャネルでターゲットオーディエンスに効率よくリーチする方法を検討する。
* チャネルに依存しないエディトリアルコンテンツを作成、管理する。
* 多様なチャネル向けのコンテンツプールを構築する。
* 特定のチャネル向けにコンテンツのバリエーションをデザインする。
* アセットを挿入することでテキストに画像を追加する（混在メディアフラグメント）。
* ネストされたコンテンツを作成して、データの複雑さを反映する。

さらにこうしたコンテンツフラグメントを集めて組み立てることで、多様なチャネルにエクスペリエンスを提供できます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fragments/content-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>
>* **コンテンツフラグメント**&#x200B;は、定義と構造を備えたエディトリアルコンテンツですが、視覚的なデザインやレイアウトは追加されていません。テキスト、数値、日付などの構造化データにアクセスするために使用できます。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
>
>詳細については、[AEM のコンテンツフラグメントおよびエクスペリエンスフラグメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments)も参照してください。

## コンテンツフラグメントとコンテンツサービス {#content-fragments-and-content-services}

AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

配信は、JSON エクスポーターを使用して JSON 形式で行われます。

AEM コンテンツフラグメントを使用して構造化コンテンツを記述し、管理できます。構造化コンテンツは、様々なコンテンツタイプを含むことができるモデルで定義されます。テキスト、数値データ、ブーリアン、日付と時刻などが含まれます。

AEM コアコンポーネントの JSON 書き出し機能と共にこの構造化コンテンツを使用して、AEM コンテンツを AEM ページ以外のチャネルに配信できます。

>[!NOTE]
>
>AEM Sites as a Cloud Service 向けヘッドレス開発の概要については、[AEM Sites as a Cloud Service 向けヘッドレス開発](/help/headless/introduction.md)を参照してください。

>[!NOTE]
>
>AEM はフラグメントコンテンツの翻訳もサポートしています。詳しくは、「[アセットの翻訳](/help/assets/translate-assets.md)」を参照してください。

## コンテンツタイプ {#content-type}

コンテンツフラグメントとは、次のようなものです。

* **Assets** として格納されます。

   * コンテンツフラグメント（とバリエーション）は、**Assets** コンソールで作成および管理できます。
   * コンテンツフラグメントエディターでオーサリングおよび編集されます。

* [コンテンツフラグメントコンポーネント（参照コンポーネント）を介してページエディター内で](/help/sites-cloud/authoring/fragments/content-fragments.md)使用されます。

   * **コンテンツフラグメント**&#x200B;コンポーネントを使用できるのはページの作成者です。作成者は、コンテンツフラグメントコンポーネントを使用して、必要なコンテンツフラグメントを HTML または JSON 形式で参照し、配信できます。

* [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) を使用してアクセスできます。

コンテンツフラグメントは、次のようなコンテンツ構造です。

* レイアウトやデザインはありません（リッチテキストモードでは多少のテキストフォーマット設定が可能です）。
* 1 つ以上の[構成要素](#constituent-parts-of-a-content-fragment)を含みます。
* [画像を含めたり、関連付けたりする](#fragments-with-visual-assets)ことができます。
* ページで参照される際に、[中間コンテンツ](#in-between-content-when-page-authoring-with-content-fragments)に使用されます。
* 配信メカニズム（ページやチャネル）に依存しません。

### ビジュアルアセットを含むフラグメント {#fragments-with-visual-assets}

作成者がより柔軟にコンテンツをコントロールできるように、画像をコンテンツフラグメントに追加したり、コンテンツフラグメントと統合したりできます。

アセットとコンテンツフラグメントの組み合わせには、様々な使用法があります。どの方法にもそれぞれの利点があります。

* フラグメントに&#x200B;**アセットを挿入**（混在メディアフラグメント）

   * フラグメントの構成要素です（[コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)を参照してください）。
   * アセットの位置を定義します。
   * 詳しくは、フラグメントエディターでの[フラグメントへのアセットの挿入](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)を参照してください。

  >[!NOTE]
  >
  >コンテンツフラグメント自体に挿入したビジュアルアセットは、前の段落に添付されます。このコンテンツフラグメントをページに追加した場合、ビジュアルアセットは、中間コンテンツが追加されたタイミングで前の段落との関連で移動します。

* **関連コンテンツ**

   * フラグメントに接続されますが、フラグメントの固定構成要素ではありません（[コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)を参照してください）。
   * 位置決めにある程度の柔軟性があります。
   * ページでフラグメントを使用する際に、中間コンテンツのように手軽に利用できます。

  詳細については、[関連コンテンツ](/help/assets/content-fragments/content-fragments-assoc-content.md)を参照してください。

* ページエディターの **Assets ブラウザー**&#x200B;で利用できるアセット

   * アセットの選択には、完全な柔軟性があります。
   * 位置決めにある程度の柔軟性があります。
   * 特定のフラグメント向けに承認されるという概念は提供しません。

  詳細については、[Assets ブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)を参照してください。

### コンテンツフラグメントの構成要素 {#constituent-parts-of-a-content-fragment}

コンテンツフラグメントアセットは、（直接的または間接的に）次の構成要素からなります。

* **フラグメントの要素**

   * 要素は、コンテンツを含むデータフィールドと相関関係にあります。
   * コンテンツモデルを使用して、コンテンツフラグメントを作成します。モデルで指定された要素（フィールド）は、フラグメントの構造を定義します。このような要素（フィールド）には様々なデータタイプがあります。

* **フラグメントの段落**

   * 個々のエンティティとして区切られたテキストのブロック（多くの場合は複数行）。

   * [リッチテキスト](/help/assets/content-fragments/content-fragments-variations.md#rich-text)モードと[ Markdown ](/help/assets/content-fragments/content-fragments-variations.md#markdown)モードでは、段落をヘッダーとして書式設定することができます。その場合、ヘッダーとその後の段落が 1 つのユニットになります。

   * ページ作成中にコンテンツを制御できます。

* **フラグメントに挿入したアセット（混在メディアフラグメント）**

   * アセット（画像）が実際のフラグメントに挿入され、フラグメントの内部コンテンツとして使用されます。
   * フラグメントの段落システムに埋め込まれます。
   * [フラグメントをページ上で使用または参照](/help/sites-cloud/authoring/fragments/content-fragments.md)するときに書式設定できます。
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、フラグメントエディターのみで行えます。これらのアクションは、ページエディターでは行えません。
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、[フラグメントエディターのリッチテキスト形式](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)を使用してのみ行うことができます。
   * 複数行テキスト要素（任意のフラグメントタイプ）にのみ追加できます。
   * 前のテキスト（段落）に添付されます。

     >[!CAUTION]
     >
     >プレーンテキスト形式に切り替えると、アセットが（誤って）フラグメントから削除されるおそれがあります。

     >[!NOTE]
     >
     >ページでフラグメントを使用する場合は、アセットを追加の（中間）コンテンツとして追加することもできます。その場合は、[関連コンテンツ](/help/assets/content-fragments/content-fragments-assoc-content.md)、またはアセットブラウザー内のアセットを使用します。

* **関連コンテンツ**

   * これはフラグメント外部のコンテンツですが、編集に関連します。通常は、画像、ビデオ、または他のフラグメントです。
   * コレクション内の個々のアセットは、ページエディターでページにフラグメントを追加するときに、フラグメントと共に使用できます。つまり、コレクション内の個々のアセットは任意であり、特定のチャネルの要件に応じて使用します。
   * アセットは、[コレクションを介してフラグメントに関連付けられます](/help/assets/content-fragments/content-fragments-assoc-content.md)。関連付けられたコレクションを使用することで、作成者はページ作成時に使用するアセットを決定できます。

      * コレクションはフラグメントにデフォルトコンテンツとして関連付けることができます。または、フラグメントの作成時に作成者が関連付けることができます。
      * [アセット（DAM）コレクション](/help/assets/manage-collections.md)は、フラグメントの関連コンテンツの基礎です。
   * オプションで、トラッキングしやすいように、コレクションにフラグメント自体を追加することもできます。

* **フラグメントのメタデータ**

   * [アセットメタデータスキーマ](/help/assets/metadata-schemas.md)を使用します。
   * タグは、次のことを行うときに作成できます。

      * フラグメントを作成してオーサリングするとき。
      * または、その後、次の方法でも作成できます。

         * コンソールでフラグメントの&#x200B;**プロパティ**&#x200B;を表示または編集することによって。
         * フラグメントエディターで&#x200B;**メタデータ**&#x200B;を編集することによって。

  >[!CAUTION]
  >
  >メタデータ処理プロファイルは、コンテンツフラグメントには適用されません。

* **マスター**

   * フラグメントの一部

      * どのコンテンツフラグメントにもマスターインスタンスが 1 つあります。
      * マスターは削除できません。

   * マスターには、フラグメントエディターの「**[バリエーション](/help/assets/content-fragments/content-fragments-variations.md)**」の下でアクセスできます。
   * マスター自体はバリエーションではありませんが、すべてのバリエーションの基礎となります。

* **バリエーション**

   * 編集目的に特化したフラグメントテキストのレンディション。チャネルに関連付けることができますが、必須ではありません。アドホックなローカル変更の場合にも使用できます。
   * **マスター**&#x200B;のコピーとして作成しますが、必要に応じて編集できます。バリエーション自体の間にはコンテンツの重複があります。
   * フラグメントのオーサリング中に定義できます。
   * コンテンツコピーの分散を避けるために、フラグメントに格納されます。
   * マスター側のコンテンツが更新されている場合は、バリエーションをマスターと[同期](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)できます。
   * [要約](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)することで、あらかじめ定義した長さにテキストをすばやく切り詰めることができます。
   * フラグメントエディターの「[バリエーション](/help/assets/content-fragments/content-fragments-variations.md)」タブにあります。

### コンテンツフラグメントを使用したページのオーサリング時の中間コンテンツ {#in-between-content-when-page-authoring-with-content-fragments}

中間コンテンツの特徴は次のとおりです。

* コンテンツフラグメントを操作するときにページエディターで使用できます。
* ページ上で使用または参照された後、[フラグメントのフロー内に追加されるコンテンツ](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-in-between-content)。
* [コンテンツフラグメントを操作するときにページエディター](/help/sites-cloud/authoring/fragments/content-fragments.md)で使用できます。
* 中間コンテンツは、1 つの要素のみが表示される任意のフラグメントに追加できます。
* 該当するブラウザーで使用できるアセットやコンポーネントと同様に、関連コンテンツを使用できます。

>[!CAUTION]
>
>中間コンテンツは、ページコンテンツです。中間コンテンツはコンテンツフラグメントに保存されません。

### フラグメントを利用するための要件 {#required-by-fragments}

コンテンツフラグメントを作成するには、以下が必要です。

* **コンテンツモデル**

   * ](/help/assets/content-fragments/content-fragments-configuration-browser.md)設定ブラウザーを使用して有効化[されます。
   * [ツールを使用して作成](/help/assets/content-fragments/content-fragments-models.md)されます。
   * [フラグメントを作成](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments)するために必要です。
   * フラグメントの構造（タイトル、コンテンツ要素、タグ定義）を定義します。
   * コンテンツモデル定義にはタイトルと 1 つのデータ要素が必要です。その他すべてはオプションです。
   * モデルでは、デフォルトコンテンツを定義できます（該当する場合）。
   * 作成者は、フラグメントコンテンツのオーサリング時に、定義された構造を変更することはできません。
   * 依存コンテンツフラグメントの作成後にモデルに対して行った変更は、これらのコンテンツフラグメントに影響を与える可能性があります。

コンテンツフラグメントをページオーサリングに使用するには、次のものも必要です。

* **コンテンツフラグメントコンポーネント**

   * フラグメントを HTML 形式、JSON 形式、またはその両方で配信するのに役立ちます。
   * [ページ上でフラグメントを参照](/help/sites-cloud/authoring/fragments/content-fragments.md)するために必要です。
   * フラグメントのレイアウトと配信（チャネル）を行います。
   * フラグメントは、レイアウトを定義し、一部またはすべての要素／バリエーションと関連するコンテンツを配信するために、1 つ以上の専用コンポーネントを必要とします。
   * 作成時にフラグメントをページにドラッグすると、必須コンポーネントが自動的に関連付けられます。

## MSM でのコンテンツフラグメントの再利用 {#reusing-content-fragments-with-msm}

**Assets** コンソールからアクセスする場合、MSM を使用してフラグメントのライブコピーを作成できます。

詳しくは、次を参照してください。

* [MSM を使用したコンテンツフラグメントの再利用](/help/assets/content-fragments/content-fragments-msm.md)
* [MSM for Assets を使用したアセットの再利用](/help/assets/reuse-assets-using-msm.md)。

これらにより、フラグメントのバリエーションおよび個々のフィールドの両方に対する[継承](/help/assets/content-fragments/content-fragments-variations.md#inheritance)が有効になります。

>[!CAUTION]
>
>（コンテンツフラグメントのコピーを作成する）MSM を使用する場合は、それぞれの[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)で使用されているすべてのデータタイプから&#x200B;**一意**&#x200B;の制約を削除する必要があります。

## 使用例 {#example-usage}

フラグメントと、その要素およびバリエーションを一緒に使用すると、複数のチャネルに対応した一貫性のあるコンテンツを作成できます。フラグメントをデザインする際は、何をどこで使用するかを考慮します。

### WKND のサンプル {#wknd-sample}

AEM as a Cloud Service の習得に役立つ [WKND サイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)サンプルが用意されています。

WKND プロジェクトには、次のものが含まれます。

* 次の URL で入手できるコンテンツフラグメントモデル：
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

## ベストプラクティス {#best-practices}

コンテンツフラグメントを使用して、複雑な構造を形成できます。 Adobeは、モデルとフラグメントの両方を定義および使用する際のベストプラクティスに関する推奨事項を提供します。

### シンプルに {#keep-it-simple}

AEMで構造化コンテンツをモデリングする場合は、システムの強力なパフォーマンスと効率化されたガバナンスを確保するために、コンテンツ構造をできるだけシンプルにします。

### モデル数 {#number-of-models}

必要な数のコンテンツモデルを作成しますが、それ以上は作成しません。

モデルが多すぎると、ガバナンスが複雑になり、GraphQLのクエリの速度が低下する可能性があります。 通常、モデルの小さなセット（最大 10 分の 1）で十分です。 10 以上の高さに近づいた場合は、モデリング方法を再検討してください。

### モデルとフラグメントのネスト（非常に重要） {#nesting-models-and-fragments}

コンテンツフラグメント参照を使用してコンテンツフラグメントを深くネストしたり、過度にネストしたりしないでください。これにより、フラグメントは他のフラグメントを、場合によっては複数のレベルで参照できます。

コンテンツフラグメント参照を頻繁に使用すると、システムのパフォーマンス、UI の応答性およびGraphQLのクエリの実行に大きな影響を与える可能性があります。 10 レベル以下にネストを維持することを目指します。

### モデルあたりのデータ フィールドとタイプの数  {#number-of-data-fields-and-types-per-model}

モデルに本当に必要なデータフィールドとタイプのみを含めます。

モデルが過度に複雑になると、フラグメントが過度に複雑になり、オーサリングが困難になり、エディターのパフォーマンスが低下する可能性があります。

### リッチテキストフィールド {#rich-text-fields}

リッチテキストフィールド（**複数行テキスト** データタイプ）の使用を考慮する。

モデルあたりのリッチテキストフィールドの数を制限します。 また、各フラグメントに保存されるテキストの量とHTMLの書式設定の量も指定します。 非常に大きなリッチテキストコンテンツは、システムのパフォーマンスに悪影響を及ぼす可能性があります。

### バリエーション数 {#number-of-variations}

必要な数のフラグメントバリエーションを作成しますが、それ以上は作成しません。

バリエーションにより、オーサー環境と配信時に、コンテンツフラグメントに処理時間も追加されます。 バリエーションの数は管理可能な最小限に抑えることをお勧めします。

ベストプラクティスは、コンテンツフラグメントあたり 10 個のバリエーションを超えないようにすることです。

### 実稼動前のテスト {#test-before-production}

確信がない場合は、実稼動環境にロールアウトする前に、意図したコンテンツ構造のプロトタイプを作成します。 概念実証を早期に実施し、技術的な受け入れとユーザーによる受け入れの両方で適切なテストを実施することで、後で本番環境の期限に遭遇した場合の問題を回避できます。
