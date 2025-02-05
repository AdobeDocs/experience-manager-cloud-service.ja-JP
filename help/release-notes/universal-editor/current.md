---
title: ユニバーサルエディター 2054.01.16 リリースノート
description: ユニバーサルエディターの 2025.01.16 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 77%

---


# ユニバーサルエディター 2025.01.16 リリースノート {#release-notes}

ユニバーサルエディターの 2025年1月16日（PT）リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Serviceの最新のリリースノートについては、[ このページ ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## 新機能 {#what-is-new}

* **3.0.0 より前の CORS ライブラリの廃止** - 今後の互換性を確保し、セキュリティを強化するために、ユニバーサルエディターはバージョン 3.0.0 以降の
  `@Adobe Express/universal-editor-cors` ライブラリのみをサポートするようになりました。
   * ライブラリは、現在は [`universal-editor-service.adobe.io/cors.js`](http://universal-editor-service.adobe.io/cors.js) のみを介して配信されます。
   * 古いバージョンの CORS ライブラリを使用するページを開くと、ユーザーに廃止のお知らせが表示され、更新を促されます。
* **ランディングページの拡張機能ポイント** - ユニバーサルエディターのランディングページのサイドパネルに、拡張機能を表示するための[新しい拡張機能ポイント](/help/implementing/universal-editor/customizing.md#extending)が導入されました。
   * 開発者は、拡張機能をエディター、ランディングページ、またはその両方に適用するかどうかを指定できるようになり、カスタマイズと使いやすさが向上しました。

## その他の改善点 {#other-improvements}

* **ランディングページの最近の項目で無効な URL を修正しました** - ユニバーサルエディターのランディングページの「最近」リストに表示される URL が壊れる問題が解決されました。
* **統合シェルでのテーマの同期** - ユニバーサルエディターは、テーマをシステムの統合シェル設定と動的に同期し、ライトモードとダークモードを自動的に調整するようになりました。
   * これにより、フラグメントやアセットセレクターを含むマイクロフロントエンド全体で、一貫した外観が確保されます。
