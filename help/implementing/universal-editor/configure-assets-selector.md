---
title: ユニバーサルエディター用のAssets セレクターの設定
description: ユニバーサルエディターで使用するアセットセレクターの設定方法を説明します。
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# ユニバーサルエディター用のAssets セレクターの設定 {#configure-assets-selector}

ユニバーサルエディターで使用するアセットセレクターの設定方法を説明します。

## 概要 {#overview}

ユニバーサルエディターでは [&#x200B; アセットセレクター &#x200B;](/help/assets/overview-asset-selector.md#using-asset-selector) を使用して、作成者がコンテンツに挿入するアセットを参照して選択できるようにします。

アセットセレクターは、ユニバーサルエディター内で [&#x200B; コンポーネントフィルターを使用して設定できます。](/help/implementing/universal-editor/filtering.md) このドキュメントでは、使用可能な設定オプションについて説明します。

>[!NOTE]
>
>ユニバーサルエディタープロジェクトを開始する場合、アセットセレクターのフィルターは設定されません。 作成者は、ユーザー権限で通常許可されるすべてのアセットにアクセスできます。

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

`assets` フィルターには、次のオプションを含めることができます。

* `deliveryTier?`: – 使用する配信層を次の中から定義します。
   * `dm`:Dynamic Media （推奨）（必要に応じて `publish` へのフォールバックを使用）
   * `publish`:AEM パブリッシュインスタンス
* `repoNames?`：文字列 – 画像の選択に使用できるAEM リポジトリのリスト。
   * デフォルト：すべての配信リポジトリ
* `selectionTier?`：文字列 – アセットを選択するAEM層
   * デフォルト：`["author", "delivery"]`
* `disableRemote?`：ブール値 – リモートリポジトリのサポートを無効にします
* `preselectedTypes?`：文字列 – アセットセレクターでデフォルトのフィルターとして適用される、事前に選択されたファイルタイプ
* `minMaxDimensions?`: オブジェクト – アセットセレクターでデフォルトフィルターとして適用する最小サイズと最大サイズ（ピクセル単位）を指定します
   * `widthMin?`：数値 – 最小幅
   * `widthMax?`：数値 – 最大幅
   * `heightMin?`：数値 – 最小の高さ
   * `heightMax?`：数値 – 最大の高さ
* `minMaxFileSize?`: オブジェクト – アセットセレクターでデフォルトフィルターとして適用する最小または最大ファイルサイズ（バイト単位）を指定します
   * `min?`：数値 – 最小ファイルサイズ
   * `max?`: number – 最大ファイルサイズ
* `customFileTypeFilters?`: オブジェクト – アセットセレクターに表示されるカスタムファイルタイプフィルターを提供します
   * `label`:String - アセット選択 UI に表示されるラベル
   * `value`：文字列 – フィルターするファイルタイプの値
* `displayFilters?`：ブール値 – アセットセレクターでフィルター UI を無効にするために使用されます。デフォルトでは true です

## 例 {#example}

次の例には、説明用のほとんどのオプションが含まれています。

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

## その他のリソース {#additional-resources}

アセットセレクターについて詳しくは、アセットドキュメントの [&#x200B; マイクロフロントエンドアセットセレクター &#x200B;](/help/assets/overview-asset-selector.md#using-asset-selector) のドキュメントを参照してください。
