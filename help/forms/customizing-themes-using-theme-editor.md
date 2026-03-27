---
title: テーマエディターを使用したアダプティブフォームのテーマのカスタマイズ
description: Adobe Experience Managerでテーマエディターを使用して、コアコンポーネントベースのアダプティブFormsのビジュアルテーマを作成およびカスタマイズする方法を説明します。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: f1b318803b9b854ec2ce800670f6484799113599
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 2%

---


# フォームテーマのカスタマイズ {#customizing-form-themes}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/template-editor.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager（AEM）Formsのテーマエディターは、コードを手動で記述することなく、アダプティブFormsのテーマを作成およびカスタマイズできるビジュアルインターフェイスです。 テーマは、背景色、フォントスタイル、境界線、寸法、間隔など、フォームコンポーネントやパネルのルックアンドフィールを定義します。 テーマを適用すると、指定したスタイルが対応するコンポーネントに反映され、複数のアダプティブ Formsで同じテーマを再利用できます。

テーマエディターにより、基本的なフォームのスタイル設定のための専用の開発者ペルソナは不要になります。 CSSの知識があれば、ビジュアルサイドバーを使用してフォームのスタイルを設定したり、エディター内でCSSの詳細な上書きを直接記述したりできます。

## 前提条件 {#prerequisites}

* Adobe Experience Manager Formsの作成者レベルの権限。
* CSS スタイルの原則に関する基本的な理解。 完全なCSS参照については、[MDN Web Docs CSS リファレンス ](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)を参照してください。

## テーマディレクトリに移動します {#navigate-to-themes}

1. AEM オーサーインスタンスにログインします。
1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL テーマ]**&#x200B;に移動します。

   テーマディレクトリには、AEM Canvasが提供する標準テーマを含め、利用可能なすべてのテーマと、ユーザーまたは組織が作成したカスタムテーマが表示されます。

### 新しいテーマの作成 {#create-a-new-theme}

1. テーマディレクトリで、新しいテーマを保存するフォルダーを選択します。
1. **[!UICONTROL 作成]** / **[!UICONTROL テーマ]**&#x200B;をクリックします。

   ![新しいテーマを作成](/help/forms/assets/custom-theme-create.png)

1. **[!UICONTROL テーマを作成]** ダイアログで、次の詳細を指定します。
   * **[!UICONTROL タイトル]**: テーマの説明的なタイトル。
   * **[!UICONTROL Name]**: テーマのノード名。
   * テーマをプレビューする&#x200B;**[!UICONTROL アダプティブフォーム]**: コアコンポーネントベースのアダプティブフォームをコアコンポーネントテーマとして選択します。 **[!UICONTROL デフォルトのアダプティブフォームを使用]**&#x200B;では、コアコンポーネントではなく基盤のアダプティブフォームを使用します。 選択したフォームは、編集中にリアルタイムにプレビューするためにテーマエディターキャンバスに表示されます。
   * **[!UICONTROL 説明]** *（オプション）*: テーマの簡単な説明。
   * **[!UICONTROL Configuration Container]** *（オプション）*: Adobe Font設定の詳細を保持する設定コンテナ。
   * **[!UICONTROL タグ]** *（オプション）*：識別と検索用にテーマに添付されたタグ。
1. 「**[!UICONTROL 作成]**」をクリックします。

   ![ カスタムテーマの設定](/help/forms/assets/custom-theme-name.png)

   テーマが作成されます。 **[!UICONTROL 編集]**&#x200B;をクリックして、テーマエディターで開くことができるようになりました。

### 既存のテーマの編集 {#edit-an-existing-theme}

1. **テーマ** ディレクトリで、変更するテーマを選択します。
1. アクションバーの&#x200B;**[!UICONTROL 編集]**&#x200B;をクリックして、テーマエディターでテーマを開きます。

   ![ テーマの編集](/help/forms/assets/custom-theme-edit.png)

### テーマをアップロード {#upload-a-theme}

テーマパッケージ（例えば、別の環境から書き出したテーマパッケージ）をテーマディレクトリに読み込むことができます。

1. **テーマ** ディレクトリで、**[!UICONTROL 作成]**/**[!UICONTROL ファイルアップロード]**&#x200B;をクリックします。
1. コンピューター上のテーマパッケージ（ZIP ファイル）を参照して選択し、「**[!UICONTROL アップロード]**」をクリックします。

   ![ テーマのアップロード – ファイルのアップロードオプションを使用したメニューの作成](/help/forms/assets/custom-theme-upload.png)

アップロードしたテーマはテーマディレクトリに表示され、他のテーマと同様に編集できます。

### テーマのダウンロード {#download-a-theme}

テーマをパッケージ（ZIP ファイル）として書き出して、別のAEM Forms環境で再利用したり、バックアップしたりできます。

1. **テーマ** ディレクトリで、1つ以上のテーマを選択します（テーマカードのチェックボックスを使用）。
1. アクションバーの「**[!UICONTROL ダウンロード]**」をクリックします。 選択したテーマの詳細を含むダイアログが表示されることがあります。
1. ダイアログで「**[!UICONTROL ダウンロード]**」を確認またはクリックします。 テーマパッケージは、ZIP ファイルとしてコンピューターにダウンロードされます。

   ![ テーマをダウンロード – テーマを選択し、「ダウンロード」をクリック ](/help/forms/assets/custom-theme-download.png)

このZIP ファイルは、後で[同じ環境または別の環境でテーマ ](#upload-a-theme)をアップロードすることでアップロードできます。

## テーマエディターのインターフェイス {#understand-the-theme-editor}

テーマエディターでテーマを開くと、次の2つの主な領域が表示されます。

![ テーマエディター](/help/forms/assets/custom-theme-editor.png)

* **キャンバス** （右側）: テーマにリンクされたアダプティブフォームのプレビューを表示します。 スタイルの変更はすべて瞬時に反映されるため、編集内容の影響をリアルタイムで確認できます。
* **サイドバー** （左側）: ページ、フォーム、フィールド、ボタン、パネル、画像、Captcha、reCaptchaなど、ツリー構造のすべてのスタイル可能なフォームコンポーネントを一覧表示する&#x200B;**セレクター** パネルが含まれています。

### カンバスツールバー {#canvas-toolbar}

![ サイドパネルの切り替え、取り消し、やり直し、エミュレーター、編集/プレビュー、およびテーマオプションを備えたテーマエディターキャンバスツールバー](/help/forms/assets/custom-theme-toolbar-utilities.png)

左から右へ、ツールバーには次の機能があります。
* **A: サイドパネルを切り替え**: セレクターのサイドバーを表示または非表示にします。 カンバスにフォーカスする場合はフォームのプレビュー領域を最大化し、コンポーネントの選択やスタイル設定が必要な場合はサイドバーをもう一度表示します。
* **B: テーマオプション** （ドロップダウン）: 4つのオプションを含むメニューを開きます。 プレビューフォームの変更、CSSの表示、保存したスタイルの管理、エディター内のヘルプの表示が必要な場合にクリックします。 テーマオプション ドロップダウンを開くと、次のような表示になります。

  ![設定、テーマ CSSの表示、スタイルの管理、ヘルプを表示するテーマ オプション ドロップダウン ](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL 設定]**: キャンバスに表示されているフォームを別のアダプティブフォームに切り替えます。 エディターを離れることなく、別のフォームでテーマがどのように表示されるかを確認する場合に使用します。
     ![ テーマのプレビュー用にアダプティブフォームを設定](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL テーマ CSS]**&#x200B;を表示：テーマの完全なコンパイル済みCSSを含むダイアログを開きます。 現在選択されているコンポーネントのCSSのみを表示するには、代わりにサイドバーで&#x200B;**[!UICONTROL CSS]**を表示します（ルールのデバッグまたはコピーに便利）。
     ![最終的なCSSを表示](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL スタイルの管理]**: ダイアログを開いて、テキストと画像のスタイルを保存、名前、再利用します。 保存したスタイルは他のコンポーネントに適用できます。最近使用したスタイルも簡単に再利用できます。
   * **[!UICONTROL ヘルプ]**: テーマエディターの画像ガイド付きツアーを開始します。
* **C：取り消し/やり直し**：最後のスタイル変更を元に戻すか、再適用します。 スタイルを試し、他の編集を失うことなく一歩下がりたい場合に便利です。
* **D: エミュレーター**: デバイスまたはブレークポイント （デスクトップ、タブレット、モバイルなど）を選択して、その画面サイズでフォームをプレビューします。 選択したブレークポイントに合わせて、フォームのプレビューのサイズが変更されます。 ブレークポイントの選択時に設定したスタイルは、そのブレークポイントにのみ適用されるため、レスポンシブスタイルを定義できます。 詳しくは、様々な画面サイズに合わせた[ スタイル設定](#styling-for-different-screen-sizes)を参照してください。
* **E：編集/ プレビュー**:2つのモードを切り替えます。 **編集**&#x200B;がデフォルトです。キャンバス上のコンポーネントをクリックして選択し、サイドバーでスタイルを変更できます。 **プレビュー**&#x200B;は、エンドユーザーが選択範囲の境界線、コンポーネントラベル、またはスタイル設定サイドバーなしでフォームを表示するので、フォームが公開される前に、テーマ別のフォームがどのように表示され、動作するかを確認できます。

<!--**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).-->

### コンポーネントのスタイル設定

スタイルを設定するコンポーネントは、次の2つの方法で選択できます。
* **キャンバスから**: フォーム内のコンポーネント（テキストフィールド、ボタン、ドロップダウンなど）を直接クリックします。 選択したエレメントが境界線でハイライト表示され、その上にコンポーネントラベル（例：「テキスト入力ウィジェット」）が表示されます。 そのコンポーネントのスタイル設定オプションがサイドバーに表示されます。

  ![ キャンバスからテーマを編集](/help/forms/assets/custom-theme-field-level.png)

* **セレクターパネル**&#x200B;から：左側のサイドバーのツリー構造を使用して、特定のコンポーネントをドリルダウンします。 例えば、**[!UICONTROL Field]** > **[!UICONTROL Widget]** > **[!UICONTROL Text Input]**&#x200B;を展開して、テキストボックスウィジェットを具体的にターゲットにします。

  ![ セレクターパネルからテーマを編集](/help/forms/assets/custom-theme-selector.png)

#### コンポーネントへのスタイルの適用 {#apply-styles-to-a-component}

コンポーネントを選択すると、サイドバーに使用可能なスタイル設定プロパティが次のカテゴリに整理されて表示されます。

* **[!UICONTROL 寸法と位置]**：整列、サイズ、パディング、マージン、幅、高さ、Z インデックスを制御します。
* **[!UICONTROL テキスト]**: フォントファミリー、太さ、色、サイズ、行の高さ、整列、文字間隔、テキストの装飾、変形を設定します。 サポートされているCSS テキストプロパティの一覧については、[MDN CSS テキストのドキュメント ](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text)を参照してください。
* **[!UICONTROL 背景]**：背景色、画像、またはグラデーションを設定します。 [MDN CSS背景ドキュメント ](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders)を参照してください。
* **[!UICONTROL 境界線]**：境界線の幅、スタイル、半径、カラーを定義します。
* **[!UICONTROL 効果]**：不透明度、描画モード、シャドウを追加します。

スタイルを適用するには：

1. カンバスまたはセレクターパネルからコンポーネントを選択します。
1. サイドバーで必要なビジュアルプロパティを設定します。 例えば、**[!UICONTROL 背景色]**&#x200B;を選択し、**[!UICONTROL フォントカラー]**&#x200B;を調整します。
1. チェックマークアイコン **[!UICONTROL OK]**&#x200B;をクリックして、プロパティの変更を確認します。

   ![ スタイルの適用](/help/forms/assets/custom-theme-applying-style.png)

<!--#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.-->

### フォームレベルのスタイル {#form-level-styling}

フォームレベルのスタイル設定では、同じタイプのすべてのコンポーネントに広くスタイルが適用されます。 例えば、**[!UICONTROL セレクター]** パネルで&#x200B;**フィールド**&#x200B;を選択し、背景色を青に設定した場合、フォームのすべてのフィールド（テキストボックス、数値ボックス、日付選択、ドロップダウン）はその青い背景を継承します。

**例：** フォームのすべてのフィールドに均一な背景色を設定するには：

1. **セレクター** パネルで、**[!UICONTROL フィールド]**&#x200B;を選択します。
1. サイドバーで、**[!UICONTROL 背景色]**&#x200B;を青に設定します。
1. 「**[!UICONTROL OK]**」をクリックします。

   ![ フォームレベルのスタイル設定](/help/forms/assets/custom-theme-form-level-styling.png)

フォーム内のすべてのフィールドコンポーネントに青色の背景が表示されるようになりました。

### コンポーネントレベルのスタイル {#component-level-styling}

コンポーネントレベルのスタイル設定は、特定のコンポーネントタイプをターゲットとし、より幅広いフォームレベルのスタイルを上書きします。 例えば、テキストボックスウィジェットのみを異なる背景色にし、他のすべてのフィールドを青のままにする場合は、テキストボックスウィジェットをターゲットにします。

**例：** テキストボックスウィジェットのみに緑色の背景と紫色のフォントを設定するには：

1. セレクターパネルで、**[!UICONTROL フィールド]** > **[!UICONTROL ウィジェット]** > **[!UICONTROL テキスト入力]**&#x200B;を展開します。
1. **[!UICONTROL Font Color]**を紫色に設定します。
   ![ フィールドレベルのスタイル設定](/help/forms/assets/custom-theme-field-level-styling1.png)
1. **[!UICONTROL 背景色]**を緑に設定します。
   ![ フィールドレベルのスタイル設定](/help/forms/assets/custom-theme-field-level-styling2.png)
1. 「**[!UICONTROL OK]**」をクリックします。

テキストボックスウィジェットに、紫色のテキストを含む緑色の背景が表示され、その他のフィールドはすべてフォームレベルのスタイルから青色のままになります。

>[!NOTE]
>
> **コンポーネントレベルのスタイル設定は、常にフォームレベルのスタイル設定よりも優先されます。** スタイルが両方のレベルで定義されている場合、より具体的なコンポーネントレベルのセレクターが、より幅広いフォームレベルのセレクターを上書きします。 これは、標準の[CSS特異性ルール ](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)に従います。 例えば、すべてのフィールド（フォームレベル）に青色の背景を設定し、テキストボックスウィジェット（コンポーネントレベル）に緑色の背景を設定した場合、テキストボックスには緑色の背景が表示されます。

## 様々な画面サイズに合わせたスタイル設定 {#styling-for-different-screen-sizes}

デバイスのサイズに合わせて異なるスタイルを定義し、レスポンシブなテーマを作成できます。 テーマエディターのツールバーには、**デバイスオプション** （例：iPhone 5、iPad、デスクトップ、タブレット、小さい画面）が表示され、その画面サイズでフォームのプレビューとスタイル設定を行うことができます。

1. カンバスツールバーで、**device emulator**&#x200B;を使用します。デバイスラベルのいずれかをクリックします（例：**[!UICONTROL デスクトップ]**、**[!UICONTROL タブレット]**、**[!UICONTROL iPad]**、**[!UICONTROL 小さい画面]**）。 フォームの上の定規は、選択したデバイスのピクセル幅を示します。
1. そのデバイスを選択した状態で、サイドバーを使用してスタイルを設定または調整します。 スタイルは、選択したデバイス ビューにのみ適用されます。
1. 別のデバイスに切り替え、必要に応じてスタイルを定義します。
1. **[!UICONTROL OK]**&#x200B;をクリックし、終了したらテーマを保存します。

   ![ テーマエディターのデバイスエミュレーター – ルーラーおよびデバイスオプション（デスクトップ、タブレット、iPad、小さい画面） ](/help/forms/assets/custom-theme-emulator.png)

したがって、同じテーマには、デバイスごとに異なる間隔、フォントサイズ、またはレイアウト関連のスタイルを設定でき、レスポンシブなスタイル設定の[AEM 6.5 テーマエディターの動作](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/template-editor.html?lang=ja)と一致します。

## 高度なCSS オーバーライドの使用 {#use-advanced-css-overrides}

ビジュアルサイドバーを通じて使用できないスタイルの場合は、エディターで直接カスタム CSSを記述できます。

1. コンポーネントを選択します。
1. サイドバーで、**[!UICONTROL 詳細]** セクションを展開します。
1. カスタム CSS ルールを&#x200B;**[!UICONTROL CSS オーバーライド]**&#x200B;領域に記述します。 これらのルールは、ビジュアルコントロールで設定されたプロパティが競合する場合に上書きされます。

完全なCSS プロパティリファレンスについては、[MDN Web Docs CSS リファレンス ](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)を参照してください。

### CSS擬似要素を追加 {#add-css-pseudo-elements}

**[!UICONTROL Advanced]** セクションでは、`::before`や`::after`などのCSS擬似要素もサポートしています。 これにより、フォーム構造を変更することなく、コンポーネントの周囲にコンテンツや装飾のスタイルを挿入できます。 例えば、テキストボックスコンポーネントの前にビジュアルインジケーターを追加するには、次の手順を実行します。

1. コンポーネントを選択します（例：`CMP Textbox`）。
1. 「**[!UICONTROL 詳細]**」セクションを展開します。
1. `::before`擬似要素フィールドに、次のようなCSS プロパティを追加します。

   ```css
   color: #B10DC9;
   ```

   ![CSS](/help/forms/assets/custom-theme-before-css.png)の前

1. `::after`擬似要素フィールドに、次のようなCSS プロパティを追加します。

   ```css
   color: #006400;
   ```

   ![CSS](/help/forms/assets/custom-theme-after-css.png)の後


これらの疑似要素は、標準のCSS動作に従います。 完全な参照については、[MDN CSS擬似要素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)を参照してください。

## ベストプラクティス {#best-practices}

* **正確なターゲティングにセレクターパネルを使用する**: フィールドラベルや長い説明など、ネストされた要素のスタイルを設定する場合は、カンバスをクリックするのではなく、左側のセレクターパネルを使用します。 これにより、適切なCSS セレクターが適切な特異性を持って生成されます。
* **他のテーマからのアセットの使用を避ける**: テーマを編集する場合は、他のテーマからアセット（画像など）を参照して追加しないでください。 ソーステーマを移動または削除すると、現在のテーマが壊れます。
* **コンテナパネルのレイアウト幅を変更しない**: コンテナパネルに固定幅を指定すると、コンテナパネルが静的になり、異なる画面サイズに適応できなくなります。

## 関連トピック {#see-also}

{{see-also}}