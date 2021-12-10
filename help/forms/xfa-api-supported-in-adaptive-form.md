---
title: XDP ベースのアダプティブフォームでの XFA のサポート
seo-title: XFA support in XDP-based Adaptive Forms
description: アダプティブフォームでサポートされる XFA イベント、プロパティ、スクリプト、検証をリストします。
seo-description: Lists supported XFA events, properties, scripts, and validation in Adaptive Forms.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 100%

---


# XDP ベースのアダプティブフォームでの XFA のサポート{#xfa-support-in-xdp-based-adaptive-forms}

## はじめに {#introduction}

アダプティブフォームでは、以下を含め、XDP ファイルで定義される様々な XFA イベント、プロパティ、スクリプト、検証に対するサポートが提供されます。

* XDP ファイルのイベントで定義されたスクリプトの実行
* XDP ファイル内の各フィールドのデフォルトの値および動作プロパティの取得
* XDP ファイルで定義された検証スクリプトの実行

XDP ファイルに基づいてアダプティブフォームが作成されると、プロパティ、イベントおよび検証がフォームオーサリング UI に自動入力されます。ただし、フォーム作成者は、これらの要素の一部を上書きして代替エクスペリエンスを作成できます。

この記事では、アダプティブフォームでサポートされる XFA イベント、プロパティ、検証をリストし、アダプティブフォームでこれらを上書きする方法を説明します。

## アダプティブフォームでサポートされる XFA 要素とそのマッピング {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### フィールド {#fields}

XDP ファイルを使用してアダプティブフォームを作成すると、XFA フィールドをアダプティブフォームにドラッグ＆ドロップできます。以下の表に、XFA フィールドがアダプティブフォームのフィールドにマッピングされる方法を示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA フィールドまたはコンテナ</strong></p> </td>
   <td><p><strong>対応するアダプティブフォームのコンポーネント</strong></p> </td>
  </tr>
  <tr>
   <td><p>ボタン </p> </td>
   <td><p>ボタン</p> </td>
  </tr>
  <tr>
   <td><p>チェックボックス </p> </td>
   <td><p>チェックボックス</p> </td>
  </tr>
  <tr>
   <td><p>リストボックス </p> </td>
   <td><p>ドロップダウンリスト</p> </td>
  </tr>
  <tr>
   <td><p>日付／時間フィールド </p> </td>
   <td><p>日付選択</p> </td>
  </tr>
  <tr>
   <td><p>手書き署名</p> </td>
   <td><p>手書き署名</p> </td>
  </tr>
  <tr>
   <td><p>数値フィールド </p> </td>
   <td><p>数値ボックス</p> </td>
  </tr>
  <tr>
   <td><p>十進数フィールド</p> </td>
   <td><p>数値ボックス</p> </td>
  </tr>
  <tr>
   <td><p>テキストフィールド </p> </td>
   <td><p>テキストボックス</p> </td>
  </tr>
  <tr>
   <td><p>パスワードフィールド </p> </td>
   <td><p>パスワードボックス</p> </td>
  </tr>
  <tr>
   <td><p>画像</p> </td>
   <td><p>画像</p> </td>
  </tr>
  <tr>
   <td><p>テキスト</p> </td>
   <td><p>テキスト</p> </td>
  </tr>
  <tr>
   <td><p>サブフォーム </p> </td>
   <td><p>パネル</p> </td>
  </tr>
  <tr>
   <td><p>領域（グループ）</p> </td>
   <td><p>パネル</p> </td>
  </tr>
  <tr>
   <td><p>サブフォームセット </p> </td>
   <td><p>パネル</p> </td>
  </tr>
 </tbody>
</table>

### プロパティ {#properties}

以下の表に、XDF ファイルで定義された様々な XFA スクリプトがアダプティブフォームでどのように動作するかを示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA コンポーネントのプロパティ</strong></p> </td>
   <td><p><strong>アダプティブフォームでの対応する動作</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>アダプティブフォームのバインド参照（bindRef）プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>アダプティブフォームの visible プロパティにマッピングされる。表示式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>アダプティブフォームの enabled プロパティにマッピングされる。アクセス式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: role </p> </td>
   <td><p>アダプティブフォームの role プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: speakPriority </p> </td>
   <td><p>アダプティブフォームの speakPriority プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: speakText</p> </td>
   <td><p>アダプティブフォームのカスタムアクセシビリティテキストにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: toolTip </p> </td>
   <td><p>アダプティブフォームの short description（短い説明）プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>caption<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの Title プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの表示パターンにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの value プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>items<em>（リストボックス、チェックボックス）</em></p> </td>
   <td><p>アダプティブフォームの options プロパティにマッピングされる。オプション式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em>（テキストフィールド）</em></p> </td>
   <td><p>アダプティブフォームの Maximum characters allowed プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>multiline<em>（テキストフィールド）</em></p> </td>
   <td><p>アダプティブフォームの Allow multiple lines プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em>（数値フィールド、十進数フィールド）</em></p> </td>
   <td><p>アダプティブフォームの Frac digits プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em>（数値フィールド、十進数フィールド）</em></p> </td>
   <td><p>アダプティブフォームの Lead digits プロパティにマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em>（リストボックス）</em></p> </td>
   <td><p>アダプティブフォームの Allows multiple selection プロパティにマッピングされる。</p> </td>
  </tr>
 </tbody>
</table>

### スクリプト {#scripts}

以下の表に、XDF ファイルで定義された様々な XFA スクリプトがアダプティブフォームでどのように動作するかを示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA スクリプトイベント</strong></p> </td>
   <td><p><strong>アダプティブフォームでの対応する動作</strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。</p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>アダプティブフォームの式の計算にマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>アダプティブフォームの検証式にマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。</p> </td>
  </tr>
  <tr>
   <td><p>click（ボタンフィールド）</p> </td>
   <td><p>ボタンのクリック式にマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>Support for server-side script</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。</p> </td>
  </tr>
  <tr>
   <td><p>Support for web services</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。</p> </td>
  </tr>
  <tr>
   <td><p>Change（手書きフィールド、ラジオボタン、チェックボックス）</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームでは上書きできません。</p> </td>
  </tr>
 </tbody>
</table>

### 検証 {#validations}

以下の表に、XFA 検証がアダプティブフォームの検証にどのようにマッピングされるかを示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA 検証</strong></p> </td>
   <td><p><strong>アダプティブフォームでの対応する検証</strong></p> </td>
  </tr>
  <tr>
   <td><p>検証パターン（formatTest）</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>検証パターンのメッセージ（formatTestMessage）</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必須（nullTest）</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>メッセージを空にする（nullTestMessage） </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>スクリプトを検証（scriptTest）</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>検証スクリプトのメッセージ（scriptTestMessage）</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>XFA チェックボタンに連結されたアダプティブフォームのラジオボタンおよびチェックボックスグループの必須プロパティを上書きすることはできません。

