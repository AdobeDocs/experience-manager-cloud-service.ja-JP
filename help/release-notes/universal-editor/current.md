---
title: ユニバーサルエディター 2025.10.30 リリースノート
description: ユニバーサルエディター 2025.10.30 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: e3e571bef450ddc09eb30ab7d73b144ea521a87b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 58%

---


# ユニバーサルエディター 2025.10.30 リリースノート {#release-notes}

ユニバーサルエディターの 2025 年 10 月 30 日リリースのリリースノートです。

>[!TIP]
>
>ユニバーサルエディターの&#x200B;**今後の**&#x200B;機能をリリース前にテストしたい場合は、[ユニバーサルエディターのプレビューリリースノート](/help/release-notes/universal-editor/preview.md)を参照してください。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* [&#x200B; 新しい RTE](#new-rte) で画像を挿入できるようになりました。
   * この機能は OOtB で無効になっており、[&#x200B; フィルター定義 &#x200B;](/help/implementing/universal-editor/configure-rte.md#toolbar) を使用して明示的に有効にする必要があります。

## 早期導入機能 {#early-adopter}

これらの今後の機能をテストしてフィードバックを共有することに関心がある方は、Adobe ID に関連付けられたメールアドレスからアドビカスタマーサクセスマネージャーにメールを送信してください。

### 新規 RTE {#new-rte}

リンクダイアログにピッカーを備えた新規 ProseMirror RTE が右側のパネルで使用できるようになりました。[この RTE には、柔軟な設定オプションが用意されています。](/help/implementing/universal-editor/configure-rte.md)

## その他の改善点 {#other-improvements}

* アクションを取り消した場合に、更新イベントに通知されるようになりました。
* 文字列 `No results`、ユニバーサルエディターのタグのブラウザーロケールに依存するようになりました。
* ユニバーサルエディターの「公開」ボタンの余分な改行を修正しました。
* Patch API に対してクリーンアップが行われました。
* Safari で「コンテンツを選択」ボタンが表示されるようになりました。
* RPM ビルドが修正されました。
* CORS を更新して、保存後に編集されたテキストが再度更新されるのを回避しました。
