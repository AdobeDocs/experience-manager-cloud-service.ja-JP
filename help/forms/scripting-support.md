---
title: HTML5 フォームのスクリプティングのサポート
description: JavaScript と FormCalc プロパティ、および HTML5 フォームでサポートされているその他のメソッド。
contentOwner: robhagat
content-type: reference
topic-tags: hTML5_forms
feature: HTML5 Forms,Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '3916'
ht-degree: 100%

---

# HTML5 フォームのスクリプティングのサポート {#scripting-support-for-html-forms}

以下は、JavaScript と FormCalc プロパティ、および HTML5 フォームでサポートされているメソッドの一覧です。

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>プロパティ </th>
   <th>説明<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>ユーザーの操作に応じて変更される前のフィールドのコンテンツを指定します。この値は、元に戻す機能と同様にもう一度呼び出すことができます。</td>
   <td><p>ドロップダウンとリストボックスでは機能しません。次の場合、<code>PrevText </code> は正常に機能しません。</p>
    <ul>
     <li>iPad の数値フィールド上で一部の特殊文字キー（$、,、&amp;、@ など）を入力する場合、および </li>
     <li>日付フィールド（カレンダーを使用して日付を入力する場合）。<br /> </li>
    </ul> <p>スクリプトによる値の設定はサポートされていません。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>イベントの動作対象のオブジェクトを指定します。</td>
   <td>スクリプトによる値の設定はサポートされていません。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>ユーザーの操作に応じて変更された後のフィールドのコンテンツを指定します。</td>
   <td><p><code>newText</code> プロパティは、次の場合は正しく機能しません。</p>
    <ul>
     <li>テキストの選択と置換を行う場合</li>
     <li>テキストの削除、コピー、ペーストを行う場合。</li>
     <li>数値フィールド上で一部の特殊文字キー（$、,、&amp;、@ など）を入力する場合<br /> </li>
     <li>Shift キーと英数字キーを組み合わせて使用する場合。 </li>
     <li>日付／時間フィールドを使用したとき。</li>
    </ul>
    <div>
      スクリプトによる値の設定はサポートされていません。
    </div> </td>
  </tr>
  <tr>
   <td>change</td>
   <td>ユーザーが操作を実行した直後にフィールドに入力またはペーストした値を指定します。 </td>
   <td><p>change プロパティは、次の場合は正しく機能しません。</p>
    <ul>
     <li>テキストの選択と置換を行う場合</li>
     <li>テキストの削除、コピー、ペーストを行う場合。</li>
     <li>数値フィールド上で一部の特殊文字キー（$、,、&amp;、@ など）を入力する場合<br /> </li>
     <li>Shift キーと英数字キーを組み合わせて使用する場合。 </li>
     <li>日付／時間フィールドを使用したとき。</li>
    </ul> <p>スクリプトによる値の設定はサポートされていません。</p> </td>
  </tr>
  <tr>
   <td>keydown</td>
   <td>ユーザーが選択のために矢印キーを押しているかどうかを判定します。このプロパティは、リストボックスとドロップダウンリストでのみ使用できます。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>modifier</td>
   <td>特定のイベントの実行時に修飾キー（Microsoft® Windows® の Ctrl キーなど）が押されているかどうかを判定します。</td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>ホストのアプリケーションタイプを返します。クライアントアプリケーションのみで使用できます。</td>
   <td><code>HTML 5</code> を返します。</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>現在のアプリケーションの名前を返します。</td>
   <td>ブラウザー名とそのバージョンを返します。たとえば、Chrome ブラウザーでは、返される値は次の通りです。 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>ドキュメントのページ数を返します。</td>
   <td>HTML5 フォームのページネーションポリシーは、PDF forms のページネーションポリシーと同じではありません。したがって、numPages API は両方のケースにおいて異なる値を返すことがあります。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>スクリプトを実行しているコンピューターのプラットフォームを表す文字列を返します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>ドキュメントのタイトルを指定します。クライアントアプリケーションでのみ使用できます。</td>
   <td>PDF forms の場合のようにフォームのメタデータタイトルを返すのではなく、フォームの HTML ドキュメントのタイトルを返します。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>現在のアプリケーションのバージョン番号を表す文字列を返します。</td>
   <td>フォームのバージョンを返します。</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>計算スクリプトを実行するかどうかを指定します。<br /> </td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>検証スクリプトを実行するかどうかを指定します。<br /> </td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>前のページに移動します。</td>
   <td>HTML5 フォームと PDF forms のページネーションポリシーは異なるため、HTML5 フォームの前のページは PDF forms の前のページとは異なります。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>フォームの次のページに移動します。実行時に pageDown メソッドを使用します。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>キーボードフォーカスを指定したフィールドに設定します。フィールドをオブジェクトとして、またはフィールドの SOM 式で指定します。クライアントアプリケーションでのみ使用できます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>ドキュメント内のフィールドをデフォルト値にリセットします。</td>
   <td>結合されたデータを含むフォームのすべてのデータを、デフォルト値に復元するのではなく、消去します。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>画面にダイアログボックスを表示します。クライアントアプリケーションでのみ使用できます。</td>
   <td>「はい」／「いいえ」タイプのメッセージボックスを「OK」／「キャンセル」に変換します。3 つのボタンを含むメッセージボックスはサポートされていません。</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>実行時に、ドキュメントの現在アクティブなページを設定します。</p> <p>ページ値は 0 から始まるので、ドキュメントの最初のページは 0 の値を返します。</p> <p>currentPage プロパティは、クライアントで layout:ready を実行する場合に使用できます。ただし、サーバーで layout:ready を実行する場合は、フォームレイアウトが実行されるまでプロパティが実行されないので、使用できません。</p> </td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

### field {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>プロパティ</span></strong></th>
   <th><strong><span>説明<br /> </span></strong></th>
   <th><strong><span>例外</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>処理の異なるフェーズへの関連するオブジェクトの関与を制御します。オブジェクトがコンテナの場合、コンテナのコンテンツは、このコントロールが適用する制限を継承します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>コンテンツへのユーザーアクセスを制御します。</td>
   <td>除外グループでは機能しません。また、HTML5 フォームでは、非インタラクティブオブジェクトと保護オブジェクトを同じように処理します。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>スクリプト式でこの要素を識別するために使用される識別子。</td>
   <td>HTML5 フォームでは、オブジェクトの name プロパティを設定できません。これは、HTML5 フォームでは読み取り専用のプロパティです。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>単一のデータコンテンツを含むコンテンツ要素です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>このフィールドの形式設定されていない値を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>このフィールドの形式設定された値を指定します。</td>
   <td>スクリプトによる <code>formattedValue</code> の設定はサポートされていません。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>このフィールドの編集値を指定します。</td>
   <td>スクリプトによる <code>editValue </code> の設定はサポートされていません。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>このフィールドの形式検証メッセージの文字列を指定します。</td>
   <td>スクリプトによる <code>formatMessage </code> の設定はサポートされていません。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>このフィールドの背景色の値を指定します。別途、border.fill.presence プロパティを visible に設定する必要があります。</td>
   <td>フィールドのデフォルトの色を正しく返しません。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>border オブジェクトは、オブジェクトを囲む境界線を表します。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui オブジェクトには、フォームオブジェクトのユーザーインターフェイスでの説明が含まれます。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>フィールドの nullTest 値を指定します。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>このフィールドの境界線の色の値を指定します。別途、border.edge.presence プロパティを visible に設定する必要があります。</td>
   <td>フィールドのデフォルトの境界線の色を正しく返しません。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>リスト内にある項目数です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>現在のフィールドに新しい項目を追加します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>フィールドからすべての項目を削除します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>ドロップダウンリストまたはリストボックスの特定の表示項目の連結値を取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>フィールドの計算スクリプトを実行します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>フィールドの検証スクリプトを実行します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>オブジェクトのイベントスクリプトを実行します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>指定された項目の選択状態を返します</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>指定された項目の選択状態を設定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>指定された項目インデックスの項目表示テキストを取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>指定された項目インデックスのデータ値を取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>指定されたインデックスの項目を削除します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>指定された項目を現在のフィールドに設定します。既存の項目が置き換えられます。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>h</td>
   <td>レイアウトの高さの測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>w</td>
   <td>レイアウトの幅を指定する測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>x</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの X 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>y</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの Y 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>caption オブジェクトは、フォームデザインオブジェクトに関連付けられた説明ラベルを表します。<br /> </td>
   <td>なし</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>validate オブジェクトは、フォーム上でユーザーが提供したデータの検証を制御します。フォームが使用されている間、validate オブジェクトは何回でも有効にできます。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>このフィールドの親サブフォーム（ページ）を指定します。</td>
   <td>最初のスコープ外の親サブフォームを返す代わりに、常に親サブフォームを返します。<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>最初に選択した項目のインデックスです。</td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## フォーム {#form}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| formNodes | 指定したデータオブジェクトに連結された、すべてのフォームモデルオブジェクトのリストを返します。 |  |

## InstanceManager {#instancemanager}

| プロパティ | 説明 |
|---|---|
| `name` | スクリプト式でこの要素を識別するために使用される識別子。 |
| `occur` | 含まれるコンテナで許可されるインスタンス数の制限を説明します。 |
| `min` | インスタンス化することが可能な最小インスタンス数を指定します。 |
| `max` | インスタンス化することが可能な最大インスタンス数を指定します。 |
| `count` | インスタンス化された現在のインスタンス数を指定します。 |
| `setInstances` | このノードから指定されたサブフォームまたはサブフォームセットを追加または削除します。 |
| `addInstance` | サブフォームまたはサブフォームセットの新規インスタンスをこのノードに追加します。 |
| `removeInstance` | このノードからサブフォームまたはサブフォームセットを削除します。 |
| `moveInstance` | フォームモデルオブジェクトの子オブジェクトを、フォームモデル内の別の指定した場所に移動します。オブジェクトに対応するデータモデル情報も、データモデル内で再配置されます。 |
| `insertInstance` | このノードにサブフォームまたはサブフォームセットの新規インスタンスを挿入します。 |

## list {#list}

| プロパティ | 説明 |
|---|---|
| `length` | リスト内にある要素数。 |
| `item` | コレクションのゼロベースのインデックスです。 |
| `append` | ノードリストの末尾にノードを追加します。 |
| `remove` | ノードリストからノードを削除します。 |
| `insert` | ノードリスト内の特定のノードの前にノードを挿入します。 |

## node {#node}

| プロパティ | 説明 | 例外 |
|---|---|---|
| createNode | 有効なクラス名に基づいて新しいノードを作成します。 | なし |
| `isContainer` | このオブジェクトがコンテナオブジェクトかどうかを指定します。 | なし |
| `isNull` | 現在のデータ値が null 値かどうかを示します。 | なし |
| `resolveNode` | 現在の XML フォームオブジェクトモデルのオブジェクトから始めて、指定の SOM 式を評価し、SOM 式で指定されたオブジェクトの値を返します。 | なし |
| `resolveNodes` | 現在の XML フォームオブジェクトモデルのオブジェクトから始めて、指定の SOM 式を評価し、SOM 式で指定されたオブジェクトの値を返します。 | なし |
| oneOfChild | 有効なクラス名に基づいて新しいノードを作成します。 | なし |
| getElement | 指定された子オブジェクトを返します。 | なし |
| getAttribute | 指定されたプロパティ値を取得します。 | なし |
| setAttribute | 指定されたプロパティの値を設定します。 | なし |

## model {#model}

| プロパティ | 説明 | 例外 |
|---|---|---|
| 該当なし | 該当なし | 該当なし |

## サブフォーム {#subform}

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>他のインスタンス化されたインスタンスを基準として、オブジェクトのインデックスを指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>オブジェクトのイベントスクリプトを実行します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>サブフォーム内（サブフォームを含む）に含まれている、検証テストに失敗したノードのリストを返します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>border</td>
   <td>border オブジェクトは、オブジェクトを囲む境界線を表します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>このフィールドの境界線の色の値を指定します。別途、border.edge.presence プロパティを visible に設定する必要があります。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>h</td>
   <td>レイアウトの高さの測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>w</td>
   <td>レイアウトの幅を指定する測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>x</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの X 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>y</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの Y 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>validate オブジェクトは、フォーム上でユーザーが提供したデータの検証を制御します。フォームが使用されている間、validate オブジェクトは何回でも有効にできます。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>name</td>
   <td>スクリプト式でこの要素を識別するために使用される識別子。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>オブジェクトの表示／非表示を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>access</td>
   <td>サブフォームなどのコンテナオブジェクトのコンテンツへのユーザーアクセスを制御します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>同じフォームオブジェクトの他のインスタンスとの相対位置に基づいて、サブフォームまたはサブフォームセットのインデックスを計算します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager オブジェクトは、フォームモデルオブジェクトのインスタンスの作成、削除、および移動を管理します。<br /> </td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

### submit {#submit}

| プロパティ | 説明 |
|---|---|
| target | データの送信先の URL。この属性を省略すると、XFA 処理アプリケーションは、config オブジェクト内の製品固有の情報へのアクセスなど、製品固有の手法を使用して URI を取得します。 |

## tree {#tree}

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>nodes</td>
   <td>現在のオブジェクトのすべての子オブジェクトのリストを返します。</td>
   <td>
    <ul>
     <li>xfa.nodes、desc ではサポートされていません。</li>
     <li>PDF と HTML に対してレポートされるノード数は異なります。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>このノードの名前を指定します。</td>
   <td>スクリプトを使用した名前の設定は、HTML では許可されていません。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>このノードの親を取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>類似名、範囲内、子のような関係のノードのコレクションにおける、このノードの位置を返します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>このノードの SOM 式を取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>現在の XML フォームオブジェクトモデルのオブジェクトから始めて、指定の SOM 式を評価し、SOM 式で指定されたオブジェクトの値を返します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>現在の XML フォームオブジェクトモデルのオブジェクトから始めて、指定の SOM 式を評価し、SOM 式で指定されたオブジェクトの値を返します。</td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## subformset {#subformset}

| プロパティ | 説明 | 例外 |
|---|---|---|
| instanceManager | instanceManager オブジェクトは、フォームモデルオブジェクトのインスタンスの作成、削除、および移動を管理します。 | なし |

## content {#content}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| isNull | 現在のデータ値が null 値かどうかを示します。 |  |

## dataValue {#datavalue}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| isNull | 現在のデータ値が null 値かどうかを示します。 |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ </strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、パターンオブジェクトの一意のカラーを表します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## fill {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、一意の塗りつぶしのカラーを定義します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## linear {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、フォーム上の線形のグラデーション塗りつぶしの一意のカラーを表します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## line {#line}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>edge オブジェクトは、円弧、線、または境界線や長方形の 1 辺を表します。<br /> </td>
   <td>カラー、キャップなどの属性はサポートされていません。<br /> </td>
  </tr>
 </tbody>
</table>

## pattern {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、パターンオブジェクトの一意のカラーを表します。 </td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## radial {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、放射状オブジェクトの一意のカラーを表します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## stipple {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、点描オブジェクトの一意のカラーを表します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>プロパティ</td>
   <td>説明</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui オブジェクトには、フォームオブジェクトのユーザーインターフェイスでの説明が含まれます。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>caption オブジェクトは、フォームデザインオブジェクトに関連付けられる説明ラベルを表します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>presence</td>
   <td>オブジェクトの表示／非表示を指定します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>スクリプト式でこのオブジェクトまたはイベントを指定するために使用可能な識別子を指定します。</td>
   <td>実行時の値の設定はサポートされていません。</td>
  </tr>
  <tr>
   <td>value</td>
   <td>value オブジェクトには、データコンテンツ 1 単位が含まれます。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## corner {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>color</td>
   <td>color プロパティは、コーナーオブジェクトの一意のカラーを表します。</td>
   <td>
    <ul>
     <li>デフォルト値は取得できません。 </li>
     <li>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI に反映されません。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>border オブジェクトは、checkButton オブジェクトを囲む境界線を表します。 </td>
   <td>変更はモデルに反映され、スクリプティングに使用できますが、HTML 要素には同期されません。したがって、変更は UI には反映されません。<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<br /> </strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>border オブジェクトは、choiceList オブジェクトを囲む境界線を表します。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| border | border オブジェクトは、dateTimeEdit オブジェクトを囲む境界線を表します。 |  |

## 画像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>参照先のドキュメントのコンテンツの種類を MIME タイプで表現して指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>スクリプト式でこの要素を識別するために使用される識別子。</td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| border | border オブジェクトは、imageEdit オブジェクトを囲む境界線を表します。 |  |

## numericEdit {#numericedit}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| border | border オブジェクトは、オブジェクトを囲む境界線を表します。 | なし |

## object {#object}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>このオブジェクトのクラスの名前を特定します。<br /> </td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## rectangle {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>edge オブジェクトは、円弧、線、または境界線や長方形の 1 辺を表します。<br /> </td>
   <td>カラー、キャップなどの属性はサポートされていません。</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>border</td>
   <td>border オブジェクトは、オブジェクトを囲む境界線を表します。<br /> </td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>layout</td>
   <td>このオブジェクトで使用するレイアウト方法を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>border</td>
   <td>このフィールドを囲む境界線を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>フィールドの nullTest 値を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>このフィールドの境界線のカラー値を指定します。スクリプティングによってカラーを変更する前に、境界線を定義する必要があります。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>このフィールドの境界線の幅を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>h</td>
   <td>レイアウトの高さの測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>transient</td>
   <td>処理アプリケーションで除外グループの値の保存を、フォーム送信と保存操作のどちらの一環として行うかを指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>w</td>
   <td>レイアウトの幅を指定する測定値です。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>x</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの X 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>y</td>
   <td>位置固定レイアウトで配置した場合の、親コンテナの左上隅を基準としたコンテナのアンカーポイントの Y 座標を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>caption オブジェクトは、フォームデザインオブジェクトに関連付けられた説明ラベルを表します。<br /> </td>
   <td>なし</td>
  </tr>
  <tr>
   <td>validate</td>
   <td>validate オブジェクトは、フォーム上でユーザーが提供したデータの検証を制御します。フォームが使用されている間、validate オブジェクトは何回でも有効にできます。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>結合後にフォームノードが連結されるデータノードを取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>presence</td>
   <td>オブジェクトの表示／非表示を指定します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>access</td>
   <td>サブフォームなどのコンテナオブジェクトのコンテンツへのユーザーアクセスを制御します。</td>
   <td>exclgrp 内の個々の項目に対しては、常にオープンを返します。 </td>
  </tr>
  <tr>
   <td>name</td>
   <td>スクリプト式でこのオブジェクトまたはイベントを指定するために使用可能な識別子を指定します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>members</td>
   <td>除外グループのメンバーを指定します。 </td>
   <td>なし</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>除外グループの選択されたメンバーを返します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>指定したオブジェクトとその子オブジェクトの calculate イベントでスクリプトを実行します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>calculate</td>
   <td>calculate オブジェクトは、フィールドの値の計算を制御します。<br /> </td>
   <td>なし</td>
  </tr>
 </tbody>
</table>

## arc {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<strong></strong></strong></td>
   <td><strong>説明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>edge オブジェクトは、円弧、線、または境界線や長方形の 1 辺を表します。<br /> </td>
   <td>カラー、キャップなどの属性はサポートされていません。 </td>
  </tr>
 </tbody>
</table>

## border {#border}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ<strong></strong></strong></td>
   <td><strong>説明<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>edge オブジェクトは、円弧、線、または境界線や長方形の 1 辺を表します。<br /> </td>
   <td>カラー、キャップなどの属性はサポートされていません。 </td>
  </tr>
 </tbody>
</table>

## $layout {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>指定したフォームデザインオブジェクトの高さを判定します。<br /> </td>
   <td>
    <ul>
     <li>高さ（h）プロパティは、ページ領域およびコンテンツ領域に対してはサポートされていません。 </li>
     <li>パラメーター「Offset from first content area the XFA-Form object occurs on」はサポートされていません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定したフォームデザインオブジェクトの幅を判定します。</td>
   <td>
    <ul>
     <li>幅（w）プロパティは、ページ領域およびコンテンツ領域に対してはサポートされていません。 </li>
     <li>パラメーター「Offset from first content area the XFA-Form object occurs on」はサポートされていません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>親オブジェクトを基準とする、指定したフォームデザインオブジェクトの X 座標を判定します。</td>
   <td>
    <ul>
     <li>x 座標（x）プロパティは、ページ領域およびコンテンツ領域に対してはサポートされていません。 </li>
     <li>パラメーター「Offset from first content area the XFA-Form object occurs on」はサポートされていません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>親オブジェクトを基準とする、指定したフォームデザインオブジェクトの Y 座標を判定します。</td>
   <td>
    <ul>
     <li>y 座標（y）プロパティは、ページ領域およびコンテンツ領域に対してはサポートされていません。 </li>
     <li>パラメーター「Offset from first content area the XFA-Form object occurs on」はサポートされていません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>現在のフォームのページ数を判定します。</td>
   <td>
    <ul>
     <li>layout.pageCount() method は、PDF および HTML フォームに対して異なる値を返します。</li>
     <li>オブジェクトを非表示にすることでページカウントを少なくした場合、abspagecount メソッドは不正な値を返します。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>フォームの指定したページからフォームデザインオブジェクトの種類を取得します。</td>
   <td>なし</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>現在のフォームのページ数を判定します。</td>
   <td>
    <ul>
     <li>layout.pageCount() method は、PDF および HTML フォームに対して異なる値を返します。</li>
     <li>オブジェクトを非表示にすることでページカウントを少なくした場合、abspagecount メソッドは不正な値を返します。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## item {#items}

| **プロパティ** | **説明** | **例外** |
|---|---|---|
| presence | オブジェクトの表示／非表示を指定します。 | なし |

## FormCalc {#formcalc}

FormCalc は e フォーム中心のロジックと計算のルートを作成するための XFA 固有の言語です。FormCalculation は強力なビルド関数のセットを提供します。

### FormCalc によってサポートされている関数 {#formcalc-supported-functions}

### FormCalc 式のサポート {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>カテゴリ </strong></td>
   <td><strong>説明 </strong></td>
   <td><strong>サンプル </strong></td>
  </tr>
  <tr>
   <td>単純式</td>
   <td>加算、減算、乗算、除算および括弧</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>変数の宣言</td>
   <td>変数の定義</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>論理式</td>
   <td>
    <ul>
     <li>ロジック（and／or）</li>
     <li>比較（より大きい／より小さい／等しい）</li>
    </ul> </td>
   <td>A or 1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A or 1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>if 式</td>
   <td><br type="_moz" /> </td>
   <td>if (a&gt;b) then 2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>while (i lt 5) do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td>for</td>
   <td><br type="_moz" /> </td>
   <td>for i = 100 downto 1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>for each</td>
   <td><br type="_moz" /> </td>
   <td>for each i in (1, 2, 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>関数の宣言</td>
   <td>FormCalc でのカスタム関数の定義</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API のサポート {#acrobat-api-support}

1. **演算関数**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. Count()
   1. Floor()
   1. Max()
   1. Min()
   1. Mod()
   1. Round()
   1. Sum()

1. **科学関数**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. Tan()
   1. Exp()
   1. Log()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **会計関数**

   1. Apr()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. Term()

1. **論理関数**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **文字列関数**

   1. At()
   1. Concat()
   1. Left()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. Replace()
   1. Right()
   1. Rtrim()
   1. Space()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日付と時間**

   1. Date()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>説明</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>この Acrobat API は、出力された toJavaScript コンソールをダンプします。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>この Acrobat API は、アラートメッセージ throughJavaScript のポップアップを送信します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>システムにサウンドを再生させます。</td>
   <td>実行されたアクションはありません。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>モーダルダイアログボックスが表示されます。ホストアプリケーションを再び直接使用するには、ユーザーがモーダルダイアログボックスを閉じる必要があります。</td>
   <td>アクションは実行されません。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>ブラウザーウィンドウで URL を起動します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>JavaScript スクリプトと期間を指定します。スクリプトは期間が経過するたびに実行されます。このメソッドの戻り値は、JavaScript 変数で保持する必要があります。保持されない場合、interval オブジェクトがガベージコレクションの対象となり、時計が停止する可能性があります。定期的な実行を終了するには、返された interval オブジェクトを clearInterval に渡します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>JavaScript スクリプトと期間を指定します。スクリプトは期間の経過後に 1 回だけ実行されます。このメソッドの戻り値は、JavaScript 変数で保持する必要があります。保持されない場合、timeout オブジェクトがガベージコレクションの対象となり、時計が停止する可能性があります。timeout イベントをキャンセルするには、返された timeout オブジェクトを clearTimeOut に渡します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>setInterval メソッドによって最初に設定された、以前に登録された間隔をキャンセルします。</td>
   <td>HTML5 フォームでは、API は正常に動作しません。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>以前に登録されたタイムアウト間隔をキャンセルします。この間隔は、setTimeOut によって最初に設定されたものです。</td>
   <td>HTML5 フォームでは、API は正常に機能しません。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>指定されたスクリプトを実行します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>アクティブな各ドキュメントの Doc オブジェクトを含む配列。アクティブなドキュメントがない場合、activeDocs は何も返しません。つまり、Core JavaScript の d = new Array(0) と同じ動作になります。</td>
   <td>HTMl5 フォームに空の配列を返します。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>true（デフォルト値）の場合、計算を実行できます。false の場合、計算は許可されません。</td>
   <td>HTML5 フォームでは常に true です。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>様々な定数値を保持するためのラッパーオブジェクト。現在、このプロパティは 1 つのプロパティ、align を持つオブジェクトを返します。</td>
   <td>HTML5 フォームは空の align オブジェクトを返します。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>フォーカスの長方形のオンとオフを切り替えます。フォーカスの長方形は、ボタン、チェックボックス、ラジオボタン、署名の周囲にある薄い点線で、フォームフィールドにキーボードフォーカスがあることを示します。値を true にすると、フォーカスの長方形がオンになります。</td>
   <td>HTML5 フォームでは常に true です。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>ビューアフォームソフトウェアのバージョン番号。スクリプトの下位互換性を維持する場合は、このプロパティを確認して、新しいバージョンのソフトウェアのオブジェクト、プロパティまたはメソッドが使用できるかどうかを判断します。</td>
   <td>常に 11.001。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>実行中の Acrobat ビューアの言語。</td>
   <td>HTML5 フォームでは常に ENU です。</td>
  </tr>
 </tbody>
</table>

## サポートされる XFA イベント {#supported-xfa-events}

次のクライアント側の XFA イベントがサポートされています。

* 初期化
* Validate
* Calculate
* Click
* Enter
* 終了
* Change
* ValidationState

>[!NOTE]
>
>HTML5 フォームはクライアントサイド（ブラウザー）でレンダリングされます。サーバーサイドのスクリプトではなく、クライアントサイドの **validate** スクリプトおよび **calculate** スクリプトを使用します。
