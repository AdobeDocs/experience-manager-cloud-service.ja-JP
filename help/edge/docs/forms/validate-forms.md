---
title: スプレッドシートからFormsへ — アダプティブフォームのブロックフィールド検証のマスタリング
description: スプレッドシートとアダプティブフォームブロックフィールドを使用して、強力なフォームをより迅速に作成できます。 このガイドは、EDS Forms Block フィールドのカスタム検証を構築する場合に役立ちます。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# フォームフィールドに検証機能を追加する

アダプティブフォームブロックには、組み込みの検証機能があります。 最新のブラウザーでは、選択されたフィールドタイプと指定した追加のプロパティに基づいて、これらの検証が自動的に適用されます。

## フィールドの種類と検証について

アダプティブフォームブロックは、様々な [HTML5 の入力タイプ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)（テキスト、電子メール、数値、日付など）。 また、対応しています [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)、選択、フィールドセット、およびHTML5 に備わっている包括的な入力検証機能。

では、HTMLフィールドタイプを使用して、ユーザーが入力できるデータの種類を定義します。 フィールドの種類によって、組み込みの検証ルールが異なります。

Email：このフィールドタイプは、一般的な E メールアドレス形式に対するユーザー入力を自動的に検証します。 無効な E メールを入力したユーザーには、エラーメッセージが表示されます。
数値：このフィールドタイプは数値の入力のみ可能です。 数字以外の文字を入力したユーザーは、エラーを受け取ります。
日付：このフィールドタイプは、標準の日付形式に対してユーザー入力を検証します。 妥当な範囲外の日付も、無効としてフラグ付けされる場合があります。
URL：このフィールドタイプは、有効な URL 形式に対するユーザー入力を検証します。 ユーザーが無効な URL を入力すると、エラーメッセージが表示されます。
Tel：このフィールドタイプは、電話番号用に特別に設計されており、特定の国の形式（一般的にはサポートされていません）に基づいたトリガー検証がおこなわれる場合があります。


## 詳細を表示する

* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-eds-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)