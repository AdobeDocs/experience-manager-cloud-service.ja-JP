---
title: ContextHub でのセグメント化の設定
description: ContextHubを使用してセグメントを設定する方法を説明します。
translation-type: tm+mt
source-git-commit: c9c7176f6c3bf70529b761183341a2490d4ecbfc
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 48%

---


# ContextHub でのセグメント化の設定{#configuring-segmentation-with-contexthub}

キャンペーンを作成する場合、セグメント化を考えることが重要になります。See [Understanding Segmentation](segmentation.md) for information on how segmentation works and key terms.

サイト訪問者についてこれまでに収集した情報と、達成する目標に応じて、ターゲットコンテンツに必要なセグメントと戦略を定義する必要があります。

このようなセグメントを使用して、訪問者に特定のターゲットコンテンツを提供します。ここで定義された[アクティビティ](activities.md)は、任意のページに追加できます。また、専用のコンテンツを適用できる訪問者セグメントを定義できます。

AEMを使用すると、ユーザーの体験を簡単にパーソナライズできます。 また、セグメント定義の結果を検証することもできます。

## セグメントへのアクセス {#accessing-segments}

The [Audiences](audiences.md) console is used to manage segments for ContextHub as well as audiences for your Adobe Target account. このドキュメントでは、ContextHub のセグメントの管理について取り上げます。

セグメントにアクセスするには、グローバルナビゲーションで&#x200B;**ナビゲーション／パーソナライズ機能／オーディエンス**&#x200B;を選択します。

![オーディエンスの管理](../assets/contexthub-segmentation-audiences.png)

## セグメントエディター {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
The **Segment Editor** allows you to easily modify a segment. セグメントを編集するには、セグメントリストからセグメントを選択し、「**編集**」ボタンをクリックします。

![セグメントエディター](../assets/contexthub-segment-editor.png)

Using the components browser you can add **AND** and **OR** containers to define the segment logic, then add additional components to compare properties and values or reference scripts and other segments to define the selection criteria (see [Creating a New Segment](#creating-a-new-segment)) to define the exact scenario for selecting the segment.

ステートメント全体が true と評価されると、セグメントは解決されます。In the event of multiple segments being applicable, then the **Boost** factor is also used. See [Creating a New Segment](#creating-a-new-segment) for details on the boost factor.

>[!CAUTION]
>
>セグメントエディターは、循環参照をチェックしません。例えば、セグメントAは別のセグメントBを参照し、次にセグメントAを参照します。セグメントAに循環参照が含まれていないことを確認する必要があります。

### コンテナ {#containers}

次のコンテナは標準で用意されており、比較や参照をグループ化してブール評価をおこなうために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。See the following section [Using AND and OR Containers](#using-and-and-or-containers) for more information.

|  |  |
|---|---|
| コンテナ AND | ブール値のAND演算子 |
| コンテナ OR | ブールOR演算子 |

### 比較 {#comparisons}

次のセグメント比較は標準で用意されており、セグメントプロパティを評価するために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。

|  |  |
|---|---|
| プロパティ — 値 | ストアのプロパティと定義済みの値を比較 |
| プロパティ — プロパティ | ストアの1つのプロパティと別のプロパティを比較 |
| プロパティセグメントの参照 | 店舗のプロパティを、参照されている別のセグメントと比較します |
| プロパティスクリプトの参照 | ストアのプロパティとスクリプトの結果を比較 |
| セグメントリファレンススクリプトリファレンス | 参照セグメントとスクリプトの結果を比較 |

>[!NOTE]
>
>値を比較する際に、比較のデータタイプが設定されていない場合（つまり自動検出に設定されている場合）、ContextHubのセグメント化エンジンは、値をJavaScriptと同様に比較します。 値が想定されたタイプにキャストされないので、誤解を招く結果となることがあります。次に例を示します。
>
>`null < 30 // will return true`
>
>Therefore when [creating a segment](#creating-a-new-segment), you should select a **data type** whenever the types of compared values are known. 次に例を示します。
>
>When comparing the property `profile/age`, you already know that the compared type will be **number**, so even if `profile/age` is not set, a comparison `profile/age` less-than 30 will return **false**, as you would expect.

### 参照 {#references}

次の参照は標準で用意されており、スクリプトや別のセグメントに直接リンクするために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。

|  |  |
|---|---|
| セグメントの参照 | 参照先セグメントを評価 |
| スクリプト参照 | 参照先のスクリプトを評価します。 詳しくは、次の「スクリプト参照の [使用](#using-script-references) 」の節を参照してください。 |

## 新しいセグメントの作成 {#creating-a-new-segment}

新しいセグメントを定義するには：

1. セグメント [に](#accessing-segments)アクセスした後 [](#organizing-segments) 、セグメントを作成するフォルダーに移動するか、ルートに残します。

1. 「 **作成** 」ボタンをタップまたはクリックし、「ContextHubセグメントを **作成**」を選択します。

   ![追加セグメント](../assets/contexthub-create-segment.png)

1. 「**新しい ContextHub セグメント**」で、セグメントのタイトルと必要に応じてブースト値を入力し、「**作成**」をタップまたはクリックします。

   ![新しいセグメント](../assets/contexthub-new-segment.png)

   各セグメントには、重み付け係数として使用されるブーストパラメータがあります。 複数のセグメントが有効である場合、数値が小さいセグメントよりも、数値が大きいセグメントのほうが優先して選択されます。

   * 最小値：`0`
   * 最大値：`1000000`

1. セグメントコンソールから、新しく作成したセグメントを編集し、セグメントエディターで開きます。
1. 比較または参照をセグメントエディターにドラッグすると、デフォルトの AND コンテナに表示されます。
1. 新しい参照またはセグメントの設定オプションをダブルクリックまたはタップして、特定のパラメーターを編集します。この例では、バーゼルのユーザーのテストを行っています。

   ![バーゼルでの人のテスト](../assets/contexthub-comparing-property-value.png)

   比較が適切に評価されるように、可能であれば常に「**データタイプ**」を設定します。詳しくは、[比較](#comparisons)を参照してください。

1. Click **Done** to save your definition:
1. 必要に応じてその他のコンポーネントを追加します。AND 比較および OR 比較のコンテナコンポーネントを使用して、ブール式を作成できます（後述の [AND コンテナと OR コンテナの使用](#using-and-and-or-containers)を参照）。セグメントエディターでは、不要になったコンポーネントを削除したり、コンポーネントをステートメント内の別の場所へドラッグしたりすることができます。

### AND コンテナと OR コンテナの使用 {#using-and-and-or-containers}

AND および OR コンテナコンポーネントを使用すると、AEM で複雑なセグメントを作成できます。この際、次の基本事項に留意してください。

* 定義の最上位レベルは必ず、最初に作成された AND コンテナになります。これは変更できませんが、他のセグメント定義には影響しません。
* コンテナのネストが意味のあるものになっていることを確認してください。コンテナは、ブール式の括弧として見ることができます。

次の例は、スイスのターゲットグループで考慮される訪問者を選択する場合に使用します。

```text
 People in Basel

 OR

 People in Zürich
```

最初に、OR コンテナコンポーネントをデフォルトの AND コンテナ内に配置します。ORコンテナ内で、プロパティまたは参照コンポーネントを追加できます。

![OR演算子を使用したセグメント](../assets/contexthub-or-operator.png)

必要に応じて、複数のANDおよびOR演算子をネストできます。

### スクリプト参照の使用 {#using-script-references}

スクリプト参照コンポーネントを使用すると、セグメントプロパティの評価を外部スクリプトに委任できます。適切に設定したスクリプトは、セグメント条件の他のコンポーネントと同じように使用できます。

#### 参照するスクリプトの定義 {#defining-a-script-to-reference}

1. Add file to `contexthub.segment-engine.scripts` clientlib.
1. 値を返す関数を実装します。次に例を示します。

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Register the script with `ContextHub.SegmentEngine.ScriptManager.register`.

その他のプロパティに依存するスクリプトでは、`this.dependOn()` () を呼び出す必要があります。For example if the script depends on `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### スクリプトの参照 {#referencing-a-script}

1. ContextHub セグメントを作成します。
1. **スクリプト参照**&#x200B;コンポーネントをセグメントの目的の場所に追加します。
1. **スクリプト参照**&#x200B;コンポーネントの編集ダイアログを開きます。スクリプトが[適切に設定](#defining-a-script-to-reference)されていれば、「**スクリプト名**」ドロップダウンに表示されます。

## セグメントの整理 {#organizing-segments}

多数のセグメントがある場合、フラットリストとして管理が困難になる可能性があります。 このような場合は、フォルダーを作成してセグメントを管理すると便利です。

### Create a New Folder {#create-folder}

1. After [accessing the segments](#accessing-segments), click or tap the **Create** button and select **Folder**.

   ![追加フォルダ](../assets/contexthub-create-segment.png)

1. フォルダーの **タイトル** と **** 名前を入力します。
   * タイトル **は説明的なもの** 。
   * 「 **名前** 」は、リポジトリのノード名になります。
      * タイトルに基づいて自動的に生成され、 [AEMの命名規則に従って調整されます。](/help/implementing/developing/introduction/naming-conventions.md)
      * 必要に応じて調整できます。

   ![フォルダーを作成](../assets/contexthub-create-folder.png)

1. 「**作成**」をタップまたはクリックします。

   ![フォルダの確認](../assets/contexthub-confirm-folder.png)

1. フォルダーがセグメントのリストに表示されます。
   * 列の並べ替え方法は、リスト内の新しいフォルダが表示される場所に影響します。
   * 列見出しをタップまたはクリックして並べ替えを調整できます。
      ![新しいフォルダー](../assets/contexthub-folder.png)

### 既存のフォルダの変更 {#modify-folders}

1. セグメント [にアクセスした後](#accessing-segments)、変更するフォルダーをクリックまたはタップして選択します。

   ![フォルダーを選択](../assets/contexthub-select-folder.png)

1. ツールバーの「 **名前を変更** 」をタップまたはクリックして、フォルダー名を変更します。

1. 新しい **フォルダータイトルを指定し** 、「 **保存**」をタップまたはクリックします。

   ![フォルダ名の変更](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>フォルダ名を変更する場合は、タイトルのみを変更できます。 名前は変更できません。

### フォルダの削除

1. セグメント [にアクセスした後](#accessing-segments)、変更するフォルダーをクリックまたはタップして選択します。

   ![フォルダーを選択](../assets/contexthub-select-folder.png)

1. ツールバーの「 **削除** 」をタップまたはクリックして、フォルダーを削除します。

1. 削除対象として選択したフォルダのリストがダイアログに表示されます。

   ![削除の確認](../assets/contexthub-confirm-segment-delete.png)

   * 「 **削除** 」をタップまたはクリックして確定します。
   * 「 **キャンセル** 」をタップまたはクリックして中止します。

1. 選択したフォルダーのいずれかにサブフォルダーまたはセグメントが含まれている場合は、そのフォルダーの削除を確認する必要があります。

   ![子の削除の確認](../assets/contexthub-confirm-segment-child-delete.png)

   * 「削除を **強制** 」をタップまたはクリックして確定します。
   * 「 **キャンセル** 」をタップまたはクリックして中止します。

>[!NOTE]
>
> あるフォルダーから別のフォルダーにセグメントを移動することはできません。

## セグメントの適用のテスト {#testing-the-application-of-a-segment}

セグメントを定義したら、**[ContextHub](contexthub.md)** を使用して、考えられる結果についてテストすることができます。

1. ページのプレビュー
1. ContextHub アイコンをクリックして ContextHub ツールバーを表示します。
1. 作成したセグメントと一致するペルソナを選択します。
1. ContextHub によって、選択したペルソナに適用できるセグメントが解決されます。

例えば、Baselでユーザーを識別するための単純なセグメント定義は、ユーザーの場所に基づいています。 これらの条件に一致する特定の人物を読み込むと、セグメントが正常に解決されたかどうかが表示されます。

![解決されるセグメント](../assets/contexthub-segment-resolve.png)

解決されていない場合は次のようになります。

![解決されないセグメント](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>すべての特性がただちに解決されます。ただし、ほとんどの特性はページを再読み込みしたときにのみ変更されます。

このようなテストは、ターゲットコンテンツや関連する&#x200B;**アクティビティ**&#x200B;および&#x200B;**エクスペリエンス**&#x200B;と組み合わせて、コンテンツページでも実行できます。

アクティビティとエクスペリエンスを設定した場合は、アクティビティを使用してセグメントを簡単にテストできます。 アクティビティの設定について詳しくは、[ターゲットコンテンツのオーサリングに関するドキュメント](targeted-content.md)を参照してください。

1. ターゲットコンテンツを設定したページの編集モードでは、ターゲットとなるコンテンツが矢印アイコンによって示されます。
1. プレビューモードに切り替えてから、ContextHub を使用して、エクスペリエンスに設定されているセグメント化と一致しないペルソナに切り替えます。
1. エクスペリエンスに設定されているセグメント化と一致するペルソナに切り替え、それに応じてエクスペリエンスが変化することを確認します。

## セグメントの使用 {#using-your-segment}

セグメントは、特定のターゲットオーディエンスが表示する実際のコンテンツを制御するために使用します。 See [Managing Audiences](audiences.md) for more information about audiences and segments and [Authoring Targeted Content](targeted-content.md) about using audiences and segments to target content.
