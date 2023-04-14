---
title: コンテンツフラグメントの管理
description: コンテンツフラグメントコンソールを使用して、（ページオーサリング用、またはヘッドレスコンテンツの基礎として）AEM コンテンツフラグメントを管理する方法を説明します。
feature: Content Fragments
role: User
exl-id: fc4497cb-85ac-4d2d-aca4-588541266f0b
source-git-commit: b351582a405f5c419f3aa386faddccd6ecef3a43
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 83%

---

# コンテンツフラグメントの管理 {#managing-content-fragments}

**コンテンツフラグメント**&#x200B;コンソールを使用して AEM コンテンツフラグメントを管理する方法を説明します。これらは、ページオーサリングやヘッドレスコンテンツの基礎として使用できます。

[コンテンツフラグメントモデル](#creating-a-content-model)を定義した後、それらを使用して[コンテンツフラグメントを作成](#creating-a-content-fragment)できます。

[コンテンツフラグメントエディター](#opening-the-fragment-editor)には、次の操作を行うための様々な[モード](#modes-in-the-content-fragment-editor)が用意されています。

* [コンテンツの編集](#editing-the-content-of-your-fragment)と[バリエーションの管理](#creating-and-managing-variations-within-your-fragment)
* [フラグメントへの注釈の付加](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [コンテンツとフラグメントの関連付け](#associating-content-with-your-fragment)
* [メタデータの設定](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [構造ツリーの表示](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [JSON 表現のプレビュー](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>コンテンツフラグメントは次に使用できます。
>
>* ページのオーサリング時 -「[コンテンツフラグメントを使用したページオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)」を参照してください。
>* [GraphQL でコンテンツフラグメントを使用するヘッドレスコンテンツ配信用。](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md)


>[!NOTE]
>
>コンテンツフラグメントは&#x200B;**アセット**&#x200B;として保存されます。これらは主に&#x200B;**コンテンツフラグメント**&#x200B;コンソールから管理しますが、**Assets** コンソールからも管理できます。

## コンテンツフラグメントコンソール {#content-fragments-console}

コンテンツフラグメントコンソールを使用すると、フラグメントおよび関連タスクに直接アクセスできます。 詳しくは、以下を参照してください。

* [コンテンツフラグメントコンソールの基本構造と処理](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#basic-structure-handling-content-fragments-console)

* [コンテンツフラグメントに関して提供される情報](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments)

* [コンテンツフラグメントコンソールでのコンテンツフラグメントのアクション](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment)

* [コンテンツフラグメントコンソールで使用可能な列のカスタマイズ](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#select-available-columns)

* [コンテンツフラグメントコンソールでの検索とフィルタリング](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#filtering-fragments)

## コンテンツフラグメントの作成 {#creating-content-fragments}

### コンテンツモデルの作成 {#creating-a-content-model}

構造化コンテンツを含むコンテンツフラグメントを作成する前に、[コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)を有効にして作成できます。

### コンテンツフラグメントの作成 {#creating-a-content-fragment}

コンテンツフラグメントを作成するには：

1. **コンテンツフラグメント**&#x200B;コンソールから、「**作成**」（右上）を選択します。

   >[!NOTE]
   >
   >新しいフラグメントの場所を事前に定義するには、フラグメントを作成するフォルダーに移動するか、作成プロセス中に場所を指定します。

1. **新しいコンテンツフラグメント**&#x200B;ダイアログが開き、ここから次の項目を指定できます。

   * **場所** - 現在の場所がオートコンプリートされますが、必要に応じて別の場所を選択できます
   * **コンテンツフラグメントモデル** - ドロップダウンリストからフラグメントの基礎として使用するモデルを選択します
   * **タイトル**
   * **名前** - **タイトル**&#x200B;に基づいてオートコンプリートされますが、必要に応じて編集できます
   * **説明**

   ![新しいコンテンツフラグメントダイアログ](assets/cfm-managing-new-cf-01.png)

1. 「**作成**」または「**作成して開く**」を選択して、定義を保持します。

## コンテンツフラグメントのステータス {#statuses-content-fragments}

[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)に表示されるように、コンテンツフラグメントは、存在中、複数のステータスを持つことができます。

* **新規**
新しいコンテンツフラグメントが作成されましたが、コンテンツフラグメントエディターで編集したり、開いたりしていません。
* **ドラフト**
誰かがコンテンツフラグメントエディターで（新しい）コンテンツフラグメントを編集または開きましたが、まだ公開されていません。
* **公開済み**
コンテンツフラグメントが公開されています。
* **変更済み**
コンテンツフラグメントが公開後（ただし、変更を公開する前）に編集されています。
* **非公開**
コンテンツフラグメントが公開されていません。

## フラグメントエディターを開く {#opening-the-fragment-editor}

編集するためにフラグメントを開くには：

>[!CAUTION]
>
>コンテンツフラグメントを編集するには、 [適切な権限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 問題が発生している場合は、システム管理者に問い合わせてください。

1. **コンテンツフラグメント**&#x200B;コンソールを使用して、コンテンツフラグメントの場所に移動します。
1. フラグメントを選択して編集するためにフラグメントを開き、ツールバーから「**開く**」を選択します。

1. フラグメントエディターが開きます。必要に応じて変更を加えます。

   ![フラグメントエディター](assets/cfm-managing-03.png)

1. 変更を加えた後、必要に応じて「**保存**」、「**保存して閉じる**」、「**閉じる**」のいずれかを使用します。

   >[!NOTE]
   >
   >「**保存して閉じる**」は、**保存**&#x200B;ドロップダウンからアクセスできます。

   >[!NOTE]
   >
   >「**保存して閉じる**」と「**閉じる**」のどちらをクリックした場合も、エディターが終了します。様々なオプションがコンテンツフラグメントにどのように動作するかについて詳しくは、[保存、閉じる、バージョン](#save-close-and-versions)を参照してください。

## コンテンツフラグメントエディターのモードとアクション {#modes-actions-content-fragment-editor}

コンテンツフラグメントエディターからは、様々なモードとアクションを使用できます。

### コンテンツフラグメントエディターのモード {#modes-in-the-content-fragment-editor}

サイドパネルのアイコンを使用して、様々なモード間を移動できます。

* バリエーション：[コンテンツの編集](#editing-the-content-of-your-fragment)と[バリエーションの管理](#creating-and-managing-variations-within-your-fragment)

* [注釈](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [関連コンテンツ](#associating-content-with-your-fragment)
* [メタデータ](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [構造ツリー](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [プレビュー](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)

![モード](assets/cfm-managing-04.png)

### コンテンツフラグメントエディターのツールバーアクション {#toolbar-actions-in-the-content-fragment-editor}

上部のツールバーには、複数のモードから使用できる機能があります。

![モード](assets/cfm-managing-top-toolbar.png)

* フラグメントがコンテンツページで既に参照されている場合は、メッセージが表示されます。このメッセージは&#x200B;**閉じる**&#x200B;ことができます。

* **サイドパネルを切り替え**&#x200B;アイコンを使用してサイドパネルを非表示／表示できます。

* フラグメント名の下に、現在のフラグメントの作成に使用された[コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)の名前が表示されます。

   * また、この名前はモデルエディターを開くリンクでもあります。

* 例えば、フラグメントの作成、変更、公開の日時については、フラグメントのステータスを参照してください。また、ステータスは次のように色分けもされています。

   * **新規**：灰色
   * **ドラフト**：青
   * **公開済み**：緑
   * **変更**：オレンジ
   * **アクティベートを解除済み**：赤

* 「**保存**」から、「**保存して閉じる**」オプションにアクセスできます。

* 3 つのドット（**...**）ドロップダウンから、以下の追加アクションにアクセスできます。
   * **ページ参照を更新**
      * すべてのページ参照が更新されます。
   * **[クイック公開](#publishing-and-referencing-a-fragment)**
   * **[公開を管理](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 保存、閉じる、バージョン {#save-close-and-versions}

>[!NOTE]
>
>バージョン[を作成／比較したり元に戻したりする操作は、タイムラインから](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)も行えます。

エディターには、次のような様々なオプションがあります。

* 「**保存**」と「**保存して閉じる**」

   * 「**保存**」を選択すると、最新の変更が保存され、その後もエディターは開いたままです。
   * 「**保存して閉じる**」を選択すると、最新の変更が保存された後、エディターが終了します。

   >[!CAUTION]
   >
   >コンテンツフラグメントを編集するには、 [適切な権限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 問題が発生している場合は、システム管理者に問い合わせてください。

   >[!NOTE]
   >
   >エディターを開いたまま、一連の変更を加えてから保存することもできます。

   >[!CAUTION]
   >
   >これらの操作では、変更を保存するだけでなく、参照もすべて更新し、Dispatcher が必要に応じてフラッシュされます。これらの変更の処理には時間がかかる場合があります。 このため、大規模/複雑/負荷の高いシステムにパフォーマンスが影響を与える可能性があります。
   >
   >「**保存して閉じる**」を使用する際はこの点に留意し、フラグメントエディターをすぐに開いて、さらに変更を加え保存してください。

* **閉じる**

   最新の変更（前回の「**保存**」操作以降に行った変更）を保存せずにエディターを終了します。

コンテンツフラグメントを編集するとき、AEM によって自動的にバージョンが作成されます。これにより、（保存せずに「**閉じる**」を使用して）変更内容を取り消した場合でも、以前のコンテンツを復元できるようになります。

1. コンテンツフラグメントを開いて編集しようとすると、AEM は&#x200B;*編集セッション*&#x200B;が存在しているかどうかを示す cookie ベースのトークンの存在を確認します。

   1. トークンが見つかると、そのフラグメントは既存の編集セッションの一部であると見なされます。
   2. トークンがないときにユーザーが編集を開始すると、バージョンが作成され、この新しい編集セッションのトークンがクライアントに送られ、cookie に保存されます&#x200B;*。*

2. アクティブな編集セッションがあるとき、編集中のコンテンツは自動的に 600 秒ごとに保存されます（デフォルト）*。*

   >[!NOTE]
   >
   >自動保存間隔は `/conf` メカニズムを使用して設定できます。
   >
   >デフォルト値については、以下を参照してください。
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. ユーザーが編集をキャンセルした場合は、編集セッションの開始時に作成されたバージョンが復元され、トークンが削除されて編集セッションが終了します。
4. ユーザーが編集内容の「**保存**」を選択すると、更新された要素とバリエーションが保存され、トークンが削除されて編集セッションが終了します。

## フラグメントのコンテンツの編集 {#editing-the-content-of-your-fragment}

フラグメントを開いたら、 [バリエーション](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) タブを使用して、コンテンツを作成します。

## フラグメント内のバリエーションの作成と管理 {#creating-and-managing-variations-within-your-fragment}

プライマリコンテンツを作成したら、そのコンテンツの[バリエーション](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)を作成して管理できます。

## コンテンツとフラグメントの関連付け {#associating-content-with-your-fragment}

また、 [コンテンツを関連付け](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) フラグメントを含む これにより、アセット（画像）をフラグメントと共に（オプションで）コンテンツページに追加する際に使用できるようにする接続が提供されます。

## フラグメントのメタデータ（プロパティ）の表示と編集 {#viewing-and-editing-the-metadata-properties-of-your-fragment}

「[メタデータ](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md)」タブを使用し、フラグメントのプロパティを表示して編集できます。

## フラグメントの公開と参照 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
フラグメントがモデルに基づいている場合、 [モデルが公開されました](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

コンテンツフラグメントをパブリッシュ環境で使用するには、公開する必要があります。

* [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment)のツールバーの「**公開**」オプションから
   * **今すぐ** - 確認後、フラグメントは直ちに公開されます
   * **スケジュール** - フラグメントを公開する日時を選択できます

   必要に応じて、**アクティベーション日**と公開する参照を指定する必要があります。次に例を示します。
   ![公開ダイアログ](assets/cfm-publish-01.png)

* [コンテンツフラグメントエディター](#toolbar-actions-in-the-content-fragment-editor)から
   * [**クイック公開**](/help/assets/manage-publication.md#quick-publish)
   * [**パブリケーションの管理**](/help/assets/manage-publication.md#manage-publication)

さらに、[フラグメントを使用するページを公開](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing)するとき。フラグメントはページ参照にリスト表示されます。

>[!CAUTION]
フラグメントが公開または参照（あるいは両方）された後に、作成者がフラグメントを開いて編集しようとすると警告が表示され、フラグメントを変更すると、参照されているページにも影響が及ぶことが警告されます。

## フラグメントの非公開 {#unpublishing-a-fragment}

コンテンツフラグメントを非公開にするには、1 つ以上のフラグメントを選択してから、**非公開**&#x200B;します。

>[!NOTE]
公開されたフラグメントが利用可能になると、**非公開**&#x200B;アクションが表示されます。

>[!CAUTION]
フラグメントが既に別のフラグメントから参照されている場合、またはページから参照されている場合は、警告メッセージが表示され、続行を確認する必要があります。

## フラグメントの削除 {#deleting-a-fragment}

フラグメントを削除するには：

1. **コンテンツフラグメント**&#x200B;コンソールで、コンテンツフラグメントの場所に移動します。
2. フラグメントを選択します。

   >[!NOTE]
   この **削除** アクションは、クイックアクションとして使用できません。

3. ツールバーから「**削除**」を選択します。
4. 「**削除**」アクションを確認します。

   >[!CAUTION]
   フラグメントが既に別のフラグメントから参照されている場合、またはページから参照されている場合は、警告メッセージが表示されます。「**削除を強制**」を選択して続行を確認する必要があります。フラグメントはコンテンツフラグメントコンポーネントと一緒に、すべてのコンテンツページから削除されます。

## フラグメントの親参照の検索 {#parent-references-fragment}

親参照の詳細には、[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments)の&#x200B;**参照**&#x200B;列からアクセスできます。

## フラグメントの言語コピーの検索 {#language-copies-fragment}

言語コピーの詳細には、[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments)の&#x200B;**言語**&#x200B;列からアクセスできます。

## コンテンツフラグメントのタイムライン {#timeline-for-content-fragments}

>[!NOTE]
この機能は、**Assets** コンソールでのみ利用できます

標準オプションに加えて、 [タイムライン](/help/assets/manage-digital-assets.md#timeline) には、コンテンツフラグメントに固有の情報とアクションの両方が用意されています。

* バージョン、コメント、注釈に関する情報の表示
* バージョンに対するアクション

   * **[このバージョンに戻る](#reverting-to-a-version)**（既存のフラグメントを選択してから特定のバージョンを選択）

   * **[現在のバージョンと比較](#comparing-fragment-versions)**（既存のフラグメントを選択してから特定のバージョンを選択）

   * **ラベル**&#x200B;や&#x200B;**コメント**&#x200B;の追加（既存のフラグメントを選択してから特定のバージョンを選択）

   * **バージョンとして保存** （既存のフラグメントを選択してから、タイムラインの下部にある上向き矢印を選択）

* 注釈のアクション

   * **削除**

>[!NOTE]
コメントは次のとおりです。
* すべてのアセットの標準機能
* タイムラインで作成
* フラグメントアセットに関連
>
注釈（コンテンツフラグメント用）は次のとおりです。
* フラグメントエディターに入力
* フラグメント内の選択したテキストセグメントに固有
>


次に例を示します。

![タイムライン](assets/cfm-managing-05.png)

## フラグメントのバージョンの比較 {#comparing-fragment-versions}

>[!NOTE]
この機能は、**Assets** コンソールでのみ利用できます

この **現在と比較** アクションは、 [タイムライン](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 特定のバージョンを選択した後。

開く：

* **現在**（最新）のバージョン（左）

* 選択されたバージョン **v&lt;*x.y*>**（右）

これらは左右に並んで表示されます。この画面について以下で説明します。

* 違いが強調表示されます

   * 削除されたテキスト — 赤
   * 挿入されたテキスト - 緑
   * 置換されたテキスト — 青

* 全画面表示アイコンを使用すれば、どちらかのバージョンで開いた後で、並列表示に切り替えることができます
* 以下が可能です。 **元に戻す** 特定のバージョンに
* **完了** コンソールに戻ります

>[!NOTE]
フラグメントの比較時にフラグメントコンテンツを編集することはできません。

![比較](assets/cfm-managing-06.png)

## 特定のバージョンへの復帰   {#reverting-to-a-version}

>[!NOTE]
この機能は、**Assets** コンソールでのみ利用できます

フラグメントの特定のバージョンに戻すことができます。

* 直接 [タイムライン](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   必要なバージョンを選択した後、「**このバージョンに戻す**」アクションを選択します。

* [あるバージョンと現在のバージョンを比較](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#comparing-fragment-versions)し、選択したバージョンに&#x200B;**戻す**&#x200B;ことができます。
