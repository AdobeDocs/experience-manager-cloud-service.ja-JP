---
title: ページの差分
description: ページの差分機能を使用すると、2 つのページを並べて比較し、違いを強調表示するのに便利です。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 38%

---

# ページの差分  {#page-diff}

## はじめに {#introduction}

コンテンツの作成は反復的なプロセスです。 効率的にオーサリングを行うには、何がイテレーションから別のイテレーションに変わったかを確認できる必要があります。 あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページを他のバージョンと並べて簡単に比較できるようにしたいと考えています。

ページの差分機能を使用すると、2 つのページを並べて比較し、違いを強調表示するのに便利です。

>[!NOTE]
>
>ユーザーは、 **変更/作成/削除** ノードに対する権限 `/content/versionhistory` 」をクリックして機能を使用します。
>
>この機能の技術的詳細については、[開発とページの差分](/help/implementing/developing/introduction/page-diff.md#operation-details)を参照してください。

## 使用方法 {#use}

並列比較による差分表示では、次のものを比較できます。

* [バージョン](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) - ページの以前のバージョンとその現在の状態
* [ライブコピー](/help/sites-cloud/administering/msm/creating-live-copies.md#comparing-a-live-copy-page-with-a-blueprint-page) - ライブコピーとそのブループリント
* [ローンチ](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) - ローンチとそのソース
* [言語コピー](/help/sites-cloud/administering/translation/managing-projects.md#comparing-language-copies) - （再）翻訳前と（再）翻訳後のページ

これらのコンテキスト内で差分を開始する方法については、それぞれのトピックを参照してください。

### 差異の表示 {#presentation-of-differences}

比較するコンテンツに関係なく、差分の表示は同じです。

* 差分を開始したときに選択したコンテンツが左側（差分エントリポイント）に表示されます。
* 比較対象のコンテンツが右側に表示されます（選択したコンテンツとの比較対象）。

例えば、バージョンを比較する場合、現在のバージョンが左側に、以前のバージョンが右側に表示されます。

両方のページのソースは、ブラウザーウィンドウ上部のヘッダーバーにはっきりと表示されます。

![バージョンの並列表示](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差分表示では、コンポーネントおよびHTMLレベルでの変更が検出されます。 変更された項目は、異なる色でハイライト表示されます。

**コンポーネントの変更**

* ライトグリーン — 追加されたコンポーネント
* ピンク — 削除されたコンポーネント

**HTMLの変更**

* ダークグリーン —HTML追加
* 赤 - 削除された HTML

>[!NOTE]
>
>言語コピーを比較する場合は、翻訳ですべてが変更され、強調表示をしても意味がないので、強調表示は無効になります。

### 全画面表示および終了 {#fullscreen-and-exiting}

特定のコンテンツに焦点を当てるには、並列比較による差分表示の「側」の全画面表示アイコンをクリックして、それをフルブラウザーウィンドウに拡大します。

![全画面表示ボタン](/help/sites-cloud/authoring/assets/versions-full-screen.png)

選択された側がウィンドウ全体に表示されますが、バーは上部に残るので、2 枚のページを切り替えることができます。

![全画面表示モード](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>全画面表示で両方のページ名がブラウザーの幅に収まらない場合は、表示中のページの名前のみが表示され、もう一方のページは省略記号の後ろに表示されます。

また全画面表示終了アイコンをクリックして、全画面表示を閉じることができます。

![全画面モードを終了](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

ヘッダーの「閉じる」ボタンをクリックすることで、並列比較による差分表示はいつでも終了することができます。

## 制限事項 {#limitations}

ページの差分によって、期待どおりに違いが検出されない場合があります。

* バージョンと起動を異なる場合、差分では、パンくずリスト、メニュー、製品リスト、ロゴ（コンテンツのレンダリングにサイト構造に依存するコンポーネント）などの動的コンポーネントは考慮されません。
* バージョンの差分表示では、アクセスコントロールポリシーおよびライブコピー関係は再現されません。
* ページを移動すると、移動前におこなわれたバージョンとの差分表示を実行できなくなります。
   * 差分に関する問題が発生した場合は、 [タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) ページが移動されたかどうかを確認するために使用します。

>[!NOTE]
>
>古いバージョン同士を比較することはできません。比較できるのは、現在のバージョンと古いバージョンの組み合わせだけです。変更の強調表示は、必ず現在のバージョンに対しておこなわれます。

>[!NOTE]
>
>ページの差分操作の仕組みと、ページの差分に影響を与える可能性のある制限について詳しくは、 [開発者向けドキュメント](/help/implementing/developing/introduction/page-diff.md) を参照してください。
