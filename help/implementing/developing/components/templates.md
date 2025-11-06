---
title: 編集可能テンプレート
description: ページを作成する際や、初期コンテンツ、構造化コンテンツ、オーサリングポリシー、レイアウトを定義する際の、編集可能テンプレートを使用する方法について説明します。
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 100%

---

# 編集可能テンプレート {#editable-templates}

ページを作成する際や、初期コンテンツ、構造化コンテンツ、オーサリングポリシー、レイアウトを定義する際の、編集可能テンプレートを使用する方法について説明します。

## 概要 {#overview}

ページを作成する場合は、テンプレートを選択する必要があります。ページテンプレートは、新しいページのベースとして使用されます。テンプレートでは、結果ページの構造、すべての初期コンテンツ、使用可能なコンポーネント（デザインプロパティ）を定義できます。

* 編集可能テンプレートを使用すると、作成者はテンプレートを作成して使用できます。
* 編集可能テンプレートを使用すると、次の両方で編集可能なページを作成できます
   * [ページエディター](/help/sites-cloud/authoring/page-editor/templates.md)
   * [ユニバーサルエディター](/help/sites-cloud/authoring/universal-editor/templates.md)

ユニバーサルエディターで編集可能なページの作成に使用されるページテンプレートでは、編集可能テンプレート機能の制限されたサブセットを使用します。したがって、このドキュメントの残りの部分では、ページエディターで編集可能なページの作成に使用される編集可能テンプレートに焦点を当てます。

## 編集可能テンプレートとページエディターで編集されたページ {#page-editor}

ページエディターで編集可能なページを作成するテンプレートを作成する場合、通常は専門的な作成者が特定されます。

* このような専門的な作成者は、**テンプレート作成者**&#x200B;と呼ばれます。
* テンプレート作成者は、`template-authors` グループのメンバーである必要があります。
* 編集可能テンプレートから作成されたすべてのページと編集可能テンプレートとの動的な接続が保持されます。これにより、テンプレートに対するあらゆる変更がページに反映されます。
* 編集可能テンプレートによって、ページコンポーネントの汎用性が高まり、核となるページコンポーネントをカスタマイズなしで使用できます。

編集可能テンプレートを使用すると、ページの構成要素がコンポーネント内で分離されます。UI で必要なコンポーネントの組み合わせを設定できるので、ページのバリエーションごとに新しいページコンポーネントを開発する必要はなくなります。

このドキュメントでは、

* 編集可能テンプレートの作成の概要を説明します。
* 編集可能テンプレートの作成に必要な管理者や開発者のタスクについて説明します
* 編集可能テンプレートの技術的基礎について説明します
* AEM がテンプレートの利用可能性を評価する方法について説明します

>[!NOTE]
>
>このドキュメントでは、テンプレートの作成と編集について既に理解していることを前提としています。テンプレート作成者に公開される編集可能テンプレートの機能について詳しくは、オーサリングに関するドキュメントの[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md)を参照してください。

>[!TIP]
>
>[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、編集可能テンプレートの使用方法を例を実装して詳しく説明しているので、新しいプロジェクトでのテンプレートの設定方法を理解するのに非常に役立ちます。

## 新しい編集可能テンプレートの作成 {#creating-a-new-template}

編集可能テンプレートの作成は、主にテンプレート作成者が、[テンプレートコンソールとテンプレートエディター](/help/sites-cloud/authoring/page-editor/templates.md)を使用して行います。ここでは、そのプロセスの概要を示し、技術的なレベルでどのような処理が行われるかを説明します。

編集可能テンプレートを作成する場合は、次の操作を実行します。

1. [テンプレート用フォルダー](#template-folders)を作成します。これは必須ではありませんが、ベストプラクティスとして推奨されます。
1. [テンプレートタイプ](#template-type)を選択します。これをコピーして、[テンプレート定義](#template-definitions)を作成します。

   >[!NOTE]
   >
   >すぐに利用できるテンプレートタイプが用意されています。必要に応じて、[独自のサイト固有のテンプレートタイプを作成する](#creating-template-types)こともできます。

1. 新しいテンプレートの構造、コンテンツポリシー、初期コンテンツおよびレイアウトを設定します。

   **構造**

   * 構造では、テンプレートのコンポーネントおよびコンテンツを定義できます。
   * テンプレート構造で定義されたコンポーネントは、結果ページに移動することも、結果ページから削除することもできません。
   * ページ作成者がコンポーネントを追加または削除するには、テンプレートに段落システムを追加する必要があります。
   * コンポーネントのロックを解除（再度ロックできます）して、初期コンテンツを定義できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author)を参照してください。

   構造の技術的な詳細については、このドキュメントの[構造](#structure)を参照してください。

   **ポリシー**

   * コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。

      * 例えば、使用できるコンポーネントや最小／最大サイズを定義できます。

   * これらのポリシーは、テンプレート（および、そのテンプレートを使用して作成されるページ）に適用されます。

   テンプレート作成者がポリシーを定義する方法について詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-structure-template-author)を参照してください。

   ポリシーの技術的な詳細については、このドキュメントの[コンテンツポリシー](#content-policies)を参照してください。

   **初期コンテンツ**

   * 初期コンテンツは、テンプレートに基づいてページが最初に作成される際に表示されるコンテンツを定義します。
   * その後、ページ作成者が初期コンテンツを編集できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-initial-content-author)を参照してください。

   初期コンテンツの技術的な詳細については、このドキュメントの[初期コンテンツ](#initial-content)を参照してください。

   **レイアウト**

   * デバイスの形式に合わせてテンプレートのレイアウトを定義できます。
   * テンプレートがページオーサリングと同じように動作するには、レスポンシブレイアウトを使用します。

   テンプレート作成者がテンプレートレイアウトを定義する方法について詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#editing-a-template-layout-template-author)を参照してください。

   テンプレートレイアウトの技術的な詳細については、このドキュメントの[レイアウト](#layout)を参照してください。

1. テンプレートを有効にし、特定のコンテンツツリーに対して許可します。

   * テンプレートを有効または無効にして、ページ作成者が使用できるようにしたり、使用できなくしたりできます。
   * テンプレートは、特定のページブランチに対して使用可能または使用不可にすることができます。

   テンプレート作成者がテンプレートを有効にする方法について詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)を参照してください。

   テンプレートの有効化の技術的な詳細については、このドキュメントの[使用するテンプレートの有効化と許可](#enabling-and-allowing-a-template-for-use)を参照してください。

1. テンプレートを使用してコンテンツページを作成します。

   * テンプレートを使用してページを作成した場合、静的テンプレートと編集可能テンプレートの見た目に違いはなく、どちらが使用されたかはわかりません。
   * ページの作成者にとって、この処理は透過的です。

   ページ作成者がテンプレートを使用してページを作成する方法について詳しくは、[ページの作成と整理](/help/sites-cloud/authoring/sites-console/organizing-pages.md#templates)を参照してください。

   編集可能テンプレートを使用したページ作成の技術的な詳細については、このドキュメントの[作成されるコンテンツページ](#resultant-content-pages)を参照してください。

>[!TIP]
>
>国際化が必要な情報は、決してテンプレートに含めないようにしてください。国際化のためには、[コアコンポーネントのローカライゼーション機能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=ja)の利用をお勧めします。

>[!NOTE]
>
>テンプレートは、ページ作成ワークフローを効率化する強力なツールです。ただし、テンプレートが多すぎると作成者が圧倒され、ページ作成がを混乱するおそれがあります。経験上、テンプレートの数を 100 未満に抑えるのがよいでしょう。
>
>パフォーマンスに影響が及ぶ可能性があるので、1000 個を超えるテンプレートを用意することはお勧めしません。

>[!NOTE]
>
>エディタークライアントライブラリは、コンテンツページに `cq.shared` 名前空間が存在することを前提としています。名前空間が存在しない場合は、JavaScript エラー「`Uncaught TypeError: Cannot read property 'shared' of undefined`」が発生します。
>
>すべてのサンプルコンテンツページには `cq.shared` が含まれているので、それらをベースとするコンテンツには自動的に `cq.shared` が含められます。ただし、サンプルコンテンツをベースとせず、ゼロから独自のコンテンツページを作成する場合は、`cq.shared` 名前空間を含める必要があります。
>
>詳しくは、[クライアントサイドライブラリの使用](/help/implementing/developing/introduction/clientlibs.md)を参照してください。

## テンプレートフォルダー {#template-folders}

以下のフォルダーを使用してテンプレートを整理できます。

* `global`
* サイト固有

>[!NOTE]
>
>フォルダーはネストできますが、**テンプレート**&#x200B;コンソールで表示すると、フラット構造として表されます。

標準の AEM インスタンスでは、テンプレートコンソールに既に `global` フォルダーが存在します。この中にデフォルトのテンプレートが格納されており、現在のフォルダーにポリシーやテンプレートタイプがない場合にはフォールバックとして機能します。このフォルダーに独自のデフォルトのテンプレートを追加することも、新しいフォルダーを作成すること（推奨）もできます。

>[!NOTE]
>
>カスタマイズしたテンプレートを格納するフォルダーを作成し、`global` フォルダーは使用しないことをお勧めします。

>[!CAUTION]
>
>フォルダーは、`admin` 権限を持つユーザーが作成する必要があります。

テンプレートのタイプやポリシーは、次の優先順位に従ってすべてのフォルダーに継承されます。

1. 現在のフォルダー
1. 現在のフォルダーの親
1. `/conf/global`
1. `/apps`
1. `/libs`

許可されたすべてのエントリのリストが表示されます。オーバーラップする設定がある場合（`path`／`label`）、現在のフォルダーに最も近いインスタンスがユーザーに表示されます。

フォルダーを作成するには、次のいずれかの方法を使用できます。

* プログラムで自動的に、または CRXDE Lite を使用して作成
* [設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)の使用 

## CRXDE Lite の使用 {#using-crxde-lite}

1. インスタンスの新しいフォルダー（/conf の下）は、プログラムで自動的にまたは CRXDE Lite を使用して作成できます。

   次の構造を使用する必要があります。

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. その後、フォルダーのルートノードに次のプロパティを定義できます。

   `<your-folder-name> [sling:Folder]`

   * 名前：`jcr:title`
   * 型：`String`
   * 値：**テンプレート**&#x200B;コンソールに表示される（フォルダーの）タイトルです。

1. 作成者が新しいフォルダーにテンプレートを作成できるようにするには、標準のオーサリング権限と特権（`content-authors` など）に加え、グループを割り当てて作成者に必要なアクセス権限（ACL）を定義する必要があります。

   割り当てる必要があるデフォルトのグループは、`template-authors` グループです。詳しくは、[ACL とグループ](#acls-and-groups)の節を参照してください。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 設定ブラウザーの使用 {#using-the-configuration-browser}

1. **グローバルナビゲーション**／**ツール**／[**設定ブラウザー**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)&#x200B;に移動します。

   `global` フォルダーなどの既存のフォルダーは左側に一覧表示されます。

1. 「**作成**」をクリックします。
1. **設定を作成**&#x200B;ダイアログで、以下のフィールドを設定する必要があります。

   * **タイトル**：設定フォルダーのタイトルを指定します
   * **編集可能テンプレート**：このフォルダー内で編集可能なテンプレートを許可する場合にチェックマークを付けます

1. 「**作成**」をクリックします。

>[!NOTE]
>
>グローバルフォルダーにテンプレートを作成する場合は、[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)でグローバルフォルダーを編集し、「**編集可能なテンプレート**」オプションをオンにします。ただし、これは推奨されるベストプラクティスではありません。

### ACL とグループ {#acls-and-groups}

（CRXDE または設定ブラウザーを使用して）テンプレートフォルダーが作成されたら、セキュリティを確保するために、テンプレートフォルダーの適切なグループに ACL を定義する必要があります。

例として、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)のテンプレートフォルダーを使用できます。

#### template-authors グループ {#the-template-authors-group}

`template-authors` グループは、テンプレートへのアクセスを管理するために使用されるグループで、AEM に標準で付属していますが空です。ユーザーは、プロジェクト／サイトのグループに追加する必要があります。

>[!CAUTION]
>
>`template-authors` グループは、新しいテンプレートを作成する必要があるユーザー専用です。
>
>テンプレートの編集は非常に強力なので、正しく行わないと既存のテンプレートが壊れる場合があります。そのため、このロールには注意深く、ふさわしいユーザーだけを含めてください。

次の表に、テンプレートの編集に必要な権限を示します。

<table>
 <tbody>
  <tr>
   <th>パス</th>
   <th>ロール／グループ</th>
   <th>権限<br /> </th>
   <th>説明</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>テンプレート作成者<br /> </td>
   <td>読み取り、書き込み、複製</td>
   <td>サイト固有の <code>/conf</code> スペースでテンプレートを作成、読み取り、更新、削除、複製するテンプレート作成者</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にテンプレートを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>replicateContent 作成者は、ページをアクティブ化する際に、ページのテンプレートをアクティブ化する必要があります</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>読み取り、書き込み、複製</td>
   <td>サイト固有の <code>/conf</code> スペースでテンプレートを作成、読み取り、更新、削除、複製するテンプレート作成者</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>読み取り</td>
   <td>匿名 Web ユーザーは、ページのレンダリング中にポリシーを読む必要があります</td>
  </tr>
  <tr>
   <td>コンテンツ作成者</td>
   <td>複製</td>
   <td>コンテンツ作成者は、ページをアクティブ化する際に、ページのテンプレートのポリシーをアクティブ化する必要があります</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>テンプレート作成者</td>
   <td>読み取り</td>
   <td>テンプレート作成者は、定義済みのテンプレートタイプの 1 つに基づいて新しいテンプレートを作成します。</td>
  </tr>
  <tr>
   <td>匿名 Web ユーザー</td>
   <td>なし</td>
   <td>匿名 Web ユーザーはテンプレートの種類にアクセスできません</td>
  </tr>
 </tbody>
</table>

デフォルトの `template-authors` グループは、プロジェクト設定のみに対応しています。この場合、`template-authors` のすべてのメンバーは、すべてのテンプレートへのアクセスとそれらの作成が許可されています。より複雑な設定では、テンプレートに個別にアクセスするためにテンプレート作成者グループが複数必要になるので、さらに多くのカスタムテンプレート作成者グループを作成する必要があります。ただし、テンプレート作成者グループの権限は変わりません。

## テンプレートタイプ {#template-type}

新しいテンプレートの作成時には、テンプレートタイプを指定する必要があります。

* テンプレートタイプは、テンプレートのためのテンプレートを効果的に提供します。新規テンプレート作成時に選択したテンプレートタイプの構造および初期コンテンツに基づいて、新しいテンプレートが作成されます。

   * テンプレートタイプがコピーされて、テンプレートが作成されます。
   * コピー後のテンプレートとテンプレートタイプとの関連付けは、情報を取得するだけの静的参照のみとなります。

* テンプレートタイプでは、以下の項目を定義できます。

   * ページコンポーネントのリソースタイプ。
   * ルートノードのポリシー。テンプレートエディターで許可されるコンポーネントを定義します。
   * そのテンプレートタイプで、モバイルエミュレーターのレスポンシブグリッドと設定のブレークポイントを定義することをお勧めします。

* AEM には、既製のテンプレートタイプがいくつか用意されています（HTML5 ページ、アダプティブフォームページなど）。

   * その他の例は、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)の一部として提供されます。

* テンプレートタイプは通常、開発者が定義します。

既製のテンプレートタイプは次のフォルダーに保存されています。

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>`/libs` パス内のものは一切変更しないでください。これは、`/libs` のコンテンツが AEM の更新によっていつでも上書きされる可能性があるためです。

サイト固有のテンプレートタイプは、以下に相当する場所に保存してください。

* `/apps/settings/wcm/template-types`

カスタマイズしたテンプレートタイプの定義は、ユーザー定義フォルダー（推奨）または `global` フォルダーに保存してください。例：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>テンプレートタイプは、正しいフォルダー構造（つまり、`/settings/wcm/...`）を遵守する必要があります。遵守しないとテンプレートタイプが見つからなくなります。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating an editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### テンプレートタイプの作成 {#creating-template-types}

他のテンプレートの基盤となるテンプレートを作成した場合、このテンプレートをテンプレートタイプとしてコピーできます。

1. ページテンプレートの場合と同様にテンプレートを作成します。詳しくは、[ページエディターで編集可能なページを作成するテンプレート](/help/sites-cloud/authoring/page-editor/templates.md#creating-a-new-template-template-author)を参照してください。これは、テンプレートタイプの基盤となります。
1. CRXDE Lite を使用して、[テンプレートフォルダー](#template-folders)の `templates` ノードから `template-types` ノードに、作成したテンプレートをコピーします。
1. このテンプレートを[テンプレートフォルダー](#template-folders)の下の `templates` ノードから削除します。
1. `template-types` ノードの下にあるテンプレートのコピーで、すべての `jcr:content` ノードから `cq:template` および `cq:templateType` プロパティをすべて削除します。

また、GitHub で入手できる、編集可能テンプレートのサンプルを基盤として使用し、独自のテンプレートタイプを作成することもできます。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-sites-example-custom-template-type プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)としてダウンロードします

## テンプレート定義 {#template-definitions}

編集可能テンプレートの定義は、[ユーザー定義フォルダー](#template-folders)（推奨）または `global` フォルダーに格納されます。例：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

テンプレートのルートノードは、以下のスケルトン構造を持つ `cq:Template` タイプです。

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主な要素は以下のとおりです。

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

このノードは、テンプレートのプロパティを保持します。

* **名前**：`jcr:title`
* **名前**：`status`
   * ``**型**：`String`
   * **値**：`draft`、`enabled` または `disabled`

### 構造 {#structure}

作成されるページの構造を定義します。

* ページの作成時に初期コンテンツ（`/initial`）と統合されます。
* 構造に加えた変更は、そのテンプレートを使用して作成されたすべてのページに反映されます。
* `root`（`structure/jcr:content/root`）ノードは、作成されたページで使用できるコンポーネントのリストを定義します。
   * テンプレート構造で定義されたコンポーネントは、作成されたページで移動することも、作成されたページから削除することもできません。
   * コンポーネントをロック解除すると、`editable` プロパティが `true` に設定されます。
   * 既にコンテンツを含むコンポーネントをロック解除すると、このコンテンツは `initial` 分岐に移動します。

* `cq:responsive` ノードは、レスポンシブレイアウトの定義を保持します。

### 初期コンテンツ {#initial-content}

作成時に新しいページに表示される初期コンテンツを定義します。

* すべての新しいページにコピーされる `jcr:content` ノードが含まれます。
* ページ作成時に構造（`/structure`）と統合されます。
* 作成後に初期コンテンツが変更されても、既存のページは更新されません。
* `root` ノードにはコンポーネントのリストが格納され、結果として得られるページで使用できるコンポーネントを定義します。
* コンテンツが構造モードでコンポーネントに追加された後、そのコンポーネントがその後アンロックされた場合（またはその逆の場合）、このコンテンツは初期コンテンツとして使用されます。

### レイアウト {#layout}

[テンプレートの編集時にレイアウトを定義できます](/help/sites-cloud/authoring/page-editor/templates.md)。レイアウトには[標準のレスポンシブレイアウト](/help/sites-cloud/administering/responsive-layout.md)（[コンテンツ作成者がページ上で設定できる](/help/sites-cloud/authoring/page-editor/responsive-layout.md)）を使用します。

### コンテンツポリシー {#content-policies}

コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。例えば、使用できるコンポーネントや最小／最大サイズを定義できます。これらのポリシーは、テンプレート（および、そのテンプレートを使用して作成されるページ）に適用されます。コンテンツポリシーは、テンプレートエディターで作成および選択できます。

* `root` ノード上の `cq:policy` プロパティ
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
ページの段落システムのコンテンツポリシーに対する相対参照を提供します。

* `root` の下のコンポーネントを明示的に示すノードの `cq:policy` プロパティは、個々のコンポーネントのポリシーへのリンクを提供します。

* 実際のポリシー定義は、次の場所に保存されます。
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>ポリシー定義のパスは、コンポーネントのパスによって異なります。`cq:policy` は、設定自体への相対参照を保持します。

### ページポリシー {#page-policies}

ページポリシーを使用して、テンプレートまたは作成されるページで、ページ（メインの parsys）の[コンテンツポリシー](#content-policies)を定義できます。

### 使用するテンプレートの有効化と許可 {#enabling-and-allowing-a-template-for-use}

1. **テンプレートを有効にする**

   テンプレートを使用する前に、次のいずれかの方法で有効にする必要があります。

   * **テンプレート**&#x200B;コンソールから[テンプレートを有効に](/help/sites-cloud/authoring/page-editor/templates.md)します。

   * `jcr:content` ノードの status プロパティを設定する。

      * 例：
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 次のプロパティを定義します。

         * 名前：ステータス
         * タイプ：String
         * 値：`enabled`

1. **許可されたテンプレート**

   * [適切なページまたはサブブランチのルートページの&#x200B;**ページプロパティ**](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author)&#x200B;に対して許可されたテンプレートのパスを定義します。
   * プロパティを設定します。
     `cq:allowedTemplates`
必要なブランチの `jcr:content` ノードに設定します。

   例えば、次の値を使用します。

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 作成されるコンテンツページ {#resultant-content-pages}

編集可能テンプレートから作成されるページには、次の特徴があります。

* テンプレートの `structure` と `initial` を統合したサブツリーを使用して作成されます。

* テンプレートおよびテンプレートタイプに保持されている情報への参照を保持します。これは、次のプロパティを持つ `jcr:content` ノードを使用して行います。

   * `cq:template` - 実際のテンプレートへの動的参照を提供します。テンプレートへの変更を実際のページに反映させることができます。

   * `cq:templateType` - テンプレートタイプへの参照を提供します。

![テンプレート、コンテンツ、コンポーネントの相互関係](assets/templates-content-components.png)

上の図は、テンプレート、コンテンツおよびコンポーネントの相関関係を示したものです。

* コントローラー - `/content/<my-site>/<my-page>` - テンプレートを参照して作成されるページです。コンテンツがプロセス全体を制御します。定義に従って、適切なテンプレートとコンポーネントにアクセスします。
* 設定 - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - ページ設定を定義する[テンプレートおよび関連するコンテンツポリシー](#template-definitions)です。
* モデル - OSGi バンドル - [OSGI バンドル](/help/implementing/deploying/configuring-osgi.md)が機能を実装します。
* 表示 - `/apps/<my-site>/components` - オーサー環境と公開環境の両方で、コンテンツがコンポーネントによってレンダリングされます。

ページのレンダリング時：

* **テンプレート**:

   * `jcr:content` ノードの `cq:template` プロパティが、そのページに対応するテンプレートにアクセスするために参照されます。

* **コンポーネント**:

   * ページコンポーネントは、テンプレートの `structure/jcr:content` ツリーとページの `jcr:content` ツリーを統合します。
      * 作成者は、ページコンポーネントを使用して、編集可能のフラグが設定されているテンプレート構造のノード（およびいずれかの子）のみを編集できます。
      * ページでコンポーネントをレンダリングする際、そのコンポーネントの相対パスが `jcr:content` ノードから取得されます。その後、テンプレートの `policies/jcr:content` ノードの下の同じパスが検索されます。
         * このノードの `cq:policy` プロパティは、実際のコンテンツポリシーを指します（すなわち、このプロパティは、そのコンポーネントのデザイン設定を保持しています）。
            * このため、同じコンテンツポリシー設定を再利用する複数のテンプレートを持つことができます。

### 使用可能なテンプレート {#template-availability}

サイト管理インターフェイスでページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、新しいページをページ `P` の子として配置する場合に、テンプレート `T` を使用できるかどうかを決定します。これらの各プロパティは、0 個以上の正規表現を保持する複数値の文字列で、パスの照合に使用されます。

* `jcr:content` サブノードの `P` または `P` の上位ページの `cq:allowedTemplates` プロパティ。

* `T` の `allowedPaths` プロパティ。

* `T` の `allowedParents` プロパティ。

* `P` のテンプレートの `allowedChildren` プロパティ。

評価は次のように行われます。

* `P` で始まるページ階層を昇順にしているときに見つかった、最初の空でない `cq:allowedTemplates` プロパティは、`T` のパスと一致します。一致する値がない場合、`T` は拒否されます。

* `T` に空でない `allowedPaths` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* 上記のプロパティの両方が空または存在しない場合、`P` と同じアプリケーションに属さない限り、`T` は拒否されます。`T` は、`T` のパスの 2 番目のレベルの名前が `P` のパスの 2 番目のレベルの名前と同じである場合に限り、`P` と同じアプリケーションに属します。例えば、テンプレート `/apps/wknd/templates/foo` は、ページ `/content/wknd` と同じアプリに属しています。

* `T` に空でない `allowedParents` プロパティがあるものの、`P` のパスと一致する値がない場合、`T` は拒否されます。

* `P` のテンプレートに空でない `allowedChildren` プロパティがあるものの、`T` のパスと一致する値がない場合、`T` は拒否されます。

* その他すべての場合は、`T` は許可されます。

以下の図は、テンプレートの評価プロセスを示しています。

![テンプレート評価プロセス](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM は、複数のプロパティをオファーして、**Sites** で許可されるテンプレートを制御します。ただし、組み合わせることで非常に複雑なルールになり、追跡や管理が困難になる可能性があります。
>
>したがって、アドビでは、次の項目を定義して、単純に開始することをお勧めします。
>
>* プロパティは `cq:allowedTemplates` のみ
>
>* サイトのルートにのみ
>
>例については、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)のコンテンツ `/content/wknd/jcr:content` を参照してください。
>
>プロパティ `allowedPaths`、`allowedParents`、`allowedChildren` をテンプレートに配置して、より高度なルールを定義することもできます。ただし、可能な場合、許可されるテンプレートをさらに制限する必要がある場合は、サイトのサブセクションでさらに `cq:allowedTemplates` プロパティを定義する方が&#x200B;*はるかに*&#x200B;簡単です。
>
>また、**ページプロパティ**&#x200B;の「**詳細**」タブで、作成者が `cq:allowedTemplates` プロパティを更新できるという利点もあります。その他のテンプレートプロパティは、（標準）UI を使用して更新することはできないので、変更するたびに、ルールとコードのデプロイメントを管理する開発者が必要になります。

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります（`/apps/wknd/templates/page-content` など）。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての作成されたページにこの設定を適用できます。

例えばテンプレート階層に対してさらに制約を追加する場合は、テンプレートの `allowedParents/allowedChildren` プロパティを使用できます。その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。
