---
title: ページの差分
description: ページの差分表示を使用すると、2 つのページを並べて比較し、差分をハイライト表示できます。
exl-id: 6e5c7f14-c980-48e3-8bdd-a7ec10a9e680
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 79%

---

# ページの差分  {#page-diff}

## はじめに {#introduction}

コンテンツ作成は反復的なプロセスです。効率的なオーサリングでは、ある反復から他の反復で何が変化したかを知る必要があります。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。ある作成者が、現在のページを他のバージョンと並べて簡単に比較できるようにしたいと考えます。

ページの差分表示を使用すると、2 つのページを並べて比較し、差分をハイライト表示できます。

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

それらのコンテキスト内で差分の確認を開始する方法については、それぞれのトピックを参照してください。

### 差分の表示 {#presentation-of-differences}

比較対象のコンテンツに関わらず、差分の表示は同じです。

* 差分の確認を開始したときに選択されたコンテンツが左側に表示されます（差分のエントリポイント）。
* 比較対象のコンテンツが右側に表示されます（選択されたコンテンツの比較対象となるもの）。

例えば、バージョンを比較する場合、現在のバージョンが左側に、以前のバージョンが右側に表示されます。

両方のページのソースは、ブラウザーウィンドウ上部のヘッダーバーにはっきりと表示されます。

![バージョンの並列表示](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差分によりコンポーネントおよび HTML レベルの変更が検出されます。変更された項目は、異なる色でハイライト表示されます。

**コンポーネントの変更点**

* ライトグリーン - 追加されたコンポーネント
* ピンク - 削除されたコンポーネント

**HTML の変更点**

* ダークグリーン - 追加された HTML
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

ページの差分表示で期待どおりに差分が検出されない場合があります。

* バージョンおよびローンチが異なるとき、差分は、パンくずリスト、メニュー、製品リスト、ロゴなどのダイナミックコンポーネント（コンテンツを表示する際にサイト構造に依存するコンポーネント）を考慮しません。
* バージョンの差分表示では、アクセスコントロールポリシーおよびライブコピー関係は再現されません。
* ページを移動すると、移動前に作成したバージョンとの差分を実行できなくなります。
   * 差分で問題が発生した場合は、ページの[タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)を調べて、ページを移動したかどうかを確認します。

>[!NOTE]
>
>バージョンを互いに比較することはできません。 比較できるのは、現在のバージョンと古いバージョンの組み合わせだけです。変更の強調表示は、必ず現在のバージョンに対しておこなわれます。

>[!NOTE]
>
>ページの差分操作の仕組みと、ページの差分に影響を与える可能性のある制限について詳しくは、 [開発者向けドキュメント](/help/implementing/developing/introduction/page-diff.md) を参照してください。
