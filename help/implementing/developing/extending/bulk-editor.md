---
title: ページプロパティの一括編集の設定
description: 複数のページのプロパティを一度に編集できるように一括編集を設定する方法を説明します。
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 13%

---


# ページプロパティの一括編集の設定 {#configuring-bulk-editing-of-page-properties}

[ページプロパティの一括編集](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) を使用すると、複数のページのプロパティを一度に編集できます。

## 検討事項 {#considerations}

ページプロパティは、デフォルトでは一括編集が有効になっていません。 明示的に有効にする必要があります。 一括編集で使用できるようにページプロパティを定義する場合は、次のような特定の影響を考慮する必要があります。

* 通常、一部のフィールドは一意です。1 つの値が適用される場合に、そのようなフィールドを一括編集用に有効にしても意味があるかどうかを決定する必要があります。
   * 例えば、ページタイトルはほとんど常に一意です。
* 特定のフィールドには、レンダリング時に意味のある表現が必要な複数の値が含まれる場合があります。
   * 例えば、ラベルの付いたステータスドロップダウン **公開準備完了**. 一括編集の前に、次のような複数の値が含まれる場合があります。 **準備完了**, **レビュー中**, **進行中**&#x200B;など

複数の値が存在する可能性があるので、次のフィールドタイプのみを一括編集で有効にすることをお勧めします。

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## フィールドの有効化 {#enabling-a-field}

以下の手順では、 `/apps/core/wcm/components/page/v1/page` から [WKND サンプルコンテンツ](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 開発環境のフィールドで一括編集を有効にする例を示します。

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
* 同じリソースタイプを持つページでのみ使用できます。
