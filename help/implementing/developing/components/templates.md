---
title: ページテンプレート
description: ページテンプレートは、新しいページのベースとして使用するページを作成する際に使用します
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '3228'
ht-degree: 98%

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
* 編集可能テンプレートの作成に必要な管理者／開発者のタスク
* 編集可能テンプレートの技術基盤
* AEM がテンプレートの利用可能性を評価する方法について説明します

>[!NOTE]
>
>このドキュメントでは、テンプレートの作成と編集について既に理解していることを前提としています。オーサリングに関するドキュメント[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md)を参照してください。ここでは、テンプレート作成者に公開されている編集可能テンプレートの機能について詳しく説明されています。

>[!TIP]
>
>[WKND のチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)では、例を実装してページテンプレートの使用方法を詳しく説明しているので、新しいプロジェクトでのテンプレートの設定方法を理解するのに非常に役立ちます。

## 新しいテンプレートの作成 {#creating-a-new-template}

ページテンプレートの作成は、主にテンプレート作成者が、[テンプレートコンソールおよびテンプレートエディター](/help/sites-cloud/authoring/features/templates.md)を使用しておこないます。ここでは、そのプロセスの概要を示し、技術的なレベルでどのような処理がおこなわれるかを説明します。

新しい編集可能テンプレートを作成する場合は、次の手順を実行します。

1. [テンプレート用のフォルダー](#template-folders)を作成します。これは必須ではありませんが、推奨されるベストプラクティスです。
1. [テンプレートタイプ](#template-type)を選択します。[テンプレート定義](#template-definitions)を作成するために、このタイプがコピーされます。

   >[!NOTE]
   >
   >様々なテンプレートタイプが標準で提供されています。必要に応じて、[独自のサイト固有のテンプレートタイプを作成する](#creating-template-types)こともできます。

1. 新しいテンプレートの構造、コンテンツポリシー、初期コンテンツおよびレイアウトを設定します。

   **構造**

   * 構造では、テンプレートのコンポーネントとコンテンツを定義できます。
   * テンプレート構造で定義されたコンポーネントは、結果ページに移動することも、結果ページから削除することもできません。
   * ページ作成者がコンポーネントを追加または削除するには、テンプレートに段落システムを追加する必要があります。
   * コンポーネントのロックを解除（再度ロックできます）して、初期コンテンツを定義できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)を参照してください。

   構造の技術的な詳細については、このドキュメントの[構造](#structure)を参照してください。

   **ポリシー**

   * コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。

      * 例えば、使用できるコンポーネントや最小／最大サイズを定義できます。
   * これらのポリシーは、テンプレートと、そのテンプレートを使用して作成されるページに適用されます。

   テンプレート作成者がポリシーを定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)を参照してください。

   ポリシーの技術的な詳細については、このドキュメントの[コンテンツポリシー](#content-policies)を参照してください。

   **初期コンテンツ**

   * 初期コンテンツでは、テンプレートに基づいてページが最初に作成されたときに表示されるコンテンツを定義します。
   * その後、ページ作成者が初期コンテンツを編集できます。

   テンプレート作成者が構造を定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)を参照してください。

   初期コンテンツの技術的な詳細については、このドキュメントの[初期コンテンツ](#initial-content)を参照してください。

   **レイアウト**

   * デバイスの形式に合わせてテンプレートのレイアウトを定義できます。
   * テンプレートがページオーサリングと同じように動作するには、レスポンシブレイアウトを使用します。

   テンプレート作成者がテンプレートレイアウトを定義する方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)を参照してください。

   テンプレートレイアウトの技術的な詳細については、このドキュメントの[レイアウト](#layout)を参照してください。

1. テンプレートを有効化し、特定のコンテンツツリーに対して許可します。

   * テンプレートを有効にするか無効して、ページ作成者による使用可否を決めることができます。
   * テンプレートは、特定のページブランチに対して使用可能または使用不可にすることができます。

   テンプレート作成者がテンプレートを有効にする方法について詳しくは、[ページテンプレートの作成](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)を参照してください。

   テンプレートの有効化の技術的な詳細については、このドキュメントの[使用するテンプレートの有効化と許可](#enabling-and-allowing-a-template-for-use)を参照してください。

1. テンプレートを使用してコンテンツページを作成します。

   * テンプレートを新しいページを作成するために使用するときは、静的テンプレートと編集可能なテンプレートの間に視覚的な違いはありません。
   * ページの作成者にとって、この処理は透過的です。

   ページ作成者がテンプレートを使用してページを作成する方法について詳しくは、[ページの作成と整理](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates)を参照してください。

   編集可能テンプレートを使用したページ作成の技術的な詳細については、このドキュメントの[作成されるコンテンツページ](#resultant-content-pages)を参照してください。

>[!NOTE]
>
>エディタークライアントライブラリは、コンテンツページに `cq.shared` 名前空間が存在することを前提としています。名前空間が存在しない場合は、JavaScript エラー「`Uncaught TypeError: Cannot read property 'shared' of undefined`」が発生します。
>
>すべてのサンプルコンテンツページには `cq.shared` が含まれているので、それらをベースとするコンテンツには自動的に `cq.shared` が含められます。ただし、サンプルコンテンツをベースとせず、ゼロから独自のコンテンツページを作成する場合は、`cq.shared` 名前空間を含める必要があります。
>
>詳しくは、[クライアントサイドライブラリの使用](/help/implementing/developing/introduction/clientlibs.md)を参照してください。

>[!CAUTION]
>
>国際化する必要がある情報は、テンプレートに含めないでください。

## テンプレートフォルダー {#template-folders}

以下のフォルダーを使用してテンプレートを整理できます。

* `global`
* サイト固有

>[!NOTE]
>
>フォルダーはネストできますが、**テンプレート**&#x200B;コンソールで表示すると、フラット構造として表されます。

標準の AEM インスタンスでは、テンプレートコンソールに既に `global` フォルダーが存在します。この中にデフォルトのテンプレートが格納されており、現在のフォルダーにポリシーやテンプレートタイプがない場合にはフォールバックとして機能します。このフォルダーにデフォルトのテンプレートを追加することも、新しいフォルダーを作成すること（推奨）もできます。

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

新しいフォルダーを作成するには、次のいずれかの方法を使用できます。

* プログラムで自動的に、または CRXDE Lite を使用して作成する
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

1. 作成者が新しいフォルダーにテンプレートを作成できるようにするには、標準のオーサリング権限（`content-authors` など）に加え、グループを割り当てて作成者に必要なアクセス権限（ACL）を定義する必要があります。

   割り当てる必要があるデフォルトのグループは、`template-authors` グループです。詳しくは、[ACL とグループ](#acls-and-groups)の節を参照してください。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 設定ブラウザーの使用 {#using-the-configuration-browser}

1. **グローバルナビゲーション**／**ツール**／[**設定ブラウザー**&#x200B;に移動します。](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

   `global` フォルダーなどの既存のフォルダーは左側に一覧表示されます。

1. 「**作成**」をクリックします。
1. **設定を作成**&#x200B;ダイアログで、以下のフィールドを設定する必要があります。

   * **タイトル**：設定フォルダーのタイトルを指定します。
   * **編集可能なテンプレート**：このフォルダー内で編集可能テンプレートを許可する場合にチェックします。

1. 「**作成**」をクリックします。

>[!NOTE]
>
>[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)で、グローバルフォルダーを編集し、このフォルダー内にテンプレートを作成する場合は、**編集可能なテンプレート**&#x200B;オプションをアクティブにできますが、ベストプラクティスは推奨されません。

### ACL とグループ {#acls-and-groups}

（CRXDE または設定ブラウザーを使用して）テンプレートフォルダーが作成されたら、セキュリティを確保するために、テンプレートフォルダーの適切なグループに ACL を定義する必要があります。

例として、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)のテンプレートフォルダーを使用できます。

#### template-authors グループ {#the-template-authors-group}

`template-authors` グループは、テンプレートへのアクセスを管理するために使用されるグループで、AEM に標準で付属していますが空です。ユーザーは、プロジェクト／サイトのグループに追加する必要があります。

>[!CAUTION]
>
>`template-authors` グループは、新しいテンプレートを作成する必要があるユーザー専用です。
>
>テンプレートの編集は非常に強力なので、正しくおこなわないと既存のテンプレートが壊れる場合があります。そのため、この役割には注意深く、ふさわしいユーザーだけを含めてください。

次の表に、テンプレートの編集に必要な権限の詳細を示します。

<table>
 <tbody>
  <tr>
   <th>パス</th>
   <th>役割／グループ</th>
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

* テンプレートタイプは、テンプレートのためのテンプレートとなるものです。テンプレート作成時に選択したテンプレートタイプの構造と初期コンテンツに基づいて、新しいテンプレートが作成されます。

   * テンプレートはテンプレートタイプをコピーして作成されます。
   * コピー後のテンプレートとテンプレートタイプとの関連付けは、情報を取得するだけの静的参照のみとなります。

* テンプレートタイプでは、以下の項目を定義できます。

   * ページコンポーネントのリソースタイプ。
   * ルートノードのポリシー。テンプレートエディターで許可されるコンポーネントを定義します。
   * そのテンプレートタイプで、モバイルエミュレーターのレスポンシブグリッドと設定のブレークポイントを定義することをお勧めします。

* AEM には、既製のテンプレートタイプがいくつか用意されています（HTML5 ページ、アダプティブフォームページなど）。

   * その他の例は、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)の一部として提供されています。

* テンプレートタイプは通常、開発者が定義します。

既製のテンプレートタイプは次のフォルダーに保存されています。

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>`/libs` パス内の設定は一切変更しないでください。これは、`/libs` のコンテンツが AEM の更新によっていつでも上書きされる可能性があるためです。

サイト固有のテンプレートタイプは、以下に相当する場所に保存してください。

* `/apps/settings/wcm/template-types`

カスタマイズしたテンプレートタイプの定義は、ユーザー定義フォルダー（推奨）または `global` フォルダーに保存してください。次に例を示します。

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>テンプレートタイプの保存は、正しいフォルダー構造（`/settings/wcm/...`）に従う必要があります。そうしないと、テンプレートタイプが見つからなくなります。

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
1. CRXDE Lite を使用している場合は、新しく作成したテンプレートを `templates` ノードから`template-types`テンプレートフォルダー[の下の ](#template-folders) ノードにコピーします。
1. このテンプレートを[テンプレートフォルダー](#template-folders)の下の `templates` ノードから削除します。
1. `template-types` ノードの下にあるテンプレートのコピーで、`cq:template` および `cq:templateType` `jcr:content` プロパティをすべて削除します。

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
* 構造に加えた変更は、そのテンプレートを使用して作成されたすべてのページに反映されます。
* `structure/jcr:content/root`（`root`）ノードは、作成されたページで使用できるコンポーネントのリストを定義します。
   * テンプレート構造で定義されたコンポーネントは、作成されたページで移動することも、作成されたページから削除することもできません。
   * コンポーネントをロック解除すると、`editable` プロパティが `true` に設定されます。
   * 既にコンテンツを含むコンポーネントをロック解除すると、このコンテンツは `initial` ブランチに移動されます.

* `cq:responsive` ノードは、レスポンシブレイアウトの定義を保持します。

### 初期コンテンツ {#initial-content}

作成時に新しいページに表示される初期コンテンツを定義します。

* すべての新しいページにコピーされる `jcr:content` ノードが含まれます。
* 新しいページの作成時に構造（`/structure`）と統合されます。
* 作成後に初期コンテンツが変更されても、既存のページはすべて更新されません。
* `root` ノードは、作成されたページで使用できるコンポーネントを定義する、コンポーネントのリストを保持します。
* コンテンツが構造モードでコンポーネントに追加され、その後、そのコンポーネントがロック解除された場合（またはコンポーネントのロック解除後にコンテンツが追加された場合）、このコンテンツは初期コンテンツとして使用されます。

### レイアウト {#layout}

[テンプレートを編集する際に、レイアウトを定義できます](/help/sites-cloud/authoring/features/templates.md)。これには、[標準のレスポンシブレイアウト](/help/sites-cloud/authoring/features/responsive-layout.md)が使用されます。

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### コンテンツポリシー {#content-policies}

コンテンツポリシーでは、コンポーネントのデザインプロパティを定義します。例えば、使用できるコンポーネントや最小／最大サイズを定義できます。これらのポリシーは、テンプレートと、そのテンプレートを使用して作成されるページに適用されます。テンプレートエディターでコンテンツポリシーを作成して選択できます。

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

### 使用するテンプレートの有効化と許可  {#enabling-and-allowing-a-template-for-use}

1. **テンプレートの有効化**

   テンプレートは、次のどちらかの方法で有効化してからでなければ使用できません。

   * **テンプレート**&#x200B;コンソールから[テンプレートを有効化](/help/sites-cloud/authoring/features/templates.md)する。

   * `jcr:content` ノードの status プロパティを設定する。

      * 例：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * プロパティの定義

         * 名前：status
         * タイプ：String
         * 値：`enabled`

1. **許可されたテンプレート**

   * 適切なページまたはサブブランチのルートページの[**ページプロパティ**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author)&#x200B;に対して許可されたテンプレートのパスを定義します。
   * プロパティを設定します。
      `cq:allowedTemplates` 
を 
必要なブランチの `jcr:content` ノードに設定します。
   例えば、次の値を使用します。

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 作成されるコンテンツページ {#resultant-content-pages}

編集可能テンプレートから作成されるページには、次の特徴があります。

* テンプレートの `structure` と `initial` を統合したサブツリーを使用して作成されます。

* テンプレートおよびテンプレートタイプに保持されている情報への参照を保持します。これは、次のプロパティを持つ `jcr:content` ノードを使用しておこないます。

   * `cq:template` - 実際のテンプレートへの動的参照を提供します。テンプレートへの変更を実際のページに反映させることができます。

   * `cq:templateType` - テンプレートタイプへの参照を提供します。

![テンプレート、コンテンツ、コンポーネントの相互関係](assets/templates-content-components.png)

上の図は、テンプレート、コンテンツおよびコンポーネントの相関関係を示したものです。

* コントローラー - `/content/<my-site>/<my-page>` - テンプレートを参照して作成されるページです。コンテンツがプロセス全体を制御します。定義に従って、適切なテンプレートとコンポーネントにアクセスします。
* 設定 - `/conf/<my-folder>/settings/wcm/templates/<my-template>` - ページ設定を定義する[テンプレートおよび関連するコンテンツポリシー](#template-definitions)です。
* モデル - OSGi バンドル - [OSGI バンドル](/help/implementing/deploying/configuring-osgi.md)が機能を実装します。
* 表示 - `/apps/<my-site>/components` - オーサー環境とパブリッシュ環境の両方で、コンテンツがコンポーネントによってレンダリングされます。

ページのレンダリング時

* **テンプレート**:

   * `cq:template` ノードの `jcr:content` プロパティが、そのページに対応するテンプレートにアクセスするために参照されます。

* **コンポーネント**:

   * ページコンポーネントは、テンプレートの `structure/jcr:content` ツリーとページの `jcr:content` ツリーを統合します。
      * 作成者は、ページコンポーネントを使用して、「編集可能」のフラグが設定されているテンプレート構造のノード（およびいずれかの子）を編集できるだけです。
      * ページ上にコンポーネントをレンダリングする際、そのコンポーネントの相対パスが `jcr:content` ノードから取得されます。その後、テンプレートの `policies/jcr:content` ノードの下の同じパスが検索されます。
         * このノードの `cq:policy` プロパティは、実際のコンテンツポリシーを指します（すなわち、このプロパティは、そのコンポーネントのデザイン設定を保持しています）。
            * このため、同じコンテンツポリシー設定を再利用する複数のテンプレートを持つことができます。

### Template Availability {#template-availability}

サイト管理インターフェイスで新しいページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、新しいページをページ `P` の子として配置する場合に、テンプレート `T` を使用できるかどうかを決定します。これらの各プロパティは、0 個以上の正規表現を保持する複数値の文字列で、パスの照合に使用されます。

* `jcr:content` サブノードの `P` または `P` の上位ページの `cq:allowedTemplates` プロパティ。

* `T` の `allowedPaths` プロパティ。

* `T` の `allowedParents` プロパティ。

* `P` のテンプレートの `allowedChildren` プロパティ。

評価は次のようにおこなわれます。

* `P` で始まるページ階層を昇順にしているときに見つかった、最初の空でない `cq:allowedTemplates` プロパティは、`T` のパスと一致します。一致する値がない場合、`T` は拒否されます。

* `T` に空でない `allowedPaths` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* 上記のプロパティの両方が空または存在しない場合、`P` と同じアプリケーションに属さない限り、`T` は拒否されます。`T` は、`T` のパスの 2 番目のレベルの名前が `P` のパスの 2 番目のレベルの名前と同じである場合に限り、`P` と同じアプリケーションに属します。例えば、テンプレート `/apps/geometrixx/templates/foo` は、ページ `/content/geometrixx` と同じアプリに属しています。

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
   >
* サイトのルートにのみ
>
>
例については、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)のコンテンツ `/content/wknd/jcr:content` を参照してください。
>
>プロパティ `allowedPaths`、`allowedParents`、`allowedChildren` をテンプレートに配置して、より高度なルールを定義することもできます。ただし、可能な場合、許可されるテンプレートをさらに制限する必要がある場合は、サイトのサブセクションでさらに `cq:allowedTemplates` プロパティを定義する方が&#x200B;*はるかに*&#x200B;簡単です。
>
>また、**ページプロパティ**&#x200B;の「**詳細**」タブで、作成者が `cq:allowedTemplates` プロパティを更新できるという利点もあります。その他のテンプレートプロパティは、（標準）UI を使用して更新することはできないので、変更するたびに、ルールとコードのデプロイメントを管理する開発者が必要になります。

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。例えば、`/apps/wknd/templates/page-content` リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての新規作成ページにこの設定を適用できます。

テンプレート階層に関する制約などをさらに追加する場合は、テンプレートの `allowedParents/allowedChildren` プロパティを使用できます。その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。
