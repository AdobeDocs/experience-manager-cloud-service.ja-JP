---
title: AEM Forms Edge Delivery Servicesフォームコンポーネント
description: AEM Forms Edge Delivery Services は、ピークパフォーマンスを発揮するように作られており、ユーザーは合理化されたデータ収集とユーザーエンゲージメントの今後を思い描くことができます。この記事では、EDD フォームで初期状態で使用できるすべてのフォームコンポーネントを示します。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 9%

---




# フォームブロックEdge DeliveryでサポートされるHTMLコンポーネント

AEM Forms Edge Deliveryには、フォームブロックが 1 つ含まれています。 フォームブロックを使用すると、取り込んだデータを取得および保存するフォームを簡単に作成できます。

フォームブロックは、テキスト、メール、数値、日付など、OOTB HTML 5 のコンポーネントをサポートします。 また、テキスト領域、select 要素、fieldset 要素もサポートしており、HTML 5 にネイティブな入力検証機能が含まれています。 フォームブロックは、すべてのフィールドタイプとコンテナに対して均一なHTML構造を作成し、一貫性を確保します。 また、`form.css` ファイルを使用して [ フィールドタイプのスタイルを設定 ](https://adobe-rnd.github.io/form-block/customization/styling_form) することもできます。

## フォームブロックでサポートされるHTML5 入力タイプ

フォームブロックは、HTML 5 の入力タイプを幅広くサポートし、AEM コアコンポーネントを使用して作成されたフォームもシームレスにレンダリングします。

次の表に、コアコンポーネントがEdge DeliveryのHTML 5 入力タイプにどのように対応するかを示します。

<table>
 <tbody>
  <tr>
   <td><b>コアコンポーネント</b> </td>
   <td><b>HTML 5 の入力の種類 </b> </td>
   <td><b>詳細</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">フォームコンテナ</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">フォーム </td>
   <td> ユーザー入力を取得するフォームを作成します。
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">テキスト入力</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> 1 行テキスト入力フィールドを定義します。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">数値入力</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">数値</a></td>
   <td>ユーザーが数値を入力できます。 数値以外の入力を拒否する組み込み検証を追加することもできます。 ユーザーが数値を入力できます。 数値以外の入力を拒否する組み込み検証を追加することもできます。 最初は、入力フィールドが数値入力として表示されます。 表示パターンを適用すると、HTML 5 では表示パターンがサポートされていないので、作成者が数値の書式設定を適用できるようにテキストに変わります。 ただし、ユーザーがクリックすると、数字の入力に戻ります。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">日付選択</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> 日付入力用の入力フィールドを作成します。 エントリを検証するテキストボックスまたは専用の日付選択インターフェイスを使用して、日付を入力するオプションがあります。 最初は、ネイティブの日付入力フィールドが表示されます。 表示パターンを適用すると、HTML 5 は表示パターンをサポートしていないので、テキストに変わり、書式設定を適用できます。 ただし、ユーザーがクリックすると、日付の入力に戻ります。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">ファイル添付</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">ファイル</a></td>
   <td> ユーザーがデバイスの記憶域から 1 つ以上のファイルを選択できるようにします。 受け入れ可能なファイルタイプ、ファイルサイズ制限、最小/最大ファイル選択制限など、強化されたファイル入力検証をサポートします。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> ドロップダウンリスト</a></td>
   <td><a href ="https://developer.mozilla.org/ja-JP/docs/Web/HTML/Element/select">select</a></td>
   <td> 定義済みオプションのリストから 1 つ以上のオプションを選択できるようにします。 オプションのタイプは、文字列、数値またはブール値です。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">チェックボックスグループ</a></td>
   <td><a href ="https://developer.mozilla.org/ja-JP/docs/Web/HTML/Element/input/checkbox">複数チェックボックス</a></td>
   <td> ユーザーがリストから 1 つ以上のオプションを選択できるようにします。 複数のチェックボックスが同じ名前で生成され、それぞれが列挙内の項目に対応します。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">ラジオボタングループ</td>
   <td><a href ="https://developer.mozilla.org/ja-JP/docs/Web/HTML/Element/input/radio">多重無線</a></td>
   <td> ユーザーが関連オプションのグループから 1 つのオプションを選択できるようにします。 複数のラジオボタンが同じ名前で生成され、それぞれが列挙内の項目に対応します。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">ボタン</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>クリック時にアクションをトリガーできる UI 要素。 </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">パネル</a></td>
   <td><a href ="https://developer.mozilla.org/ja-JP/docs/Web/HTML/Element/fieldset">凡例を使用したフィールドセット</a></td>
   <td> フォーム内のセクションをグループ化します。この場合、ネストされた*legend*要素によってフォームのキャプションが追加されます。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=ja">ウィザード</a></td>
   <td><a href ="https://developer.mozilla.org/ja-JP/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>フォーム内の関連するセクションをグループ化します。 また、配置を制御し、上部または左側に配置するための表示オプションをサポートします。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">テキスト</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>p タグは段落を示します。 ビジュアルコンテンツでは、段落は空白行またはインデントされた最初の行で区切られたテキストの塊です</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">送信ボタン</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> ユーザーがクリック時にフォームをサーバーに送信できる UI 要素。 ユーザーが送信ルールをボタンに追加すると、送信ボタンとして機能します。 </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">リセットボタン</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>クリックするとフォームをリセットする UI 要素。 ユーザーがボタンにリセットルールを追加すると、リセットボタンとして機能します。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">メール入力</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> ユーザーがメールアドレスを入力および編集できるようにします。 ユーザーが複数の属性を追加する場合、メールアドレスのリストを追加または編集できます。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">電話入力</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>ユーザーが電話番号を入力および編集できるようにします。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">ヘッダー</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> ヘッダー</a></td>
   <td>これには紹介コンテンツが含まれ、通常は紹介用またはナビゲーション用の補助具のグループが含まれます。 フォームコンテナの外部でサポートされます。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">フッター</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">フッター</a></td>
   <td> 著作権データや関連ドキュメントへのリンクなどの情報が含まれます。 フォームコンテナの外部でサポートされます。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=ja">アコーディオン<a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> フォーム内に展開と折りたたみが可能なセクションを作成できるようにします。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=ja">水平タブ</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td>フォームの複数のセクションを別々のタブに整理し、水平に表示します。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">画像</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> ユーザーがフォームに画像を含めることができます。</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">タイトル</a></td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> フォームの上部に表示されるテキストを指します。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">スイッチ</td>
   <td><i>フォームブロックではまだサポートされていません</i></td>
   <td> 2 つの状態（機能、設定、機能の有効化または無効化など）を選択できる 2 つの状態トグル。</td>
  </tr>
 </tbody>
</table>


