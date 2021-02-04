---
title: AEM内での外部SPAの編集
description: このドキュメントでは、スタンドアロンSPAをAEMインスタンスにアップロードし、編集可能なコンテンツのセクションを追加し、オーサリングを有効にするための推奨手順について説明します。
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 1%

---

# AEM内での外部SPAの編集{#editing-external-spa-within-aem}

外部SPAとAEMの間でどのレベルの統合を行うかを決める際に、AEM内でSPAを表示するだけでなく、編集も可能にする必要があります。[](/help/implementing/developing/headful-headless.md)

## 概要 {#overview}

このドキュメントでは、スタンドアロンSPAをAEMインスタンスにアップロードし、編集可能なコンテンツのセクションを追加し、オーサリングを有効にするための推奨手順について説明します。

## 前提条件 {#prerequisites}

前提条件は簡単です。

* AEMのインスタンスがローカルで実行されていることを確認します。
* [AEMプロジェクトのアーキタイプを使用して、基本AEM SPAプロジェクトを作成します。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * これはAEMプロジェクトの基盤となり、外部SPAが含まれるように更新されます。
   * このドキュメントのサンプルでは、[WKND SPAプロジェクトの開始点を使用しています。](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* 社内で統合したい外部のReact SPAを使用できます。

## SPAをAEMプロジェクトにアップロード{#upload-spa-to-aem-project}

まず、外部SPAをAEMプロジェクトにアップロードする必要があります。

1. `/ui.frontend`プロジェクトフォルダー内の`src`を、Reactアプリケーションの`src`フォルダーに置き換えます。
1. アプリの`package.json`内の`/ui.frontend/package.json`ファイルに、追加の依存関係を含めます。
   * SPA SDKの依存関係が[推奨バージョンであることを確認します。](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. `/public`フォルダーにカスタマイズを含めます。
1. `/public/index.html`ファイルに追加されたインラインスクリプトまたはスタイルを含めます。

## リモートSPAの構成{#configure-remote-spa}

外部SPAがAEMプロジェクトの一部になったので、AEM内で設定する必要があります。

### AdobeSPA SDKパッケージを含める{#include-spa-sdk-packages}

AEM SPAの機能を活用するために、次の3つのパッケージに依存しています。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` は、Model Managerを初期化し、AEMインスタンスからモデルを取得するAPIを提供します。その後、このモデルを使用して、`@adobe/aem-react-editable-components`と`@adobe/aem-spa-component-mapping`のAPIを使用してAEMコンポーネントをレンダリングできます。

#### インストール {#installation}

次のnpmコマンドを実行して、必要なパッケージをインストールします。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManagerの初期化{#model-manager-initialization}

アプリがレンダリングされる前に、AEM `ModelStore`の作成を処理するために[`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)を初期化する必要があります。

これは、アプリケーションの`src/index.js`ファイル内、またはアプリケーションのルートがレンダリングされる場所で行う必要があります。

このために、`ModelManager`が提供する`initializationAsync` APIを使用できます。

次のスクリーンショットは、単純なReactアプリケーションで`ModelManager`の初期化を有効にする方法を示しています。 唯一の制約は、`initializationAsync`を`ReactDOM.render()`の前に呼び出す必要があることです。

![ModelManagerの初期化](assets/external-spa-initialize-modelmanager.png)

この例では、`ModelManager`が初期化され、空の`ModelStore`が作成されます。

`initializationAsync` 必要に応じて、 `options` オブジェクトをパラメーターとして受け入れることができます。

* `path`  — 初期化時に、定義されたパスのモデルがフェッチされ、に保存され `ModelStore`ます。これは、必要に応じて初期化時に`rootModel`を取得するのに使用できます。
* `modelClient`  — モデルの取得を担当するカスタムクライアントを提供できます。
* `model` - SSRを `model` 使用する場合に通常入力されるパラメーターとして渡される [オブジェクト。](/help/implementing/developing/hybrid/ssr.md)

### AEM認証可能なリーフコンポーネント{#authorable-leaf-components}

1. 承認可能なReactコンポーネントが作成されるAEMコンポーネントを作成または識別します。 この例では、WKNDプロジェクトのテキストコンポーネントを使用しています。

   ![WKNDテキストコンポーネント](assets/external-spa-text-component.png)

1. SPAで単純なReactテキストコンポーネントを作成します。 この例では、次の内容の新しいファイル`Text.js`が作成されています。

   ![Text.js](assets/external-spa-textjs.png)

1. AEMの編集を有効にするために必要な属性を指定する設定オブジェクトを作成します。

   ![configオブジェクトの作成](assets/external-spa-config-object.png)

   * `resourceType` は、ReactコンポーネントをAEMコンポーネントにマップし、AEMエディタで開いたときに編集を有効にする場合に必須です。

1. ラッパ関数`withMappable`を使用します。

   ![Mappableで使用](assets/external-spa-withmappable.png)

   このラッパー関数は、Reactコンポーネントをconfigで指定されたAEM `resourceType`にマッピングし、AEMエディタで開いたときの編集機能を有効にします。 スタンドアロンコンポーネントの場合は、特定のノードのモデルコンテンツも取得されます。

   >[!NOTE]
   >
   >この例では、コンポーネントに別のバージョンがあります。AEMでラップおよびアンラップされたReactコンポーネント。 コンポーネントを明示的に使用する場合は、ラップバージョンを使用する必要があります。 コンポーネントがページの一部になっている場合は、SPAエディターで行ったとおりに、デフォルトのコンポーネントを使用し続けることができます。

1. コンポーネント内のコンテンツをレンダリングします。

   テキストコンポーネントのJCRプロパティは、AEMでは次のように表示されます。

   ![テキストコンポーネントのプロパティ](assets/external-spa-text-properties.png)

   これらの値は、新しく作成された`AEMText` Reactコンポーネントにプロパティとして渡され、コンテンツのレンダリングに使用できます。

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   AEMの設定が完了すると、このようにコンポーネントが表示されます。

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >この例では、既存のテキストコンポーネントに合わせて、レンダリングされたコンポーネントをさらにカスタマイズしました。 ただし、これはAEMでのオーサリングとは関係ありません。

#### 許可可能な追加コンポーネントのページ{#add-authorable-component-to-page}

承認可能なReactコンポーネントが作成されたら、アプリケーション全体で使用できます。

WKND SPAプロジェクトからテキストを追加する必要があるページの例を見てみましょう。 この例では、「Hello World!」というテキストを表示します。 スタートアップ時に `/content/wknd-spa-react/us/en/home.html`.

1. 表示するノードのパスを指定します。

   * `pagePath`:この例では、ノードを含むページ  `/content/wknd-spa-react/us/en/home`
   * `itemPath`:この例では、ページ内のノードへのパス  `root/responsivegrid/text`
      * これは、ページ上の含まれる項目の名前で構成されます。

   ![ノードのパス](assets/external-spa-path.png)

1. コンポー追加ネントをページ内の必要な位置に配置する。

   ![ページ追加のコンポーネント](assets/external-spa-add-component.png)

   `AEMText`コンポーネントは、`pagePath`値と`itemPath`値をプロパティとして設定して、ページ内の必要な位置に追加できます。 `pagePath` は必須のプロパティです。

#### AEMでのテキストコンテンツの編集の確認{#verify-text-edit}

これで、実行中のAEMインスタンスでコンポーネントをテストできます。

1. `aem-guides-wknd-spa`ディレクトリから次のMavenコマンドを実行し、プロジェクトを構築してAEMにデプロイします。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. AEMインスタンスで、`http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`に移動します。

![AEMでのSPAの編集](assets/external-spa-edit-aem.png)

`AEMText`コンポーネントは、AEM上で認証できるようになりました。

### AEM承認可能なページ{#aem-authorable-pages}

1. SPAでのオーサリング用に追加するページを指定します。 この例では`/content/wknd-spa-react/us/en/home.html`を使用しています。
1. 新しいファイル(`Page.js`)を認証可能なページコンポーネントに置き換えます。 ここでは、`@adobe/cq-react-editable-components`で提供されるページコンポーネントを再利用できます。
1. [AEM認証可能なリーフコンポーネントのセクションで手順4を繰り返します。](#authorable-leaf-components) コンポーネント `withMappable` でwrapper関数を使用します。
1. 前に述べたように、ページ内のすべての子コンポーネントのAEMリソースタイプに`MapTo`を適用します。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >この例では、前に作成した`AEMText`を含める代わりに、ラップ解除されたReactテキストコンポーネントを使用します。 これは、コンポーネントがページ/コンテナの一部で、単独ではない場合、コンテナはコンポーネントのマッピングを再帰的に行い、オーサリング機能を有効にし、子ごとに追加のラッパーを必要としないためです。

1. SPAで承認可能なページを追加するには、[承認可能なコンポーネントをページに追加するのと同じ手順追加に従います。](#add-authorable-component-to-page) ここでは、 `itemPath` プロパティをスキップできます。

#### AEMでのページコンテンツの確認{#verify-page-content}

ページが編集可能であることを確認するには、「AEMでのテキストコンテンツの編集の確認」のセクションと同じ手順に従います。](#verify-text-edit)[

![AEMでのページの編集](assets/external-spa-edit-page.png)

レイアウトコンテナと子テキストコンポーネントを持つAEMでページを編集できるようになりました。

### 仮想リーフコンポーネント{#virtual-leaf-components}

前の例では、既存のAEMコンテンツを持つSPAにコンポーネントを追加しました。 ただし、AEMでコンテンツがまだ作成されていないが、後でコンテンツの作成者が追加する必要がある場合があります。 これに対応するために、フロントエンド開発者はSPA内の適切な場所にコンポーネントを追加できます。 これらのコンポーネントは、AEMのエディターで開くとプレースホルダーを表示します。 コンテンツの作成者がこれらのプレースホルダー内にコンテンツを追加すると、ノードがJCR構造に作成され、コンテンツが保持されます。 作成したコンポーネントでは、スタンドアロンのリーフコンポーネントと同じ操作のセットを使用できます。

この例では、以前に作成した`AEMText`コンポーネントを再利用しています。 WKNDホームページの既存のテキストコンポーネントの下に新しいテキストを追加する必要があります。 コンポーネントの追加は、通常のリーフコンポーネントの場合と同じです。 ただし、`itemPath`は、新しいコンポーネントを追加する必要があるパスに更新できます。

新しいコンポーネントは、`root/responsivegrid/text`にある既存のテキストの下に追加する必要があるので、新しいパスは`root/responsivegrid/{itemName}`になります。

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

`TestPage`コンポーネントは、仮想コンポーネントを追加すると次のようになります。

![仮想コンポーネントのテスト](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>この機能を有効にするには、`AEMText`コンポーネントの`resourceType`が構成内に設定されていることを確認します。

「AEMでのテキストコンテンツの編集の確認」の手順に従って、AEMに変更をデプロイできるようになりました。[](#verify-text-edit) 現在存在しない `text_20` ノードに対してプレースホルダーが表示されます。

![aemのtext_20ノード](assets/external-spa-text20-aem.png)

コンテンツ作成者がこのコンポーネントを更新すると、新しい`text_20`ノードが`/content/wknd-spa-react/us/en/home`の`root/responsivegrid/text_20`に作成されます。

![text20ノード](assets/external-spa-text20-node.png)

#### 要件と制限{#limitations}

仮想リーフコンポーネントを追加するための要件はいくつかあり、制限もいくつかあります。

* `pagePath`プロパティは、仮想コンポーネントを作成する場合に必須です。
* `pagePath`のパスに指定されたページノードは、AEMプロジェクト内に存在する必要があります。
* 作成するノードの名前は、`itemPath`で指定する必要があります。
* コンポーネントは任意のレベルで作成できます。
   * 前の例で`itemPath='text_20'`を提供すると、新しいノードはページのすぐ下に作成されます。`/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* 新しいノードが作成されるノードへのパスは、`itemPath`経由で提供された場合に有効である必要があります。
   * この例では、新しいノード`text_20`を作成できるように、`root/responsivegrid`が存在する必要があります。
* リーフコンポーネントの作成のみがサポートされます。 仮想コンテナと仮想ページは、今後のバージョンでサポートされる予定です。

## 追加のカスタマイズ{#additional-customizations}

前の例に従った場合、外部SPAはAEM内で編集できるようになりました。 ただし、外部SPAには、さらにカスタマイズできる要素があります。

### ルートノードID {#root-node-id}

デフォルトでは、Reactアプリケーションが要素ID `spa-root`の`div`内でレンダリングされると想定します。 必要に応じて、これをカスタマイズできます。

例えば、要素ID `root`の`div`内部にアプリケーションがレンダリングされるSPAがあるとします。 これは、3つのファイルに反映する必要があります。

1. Reactアプリケーションの`index.js`内（または`ReactDOM.render()`が呼び出される場所）

   ![index.jsファイル内のReactDOM.render()](assets/external-spa-root-index.png)

1. Reactアプリケーションの`index.html`内

   ![アプリケーションのindex.html](assets/external-spa-index.png)

1. AEMアプリのページコンポーネント本文では、次の2つの手順に従います。

   1. ページコンポーネント用に新しい`body.html`を作成します。

   ![新しいbody.htmlファイルの作成](assets/external-spa-update-body.gif)

   1. 新追加しい`body.html`ファイルの新しいルート要素。

   ![body.html追加へのルート要素](assets/external-spa-add-root.png)

### ルーティング{#editing-react-spa-with-routing}を使用したリアクションSPAの編集

外部React SPAアプリケーションに複数のページがある場合、[レンダリングするページ/コンポーネントを決定する際にルーティングを使用できます。](/help/implementing/developing/hybrid/routing.md) 基本的な使用例は、現在アクティブなURLとルートに指定されたパスを一致させることです。このようなルーティング対応アプリケーションでの編集を可能にするには、対応するパスをAEM固有の情報に合わせて変換する必要があります。

次の例では、2つのページを含む単純なReactアプリケーションを示します。 レンダリングするページは、ルータに提供されるパスとアクティブなURLとを一致させることで決定されます。 例えば、`mydomain.com/test`上にある場合、`TestPage`がレンダリングされます。

![外部SPAのルーティング](assets/external-spa-routing.png)

このSPAの例でAEM内での編集を有効にするには、次の手順が必要です。

1. AEMのルートとなるレベルを特定します。

   * このサンプルでは、wknd-spa-react/us/enをSPAのルートとして検討しています。 つまり、そのパスより前のものはすべてAEMのページ/コンテンツのみです。

1. 必要なレベルで新しいページを作成します。

   * この例では、編集するページは`mydomain.com/test`です。 `test` がアプリのルートパスにある。これは、AEMでページを作成する場合にも保持する必要があります。 したがって、前の手順で定義したルートレベルで新しいページを作成できます。
   * 新しく作成するページは、編集するページと同じ名前にする必要があります。 この`mydomain.com/test`の例では、新しく作成するページは`/path/to/aem/root/test`にする必要があります。

1. SPA追加ルーティング内のヘルパー。

   * 新しく作成されたページは、AEMでは、まだ期待されたコンテンツをレンダリングしません。 これは、ルータが`/test`のパスを想定しているのに対し、AEMのアクティブパスは`/wknd-spa-react/us/en/test`であるからです。 AEM固有のURL部分を受け入れるには、SPA側にヘルパーを追加する必要があります。

   ![ルーティングヘルパー](assets/external-spa-router-helper.png)

   * `@adobe/cq-spa-page-model-manager`が提供する`toAEMPath`ヘルパーを使用できます。 アプリケーションがAEMインスタンスで開かれる場合に、ルーティング用に指定されたパスをAEM固有の部分を含めるように変換します。 次の3つのパラメーターを受け取ります。
      * ルーティングに必要なパス
      * SPAが編集されるAEMインスタンスの接触チャネルURL
      * 最初の手順で決定したAEMのプロジェクトルート
   * これらの値は、環境変数として設定でき、より柔軟に設定できます。



1. AEMでのページの編集を確認します。

   * プロジェクトをAEMにデプロイし、新しく作成した`test`ページに移動します。 これで、ページコンテンツがレンダリングされ、AEMコンポーネントが編集可能になります。

## その他のリソース {#additional-resources}

AEMのコンテキストでSPAを理解するには、次の参照資料が役立ちます。

* [headful and headless in AEM](/help/implementing/developing/headful-headless.md)
* [AEMプロジェクトのアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPAプロジェクト](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [React を使用した AEM での SPA の概要](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPAリファレンス資料（APIリファレンス）](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA BlueprintとPageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA モデルルーティング](/help/implementing/developing/hybrid/routing.md)
* [SPA およびサーバーサイドレンダリング](/help/implementing/developing/hybrid/ssr.md)
