---
title: AEM FormsEdge Delivery Servicesフォームコンポーネント
description: AEM FormsEdge Delivery Servicesは、効率的なデータ収集とユーザーエンゲージメントの将来を想像できるように、ピークパフォーマンスを実現するために構築されています。 この記事では、EDD フォームですぐに使用できるすべてのフォームコンポーネントの一覧を示します。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 5%

---




# フォームブロックエッジ配信でサポートされるHTMLコンポーネント

AEM Forms Edge Delivery には、フォームブロックが含まれます。 フォームブロックを使用すると、取り込んだデータを簡単に取り込んで保存するためのフォームを簡単に作成できます。

フォームブロックは、テキスト、電子メール、数値、日付など、OOTBHTML5 のコンポーネントをサポートしています。 また、テキスト領域、選択要素、フィールドセット要素もサポートし、HTML5 に固有の入力検証機能が含まれます。 フォームブロックは、すべてのフィールドタイプとHTMLの一貫性を確保するために、統一されたコンテナ構造を作成します。 また、 [フィールドタイプのスタイル設定](https://adobe-rnd.github.io/form-block/customization/styling_form) の使用 `form.css` ファイル。

## フォームブロックでサポートされるHTML5 の入力タイプ

フォームブロックは様々なHTML5 の入力タイプをサポートし、AEMコアコンポーネントを使用して作成されたフォームをシームレスにレンダリングできます。

次の表に、コアコンポーネントがエッジ配信のHTML5 の入力タイプに対応する方法を示します。

<table>
 <tbody>
  <tr>
   <td><b>コアコンポーネント</b> </td>
   <td><b>HTML5 の入力タイプ</b> </td>
   <td><b>詳細</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">フォームコンテナ</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">フォーム </td>
   <td> ユーザー入力を取り込むためのフォームを作成します。
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">テキスト入力</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> 1 行のテキスト入力フィールドを定義します。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">数値入力</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">数値</a></td>
   <td>ユーザーが数値を入力できるようにします。 また、組み込みの検証を追加して、数値以外の入力を拒否することもできます。 ユーザーが数値を入力できるようにします。 また、組み込みの検証を追加して、数値以外の入力を拒否することもできます。 最初は、入力フィールドが数値入力として表示されます。 HTML5 は表示パターンをサポートしていないので、ユーザーが表示パターンを適用すると、作成者が番号の書式を適用できるようにテキストに変更されます。 ただし、ユーザーがクリックすると、数値を入力する際に戻ります。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">日付選択</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> 日付を入力するための入力フィールドを作成します。 テキストボックスを使用して日付を入力するか、入力を検証するか、専用の日付選択インターフェイスを使用して日付を入力するかのどちらかを選択できます。 最初に、ネイティブな日付入力フィールドが表示されます。 HTML5 は表示パターンをサポートしていないので、表示パターンを適用すると、テキストに変更されて書式を適用できます。 ただし、ユーザーがクリックすると、日付の入力に戻ります。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">ファイル添付</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">ファイル</a></td>
   <td> ユーザーがデバイスストレージから 1 つ以上のファイルを選択できるようにします。 使用可能なファイルタイプ、ファイルサイズの制限、最小/最大ファイル選択制限など、拡張されたファイル入力検証をサポートします。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> ドロップダウンリスト</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> 定義済みオプションのリストから 1 つ以上のオプションを選択できます。 オプションのタイプは、文字列、数値またはブール値です。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">チェックボックスグループ</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">複数のチェックボックス</a></td>
   <td> ユーザーがリストから 1 つ以上のオプションを選択することを許可します。 同じ名前の複数のチェックボックスが生成され、それぞれが列挙内の項目に対応します。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">ラジオボタングループ</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">多重無線</a></td>
   <td> ユーザーが関連するオプションのグループから 1 つのオプションを選択できるようにします。 同じ名前のラジオボタンが複数生成され、それぞれが列挙内の項目に対応します。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">ボタン</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>ユーザーがクリックしたときにアクションをトリガーできる UI 要素。 </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">パネル</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">凡例付きフィールドセット</a></td>
   <td> フォーム内のセクションをグループ化します。ネストされた*凡例*要素によって、フォームのキャプションが追加されます。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja">ウィザード</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>フォーム内の関連セクションをグループ化します。 また、上または左側に配置するための表示オプションをサポートする、配置を制御します。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">テキスト</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>p タグは段落をマークします。 ビジュアルコンテンツでは、段落は、空白行またはインデントされた最初の行で区切られたテキストのチャンクです</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">送信ボタン</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> クリック時にユーザーがフォームをサーバーに送信できる UI 要素。 ユーザーがボタンに送信ルールを追加した場合、そのルールは送信ボタンとして機能します。 </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">リセットボタン</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>クリック時にフォームをリセットする UI 要素。 ユーザーがボタンにリセットルールを追加した場合、そのボタンはリセットボタンとして機能します。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">電子メール入力</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> ユーザーが電子メールアドレスを入力および編集できるようにします。 ユーザーが複数の属性を追加した場合は、E メールアドレスのリストを追加または編集できます。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">電話入力</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">電話番号</a></td>
   <td>ユーザーが電話番号を入力および編集できるようにします。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">ヘッダー</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> ヘッダー</a></td>
   <td>これには、紹介コンテンツ（通常、紹介ツールやナビゲーションツールのグループ）が含まれます。 フォームコンテナの外部でサポートされています。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">フッター</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">フッター</a></td>
   <td> 著作権データや関連ドキュメントへのリンクなどの情報が含まれます。 フォームコンテナの外部でサポートされています。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja">アコーディオン<a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> フォーム内に展開可能な折りたたみ可能なセクションを作成できます。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja">水平タブ</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td>フォームの複数のセクションを、水平方向に表示される個別のタブに編成します。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">画像</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> ユーザーがフォームに画像を含めることを許可します。</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">タイトル</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> フォームの上部に表示されるテキストを参照します。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">スイッチ</td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> 機能、設定、機能の有効化/無効化など、2 つの状態から選択できる 2 つの状態切り替え。</td>
  </tr>
 </tbody>
</table>


