---
title: ユニバーサルエディター 2025.09.04 リリースノート
description: ユニバーサルエディター 2025.09.04 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 71%

---


# ユニバーサルエディター 2025.09.04 リリースノート {#release-notes}

ユニバーサルエディターの 2025 年 9 月 4 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* コピーと貼り付けは、[ 早期導入 ](#copy-paste) に使用できます

### 取り消し／やり直し {#undo-redo}

ユニバーサルエディターのコンテンツ作成者が取り消しとやり直しを使用できるようになりました。

* これには、コンテキスト内での編集、プロパティパネルを使用した編集、ブロックの追加（または複製）、移動、削除が含まれます。
* 取り消しとやり直しは、現在のブラウザーセッションに限定されます。

## 早期導入機能 {#early-adopter}

これらの今後の機能をテストしてフィードバックを共有することに関心がある方は、Adobe ID に関連付けられたメールアドレスからアドビカスタマーサクセスマネージャーにメールを送信してください。

### 新規 RTE {#new-rte}

リンクダイアログにページピッカーを備えた新規 ProseMirror RTE が右側のパネルで使用できるようになりました。

### コピー/ペースト {#copy-paste}

同じページ内のコンポーネントをコンテンツ作成者がコピーして貼り付けることができるようになりました。

## その他の改善点 {#other-improvements}

* エディターツールバーのスタイル設定が更新され、今後の新しい RTE との連携が改善されました。
* アセットピッカーダイアログのフィルターが復元されました。

## 廃止 {#deprecations}

* `text-input` コンポーネントと `text-area` コンポーネントは、[リリース 2025.07.09](/help/release-notes/universal-editor/2025/2025-07-09.md) で、正式に非推奨（廃止予定）となりました。
   * `model-definition.json` では、テキストコンポーネントを使用して、プロパティパネルのテキスト入力を作成します。
