---
title: ユニバーサルエディター 2025.03.10 リリースノート
description: ユニバーサルエディターの 2025.03.10 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 23%

---


# ユニバーサルエディター 2025.03.10 リリースノート {#release-notes}

ユニバーサルエディターの 2025 年 3 月 10 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* **コンポーネントの移動：**[ コンテナ間でコンポーネントを移動 ](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) ターゲットコンテナのコンポーネントフィルターを監視するようになりました。
   * コンテナ間でコンポーネントを移動するために、ターゲットコンテナと宛先コンテナの両方に同じ [ フィルター定義 ](/help/implementing/universal-editor/filtering.md) を使用する必要がなくなりました。
* **ロックされたページ：** ユニバーサルエディターサービスは、[ ページのロック状態 ](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) を監視し、ロックされていないページや、ユーザーによってロックされているページへの書き込みのみを行います。

## その他の改善点 {#other-improvements}

* ヘッドレスキャンバスの正しい検証を修正しました。

## 廃止 {#deprecation}

* npm または `https://unviersal-editor-service.experiencecloud.live/corslib/*` を介して提供される `universal-editor-cors` ライブラリは使用できなくなりました。
   * 代わりに、`https://universal-editor-service.adobe.io/cors.js` を指すスクリプトタグを使用してください。
   * ユニバーサルエディターで使用するページを適切に実装する方法について詳しくは、[AEM Developers のユニバーサルエディターの概要 ](/help/implementing/universal-editor/developer-overview.md) を参照してください。
   * 間違った方法を使用すると、非推奨メッセージが 1 日に 1 回表示されます。
