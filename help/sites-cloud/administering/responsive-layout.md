---
title: レイアウトコンテナとレイアウトモードの設定
description: レスポンシブレイアウトをコンテンツ作成者に対して有効にするためのレイアウトコンテナおよびレイアウトモードの設定方法について説明します。
source-git-commit: 4ae0ae4fbf8f6a97434628f5f6049720c6c43118
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 50%

---


# レイアウトコンテナとレイアウトモードの設定 {#configuring-layout-container-and-layout-mode}

[レスポンシブレイアウト](/help/sites-cloud/authoring/features/responsive-layout.md) ～を実現するメカニズムである [レスポンシブ web デザイン。](https://ja.wikipedia.org/wiki/Responsive_web_design) これにより、コンテンツ作成者は、ユーザーが使用するデバイスに応じたレイアウトとサイズの Web ページを作成できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* **[レイアウトコンテナ](/help/sites-cloud/authoring/features/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)**  — このコンポーネントは、レスポンシブグリッド内にコンポーネントを追加および配置できるグリッド段落システムを提供します。
   * ページのデフォルトの parsys として使用したり、コンポーネントブラウザーで作成者が使用できるようにしたりできます。
   * デフォルト **レイアウトコンテナ** コンポーネントは以下で定義されます。 `/libs/wcm/foundation/components/responsivegrid`.
   * レイアウトコンテナは次のように定義できます。
      * ユーザーがページに追加できるコンポーネントとして。
      * ページのデフォルトの parsys として。
      * コンポーネントとデフォルトの parsys の両方として。
         * レイアウトコンテナをページの標準とし、この中でユーザーがレイアウトコンテナをさらに追加できるようにすることができます。例えば、列を制御する場合などです。
* **[レイアウトモード](/help/sites-cloud/authoring/fundamentals/environment-tools.md)**  — レイアウトコンテナをページに配置したら、 **レイアウト** モード：レスポンシブグリッド内にコンテンツを配置します。
* **[エミュレーター](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate)**  — コンポーネントのサイズをインタラクティブに変更することで、デバイスやウィンドウのサイズに従ってレイアウトを並べ替えるレスポンシブ Web サイトを作成および編集できます。 その後、ユーザーはエミュレーターを使用してコンテンツがどのようにレンダリングされるかを確認できます。

これらのレスポンシブグリッドのメカニズムを使用すると、次のことができます。

* ブレークポイント（デバイスのグループ化を示す）を使用して、デバイスのレイアウトに基づいて様々なコンテンツの動作を定義します。
* デバイスグループに基づいてコンポーネントを非表示にします（コンポーネントを非表示にするブレークポイントを定義します）。
* 水平にグリッドにスナップを使用します（グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横並びまたは上下に並べて折たたみやリフローのタイミングを定義）。
* 列の制御を実現します。

>[!NOTE]
>
>サイトを [プロジェクトアーキタイプ](#addlink) または [標準サイトテンプレート](#addlink)の場合、レスポンシブレイアウトは通常設定されます。 それ以外の場合は、 [レイアウトコンテナコンポーネントをアクティブにします。](#enable-the-layout-container-component-for-page) 」を設定します。

## エミュレーターの有効化 {#enabling-emulator}

The [プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) そして [標準サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template) は、既にエミュレーターの使用を有効にしています。 コアコンポーネントやアーキタイプに基づかない独自のコンテンツを開発した場合は、このドキュメントを参照してください [レスポンシブデザイン](/help/implementing/developing/introduction/responsive-design.md) を参照してください。

## サイトのレイアウトモードのアクティベート {#activate-layout-mode-for-your-site}

**レイアウト** モードでは、エミュレーターを使用して、様々なデバイス向けにコンテンツのレイアウトを調整できます。 WKND サンプルサイトは、既に **レイアウト** モード。 次の手順に従って、独自のサイトを有効にします。

### ブレークポイントの設定 {#configure-breakpoints}

ブレークポイントは、レスポンシブデザインに不可欠で、コンテンツをターゲットデバイスに合わせて調整する方法とタイミングを定義するのに役立ちます。 ただし、導入するブレークポイントごとに、コンテンツに対応するための作成者向けの追加作業が生じるので、注意が必要です。 常に存在するデフォルトのブレークポイントを含め、2 つのブレークポイントで十分な場合が多くあります。 Adobeでは、デフォルトを含む 3 つ以上のブレークポイントを作成しないことをお勧めします（つまり、以下の 2 つ以下のノード）。 `cq:responsive/breakpoint`.

* ブレークポイントにはタイトルと幅があります。
   * タイトルは、必要に応じて向きと共に、一般的なデバイスのグループ化を表します。
      * 例：`phone`、`tablet`
   * 幅は、その汎用デバイスのグループ化の最大幅をピクセル単位で定義します。
      * 例えば、電話のブレークポイントの幅が 768 である場合、これが電話デバイスに使用されるレイアウトの最大幅になります。
* ブレークポイントは次のように定義できます。
   * ページテンプレートでは、設定は該当するテンプレートで作成されたすべてのページにコピーされます。
   * ページノードでは、設定は子ページに継承されます。
* ブレークポイントは、エミュレーターを使用しているときに、ページエディターの上部にマーカーとして表示されます。
* ブレークポイントは親ノード階層から継承され、自由に上書きできます。
* デフォルト（標準）のブレークポイントがあり、最後に設定したブレークポイントより上の部分をすべてカバーします。
* ブレークポイントは、CRXDE Liteまたは XML を使用して定義できます。

新規プロジェクトと既存プロジェクトの両方でブレークポイントを考慮する必要があります。

* 新しいプロジェクトを設定する場合は、テンプレートにブレークポイントを追加する必要があります。
* 既存のプロジェクト（既存のコンテンツを含む）を移行する場合は、次の操作を行います。
   * テンプレートにブレークポイントを追加します。
   * 既存のページに同じブレークポイントを追加します。

継承のため、これはコンテンツのルートページに対してのみおこなう必要があります。

#### CRXDE Lite を使用したブレークポイントの設定 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Liteを使用して、次のいずれかに移動します。

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
   * 幅： `Decimal <value of breakpoint>`

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

## ページのコンポーネントサイズ変更の有効化 {#enable-component-resizing-for-the-page}

内のコンポーネントのサイズ変更 **レイアウト** モードは、レスポンシブデザインの重要な部分で、WKND サンプルサイトで使用できます。 次の手順に従って、独自のサイトを有効にします。

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

次を作成する必要があります： [クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md) 追加の設定および関数呼び出しを提供する。 次の LESS エクストラクトは、プロジェクトに追加する必要がある最小限の例です。

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

例：

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

例：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

アダプティブ画像のメカニズムは、現在のウィンドウサイズに適した画像の選択を制御するスクリプトを介して使用可能になります。DOM の準備が整った後、または専用のイベントを受信するとアクティベートされます。現時点のところ、ユーザーのアクションの結果を適切に反映するには、ページを更新する必要があります。

>[!CAUTION]
>
>カスタムスタイルシートの clientlibs を作成時と公開時に適切に機能させるには、これをヘッダーの一部として読み込む必要があります。

## ページ用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page}

効果的なレスポンシブレイアウトを実現するには、コンテンツ作成者がレイアウトコンテナコンポーネントのインスタンスをページにドラッグできる必要があります。 これは、WKND サンプルサイトで既に有効になっています。 次の手順に従って、独自のサイトを有効にします。

### ページ編集用のレイアウトコンテナコンポーネントの有効化 {#enable-the-layout-container-component-for-page-editing}

作成者がさらに多くのレスポンシブグリッドをコンテンツページに追加できるようにするには、ページのレイアウトコンテナコンポーネントを有効にする必要があります。これは、次のいずれかを使用して行います。

* **オーサー環境を使用する** - [ページテンプレートの編集](/help/sites-cloud/authoring/features/templates.md) をクリックして、ページのレイアウトコンテナを有効にします。
* **コンポーネント定義**  — 用途 `allowedComponent` または静的インクルードを使用してコンポーネントを定義します。

### レイアウトコンテナのグリッドの設定 {#configure-the-grid-of-the-layout-container}

レイアウトコンテナの特定のインスタンスごとに使用できる列数を設定できます [ページテンプレートを編集して、](/help/sites-cloud/authoring/features/templates.md)
