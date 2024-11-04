---
title: ユニバーサルエディター 2024.09.3 リリースノート
description: ユニバーサルエディターの 2024.09.3 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b70acef8dc259fff3041617abe0a89f7eb73dfab
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# ユニバーサルエディター 2024.09.3 リリースノート {#release-notes}

ユニバーサルエディターの 2024 年 9 月 3 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Serviceの最新のリリースノートについては、[ このページ ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## 新機能 {#what-is-new}

* **`rootPath`がコンテンツ選択で使用できるようになりました**:[AEM コンテンツ、](/help/implementing/universal-editor/field-types.md#aem-content)[ コンテンツフラグメント、](/help/implementing/universal-editor/field-types.md#content-fragment) および [ エクスペリエンスフラグメント ](/help/implementing/universal-editor/field-types.md#experience-fragment) フィールドタイプを使用する際に、ターゲット設定されたコンテンツ選択をユーザーに表示する `rootPath` をコンテンツ選択で提供できるようになりました。
   * これにより、コンテンツの選択は、指定されたパス内のコンテンツおよび任意のサブディレクトリに限定される。

## 6.5 のサポートのための早期導入プログラム {#early-adoption}

ユニバーサルエディターが、早期導入プログラムの一環としてAEM 6.5 を使用する際のヘッドレスユースケースで利用できるようになりました。

この新機能のテストやフィードバックの提供に関心がある場合は、Adobe IDに関連付けられたメールアドレスからAdobe担当者にメールを送信してください。

## バグ修正 {#bug-fixes}

* **クロスコンテナのドラッグ&amp;ドロップ**:[ ドラッグ&amp;ドロップを使用して異なるコンテナ間でコンポーネントを移動 ](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) では、ソースとターゲットの両方で [ コンポーネントフィルター ](/help/implementing/universal-editor/customizing.md#filtering-components) を順守するようになりました。
