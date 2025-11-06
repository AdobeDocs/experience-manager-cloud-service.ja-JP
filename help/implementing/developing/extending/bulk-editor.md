---
title: ページプロパティの一括編集の設定
description: 複数のページのプロパティを一度に編集できるように一括編集を設定する方法を説明します。
exl-id: 0d10c6b9-8643-479d-adc1-4066d227e83d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 100%

---

# ページプロパティの一括編集の設定 {#configuring-bulk-editing-of-page-properties}

[ページプロパティの一括編集](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#from-the-sites-console-multiple-pages)を使用すると、複数のページのプロパティを一度に編集できます。

## 検討事項 {#considerations}

ページプロパティは、デフォルトでは一括編集が有効になっていません。明示的に有効にする必要があります。一括編集できるようにページプロパティを定義する場合は、次のような避けられない影響を考慮する必要があります。

* 通常は一意なフィールドがあります。1 つの値を適用した場合に、そのようなフィールドの一括編集を有効にして意味があるかどうかを判断する必要があります。
   * 例えば、ページタイトルはほとんど常に一意です。
* 特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。
   * 例えば、**公開準備完了**&#x200B;とラベルが付けられたステータスドロップダウンがあります。これには、一括編集の前にいくつかの値を持つ場合があります（例：**準備完了**、**レビュー中**、**処理中**）。

複数の値が存在する可能性があるので、次のフィールドタイプのみを一括編集で有効にすることをお勧めします。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## フィールドの有効化 {#enabling-a-field}

これらの手順は、開発環境のフィールドで一括編集を有効にする例として、`/apps/core/wcm/components/page/v1/page` から [WKND サンプルコンテンツ](/help/implementing/developing/introduction/develop-wknd-tutorial.md)を使用します。

1. CRXDE を使用して、ページコンポーネントを開きます。
1. `cq:dialog` 定義内の必要なフィールドに移動します。
1. フィールドノードで次のプロパティを定義します。

   * **名前**：`allowBulkEdit`
   * **型**：`Boolean`
   * **値**：`true`

1. 「**すべて保存**」を選択して更新内容を保持します。

## 制限事項 {#limitations}

ページプロパティの一括編集には次の特徴があります。

* ライブコピー内のページでは使用できません。
* リソースタイプが同じページでのみ使用できます。
