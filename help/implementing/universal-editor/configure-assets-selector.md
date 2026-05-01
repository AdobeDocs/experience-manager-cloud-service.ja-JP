---
title: ユニバーサルエディター用のAssets セレクターの設定
description: ユニバーサルエディターで使用するアセットセレクターの設定方法について説明します。
feature: Developing
role: Admin, Developer
exl-id: 0bf7b418-5ecd-454f-ac46-03792268c59c
source-git-commit: a03eb72ee1b46756f003a60709019aa3122d26f2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# ユニバーサルエディター用のAssets セレクターの設定 {#configure-assets-selector}

ユニバーサルエディターで使用するアセットセレクターの設定方法について説明します。

## 概要 {#overview}

ユニバーサルエディターでは、アセットセレクターを使用して、作成者がコンテンツに挿入するアセットを参照および選択できるようにします。

アセットセレクターは、[ コンポーネントフィルター](/help/implementing/universal-editor/filtering.md)を使用して、ユニバーサルエディター内で設定できます。 このドキュメントでは、使用可能な設定オプションについて説明します。

>[!NOTE]
>
>ユニバーサルエディタープロジェクトを開始する際に、アセットセレクターのフィルターが配置されていません。 作成者は、ユーザー権限で通常は許可されているすべてのアセットにアクセスできます。

## フィルター定義 {#filter-definition}

アセットセレクターのフィルター定義はシンプルな構造です。

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## フィルターオプション {#filter-options}

`assets` フィルターには、次のオプションを指定できます。

* `deliveryTier?`: – 使用する配信階層を定義します。
   * `dm`：必要に応じて`publish`にフォールバックするDynamic Media （推奨）
   * `publish`: AEM パブリッシュインスタンス
* `repoNames?`：文字列 – イメージの選択に使用できるAEM リポジトリのリスト。
   * デフォルト：すべての配信リポジトリ
* `selectionTier?`：文字列 – アセットを選択するAEM層
   * デフォルト：`["author", "delivery"]`
* `disableRemote?`: ブール値 – リモートリポジトリサポートを無効にする
* `preselectedTypes?`：文字列 – アセットセレクターでデフォルトのフィルターとして適用される、事前に選択されたファイルタイプ
* `minMaxDimensions?`: オブジェクト – アセットセレクターでデフォルトフィルターとして適用される最小および/または最大ディメンション（ピクセル単位）を提供します
   * `widthMin?`：数値 – 最小幅
   * `widthMax?`：数値 – 最大幅
   * `heightMin?`：数値 – 最小高さ
   * `heightMax?`：数値 – 最大高さ
* `minMaxFileSize?`: オブジェクト – アセットセレクターでデフォルトフィルターとして適用する最小および/または最大ファイルサイズ（バイト単位）を指定します
   * `min?`：数値 – 最小ファイルサイズ
   * `max?`：数値 – 最大ファイルサイズ
* `customFileTypeFilters?`: オブジェクト – アセットセレクターに表示するカスタムファイルタイプフィルターを提供します
   * `label`：文字列 – アセット選択UIに表示されるラベル
   * `value`：文字列 – フィルタリングするファイルタイプの値
* `displayFilters?`: ブール値 – アセットセレクターでフィルターUIを無効にするために使用されます。デフォルトではtrue

## 例 {#example}

次の例には、イラスト用のほとんどのオプションが含まれています。

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

<!--

## Additional Resources {#additional-resources}

For details on the assets selector, please see the document [Micro-Frontend Asset Selector](/help/assets/overview-asset-selector.md#using-asset-selector) in the assets documentation.

-->
