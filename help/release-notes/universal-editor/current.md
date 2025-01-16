---
title: ユニバーサルエディター 2054.01.16 リリースノート
description: ユニバーサルエディターの 2025.01.16 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 19%

---


# ユニバーサルエディター 2025.01.16 リリースノート {#release-notes}

ユニバーサルエディターの 2025 年 1 月 16 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* **CORS ライブラリ &lt; 3.0.0 の廃止** – 今後の互換性を確保し、セキュリティを強化するために、ユニバーサルエディターは以下のバージョン 3.0.0 以降のみをサポートするようになりました
  `@Adobe Express/universal-editor-cors` ライブラリ。
   * ライブラリは、[`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js) を介してのみ配信されるようになりました。
   * 古いバージョンの CORS ライブラリを使用するページを開くと、非推奨（廃止予定）の通知が表示され、更新を促されます。
* **ランディングページの拡張ポイント** - [ ユニバーサルエディターのランディングページのサイドパネルに表示される拡張機能の新しい拡張ポイント ](/help/implementing/universal-editor/customizing.md#extending) が導入されました。
   * 開発者は、拡張機能をエディター、ランディングページまたはその両方に適用できるかどうかを指定できるようになり、カスタマイズと操作性が向上しました。

## その他の改善点 {#other-improvements}

* **ランディングページの最近の項目で無効な URL を修正しました** - ユニバーサルエディターのランディングページの「最近」リストに表示される URL が壊れる問題が解決されました。
* **統合シェルでのテーマの同期** - ユニバーサルエディターは、テーマをシステムの統合シェル設定と動的に同期し、明暗モードを自動的に調整するようになりました。
   * これにより、フラグメントセレクターやアセットセレクターなど、マイクロフロントエンド全体で一貫した視覚的な外観が確保されます。
