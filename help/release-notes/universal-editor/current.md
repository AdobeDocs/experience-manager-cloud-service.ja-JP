---
title: ユニバーサルエディター 2024.12.02 リリースノート
description: ユニバーサルエディターの 2024.12.02 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 16%

---


# ユニバーサルエディター 2024.12.02 リリースノート {#release-notes}

ユニバーサルエディターの 2024 年 12 月 2 日（PT）リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* **コンテンツツリーのキーボードナビゲーション**:[ サイドパネルで使用できるコンテンツツリー ](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) に、キーボードから完全にアクセスできるようになりました。
   * 作成者は、アクセシビリティのために [WCAG 2.1 ガイドライン ](/help/sites-cloud/authoring/page-editor/accessible-content.md) に準拠した標準のキーボードコントロールを使用して、ツリービュー項目を移動および操作できます。
   * この機能強化により、ツリー内のすべてのインタラクティブ要素がキーボードで操作できるようになり、キーボードナビゲーションに依存するユーザーの操作性が向上します。
* **編集可能の選択解除**：作成者は、ページ上で以前に選択した編集可能な要素を選択解除できるようになりました。
   * これにより、作成者がアクティブな選択範囲の境界線なしでページを表示する場合に妨げとなるのを防ぐことができます。
* **フラグメントセレクター**:AEM as a Cloud Service インスタンスで、フラグメント参照によってフラグメントセレクターがコンテンツピッカーとして開かれるようになり、許可されたコンテンツフラグメントモデルへの準拠、コンテンツフラグメントの検索、全体的なエクスペリエンスの向上など、機能が向上しています。
   * これにより、他のAdobeUI と連携し、一貫性が向上します。
   * [AEM 6.5 環境の場合 ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)、既存のコンテンツピッカーは引き続き使用されます。
* **コンテナの説明**:[ プロパティパネル ](/help/implementing/universal-editor/field-types.md#container) でコンテンツを参照するために使用される [ コンテナコンポーネント ](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail) で、コンテナフィールドの上に表示される説明属性がサポートされるようになりました。
   * この追加により、作成者に編集中のグループ化フィールドに関するコンテキストが提供されるため、明確さが向上します。

## その他の改善点 {#other-improvements}

* **リッチテキストフィールドの同期**：プロパティパネルのリッチテキストフィールド内で生のコンテンツとレンダリングされたコンテンツの同期を改善し、リッチテキストコンテンツとレンダリングされた表現が異なる可能性があるEdge Delivery Servicesプロジェクト内の問題を解決しました。
* **編集モードイベント**：リモートアプリを再読み込みした後も含め、ユニバーサルエディターが編集モードイベントを確実に発行するようになりました。
