---
title: レイアウトコンテナおよびレイアウトモードの設定
description: コンテンツ作成者がレスポンシブレイアウトを使用できるように、レイアウトコンテナとレイアウトモードを設定する方法について説明します。
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 70a35cfeb163967b0f627d3ac6495f112d922974
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 88%

---


# レイアウトコンテナおよびレイアウトモードの設定 {#configuring-layout-container-and-layout-mode}

コンテンツ作成者がレスポンシブレイアウトを使用できるように、レイアウトコンテナとレイアウトモードを設定する方法について説明します。

>[!TIP]
>
>このドキュメントでは、レスポンシブ web デザインをサポートするようにサイト管理者がレイアウトコンテナを設定する方法について説明します。 その他のリソースを利用できます。
>
>* コンテンツ作成者がコンテンツページでレスポンシブデザイン機能を使用する方法の詳細については、ドキュメント [ レスポンシブレイアウト ](/help/sites-cloud/authoring/page-editor/responsive-layout.md) を参照してください。
>* 開発者向けに、レイアウトコンテナとレスポンシブグリッドの詳細については、[ レスポンシブデザインドキュメント ](/help/implementing/developing/introduction/responsive-design.md) に説明されています。このドキュメントでは、サイトをデザインする際にレイアウトコンテナとレスポンシブグリッドを使用するためのヒントが提供されています。

## 概要 {#overview}

レスポンシブレイアウトは、[ レスポンシブ web デザイン ](https://en.wikipedia.org/wiki/Responsive_web_design) を実現するためのメカニズムです。 これにより、コンテンツ作成者は、ユーザーが使用するデバイスのレイアウトとサイズに応じて web ページを作成できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* **[レイアウトコンテナ](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)** - このコンポーネントは、レスポンシブグリッド内にコンポーネントを追加および配置できるグリッド段落システムを提供します。
   * ページのデフォルトの parsys として使用したり、コンポーネントブラウザーで作成者が使用できるようにしたりできます。
   * デフォルトの&#x200B;**レイアウトコンテナ**&#x200B;コンポーネントは `/libs/wcm/foundation/components/responsivegrid` で定義します。
   * レイアウトコンテナは次のように定義できます。
      * ユーザーがページに追加できるコンポーネントとして。
      * ページのデフォルトの parsys として。
      * コンポーネントとデフォルトの両方の parsys として。
         * レイアウトコンテナをページの標準として使用し、その中にユーザーがレイアウトコンテナをさらに追加できるようにすることができます。例えば、列を制御する場合などです。
* **[レイアウトモード](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)** - レイアウトコンテナをページに配置したら、**レイアウト**&#x200B;モードを使用して、レスポンシブグリッド内にコンテンツを配置できます。
* **[エミュレーター](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)** - これにより、コンポーネントのサイズをインタラクティブに変更することで、デバイスやウィンドウのサイズに従ってレイアウトを並べ替えるレスポンシブ web サイトを作成および編集できます。その後、ユーザーはエミュレーターを使用してコンテンツがどのようにレンダリングされるかを確認できます。

これらのレスポンシブグリッドのメカニズムを使用すると、次のことができます。

* ブレークポイント（デバイスのグループ化を示す）を使用して、デバイスのレイアウトに基づいて様々なコンテンツの動作を定義します。
* デバイスグループに基づいてコンポーネントを非表示にします（コンポーネントを非表示にするブレークポイントを定義します）。
* 水平にグリッドにスナップを使用します（グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横並びまたは上下に並べて折たたみやリフローのタイミングを定義）。
* 列の制御を実現します。

>[!NOTE]
>
>[プロジェクトアーキタイプ](#addlink)または[標準サイトテンプレート](#addlink)からサイトを作成する場合、通常はレスポンシブレイアウトが設定されます。それ以外の場合は、ページの[レイアウトコンテナコンポーネントをアクティベート](#enable-the-layout-container-component-for-page)する必要があります。

## エミュレーターの有効化 {#enabling-emulator}

[プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)と[標準サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template)は、エミュレーターを使用するために既に有効になっています。コアコンポーネントやアーキタイプに基づいていない独自のコンテンツを開発した場合、これらの機能を活用しながらコンポーネントを開発することができます。この方法について詳しくは、[レスポンシブデザイン](/help/implementing/developing/introduction/responsive-design.md)のドキュメントを参照してください。

## サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}

**レイアウト**&#x200B;モードでは、エミュレーターを使用して、様々なデバイスに合わせてコンテンツのレイアウトを調整できます。WKND サンプルサイトでは、**レイアウト**&#x200B;モードが既に有効になっています。独自のサイトを有効にするには、次の手順に従います。

### ブレークポイントを設定 {#configure-breakpoints}

ブレークポイントは、レスポンシブデザインに不可欠で、コンテンツをターゲットデバイスに合わせて調整する方法とタイミングを定義します。ただし、導入するブレークポイントが増えると、作成者がコンテンツを調整するために行う作業が増えるため、注意してください。多くの場合、常に存在するデフォルトのブレークポイントを含め、2 つのブレークポイントで十分です。アドビでは、デフォルトを含めて 3 つ以上のブレークポイントを作成しないこと、つまり `cq:responsive/breakpoint` の下に 2 つ以上のノードを作成しないことをお勧めします。

* 次のように、ブレークポイントにはタイトルと幅があります。
   * タイトルは、一般的なデバイスグループを示し、必要に応じてデバイスの向きも含まれます。
      * 例：`phone`、`tablet`
   * 幅は、一般的なデバイスグループの最大幅をピクセル単位で定義します。
      * 例えば、電話のブレークポイントの幅が 768 である場合、これが電話デバイスに使用されるレイアウトの最大幅になります。
* 次のように、ブレークポイントを定義できます。
   * ページテンプレートでは、設定は該当するテンプレートで作成されたすべてのページにコピーされます。
   * ページノードでは、設定は子ページに継承されます。
* ブレークポイントは、エミュレーターの使用中に、ページエディターの上部にマーカーとして表示されます。
* ブレークポイントは、親ノード階層から継承され、自由に上書きできます。
* 最後に設定されたブレークポイントより上のすべてに対応するデフォルト（標準）のブレークポイントがあります。
* ブレークポイントは、CRXDE Lite または XML を使用して定義できます。

ブレークポイントは、新しいプロジェクトと既存のプロジェクトの両方で考慮する必要があります。

* 新しいプロジェクトを設定する場合は、テンプレートにブレークポイントを追加する必要があります。
* 既存のプロジェクト（既存のコンテンツを含む）を移行する場合は、次の操作を行います。
   * テンプレートにブレークポイントを追加します。
   * 既存のページに同じブレークポイントを追加します。

継承のため、コンテンツのルートページに対してのみ行う必要があります。

#### CRXDE Lite を使用したブレークポイントの設定 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite を使用して、次のいずれかに移動します。

   * テンプレート定義。
   * ページの `jcr:content` ノード。

1. `jcr:content` の下に、以下のノードを作成します。

   * 名前：`cq:responsive`
   * 型：`nt:unstructured`

1. この下に、次のノードを作成します。

   * 名前：`breakpoints`
   * 型：`nt:unstructured`

1. breakpoints ノードの下に、任意の数のブレークポイントを作成できます。それぞれ、以下のプロパティを持つ単一のノードとして定義してください。

   * 名前：`<descriptive name>`
   * 型：`nt:unstructured`
   * タイトル：`String <descriptive title seen in Emulator>`
   * 幅：`Decimal <value of breakpoint>`

#### XML を使用したブレークポイントの設定 {#configuring-breakpoints-using-xml}

ブレークポイントは、該当するテンプレート（またはコンテンツ）フォルダーの下で `.context.html` の `<jcr:content>` セクション内に配置されます。

定義の例は次のとおりです。

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## ページのコンポーネントサイズ変更を有効にする {#enable-component-resizing-for-the-page}

**レイアウト**&#x200B;モードでのコンポーネントのサイズ変更は、レスポンシブデザインの重要な部分で、WKND サンプルサイトで使用できます。独自のサイトを有効にするには、次の手順に従います。

### レイアウトコンテナをメインの parsys として設定する {#set-layout-container-as-main-parsys}

ページのメインの parsys をレイアウトコンテナとして設定するには、parsys を次のように定義します。

`wcm/foundation/components/responsivegrid`

次のいずれかで定義します。

* ページコンポーネント
* ページテンプレート（今後の使用のため）

以下に、定義を説明する 2 つの例を示します。

* **HTL：**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### レスポンシブ CSS を含める {#include-the-responsive-css}

#### LESS を使用した CSS のブレークポイント {#css-for-breakpoints-using-less}

AEM では、必要な CSS の一部の生成に LESS を使用するため、これらをプロジェクトに含める必要があります。

追加の設定と関数呼び出しを提供するには、[クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)を作成する必要があります。次の LESS エクストラクトは、プロジェクトに追加する必要がある最小限の例です。

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

基本のグリッドの定義は、次の場所にあります。

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### スタイル設定に関する考慮事項 {#styling-considerations}

レスポンシブコンテナ内に保持されるコンポーネントは、レスポンシブグリッドのサイズに従って（それぞれの HTML DOM 要素と共に）サイズ変更されます。したがって、このような状況では、（含まれている）固定幅の DOM 要素の定義を回避（または更新）することをお勧めします。

次に例を示します。

* 前：

   * `width=100px`

* 後：

   * `max-width=100px`

#### サイズ変更とアダプティブ画像の整合性 {#resizing-and-adaptive-image-compliance}

グリッド内でコンポーネントのサイズを変更すると、次のリスナーが適宜トリガーされます。

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

レスポンシブグリッドに含まれているアダプティブ画像のコンテンツを適切にサイズ変更および更新するには、`REFRESH_PAGE` リスナーに設定されている `afterEdit` を、含まれているすべてのコンポーネントの `EditConfig` ファイルに追加する必要があります。

次に例を示します。

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

アダプティブ画像のメカニズムは、現在のウィンドウサイズに適した画像の選択を制御するスクリプトを介して使用可能になります。DOM の準備が整った後、または専用のイベントを受信するとアクティベートされます。現時点のところ、ユーザーのアクションの結果を適切に反映するには、ページを更新する必要があります。

>[!CAUTION]
>
>カスタムスタイルシートの clientlibs を作成時と公開時に適切に機能させるには、これをヘッダーの一部として読み込む必要があります。

## ページ用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page}

効果的なレスポンシブレイアウトを実現するには、コンテンツ作成者がレイアウトコンテナコンポーネントのインスタンスをページにドラッグできる必要があります。これは、WKND サンプルサイトで既に有効になっています。独自のサイトを有効にするには、次の手順に従います。

### ページ編集用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page-editing}

作成者がさらに多くのレスポンシブグリッドをコンテンツページに追加できるようにするには、ページのレイアウトコンテナコンポーネントを有効にする必要があります。これは、次のいずれかを使用して行います。

* **オーサー環境経由** - [ページテンプレートを編集](/help/sites-cloud/authoring/page-editor/templates.md)して、ページのレイアウトコンテナを有効にします。
* **コンポーネント定義** - コンポーネントを定義するときに、`allowedComponent` または静的インクルードを使用します。

### レイアウトコンテナのグリッドを設定する {#configure-the-grid-of-the-layout-container}

レイアウトコンテナの特定のインスタンスごとに使用可能な列の数を設定するには [ ページテンプレートを編集します ](/help/sites-cloud/authoring/page-editor/templates.md)。

### ネストされたレスポンシブグリッド {#nested-responsive-grids}

Adobeが推奨するベストプラクティスは、構造をできるだけ平らにすることです。

ネストされたレスポンシブグリッドの使用が避けられない場合は、開発者用ドキュメント [ レスポンシブデザイン ](/help/implementing/developing/introduction/responsive-design.md#nested-responsive-grids) を参照してください。
