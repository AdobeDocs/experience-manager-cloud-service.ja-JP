---
title: コンポーネントリファレンスガイド
description: コンポーネントとその構造の詳細に関するデベロッパー向けリファレンスガイド
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3476'
ht-degree: 98%

---

# コンポーネントリファレンスガイド {#components-reference-guide}

コンポーネントは、AEM でエクスペリエンスを構築する際の中心です。[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)と[&#x200B; AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を使うと、堅牢な既製のコンポーネントのツールセットを簡単に使い始めることができます。[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、デベロッパーがこれらのツールの使用方法と、AEM サイトを作成するためのカスタムコンポーネントの作成方法を学びます。

>[!TIP]
>
>このドキュメントを参照する前に、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)を完了し、[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)と [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)についてよく理解しておく必要があります。

WKND チュートリアルでは、ほとんどの使用例をカバーしているので、このドキュメントはこれらのリソースを補完する目的でのみ提供されます。AEM でのコンポーネントの構造化および設定方法に関する詳細な技術的詳細を説明するものであり、入門用ガイドとしての意図されたものではありません。

## 概要 {#overview}

この節では、独自コンポーネントの開発時に知っておくべき詳細の導入段階として、基本的な概念と注意点について説明します。

### 計画 {#planning}

実際にコンポーネントの設定やコーディングを開始する前に、次の点について理解する必要があります。

* そもそも新しいコンポーネントで何をするか
* コンポーネントを一から作成する必要があるか、基本部分を既存のコンポーネントから継承できるか
* コンポーネントのコンテンツを選択または操作するためのロジックが必要か
   * ロジックは、ユーザーインターフェイスレイヤーから分離しておく必要があります。HTL はこれに対応した設計になっています。
* コンポーネントを CSS で書式設定する必要があるか
   * CSS による書式設定は、コンポーネント定義から分離しておく必要があります。外部 CSS ファイルを使用して HTML 要素を変更できるように、HTML 要素の命名規則を定義します。
* 新しいコンポーネントがもたらすセキュリティ上の影響はなにか

### 既存コンポーネントの再利用 {#reusing-components}

全く新しいコンポーネントの作成に時間を費やす前に、既存のコンポーネントのカスタマイズや拡張を検討してください。[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)は、柔軟で堅牢かつ十分にテストされた実稼働用コンポーネントのセットを提供します。

#### コアコンポーネントの拡張 {#extending-core-components}

また、コアコンポーネントは、[明確なカスタマイズパターン](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja)を備えており、独自のプロジェクトのニーズに合わせることもできます。

#### コンポーネントのオーバーレイ {#overlying-components}

コンポーネントは、検索パスロジックに基づいた[オーバーレイ](/help/implementing/developing/introduction/overlays.md)を使用して再定義することもできます。ただし、その場合 [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) が呼び出されないので、`/apps` でオーバーレイ全体を定義する必要があります。

#### コンポーネントダイアログの拡張 {#extending-component-dialogs}

Sling Resource Merger を使用し、`sling:resourceSuperType` プロパティを定義して、コンポーネントダイアログをオーバーライドすることもできます。

つまり、ダイアログ全体を再定義するのとは対照的に、再定義する必要があるのは相違点だけです。

### コンテンツのロジックとマークアップのレンダリング  {#content-logic-and-rendering-markup}

コンポーネントは [HTML](https://www.w3schools.com/htmL/html_intro.asp) を使用してレンダリングされます。コンポーネントでは、必要なコンテンツを取得して、オーサー環境とパブリッシュ環境の両方で必要に応じてレンダリングするために必要な HTML を定義しなければなりません。

マークアップおよびレンダリングを行うコードと、コンポーネントのコンテンツ選択に関するロジックを制御するコードは、分離しておくことをお勧めします。

この方法をサポートするテンプレート言語が [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) です。HTL では、基盤となるビジネスロジックを定義するときにのみプログラミング言語を使用します。このメカニズムは、特定のビューに対して呼び出されるコードを強調表示し、必要に応じて、同じコンポーネントの異なるビューに対して特定のロジックを使用できるようにします。

この（オプション）ロジックは様々な方法で実装でき、特定のコマンドを使用して HTL から呼び出します。

* Java の使用 - [HTL Java Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=ja) を使用すると、HTL ファイルからカスタム Java クラスのヘルパーメソッドへのアクセスが可能になります。そのため、Java コードを使用して、コンポーネントのコンテンツを選択および設定するためのロジックを実装できます。
* JavaScript の使用 - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html?lang=ja) を使用すると、HTL ファイルから JavaScript で書かれたヘルパーコードへのアクセスが可能になります。この結果、JavaScript コードを使用して、コンポーネントのコンテンツを選択および設定するためのロジックを実装できます。
* クライアントサイドライブラリの使用 - 最近の Web サイトは、複雑な JavaScript や CSS コードを利用したクライアントサイド処理に大きく依存しています。詳しくは、「[AEM as a Cloud Service でのクライアントサイドライブラリの使用](/help/implementing/developing/introduction/clientlibs.md)」ドキュメントを参照してください。

## コンポーネント構造 {#structure}

AEM コンポーネントの構造は強力で柔軟性があります。以下は主な部分です。

* [リソースタイプ](#resource-type)
* [コンポーネント定義](#component-definition)
* [コンポーネントのプロパティおよび子ノード](#properties-and-child-nodes-of-a-component)
* [ダイアログ](#dialogs)
* [デザインダイアログ](#design-dialogs)

### リソースタイプ {#resource-type}

構造の重要な構成要素となるのが、リソースタイプです。

* コンテンツの構造は意図を宣言します。
* これらは、リソースタイプによって実装されます。

このような抽象化をすることで、時間の経過と共にルックアンドフィールが変化しても、意図が変わることはありません。

### コンポーネント定義 {#component-definition}

コンポーネントの定義は次のように分解できます。

* AEM コンポーネントは、[Sling](https://sling.apache.org/documentation.html) に基づいています。
* AEM コンポーネントは、`/libs/core/wcm/components` の下に配置されています。
* プロジェクトまたはサイトに固有のコンポーネントは、`/apps/<myApp>/components` の下に配置されています。
* AEM の標準コンポーネントは、`cq:Component` として定義され、次の主要な構成要素を持ちます。
   * jcr プロパティ - jcr プロパティのリスト。これらは可変であり、コンポーネントノードの基本構造、そのプロパティ、およびサブノードは `cq:Component` 定義によって定義されますが、一部はオプションの場合があります。
   * リソース - コンポーネントが使用する静的要素を定義します。
   * スクリプト - コンポーネントの結果インスタンスの動作を実装するために使用されます。

#### 重要なプロパティ {#vital-properties}

* **ルートノード**：
   * `<mycomponent> (cq:Component)` - コンポーネントの階層ノード
* **重要なプロパティ**：
   * `jcr:title` - コンポーネントのタイトル。例えば、コンポーネントを[コンポーネントブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)および[コンポーネントコンソール](/help/sites-cloud/authoring/components-console.md)にリストする際にラベルとして使用されます。
   * `jcr:description` - コンポーネントの説明。コンポーネントブラウザーおよびコンポーネントコンソールで、ポインタを合わせると表示されるヒントとして使用されます。
   * 詳しくは、[コンポーネントアイコン](#component-icon)の節を参照してください。
* **重要な子ノード**：
   * `cq:editConfig (cq:EditConfig)` - コンポーネントの編集プロパティを定義し、コンポーネントをコンポーネントブラウザーに表示できるようにします。
      * コンポーネントにダイアログがある場合は、cq:editConfig が存在しなくても、コンポーネントブラウザーまたはSidekickに自動的に表示されます。
   * `cq:childEditConfig (cq:EditConfig)` - 独自の `cq:editConfig` を定義しない子コンポーネントの作成者 UI 要素を制御します。
   * `cq:dialog (nt:unstructured)` - このコンポーネントのダイアログ。ユーザーがコンポーネントを設定したり、コンテンツを編集したりできるインターフェイスを定義します。
   * `cq:design_dialog (nt:unstructured)` - このコンポーネントのデザイン編集。

#### コンポーネントアイコン {#component-icon}

コンポーネントのアイコンまたは省略形は、デベロッパーがコンポーネントを作成する際にコンポーネントの JCR プロパティで定義します。これらのプロパティは、次の順番で評価され、最初に見つかった有効なプロパティが使用されます。

1. `cq:icon` - コンポーネントブラウザーで表示する [Coral UI ライブラリ](https://opensource.adobe.com/coral-spectrum/examples/#icon)の標準的なアイコンを指定する String プロパティ。
   * Coral アイコンの HTML 属性の値を使用します。
1. `abbreviation` - コンポーネントブラウザーでのコンポーネント名の省略形をカスタマイズする String プロパティ。
   * 省略形は最大 2 文字までにする必要があります。
   * 空の文字列が指定されると、`jcr:title` プロパティの最初の 2 文字を使用して省略形が作成されます。
      * 例えば、「Image」の場合は「Im」になります。
      * ローカライズされたタイトルが省略形の作成に使用されます。
   * 省略形は、コンポーネントに `abbreviation_commentI18n` プロパティがある場合にのみ翻訳されます。これは、翻訳ヒントとして使用されます。
1. `cq:icon.png` または `cq:icon.svg` - コンポーネントブラウザーに表示される、このコンポーネントのアイコン。
   * 20 x 20 ピクセルは、標準的なコンポーネントのアイコンのサイズです。
      * 大きいアイコンはクライアントサイドで縮小されます。
   * お勧めの色は、RGB（112、112、112）、つまり #707070 です。
   * 標準的なコンポーネントアイコンの背景は、透明です。
   * `.png` および `.svg` ファイルのみがサポートされます。
   * Eclipse プラグインを使用してファイルシステムから読み込む場合、例えば `_cq_icon.png` や `_cq_icon.svg` のように、ファイル名をエスケープする必要があります。
   * 両方が存在する場合は、`.png` が `.svg` よりも優先されます

コンポーネントで上述のプロパティ（`cq:icon`、`abbreviation`、`cq:icon.png` または `cq:icon.svg`）が見つからない場合：

* システムは、`sling:resourceSuperType` プロパティに続くスーパーコンポーネント上の同じプロパティを検索します。
* スーパーコンポーネントレベルで見つからないか空の省略形が見つかった場合、システムは現在のコンポーネントの `jcr:title` プロパティの最初の文字から省略形を作成します。

スーパーコンポーネントからアイコンの継承をキャンセルするために、コンポーネントで空の `abbreviation` プロパティを設定すると、デフォルトの動作に戻ります。

[コンポーネントコンソール](/help/sites-cloud/authoring/components-console.md#component-details)には、特定のコンポーネントのアイコンの定義方法が表示されます。

#### SVG アイコンの例 {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### コンポーネントのプロパティおよび子ノード {#properties-and-child-nodes-of-a-component}

コンポーネントの定義に必要なノードまたはプロパティの多くは、両方の UI に共通です。コンポーネントがどちらの環境でも機能できるよう、相違点の独立性は確保されています。

コンポーネントはタイプ `cq:Component` のノードで、次のプロパティと子ノードがあります。

| 名前 | 種類 | 説明 |
|---|---|---|
| `.` | `cq:Component` | これは現在のコンポーネントを表します。ノードタイプ `cq:Component` のコンポーネント。 |
| `componentGroup` | `String` | これは、[コンポーネントブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)でコンポーネントを選択できるグループを表します。「`.`」で始まる値は、他のコンポーネントが継承する基本コンポーネントなど、UI から選択できないコンポーネントに使用されます。 |
| `cq:isContainer` | `Boolean` | コンポーネントがコンテナコンポーネントかどうか、したがって段落システムなど他のコンポーネントを格納できるかどうかを示します。 |
| `cq:dialog` | `nt:unstructured` | これは、コンポーネントの編集ダイアログの定義です。 |
| `cq:design_dialog` | `nt:unstructured` | これは、コンポーネントのデザインダイアログの定義です。 |
| `cq:editConfig` | `cq:EditConfig` | これは、[コンポーネントの編集設定](#edit-behavior)を定義します。 |
| `cq:htmlTag` | `nt:unstructured` | 対象を囲んでいる HTML タグに追加されたその他のタグ属性を返します。自動生成された div に属性を追加できます。 |
| `cq:noDecoration` | `Boolean` | true の場合、コンポーネントは、自動生成された div クラスと css クラスでレンダリングされません。 |
| `cq:template` | `nt:unstructured` | このプロパティがある場合、コンポーネントがコンポーネントブラウザーから追加された際に、コンテンツテンプレートとしてこのノードを使用します。 |
| `jcr:created` | `Date` | コンポーネントの作成日です。 |
| `jcr:description` | `String` | コンポーネントの説明です。 |
| `jcr:title` | `String` | コンポーネントのタイトルです。 |
| `sling:resourceSuperType` | `String` | 設定した場合、コンポーネントの継承元がこのコンポーネントになります。 |
| `component.html` | `nt:file` | コンポーネントの HTL スクリプトファイルです。 |
| `cq:icon` | `String` | この値は、[&#128279;](#component-icon)コンポーネントのアイコンを指し、コンポーネントブラウザーに表示されます。 |

**テキスト**&#x200B;コンポーネントを見ると、次のいくつかの要素が表示されます。

![テキストコンポーネントの構造](assets/components-text.png)

特に重要なプロパティを次に示します。

* `jcr:title` - これは、コンポーネントブラウザ内のコンポーネントを識別するために使用されるコンポーネントのタイトルです。
* `jcr:description` - コンポーネントの説明です。
* `sling:resourceSuperType` - （定義のオーバーライドによる）コンポーネントの拡張時に、継承パスを示します。

特に重要な子ノードを次に示します。

* `cq:editConfig` - 編集時のコンポーネントの視覚的な外観を制御します。
* `cq:dialog` - このコンポーネントのコンテンツを編集するためのダイアログを定義します。
* `cq:design_dialog` - このコンポーネントのデザイン編集オプションを指定します。

### ダイアログ {#dialogs}

ダイアログは、コンポーネントの主要な要素の 1 つです。作成者がコンテントページでコンポーネントを設定し、必要情報を提供するためのインターフェイスをダイアログが備えているからです。コンテンツ作成者がコンポーネントとやり取りする方法の詳細については、[オーサリングドキュメント](/help/sites-cloud/authoring/page-editor/edit-content.md)を参照してください。

コンポーネントの複雑さに応じて、ダイアログに 1 つ以上のタブが必要になる場合があります。

AEM コンポーネントのダイアログ：

* タイプ `nt:unstructured` の `cq:dialog` ノードです。
* `cq:Component` ノードの下のコンポーネント定義の横にあります。
* このコンポーネントのコンテンツ編集に使用するダイアログを定義します。
* Granite UI コンポーネントを使用して定義されます。
* コンテンツ構造と `sling:resourceType` プロパティに基づいて、サーバーサイドで（Sling コンポーネントとして）レンダリングされます。
* ダイアログ内のフィールドを記述したノード構造を含みます。
   * これらのノードは、必須の `nt:unstructured` プロパティを持つ `sling:resourceType` ノードです。

![タイトルコンポーネントのダイアログ定義](assets/components-title-dialog.png)

ダイアログ内で、個々のフィールドは次のように定義されます。

![タイトルコンポーネントのダイアログ定義のフィールド](assets/components-title-dialog-items.png)

### デザインダイアログ {#design-dialogs}

デザインダイアログは、コンテンツの編集と構成に使用されるダイアログに似ていますが、テンプレート作成者がページテンプレート上のそのコンポーネントのデザインの詳細をプロ構成および提供するためのインターフェイスを提供します。次に、コンテンツ作成者がページテンプレートを使用してコンテンツページを作成します。テンプレートの作成方法の詳細については、[テンプレートドキュメント](/help/sites-cloud/authoring/page-editor/templates.md)を参照してください。

[ページテンプレートの編集時にはデザインダイアログが使用されます](/help/sites-cloud/authoring/page-editor/templates.md)。ただし、すべてのコンポーネントで必要とされるわけではありません。例えば、**タイトル**&#x200B;と&#x200B;**画像コンポーネント**&#x200B;の両方にデザインのダイアログがありますが、**ソーシャルメディア共有コンポーネント**&#x200B;はありません。

### Coral UI と Granite UI {#coral-and-granite}

AEM のルックアンドフィールは Coral UI と Granite UI で定義されています。

* [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) はすべてのクラウドソリューションに一貫性ある UI を提供します。
* [Granite UI](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) は、コンソールおよびダイアログの構築用に Coral UI マークアップを Sling コンポーネントにラップして提供します。

Granite UI で提供される幅広い基本ウィジェットは、オーサー環境でダイアログを作成するために使用されます。必要な場合には、選択したウィジェットを拡張し、独自のウィジェットを作成することができます。

以下のリソースについても参照してください。

* [AEM UI の構造](/help/implementing/developing/introduction/ui-structure.md)

### ダイアログフィールドのカスタマイズ {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

コンポーネントダイアログで使用するウィジェットを作成するには、Granite UI フィールドコンポーネントを作成する必要があります。

ダイアログをフォーム要素の単純なコンテナと見なす場合、ダイアログコンテンツの主なコンテンツをフォームフィールドとして表示することもできます。新しいフォームフィールドを作成するには、リソースタイプを作成する必要があります。これは、コンポーネントの作成と同じです。この作業を容易にするには、Granite UI は、`sling:resourceSuperType` を使用して以下を継承する汎用フィールドコンポーネントを提供しています。

`/libs/granite/ui/components/coral/foundation/form/field`

より正確に言えば、Granite UI には、ダイアログ（一般的に言えば[フォーム](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)）での使用に適した、幅広いフィールドコンポーネントが用意されています。

リソースタイプを作成したら、`sling:resourceType` プロパティで参照して新しいノードをダイアログに追加することで、フィールドをインスタンス化できます。

#### ダイアログフィールドへのアクセス {#access-to-dialog-fields}

レンダリング条件（`rendercondition`）を使用して、ダイアログ内の特定のタブやフィールドへのアクセス権を持つユーザーを制御することもできます。以下に例を示します。

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## コンポーネントの使用 {#using-components}

コンポーネントを作成したら、それを使用できるようにする必要があります。コンポーネントを使用すると、コンポーネントの構造とリポジトリの結果として得られるコンテンツの構造との関連がかわります。

### コンポーネントをテンプレートに追加する {#adding-your-component-to-the-template}

コンポーネントを定義した上で、使用可能にする必要があります。コンポーネントをテンプレートで使用できるようにするには、テンプレートのレイアウトコンテナのポリシーでそのコンポーネントを有効にする必要があります。

テンプレートの作成方法の詳細については、[テンプレートドキュメント](/help/sites-cloud/authoring/page-editor/templates.md)を参照してください。

### コンポーネントおよびコンポーネントによって作成されるコンテンツ {#components-and-the-content-they-create}

次のページに&#x200B;**タイトル**&#x200B;コンポーネントのインスタンスを作成して設定する場合：`/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![タイトル編集ダイアログ](assets/components-title-dialog.png)

ここで、リポジトリー内に作成されたコンテンツの構造を確認できます。

![タイトルコンポーネントのノード構造](assets/components-title-content-nodes.png)

特に、**タイトル**&#x200B;コンポーネントの実際のテキストに着目した場合：

* コンテンツには `jcr:title` プロパティが含まれており、このプロパティには作成者が入力したタイトルの実際のテキストが含まれています。
* また、コンポーネント定義への `sling:resourceType` 参照も含まれます。

定義されるプロパティは、個々の定義によって異なります。上記よりも複雑になる場合がありますが、同じ基本原則に従っています。

## コンポーネントの階層と継承 {#component-hierarchy-and-inheritance}

AEM 内のコンポーネントは、**リソースタイプの階層**&#x200B;の対象となります。プロパティでコンポーネントを拡張する場合に使用されます。`sling:resourceSuperType`これにより、コンポーネントは別のコンポーネントから継承できます。

詳しくは、「[コンポーネントの再利用](#reusing-components)」を参照してください。

## 編集動作 {#edit-behavior}

この節では、コンポーネントの編集動作の設定方法について説明します。これには、コンポーネントに対して使用可能なアクションなどの属性、インプレースエディターの特性、コンポーネントに対するイベントに関連するリスナーも含まれます。

コンポーネントの編集動作を設定するには、タイプ `cq:editConfig` の `cq:EditConfig` ノードをコンポーネントノード（タイプ `cq:Component`）の下に追加し、特定のプロパティと子ノードを追加します。使用可能なプロパティと子ノードを次に示します。

* `cq:editConfig` ノードのプロパティ
* [`cq:editConfig` 子ノード](#configuring-with-cq-editconfig-child-nodes)：
   * `cq:dropTargets`（ノードタイプ `nt:unstructured`）：コンテンツファインダーのアセットからのドロップを受け入れることができるドロップターゲットのリストを定義します（1 つのドロップターゲットを許可します）
   * `cq:inplaceEditing`（ノードタイプ `cq:InplaceEditingConfig`）：コンポーネントのインプレース編集設定を定義します
   * `cq:listeners`（ノードタイプ `cq:EditListenersConfig`）：コンポーネントでアクションを実行する前後の処理を定義します

AEM には、既存の設定が多数あります。**CRXDE Lite** のクエリツールを使用すると、特定のプロパティまたは子ノードを簡単に検索できます。

### コンポーネントプレースホルダー {#component-placeholders}

コンポーネントは、コンテンツがない場合でも必ず、作成者に表示される一部の HTML をレンダリングする必要があります。そうしないと、エディターのインターフェイスから視覚的に消えてしまい、技術的には存在しても、ページやエディターには表示されなくなります。この場合、作成者は空のコンポーネントを選択して操作することができません。

このため、ページがページエディターでレンダリングされる（WCM モードが `edit` または `preview` の場合）際に、コンポーネントは、表示された出力をレンダリングしない限り、プレースホルダーをレンダリングする必要があります。
プレースホルダーの一般的な HTML マークアップは次のとおりです。

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

上記のプレースホルダー HTML をレンダリングする一般的な HTL スクリプトは次のとおりです。

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

前の例では、`isEmpty` は、コンポーネントにコンテンツがなくて作成者には見えない場合にのみ true になる変数です。

繰り返しを避けることを目的に、アドビでは、これらのプレースホルダーに、[コアコンポーネントで提供されるような](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html) HTL テンプレートを使用することをコンポーネントの実装者にお勧めします。

その後、前のリンクでのテンプレートの使用は、次の HTL 行で行います。

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

前の例では、`model.text` はコンテンツが含まれていて表示されている場合にのみ true になる変数です。

このテンプレートの使用例は、[タイトルコンポーネントなど](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)、コアコンポーネントで確認できます。

### cq:EditConfig 子ノードを使用した設定 {#configuring-with-cq-editconfig-child-nodes}

#### Assetsをダイアログにドロップする – cq:dropTargets {#cq-droptargets}

`cq:dropTargets` ノード（ノードタイプ `nt:unstructured`）では、コンテンツファインダーからドラッグしたアセットからのドロップを受け入れ可能なドロップターゲットを定義します。`cq:DropTargetConfig` 型のノードです。

タイプ `cq:DropTargetConfig` の子ノードでは、コンポーネントのドロップターゲットを定義します。

### インプレース編集 – cq:inplaceEditing {#cq-inplaceediting}

インプレースエディターを使用すると、ダイアログを開くことなく、コンテンツフロー内で直接コンテンツを編集できます。例えば、標準の&#x200B;**テキスト**&#x200B;と&#x200B;**タイトル**&#x200B;のコンポーネントには、どちらもインプレースエディターがあります。

インプレースエディターは、すべてのコンポーネントタイプで必要なものではありません。

`cq:inplaceEditing` ノード（ノードタイプ `cq:InplaceEditingConfig`）では、コンポーネントのインプレース編集設定を定義します。このノードは、次のプロパティを持つことができます。

| プロパティ名 | プロパティタイプ | プロパティの値 |
|---|---|---|
| `active` | `Boolean` | `true` を使用して、コンポーネントのインプレース編集を有効にします。 |
| `configPath` | `String` | エディター設定のパス（設定ノードで指定可能） |
| `editorType` | `String` | 次のタイプを使用できます。非 HTML のコンテンツ用の `plaintext`、編集を開始する前にグラフィカルタイトルをプレーンテキストに変換する `title`、リッチテキストエディターを使用する `text` |

次の設定では、コンポーネントのインプレース編集が可能になり、エディタータイプとして `plaintext` が定義されます。

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### フィールドイベントの処理 – cq:listeners {#cq-listeners}

ダイアログフィールドのイベントの処理は、カスタム[クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)のリスナーで行われます。

フィールドにロジックを挿入するには、以下を実行する必要があります。

* 対象となるフィールドを、指定された CSS クラス（フック）でマークします。
* クライアントライブラリ内で、その CSS クラス名に対してフックされる JS リスナーを定義します（これによって、カスタムロジックの範囲がそのフィールドのみに限定され、同じタイプの他のフィールドに影響を与えなくなります）。

これを実現するには、やり取りする、基になるウィジェットライブラリについて理解する必要があります。[反応するイベントの識別については、Coral UI ドキュメント](https://opensource.adobe.com/coral-spectrum/documentation/)を参照してください

`cq:listeners` ノード（ノードタイプ `cq:EditListenersConfig`）では、コンポーネントでアクションを実行する前後の処理を定義します。次の表では、使用する可能性のあるプロパティ値の定義を示します。

| プロパティ名 | プロパティの値 |
|---|---|
| `beforedelete` | コンポーネントを削除する前にハンドラーがトリガーされます。 |
| `beforeedit` | コンポーネントを編集する前にハンドラーが呼び出されます。 |
| `beforecopy` | コンポーネントをコピーする前にハンドラーが呼び出されます。 |
| `beforeremove` | コンポーネントを移動する前にハンドラーが呼び出されます。 |
| `beforeinsert` | コンポーネントを挿入する前にハンドラーが呼び出されます。 |
| `beforechildinsert` | コンポーネントを別のコンポーネント（コンテナのみ）の内部に挿入する前にハンドラーが呼び出されます。 |
| `afterdelete` | コンポーネントを削除した後にハンドラーが呼び出されます。 |
| `afteredit` | コンポーネントを編集した後にハンドラーが呼び出されます。 |
| `aftercopy` | コンポーネントをコピーした後にハンドラーが呼び出されます。 |
| `afterinsert` | コンポーネントを挿入した後にハンドラーが呼び出されます。 |
| `aftermove` | コンポーネントを移動した後にハンドラーが呼び出されます。 |
| `afterchildinsert` | コンポーネントを別のコンポーネント（コンテナのみ）の内部に挿入した後にハンドラーが呼び出されます。 |

>[!NOTE]
>
>コンポーネントがネストされている場合は、`cq:listeners` ノードでプロパティとして定義されるアクションに一定の制限があります。コンポーネントがネストされている場合、次のプロパティの値を **にする必要があります** `REFRESH_PAGE`。
>
>* `aftermove`
>* `aftercopy`

イベントハンドラーを実装するときは、カスタム実装を組み込むことができます。次に例を示します（`project.customerAction` は静的メソッドです）。

`afteredit = "project.customerAction"`

次の例は、`REFRESH_INSERTED` 設定と同等です。

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

次の設定では、コンポーネントを削除、編集、挿入または移動した後にページが更新されます。

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### フィールドの検証 {#field-validation}

Granite UI および Granite UI ウィジェットでのフィールド検証は、`foundation-validation` API を使用して実行します。詳しくは、[`foundation-valdiation`Granite のドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)を参照してください。

### ダイアログの可用性の検出 {#dialog-ready}

ダイアログが使用可能で準備が整っている場合にのみ実行する必要があるカスタム JavaScript がある場合は、`dialog-ready` イベントをリッスンする必要があります。

このイベントは、ダイアログが読み込まれて（または再度読み込まれて）、使用の準備ができたときにトリガーされます。つまり、ダイアログの DOM に変更（作成／更新）がある場合に必ずトリガーされます。

`dialog-ready` は、ダイアログ内のフィールドや類似のタスクをカスタマイズする JavaScript カスタムコードをフックするために使用できます。

## プレビュー動作 {#preview-behavior}

プレビューモードに切り替えると、ページが更新されなくても [WCM モード](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie が設定されます。

レンダリングが WCM モードの影響を受けるコンポーネントの場合は、明確にそのコンポーネントを更新し、この Cookie の値を使用するように定義する必要があります。

## コンポーネントのドキュメント化 {#documenting-components}

デベロッパーは、以下をすばやく把握できるようにコンポーネントドキュメントに簡単にアクセスしたいと考えます。

* 説明
* 使用目的
* コンテンツの構造とプロパティ
* 公開済みの API と拡張ポイント
* 等。

このため、コンポーネント内で既存のドキュメントマークダウンを利用できるようにするのは非常に簡単です。

これには、コンポーネント構造に `README.md` ファイルを配置するだけです。

![README.md （コンポーネント構造内）](assets/components-documentation.png)

その後、このマークダウンは[コンポーネントコンソール](/help/sites-cloud/authoring/components-console.md)に表示されるようになります。

![コンポーネントコンソールに表示される README.md](assets/components-documentation-console.png)

サポートされているマークダウンは、[コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)の場合と同じです。
