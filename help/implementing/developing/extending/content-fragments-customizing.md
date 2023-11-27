---
title: コンテンツフラグメントのカスタマイズと拡張
description: コンテンツフラグメントは、標準アセットを拡張します。カスタマイズ方法を学びます。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '1782'
ht-degree: 56%

---

# コンテンツフラグメントのカスタマイズと拡張{#customizing-and-extending-content-fragments}

Adobe Experience Manager as a Cloud Service 内で、コンテンツフラグメントは標準アセットを拡張します。

* コンテンツフラグメントについて詳しくは、[コンテンツフラグメントの作成と管理](/help/sites-cloud/administering/content-fragments/overview.md)および[コンテンツフラグメントを使用したページオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)を参照してください。

* 「[アセットの管理](/help/assets/manage-digital-assets.md)」を参照してください。

## アーキテクチャ {#architecture}

基本 [構成部品](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) コンテンツフラグメントの次の要素が含まれます。

* A *コンテンツフラグメント* 自然
* これは、1 つ以上の *コンテンツ要素*
* 1 つ以上の *コンテンツのバリエーション*

個々のコンテンツフラグメントは、コンテンツフラグメントモデルに基づいています。

* コンテンツフラグメントモデルでは、コンテンツフラグメントの作成時にその構造を定義します。
* フラグメントはモデルを参照するので、モデルに対する変更は、そのモデルに影響を与える場合も、依存するフラグメントに影響を与える場合もあります。
* モデルはデータタイプで構成されています。
* 新しいバリエーションを追加する関数などは、それに応じてフラグメントを更新する必要があります。

  >[!NOTE]
  >
  >コンテンツフラグメントを表示およびレンダリングするには、アカウントにモデルへの `read` 権限が必要です。

  >[!CAUTION]
  >
  >既存のコンテンツフラグメントモデルに変更を加えると、そのモデルに関連付けられているフラグメントに影響が生じる場合があり、対象のフラグメントで孤立プロパティが生まれることもあります。

### Sites と Assets の統合 {#integration-of-sites-with-assets}

コンテンツフラグメント管理 (CFM) は、Adobe Experience Manager(AEM)Assets の一部で、次の機能を持ちます。

* コンテンツフラグメントはアセットです。
* 既存のアセット機能を使用します。
* Assets と完全に統合されています（管理コンソールなど）。

コンテンツフラグメントは、AEM Sitesの機能と見なされます。

* ページのオーサリング時に使用されます。

#### コンテンツフラグメントとアセットのマッピング {#mapping-content-fragments-to-assets}

![コンテンツフラグメントをアセットへ](assets/content-fragment-to-assets.png)

コンテンツフラグメントモデルがベースのコンテンツフラグメントは、単一のアセットにマッピングされます。

* すべてのコンテンツはアセットの `jcr:content/data` ノードに格納されます。

   * 要素のデータは次のマスターサブノードに格納されます。

     `jcr:content/data/master`

   * バリエーションは、そのバリエーションの名前を持つサブノードに格納されます（例： ）。 `jcr:content/data/myvariation`

   * 各要素のデータは、要素名（要素のコンテンツなど）を持つプロパティとしてそれぞれのサブノードに保存されます。 `text` はプロパティとして保存されます `text` オン `jcr:content/data/master`

* メタデータと関連コンテンツは、`jcr:content/metadata` に格納されます。
ただし、タイトルと説明は従来のメタデータと見なされないので、`jcr:content` に格納されます。

#### アセットの場所 {#asset-location}

標準アセットの場合、コンテンツフラグメントは次の場所に保持されます。

`/content/dam`

#### アセットの権限 {#asset-permissions}

詳しくは、 [コンテンツフラグメント — 削除に関する考慮事項](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### 機能の統合 {#feature-integration}

Assets コアと統合するには：

* コンテンツフラグメント管理（CFM）機能は、アセットコアを基に構築されます。

* CFM は、カード／列／リスト表示の項目に独自の実装を提供します。つまり、それらの項目が、既存のアセットコンテンツのレンダリング実装に挿入されます。

* コンテンツフラグメントに対応するために、いくつかのアセットコンポーネントが拡張されています。

### ページでのコンテンツフラグメントの使用 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>[コンテンツフラグメントコンポーネントは、コアコンポーネントの一部です](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)。詳しくは、[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。

コンテンツフラグメントは、他のアセットタイプと同様に、AEM ページから参照できます。AEMが **[コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)** - a [ページにコンテンツフラグメントを組み込むためのコンポーネント](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). この&#x200B;**[コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)**&#x200B;コアコンポーネントを拡張することもできます。

* このコンポーネントは、`fragmentPath` プロパティを使用して、実際のコンテンツフラグメントを参照します。`fragmentPath` プロパティは、その他のアセットタイプの類似プロパティと同じ方法で処理されます。例えば、コンテンツフラグメントが別の場所に移動された場合などです。

* コンポーネントを使用すると、表示するバリエーションを選択できます。

* また、段落の範囲を選択して出力を制限することもできます。例えば、複数列の出力に使用できます。

* このコンポーネントは、中間コンテンツを許可します。

   * ここで、コンポーネントを使用して、参照されるフラグメントの段落の間に他のアセット（画像など）を配置できます。

   * 中間コンテンツの場合：

      * 不安定な参照の可能性に注意してください。 中間コンテンツ（ページのオーサリング時に追加）には、横に配置された段落との固定関係はありません。 中間コンテンツの位置の前に（コンテンツフラグメントエディターで）新しい段落を挿入すると、相対位置が失われる場合があります。

      * ページ上にレンダリングされる内容を設定する際には、追加のパラメーター（バリエーションや段落フィルターなど）を考慮します。

>[!NOTE]
>
>**コンテンツフラグメントモデル：**
>
>コンテンツフラグメントをページで使用する場合、そのフラグメントの基になるコンテンツフラグメントモデルが参照されます。
>
>そのため、ページ公開時にモデルが公開されていない場合は、フラグが付けられ、リソースに追加されているモデルがページとともに公開されます。

### その他のフレームワークとの統合 {#integration-with-other-frameworks}

コンテンツフラグメントは、次のものと統合できます。

* **翻訳**

  コンテンツフラグメントは、[AEM の翻訳ワークフロー](/help/sites-cloud/administering/translation/overview.md)と完全に統合されています。つまり、アーキテクチャレベルでは以下を意味します。

   * コンテンツフラグメントの個々の翻訳は、別々のフラグメントです。次に例を示します。

      * 異なる言語のルートの下に配置されますが、関連する言語ルートの下の相対パスを共有します。

        `/content/dam/<path>/en/<to>/<fragment>`

        上記に対して次のようになります。

        `/content/dam/<path>/de/<to>/<fragment>`

   * ルールベースのパスに加えて、コンテンツフラグメントの異なる言語バージョン間には他の接続はありません。 2 つの異なるフラグメントとして処理されますが、UI では言語のバリアント間を移動する手段を提供します。

  >[!NOTE]
  >
  >AEM 翻訳ワークフローでは、`/content` が使用されます。
  >
  >* コンテンツフラグメントモデルは `/conf` 内に配置されるので、これらの翻訳には含まれません。UI 文字列を国際化できます。

* **メタデータスキーマ**

   * コンテンツフラグメントは、 [メタデータスキーマ](/help/assets/metadata-schemas.md) 標準アセットで定義できます。

   * CFM には、次のような独自の固有のスキーマがあります。

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     必要に応じて、拡張できます。

   * 各スキーマフォームは、フラグメントエディターと統合されます。

## コンテンツフラグメント管理 API - サーバーサイド {#the-content-fragment-management-api-server-side}

サーバー側 API を使用して、コンテンツフラグメントにアクセスできます。以下を参照してください。

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobeでは、コンテンツ構造に直接アクセスする代わりに、サーバー側 API を使用することをお勧めします。

### 主要インターフェイス {#key-interfaces}

次の 3 つのインターフェイスが、入口の役割を果たします。

* **コンテンツフラグメント**（[ContentFragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)）

  このインターフェイスを使用すると、コンテンツフラグメントを抽象的に操作できます。

  このインターフェイスでは、次のことを実行できます。

   * 基本データを管理する（名前の取得、タイトルまたは説明の取得／設定など）
   * メタデータへのアクセス
   * 要素にアクセスするには、次の操作を実行します。

      * 要素を一覧表示する
      * 名前で要素を取得する
      * 要素を作成します ( [注意事項](#caveats))

      * 要素データにアクセスする（`ContentElement` を参照）

   * フラグメントに定義されたバリエーションを一覧表示する
   * バリエーションをグローバルに作成
   * 関連コンテンツを管理するには、次の操作を実行します。

      * コレクションを一覧表示する
      * コレクションを追加する
      * コレクションを削除する

   * フラグメントのモデルにアクセスする

  フラグメントの主要要素を表すインターフェイスは、次のとおりです。

   * **コンテンツ要素**（[ContentElement](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html)）

      * 基本データ（名前、タイトル、説明）を取得
      * コンテンツを取得／設定する
      * 要素のバリエーションにアクセスするには、次の操作を実行します。

         * バリエーションを一覧表示する
         * 名前でバリエーションを取得する
         * バリエーションを作成します ( [注意事項](#caveats))
         * バリエーションを削除する（[注意事項](#caveats)を参照）
         * バリエーションデータにアクセスする（`ContentVariation` を参照）

      * バリエーションを解決するためのショートカット（要素に指定されたバリエーションを使用できない場合は実装固有の追加のフォールバックロジックを適用）

   * **コンテンツのバリエーション**（[ContentVariation](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html)）

      * 基本データ（名前、タイトル、説明）を取得
      * コンテンツを取得／設定する
      * 最終変更情報に基づく単純な同期

  3 つのインターフェイス（`ContentVariation`、`ContentFragment`、`ContentElement`、）すべてによって `Versionable` インターフェイスを拡張し、コンテンツフラグメントに必要な次のバージョン管理機能を追加します。

   * 要素のバージョンを作成する
   * 要素のバージョンを一覧表示する
   * バージョン管理された要素の特定のバージョンのコンテンツを取得する

### 適応 - adaptTo() の使用  {#adapting-using-adaptto}

次のものを適応させることができます。

* `ContentFragment` は、次のものに適応させることができます。

   * `Resource` - 基になる Sling リソース。基になる `Resource` を直接更新するには `ContentFragment` オブジェクトを再構築します。

   * `Asset` - コンテンツフラグメントを表す DAM `Asset`の抽象化。`Asset` を直接更新するには `ContentFragment` オブジェクトを再構築する必要があります。

* `ContentElement` は、次のものに適応させることができます。

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - 要素の構造に関する情報にアクセスするためのものです。

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` は、次のものに適応させることができます。

   * `ContentFragment`

### 注意事項 {#caveats}

次のことに注意してください。

* API 全体は、（API JavaDoc で特に記載がない限り）変更を自動的に永続化&#x200B;**しない**&#x200B;ように設計されています。したがって、各リクエスト（または実際に使用しているリゾルバー）のリソースリゾルバーを常にコミットします。

* 追加の作業が必要になる可能性のあるタスクは、次のとおりです。

   * Adobeでは、次の場所からバリエーションを作成することをお勧めします。 `ContentFragment`. これにより、すべての要素がこのバリエーションを共有し、必要に応じて適切なグローバルデータ構造が更新され、コンテンツ構造に新しいバリエーションが反映されます。

   * 要素を使用して既存のバリエーションを削除する `ContentElement.removeVariation()`では、バリエーションに割り当てられたグローバルデータ構造は更新されません。 これらのデータ構造を確実に同期させるには、代わりに `ContentFragment.removeVariation()` を使用すると、バリエーションがグローバルに削除されます。

## コンテンツフラグメント管理 API - クライアント側 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>クライアントサイド API は内部用です。

### 追加情報 {#additional-information}

次のファイルを参照してください。

* `filter.xml`

  コンテンツフラグメント管理のための `filter.xml` は、アセットのコアコンテンツパッケージと重複しないように設定されています。

## 編集セッション {#edit-sessions}

>[!CAUTION]
>
>この背景情報を考慮してください。ここでは ( *私有地* リポジトリ内で ) でも、内部での動作を理解するのに役立つ場合があります。

複数のビュー（= HTML ページ）にまたがる可能性があるコンテンツフラグメントの編集はアトミックです。このようなアトミックなマルチ表示編集機能は、一般的な AEM の概念ではないので、コンテンツフラグメントは、*編集セッション*&#x200B;と呼ばれるものを使用します。

編集セッションは、ユーザーがエディターでコンテンツフラグメントを開くと開始されます。ユーザーが「**保存**」または「**キャンセル**」を選択してエディターから移動すると、編集セッションは終了します。

技術的には、すべての編集は *live* 他のすべてのAEM編集と同様に、コンテンツを編集できます。 編集セッションが開始されると、現在の未編集ステータスのバージョンが作成されます。ユーザーが編集をキャンセルすると、そのバージョンが復元されます。ユーザーが **保存**&#x200B;の場合、特定の操作はおこなわれません。これは、編集が *live* コンテンツを使用するので、すべての変更が既に保持されています。 また、 **保存** トリガーフルテキスト検索情報の作成、混在メディアアセットの処理、その両方など、一部のバックグラウンド処理。

エッジケースには、いくつかの安全対策があります。例えば、ユーザーが編集セッションを保存またはキャンセルせずにエディターを終了しようとした場合です。 また、データの損失を防ぐために、定期的な自動保存を使用できます。
2 人のユーザーが同じコンテンツフラグメントを同時に編集できるので、互いの変更内容が上書きされます。 これを防ぐには、DAM 管理の *チェックアウト* アクションをフラグメントに追加します。

## 例 {#examples}

### 例：既存のコンテンツフラグメントへのアクセス {#example-accessing-an-existing-content-fragment}

これを実現するには、API を表すリソースを次のように適応させます。

`com.adobe.cq.dam.cfm.ContentFragment`

次に例を示します。

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 例：コンテンツフラグメントの作成 {#example-creating-a-new-content-fragment}

コンテンツフラグメントをプログラムで作成するには、 `FragmentTemplate` モデルリソースから適応させたもの。

次に例を示します。

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 例：自動保存間隔の指定 {#example-specifying-the-auto-save-interval}

The [自動保存間隔](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) （秒単位で測定）設定マネージャー (ConfMgr) を使用して定義できます。

* ノード：`<conf-root>/settings/dam/cfm/jcr:content`
* プロパティ名：`autoSaveInterval`
* 型：`Long`

* デフォルト：`600`（10 分）。`/libs/settings/dam/cfm/jcr:content` で定義されています

自動保存間隔を 5 分に設定する場合は、ノードでプロパティを定義します。

次に例を示します。

* ノード：`/conf/global/settings/dam/cfm/jcr:content`
* プロパティ名：`autoSaveInterval`

* 型：`Long`

* 値：`300`（5 分は 300 秒です）

## ページオーサリング用コンポーネント {#components-for-page-authoring}

詳しくは、次を参照してください。

* [コアコンポーネント - コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)（推奨）
