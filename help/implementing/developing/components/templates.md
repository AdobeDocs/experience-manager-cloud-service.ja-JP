---
title: ページテンプレート
description: ページテンプレートは、新しいページのベースとして使用するページを作成する際に使用します
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 77%

---

# ページテンプレート {#page-templates}

ページを作成する場合は、テンプレートを選択する必要があります。ページテンプレートは、新しいページのベースとして使用されます。テンプレートによって、結果ページの構造、すべての初期コンテンツ、使用可能なコンポーネント（設計プロパティ）が定義されます。これには、次のようないくつかの利点があります。

* ページテンプレートによって、専門的な作成者が[テンプレートを作成および編集](/help/sites-cloud/authoring/features/templates.md)できます。
   * このような専門的な作成者は、**テンプレート作成者**&#x200B;と呼ばれます。
   * テンプレート作成者は、`template-authors` グループのメンバーである必要があります。
* ページテンプレートから作成されたすべてのページとページテンプレートとの動的な接続が保持されます。これにより、テンプレートに対するあらゆる変更がページに反映されます。
* ページテンプレートによって、ページコンポーネントの汎用性が高まり、核となるページコンポーネントをカスタマイズなしで使用できます。

ページテンプレートを使用すると、ページの構成要素がコンポーネント内で分離されます。UI で必要なコンポーネントの組み合わせを設定できるので、ページのバリエーションごとに新しいページコンポーネントを開発する必要はなくなります。

このドキュメントでは、

* ページテンプレートの作成の概要を示します。
* 編集可能なテンプレートの作成に必要な管理者/開発者のタスクについて説明します
* 編集可能なテンプレートの技術的基礎について説明します
* AEM がテンプレートの利用可能性を評価する方法について説明します

>[!NOTE]
>
>このドキュメントでは、テンプレートの作成と編集について既に理解していることを前提としています。オーサリングに関するドキュメント[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md)を参照してください。ここでは、テンプレート作成者に公開されている編集可能テンプレートの機能について詳しく説明されています。

>[!TIP]
>
>[WKND のチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、例を実装してページテンプレートの使用方法を詳しく説明しているので、新しいプロジェクトでのテンプレートの設定方法を理解するのに非常に役立ちます。

## 新しいテンプレートの作成 {#creating-a-new-template}

ページテンプレートの作成は、主にテンプレート作成者が、[テンプレートコンソールおよびテンプレートエディター](/help/sites-cloud/authoring/features/templates.md)を使用して行います。ここでは、そのプロセスの概要を示し、技術的なレベルでどのような処理が行われるかを説明します。

新しい編集可能テンプレートを作成する場合は、次の手順を実行します。

1. の作成 [テンプレート用のフォルダー](#template-folders). これは必須ではありませんが、推奨されるベストプラクティスです。
1. [テンプレートタイプ](#template-type)を選択します。[テンプレート定義](#template-definitions)を作成するために、このタイプがコピーされます。

   >[!NOTE]
   >
   >選択したテンプレートタイプが標準で提供されます。 また、 [独自のサイト固有のテンプレートタイプを作成する](#creating-template-types) （必要に応じて）

1. 新しいテンプレートの構造、コンテンツポリシー、初期コンテンツ、レイアウトを設定します。

   **構造**

   * 構造を使用して、テンプレートのコンポーネントとコンテンツを定義できます。
   * テンプレート構造で定義されたコンポーネントは、結果ページに移動することも、結果ページから削除することもできません。
   * ページ作成者がコンポーネントを追加および削除できるようにするには、テンプレートに段落システムを追加します。
   * コンポーネントのロックを解除（再度ロックできます）して、初期コンテンツを定義できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)を参照してください。

   構造の技術的な詳細については、このドキュメントの[構造](#structure)を参照してください。

   **ポリシー**

   * コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。

      * 例えば、使用できるコンポーネントや最小／最大サイズを定義できます。

   * これらは、テンプレート（およびテンプレートを使用して作成されたページ）に適用できます。

   テンプレート作成者がポリシーを定義する方法について詳しくは、 [ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   ポリシーの技術的な詳細については、このドキュメントの[コンテンツポリシー](#content-policies)を参照してください。

   **初期コンテンツ**

   * 初期コンテンツは、テンプレートに基づいてページが最初に作成されたときに表示されるコンテンツを定義します。
   * その後、ページ作成者が初期コンテンツを編集できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)を参照してください。

   初期コンテンツの技術的な詳細については、 [初期コンテンツ](#initial-content) 」を参照してください。

   **レイアウト**

   * デバイスの形式に合わせてテンプレートのレイアウトを定義できます。
   * テンプレートがページオーサリングと同じように動作するには、レスポンシブレイアウトを使用します。

   テンプレート作成者がテンプレートレイアウトを定義する方法について詳しくは、 [ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   テンプレートのレイアウトの技術的な詳細については、 [レイアウト](#layout) 」を参照してください。

1. テンプレートを有効にして、特定のコンテンツツリーに対して許可します。

   * テンプレートを有効または無効にして、ページ作成者が使用できるようにしたり、使用できなくしたりできます。
   * テンプレートは、特定のページブランチに対して使用可能または使用不可にすることができます。

   テンプレート作成者によるテンプレートの有効化方法について詳しくは、 [ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   テンプレートの有効化の技術的な詳細については、このドキュメントの[使用するテンプレートの有効化と許可](#enabling-and-allowing-a-template-for-use)を参照してください。

1. テンプレートを使用してコンテンツページを作成します。

   * テンプレートを新しいページを作成するために使用するときは、静的テンプレートと編集可能なテンプレートの間に視覚的な違いはありません。
   * ページの作成者にとって、この処理は透過的です。

   ページ作成者がテンプレートを使用してページを作成する方法について詳しくは、[ページの作成と整理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates)を参照してください。

   編集可能テンプレートを使用したページ作成の技術的な詳細については、このドキュメントの[作成されるコンテンツページ](#resultant-content-pages)を参照してください。

>[!TIP]
>
>国際化する必要がある情報は、テンプレートに含めないでください。国際化のためには、[コアコンポーネントのローカライゼーション機能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=ja)の利用をお勧めします。

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

標準の AEM インスタンスでは、テンプレートコンソールに既に `global` フォルダーが存在します。この中にデフォルトのテンプレートが格納されており、現在のフォルダーにポリシーやテンプレートタイプがない場合にはフォールバックとして機能します。このフォルダーにデフォルトのテンプレートを追加するか、新しいフォルダーを作成できます（推奨）。

>[!NOTE]
>
>カスタマイズしたテンプレートを格納する新しいフォルダーを作成し、`global` フォルダーは使用しないことをお勧めします。

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

新しいフォルダーを作成するには、次のいずれかを実行します。

* プログラムによる、またはCRXDE Lite
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

1. 次のプロパティをフォルダールートノードに定義できます。

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

   * **タイトル**:設定フォルダーのタイトルを指定します
   * **編集可能なテンプレート**:このフォルダ内で編集可能なテンプレートを許可する場合はチェックマークを付けます

1. クリック **作成**

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

デフォルトの `template-authors` グループは、プロジェクト設定のみに対応しています。この場合、`template-authors` のすべてのメンバーは、すべてのテンプレートへのアクセスとそれらの作成が許可されています。より複雑な設定では、テンプレートへのアクセスを分離するために複数のテンプレート作成者グループが必要な場合、より多くのカスタムテンプレート作成者グループを作成する必要があります。 ただし、テンプレート作成者グループの権限は同じです。

## テンプレートタイプ {#template-type}

新しいテンプレートの作成時には、テンプレートタイプを指定する必要があります。

* テンプレートタイプは、テンプレートのテンプレートを効果的に提供します。 新しいテンプレートを作成する際、選択したテンプレートタイプの構造と初期コンテンツを使用して、新しいテンプレートが作成されます。

   * テンプレートタイプがコピーされて、テンプレートが作成されます。
   * コピーが実行されると、テンプレートとテンプレートタイプの間の接続は、情報を提供するための静的参照のみになります。

* テンプレートタイプを使用して、次の項目を定義できます。

   * ページコンポーネントのリソースタイプ。
   * ルートノードのポリシー。テンプレートエディターで許可されるコンポーネントを定義します。
   * そのテンプレートタイプで、モバイルエミュレーターのレスポンシブグリッドと設定のブレークポイントを定義することをお勧めします。

* AEM には、既製のテンプレートタイプがいくつか用意されています（HTML5 ページ、アダプティブフォームページなど）。

   * その他の例は、 [WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* テンプレートタイプは、通常、開発者が定義します。

既製のテンプレートタイプは次のフォルダーに保存されています。

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>`/libs` パス内のものは一切変更しないでください。これは、`/libs` のコンテンツが AEM の更新によっていつでも上書きされる可能性があるためです。

サイト固有のテンプレートタイプは、以下に相当する場所に保存してください。

* `/apps/settings/wcm/template-types`

カスタマイズしたテンプレートタイプの定義は、ユーザー定義フォルダー（推奨）または `global` フォルダーに保存してください。次に例を示します。

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>テンプレートタイプは、正しいフォルダー構造 ( つまり、 `/settings/wcm/...`) が含まれていない場合、テンプレートタイプが見つかりません。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

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

1. [こちらのドキュメント](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)で説明されているページテンプレートと同じようにテンプレートを作成します。これは、テンプレートタイプの基盤となります。
1. CRXDE Liteを使用して、新しく作成したテンプレートを `templates` ノードから `template-types` ノードの [テンプレートフォルダー](#template-folders).
1. このテンプレートを[テンプレートフォルダー](#template-folders)の下の `templates` ノードから削除します。
1. `template-types` ノードの下にあるテンプレートのコピーで、すべての `jcr:content` ノードから `cq:template` および `cq:templateType` プロパティをすべて削除します。

また、GitHub で入手できる、編集可能テンプレートのサンプルを基盤として使用し、独自のテンプレートタイプを作成することもできます。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-sites-example-custom-template-type プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)としてダウンロードします

## テンプレート定義 {#template-definitions}

編集可能テンプレートの定義は、[ユーザー定義フォルダー](#template-folders)（推奨）または `global` フォルダーに格納されます。次に例を示します。

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

* 新しいページの作成時に初期コンテンツ（`/initial`）と統合されます。
* 構造に加えた変更は、そのテンプレートで作成されたすべてのページに反映されます。
* この `root` ( `structure/jcr:content/root`) ノードは、作成されたページで使用できるコンポーネントのリストを定義します。
   * テンプレート構造で定義されたコンポーネントは、作成されたページで移動することも、作成されたページから削除することもできません。
   * コンポーネントをロック解除した後、 `editable` プロパティをに設定します。 `true`.
   * 既にコンテンツを含むコンポーネントをロック解除すると、そのコンテンツは `initial` 分岐。

* `cq:responsive` ノードは、レスポンシブレイアウトの定義を保持します。

### 初期コンテンツ {#initial-content}

作成時に新しいページに表示される初期コンテンツを定義します。

* すべての新しいページにコピーされる `jcr:content` ノードが含まれます。
* 新しいページの作成時に構造（`/structure`）と統合されます。
* 作成後に初期コンテンツが変更されても、既存のページはすべて更新されません。
* この `root` ノードは、作成されたページで使用可能なコンポーネントを定義する、コンポーネントのリストを保持します。
* コンテンツが構造モードでコンポーネントに追加され、その後、そのコンポーネントがロック解除された場合（またはコンポーネントのロック解除後にコンテンツが追加された場合）、このコンテンツは初期コンテンツとして使用されます。

### レイアウト {#layout}

[テンプレートを編集する際に、レイアウトを定義できます](/help/sites-cloud/authoring/features/templates.md)。これには、[標準のレスポンシブレイアウト](/help/sites-cloud/authoring/features/responsive-layout.md)が使用されます。

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### コンテンツポリシー {#content-policies}

コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。例えば、使用できるコンポーネントや最小／最大サイズを定義できます。これらは、テンプレート（およびテンプレートを使用して作成されたページ）に適用できます。 コンテンツポリシーは、テンプレートエディターで作成および選択できます。

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

ページポリシーを使用すると、 [コンテンツポリシー](#content-policies) （メイン parsys）ページの場合は、テンプレートまたは結果ページのいずれか。

### テンプレートの使用の有効化と許可 {#enabling-and-allowing-a-template-for-use}

1. **テンプレートの有効化**

   テンプレートを使用する前に、次のいずれかの方法で有効にする必要があります。

   * [テンプレートの有効化](/help/sites-cloud/authoring/features/templates.md) から **テンプレート** コンソール。

   * `jcr:content` ノードの status プロパティを設定する。

      * 例：
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * プロパティを定義します。

         * 名前：ステータス
         * タイプ：String
         * 値：`enabled`

1. **許可されたテンプレート**

   * [適切なページまたはサブブランチのルートページの&#x200B;**ページプロパティ**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author)&#x200B;に対して許可されたテンプレートのパスを定義します。
   * プロパティを設定します。
     `cq:allowedTemplates` 
を必要なブランチの `jcr:content` ノードに設定します。

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

ページをレンダリングする際の動作：

* **テンプレート**:

   * この `cq:template` 財産 `jcr:content` ノードが参照され、そのページに対応するテンプレートにアクセスできます。

* **コンポーネント**:

   * ページコンポーネントは、テンプレートの `structure/jcr:content` ツリーとページの `jcr:content` ツリーを統合します。
      * ページコンポーネントを使用すると、作成者は、「編集可能」のフラグが設定されたテンプレート構造のノード（およびその他の子）の編集のみ可能になります。
      * ページ上にコンポーネントをレンダリングすると、そのコンポーネントの相対パスは `jcr:content` ノード；下の同じ道 `policies/jcr:content` その後、テンプレートのノードが検索されます。
         * この `cq:policy` このノードのプロパティは、実際のコンテンツポリシーを指します（つまり、このプロパティは、そのコンポーネントのデザイン設定を保持しています）。
            * このため、同じコンテンツポリシー設定を再利用する複数のテンプレートを持つことができます。

### 使用可能なテンプレート {#template-availability}

サイト管理インターフェイスで新しいページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

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

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。例えば、`/apps/wknd/templates/page-content` リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての新規作成ページにこの設定を適用できます。

テンプレート階層に関する制約などをさらに追加する場合は、テンプレートの `allowedParents/allowedChildren` プロパティを使用できます。その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。
