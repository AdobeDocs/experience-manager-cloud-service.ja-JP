---
title: レスポンシブレイアウト
description: AEM では、ページにレスポンシブレイアウトを作成できます
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# レスポンシブレイアウト {#responsive-layout}

AEM では、**レイアウトコンテナ**&#x200B;コンポーネントを使用して、ページのレスポンシブレイアウトを作成できます。

レスポンシブグリッド内にコンポーネントを配置できる段落システムを提供します。このグリッドでは、デバイスやウィンドウのサイズおよび形式に従ってレイアウトを再編成できます。The component is used in conjunction with the [**Layout **mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes), which allows you to create and edit your responsive layout dependent on device.

レイアウトコンテナには、次の特徴があります。

* 水平方向のスナップをグリッドに提供します。また、コンポーネントをグリッドに並べて配置して、折りたたみやリフローのタイミングを定義できます。
* 事前定義済みのブレークポイント（電話、タブレット用など）を使用して、関連するデバイスまたは向きのコンテンツに必要な動作を定義できます。
   * 例えば、コンポーネントのサイズや、特定のデバイスでコンポーネントを表示するかどうかをカスタマイズできます。
* ネストして、列を制御できます。

その後、エミュレーターを使用して、特定のデバイスのコンテンツのレンダリング方法を確認できます。

AEM は、次のメカニズムを組み合わせて使用することにより、ページのレスポンシブレイアウトを実現します。

* [**Layout Containerコンポーネント&#x200B;**](#adding-a-layout-container-and-its-content-edit-mode)

   This component is available in the [component browser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) and provides a grid-paragraph system to allow you to add and position components within a responsive grid. ページ上のデフォルトの段落システムとしても設定できます。

* [**レイアウトモード&#x200B;**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

   Once the layout container is positioned on your page you can use the **Layout** mode to position content within the responsive grid.

* [**エミュレーター&#x200B;**](#selecting-a-device-to-emulate)コンポーネントをインタラクティブにサイズ変更することによってデバイスやウィンドウのサイズに従ってレイアウトを再編成する、レスポンシブ Web サイトを作成および編集できます。その後、エミュレーターを使用して、コンテンツのレンダリング方法を確認できます。

これらのレスポンシブグリッドメカニズムを使用すると、次のことが可能になります。

* ブレークポイントを使用して、（デバイスのタイプと向きを基準とした）デバイスの幅に基づいて異なるコンテンツのレイアウトを定義する。
* これらの同じブレークポイントとコンテンツのレイアウトを使用して、デスクトップ上のブラウザーウィンドウのサイズに応じたコンテンツを作成する。
* グリッドに対して水平方向のスナップを使用し、グリッドにコンポーネントを配置し、必要に応じてサイズ変更し、横方向や上限／下限方向への折たたみや折り返しのタイミングを定義する。
* 特定のデバイスレイアウトのコンポーネントを非表示にする。
* 列の制御を実現する。

プロジェクトに応じて、レイアウトコンテナは、ページのデフォルトの段落システムとして、またはコンポーネントブラウザ（またはその両方）を介してページに追加できるコンポーネントとして使用できます。

>[!TIP]
>
>Adobe provides [GitHub documentation](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) of the responsive layout as a reference that can be given to front-end developers allowing them to use the AEM grid outside of AEM, for example when creating static HTML mock-ups for a future AEM site.

>[!NOTE]
>
>前述のメカニズムの使用は、テンプレートでの設定によって有効になります。See Configuring Responsive Layout for further information. <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## レイアウトの定義、デバイスのエミュレーションおよびブレークポイント {#layout-definitions-device-emulation-and-breakpoints}

Web サイトのコンテンツを作成する場合は、使用するデバイスに適した方法でコンテンツが表示されるようにする必要があります。

AEM では、デバイスの幅に依存するレイアウトを定義できます。

* エミュレーターを使用すると、これらのレイアウトを様々なデバイスに基づいてエミュレートできます。In addition to the device type, the orientation, selected by the **Rotate device** option, can impact the breakpoint selected as the width changes.
* ブレークポイントとは、レイアウトの定義を区切るポイントのことです。
   * ブレークポイントでは、専用のレイアウトを使用するあらゆるデバイスの最大幅を（ピクセル単位で）効果的に定義します。
   * ブレークポイントは通常、デバイスのディスプレイの幅に応じて、様々なデバイスに使用できます。
   * ブレークポイントの範囲は、次のブレークポイントまで、左側に広がります。
   * ブレークポイントを具体的に選択することはできず、デバイスと向きの選択によって、適切なブレークポイントが自動的に選択されます。

**デスクトップ**&#x200B;デバイスには、特定の幅がなく、デフォルトのブレークポイントに関連します（つまり、すべてが最後に設定したブレークポイントを上回る）。

>[!NOTE]
>
>個別のデバイスごとにブレークポイントを定義するという方法も考えられますが、そうするとレイアウトの定義とメンテナンスに必要となる作業が大幅に増加することになります。

エミュレーターを使用してエミュレーションおよびレイアウト定義用の特定のデバイスを選択すると、関連するブレークポイントもハイライト表示されます。レイアウト変更は、ブレークポイントが適用される他のデバイス（アクティブなブレークポイントマーカーの左側で、次のブレークポイントマーカーの前に位置するすべてのデバイス）にも適用できます。

例えば、エミュレーションとレイアウトのためにデバイス **iPhone 6 Plus**（幅の定義は 540 ピクセル）を選択した場合、ブレークポイント&#x200B;**電話**（768 ピクセルで定義）もアクティブ化されます。**iPhone 6** へのレイアウト変更は、**電話**&#x200B;ブレークポイントの下の他のデバイス（**iPhone 5**（320 ピクセルで定義）など）に適用できます。

![エミュレーター](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## エミュレートするデバイスの選択 {#selecting-a-device-to-emulate}

1. 必要なページを編集用に開きます。次に例を示します。

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. 上部のツールバーから&#x200B;**エミュレーター**&#x200B;アイコンを選択します。

   ![エミュレータボタン](/help/sites-cloud/authoring/assets/emulator.png)

1. エミュレーターツールバーが開きます。

   ![エミュレータツールバー](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   エミュレーターツールバーに追加のレイアウトオプションが表示されます。

   * **デバイスの回転** — デバイスを垂直方向（縦長）から水平方向（横長）に回転させたり、逆に回転させたりできます。
   ![デバイスの横向き回転ボタン](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![デバイスを縦に回転ボタン](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **デバイスを選択** - エミュレートする特定のデバイスをリストから定義します（詳しくは次のステップを参照）。
   ![デバイスの選択ボタン](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. エミュレートするデバイスを選択するには、次のどちらかの方法を使用できます。

   * デバイスを選択アイコンを使用して、ドロップダウンセレクターから選択します。
   * エミュレーターツールバーのデバイスのインジケーターをタップまたはクリックする。
   ![&#91;デバイスの選択&#93;ドロップダウン](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. 特定のデバイスを選択すると、次のことができます。

   * See the active marker for the selected device, such as **iPad.**
   * See the active marker for the appropriate [breakpoint](#layout-definitions-device-emulation-and-breakpoints) such as **Tablet.**
   * The blue dotted line represents the *fold* for the selected device (here an **iPhone 6 Plus** in landscape).
   ![フォールド](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * フォールドは、コンテンツのページの改行と見なすこともできます（[ブレークポイント](#layout-definitions-device-emulation-and-breakpoints)と混同しないでください）。これは、デバイスでスクロールする前にユーザーに表示されるコンテンツの部分を確認するために表示されます。
   * エミュレートしているデバイスの高さが画面サイズより高い場合、フォールドの線は表示されません。
   * フォールドは、作成者の利便性のために表示されます。公開されたページには表示されません。


## Adding a Layout Container and its Content (Edit mode) {#adding-a-layout-container-and-its-content-edit-mode}

**レイアウトコンテナ**&#x200B;は、次の特徴を持つ段落システムです。

* 他のコンポーネントを含む。
* レイアウトを定義する。
* 変更に応答する。

>[!NOTE]
>
>まだ使用できない場合は、段落シス **テム** /ページに対してレイアウトコンテナを明示的にアクティブ化する必要があります。 <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. **レイアウトコンテナ**&#x200B;は、[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)で標準コンポーネントとして使用できます。ここから、ページ上の必要な場所へドラッグできます。そうすると、「**コンポーネントをここにドラッグ**」プレースホルダーが表示されます。
1. その後、コンポーネントをレイアウトコンテナに追加できます。これらのコンポーネントには実際のコンテンツが含まれます。

   ![レイアウトコンテナ](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selecting and Taking Action on a Layout Container (Edit mode) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

他のコンポーネントと同様に、レイアウトコンテナは、選択してからアクション（切り取り、コピー、削除）を実行できます（**編集**&#x200B;モードのとき）。

>[!CAUTION]
>
>レイアウトコンテナは段落システムなので、このコンポーネントを削除すると、レイアウトグリッドに加えて、そのコンテナ内にあるすべてのコンポーネント（およびそのコンテンツ）も削除されます。

1. グリッドのプレースホルダーの上にマウスを移動するか、タップすると、アクションメニューが表示されます。

   ![レイアウトコンテナに追加](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   You need to select the **Parent** option.

   ![親ボタン](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. レイアウトコンポーネントがネストされている場合は、**親**&#x200B;オプションを選択するとドロップダウンに選択肢が表示され、ネストしたレイアウトコンテナまたはその親を選択できます。

   ドロップダウンのコンテナ名の上にマウスを移動すると、アウトラインがページに表示されます。

   * 最も低いネストされたレイアウトコンテナは青で囲まれます。
   * 連続するコンテナはすべて、明るい青の色合いになります。
   ![ネストされたコンテナ](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. グリッド全体が、コンテンツも含めて強調表示されます。The action toolbar will be shown, from where you can select an action such as **Delete.**

## Defining Layouts (Layout mode) {#defining-layouts-layout-mode}

>[!NOTE]
>
>[ブレークポイント](#layout-definitions-device-emulation-and-breakpoints)ごとに別々のレイアウトを定義できます（エミュレートされたデバイスのタイプと向きによって決定）。

To configure the layout of a responsive grid implemented with the Layout Container you need to use the **Layout** mode.

**レイアウト**&#x200B;モードは 2 つの方法で開始できます。

* By using the [mode menu in the toolbar](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) and choosing **Layout** mode
   * Select the **Layout** mode just as you would switch to **Edit** mode or **Targeting** mode.
   * **レイアウト** モードは永続的なままで、モードセレクターを使用して別のモ **** ードを選択するまで、レイアウトモードを終了しません。
* [個別のコンポーネントを編集する](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)場合。
   * コンポーネントのクイックアクションメニューの「**レイアウト**」オプションを使用すると、**レイアウト**&#x200B;モードに切り替えることができます。
   * **レイアウト**&#x200B;モードはコンポーネントを編集している間持続し、フォーカスが別のコンポーネントに移ると&#x200B;**編集**&#x200B;モードに戻ります。

レイアウトモードでは、グリッドに対して様々なアクションを実行できます。

* 青いドットを使用して、コンテンツのコンポーネントのサイズを変更します。サイズ変更は常にグリッドにスナップされます。背景のサイズを変更する際には、次のように位置揃えを補助するためのグリッドが表示されます。

   ![コンポーネントのサイズ変更](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   >[!NOTE]
   >
   >コンポーネント（**画像**&#x200B;など）のサイズが変更されても、割合と比率は維持されます。

* コンテンツコンポーネントをクリックまたはタップします。ツールバーで次の操作を実行できます。
   * **Parent** — レイアウトコンテナコンポーネント全体に対してアクションを実行する場合に、コンポーネント全体を選択できます。
   * **[新しい線分に分離** ]：コンポーネントは新しい線分に移動され、グリッド内で使用可能なスペースに応じて異なります。
   * **コンポーネントを非表示** — コンポーネントは非表示になります（レイアウトコンテナのツールバーから復元できます）。
   ![コンポーネントを非表示](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* In **Layout** mode you can tap/click on the **Drag components here** to select the entire component. そうすると、このモードのツールバーが表示されます。

   ツールバーには、レイアウトコンポーネントの状態やそれに属するコンポーネントに応じて異なるオプションが表示されます。次に例を示します。

   * **親** — 親コンポーネントを選択します。

      ![親ボタン](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **非表示のコンポーネントを表示** — すべてのまたは個々のコンポーネントを表示します。数字は、現在の非表示のコンポーネントの数を示します。 カウンターには、非表示になっているコンポーネントの数が表示されます。

      ![非表示のコンポーネントを表示ボタン](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **ブレークポイントのレイアウトを元に戻す** — デフォルトのレイアウトに戻します。つまり、カスタマイズされたレイアウトは適用されません。

      ![ブレークポイントレイアウトボタンを元に戻す](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Float to new line** — 間隔が許される場合は、コンポーネントを上に移動します。

      ![新しい行に分離ボタン](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Hide component** — 現在のコンポーネントを非表示にします。

      ![コンポーネントボタンを非表示](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)
   >[!NOTE]
   >
   >上記の例では、フロートと非表示のアクションが使用可能になっています。これは、このレイアウトコンテナが親レイアウトコンテナ内にネストされているからです。

   * **コンポーネントを表示**&#x200B;親コンポーネントを選択して、「**非表示のコンポーネントを表示**」オプションを含むアクションツールバーを表示します。この例では、2 つのコンポーネントが非表示にされています。

      ![コンポーネントの再表示](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)
   「**非表示のコンポーネントを表示**」オプションを選択すると、現在非表示のコンポーネントが元の場所で青色で表示されます。

   ![すべて復元ボタン](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

   「**すべてを復元**」を選択すると、非表示のすべてのコンポーネントが表示されます。
