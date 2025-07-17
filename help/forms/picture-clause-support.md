---
title: HTML5 フォームにおけるパターン形式文字列サポート
description: HTML5 フォームは、日付、テキストおよび数値記号の表示値と形式設定された値の XFA パターン形式文字列をサポートしています。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 95%

---

# HTML5 フォームにおけるパターン形式文字列サポート {#picture-clause-support-for-html-forms}

<span class="preview"> HTML5 Forms機能は、早期アクセスプログラムの一部として提供されています。 アクセスをリクエストするには、公式（職場）メール ID からaem-forms-ea@adobe.comにメールを送信します。
</span>

HTML5 フォームは、日付、テキストおよび数値記号の表示値と形式設定された値の XFA パターン形式文字列をサポートしています。次のパターン形式文字列の式がサポートされています。

* category （locale） {picture-clause} | category （locale） {picture-clause} | category （locale）{picture-clause}
* category.subcategory{}

>[!NOTE]
>
>現在 Mobiles Forms はパターン形式文字列の編集をサポートしていません。また、DateTime と Time のパターン形式文字列の記号もサポートされていません。

## サポートされている日付フィールドの記号 {#supported-date-field-symbols}

サポートされている日付のパターン形式文字列の式

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause symbols}

>[!NOTE]
>
>パターン形式文字列のデフォルトパターンは {MMM D, YYYY} パターンです。パターンが適用されない場合は、デフォルトパターンが使用されます。

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th>解釈</th>
  </tr>
  <tr>
   <td>D</td>
   <td>日付を 1 桁または 2 桁の数値（1～31）で表します。</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>日付をゼロで埋められた 2 桁の数値（01～31）で表します。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>月を 1 桁または 2 桁の数値（1～12）で表します。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>月をゼロで埋められた 2 桁の数値（01～12）で表します。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>現在のロケールの略された月名<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>現在のロケールの完全な月名<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>現在のロケールの略された曜日<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>現在のロケールの完全な曜日<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2 桁の年、00 = 2000、29 = 2029、30 = 1930、99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4 桁の年<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> デザイン上、HTML5 フォームの日付フィールドは編集形式の `MM-YYYY` パターンをサポートしていません。ただし、表示形式ではこのパターンがサポートされます。

## 数値のパターン形式文字列 {#numeric-picture-clause}

HTML5 フォームは、数値のパターン形式文字列の記号をサポートしています。ただし、PDF フォームと HTML フォームの間でサポートに違いがあります。

**PDF フォーム**&#x200B;では、パターン形式文字列の記号の数に関わらず数字が形式設定されます。

**HTML フォーム**&#x200B;では、パターン形式文字列の記号の数より数字の桁数が少ない場合にのみ、数字が形式設定されます。

**例**：num{zzz,zzz,zz9} というパターン形式文字列について考えます。

**10000** の数字は HTML フォームと PDF フォームの両方で **10,000** として形式設定されます。

PDF フォームでは、1000000 の数字は 1,000,000 として形式設定されます。ただし、この数字は HTML フォームでは形式設定されず、1000000 のままになります。

**HTML フォーム**&#x200B;においてサポートされている数値のパターン形式文字列の式は次の通りです。

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th><strong>解釈</strong></th>
   <th>入力の解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または、対応する位置にある入力データが空またはスペースの場合は 0 で桁埋め。<br /> </td>
   <td>1 桁の数値</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または、対応する位置にある入力データのが空、スペース、または 0 の桁の場合はスペース。<br /> </td>
   <td>1 桁の数値またはスペース</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または対応する位置にある入力データが空、スペース、または 0 の桁の場合は空。<br /> </td>
   <td>1 桁の数値または空</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>出力の形式設定</strong>：指数の記号（E）から成る浮動小数点値の指数の部分。オプションのプラス記号またはマイナス記号が後に続きます。指数値が後に続きます。<br /> </td>
   <td>出力の形式設定と同じ</td>
  </tr>
  <tr>
   <td>CR または cr<br /> </td>
   <td>負の数の場合は貸方記号（CR）。そうでない場合は空。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S または s<br /> </td>
   <td>出力の形式設定：負の数の場合はマイナス記号。そうでない場合はスペース。<br /> </td>
   <td>負の数の場合はマイナス記号。正の数の場合はプラス記号。</td>
  </tr>
  <tr>
   <td>V</td>
   <td>現行のロケールの小数点。入力の解析時に小数点を暗黙なものとします。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>現行のロケールの小数点。入力を解析、および出力を形式設定するときに小数点を暗黙なものとします。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>現行のロケールの小数点。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>現行のロケールのグループセパレータ。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>現行のロケールの通貨記号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>現行のロケールのパーセント記号</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>負の数の場合は左括弧。そうでない場合はスペース。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>負の数の場合は右括弧。そうでない場合はスペース。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>タブ文字</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## テキストのパターン形式文字列 {#text-picture-clause}

HTML5 フォームは、次のテキストのパターン形式文字列の式をサポートしています。

* text{text Picture clause symbols}

| **記号** | **解釈** |
|---|---|
| A | 英字 1 文字。 |
| X | 1 文字。 |
| O | 英数字 1 文字。 |
| 0（ゼロ） | 英数字 1 文字。 |
| 9 | 1 桁の数値。 |
