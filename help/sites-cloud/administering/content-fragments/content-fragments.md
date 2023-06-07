---
title: コンテンツフラグメントの使用方法
description: Adobe Experience Manager（AEM）as a Cloud Service のコンテンツフラグメントで、ページオーサリングやヘッドレス配信に最適な、ページに依存しないコンテンツをデザイン、作成、キュレーションおよび使用する方法を説明します。
feature: Content Fragments
role: User
exl-id: d12b1dda-85ce-4665-b8b1-915b74231bb8
source-git-commit: e99522cb6221285b5b4de5f026dcc4d925035ec1
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 65%

---

# コンテンツフラグメントの操作 {#working-with-content-fragments}

Adobe Experience Manager（AEM）as a Cloud Service でコンテンツフラグメントを使用すると、[ページに依存しないコンテンツ](/help/sites-cloud/authoring/fundamentals/content-fragments.md)をデザイン、作成、キュレーションおよび公開できます。ページオーサリングやヘッドレス配信に最適な、複数の場所や複数のチャネルでの使用に対応したコンテンツを準備できます。

コンテンツフラグメントには、構造化されたコンテンツが含まれます。

* 作成されるフラグメントの構造を事前定義する[コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)に基づいています。
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

コンテンツフラグメントは、AEMコアコンポーネントの Sling Model(JSON) 書き出し機能を使用して、JSON 形式で配信することもできます。 この形式の配信：

* を使用すると、コンポーネントを使用して、フラグメントの配信する要素を管理できます
* API 配信に使用するページに複数のコンテンツフラグメントコアコンポーネントを追加して一括配信を許可します。

このページと後続のページでは、コンテンツフラグメントを作成、設定、維持管理および使用するためのタスクについて説明しています。

* [インスタンスに対するコンテンツフラグメント機能を有効化します。](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) - モデルを有効化、作成および定義します。
* [コンテンツフラグメントコンソールの使用](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) - フラグメントにアクセス、作成、編集、公開、参照します。
* [コンテンツフラグメントの管理](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md) - コンテンツフラグメントを作成し、編集、公開、参照します。
* [バリエーション - フラグメントコンテンツのオーサリング](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) - フラグメントコンテンツをオーサリングし、マスターのバリエーションを作成します。
* [Markdown](/help/sites-cloud/administering/content-fragments/content-fragments-markdown.md) - フラグメントに Markdown 構文を使用します。
* [関連コンテンツの使用](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) - 関連コンテンツを追加します。
* [メタデータ - フラグメントのプロパティ](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md) - フラグメントのプロパティを表示および編集します。
* コンテンツフラグメントを使用する：

   * [ページオーサリング用](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
   * [GraphQL と組み合わせて、アプリケーションへのヘッドレス配信を実現します](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md)。
これに役立つように、[構造ツリー](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)と [JSON 出力](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)をプレビューできます。

>[!NOTE]
>
>これらのページと併せて、次のページも参照してください。
>
>* [コンテンツフラグメントを使用したページのオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
>* [コンテンツフラグメントのカスタマイズと拡張](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [レンダリングコンポーネントのコンテンツフラグメントの設定](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [AEM Assets HTTP API でのコンテンツフラグメントのサポート](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [コンテンツフラグメントと共に使用する AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
>* [MSM for Assets を使用したコンテンツフラグメントの再利用](/help/assets/reuse-assets-using-msm.md) ( **Assets** コンソール )


通信チャネルの数は年々増加しています。通常、チャネルとは配信メカニズムのことであり、次のどちらも指します。

* 物理チャネル：例えば、デスクトップ、モバイルなど。
* 物理チャネルでの配信形式：デスクトップ用の「製品詳細ページ」や「製品カテゴリーページ」、モバイル用の「モバイル web」や「モバイルアプリ」など。

ただし、すべてのチャネルで同じコンテンツを使用するのは（おそらく）望ましくないでしょう。特定のチャネルに従ってコンテンツを最適化する必要があります。

コンテンツフラグメントを使用すると、次のことができます。

* 複数のチャネルをまたいで、ターゲットオーディエンスに効率的にリーチする方法を検討します。
* チャネルに依存しない編集コンテンツを作成および管理します。
* 様々なチャネル用のコンテンツプールを構築します。
* 特定のチャネル用にコンテンツのバリエーションをデザインする。
* アセット（混在メディアフラグメント）を挿入して、テキストに画像を追加します。
* データの複雑さを反映して、ネストされたコンテンツを作成する。

さらにこうしたコンテンツフラグメントを集めて組み立てることで、多様なチャネルにエクスペリエンスを提供できます。

>[!NOTE]
>
>**コンテンツフラグメント**&#x200B;と&#x200B;**[エクスペリエンスフラグメント](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**&#x200B;は、AEM 内の異なる機能です。
>* **コンテンツフラグメント**&#x200B;は、定義と構造を備えたエディトリアルコンテンツですが、視覚的なデザインやレイアウトは追加されていません。コンテンツフラグメントを使用すれば、テキスト、数値、日付などの構造化データにアクセスできます。
>* **エクスペリエンスフラグメント**&#x200B;は完全にレイアウトされたコンテンツであり、web ページのフラグメントです。
>
>エクスペリエンスフラグメントには、コンテンツフラグメントの形式でコンテンツを含めることができますが、その逆はできません。
>
>さらなる情報については、[AEM のコンテンツフラグメントとエクスペリエンスフラグメントについて](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=ja#content-fragments)も参照してください。

## コンテンツフラグメントとコンテンツサービス {#content-fragments-and-content-services}

AEM Content Services は、AEMでのコンテンツの説明と配信を、Web ページに焦点を当てるだけでなく、一般化するように設計されています。

従来のAEM Web ページではないチャネルに対して、あらゆるクライアントが利用できる標準化された方法を使用してコンテンツを配信します。 次のチャネルが含まれます。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

配信は、JSON エクスポーターを使用して JSON 形式で行われます。

AEMコンテンツフラグメントを使用して、構造化コンテンツを説明し、管理できます。 構造化コンテンツは、様々なコンテンツタイプを含むことができるモデルで定義されます。テキスト、数値データ、ブール値、日付と時刻などを含みます。

AEM コアコンポーネントの JSON 書き出し機能と共にこの構造化コンテンツを使用して、AEM コンテンツを AEM ページ以外のチャネルに配信できます。

>[!NOTE]
>
>AEM Sites as a Cloud Service 向けヘッドレス開発の概要については、[AEM Sites as a Cloud Service 向けヘッドレス開発](/help/headless/introduction.md)を参照してください。

>[!NOTE]
>
>AEM はフラグメントコンテンツの翻訳もサポートしています。詳しくは、「[アセットの翻訳](/help/assets/translate-assets.md)」を参照してください。

## 公開とプレビュー {#publish-and-preview}

すべてのコンテンツと同様に、最終的には、コンテンツフラグメントをに公開します。 **[パブリッシュサービス](/help/overview/architecture.md#runtime-architecture)**.

それ以前に、コンテンツフラグメントを使用して配信されたエクスペリエンスをプレビューすることもできます。それには、 [コンテンツフラグメントの公開](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md##publishing-and-previewing-a-fragment) AEM **[プレビューサービス](/help/overview/architecture.md#runtime-architecture)**.

>[!CAUTION]
>
>への公開 **プレビューサービス** は、 **コンテンツフラグメント** コンソール。

## コンテンツタイプ {#content-type}

コンテンツフラグメントは次のとおりです。

* **Sites** 機能。

* **Assets** として格納されます。

   * コンテンツフラグメント（とそのバリエーション）は、 **コンテンツフラグメント**&#x200B;コンソールと **Assets** コンソールの両方で作成および管理できます。
   * コンテンツフラグメントエディターでオーサリングおよび編集されます。

* [コンテンツフラグメントコンポーネント（参照コンポーネント）を介してページエディター内で](/help/sites-cloud/authoring/fundamentals/content-fragments.md)使用されます。

   * **コンテンツフラグメント**&#x200B;コンポーネントを使用できるのはページの作成者です。作成者は、コンテンツフラグメントコンポーネントを使用して、必要なコンテンツフラグメントを HTML または JSON 形式で参照し、配信できます。

* [AEM GraphQL API](/help/headless/graphql-api/content-fragments.md) を使用してアクセスできます。

コンテンツフラグメントは、次のようなコンテンツ構造です。

* レイアウトやデザインがありません（リッチテキストモードでは、一部のテキスト書式が可能です）。
* 1 つ以上の [構成部品](#constituent-parts-of-a-content-fragment).
* 可能 [画像を含む、または、画像に接続する](#fragments-with-visual-assets).
* ページで参照される場合、[中間コンテンツ](#in-between-content-when-page-authoring-with-content-fragments)を使用できます。

* 配信メカニズム（ページやチャネル）に依存しません。

### ビジュアルアセットを含むフラグメント {#fragments-with-visual-assets}

作成者がより柔軟にコンテンツをコントロールできるように、画像をコンテンツフラグメントに追加したり、コンテンツフラグメントと統合したりできます。

アセットとコンテンツフラグメントの組み合わせには、様々な使用法があります。どの方法にもそれぞれの利点があります。

* フラグメントに&#x200B;**アセットを挿入**（混在メディアフラグメント）

   * フラグメントの不可欠な部分です ( [コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)) をクリックします。
   * アセットの位置を定義します。
   * 詳しくは、 [フラグメントへのアセットの挿入](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) （フラグメントエディター）を参照してください。

   >[!NOTE]
   >
   >コンテンツフラグメント自体に挿入したビジュアルアセットは、前の段落に添付されます。このコンテンツフラグメントをページに追加した場合、ビジュアルアセットは、中間コンテンツが追加されたタイミングで前の段落との関連で移動します。

* **関連コンテンツ**

   * フラグメントに接続されている。ただし、フラグメントの固定部分ではありません ( [コンテンツフラグメントの構成要素](#constituent-parts-of-a-content-fragment)) をクリックします。
   * 位置決めを柔軟に行えます。
   * ページでフラグメントを使用する際に、（中間コンテンツのように）簡単に使用できます。
   * 詳しくは、 [関連コンテンツ](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) を参照してください。

* ページエディターの **Assets ブラウザー**&#x200B;で利用できるアセット

   * アセットを最大限に柔軟に選択できます。
   * 位置決めを柔軟に行えます。
   * 特定のフラグメントに対して承認されるという概念を提供しません。
   * 詳細については、[Assets ブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser)を参照してください。

### コンテンツフラグメントの構成要素 {#constituent-parts-of-a-content-fragment}

コンテンツフラグメントアセットは、次の部分（直接または間接的）で構成されます。

* **フラグメント要素**

   * 要素は、コンテンツを保持するデータフィールドに関連付けられます。
   * コンテンツモデルを使用して、コンテンツフラグメントを作成します。モデルで指定された要素（フィールド）は、フラグメントの構造を定義します。 これらの要素（フィールド）は、様々なデータタイプに対応しています。

* **フラグメントの段落**

   * 個々のエンティティとして区切られたテキストのブロック（多くの場合は複数行）。

   * [リッチテキスト](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#rich-text)モードと[ Markdown ](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#markdown)モードでは、段落をヘッダーとして書式設定することができます。その場合、ヘッダーとその後の段落が 1 つのユニットになります。

   * ページオーサリング中にコンテンツを制御できるようにします。

* **フラグメントに挿入されたアセット（混在メディアフラグメント）**

   * アセット（画像）が実際のフラグメントに挿入され、フラグメントの内部コンテンツとして使用されます。
   * フラグメントの段落システムに埋め込まれます。
   * 書式設定は [フラグメントはページで使用または参照されます](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、フラグメントエディターのみで行えます。これらのアクションは、ページエディターでは行えません。
   * フラグメントへの追加、フラグメントからの削除、フラグメント内での移動は、[フラグメントエディターのみで、リッチテキストフォーマットを使用して](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)行えます。
   * 複数行テキスト要素（任意のフラグメントタイプ）にのみ追加できます。
   * 前のテキスト（段落）に添付されます。

      >[!CAUTION]
      >
      >プレーンテキスト形式に切り替えると、アセットが（誤って）フラグメントから削除されるおそれがあります。

      >[!NOTE]
      >
      >ページでフラグメントを使用する場合は、アセットを[追加の（中間）コンテンツ](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content)として追加することもできます。その場合は、関連コンテンツ、または Assets ブラウザー内のアセットを使用します。

* **関連コンテンツ**

   * これはフラグメントの外部のコンテンツですが、編集上の関連性を持ちます。 通常、画像、ビデオまたはその他のフラグメントです。
   * コレクション内の個々のアセットをページに追加する際に、ページエディターでフラグメントと共に使用できます。 つまり、特定のチャネルの要件に応じて、これらはオプションです。
   * アセットは、[コレクションを介してフラグメントに関連付け](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md)ます。関連付けられたコレクションを使用することで、作成者は、ページ作成時に使用するアセットを決定できます。

      * コレクションはフラグメントにデフォルトコンテンツとして関連付けることができます。または、フラグメントの作成時に作成者が関連付けることができます。
      * [アセット (DAM) コレクション](/help/assets/manage-collections.md) は、フラグメントの関連コンテンツの基礎です。
   * オプションで、フラグメント自体をコレクションに追加して、追跡を容易にすることもできます。

* **フラグメントメタデータ**

   * 以下を使用： [アセットのメタデータスキーマ](/help/assets/metadata-schemas.md).
   * タグは、次のことを行うときに作成できます。

      * フラグメントの作成とオーサリング
      * 以降：

         * フラグメントを表示または編集する **プロパティ** コンソールから
         * を編集する **メタデータ** フラグメントエディターで

   >[!CAUTION]
   >
   >メタデータ処理プロファイルは、コンテンツフラグメントには適用されません。

* **マスター**

   * フラグメントの整数部

      * すべてのコンテンツフラグメントには 1 つのマスターのインスタンスがあります。
      * マスターは削除できません。
   * マスターには、フラグメントエディターの「**[バリエーション](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)**」の下でアクセスできます。
   * マスター自体はバリエーションではありませんが、すべてのバリエーションの基礎となります。


* **バリエーション**

   * 編集目的に固有のフラグメントテキストのレンディション。チャネルに関連付けることができますが、必須ではありません。アドホックなローカル変更の場合にも使用できます。
   * **マスター**&#x200B;のコピーとして作成しますが、その後、必要に応じて編集できます。通常、バリエーション同士にはコンテンツの重複があります。
   * フラグメントのオーサリング中に定義できます。
   * コンテンツコピーの分散を避けるために、フラグメントに保存します。
   * バリエーションは [同期済み](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#synchronizing-with-master) マスター(マスターコンテンツが更新された場合 )
   * [要約](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#summarizing-text)することで、あらかじめ定義した長さにテキストをすばやく切り詰めることができます。
   * フラグメントエディターの「[バリエーション](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)」タブにあります。

### コンテンツフラグメントを使用したページのオーサリング時の中間コンテンツ {#in-between-content-when-page-authoring-with-content-fragments}

中間コンテンツの特徴は次のとおりです。

* コンテンツフラグメントを操作するときにページエディターで使用できます。
* ページ上で使用または参照されたことのある[フラグメントのフローの中に追加する、追加のコンテンツです。](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content)
* [コンテンツフラグメントを操作するときにページエディター](/help/sites-cloud/authoring/fundamentals/content-fragments.md)で使用できます。
* 中間コンテンツは、1 つの要素のみが表示される任意のフラグメントに追加できます。
* 関連するコンテンツは、アセットやコンポーネントと同様に、適切なブラウザーから使用できます。

>[!CAUTION]
>
>中間コンテンツはページコンテンツです。コンテンツフラグメントには保存されません。

### フラグメントを利用するための要件 {#required-by-fragments}

コンテンツフラグメントを作成するには、次のものが必要です。

* **コンテンツモデル**

   * ](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md)設定ブラウザーを使用して有効化[されます。
   * [ツールを使用して作成](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)されます。
   * [フラグメントを作成](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-content-fragments)するために必要です。
   * フラグメントの構造（タイトル、コンテンツ要素、タグ定義）を定義します。
   * コンテンツモデル定義にはタイトルと 1 つのデータ要素が必要です。その他すべてはオプションです。
   * モデルでは、デフォルトコンテンツを定義できます（該当する場合）。
   * 作成者は、フラグメントコンテンツのオーサリング時に、定義された構造を変更することはできません。
   * 依存コンテンツフラグメントの作成後にモデルに対して行った変更は、これらのコンテンツフラグメントに影響を与える可能性があります。

コンテンツフラグメントをページオーサリングに使用するには、次のものも必要です。

* **コンテンツフラグメントコンポーネント**

   * フラグメントをHTMLや JSON 形式で配信するのに便利です。
   * 必須 [ページ上でフラグメントを参照する](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * フラグメントのレイアウトと配信（チャネル）に対応します。
   * フラグメントは、レイアウトを定義し、一部またはすべての要素／バリエーションと関連するコンテンツを配信するために、1 つ以上の専用コンポーネントを必要とします。
   * 作成時にフラグメントをページにドラッグすると、必須コンポーネントが自動的に関連付けられます。

## 使用例 {#example-usage}

フラグメントと、その要素およびバリエーションを一緒に使用して、複数のチャネルに対応した一貫性のあるコンテンツを作成できます。フラグメントを設計するときは、何をどこで使用するかを考慮する必要があります。

### WKND サンプル {#wknd-sample}

AEM as a Cloud Service の習得に役立つ [WKND サイト](/help/implementing/developing/introduction/develop-wknd-tutorial.md)サンプルが用意されています。

WKND プロジェクトには、次のものが含まれます。

* 次の URL で入手できるコンテンツフラグメントモデル：
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* 次の URL で入手できるコンテンツフラグメント（およびその他のコンテンツ）：
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
