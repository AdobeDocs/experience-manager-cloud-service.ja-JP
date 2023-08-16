---
title: AEM as a Cloud Serviceの宛先セレクター
description: AEMの宛先セレクターを使用して、元のアセットのコピーとして使用できるアセットを表示および選択します。
contentOwner: Adobe
role: Admin,User
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 35%

---


# マイクロフロントエンドの宛先セレクター {#Overview}

マイクロフロントエンドの宛先セレクターは、 [!DNL Experience Manager Assets as a Cloud Service] リポジトリ。 検索または参照できるフォルダーは、 [!DNL Experience Manager Assets as a Cloud Service] リポジトリーを作成し、アプリケーションからアセットをアップロードします。

Micro-Frontend ユーザーインターフェイスは、宛先セレクターパッケージを使用して、アプリケーションエクスペリエンスで使用できるようになります。 パッケージに対する更新は自動的にインポートされ、最新のデプロイ済みの宛先セレクターがアプリケーション内に自動的に読み込まれます。

![概要](assets/overview-destination-selector.png)

宛先セレクターには、次のような多くの利点があります。

* Vanilla JavaScript ライブラリを使用して、あらゆるアドビアプリケーションまたはアドビ以外のアプリケーションと簡単に統合できます。
* 宛先セレクターパッケージの更新が、アプリケーションで使用可能な宛先セレクターに自動的にデプロイされるので、管理が容易です。 最新の修正内容を読み込むために、アプリケーション内でアップデートを行う必要がありません。
* アプリケーション内での宛先セレクターの表示を制御するプロパティが使用できるので、カスタマイズが容易です。
* フルテキスト検索を使用して、フォルダーにすばやく移動し、アプリケーションからアセットをアップロードします。
* フォルダーを作成し、昇順または降順でフォルダーを並べ替え、リスト、グリッド、ギャラリー、ウォーターフォールの各表示でフォルダーを表示する機能。

この記事の範囲は、宛先セレクターを [!DNL Adobe] 統合シェルの下のアプリケーション、または認証用に生成された imsToken が既にある場合。 この記事では、これらのワークフローを非 SUSI フローと呼びます。

次のタスクを実行して、宛先セレクターを [!DNL Experience Manager Assets as a Cloud Service] リポジトリ：

* [Vanilla JS を使用した宛先セレクターの統合](#integration-with-vanilla-js)
* [宛先セレクターの表示プロパティを定義](#destination-selector-properties)
* [宛先セレクターを使用](#using-destination-selector)

## Vanilla JS を使用した宛先セレクターの統合 {#integration-with-vanilla-js}

あらゆる [!DNL Adobe] アプリケーションまたはアドビ以外のアプリケーションを [!DNL Experience Manager Assets] as a [!DNL Cloud Service] リポジトリと統合し、アプリケーション内からアセットを選択できます。

統合は、宛先セレクターパッケージを読み込み、Vanilla JavaScript ライブラリを使用して Assets as a Cloud Serviceに接続することでおこなわれます。 次を編集する必要があります： `index.html` またはアプリケーション内の適切なファイルを次の場所に置き換えます。
* 認証の詳細を定義する
* Assets as a Cloud Service リポジトリにアクセスする
* 宛先セレクターの表示プロパティの設定

次の場合は、一部の IMS プロパティを定義せずに認証を実行できます。

* [統合シェル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=ja)の [!DNL Adobe] アプリケーションを統合している場合。
* 認証用に既に IMS トークンが生成されている場合。

## 前提条件 {#prerequisites}

アプリケーション実装内の `index.html` ファイルまたは同様のファイルで前提条件を定義して、[!DNL Experience Manager Assets] as a [!DNL Cloud Service] リポジトリにアクセスするための認証の詳細を定義します。前提条件は次のとおりです。
* imsOrg
* imsToken
* apikey

## インストール {#installation}

宛先セレクターは、両方の ESM CDN から使用できます ( 例： [esm.sh](https://esm.sh/)/[スキーパック](https://www.skypack.dev/)) および [UMD](https://github.com/umdjs/umd) バージョン。

**UMD バージョン**&#x200B;を使用しているブラウザー（推奨）：

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>

<script>
  const { renderDestinationSelector } = PureJSSelectors;
</script>
```

**ESM CDN バージョン**&#x200B;を使用している `import maps` 対応ブラウザー：

```
<script type="module">
  import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
</script>
```

**ESM CDN バージョン**&#x200B;を使用している Deno/Webpack Module Federation：

```
import { DestinationSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/@assets/selectors/index.js'
```

### 選択した宛先 {#selected-destination}

宛先セレクターが `onItemSelect`, `onTreeToggleItem`または `onTreeSelectionChange` を、オブジェクト（ディレクトリ、画像など）を含む選択したディレクトリに置き換えます。

**スキーマ構文**

```
interface SelectedDestination {
  id: string;
  children: SelectedDestination[];
  'repo:repositoryId': string;
  'dc:format': string;
  'repo:assetClass': string;
  'storage:directoryType': string;
  'storage:region': string;
  'repo:name': string;
  'repo:path': string;
  'repo:ancestors': string[];
  'repo:createDate': string;
  'storage:assignee':

  { type: string; id: string; }
  ;
  'repo:assetId': string;
  'aem:published': boolean;
  'repo:createdBy': string;
  'repo:state': string;
  'repo:id': string;
  'repo:modifyDate': string;
  _page:

  { orderBy: string; count: number; };
}
```

次の表に、選択した宛先の重要なプロパティの一部を示します。

| プロパティ | タイプ | 説明 |
|---|---|---|
| *repo:repositoryId* | 文字列 | アセットが保存されるリポジトリの一意の ID。 |
| *repo:id* | 文字列 | アセットの一意の ID。 |
| *repo:assetClass* | 文字列 | アセットの分類（例：画像、ビデオ、ドキュメント）。 |
| *repo:name* | 文字列 | ファイル拡張子を含むアセットの名前。 |
| *repo:size* | 数値 | アセットのサイズ（バイト単位）。 |
| *repo:path* | 文字列 | リポジトリ内のアセットの場所。 |
| *repo:ancestors* | `Array<string>` | リポジトリ内のアセットの上位項目の配列。 |
| *repo:state* | 文字列 | リポジトリ内のアセットの現在の状態（アクティブ、削除など）。 |
| *repo:createdBy* | 文字列 | アセットを作成したユーザーまたはシステム。 |
| *repo:createDate* | 文字列 | アセットが作成された日時。 |
| *repo:modifiedBy* | 文字列 | アセットを最後に変更したユーザーまたはシステム。 |
| *repo:modifyDate* | 文字列 | アセットが最後に変更された日時。 |
| *dc:format* | 文字列 | アセットの形式。 |
| *_ページ* | orderBy: string; count: number; | ドキュメントのページ番号を含めます。 |

プロパティの完全なリストと詳細な例については、 [宛先セレクターのコード例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### 非 SUSI フローの例 {#non-ims-vanilla}

この例では、 [!DNL Adobe] 統合シェルの下のアプリケーション、または既に `imsToken` 認証用に生成されました。

を使用して、宛先セレクターパッケージをコードに含めます。 `script` タグ、 _6～15 行目_ 以下の例のを参照してください。 スクリプトが読み込まれると、 `PureJSSelectors` グローバル変数は使用できます。 宛先セレクターの定義 [プロパティ](#destination-selector-properties) に示すように、 _16～23 行_. `imsOrg` プロパティと `imsToken` プロパティは、いずれも非 SUSI フローでの認証に必要です。`handleSelection` プロパティは、選択したアセットを処理するために使用されます。宛先セレクターをレンダリングするには、 `renderDestinationSelector` ～で述べられているように機能する _17 行目_. 宛先セレクターが `<div>` コンテナ要素 (「 _行 21 および 22_.

以下の手順に従うことで、宛先セレクターを SUSI 以外のフローで [!DNL Adobe] アプリケーション。

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Destination Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the DestinationSelector component
        const container = document.getElementById('destination-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const destinationSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderDestinationSelector` available in PureJSSelectors globals to render DestinationSelector
        PureJSSelectors.renderDestinationSelector(container, destinationselectorprops);
    </script>
</head>

<body>
    <div id="destination-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

詳細な例は、次を参照してください： [宛先セレクターのコード例](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## 宛先セレクターのプロパティを使用 {#destination-selector-properties}

Destination Selector のプロパティを使用して、Destination Selector のレンダリング方法をカスタマイズできます。 次の表に、宛先セレクターをカスタマイズして使用できるプロパティを示します。

| プロパティ | タイプ | 必須 | デフォルト | 説明 |
|---|---|---|---|---|
| *imsOrg* | 文字列 | はい | | [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] を組織にプロビジョニングする場合に割り当てられる Adobe Identity Management System（IMS）の ID です。The `imsOrg` キーは、アクセスする組織がAdobe IMS中かどうかを認証するために必要です。 |
| *imsToken* | 文字列 | いいえ | | 認証に使用される IMS ベアラートークンです。`imsToken` は、SUSI フローを使用する場合は必須ではありません。 ただし、非 SUSI フローを使用する場合は必須です。 |
| *apiKey* | 文字列 | いいえ | | AEM Discovery サービスへのアクセスに使用する API キーです。`apiKey` は、SUSI フローを使用する場合は必須ではありません。 ただし、SUSI 以外のフローでは必要です。 |
| *rootPath* | 文字列 | いいえ | /content/dam/ | 宛先セレクターにアセットが表示されるフォルダーパス。 `rootPath` はカプセル化の形式でも使用できます。例えば、次のパスの場合、 `/content/dam/marketing/subfolder/`の場合、宛先セレクターを使用すると、親フォルダーをトラバースできず、子フォルダーのみが表示されます。 |
| *hasMore* | ブーリアン | いいえ | | アプリケーションに表示するコンテンツが増えたら、このプロパティを使用して、コンテンツを読み込んでアプリケーションに表示するローダーを追加できます。 コンテンツの読み込みが進行中であることを示すインジケーターです。 |
| *orgName* | ブーリアン | いいえ | | AEMに関連付けられている組織の名前（おそらく orgID）です。 |
| *initRepoID* | 文字列 | いいえ | | デフォルトの初期ビューで使用するアセットリポジトリのパスです |
| *onCreateFolder* | 文字列 | いいえ | | The `onCreateFolder` プロパティを使用すると、アプリケーションに新しいフォルダーを追加するアイコンを追加できます。 |
| *onConfirm* | 文字列 | いいえ | | 「確認」ボタンを押したときのコールバックです。 |
| *confirmDisabled* | 文字列 | いいえ | | このプロパティは、確認ボタンの切り替えを制御します。 |
| *viewType* | 文字列 | いいえ | | The `viewType` プロパティは、アセットの表示に使用するビューを指定するために使用されます。 |
| *viewTypeOptions* | 文字列 | いいえ | | このプロパティは、 `viewType` プロパティ。 アセットを表示する 1 つ以上のビューを指定できます。 使用可能な viewTypeOptions は、リスト表示、グリッド表示、ギャラリー表示、ウォーターフォール表示、ツリー表示です。 |
| *itemNameFormatter* | 文字列 | いいえ | | このプロパティを使用すると、アイテム名を書式設定できます |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | いいえ |  | OOTB 翻訳がアプリケーションのニーズを満たさない場合は、独自のローカライズされたカスタム値を `i18nSymbols` プロップ経由で渡すことができるインターフェイスを表示できます。このインターフェイスを介して値を渡すと、提供されたデフォルトの翻訳が上書きされ、代わりに独自の翻訳が使用されます。上書きを実行するには、上書きしたい `i18nSymbols` のキーに有効な[メッセージ記述子](https://formatjs.io/docs/react-intl/api/#message-descriptor)オブジェクトを渡す必要があります。 |
| *inlineAlertSetup* | 文字列 | いいえ | | アプリケーションに渡すアラートメッセージが追加されます。 例えば、このフォルダーにアクセスする権限がないというアラートメッセージを追加します。 |
| *intl* | オブジェクト | いいえ | | 宛先セレクターは、デフォルトの標準の翻訳を提供します。 `intl.locale` プロップを介して有効なロケール文字列を指定することで、翻訳言語を選択できます。（例：`intl={{ locale: "es-es" }}` </br></br>）サポートされているロケール文字列は、言語名の標準規格を表す [ISO 639 - コード](https://www.iso.org/iso-639-language-codes.html)に従います。</br></br> サポートされているロケールの一覧：英語 - &#39;en-us&#39;（デフォルト）スペイン語 - &#39;es-es&#39; ドイツ語 - &#39;de-de&#39; フランス語 - &#39;fr-fr&#39; イタリア語 - &#39;it-it&#39; 日本語 - &#39;ja-jp&#39; 韓国語 - &#39;ko-kr&#39; ポルトガル語 - &#39;pt-br&#39; 中国語（簡体字） - &#39;zh-cn&#39; 中国語（繁体字） - &#39;zh-tw&#39; |

## 宛先セレクターのプロパティの使用例 {#usage-examples}

宛先セレクターを定義できます。 [プロパティ](#destination-selector-properties) （内） `index.html` ファイルを使用して、アプリケーション内の宛先セレクターの表示をカスタマイズします。

### 例 1：宛先セレクターでフォルダーを作成する

宛先セレクターを使用すると、特定の場所にアセットをアップロード、移動またはコピーするための新しいフォルダーを作成できます。

![create-folder-destination-selector](assets/create-folder-destination-selector.png)

### 例 2：宛先セレクターのビュータイプを指定する

宛先セレクターは、リスト表示、グリッド表示、ギャラリー表示、ウォーターフォール表示など、4 つの異なる表示で、様々なアセットの配列を表示します。 デフォルトのビュータイプを指定するには、 `viewType` プロパティ。 The `viewTypeOptions` プロパティは、 `viewType` プロパティを使用して他のビュータイプを指定し、他のビュータイプオプションをドロップダウンに表示できるようにします。 1 つのオプションだけを表示したい場合は、1 つの引数を使用できます。

![viewtype-destination-selector](assets/viewtype-destination-selector.png)

### 例 3：アセットフォルダーのパスを初期化する

以下を使用します。 `path` プロパティを使用して、宛先セレクターがレンダリングされる際に自動的に表示されるフォルダー名を定義します。

![initialize-folder-path](assets/initialize-folder-path.png)

## 宛先セレクターの使用 {#using-destination-selector}

宛先セレクターを設定し、宛先セレクターを [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] アプリケーションでは、アセットを選択したり、様々な操作を実行してリポジトリ内のアセットを検索したりできます。

![using-destination-selector](assets/using-destination-selector.png)

* **A**: [検索バー](#search-bar)
* **B**: [並べ替え](#sorting)
* **C**：[アセット](#assets-repo)
* **D**: [サフィックスまたはプレフィックスを追加](#add-suffix-or-prefix)
* **E**: [新しいフォルダーを作成](#create-new-folder)
* **金**: [表示](#types-of-view)
* **G**: [情報](#info)
* **H**: [フォルダーを選択](#select-folder)

### 検索バー {#search-bar}

宛先セレクターを使用すると、選択したリポジトリ内のアセットに対して、全文検索を実行できます。 例えば、検索バーにキーワード「`wave`」を入力すると、メタデータプロパティのいずれかでキーワード「`wave`」が記述されているアセットがすべて表示されます。

### 並べ替え {#sorting}

宛先セレクター内のアセットを、名前、サイズまたはアセットのサイズで並べ替えることができます。 アセットを昇順または降順で並べ替えることもできます。

### アセットリポジトリ {#assets-repo}

また、宛先セレクターでは、AEMアプリケーションで使用できる、選択したリポジトリのデータを表示することもできます。 以下を使用できます。 `repositoryID` プロパティを使用して、宛先セレクターの最初のインスタンスに表示する宛先フォルダーのパスを初期化します。

### サフィックスまたはプレフィックスを追加 {#add-suffix-or-prefix}

これは `optionsFormSetup` プロパティ。 これを使用して、選択内容を確定し、 `onConfirm` イベント。

### 新しいフォルダーを作成 {#create-new-folder}

これにより、 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].

### 表示の種類 {#types-of-view}

宛先セレクターを使用すると、次の 4 つの異なるビューでアセットを表示できます。

* **![リスト表示](assets/do-not-localize/list-view.png) [!UICONTROL リスト表示]**：リスト表示では、スクロール可能なファイルとフォルダーが 1 列に表示されます。
* **![グリッド表示](assets/do-not-localize/grid-view.png) [!UICONTROL グリッド表示]**：グリッド表示では、スクロール可能なファイルとフォルダーが行と列のグリッドに表示されます。
* **![ギャラリー表示](assets/do-not-localize/gallery-view.png) [!UICONTROL ギャラリー表示]**：ギャラリー表示では、ファイルやフォルダーが中央に固定された水平リストに表示されます。
* **![ウォーターフォール表示](assets/do-not-localize/waterfall-view.png) [!UICONTROL ウォーターフォール表示]**：ウォーターフォール表示では、ファイルやフォルダーが Bridge の形式で表示されます。

### 情報 {#info}

情報または情報アイコンを使用して、選択したアセットのメタデータを表示できます。 ディメンション、サイズ、説明、パス、変更日、作成日など、様々な詳細が含まれます。 メタデータ情報は、新しいアセットのアップロード時、コピー時、作成時に提供されます。

### フォルダーの選択 {#select-folder}

「フォルダーを選択」ボタンを使用すると、 [プロパティ](#destination-selector-properties) を設定します。