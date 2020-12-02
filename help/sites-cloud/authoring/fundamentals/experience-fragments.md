---
title: エクスペリエンスフラグメント
description: Adobe Experience Manager as a Cloud Service のエクスペリエンスフラグメントを使用すると、エクスペリエンスの再利用性と柔軟性を高めることができます。
translation-type: tm+mt
source-git-commit: b7a2e86de27dbfcdecaf3a2bc1984678b7b69375
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 100%

---


# エクスペリエンスフラグメント {#experience-fragments}

Adobe Experience Manager as a Cloud Service 内では、エクスペリエンスフラグメントは、
* 1 つ以上のコンポーネントのグループです。
* コンテンツとレイアウトの両方を含んでいます。
* ページ内で参照可能です。
* 任意のコンポーネントを含めることができます。

エクスペリエンスフラグメントは、

* エクスペリエンス（ページ）の一部です。
* 複数ページで使用できます。
* テンプレートに基づいており（編集可能なもののみ）、構造とコンポーネントを定義します。
* 段落システムにレイアウトを含む 1 つ以上のコンポーネントで構成されています。
* 他のエクスペリエンスフラグメントを含めることができます。
* 他のコンポーネント（他のエクスペリエンスフラグメントを含む）と組み合わせて、完全なページ（エクスペリエンス）を作成できます。
* 複数のバリエーションを持つことができ、コンテンツやコンポーネントを共有できます。
* フラグメントの複数のバリエーションで使用できる構築ブロックに分類できます。

エクスペリエンスフラグメントを使用できるのは、次の場合です。

* 作成者がページの一部（エクスペリエンスのフラグメント）を再利用する場合。
エクスペリエンスフラグメントを使用しなければ、作成者はそのフラグメントをコピーして貼り付ける必要があります。これらのエクスペリエンスのコピー／貼り付けの作成と管理には時間がかかり、ユーザーエラーが発生しがちです。
エクスペリエンスフラグメントは、コピー／貼り付けを不要にします。
* ヘッドレス CMS の使用例をサポートする場合。
作成者は AEM をオーサリングにのみ使用し、顧客への配信には使用しないようにします。サードパーティシステム／タッチポイントは、そのエクスペリエンスを使用してエンドユーザーに配信します。

>[!NOTE]
>
>エクスペリエンスフラグメントの書き込みアクセス権には、次のグループに登録されたユーザーアカウントが必要です。
>
>* `experience-fragments-editors`
>
>
問題が発生している場合は、システム管理者にお問い合わせください。

## エクスペリエンスフラグメントを使用するタイミング    {#when-should-you-use-experience-fragments}

エクスペリエンスフラグメントは次の場合に使用します。

* エクスペリエンスを再利用する場合。
   * 同じコンテンツまたは似たコンテンツで再利用されるエクスペリエンス。
* サードパーティのためのコンテンツ配信プラットフォームとして AEM を使用する場合。
   * コンテンツ配信プラットフォームとして AEM を使用するソリューション。
   * サードパーティのタッチポイントへのコンテンツの埋め込み。
* 異なるバリエーションまたはレンディションを持つエクスペリエンスがある場合。
   * チャネルまたはコンテキスト固有のバリエーション。
   * グループに対応したエクスペリエンス（チャネル間でエクスペリエンスが異なるキャンペーンなど）。
* オムニチャネルコマースを使用する場合。
   * 規模に応じた[ソーシャルメディア](/help/implementing/developing/extending/experience-fragments.md#social-variations)チャネルでのコマース関連コンテンツの共有。
   * タッチポイントのトランザクション化。

## エクスペリエンスフラグメントの整理 {#organizing-your-experience-fragments}

以下をお勧めします。
* フォルダーを使用してエクスペリエンスフラグメントを整理する。

* [これらのフォルダーで使用可能なテンプレートを設定する](#configure-allowed-templates-folder)。

フォルダーを作成すると、次の操作をおこなうことができます。

* エクスペリエンスフラグメントにとって意味のある構造（例：分類に従った構造）を作成する。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントの構造をサイトのページ構造に合わせる必要はありません。

* [許可されたテンプレートをフォルダーレベルで割り当てる](#configure-allowed-templates-folder)。

   >[!NOTE]
   >
   >[テンプレートエディター](/help/sites-cloud/authoring/features/templates.md)を使用すると、独自のテンプレートを作成できます。

WKND プロジェクトでは、`Contributors` に従って一部のエクスペリエンスフラグメントを構造化します。また、使用される構造は、マルチサイト管理（言語コピーを含む）などの他の機能の使用方法の例も示します。

参照先：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![エクスペリエンスフラグメントのフォルダー](/help/sites-cloud/authoring/assets/xf-folders.png)

## エクスペリエンスフラグメントのフォルダーの作成と設定 {#creating-and-configuring-a-folder-for-your-experience-fragments}

エクスペリエンスフラグメントのフォルダーを作成および設定するには、次の操作をお勧めします。

1. [フォルダーを作成](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder)します。

1. [そのフォルダーに使用できるエクスペリエンスフラグメントテンプレートを設定](#configure-allowed-templates-folder)します。

>[!NOTE]
>
>また、[インスタンスに使用できるテンプレート](#configure-allowed-templates-instance)を設定することもできますが、アップグレード時に値が上書きされる可能性があるので、この方法は&#x200B;**お勧めしません**。

### フォルダーに使用できるテンプレートの設定 {#configure-allowed-templates-folder}

>[!NOTE]
>
>アップグレード時に値が上書きされないので、「**許可されたテンプレート**」を指定する場合は、この方法をお勧めします。

1. 必要な&#x200B;**エクスペリエンスフラグメント**&#x200B;フォルダーに移動します。

1. フォルダーを選択してから、「**プロパティ**」を選択します。

1. 必要なテンプレートを取得するための正規表現を「**許可されたテンプレート**」フィールドに指定します。

   例：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   参照先：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![エクスペリエンスフラグメントのプロパティ - 許可されたテンプレート](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >詳しくは、[エクスペリエンスフラグメントのテンプレート](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments)を参照してください。

1. 「**保存して閉じる**」を選択します。

### インスタンスに使用できるテンプレートの設定 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>指定したテンプレートがアップグレード時に上書きされる可能性があるので、「**許可されたテンプレート**」をこの方法で変更することはお勧めしません。
>
>このダイアログは、情報を提供する目的でのみ使用してください。

1. 必要な&#x200B;**エクスペリエンスフラグメント**&#x200B;コンソールに移動します。

1. 「**設定オプション**」を選択します。

   ![設定ボタン](/help/sites-cloud/authoring/assets/xf-18.png)

1. **エクスペリエンスフラグメントを設定**&#x200B;ダイアログで、必要なテンプレートを指定します。

   ![エクスペリエンスフラグメントを設定](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >詳しくは、[エクスペリエンスフラグメントのテンプレート](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments)を参照してください。

1. 「**保存**」を選択します。


## エクスペリエンスフラグメントの作成 {#creating-an-experience-fragment}

エクスペリエンスフラグメントを作成するには、次の手順に従います。

1. グローバルナビゲーションから「**エクスペリエンスフラグメント**」を選択します。

   ![ナビゲーションパネルのエクスペリエンスフラグメント](/help/sites-cloud/authoring/assets/xf-01.png)

1. 目的のフォルダーに移動し、「**作成**」をクリックします。

   ![エクスペリエンスフラグメントのフォルダーの作成](/help/sites-cloud/authoring/assets/xf-02.png)

1. 「**エクスペリエンスフラグメント**」を選択して、**エクスペリエンスフラグメントを作成**&#x200B;ウィザードを開きます。

   適切な&#x200B;**テンプレート**&#x200B;を選択して、「**次へ**」を選択します。

   ![エクスペリエンスフラグメントテンプレートの選択](/help/sites-cloud/authoring/assets/xf-03.png)


1. **エクスペリエンスフラグメント**&#x200B;の&#x200B;**プロパティ**&#x200B;を入力します。

   **タイトル**&#x200B;は必須です。**名前**&#x200B;が空欄のままの場合、**タイトル**&#x200B;から派生されます。

   ![エクスペリエンスフラグメントのプロパティ](/help/sites-cloud/authoring/assets/xf-04.png)

1. 「**作成**」をクリックします。

   メッセージが表示されます。以下から選択します。

   * 「**完了**」を選択すると、コンソールに戻ります。
   * 「**開く**」を選択すると、フラグメントエディターを開きます。

## エクスペリエンスフラグメントの編集 {#editing-your-experience-fragment}

エクスペリエンスフラグメントエディターには、通常のページエディターと似た機能があります。

>[!NOTE]
>
>ページエディターの使用方法について詳しくは、[ページのコンテンツの編集](/help/sites-cloud/authoring/fundamentals/editing-content.md)を参照してください。

次の手順の例では、商品のティーザーを作成する方法を示します。

1. 必要なコンポーネントを[コンポーネントブラウザー](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)からドラッグ＆ドロップします。

1. コンポーネントに応じて以下をおこないます。
   * コンテンツやアセットを必要に応じて追加します。
   * プロパティを必要に応じて設定します。

1. 必要に応じてその他のコンポーネントを追加します。

例：`http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![ページ上のエクスペリエンスフラグメント](/help/sites-cloud/authoring/assets/xf-05.png)

## エクスペリエンスフラグメントのバリエーションの作成 {#creating-an-experience-fragment-variation}

必要に応じて、エクスペリエンスフラグメントのバリエーションを作成できます。

1. [編集](#editing-your-experience-fragment)するフラグメントを開きます。
1. 「**バリエーション**」タブを開きます。

   ![エクスペリエンスフラグメントのバリエーションの作成](/help/sites-cloud/authoring/assets/xf-06.png)

1. 「**作成**」を使用すると、以下を作成できます。

   * **バリエーション**
   * **バリエーションをライブコピーとして**。

1. 必要なプロパティを定義します。

   * **テンプレート**
   * **タイトル**
   * **名前**（空欄のままの場合、タイトルから派生される）
   * **説明**
   * **バリエーションのタグ**

   次に例を示します。

   ![バリエーションのプロパティ](/help/sites-cloud/authoring/assets/xf-07.png)

1. 「**完了**」で確定すると、新しいバリエーションがパネルに表示されます。

## エクスペリエンスフラグメントの使用 {#using-your-experience-fragment}

ページをオーサリングする際に、エクスペリエンスフラグメントを使用できるようになりました。

1. 編集するページを開きます。

1. ページの段落システム内に、エクスペリエンスフラグメントコンポーネントのインスタンスを作成します。

1. 次のいずれかの方法で、実際のエクスペリエンスフラグメントをコンポーネントインスタンスに追加します。

   * アセットブラウザーから必要なフラグメントをドラッグして、コンポーネントにドロップします。
   * コンポーネントツールバーから&#x200B;**設定**&#x200B;を選択して、使用するフラグメントを指定し、「**完了**」で確定します。

   >[!NOTE]
   >
   >コンポーネントツールバーの「編集」は、フラグメントエディターでフラグメントを開くためのショートカットとして動作します。

例：`http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![ページエディター内のエクスペリエンスフラグメント](/help/sites-cloud/authoring/assets/xf-08.png)

## 構築ブロック {#building-blocks}

1 つ以上のコンポーネントを選択して、フラグメント内で再利用するための構築ブロックを作成できます。

### 構築ブロックの作成 {#creating-a-building-block}

新しい構築ブロックを作成するには、次の手順に従います。

1. エクスペリエンスフラグメントエディターで、再利用するコンポーネントを選択します。

   ![構築ブロック用コンポーネントの選択](/help/sites-cloud/authoring/assets/xf-09.png)

1. コンポーネントツールバーから、「**構築ブロックに変換**」を選択します。

   ![構築ブロックボタン](/help/sites-cloud/authoring/assets/xf-10.png)

1. **構築ブロック**&#x200B;の名前を入力して、「**変換**」で確定します。

   ![構築ブロック名の設定](/help/sites-cloud/authoring/assets/xf-11.png)

1. **構築ブロック**&#x200B;が左タブ（「**ローカル**」）に表示され、以降のアクションで選択できます。

   ![パネル内の構築ブロック](/help/sites-cloud/authoring/assets/xf-12.png)

#### 構築ブロックの管理 {#managing-a-building-block}

構築ブロックは、「**構築ブロック**」タブに表示されます。各ブロックでは、次の操作をおこなえます。

* ****&#x200B;マスターに移動（マスターバリエーションを新しいタブで開く）
* **名前を変更**
* **削除**

![構築ブロックの管理](/help/sites-cloud/authoring/assets/xf-13.png)

#### 構築ブロックの使用 {#using-a-building-block}

任意のコンポーネントと同様に、構築ブロックをフラグメントの段落システムにドラッグできます。

エクスペリエンスフラグメントを編集する際に、使用可能な構築ブロックが左側のタブに表示されます。次の条件でフィルタリングできます。

* **ローカル** - 現在のエクスペリエンスフラグメントの構築ブロック
* **すべて** - すべてのフラグメントの構築ブロック

![構築ブロックの選択](/help/sites-cloud/authoring/assets/xf-14.png)

## エクスペリエンスフラグメントの詳細 {#details-of-your-experience-fragment}

フラグメントの詳細は、以下のようにして確認できます。

1. エクスペリエンスフラグメントの場所に移動します（フラグメント内のバリエーションまで移動しないでください）。
詳細は、**エクスペリエンスフラグメント**&#x200B;コンソールのすべてのビューに表示されます。**リスト表示**&#x200B;には、Adobe Target への書き出しの詳細も含まれます。<!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![エクスペリエンスフラグメントの詳細](/help/sites-cloud/authoring/assets/xf-15.png)

1. エクスペリエンスフラグメントの&#x200B;**プロパティ**&#x200B;を開くと、

   ![「プロパティ」ボタン](/help/sites-cloud/authoring/assets/xf-16.png)

   プロパティが次のように様々なタブに表示されます。

   >[!CAUTION]
   >
   >これらのタブは、エクスペリエンスフラグメントコンソールから「**プロパティ**」を開くと表示されます。
   >
   >エクスペリエンスフラグメントの編集時に&#x200B;**プロパティを開く**&#x200B;と、適切な[ページのプロパティ](/help/sites-cloud/authoring/fundamentals/page-properties.md)が表示されます。

   ![エクスペリエンスフラグメントのプロパティ](/help/sites-cloud/authoring/assets/xf-17.png)

   * **基本**
      * **タイトル**（必須）
      * **説明**
      * **タグ**
      * **バリアントの合計数** - 情報提供のみ
      * **Web バリアントの数** - 情報提供のみ
      * **非 Web バリアントの数** - 情報提供のみ
      * **このフラグメントを使用するページの数** - 情報提供のみ
   * **Cloud Services**
      * **クラウド設定**
      * **クラウドサービス設定**
      * **Facebook ページ ID**
      * **Pinterest ボード**
   * **参照**
      * 参照のリスト
   * **ソーシャルメディアのステータス**
      * ソーシャルメディアバリエーションの詳細

## プレーン HTML レンディション {#the-plain-html-rendition}

URL の `.plain.` セレクターを使用すると、ブラウザーからプレーン HTML レンディションにアクセスできます。

>[!NOTE]
>
>ブラウザーから直接利用することもできますが、[主な目的は、他のアプリケーション（例えば、サードパーティ Web アプリ、カスタムモバイル実装など）が、URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition)

## エクスペリエンスフラグメントの書き出し  {#exporting-experience-fragments}

デフォルトでは、エクスペリエンスフラグメントは HTML 形式で配信され、AEM とサードパーティチャネルのどちらでも同じように使用できます。

Adobe Target への書き出しには、JSON も使用できます。詳しくは、Adobe Target とエクスペリエンスフラグメントの統合を参照してください。<!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
