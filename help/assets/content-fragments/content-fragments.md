---
title: コンテンツフラグメントの操作
description: Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントで、（ヘッドレス配信に最適な）ページに依存しないコンテンツをデザイン、作成、キュレーションおよび使用する方法を説明します。
feature: コンテンツフラグメント
role: User
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 100%

---

# コンテンツフラグメントの操作 {#working-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service でコンテンツフラグメントを使用すると、[ページに依存しないコンテンツ](/help/sites-cloud/authoring/fundamentals/content-fragments.md)をデザイン、作成、キュレーションおよび公開できます。（ヘッドレス配信に最適な）複数の場所や複数のチャネルでの使用に対応したコンテンツを準備できます。

コンテンツフラグメントには、構造化されたコンテンツが含まれます。

* 作成されるフラグメントの構造を事前定義する[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)に基づいています。
* 構造の範囲は次のとおりです。
   * 基本
      * 例えば、1 つの複数行テキストフィールドなどです。
      * ページオーサリングで使用する単純なコンテンツを用意するのに使用できます。
   * 複合
      * テキスト、数値、ブール値、日時などの様々なデータタイプのフィールドを多数組み合わせたもの。
      * ページオーサリング用のより構造化されたコンテンツを用意するためや、アプリケーションに配信するために使用できます。
   * 入れ子
      * 使用可能な参照データ型を使用して、コンテンツをネストできます。
      * アプリケーションへの配信に使用される傾向があります。

コンテンツフラグメントは、AEM コアコンポーネントの Sling Model（JSON）書き出し機能を使用して、JSON 形式で配信することもできます。この形式の配信では次のことが可能です。

* コンポーネントを使用して、配信するフラグメントの要素を管理できます。
* API 配信に使用されるページで複数のコンテンツフラグメントコアコンポーネントを追加して、一括配信できます。

このページおよび以下のページでは、コンテンツフラグメントを作成、設定、維持管理および使用するためのタスクについて説明しています。

* [インスタンスに対するコンテンツフラグメント機能を有効化します。](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md) - モデルを有効化、作成および定義します。
* [コンテンツフラグメントの管理](/help/assets/content-fragments/content-fragments-managing.md) - コンテンツフラグメントを作成し、編集、公開、参照します。
* [バリエーション - フラグメントコンテンツのオーサリング](/help/assets/content-fragments/content-fragments-variations.md) - フラグメントコンテンツをオーサリングし、マスターのバリエーションを作成します。
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - フラグメントに Markdown 構文を使用します。
* [関連コンテンツの使用](/help/assets/content-fragments/content-fragments-assoc-content.md) - 関連コンテンツを追加します。
* [メタデータ - フラグメントのプロパティ](/help/assets/content-fragments/content-fragments-metadata.md) - フラグメントのプロパティを表示および編集します。
* [コンテンツフラグメントと GraphQL を併用してアプリケーション用コンテンツを配信](/help/assets/content-fragments/content-fragments-graphql.md)します。その一助として、[JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。

>[!NOTE]
>
>これらのページと併せて、次のページも参照してください。
>
>* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
>* [コンテンツフラグメントのカスタマイズと拡張](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [レンダリングコンポーネントのコンテンツフラグメントの設定](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API でのコンテンツフラグメントのサポート ](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)


通信チャネルの数は年々増加しています。通常、チャネルとは配信メカニズムのことであり、次のどちらも指します。

* 物理チャネル（デスクトップ、モバイルなど）
* 物理チャネルでの配信方法（デスクトップ用の「製品詳細ページ」や「製品カテゴリページ」、モバイル用の「モバイル Web」や「モバイルアプリ」など）

しかしながら、すべてのチャネルでのまったく同じコンテンツの使用はお勧めしません。特定のチャネルに合わせてコンテンツを最適化する必要があります。

コンテンツフラグメントを使用すると、次のことが可能になります。

* 複数のチャネルでいかにターゲットオーディエンスに効率よく伝えるかを考慮する。
* チャネルに依存しない編集コンテンツを作成、管理する
* 多様なチャネル向けのコンテンツプールを構築する。
* 特定のチャネル向けにコンテンツのバリエーションをデザインする。
* アセットを挿入することでテキストに画像を追加する（混在メディアフラグメント）
* データの複雑さを反映して、ネストされたコンテンツを作成します。

さらにこうしたコンテンツフラグメントを集めて組み立てることで、多様なチャネルにエクスペリエンスを提供できます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>* **コンテンツフラグメント**&#x200B;は編集コンテンツで、テキスト、数値、日付などの構造化されたデータにアクセスするのに使用できます。これらは、定義と構造を備えた純粋なコンテンツですが、視覚的なデザインやレイアウトは追加されていません。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、Web ページのフラグメントです。

エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
詳細については、](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments)AEM のコンテンツフラグメントおよびエクスペリエンスフラグメントについて[も参照してください。

## コンテンツフラグメントとコンテンツサービス {#content-fragments-and-content-services}

AEM コンテンツサービスは、Web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM Web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

配信は、JSON エクスポーターを使用して JSON 形式で行われます。

AEM コンテンツフラグメントを使用して構造化コンテンツを記述し、管理できます。構造化コンテンツは、テキスト、数値データ、ブール値、日付と時刻など、様々なコンテンツタイプを含めることができるモデルを使用して定義します。

AEM コアコンポーネントの JSON 書き出し機能と共にこの構造化コンテンツを使用して、AEM コンテンツを AEM ページ以外のチャネルに配信できます。

>[!NOTE]
>
>AEM Sites as a Cloud Service 向けヘッドレス開発の概要については、[AEM Sites as a Cloud Service 向けヘッドレス開発](/help/implementing/developing/headless/introduction.md)を参照してください。

>[!NOTE]
>
>AEM はフラグメントコンテンツの翻訳もサポートしています。

>[!NOTE]
>
>AEM はフラグメントコンテンツの翻訳もサポートしています。詳しくは、「[アセットの翻訳](/help/assets/translate-assets.md)」を参照してください。

## コンテンツタイプ {#content-type}

コンテンツフラグメントとは、次のようなものです。

* **Assets** として格納されます。

   * コンテンツフラグメント（とバリエーション）は、**Assets** コンソールで作成および管理できます。
   * コンテンツフラグメントエディターでオーサリングおよび編集されます。

* [コンテンツフラグメントコンポーネント（参照コンポーネント）を介してページエディター内で](/help/sites-cloud/authoring/fundamentals/content-fragments.md)使用されます。

   * **コンテンツフラグメント**&#x200B;コンポーネントを使用できるのはページの作成者です。作成者は、コンテンツフラグメントコンポーネントを使用して、必要なコンテンツフラグメントを HTML または JSON 形式で参照し、配信できます。

* [AEM GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) を使用してアクセスできます。

コンテンツフラグメントは、次のようなコンテンツ構造です。

* レイアウトやデザインを伴いません（リッチテキストモードでは多少のテキストの書式設定が可能です）。
* 1 つ以上の[構成要素](#constituent-parts-of-a-content-fragment)を含みます。
* [画像を含めたり、関連付けたりする](#fragments-with-visual-assets)ことができます。
* ページで参照される場合、[中間コンテンツ](#in-between-content-when-page-authoring-with-content-fragments)を使用できます。

* 配信メカニズム（ページやチャネル）に依存しません。

### ビジュアルアセットを含むフラグメント {#fragments-with-visual-assets}

作成者がより柔軟にコンテンツをコントロールできるように、画像をコンテンツフラグメントに追加したり、コンテンツフラグメントと統合したりできます。

アセットとコンテンツフラグメントの組み合わせには、様々な使用法があります。どの方法にもそれぞれの利点があります。

* フラグメントに&#x200B;**アセットを挿入**（混在メディアフラグメント）

   * フラグメントの不可欠な構成要素です（[コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)を参照してください）。
   * アセットの位置を定義します。
   * 詳しくは、フラグメントエディターでの[フラグメントへのアセットの挿入](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)を参照してください。

   >[!NOTE]
   >
   >コンテンツフラグメント自体に挿入したビジュアルアセットは、前の段落に添付されます。このコンテンツフラグメントをページに追加した場合、ビジュアルアセットは、中間コンテンツが追加されたタイミングで前の段落との関連で移動します。

* **関連コンテンツ**

   * フラグメントに接続されます。ただし、フラグメントの固定構成要素ではありません（[コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)を参照してください）。
   * 位置決めには、ある程度の柔軟性があります。
   * ページでフラグメントを使用する場合に、（中間コンテンツのように）手軽に利用できます。
   * 詳細については、[関連コンテンツ](/help/assets/content-fragments/content-fragments-assoc-content.md)を参照してください。

* ページエディターの **Assets ブラウザー**&#x200B;で利用できるアセット

   * アセットの選択には、完全な柔軟性があります。
   * 位置決めには、ある程度の柔軟性があります。
   * 特定のフラグメント向けに承認されるという概念は提供しません。
   * 詳細については、[Assets ブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)を参照してください。

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
   * [フラグメントをページ上で使用または参照](/help/sites-cloud/authoring/fundamentals/content-fragments.md)するときに書式設定できます。
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、フラグメントエディターのみで行えます。これらのアクションは、ページエディターでは行えません。
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、[フラグメントエディターのみで、リッチテキストフォーマットを使用して](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)行えます。
   * 複数行テキスト要素（任意のフラグメントタイプ）にのみ追加できます。
   * 前のテキスト（段落）に添付されます。

      >[!CAUTION]
      >
      >プレーンテキスト形式に切り替えると、アセットが（誤って）フラグメントから削除されるおそれがあります。

      >[!NOTE]
      >
      >ページでフラグメントを使用する場合は、アセットを[追加の（中間）コンテンツ](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)として追加することもできます。その場合は、関連コンテンツ、または Assets ブラウザー内のアセットを使用します。

* **関連コンテンツ**

   * これはフラグメント外部のコンテンツですが、編集に関連します。通常は、画像、ビデオ、または他のフラグメントです。
   * コレクション内の個々のアセットは、ページエディターでページにフラグメントを追加するときに、フラグメントと共に使用できます。つまり、コレクション内の個々のアセットは任意であり、特定のチャネルの要件に応じて使用します。
   * アセットは、[コレクションを介してフラグメントに関連付け](/help/assets/content-fragments/content-fragments-assoc-content.md)ます。関連付けられたコレクションを使用することで、作成者は、ページ作成時に使用するアセットを決定できます。

      * コレクションはフラグメントにデフォルトコンテンツとして関連付けることができます。または、フラグメントの作成時に作成者が関連付けることができます。
      * [Assets（DAM）コレクション](/help/assets/manage-collections.md)は、フラグメントの関連コンテンツの基礎です。
   * オプションで、追跡しやすいように、コレクションにフラグメント自体を追加することもできます。

* **フラグメントのメタデータ**

   * [アセットメタデータスキーマ](/help/assets/metadata-schemas.md)を使用します。
   * タグは、次のことを行うときに作成できます。

      * フラグメントを作成してオーサリングするとき
      * または、その後、次の方法でも作成できます。

         * コンソールでフラグメントの&#x200B;**プロパティ**&#x200B;を表示または編集することによって
         * フラグメントエディターで&#x200B;**メタデータ**&#x200B;を編集することによって

   >[!CAUTION]
   >
   >メタデータ処理プロファイルは、コンテンツフラグメントには適用されません。

* **マスター**

   * フラグメントの不可欠な構成要素。

      * どのコンテンツフラグメントにもマスターインスタンスが 1 つあります。
      * マスターは削除できません。
   * マスターには、フラグメントエディターの「**[バリエーション](/help/assets/content-fragments/content-fragments-variations.md)**」の下でアクセスできます。
   * マスター自体はバリエーションではありませんが、すべてのバリエーションの基礎となります。


* **バリエーション**

   * 編集目的に合わせたフラグメントテキストのレンディション。チャネルに関連付けることができますが必須ではありません。ローカルで臨時に変更する場合にも使用できます。
   * **マスター**&#x200B;のコピーとして作成しますが、その後、必要に応じて編集できます。通常、バリエーション同士にはコンテンツの重複があります。
   * フラグメントのオーサリング中に定義できます。
   * コンテンツコピーの分散を避けるために、フラグメントに格納されます。
   * マスター側のコンテンツが更新されている場合は、バリエーションをマスターと[同期](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master)することができます。
   * [要約](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text)することで、あらかじめ定義した長さにテキストをすばやく切り詰めることができます。
   * フラグメントエディターの「[バリエーション](/help/assets/content-fragments/content-fragments-variations.md)」タブにあります。

### コンテンツフラグメントを使用したページのオーサリング時の中間コンテンツ {#in-between-content-when-page-authoring-with-content-fragments}

中間コンテンツの特徴は次のとおりです。

* コンテンツフラグメントを操作するときにページエディターで使用できます。
* ページ上で使用または参照されたことのある[フラグメントのフローの中に追加する、追加のコンテンツです。](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content)
* [コンテンツフラグメントを操作するときにページエディター](/help/sites-cloud/authoring/fundamentals/content-fragments.md)で使用できます。
* 中間コンテンツは、1 つの要素のみが表示される任意のフラグメントに追加できます。
* 該当するブラウザーで使用できるアセットやコンポーネントと同様に、関連コンテンツを使用できます。

>[!CAUTION]
>
>中間コンテンツは、ページコンテンツです。中間コンテンツはコンテンツフラグメントに保存されません。

### フラグメントを利用するための要件 {#required-by-fragments}

コンテンツフラグメントを作成するには、次のものが必要です。

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

   * フラグメントを HTML 形式や JSON 形式で配信するのに役立ちます。
   * [ページ上でフラグメントを参照](/help/sites-cloud/authoring/fundamentals/content-fragments.md)するために必要です。
   * フラグメントのレイアウトと配信（チャネル）に対応します。
   * フラグメントは、レイアウトを定義し、一部またはすべての要素／バリエーションと関連するコンテンツを配信するために、1 つ以上の専用コンポーネントを必要とします。
   * 作成時にフラグメントをページにドラッグすると、必須コンポーネントが自動的に関連付けられます。

## 使用例 {#example-usage}

フラグメントと、その要素およびバリエーションを一緒に使用して、複数のチャネルに対応する明解なコンテンツを作成できます。フラグメントを設計するときは、何をどこで使用するかを考慮する必要があります。

### WKND サンプル {#wknd-sample}

AEM as a Cloud Service の習得に役立つ [WKND サイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)サンプルが用意されています。

WKND プロジェクトには、次のものが含まれます。

* 次の URL で入手できるコンテンツフラグメントモデル：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
