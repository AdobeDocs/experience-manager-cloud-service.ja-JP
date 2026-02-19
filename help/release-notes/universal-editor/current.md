---
title: ユニバーサルエディター 2026.02.19 リリースノート
description: ユニバーサルエディターの 2026.02.19 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 28%

---


# ユニバーサルエディター 2026.02.19 リリースノート {#release-notes}

ユニバーサルエディターの 2026 年 2 月 19 日リリースのリリースノートです。

>[!TIP]
>
>ユニバーサルエディターの&#x200B;**今後の**&#x200B;機能をリリース前にテストしたい場合は、[ユニバーサルエディターのプレビューリリースノート](/help/release-notes/universal-editor/preview.md)を参照してください。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* RTE が改善されました。
   * [ コンテキスト RTE でのツールバー項目の非表示 ](/help/implementing/universal-editor/configure-rte.md#common-action-options) がサポートされるようになりました。
   * [ テーブル内のテキストを段落で折り返す ](/help/implementing/universal-editor/configure-rte.md#table-actions) がサポートされるようになりました。
   * [ サポートされていないHTML タグ ](/help/implementing/universal-editor/configure-rte.md#unsupported-html) タグが RTE で保持できるようになりました。
   * RTE ロジックが別のファイルから提供されるようになりました。
   * [ テーブルを作成し ](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options)RTE を使用して編集できるようになりました。
* ラベルを設定しない場合は、コンポーネント定義のコンポーネントタイトルが使用されるようになります。
* 拡張機能から `setEditorMode` を使用できるようになりました。

## 早期導入機能 {#early-adopter}

以下に示す今後の機能のテストおよびフィードバックの提供に興味がある場合は、Adobe IDに関連付けられたメールアドレスからAdobe カスタマーサクセスマネージャーにメールを送信してください。

* シャローコピーがコンテンツフラグメントに実装されました。

## その他の改善点 {#other-improvements}

* RTE エンドポイントがインプレースエディターで提供されるようになりました。
* ネストされたフィールドを編集しても、これらの構造からピアエントリが上書きされなくなりました。
* 必須の RTE フィールドを空として保存できなくなりました。
* 書式設定後にリンクを追加した際に、インプレース書式設定が誤って適用されなくなりました。
