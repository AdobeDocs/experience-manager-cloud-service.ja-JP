---
title: SPAの複合コンポーネント
description: AEMシングルページアプリケーション(SPA)エディターで動作する、他のコンポーネントで構成される独自の複合コンポーネントを作成する方法を説明します。
exl-id: fa1ab1dd-9e8e-4e2c-aa9a-5b46ed8a02cb
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# SPAの複合コンポーネント{#composite-components-in-spas}

複合コンポーネントは、複数のベースコンポーネントを1つのコンポーネントに組み合わせることで、AEMコンポーネントのモジュラー性を活用します。 一般的な複合コンポーネントの使用例は、画像コンポーネントとテキストコンポーネントの組み合わせで構成されるカードコンポーネントです。

複合コンポーネントがAEMシングルページアプリケーション(SPA)エディターフレームワーク内で適切に実装されている場合、コンテンツ作成者は、そのようなコンポーネントを他のコンポーネントと同様にドラッグ&amp;ドロップできますが、複合コンポーネントを構成する各コンポーネントを個別に編集できます。

この記事では、AEM SPA Editorとシームレスに連携する複合コンポーネントをシングルページアプリケーションに追加する方法について説明します。

## ユースケース {#use-case}

この記事では、一般的なカードコンポーネントを使用例として使用します。 カードは、多くのデジタルエクスペリエンスに共通のUI要素で、通常は画像と関連するテキストまたはキャプションで構成されます。 作成者は、カード全体をドラッグ&amp;ドロップできるようにしたいが、カードの画像を個別に編集したり、関連するテキストをカスタマイズしたりできます。

## 前提条件 {#prerequisites}

複合コンポーネントの使用例をサポートする次のモデルでは、次の前提条件が必要です。

* AEM開発インスタンスは、サンプルプロジェクトを使用して、ポート4502上でローカルに実行されています。
* AEMでの編集が有効な外部Reactアプリ[が作業中です。](editing-external-spa.md)
* Reactアプリは、RemotePageコンポーネントを使用してAEMエディター[に読み込まれます。](remote-page.md)

## 複合コンポーネントをSPAに追加する{#adding-composite-components}

AEM内のSPA実装に応じて、複合コンポーネントを実装するための3つの異なるモデルがあります。

* [コンポーネントはAEMプロジェクトに存在しません。](#component-does-not-exist)
* [コンポーネントはAEMプロジェクトに存在しますが、必要なコンテンツは存在しません。](#content-does-not-exist)
* [コンポーネントとその必要なコンテンツは共にAEMプロジェクトに存在します。](#both-exist)

以下の節では、カードコンポーネントを例として使用して各ケースを実装する例を示します。

### コンポーネントはAEMプロジェクトに存在しません。{#component-does-not-exist}

まず、合成コンポーネントを構成するコンポーネント（画像とそのテキストのコンポーネント）を作成します。

1. AEMプロジェクトにテキストコンポーネントを作成します。
1. 対応する`resourceType`をコンポーネントの`editConfig`ノードのプロジェクトから追加します。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. `withMappable`ヘルパーを使用して、コンポーネントの編集を有効にします。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

テキストコンポーネントは次のようになります。

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

同様の方法で画像コンポーネントを作成した場合は、画像コンポーネントとテキストコンポーネントを子として使用し、`AEMText`コンポーネントと組み合わせて新しいカードコンポーネントにすることができます。

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

この合成コンポーネントは、アプリ内の任意の場所に配置でき、がSPAエディターでテキストと画像コンポーネントのプレースホルダーを追加します。 以下のサンプルでは、カードコンポーネントがタイトルの下のホームコンポーネントに追加されています。

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

これにより、エディターでテキストと画像の空のプレースホルダーが表示されます。 エディターを使用してこれらの値を入力すると、指定されたページパス（ルートレベルの`/content/wknd-spa/home`に、`itemPath`で指定された名前で格納）に格納されます。

![エディター内の複合カードコンポーネント](assets/composite-card.png)

### コンポーネントはAEMプロジェクトに存在しますが、必要なコンテンツは存在しません。{#content-does-not-exist}

この場合、カードコンポーネントは、タイトルと画像ノードを含むAEMプロジェクトに既に作成されています。 子ノード（テキストと画像）には、対応するリソースタイプが含まれます。

![カードコンポーネントのノード構造](assets/composite-node-structure.png)

その後、それをSPAに追加して、そのコンテンツを取得できます。

1. このに対応するコンポーネントをSPAに作成します。 子コンポーネントが、SPAプロジェクト内の対応するAEMリソースタイプにマッピングされていることを確認します。 この例では、前の例で説明した[と同じ`AEMText`コンポーネントと`AEMImage`コンポーネントを使用します。](#component-does-not-exist)

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
   * AEMプロジェクトに既にコンテナが存在する場合は、代わりにSPAにコンテナを含め、代わりにAEMからコンテナにコンポーネントを追加できます。
   * カードコンポーネントが、SPAの対応するリソースタイプにマッピングされていることを確認します。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 作成した`wknd-spa/components/imagecard`コンポーネントを、ページテンプレート内のコンテナコンポーネント[に使用できるコンポーネントに追加します。](/help/sites-cloud/authoring/features/templates.md)

これで、`imagecard`コンポーネントをAEMエディターでコンテナに直接追加できます。

![エディター内のコンポジットカード](assets/composite-card.gif)

### コンポーネントとその必要なコンテンツは共にAEMプロジェクトに存在します。{#both-exist}

コンテンツがAEMに存在する場合は、コンテンツへのパスを指定して、SPAに直接含めることができます。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![ノード構造内の複合パス](assets/composite-path.png)

`AEMCard`コンポーネントは、前の使用例で定義した[と同じです。](#content-does-not-exist) ここでは、AEMプロジェクトの上記の場所で定義されたコンテンツがSPAに含まれます。
