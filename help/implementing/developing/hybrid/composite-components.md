---
title: SPAの複合コンポーネント
description: AEMシングルページアプリケーション(SPA)エディタで動作する、独自の複合コンポーネント（他のコンポーネントで構成されるコンポーネント）を作成する方法を学びます。
translation-type: tm+mt
source-git-commit: 8623a043fd7253f94e0673b18053a6af922367b5
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# SPA {#composite-components-in-spas}の複合コンポーネント

複合コンポーネントは、複数のベースコンポーネントを1つのコンポーネントに組み合わせることで、AEMコンポーネントのモジュラー性を活用します。 一般的な複合コンポーネントの使用例は、画像とテキストコンポーネントの組み合わせで構成されるカードコンポーネントです。

AEM Single Page Application (SPA) Editorフレームワーク内で複合コンポーネントが適切に実装されている場合、コンテンツ作成者は、そのようなコンポーネントを他のコンポーネントと同様にドラッグ&amp;ドロップできますが、複合コンポーネントを構成する各コンポーネントを個別に編集できます。

この記事では、AEM SPAエディタでシームレスに機能するように、単一ページアプリケーションに複合コンポーネントを追加する方法を説明します。

## ユースケース {#use-case}

この記事では、一般的なカードコンポーネントを使用例として使用します。 カードは、多くのデジタルエクスペリエンスに共通のUI要素で、通常は画像と関連するテキストまたはキャプションで構成されます。 作成者は、カード全体をドラッグ&amp;ドロップできるようにしたいと考えていますが、カードの画像を個別に編集したり、関連するテキストをカスタマイズしたりできます。

## 前提条件 {#prerequisites}

複合コンポーネントの使用例をサポートする次のモデルでは、次の前提条件が必要です。

* AEM開発インスタンスは、サンプルプロジェクトを含むポート4502上でローカルに実行されています。
* AEMでの編集に対して、[有効な外部Reactアプリが作業中です。](editing-external-spa.md)
* Reactアプリは、RemotePageコンポーネントを使用してAEMエディター[に読み込まれます。](remote-page.md)

## SPAへの複合コンポーネントの追加{#adding-composite-components}

AEMでのSPAの実装に応じて、複合コンポーネントを実装する場合のモデルは3つあります。

* [コンポーネントがAEMプロジェクトに存在しません。](#component-does-not-exist)
* [コンポーネントはAEMプロジェクトに存在しますが、必要なコンテンツは存在しません。](#content-does-not-exist)
* [コンポーネントと必要なコンテンツはどちらもAEMプロジェクトに存在します。](#both-exist)

以下の節では、カードコンポーネントを例として使用して各ケースを実装する例を示します。

### コンポーネントがAEMプロジェクトに存在しません。{#component-does-not-exist}

開始を行うには、合成コンポーネントを構成するコンポーネント（画像とテキストのコンポーネントなど）を作成します。

1. AEMプロジェクトでテキストコンポーネントを作成します。
1. コンポ追加ーネントの`editConfig`ノード内のプロジェクトの対応する`resourceType`。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. `withMappable`ヘルパーを使用して、コンポーネントの編集を有効にします。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

テキストコンポーネントは、次のようになります。

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

同様の方法で画像コンポーネントを作成する場合は、`AEMText`コンポーネントと組み合わせて新しいカードコンポーネントにし、画像とテキストのコンポーネントを子として使用できます。

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

この合成コンポーネントは、アプリ内の任意の場所に配置でき、SPAエディターでテキストと画像コンポーネントのプレースホルダーが追加されます。 下のサンプルでは、カードコンポーネントがタイトルの下のホームコンポーネントに追加されています。

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

これにより、エディターにテキストと画像の空のプレースホルダーが表示されます。 エディターを使用してこれらの値を入力すると、`itemPath`で指定された名前でルートレベルの`/content/wknd-spa/home`のように、指定されたページパスに保存されます。

![エディター内の複合カードコンポーネント](assets/composite-card.png)

### コンポーネントはAEMプロジェクトに存在しますが、必要なコンテンツは存在しません。{#content-does-not-exist}

この場合、カードコンポーネントは、タイトルと画像ノードを含むAEMプロジェクトに既に作成されています。 子ノード（テキストと画像）には、対応するリソースタイプが含まれます。

![カードコンポーネントのノード構造](assets/composite-node-structure.png)

その後、SPAに追加して、そのコンテンツを取得できます。

1. SPAで、これに対応するコンポーネントを作成します。 子コンポーネントがSPAプロジェクト内の対応するAEMリソースタイプにマップされていることを確認します。 この例では、前の例で詳細に説明した[と同じ`AEMText`と`AEMImage`のコンポーネントを使用します。](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. `imagecard`コンポーネントのコンテンツがないので、ページにカードを追加します。 AEMの既存のコンテナをSPAに含めます。
   * AEMプロジェクトに既にコンテナが存在する場合は、代わりにSPAにこれを含め、AEMからコンテナにコンポーネントを追加します。
   * カードコンポーネントがSPAの対応するリソースタイプにマップされていることを確認します。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 作成追加された`wknd-spa/components/imagecard`コンポーネントは、ページテンプレート内のコンテナコンポーネント[に対して許可されているコンポーネントに対して使用されます。](/help/sites-cloud/authoring/features/templates.md)

これで、`imagecard`コンポーネントをAEMエディタ内のコンテナに直接追加できます。

![エディタ内の複合カード](assets/composite-card.gif)

### コンポーネントと必要なコンテンツはどちらもAEMプロジェクトに存在します。{#both-exist}

コンテンツがAEMに存在する場合は、コンテンツへのパスを指定することで、SPAに直接コンテンツを含めることができます。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![ノード構造内の複合パス](assets/composite-path.png)

`AEMCard`コンポーネントは、前の使用例で定義した[と同じです。](#content-does-not-exist) AEMプロジェクトの上記の場所で定義されたコンテンツは、SPAに含まれます。
