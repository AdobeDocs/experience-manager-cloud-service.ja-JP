---
title: バリエーションの生成
description: AEM as a Cloud Serviceからアクセスできるバリエーションの生成とEdge Delivery ServicesのSidekickについて説明します
exl-id: 9114037f-37b9-4b2f-a714-10933f69b2c3
feature: Generate Variations
role: Admin, Architect, Developer
source-git-commit: bbc51796c610af02b5260c063213cde2ef610ba2
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---


# バリエーションの生成 {#generate-variations}

デジタルチャネルを最適化し、コンテンツの作成を高速化する方法を探している場合は、バリエーションの生成を使用できます。 バリエーションを生成では、ジェネレーティブ人工知能（AI）を使用して、プロンプトに基づくコンテンツのバリエーションを作成します。これらのプロンプトは、Adobeから提供されるか、ユーザーが作成および管理します。 バリエーションを作成した後、Web サイトでコンテンツを使用したり、[Edge Delivery Services[ の ](https://www.aem.live/docs/experimentation) 実験 ](/help/edge/overview.md) 機能を使用して成功を測定したりできます。

[ バリエーションを生成 ](#access-generate-variations) には、次の場所からアクセスできます。

* [Adobe Experience Manager（AEM）as a Cloud Service内](#access-aemaacs)
* [AEM Edge Delivery ServicesのSidekick](#access-aem-sidekick)
* [コンテンツフラグメントエディター内](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)

>[!NOTE]
>
>どのような場合でも、バリエーションの生成を使用するには、[ アクセスの前提条件 ](#access-prerequisites) が満たされていることを確認する必要があります。

これにより、以下のことが可能になります。

* [ 基本を学ぶ ](#get-started)Adobeが特定のユースケース用に作成したプロンプトテンプレートを使用する。
* [ 既存のプロンプトを編集 ](#edit-the-prompt) できます。
* または [ 独自のプロンプトを作成および使用する ](#create-prompt):
   * 後で使用できるように [ プロンプトを保存 ](#save-prompt) します
   * [ 共有プロンプトへのアクセスと使用 ](#select-prompt) 組織全体
* [ パーソナライズされたオーディエンス固有のコンテンツの生成 ](#audiences) 時に、プロンプトで使用する [ オーディエンス ](#generate-copy) セグメントを定義します。
* 必要に応じて、変更を加えたり結果を調整したりする前に、プロンプトと共に出力をプレビューします。
* コピーバリエーションに基づいて ](#generate-image) 画像を生成するために、[Adobe Expressを使用します。これには、Fireflyの生成 AI 機能が使用されます。
* Web サイトで使用するコンテンツや実験で使用するコンテンツを選択します。

## 法的事項および使用上の注意 {#legal-usage-note}

ジェネレーティブ AI とAEM用 Generate バリエーションは強力なツールです。ただし、出力の使用は **ユーザー** が担当します。

サービスへの入力は、コンテキストに関連付ける必要があります。 このコンテキストには、ブランディング資料、web サイトコンテンツ、データ、このようなデータのスキーマ、テンプレートまたはその他の信頼できるドキュメントを使用できます。

出力の精度は、ユースケースに合わせて評価する必要があります。

バリエーションを生成を使用する前に、[Adobe生成 AI ユーザーガイドライン ](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) に同意する必要があります。

[ バリエーションを生成の使用 ](#generative-action-usage) は、生成アクションの使用に関連付けられています。

## 概要 {#overview}

「バリエーションを生成」を開き（左側のパネルを展開して）、次の項目が表示されます。

![ バリエーションを生成 – メインパネル ](assets/generate-variations-main-panel.png)

* 右側のパネル
   * これは、左側のナビゲーションで選択した内容によって異なります。
   * デフォルトでは、**プロンプトテンプレート** が表示されます。
* 左側のナビゲーション
   * **バリエーションを生成** の左側には、左側のナビゲーションパネルを展開または非表示にするオプション（サンドイッチメニュー）があります。
   * **プロンプト テンプレート**:
      * 様々なプロンプトへのリンクを表示します。これにはプロンプトを含めることができます。
         * コンテンツの生成に役立つようにAdobeによって提供されます。「Adobe」アイコンのフラグが付いています。
         * 自分で作成します。
         * IMS 組織内で作成されました。複数のヘッドを示すアイコンが付いています。
      * 独自のプロンプトを作成するための [ 新しいプロンプト ](#create-prompt) リンクが含まれます。
      * 自分で、または IMS 組織内で作成されたプロンプトを **削除** できます。 それには、該当するカードの楕円でアクセスしたメニューを使用します。
   * [ お気に入り ](#favorites)：お気に入りとしてフラグを設定した、以前の世代の結果を表示します。
   * [ 最近 ](#recents)：最近使用したプロンプトおよびその入力へのリンクを提供します。
   * **ヘルプと FAQ**:FAQ を含むドキュメントへのリンクです。
   * **ユーザーガイドライン**：法務ガイドラインへのリンク。

## はじめに {#get-started}

インターフェイスのガイドに従ってコンテンツを生成できます。 インターフェイスを開いた後、最初の手順は使用するプロンプトを選択することです。

### プロンプトを選択 {#select-prompt}

メインパネルから、次の項目を選択できます。

* コンテンツの生成を開始するためにAdobeから提供されたプロンプトテンプレート。
* [ 新しいプロンプト ](#create-prompt)：独自のプロンプトを作成する
* 自身が使用するためにのみ作成したテンプレート
* 自分または組織内のユーザーが作成したテンプレート。

区別するには：

* Adobeが指定したプロンプトには、Adobeアイコンのフラグが付きます
* IMS 組織全体で使用可能なプロンプトには、複数ヘッドのアイコンが付きます。
* プライベートプロンプトには、特別なフラグは付きません。

![ バリエーションの生成 – プロンプトテンプレート ](assets/generate-variations-prompt-templates.png)

### 入力を指定 {#provide-inputs}

ジェネレーティブ AI から適切なコンテンツを取り戻すことができるように、プロンプトごとに特定の情報を指定する必要があります。

入力フィールドの指示に従って、必要な情報を入力します。 そのため、特定のフィールドには、デフォルト値を使用したり、必要に応じて変更したり、要件を説明する説明を追加したりできます。

複数のプロンプトに共通する複数のキー入力フィールドがあります（特定のフィールドが常に使用できるとは限りません）。

* **Count of**/**Number of**
   * 1 つの世代で作成するコンテンツバリエーションの数を選択できます。
   * プロンプトに応じて、様々なラベル（カウント、バリエーション数、アイデア数など）の 1 つが表示される場合があります。
* **オーディエンス Source**/**Target オーディエンス**
   * 特定のオーディエンスに対してパーソナライズされたコンテンツを生成できます。
   * Adobeには、デフォルトオーディエンスが用意されています。または、追加のオーディエンスを指定できます。[ オーディエンス ](#audiences) を参照してください。
* **追加のコンテキスト**
   * ジェネレーティブ AI が入力に基づいてより優れた応答を作成するのに役立つ、関連するコンテンツを挿入します。 例えば、特定のページや製品の web バナーを作成する場合に、そのページや製品に関する情報を含めることができます。
* **温度**
を使用して、Adobe生成 AI の温度を変更します。
   * 温度が高いほど、プロンプトから逸脱し、より多くのバリエーション、ランダム性、創造性につながります。
   * 温度が低いほど、より決定的で、プロンプトに近い状態になります。
   * デフォルトでは、温度は 1 に設定されています。 生成された結果が気に入らない場合は、異なる温度を試すことができます。
* **プロンプトの編集**
   * 基になる [ プロンプトを編集 ](#edit-the-prompt) して、生成された結果を絞り込むことができます。

### コピーを生成 {#generate-copy}

入力フィールドに入力したり、プロンプトを変更したりしたら、コンテンツを生成して応答をレビューする準備が整います。

**生成** を選択して、生成 AI によって生成された応答を確認します。 生成されたコンテンツのバリエーションは、生成したプロンプトの下に表示されます。

![ バリエーションを生成 – コピーを生成 ](assets/generate-variations-generate-content.png)

>[!NOTE]
>
>ほとんどのAdobeプロンプトテンプレートには、バリエーション対応に **AI の根拠** が含まれています。 これにより、生成 AI が特定のバリエーションを生成した理由が明確になります。

1 つのバリエーションを選択した場合、次のアクションを使用できます。

* **お気に入り**
   * 今後の使用のために **お気に入り** としてフラグを設定します（[ お気に入り ](#favorites) に表示されます）。
* サムズアップ/サムズダウン
   * サムズアップ/ダウンインジケーターを使用して、応答の質をAdobeに通知します。
* **コピー**
   * クリップボードにコピーして、Web サイト上のコンテンツをオーサリングする際や [ 実験 ](https://www.aem.live/docs/experimentation) で使用します。
* **削除**

入力またはプロンプトを調整する必要がある場合は、調整を行い、**生成** を再度選択して、一連の新しい応答を取得できます。 新しいプロンプトと応答は、最初のプロンプトと応答の下に表示されます。上下にスクロールして、様々なコンテンツセットを表示できます。

各バリエーションのセットの上には、それらを作成したプロンプトと **再利用** オプションがあります。 入力を含むプロンプトを再実行する必要がある場合は、[**再利用**] を選択して **入力** に再ロードします。

### 画像を生成 {#generate-image}

テキストバリエーションを生成したら、Fireflyの生成 AI 機能を使用して、Adobe Expressで画像を生成できます。

>[!NOTE]
>
>**画像を生成** は、IMS 組織の一部としてAdobe Express使用権限があり、Admin Consoleでアクセス権が付与されている場合にのみ使用できます。

バリエーションを選択し、続いて **Generate Image** を選択して、[Adobe Express **で** Text to Image](https://www.adobe.com/express/) を直接開きます。 プロンプトはバリアントの選択に基づいて事前入力され、画像はそのプロンプトに従って自動的に生成されます。

![ バリエーションの生成 – 画像の表現 ](assets/generate-variations-express-images.png)

さらに次の変更を行うことができます。

* 表示する内容を記述して [Adobe Expressで独自のプロンプトを記述 ](https://helpx.adobe.com/firefly/using/tips-and-tricks.html) します。
* 「**テキストから画像へ** オプションを調整し、
* 次に **更新** 生成された画像。

また、「**その他を検索** を使用して、さらに高度な設定を行うこともできます。

完了したら、目的の画像を選択し **「保存** してAdobe Expressを閉じます。 画像が返され、バリエーションと共に保存されます。

![ バリエーションの生成 – Express 画像を保存しました ](assets/generate-variations-express-image-saved.png)

画像の上にマウスポインターを置くと、次のアクション項目を表示できます。

* **コピー**:[ 画像をクリップボードにコピーして他で使用します ](#use-content)
* **編集**:Adobe Expressを開いて、画像を変更できるようにします
* **ダウンロード**：画像をローカルマシンにダウンロードします
* **削除**：バリエーションから画像を削除します

>[!NOTE]
>
>[Content credentials](https://helpx.adobe.com/creative-cloud/help/content-credentials.html) は、ドキュメントベースのオーサリングで使用される場合、保持されません。

### コンテンツの使用 {#use-content}

生成 AI で生成されたコンテンツを使用するには、コンテンツをクリップボードにコピーして、他で使用できるようにする必要があります。

これは、コピーアイコンを使用して行います。

* テキストの場合：バリエーションパネルに表示されているコピーアイコンを使用します
* 画像の場合：画像の上にマウスポインターを置くと、コピーアイコンが表示されます

クリップボードにコピーしたら、情報を貼り付けて、web サイトのコンテンツをオーサリングする際に使用できます。 [ 実験 ](https://www.aem.live/docs/experimentation) を実行することもできます。

## お気に入り {#favorites}

コンテンツを確認した後、選択したバリエーションをお気に入りとして保存できます。

保存すると、左側のナビゲーションの **お気に入り** の下に表示されます。 お気に入りは（ブラウザーのキャッシュを **削除** またはクリアするまで）保持されます。

* お気に入りとバリエーションをクリップボードにコピー/貼り付けて、web サイトコンテンツで使用できます。
* お気に入りは **削除** できます。

## 最近使用したもの {#recents}

このセクションには、最近のアクティビティへのリンクが表示されます。 「**生成**」を選択すると、「**最近**」エントリが追加されます。 これには、プロンプト名とタイムスタンプがあります。 リンクを選択すると、プロンプトが読み込まれ、必要に応じて入力フィールドに値が入力され、生成されたバリエーションが表示されます。

## プロンプトを編集する {#edit-the-prompt}

基になるプロンプトは編集できます。 次の操作が可能です。

* 生成された結果を取得する場合は、さらに絞り込む必要があります
* 後で使用するために、変更して [ プロンプトを保存 ](#save-prompt) する

**プロンプトを編集** を選択します。

![ バリエーションの生成 – 編集プロンプト ](assets/generate-variations-prompt-edit.png)

これによりプロンプトエディターが開き、変更を加えることができます。

![ バリエーションを生成 – プロンプトエディター ](assets/generate-variations-prompt-editor.png)

### プロンプト入力の追加 {#add-prompt-inputs}

プロンプトを作成または編集する際に、入力フィールドを追加できます。 入力フィールドはプロンプトの変数として機能し、同じプロンプトを様々なシナリオで柔軟に使用できるようにします。 これにより、ユーザーはプロンプト全体を記述しなくても、プロンプトの特定の要素を定義できます。

* フィールドは、プレースホルダー名を囲む `{{ }}` に二重の中括弧で定義されます。
例えば、`{{tone_of_voice}}` のように指定します。

  >[!NOTE]
  >
  >二重中括弧の間にスペースを入れることはできません。

* また、`METADATA` の下で定義され、次のパラメーターが指定されます。
   * `label`
   * `description`
   * `default`
   * `type`

#### 例：新しいテキストフィールドの追加 – 声のトーン {#example-add-new-text-field-tone-of-voice}

**トーン・オブ・ボイス** というタイトルの新しいテキスト・フィールドを追加するには、プロンプトで次の構文を使用します。

```prompt
{{@tone_of_voice, 
  label="Tone of voice",
  description="Indicate the desired tone of voice",
  default="optimistic, smart, engaging, human, and creative",
  type=text
}}
```

![ バリエーションの生成 – 音声トーンで編集されたプロンプト ](assets/generate-variations-prompt-edited.png)

<!--
#### Example: Add new dropdown field - Page Type {#example-add-new-dropdown-field-page-type}

To create an input field Page Type providing a dropdown selection:

1. Create a spreadsheet named `pagetype.xls` in the top-level directory of your folder structure.
1. Edit the spreadsheet:

   1. Create two columns: **Key** and **Value**.
   1. In the **Key** column, enter labels that will appear in the dropdown.
   1. In the **Value** column, describe the key value so the generative AI has context.

1. In your prompt, refer to the title of the spreadsheet along with the appropriate type. 

   ```prompt
   {{@page_type, 
     label="Page Type",
     description="Describes the type of page",
     spreadsheet=pagetype
   }}
   ```
-->

## プロンプトの作成 {#create-prompt}

**プロンプトテンプレート** から **新しいプロンプト** を選択すると、新しいパネルで新しいプロンプトを入力できます。 次に、これらを **温度** と共に指定して **生成** コンテンツを生成できます。

プロンプトを今後保存する方法については、[ プロンプトの保存 ](#save-prompt) を参照してください。

独自のプロンプト入力の追加について詳しくは、[ プロンプト入力の追加 ](#add-prompt-inputs) を参照してください。

UI での書式設定を保持し、ドキュメントベースのオーサリングフローにコピーして貼り付ける際に書式設定を保持する場合は、プロンプトに次の内容を含めます。

<!-- CHECK - are the double-quotes needed? -->

* `"Format the response as an array of valid, iterable RFC8259 compliant JSON"`

次の画像は、この方法の利点を示しています。

* 最初の例では、`Title` と `Description` が結合されています
* 2 つ目の例では別々にフォーマットされていますが、これはプロンプトに JSON リクエストを含めることで行われています。

![ バリエーションの生成 – タイトルと説明を個別に書式設定したプロンプト ](assets/generate-variations-prompt-formatted.png)

## プロンプトを保存 {#save-prompt}

プロンプトを編集または作成した後、IMS 組織または自分自身のために、後で使用するためにプロンプトを保存することができます。 保存したプロンプトは、**プロンプトテンプレート** カードとして表示されます。

プロンプトを編集すると、**Generate** の左側の入力セクションの下部に **Save** オプションが表示されます。

選択すると、**プロンプトを保存** ダイアログが開きます。

![ バリエーションを生成 – 保存プロンプトのダイアログ ](assets/generate-variations-prompt-save-dialog.png)

1. 一意の **プロンプト名** を追加します。**プロンプトテンプレート** 内でプロンプトを識別するために使用します。
   1. 一意の新しい名前を指定すると、新しいプロンプト テンプレートが作成されます。
   1. 既存の名前を指定すると、プロンプトが上書きされ、メッセージが表示されます。
1. 必要に応じて、説明を追加します。
1. プロンプトをプライベートにするか、IMS 組織全体で使用可能にするかに応じて、オプション **組織全体で共有** を有効または無効にします。 このステータスは、[ プロンプトテンプレートに表示される結果カード ](#select-prompt) に表示されます。
1. **保存** プロンプト、または **キャンセル** アクション。

>[!NOTE]
>
>既存のプロンプトを上書きまたは更新すると、通知が送信されます（警告）。

>[!NOTE]
>
>**プロンプトテンプレート** から、自分または IMS 組織内で作成されたプロンプトを（楕円でアクセスされるメニューを使用して）削除できます。

## 対象読者 {#audiences}

パーソナライズされたコンテンツを生成するには、ジェネレーティブ AI がオーディエンスを理解している必要があります。 Adobeには、多数のデフォルトオーディエンスが用意されています。独自のオーディエンスを追加することもできます。

オーディエンスを追加する場合は、自然言語でオーディエンスを記述する必要があります。 次に例を示します。

* オーディエンスを作成するには：
   * `Student`
* 次のようになります。
   * `The audience consists of students, typically individuals who are pursuing education at various academic levels, such as primary, secondary, or tertiary education. They are engaged in learning and acquiring knowledge in diverse subjects, seeking academic growth, and preparing for future careers or personal development.`

次の 2 つのオーディエンスソースをサポートしています。

* [Adobe Target](#audience-adobe-target)
* [CSV ファイル](#audience-csv-file)

![ バリエーションの生成 – オーディエンスソース ](assets/generate-variations-audiences.png)

### 対象読者 – Adobe Target {#audience-adobe-target}

プロンプトで **Adobe Target** オーディエンスを選択すると、そのオーディエンスに合わせてコンテンツを作成できます。

>[!NOTE]
>
>このオプションを使用するには、IMS 組織がAdobe Targetにアクセスできる必要があります。

1. 「**Adobe Target**」を選択します。
1. 次に、表示されるリストから必要な **ターゲットオーディエンス** を選択します。

   >[!NOTE]
   >
   >**Adobe Target** オーディエンスを使用するには、説明フィールドに入力する必要があります。 そうでない場合、オーディエンスはドロップダウンリストで使用不可として表示されます。 説明を追加するには、Target に移動し、[ オーディエンスの説明を追加 ](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences) します。

   ![ バリエーションの生成 – オーディエンスソース - Adobe Target](assets/generate-variations-audiences-adobe-target.png)

#### Adobe Target オーディエンスを追加 {#add-adobe-target-audience}

Adobe Targetでオーディエンスを作成するには、[ オーディエンスの作成 ](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences) を参照してください。

### オーディエンス - CSV ファイル {#audience-csv-file}

プロンプトで **CSV ファイル** オーディエンスを選択すると、選択した **ターゲットオーディエンス** に合わせてコンテンツを生成できます。

Adobeでは、使用するオーディエンスの数を用意しています。

1. **CSV ファイル** を選択します。
1. 次に、表示されるリストから必要な **ターゲットオーディエンス** を選択します。

   ![ バリエーションの生成 – オーディエンスソース - CSV ファイル ](assets/generate-variations-audiences-csv-file.png)

#### オーディエンス CSV ファイルを追加 {#add-audience-csv-file}

様々なプラットフォーム（Google ドライブ、Dropbox、SharePoint など）から CSV ファイルを追加できます。このプラットフォームでは、ファイルの公開後に、ファイルへの URL を指定できます。

>[!NOTE]
>
>共有プラットフォームでは、ファイルを公開してアクセスできるようにする *必要があります*。

例えば、Google ドライブのファイルからオーディエンスを追加するには、次のようにします。

1. Google Drive で、次の 2 つの列を持つスプレッドシートファイルを作成します。
   1. 最初の列がドロップダウンに表示されます。
   1. 2 番目の列はオーディエンスの説明です。
1. ファイルをPublishします。
   1. ファイル/共有/web に公開/CSV
1. 公開されたファイルに URL をコピーします。
1. バリエーションを生成に移動します。
1. プロンプトエディターを開きます。
1. メタデータで **Adobe Target** オーディエンスを見つけて、URL を置き換えます。

   >[!NOTE]
   >
   >URL の両端に二重引用符（&quot;）が付いていることを確認してください。

   次に例を示します。

   ![ バリエーションの生成 – オーディエンス CSV ファイルの追加 ](assets/generate-variations-audiences-csv-save.png)

## 生成アクションの使用 {#generative-action-usage}

使用状況の管理は、実行されるアクションに応じて異なります。

* バリエーションの生成

  コピーバリアントの 1 つの世代は、1 つの生成アクションと等しくなります。 お客様は、AEM ライセンスに一定数の生成アクションが付属しています。 基本使用権限が消費されると、追加のアクションを購入できます。

  >[!NOTE]
  >
  >[Adobe Experience Manager:Cloud Serviceを参照してください |製品説明 ](https://helpx.adobe.com/legal/product-descriptions/aem-cloud-service.html) 基本使用権限の詳細については、アカウントチームにお問い合わせください。より生産的なアクションを購入したい場合は、お問い合わせください。

* Adobe Express

  画像生成の使用は、Adobe Expressの使用権限と [ 生成クレジット ](https://helpx.adobe.com/firefly/using/generative-credits-faq.html) で処理されます。

## Access バリエーションを生成 {#access-generate-variations}

前提条件を満たしたら、AEM as a Cloud ServiceまたはEdge Delivery ServicesのSidekickからバリエーションを生成にアクセスできます。

### アクセスのための前提条件 {#access-prerequisites}

バリエーションの生成を使用するには、前提条件を満たしていることを確認する必要があります。

* [Edge Delivery Servicesを持つExperience Managerのas a Cloud Serviceへのアクセス](#access-to-aemaacs-with-edge-delivery-services)

#### Edge Delivery Servicesを持つExperience Managerのas a Cloud Serviceへのアクセス{#access-to-aemaacs-with-edge-delivery-services}

バリエーションを生成するためのアクセス権を必要とするユーザーは、Edge Delivery Servicesを持つExperience Managerのas a Cloud Serviceを取得する権限が必要です。

>[!NOTE]
>
>AEM Sitesのas a Cloud Serviceの契約にEdge Delivery Servicesが含まれていない場合、アクセスするには新しい契約に署名する必要があります。
>
>Edge Delivery Servicesを使用してAEM Sitesのas a Cloud Service版に移行する方法については、アカウントチームにお問い合わせください。

特定のユーザーにアクセス権を付与するには、そのユーザーアカウントをそれぞれの製品プロファイルに割り当てます。 詳しくは [AEM製品プロファイルの割り当て ](/help/journey-onboarding/assign-profiles-cloud-manager.md) を参照してください。

### AEM as a Cloud Serviceからのアクセス {#access-aemaacs}

「バリエーションを生成」は、AEM as a Cloud Serviceの [ ナビゲーションパネル ](/help/sites-cloud/authoring/basic-handling.md#navigation-panel) からアクセスできます。

![ナビゲーションパネル](/help/sites-cloud/authoring/assets/basic-handling-navigation.png)

### AEM Sidekickからのアクセス {#access-aem-sidekick}

（Edge Delivery Servicesの）Sidekickから「バリエーションを生成」にアクセスするには、ある程度の設定が必要です。

1. Sidekickのインストールおよび設定方法については、[AEM Sidekickのインストール ](https://www.aem.live/docs/sidekick-extension) を参照してください。

1. （Edge Delivery Servicesの）Sidekickでバリエーションを生成を使用するには、の下のEdge Delivery Servicesプロジェクトに次の設定を含めます。

   * `tools/sidekick/config.json`

   これは、既存の設定に結合してからデプロイする必要があります。

   次に例を示します。

   ```prompt
   {
     // ...
     "plugins": [
       // ...
       {
         "id": "generate-variations",
         "title": "Generate Variations",
         "url": "https://experience.adobe.com/aem/generate-variations",
         "passConfig": true,
         "environments": ["preview","live", "edit"],
         "includePaths": ["**.docx**"]
       }
       // ...
     ]
   }
   ```

1. その後、ユーザーが [Edge Delivery Servicesを持つExperience Manageras a Cloud Serviceへのアクセス ](#access-to-aemaacs-with-edge-delivery-services) 権を持っていることを確認する必要が生じる場合があります。

1. その後、Sidekickのツールバーから「**バリエーションを生成**」を選択して、この機能にアクセスできます。

   ![ バリエーションの生成 – AEM Sidekicj からのアクセス ](assets/generate-variations-sidekick-toolbar.png)

## その他の情報 {#further-information}

詳しくは、次のリンクも参照してください。

* [GenAI が GitHub にバリエーションを生成 ](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Edge Delivery Services実験 ](https://www.aem.live/docs/experimentation)

## FAQ {#faqs}

### フォーマットされた出力 {#formatted-outpu}

**生成された応答では、必要な形式の出力は提供されません。 形式を変更するにはどうすればよいですか？ 例：タイトルとサブタイトルが必要ですが、応答はタイトルのみです**

1. 編集モードで実際のプロンプトを開きます。
1. 要件に移動します。
1. 出力について説明する要件があります。
   1. 例：「テキストは、タイトル、本文、ボタンラベルの 3 つの部分で構成する必要があります。」 または「属性「Title」、「Body」、「ButtonLabel」を持つオブジェクトの有効な JSON 配列として応答をフォーマットします。
1. 要件をニーズに合わせて変更します。

   >[!NOTE]
   >
   >入力する新しい出力に対して単語数/文字数の制限がある場合は、要件を作成します。

   例：「タイトルテキストは、スペースを含めて 10 単語または 50 文字を超えないようにする」
1. 今後の使用のためにプロンプトを保存します。

### 応答の長さ {#length-of-response}

**生成された応答が長すぎるか短すぎます。 長さを変更するにはどうすればよいですか？**

1. 編集モードで実際のプロンプトを開きます。
1. 要件に移動します。
1. 各出力に対して、対応する単語/文字の制限があります。
   1. 例：「タイトルテキストは、スペースを含めて 10 単語または 50 文字を超えないようにする」
1. 要件をニーズに合わせて変更します。
1. 今後の使用のためにプロンプトを保存します。

### 回答の改善 {#improve-responses}

**返される応答は、私が探しているものと正確には異なります。 改善するにはどうすればよいですか？**

1. 詳細設定で温度を変更してみてください。
   1. 温度が高いほど、プロンプトから逸脱し、より多くのバリエーション、ランダム性、創造性につながります。
   1. 温度が低いほど、より決定論的であり、プロンプトの内容に従います。
1. 編集モードで実際のプロンプトを開き、プロンプトを確認します。 声のトーンやその他の重要な基準を説明する要件の節に特に注意してください。

### プロンプトのコメント {#comments-in-prompt}

**プロンプトでコメントを使用するにはどうすればよいですか？**

プロンプト内のコメントは、実際の出力の一部ではないメモ、説明、または指示を含めるために使用されます。 これらのコメントは、特定の構文でカプセル化されます。コメントの先頭と末尾は二重中括弧で、先頭はハッシュ（`{{# Comment Here }}` など）です。 コメントは、生成される応答に影響を与えることなく、プロンプトの構造や意図を明確にするのに役立ちます。

### 共有プロンプトの検索 {#find-a-shared-prompt}

**共有されているプロンプトテンプレートが見つからない場合はどうすればよいですか？**

このような場合、確認すべき様々な詳細があります。

1. 環境の URL を使用します。
例：https://experience.adobe.com/#/aem/generate-variations
1. 選択した IMS 組織が正しいことを確認します。
1. プロンプトが共有として保存されたことを確認します。

### v2.0.0 のカスタムプロンプト {#custom-prompts-v200}

**v.2.0.0 では、カスタムプロンプトが表示されなくなりました。どうすればよいですか？**

v2.0.0 リリースに移行すると、カスタムプロンプトテンプレートが壊れ、使用できなくなります。

これらを取得するには：

1. Sharepoint の prompt-template フォルダーに移動します。
1. プロンプトをコピーします。
1. バリエーションを生成アプリケーションを開きます。
1. 新しいプロンプトカードを選択します。
1. プロンプトを貼り付けます。
1. プロンプトが機能することを確認します。
1. プロンプトを保存します。

## リリース履歴 {#release-history}

現在および以前のリリースについて詳しくは、[ バリエーションを生成するためのリリースノート ](/help/generative-ai/release-notes-generate-variations.md) を参照してください
