---
title: スタイルAEM CIFコアコンポーネント
description: スタイルAEM CIFコアコンポーネント
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 4%

---


# スタイルAEM CIFコアコンポーネント {#style-aem-cif-core-components}

[CIFプロジェクトのアーキタイプ](https://github.com/adobe/aem-cif-project-archetype) は、AEM CIFコアコンポーネントを使用して、お客様のプロジェクトの起点として最小Adobe Experience Manager(AEM) CIFプロジェクトを作成し [](https://github.com/adobe/aem-core-cif-components)ます。 ベニアブランドと呼ばれるデフォルトのスタイルは、最初はサイトに適用されます。 このチュートリアルでは、アーキタイプによって生成される新しいAEM CIFプロジェクトを調査し、AEM CIF Coreコンポーネントで使用されるCSSとJavaScriptがどのように編成されているかを理解します。 また、CSSを使用して新しいスタイルを作成し、Product Teaserコンポーネントのデフォルトのスタイルを置き換えます。

![作成する内容](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> カードに似たProduct Teaserコンポーネントに新しいスタイルが実装されます。

## 前提条件 {#prerequisites}

次のツールとテクノロジーが必要です。

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) または [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (AEM 6.5以降のみ)
* [Apache Maven](https://maven.apache.org/) （3.3.9以降）
* Adobe Experience Manager（ローカルインスタンス）
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/ja-JP/experience-manager-64/release-notes/sp-release-notes.html)
* アーキタイプと互換性のある [バージョンを実行するMagento](https://github.com/adobe/aem-cif-project-archetype#requirements)

## プロジェクトの生成 {#generate-project}

ここでは、 [CIFプロジェクトアーキタイプを使用して新しいAEM CIFプロジェクトを生成し](https://github.com/adobe/aem-cif-project-archetype) 、デフォルトのスタイルを上書きします。

**(CIFプロジェクトのアーキタイプに基づく** )既存のプロジェクトを自由に使用し、このセクションをスキップしてください。

1. GitHubの最新リリースを確認して、CIFプロジェクトのアーキタイプ [の最新バージョンを確認します](https://github.com/adobe/aem-cif-project-archetype/releases/latest)。 次の手順で、最新リリース `x.y.z` のバージョンに置き換えます。

1. 次のMavenコマンドを実行して、 [バッチモードで新しいプロジェクトを生成します](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)。

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. プロジェクトを構築し、AEMのローカルインスタンスにデプロイします。

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. AEMインスタンス追加をMagentoインスタンスに接続したり、新しく作成したプロジェクトに設定を追加したりするために必要なOSGi設定。

1. この時点で、Magentoインスタンスに接続されたストアフロントの作業バージョンが必要です。 次の場所にある `US` / `Home` ページに移動します。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   現在、店頭ではベニアのテーマが使用されていることがわかります。 ストアフロントのメインメニューを展開すると、様々なカテゴリが表示され、接続Magentoが機能していることが示されます。

   ![ベニアテーマで構成されたストアフロント](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## クライアントライブラリの概要 {#introduction-to-client-libraries}

ストアフロントのテーマ/スタイルのレンダリングを担当するCSSとJavaScriptは、AEMで、 [クライアントライブラリ](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/developing/introduction/clientlibs.html) （短くはclientlib）によって管理されます。 クライアントライブラリは、プロジェクトのコード内でCSSとJavaScriptを整理し、ページに配信するメカニズムを提供します。

AEM CIFコアコンポーネントにブランド固有のスタイルを適用するには、これらのクライアントライブラリで管理されるCSSを追加および上書きします。 クライアントライブラリが構造化され、ページに含まれる方法を理解することが重要です。

### プロジェクトクライアントライブラリ {#project-client-libraries}

次に、アーキタイプによって自動的に生成されたクライアントライブラリを調べます。 選択したIDEを使用して、前の練習で生成したプロジェクトを [読み込みます](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)。

1. ui.apps **** モジュールに移動して展開し、フォルダー階層を展開して次の操作を行います。 `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   その下には、clientlib-base **と** themeの2つのフォルダがあります ****。

1. **clientlib-base** - [AEM Core Componentsから必要な依存関係を埋め込んだ空のクライアントライブラリ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)。

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   次に、 **clientlib-base** ( `.content.xml` ファイル)のXML定義を示します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` は、このクライアントライブラリのカテゴリです。 カテゴリはタグと考えてください。 これは、ライブラリをページに含めたり、埋め込んだりするために使用されます。

   その他のclientlibカテゴリの `embed` プロパティと配列に注目してください。 これらの各カテゴリは、クライアントライブラリを表します。 例えば、アコーディオンコンポーネントが機能するた `core.wcm.components.accordion.v1` めに必要なJavaScriptを [含めます](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) 。

   お `embed``categories` よびプロパティを使用して、異なるプロジェクトのクライアントライブラリを管理し、含めることができます。

   `allowProxy=true` クライアントライブラリのCSSとJavaScriptが、次のプリフィックスが付いたパスから提供されるようにします。 `/etc.clientlibs`. これにより、下位のアプリケーションコードはエンドユーザーから `/apps` 保護されたままになりますが、Webサイトの機能に必要なCSSやJavaScriptは、匿名で提供できます。 More details about the [allowProxy property can be found here](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **テーマ** — これは、CIFプロジェクトの開始テーマとCSSを含むクライアントライブラリです。 このクライアントライブラリは、各実装によってカスタマイズされるように設計されており、コンポーネントが開始に合わせて機能するように、既存のスタイルと開始すると便利です。

   ![theme clientlibrary](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   次に、 **テーマのXML定義を示します**。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` は、このクライアントライブラリのカテゴリです。これが、クライアントライブラリがページに含まれる方法です。

1. テ **ーマ** ・クライアント・ライブラリの下に、 **css.txtという名前のファイルが表示されます** 。次の場所にあります。 `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   **css.txt** (および **js.txt**)は、最終的なCSSファイルに個々のファイルが含まれる順序を指定するマニフェストとして機能します。 CSSとJavaScriptの両方の処理を順に行う必要があります。複数のファイルを作成してコードをより適切に管理できると便利です。 **css.txt** ファイルを調べると、スタイルが適用されるコンポーネント別にファイルが整理されていることがわかります。

1. theme **** /componentsの下にあるCSSファイルをInspectして、ootbコンポーネントのスタイルを把握します。 これらのファイルの一部は、チュートリアルの後半で更新します。

### ベースページコンポーネントを含むクライアントライブラリを含める

次に、 [](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) HTLとページコンポーネントを使用して、クライアントライブラリがページにどのように含まれるかを調べます。

1. ui.apps **モジュールで** 、次の下にある `page` コンポーネント定義に移動します。 `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. この **** ページコンポーネントは、アーキタイプによって生成され、プロジェクト内のすべてのページをレンダリングするために使用されるエントリポイントです。

1. **ページ** コンポーネントの定義(`page/.content.xml`)を調べると、を指すプロパティ `sling:resourceSuperType` が表示され `core/cif/components/structure/page/v1/page`ます。 つまり、プロジェクトの(Acme) **ページコンポーネントは、** CIF Core Page [](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) (CIF)コンポーネントのすべての機能を継承し、管理コードを削減できます。

1. ページ **コンポーネントの下に** 、2つのファイルが表示されます。 **customheaderlibs.html** および **customfooterlibs.html**。

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** は、ページのhead部分にレンダリングされるHTMLスクリプトです。 プロジェクト固有のロジックを上書きして追加するのは、一般的なスクリプトです。 この場合は、をカテゴリとしてクライアントライブラリを含めるために使用し `acme.wcm.base`ます。 Web開発のベストプラクティスに従い、ページのhead部分にCSSのみを含めます。

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** は、ページの下部、終了タグの直前にレンダリングされるHTLスクリプトで `</body>` す。 この場合も、のカテゴリ `acme.wcm.base` が使用されますが、今回はクライアントライブラリのJavaScriptのみが読み込まれます。

ページ **コンポーネントのHTLスクリプトの変更は** 、すべてのページ `acme.wcm.base` に適用される方法です。 でも何 `acme.theme`? 次の練習では、クライアントライブラリを含めるための別のオプションを見ていきます。

### ページテンプレートによるクライアントライブラリの追加 {#client-library-inclusion-pagetemplates}

クライアント側ライブラリを含める方法には、いくつかのオプションがあります。 次に、 [ページテンプレートを使用して、生成されたプロジェクトにクライアント側のテーマライブラリがどのように含まれるかを調べます](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/developing/platform/templates/page-templates-editable.html)。

新しいブラウザを開き、このチュートリアルの最初にプロジェクトを展開したAEMインスタンスにログインします。

1. AEM開始画面で、 **ツール** / **一般** / **テンプレートに移動します**。

   ![テンプレートナビゲーション](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Acme **Store Configuration** フォルダーに移動します。 **鉛筆** アイコンを選択して、 ** カテゴリページテンプレートを開きます。

   ![カテゴリページテンプレートカード](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. 左上隅の「 **ページ情報** 」アイコンを選択し、「 **ページポリシー**」をクリックします。

   ![ページポリシーメニュー項目](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. これにより、カタログページテンプレートのページポリシーが開きます。

   ![ページポリシー — カタログページ](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   右側には、このテンプレートを使用するすべてのページに含まれるクライアントライブラリ **カテゴリ** の一覧が表示されます。

   * **wcm.foundation.components.page.responsive** — 作成者がレスポンシブレイアウト [](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/authoring/siteandpage/responsive-layout.html) コントロールを有効にするために必要なCSSを提供します。
   * **acme.theme** — アーキタイプが自動的に生成する開始テーマです。 デフォルトでは、サンプルのVeniaデモストアのようにスタイル設定されています。 ただし、名前からわかるように、プロジェクトの実装によってカスタマイズされることを意図しています。 *次のセクションで変更する内容です。*
   * **core.cif.components.react** — これは、買い物かごなどの動的な機能に使用されるいくつかのReactコンポーネントをコンパイルしたクライアントライブラリです。 More [information can be found here](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   他のテンプレートでは、同じポリシー、 **コンテンツページ**、 **ランディングページ**、 同じポリシーを再使用すると、すべてのページに同じクライアントライブラリを確実に含めることができます。

   テンプレートとページポリシーを使用してクライアントライブラリの組み込みを管理する利点は、テンプレートごとにポリシーを変更できることです。 例えば、同じAEMインスタンス内で2つの異なるブランドを管理しているとします。 各ブランドには独自のスタイルまたは *テーマがあります* が、基本ライブラリとコードは同じです。 別の例として、特定のページにのみ表示したい大きなクライアントライブラリがある場合、そのテンプレートのみに固有のページポリシーを作成できます。 もう一つの利点は

### ページ上のクライアントライブラリの検証 {#verify-client-libraries}

この時点で、HTLを使用して ******** customheaderlibs.htmlおよびcustomfooterlibs.htmlスクリプトと共にクライアントライブラリを含める方法と、追加のクライアントライブラリを含めるためにテンプレートのページポリシーを使用する方法を確認しました。 次に、サイトにクライアントライブラリが含まれていることを確認します。

1. AEM開始画面で、 **Sites** / **Acme Store** / **United States** / **English/** Englishに移動し、編集用にページを開きます。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. **ページ情報** メニューを選択し、「 **表示は公開済み**」をクリックします。

   ![公開済みとして表示](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   これにより、AEM作成者のjavascriptが読み込まれずに、公開されたサイトに表示されるので、ページが開きます。 URLにクエリパラメーターが `?wcmmode=disabled` 追加されていることに注意してください。 CSSとJavaScriptを開発する場合は、このパラメーターを使用してAEM作成者が提供した内容を含めてページを簡略化することをお勧めします。

1. ページソースの表示が含まれており、次のクライアントライブラリを特定できる必要があります。 **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.theme**, **core.cif.components.react**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## Style the Product Teaser {#style-product-teaser}

アーキタイプによって生成されるクライアントライブラリ構造を理解したので、AEM CIFコアコンポーネントのカスタマイズを開始できます。 「カード」のように見えるように、Product Teaserコンポーネントのスタイルを変更します。

### Product Teaserの作成 {#author-product-teaser}

最初の手順として、AEMオーサリングツールを使用して、Product Teaserコンポーネントの新しいインスタンスをサイトのホームページに追加します。

1. 新しいブラウザータブを開き、サイトの **ホームページ** に移動します。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. ページのメインレイアウトコンテナに新しい **製品Teaser** コンポーネントを挿入します。

   ![Product Teaserの挿入](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. サイドパネルを展開し（まだ切り替えていない場合）、アセットファインダードロップダウンを **製品に切り替えます**。 これにより、接続されたMagentoインスタンスから使用可能な商品のリストが表示されます。 製品を選択し、ページ上の **製品ティーザー****(Product Teaser** )コンポーネントにドラッグ&amp;ドロップします。

   ![Product Teaserをドラッグ&amp;ドロップ](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > 注意：ダイアログ( *レンチ* アイコンをクリック)を使用してコンポーネントを設定することで、表示された製品を設定することもできます。

1. これで、Product Teaserによって製品が表示されます。 製品の名前と製品の価格は、表示されるデフォルトの属性です。

   ![製品ティーザー — デフォルトスタイル](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Product TeaserのCSSの更新 {#update-css-product-teaser}

次に、Product Teaser用のカードに似たスタイルを実装するために、 **テーマ** クライアントライブラリのCSSを変更します。

IDEと生成されたプロジェクトに戻ります。

1. ui.apps **モジュールで** 、次のフォルダーに移動します。 `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. Product Teaserのすべてのスタイルが定義される場所です。

1. ファイル **teaser.cssを開き、対応するCSSルールを更新します(または、** ソリューションteaser.cssファイルをダウンロードして置き換えます [](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) )。

   製品テ追加ィーザーのドロップシャドウと角丸を含むドロップシャドウです。

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   製品テーザーで画像の枠線を変更します。

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
    }
   ```

   製品名を更新して、ティーザーの下部に表示されるようにし、テキストの色を変更します。

   ```css
   .productteaser .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

   製品の価格を更新して、ティーザーの下部にも表示されるようにし、テキストの色を変更します。

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   992px未満の画面で名前と価格を積み重ねるには、下部のメディアクエリを更新します。

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   teaser.cssに変更を保存 **します**。 ここから、 [ソリューションteaser.cssファイルをダウンロードできます](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css)。

1. コマンドラインターミナルから、 **ui.apps** モジュールのアップデートをAEMにデプロイします。その際には、Mavenのスキルを使用します。

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >追加の [IDEの設定とツール](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) (完全なMavenビルドを実行することなく、プロジェクトファイルをローカルのAEMインスタンスに直接同期できます)。

### 表示が更新された製品ティーザー {#view-updated-product-teaser}

プロジェクトのコードをAEMに導入した後、Product Teaserの変更を確認できるようになります。

1. ブラウザに戻り、ホームページを再度更新します。 [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). 更新された製品Teaserスタイルが適用されていることが確認できます。

   ![製品ティーザースタイルの更新](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. 製品テーザーを追加してテストします。 レイアウトモードを使用して、複数のティーザーを一列に表示するためにコンポーネントの幅とオフセットを変更します。

   ![複数の製品テーザー](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >各製品のティーザーには同じスタイルが含まれます。

### トラブルシューティング {#troubleshooting}

CRXDE-Liteで、更新されたCSSファイルがデプロイされたこ [とを確認できます](http://localhost:4502/crx/de/index.jsp) 。 [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

新しいCSSファイルやJavaScriptファイルをデプロイする場合は、ブラウザーで古いファイルが提供されないようにすることも重要です。 これは、ブラウザーのキャッシュをクリアするか、新しいブラウザーセッションを開始することで解消できます。

また、AEMは、パフォーマンスを考慮してクライアントライブラリをキャッシュしようとします。 コードのデプロイメントに従って、古いファイルが提供されることがあります。 [クライアントライブラリの [再構築]ツールを使用して、AEMクライアントライブラリのキャッシュを手動で無効にすることができます](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)。 *AEMが古いバージョンのクライアントライブラリをキャッシュしていると思われる場合は、「キャッシュを無効にする」をお勧めします。 ライブラリの再構築は非効率で時間がかかります。*

### Congratulations {#congratulations}

最初のAEM CIFコアコンポーネントのスタイル設定を行いました。

### ボーナスチャレンジ {#bonus-challenge}

[AEM Styleシステムを使用して](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/developing/components/style-system.html) 、コンテンツ作成者がオン/オフを切り替えることのできる2つのスタイルを作成します。 [スタイルシステムを使用した開発では](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) 、この作業を行う方法に関する詳細な手順と情報が説明されています。

![ボーナスチャレンジ — スタイルシステム](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## その他のリソース {#additional-resources}

* [AEM CIFアーキタイプ](https://github.com/adobe/aem-cif-project-archetype)

* [AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)

* [ローカルAEM開発環境の設定](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [クライアント側ライブラリ](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/developing/introduction/clientlibs.html)
* [AEM Sites使用の手引き](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [スタイルシステムを使用した開発](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
