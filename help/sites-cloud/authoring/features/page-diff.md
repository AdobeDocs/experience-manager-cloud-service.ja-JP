---
title: ページの差分
description: ページの差分表示を使用すると、2 つのページを並べて比較し、差分を強調表示できます。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# ページの差分 {#page-diff}

## 概要 {#introduction}

コンテンツの作成は反復的なプロセスです。効率的にオーサリングをおこなうには、反復するごとに何が変更されたかがわかるようにする必要があります。あるページのバージョンを見てから他のページを見るのは非効率的でありミスが発生する可能性も高くなります。作成者は、現在のページを他のバージョンと並べて簡単に比較したいと考えます。

ページの差分表示を使用すると、2 つのページを並べて比較し、差分を強調表示できます。

>[!CAUTION]
>
>The user must have the **Modify/Create/Delete** permission on the node `/content/versionhistory` in order to use the feature.
>
>この機能の技術的詳細については、開発とページの差分を参照してください。<!-- See [Developing and Page Diff](/help/sites-developing/pagediff.md#operation-details) for more technical details on this feature.-->

## 使用方法 {#use}

並列比較による差分表示では、次のものを比較できます。

* [バージョン](/help/sites-cloud/authoring/features/page-versions.md#comparing-a-version-with-current-page) — 現在の状態を持つページの以前のバージョン
* Live Copies - Live Copy with its Blueprint <!-- [Live Copies](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - Live Copy with its Blueprint-->
* [起動回数](/help/sites-cloud/authoring/launches/editing.md#comparing-a-launch-page-to-its-source-page) — ソースで起動
* Language Copies - A page before and after (re-)translation <!-- [Language Copies](/help/sites-administering/tc-manage.md#comparing-language-copies) - A page before and after (re-)translation-->

それらのコンテキスト内で差分の確認を開始する方法については、それぞれのトピックを参照してください。

### 差分の表示 {#presentation-of-differences}

比較対象のコンテンツにかかわらず、差分の表示は同じです。

* 差分の確認を開始したときに選択されたコンテンツが左側に表示されます（差分のエントリポイント）。
* 比較対象のコンテンツが右側に表示されます（選択されたコンテンツの比較対象となるもの）。

例えば、バージョンを比較する場合、現在のバージョンが左側に表示され、以前のバージョンが右側に表示されます。

両方のページのソースは、ブラウザーウィンドウ上部のヘッダーバーに明瞭に表示されます。

![バージョンを並べて表示](/help/sites-cloud/authoring/assets/versions-side-by-side.png)

差分によりコンポーネントおよび HTML レベルの変更が検出されます。変更された項目は、異なる色で強調表示されます。

**変更の比較**

* ライトグリーン - 追加されたコンポーネント
* ピンク - 削除されたコンポーネント
* 青 - 変更されたコンポーネント
* 青 - 移動されたコンポーネント

変更されたものの色と移動されたものの色は同じです。

**HTML の変更**

* ダークグリーン - 追加された HTML
* 赤 — HTML削除

>[!NOTE]
>
>言語コピーを比較する場合は、翻訳ですべてが変更され、強調表示をしても意味がないため、強調表示は無効になります。

### フルスクリーンおよび終了 {#fullscreen-and-exiting}

特定のコンテンツに集中するために、並列比較による差分表示のいずれかの「側」の全画面表示アイコンをクリックして、それをフルブラウザーウィンドウに拡大することができます。

![フルスクリーンボタン](/help/sites-cloud/authoring/assets/versions-full-screen.png)

選択された側がウィンドウ全体に表示されますが、バーは上部に残るため、2 枚のページを切り替えることができます。

![フルスクリーンモード](/help/sites-cloud/authoring/assets/versions-full-screen-mode.png)

>[!NOTE]
>
>ブラウザーの幅で両方のページ名をフルスクリーン表示で表示できない場合は、表示中のページの名前のみが表示され、省略記号の後ろに他方のページが表示されます。

またフルスクリーン終了アイコンをクリックして、全画面表示を閉じることができます。

![全画面モードを終了](/help/sites-cloud/authoring/assets/versions-exit-full-screen.png)

ヘッダーの「閉じる」ボタンをクリックすることで、並列比較による差分表示はいつでも終了することができます。

## 制限事項 {#limitations}

ページの差分表示で期待どおりに差分が検出されない場合があります。

* バージョンおよびローンチが異なるとき、差分は、パンくずリスト、メニュー、製品リスト、ロゴなどのダイナミックコンポーネント（コンテンツを表示する際にサイト構造に依存するコンポーネント）を考慮しません。
* バージョンの差分表示では、アクセスコントロールポリシーおよびライブコピー関係は再現されません。
* alt、title、srcの属性の変更など、イメージに変更が加えられると、変更されたときに青でハイライト表示されます。 ただし、イメージにsrc属性のBase64表現が含まれ、両方のイメージが同じように見える場合でも、src属性が異なるので、diffによってマークされることがあります。
* 差分表示では、画像の回転を検出できません。
* ページを移動すると、移動前に作成したバージョンとの差分を実行できなくなります。
   * 差分で問題が発生した場合は、ページの[タイムライン](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)を調べて、ページを移動したかどうかを確認します。

>[!NOTE]
>
>バージョンは互いに比較できません。現在のバージョンのみ、ページの他のバージョンと比較できます。 必ず変更が強調表示されるのは、現在のバージョンです。

>[!NOTE]
>
>For more details about the operation of the page diff mechanism as well as limitations which can affect page diff, please see the developer documentation of this feature. <!-- For more details about the operation of the page diff mechanism as well as limitations which can affect page diff, please see the [developer documentation](/help/sites-developing/pagediff.md) of this feature.-->
