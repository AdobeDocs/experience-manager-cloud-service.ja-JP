---
title: バリエーションを生成
description: バリエーションを生成する方法を説明します。Edge Delivery ServicesのSidekickからアクセスできます。
source-git-commit: 88d0b0a6dc2dacdf907ab46c804087772ab2e030
workflow-type: tm+mt
source-wordcount: '3338'
ht-degree: 1%

---


# バリエーションを生成 {#generate-variations}

デジタルチャネルを最適化し、コンテンツ作成を高速化する方法を探している場合は、「バリエーションを生成」を使用できます。 バリエーションの生成では、生成人工知能 (AI) を使用して、プロンプトに基づいてコンテンツのバリエーションを作成します。これらのプロンプトは、Adobeが提供するか、ユーザーが作成して管理します。 バリエーションを作成した後、Web サイト上でコンテンツを使用し、 [実験](https://www.aem.live/docs/experimentation) 機能 [Edge Delivery Services](/help/edge/overview.md).

以下が可能です。 [バリエーションの生成にアクセス](#access-generate-variations) 送信元：

<!-- 
* [within Adobe Experience Manager (AEM) as a Cloud Service](#access-aemaacs)
-->

* [AEMEdge Delivery ServicesのSidekick](#access-aem-sidekick)

これにより、以下のことが可能になります。

* [基本を学ぶ](#get-started) 特定の使用例に対してAdobeが作成したプロンプトテンプレートを使用する。
* 以下が可能です。 [既存のプロンプトを編集する](#edit-the-prompt)
* または [独自のプロンプトを作成して使用する](#create-prompt):
   * [プロンプトを保存します。](#save-prompt) 将来の使用のために
   * [共有プロンプトにアクセスして使用](#select-prompt) 組織全体から
* 次を定義： [audience](#audiences) 次の場合にプロンプトで使用するセグメント [パーソナライズしたオーディエンス固有のコンテンツの生成](#generate-copy).
* プロンプトと共に出力をプレビューし、必要に応じて修正を加え、結果を調整します。
* 用途 [Adobe Expressで画像を生成](#generate-image) コピーのバリエーションに基づく。これはFireflyの生成 AI 機能を使用します。
* Web サイトまたは実験で使用するコンテンツを選択します。

## 法的事項と使用上の注意 {#legal-usage-note}

AEMの生成 AI と生成バリエーションは強力なツールです。 **あなた** は、出力の使用を担当します。

サービスへの入力は、コンテキストに関連付ける必要があります。 このコンテキストは、ブランディング資料、Web サイトコンテンツ、データ、そのようなデータ、テンプレート、または他の信頼できるドキュメントのスキーマにすることができます。

出力の精度は、使用事例に応じて評価する必要があります。

バリエーションを生成を使用する前に、 [Adobe生成 AI のユーザーガイドライン](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

[バリエーションの生成の使用](#generative-action-usage) 生成的な行動の消費に結び付いている

## 概要 {#overview}

「バリエーションを生成」を開く（および左側のパネルを展開する）と、次のように表示されます。

![バリエーションを生成 — メインパネル](assets/generate-variations-main-panel.png)

* 右パネル
   * これは、左側のナビゲーションでの選択に応じて異なります。
   * デフォルトでは、 **プロンプトテンプレート** が表示されます。
* 左ナビゲーション
   * の左側 **バリエーションを生成**&#x200B;の場合は、左側のナビゲーションパネルを展開または非表示にするオプション（サンドイッチメニュー）があります。
   * **プロンプトテンプレート**:
      * 各種プロンプトへのリンクを表示します。これらには、次のプロンプトが含まれます。
         * コンテンツの生成に役立つAdobeが提供します。Adobeアイコンでフラグ付けされます。
         * 自分で作成した。
         * IMS 組織内で作成し、複数の見出しを示すアイコンでフラグ付けします。
      * 次を含む： [新しいプロンプト](#create-prompt) 独自のプロンプトを作成するためのリンク。
      * 以下が可能です。 **削除** 自分で、または IMS 組織内で作成されたプロンプト。 これは、該当するカードの楕円でアクセスするメニューを使用して行います。
   * [お気に入力](#favorites)：お気に入りにフラグを設定した前の世代の結果を表示します。
   * [最近](#recents)：最近使用したプロンプトへのリンクと入力を表示します。
   * **ヘルプと FAQ**:FAQ を含むドキュメントへのリンクです。
   * **ユーザーガイドライン**：法的ガイドラインへのリンクです。

## はじめに {#get-started}

このインターフェイスでは、コンテンツの生成プロセスをガイドします。 インタフェースを開いた後、最初の手順は、使用するプロンプトを選択することです。

### プロンプトを選択 {#select-prompt}

メインパネルから、次の項目を選択できます。

* コンテンツの生成を開始するためのAdobeが提供するプロンプトテンプレート
* の [新しいプロンプト](#create-prompt) 独自のプロンプトを作成するには、以下を実行します。
* 作成したテンプレートは、使用のためにのみ使用します。
* 自分または組織内の任意のユーザーが作成したテンプレート。

区別する手順は次のとおりです。

* Adobeが提供するプロンプトには、Adobeアイコンでフラグが付きます
* IMS 組織全体で使用可能なプロンプトには、複数の見出しアイコンでフラグが付けられます。
* プライベートプロンプトには、特別なフラグは設定されません。

![バリエーションを生成 — プロンプトテンプレート](assets/generate-variations-prompt-templates.png)

### 入力を入力 {#provide-inputs}

生成 AI から適切なコンテンツを取り戻すために、各プロンプトで特定の情報を提供する必要があります。

入力フィールドを使用して、必要な情報を入力できます。 必要に応じて、特定のフィールドにはデフォルト値を使用または変更でき、また、要件を説明する説明が含まれています。

複数のプロンプトに共通するいくつかのキー入力フィールドがあります（特定のフィールドが常に使用可能とは限りません）。

* **の数**/**数**
   * 1 世代で作成するコンテンツのバリエーション数を選択できます。
   * プロンプトに応じて、「カウント」、「バリエーション数」、「アイデア数」など、様々なラベルの中から 1 つを選択できます。
* **Audience Source**/**ターゲットオーディエンス**
   * 特定のオーディエンス向けにパーソナライズされたコンテンツを生成するのに役立ちます。
   * Adobeは、デフォルトのオーディエンスを提供します。または、追加のオーディエンスを指定できます。詳しくは、 [オーディエンス](#audiences).
* **追加のコンテキスト**
   * 適切なコンテンツを挿入して、入力に基づいてより良い応答を生成する Generative AI を支援します。 例えば、特定のページや製品の Web バナーを作成する場合は、そのページや製品に関する情報を含めることができます。
* **温度**
Adobe生成 AI の温度を変更するために使用：
   * 温度が高いと、プロンプトから遠ざかり、より多くの変化、ランダム性、創造性につながります。
   * 温度が低いほど、より決定論的で、プロンプト内の値に近づきます。
   * デフォルトでは、温度は 1 に設定されています。 生成された結果が好みに合わない場合は、異なる温度を試すことができます。
* **プロンプトを編集**
   * 基になる [プロンプトを編集可能](#edit-the-prompt) をクリックして、生成された結果を絞り込みます。

### コピーを生成 {#generate-copy}

入力フィールドに入力し、プロンプトを変更した後、コンテンツを生成して回答を確認する準備が整いました。

選択 **生成** 生成 AI によって生成された応答を見る。 生成されたコンテンツのバリエーションが、生成されたプロンプトの下に表示されます。

![バリエーションを生成 — コピーを生成します](assets/generate-variations-generate-content.png)

>[!NOTE]
>
>ほとんどのAdobeプロンプトテンプレートには、 **AI の根拠** （バリエーション応答）。 これにより、生成 AI がその特定のバリエーションを生成した理由に関する透明性が得られます。

単一のバリエーションを選択した場合、次のアクションを使用できます。

* **お気に入り**
   * Flag as a **お気に入り** 将来の使用のため ( [お気に入力](#favorites)) をクリックします。
* 上親指/下親指
   * 親指を上/下の指標を使用して、回答の質をAdobeに通知します。
* **コピー**
   * をクリップボードにコピーして、Web サイト上のコンテンツをオーサリングする際、または [実験](https://www.aem.live/docs/experimentation).
* **削除**

入力またはプロンプトを調整する必要がある場合は、調整を行い、 **生成** 新しい応答を取得する場合は、再度お試しください。 新しいプロンプトと応答が最初のプロンプトと応答の下に表示されます。上下にスクロールして、様々なコンテンツのセットを表示できます。

各バリエーションの上に、作成したプロンプトと **再利用** オプション。 入力情報を含むプロンプトを再実行する必要がある場合は、 **再利用** 再読み込みする **入力**.

### 画像を生成 {#generate-image}

テキストのバリエーションを生成した後、Fireflyの生成 AI 機能を使用して、Adobe Expressで画像を生成できます。

>[!NOTE]
>
>**画像を生成** は、IMS 組織の一部としてのAdobe Express権限を持ち、その組織でのアクセス権限が付与されている場合にのみ使用できます。

バリエーションを選択し、その後に **画像を生成**、直接開く **テキストから画像へ** in [Adobe Express](https://www.adobe.com/express/). プロンプトは、バリアントの選択に基づいて事前に入力され、そのプロンプトに従って画像が自動的に生成されます。

![バリエーションを生成 — 簡易画像](assets/generate-variations-express-images.png)

さらに変更を加えることができます。

* [自分のプロンプトをAdobe Expressで書く](https://helpx.adobe.com/firefly/using/tips-and-tricks.html) 何を見たいか説明して
* 調整する **テキストから画像へ** オプション，
* その後 **更新** 生成された画像。

また、 **詳細情報** を参照してください。

完了したら、目的の画像を選択し、 **保存** をクリックしてAdobe Expressを閉じます。 画像が返され、バリエーションと共に保存されます。

![バリエーションを生成 — 画像を高速で保存](assets/generate-variations-express-image-saved.png)

ここで、画像の上にマウスを移動してアクション項目を表示できます。

* **コピー**: [他の場所で使用するために、画像をクリップボードにコピーします。](#use-content)
* **編集**:Adobe Expressを開き、画像を変更できるようにします。
* **ダウンロード**：ローカルマシンに画像をダウンロードします。
* **削除**：バリエーションから画像を削除します

>[!NOTE]
>
>[Content credentials](https://helpx.adobe.com/creative-cloud/help/content-credentials.html) は、ドキュメントベースのオーサリングで使用した場合、保持されません。

### コンテンツを使用 {#use-content}

生成 AI で生成されたコンテンツを使用するには、他の場所で使用するために、コンテンツをクリップボードにコピーする必要があります。

それには、コピーアイコンを使用します。

* テキストの場合：バリエーションパネルに表示されるコピーアイコンを使用します。
* 画像の場合：画像の上にマウスを移動すると、コピーアイコンが表示されます。

クリップボードにコピーしたら、その情報を貼り付けて、Web サイトのコンテンツをオーサリングする際に使用できます。 また、 [実験](https://www.aem.live/docs/experimentation).

## お気に入り {#favorites}

コンテンツを確認した後、選択したバリエーションをお気に入りとして保存できます。

保存すると、それらはに表示されます。 **お気に入力** をクリックします。 お気に入りは ( **削除** ブラウザーのキャッシュをクリアします )。

* お気に入りとバリエーションをクリップボードにコピー/貼り付けて、Web サイトのコンテンツで使用できます。
* お気に入りは、 **削除済み**.

## 最近使用したもの {#recents}

このセクションには、最近のアクティビティへのリンクが表示されます。 A **最近** エントリは **生成**. プロンプトの名前とタイムスタンプが含まれます。 リンクを選択すると、プロンプトが読み込まれ、必要に応じて入力フィールドに入力され、生成されたバリエーションが表示されます。

## プロンプトの編集 {#edit-the-prompt}

基になるプロンプトを編集できます。 次の操作を実行できます。

* 生成された結果がさらに絞り込みが必要な場合
* を変更し、 [プロンプトを保存します。](#save-prompt) 将来の使用のために

選択 **プロンプトを編集**:

![バリエーションを生成 — 編集プロンプト](assets/generate-variations-prompt-edit.png)

プロンプトエディタが開き、次の変更を行うことができます。

![バリエーションを生成 — プロンプトエディタ](assets/generate-variations-prompt-editor.png)

### プロンプト入力を追加 {#add-prompt-inputs}

プロンプトを作成または編集する際に、入力フィールドを追加する必要がある場合があります。 入力フィールドは、プロンプト内の変数として機能し、様々な状況で、同じプロンプトを柔軟に使用できます。 ユーザーは、プロンプト全体を書き込む必要なく、プロンプトの特定の要素を定義できます。

* フィールドは二重中括弧で囲んで定義します `{{ }}` プレースホルダー名を含む
例えば、`{{tone_of_voice}}` のように指定します。

  >[!NOTE]
  >
  >二重中括弧の間にはスペースを入れることはできません。

* また、次の場所でも定義されます。 `METADATA`を次のパラメーターと共に使用します。
   * `label`
   * `description`
   * `default`
   * `type`

#### 例：新しいテキストフィールドの追加 — 音声のトーン {#example-add-new-text-field-tone-of-voice}

「 」というタイトルの新しいテキストフィールドを追加するには **声のトーン**&#x200B;を使用する場合は、プロンプトで次の構文を使用します。

```prompt
{{@tone_of_voice, 
  label="Tone of voice",
  description="Indicate the desired tone of voice",
  default="optimistic, smart, engaging, human, and creative",
  type=text
}}
```

![バリエーションを生成 — 音声のトーンで編集するプロンプト](assets/generate-variations-prompt-edited.png)

#### 例：新しいドロップダウンフィールドの追加 — ページタイプ {#example-add-new-dropdown-field-page-type}

ドロップダウン選択を提供する入力フィールド「ページタイプ」を作成するには：

1. という名前のスプレッドシートを作成します。 `pagetype.xls` （フォルダー構造の最上位ディレクトリ）を参照します。
1. スプレッドシートを編集します。

   1. 2 つの列を作成します。 **キー** および **値**.
   1. Adobe Analytics の **キー** 列に、ドロップダウンに表示するラベルを入力します。
   1. Adobe Analytics の **値** 列には、生成 AI がコンテキストを持つキー値を記述します。

1. プロンプトで、スプレッドシートのタイトルと適切なタイプを参照します。

   ```prompt
   {{@page_type, 
     label="Page Type",
     description="Describes the type of page",
     spreadsheet=pagetype
   }}
   ```

## プロンプトを作成する {#create-prompt}

次を選択した場合： **新しいプロンプト** から **プロンプトテンプレート**&#x200B;を使用すると、新しいパネルで新しいプロンプトを入力できます。 これらを、 **温度**、宛先 **生成** コンテンツ。

詳しくは、 [プロンプトを保存](#save-prompt) を参照してください。

詳しくは、 [プロンプト入力を追加](#add-prompt-inputs) に、独自のプロンプト入力を追加する方法を示します。

UI での書式設定を保持し、文書ベースのオーサリングフローにコピー&amp;ペーストする場合は、プロンプトに次のように入力します。

<!-- CHECK - are the double-quotes needed? -->

* `"Format the response as an array of valid, iterable RFC8259 compliant JSON"`

次の画像に、この方法の利点を示します。

* 最初の例では、 `Title` および `Description` 組み合わせ
* 2 番目の例では、それぞれ別々に書式設定されます。これは、プロンプトに JSON リクエストを含めることでおこなわれます。

![バリエーションを生成 — プロンプトにタイトルと説明が別々に書式設定されています](assets/generate-variations-prompt-formatted.png)

## プロンプトを保存 {#save-prompt}

プロンプトを編集または作成した後、後で使用するために、IMS 組織または自分だけで保存する必要がある場合があります。 保存されたプロンプトは、 **テンプレートを確認** カード。

プロンプトを編集すると、 **保存** オプションは、「入力」セクションの下部、「 **生成**.

選択すると、 **プロンプトを保存** ダイアログが開きます。

![バリエーションを生成 — 保存プロンプト用のダイアログ](assets/generate-variations-prompt-save-dialog.png)

1. 一意の **プロンプト名**；内でプロンプトを識別するために使用します。 **プロンプトテンプレート**.
   1. 新しい一意の名前で、新しいプロンプトテンプレートが作成されます。
   1. 既存の名前でプロンプトが上書きされ、メッセージが表示されます。
1. オプションで説明を追加します。
1. オプションを有効または無効にする **組織全体で共有**&#x200B;を使用するかどうかを指定します。 このステータスは、 [プロンプトテンプレートに表示される結果カード](#select-prompt).
1. **保存** 速度、または **キャンセル** アクション。

>[!NOTE]
>
>既存のプロンプトを上書き/更新すると、通知（警告）が表示されます。

>[!NOTE]
>
>送信者 **プロンプトテンプレート** 自分で作成したプロンプト（楕円でアクセスするメニューを使用）や、IMS 組織内で作成したプロンプトを削除できます。

## 対象読者 {#audiences}

パーソナライズされたコンテンツを生成するには、生成 AI はオーディエンスを理解している必要があります。 Adobeは、多くのデフォルトオーディエンスを提供します。また、独自のオーディエンスを追加することもできます。

オーディエンスを追加する場合、オーディエンスを自然言語で説明する必要があります。 次に例を示します。

* オーディエンスを作成するには：
   * `Student`
* 次のように言うかもしれません。
   * `The audience consists of students, typically individuals who are pursuing education at various academic levels, such as primary, secondary, or tertiary education. They are engaged in learning and acquiring knowledge in diverse subjects, seeking academic growth, and preparing for future careers or personal development.`

2 つのオーディエンスソースがサポートされます。

* [Adobe Target](#audience-adobe-target)
* [CSV ファイル](#audience-csv-file)

![バリエーションの生成 — オーディエンスソース](assets/generate-variations-audiences.png)

### 対象者 — Adobe Target {#audience-adobe-target}

選択 **Adobe Target** オーディエンスを使用すると、そのオーディエンスに合わせてパーソナライズするコンテンツを生成できます。

>[!NOTE]
>
>このオプションを使用するには、IMS 組織がAdobe Targetにアクセスできる必要があります。

1. 「**Adobe Target**」を選択します。
1. 次に、必要な **ターゲットオーディエンス**&#x200B;を指定します。

   >[!NOTE]
   >
   >を使用するには **Adobe Target** オーディエンスの説明フィールドに入力する必要があります。 そうでない場合、オーディエンスはドロップダウンリストに使用不可と表示されます。 説明を追加するには、 Target に移動し、 [オーディエンスの説明を追加](https://experienceleague.adobe.com/docs/target-learn/tutorials/audiences/create-audiences).

   ![バリエーションを生成 — オーディエンスソース — Adobe Target](assets/generate-variations-audiences-adobe-target.png)

#### Adobe Target Audience を追加 {#add-adobe-target-audience}

詳しくは、 [オーディエンスの作成](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences) をクリックして、Adobe Targetでオーディエンスを作成します。

### オーディエンス — CSV ファイル {#audience-csv-file}

の選択 **CSV ファイル** オーディエンスを指定すると、選択した **ターゲットオーディエンス**.

Adobeは、使用する多数のオーディエンスを提供します。

1. 選択 **CSV ファイル**.
1. 次に、必要な **ターゲットオーディエンス**&#x200B;を指定します。

   ![バリエーションの生成 — オーディエンスソース — CSV ファイル](assets/generate-variations-audiences-csv-file.png)

#### オーディエンス CSV ファイルを追加 {#add-audience-csv-file}

CSV ファイルを様々なプラットフォーム (Google Drive、Dropbox、SharePoint など ) から追加できます。この CSV ファイルは、公開されたファイルの URL を提供できます。

>[!NOTE]
>
>共有プラットフォームでは、 *必須* は、ファイルを公開してアクセスできるようにする機能を持っています。

例えば、Google Drive 上のファイルからオーディエンスを追加するには、次のようにします。

1. Google Drive で、2 列のスプレッドシートファイルを作成します。
   1. 最初の列がドロップダウンに表示されます。
   1. 2 番目の列は、オーディエンスの説明です。
1. ファイルを公開します。
   1. ファイル/共有/Web に公開/CSV
1. URL を公開済みのファイルにコピーします。
1. 「バリエーションを生成」に移動します。
1. プロンプトエディタを開きます。
1. 検索文字列 **Adobe Target** オーディエンスをメタデータに含め、URL を置き換えます。

   >[!NOTE]
   >
   >URL の両端に二重引用符 (&quot;) を必ず付けてください。

   次に例を示します。

   ![バリエーションを生成 — オーディエンス CSV ファイルを追加](assets/generate-variations-audiences-csv-save.png)

## FAQ {#faqs}

### 形式設定された出力 {#formatted-outpu}

**生成された応答は、必要な形式の出力を提供しません。 形式を変更する方法を教えてください。 例：タイトルとサブタイトルが必要ですが、応答はタイトルに過ぎません**

1. 実際のプロンプトを編集モードで開きます。
1. 要件に移動します。
1. 出力に関する要件が表示されます。
   1. 例：「テキストは、タイトル、本文、ボタンラベルの 3 つの部分で構成する必要があります。」 または、「属性&quot;Title&quot;、&quot;Body&quot;、&quot;ButtonLabel&quot;を持つオブジェクトの有効な JSON 配列として応答をフォーマットします。
1. 必要に応じて要件を変更します。

   >[!NOTE]
   >
   >入力した新しい出力に対して単語数/文字数の制限がある場合は、要件を作成します。

   例：「タイトルテキストは、スペースを含め、10 語または 50 文字以下にする必要があります。」
1. 後で使用するためにプロンプトを保存します。

### 応答の長さ {#length-of-response}

**生成された応答が長すぎるか、短すぎます。 長さを変更する方法を教えてください。**

1. 実際のプロンプトを編集モードで開きます。
1. 要件に移動します。
1. 各出力に対して、対応する単語/文字の制限があることがわかります。
   1. 例：「タイトルテキストは、スペースを含め、10 語または 50 文字以下にする必要があります。」
1. 必要に応じて要件を変更します。
1. 後で使用するためにプロンプトを保存します。

### 回答を改善する {#improve-responses}

**私が得ている応答は、私が探しているものとは全く違う。 改善に役立つことを教えてください。**

1. 「詳細設定」で「温度」を変更してみてください。
   1. 温度が高いと、プロンプトから遠ざかり、より多くの変化、ランダム性、創造性につながります。
   1. 温度が低いほど、より決定論的で、プロンプト内の内容に従います。
1. 実際のプロンプトを編集モードで開き、確認プロンプトを表示します。 声の音色やその他の重要な基準について、要件の節に特に注意してください。

### プロンプト内のコメント {#comments-in-prompt}

**プロンプトでコメントを使用するにはどうすればよいですか？**

プロンプト内のコメントは、実際の出力に含まれない注記、説明、または指示を含めるために使用されます。 これらのコメントは特定の構文内にカプセル化されます。先頭と末尾は二重中括弧で囲み、ハッシュで始まります ( 例： `{{# Comment Here }}`) をクリックします。 コメントは、生成された応答に影響を与えることなく、プロンプトの構造や目的を明確にするのに役立ちます。

### 共有プロンプトを検索する {#find-a-shared-prompt}

**他のユーザーが共有したプロンプトテンプレートが見つからない場合は、どうすればよいですか？**

この場合は、次のように様々な詳細を確認する必要があります。

1. 環境の URL を使用します。
例： https://experience.adobe.com/#/aem/generate-variations
1. 選択した IMS 組織が正しいことを確認します。
1. プロンプトが「共有」として保存されたことを確認します。

### v2.0.0 のカスタムプロンプト {#custom-prompts-v200}

**v.2.0.0 では、カスタムプロンプトが表示されなくなりました。何ができますか。**

v2.0.0 リリースに移行すると、カスタムプロンプトテンプレートが壊れ、使用できなくなります。

詳しくは、 [v2.0.0 のリリースノート（取得方法の説明）](#release-notes-2-0-0-retrieve-prompt-templates).

## 生成作用の使用 {#generative-action-usage}

使用状況の管理は、実行されるアクションによって異なります。

* バリエーションを生成

  1 つのコピー変種の 1 つの世代は、1 つの生成動作と同じです。 お客様は、AEMライセンスに付属する一定数の生成アクションを持っています。 基本権限が消費されると、追加のアクションを購入できます。

  >[!NOTE]
  >
  >詳しくは、 [ADOBE EXPERIENCE MANAGER:CLOUD SERVICE | 製品の説明](https://helpx.adobe.com/legal/product-descriptions/aem-cloud-service.html) 基本的な使用権限の詳細については、を参照し、より生成的なアクションを購入したい場合は、アカウントチームにお問い合わせください。

* Adobe Express

  画像生成の使用は、Adobe Expressの使用権限と [生成単位](https://helpx.adobe.com/firefly/using/generative-credits-faq.html).

## バリエーションの生成にアクセス {#access-generate-variations}

<!--
### Access from AEM as a Cloud Service {#access-aemaacs}

Generate Variations can be accessed from the [Navigation Panel](/help/sites-cloud/authoring/basic-handling.md#navigation-panel) of AEM as a Cloud Service:

![Navigation panel](/help/sites-cloud/authoring/assets/basic-handling-navigation.png)
-->

### AEM Sidekickからのアクセス {#access-aem-sidekick}

一部の設定は、(Edge Delivery Servicesの )Sidekickから「バリエーションを生成」にアクセスする前に必要です。

1. ドキュメントを見る [インストールAEM Sidekick](https://www.aem.live/docs/sidekick-extension) を参照してください。

1. (Edge Delivery Servicesの )Sidekickの「バリエーションを生成」を使用するには、以下のEdge Delivery Servicesプロジェクトに次の設定を含めます。

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

1. 次に、ユーザーが [Edge Delivery Servicesでas a Cloud ServiceしたExperience Managerへのアクセス](#access-to-aemaacs-with-edge-delivery-services).

1. その後、「 」を選択して、この機能にアクセスできます。 **バリエーションを生成** Sidekickのツールバーから：

   ![バリエーションを生成 — AEM Sidekicj からアクセス](assets/generate-variations-sidekick-toolbar.png)

## Edge Delivery Servicesでas a Cloud ServiceしたExperience Managerへのアクセス{#access-to-aemaacs-with-edge-delivery-services}

「バリエーションの生成」へのアクセス権を持つユーザーは、Edge Delivery Servicesを持つExperience Manageras a Cloud Service環境に権利を持つ必要があります。

>[!NOTE]
>
>AEM Sitesas a Cloud Serviceの契約にEdge Delivery Servicesが含まれていない場合は、新しい契約に署名してアクセス権を取得する必要があります。
>
>Edge Delivery Servicesと共にAEM Sitesに移行する方法については、アカウントチームにお問い合わせください。

特定のユーザーにアクセス権を付与するには、ユーザーアカウントを各製品プロファイルに割り当てます。 詳しくは、 [詳細は、AEM製品プロファイルの割り当てを参照してください](/help/journey-onboarding/assign-profiles-cloud-manager.md).

## 参考情報 {#further-reading}

参照：

* [GenAI GitHub でバリエーションを生成](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Edge Delivery Services実験](https://www.aem.live/docs/experimentation)

## リリースノート {#release-notes}

### 2.0.0  {#release-notes-2-0-0}

* プロンプトテンプレート用のユニバーサル永続ストレージを導入しました。
* オーディエンスの新機能
   * オーディエンスはAdobe Targetから直接読み取ることができます
   * CSV ファイルの追加方法を更新しました
* 保存プロンプトのオプションを含むダイアログ
* 画像を生成する際に、Adobe Expressのプロンプトが事前に入力されます
* プロンプトカード（ホームページ上）に追加情報が表示され、削除できます

#### 2.0.0 — カスタムプロンプトテンプレートの取得方法 {#release-notes-2-0-0-retrieve-prompt-templates}

v2.0.0 リリースに移行すると、カスタムプロンプトテンプレートが壊れ、使用できなくなります。 取得する手順は、次のとおりです。

1. SharePoint の prompt-template フォルダに移動します。
1. プロンプトをコピーします。
1. バリエーションを生成アプリケーションを開きます。
1. [ 新しいプロンプト ] カードを選択します。
1. プロンプトを貼り付けます。
1. プロンプトが機能することを確認します。
1. プロンプトを保存します。

### 1.0.5 {#release-notes-1-0-5}

* Adobe Expressとの統合
* 編集プロンプトをサイドレールに移動

### 1.0.4 {#release-notes-1-0-4}

* 内部機能の強化

### 1.0.3 {#release-notes-1-0-3}

* 左側のナビゲーションパネルを展開または非表示にします
* 小規模な改善点

### 1.0.0 ～ 1.0.2 {#release-notes-1-0-0-1-0-2}

* 内部機能の強化