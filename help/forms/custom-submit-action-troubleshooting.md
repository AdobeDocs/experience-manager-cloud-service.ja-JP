---
title: アダプティブFormsのカスタム送信アクションに関する 502 エラーのトラブルシューティング
description: アダプティブForms（コアコンポーネント）でカスタム送信アクションを使用する際に発生する 502 エラーページを特定し解決する方法を説明します。 このガイドでは、未処理の例外など、一般的な原因を説明し、解決手順を示します。
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---


# トラブルシューティング：カスタム送信アクションの 502 エラーページ

アダプティブForms（コアコンポーネント）を操作する際に、カスタムの送信アクションを使用するフォームを送信した後に **HTMLで** 502 エラーページが発生する場合があります。

## 問題

**エラー：** カスタム送信アクションサービスが失敗すると、502 エラーページのHTMLが表示されます。

**理由：** これは、カスタム送信アクションで未処理のエラー（null ポインター、無効な API 応答、実行時エラーなど）がスローされた場合に発生します。

## 解決策

502 エラーページを防ぐには、送信ロジックを try-catch ブロックでラップして、エラーを適切に処理します。

手順について詳しくは、「[&#x200B; アダプティブForms（コアコンポーネント）のカスタム送信アクションの作成 &#x200B;](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md) を参照してください。
