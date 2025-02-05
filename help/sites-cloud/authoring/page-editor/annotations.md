---
title: ページ注釈の追加
description: コンテンツレビュープロセスを支援するために、付箋と同様に、注釈モードを使用して注釈やスケッチをページに残します
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 97%

---

# ページ注釈の追加 {#adding-page-annotations}

デジタルエクスペリエンス向けにコンテンツを作成するには、多くの場合、公開前にディスカッションとフィードバックが必要です。このフィードバックプロセスを容易にするために、AEM ではコンテンツに注釈を追加できます。

注釈では、単純なスケッチやメモ（付箋のようなものです）がページに配置されます。注釈を使用すると、他の作成者やレビュー担当者に対してコメントや質問を残すことができます。

>[!TIP]
>
>ページでフィードバックを提供するために、[コメント](/help/sites-cloud/authoring/basic-handling.md#timeline)も使用できます。

注釈の作成と表示には、特別な[モード](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)が使用されます。

>[!TIP]
>
>必要に応じて、注釈が追加、更新、削除されたときに通知を送信する[ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)を開発することもできます。

## 注釈インジケーター {#annotation-indicator}

注釈は編集モードでは表示されませんが、ツールバーの右上にあるバッジに、現在のページに存在する注釈の数が示されます。このバッジは、デフォルトの注釈アイコンに代わるものですが、注釈モードと切り替えるクイックリンクとしても動作します。

![注釈インジケーター](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注釈モード {#annotate-mode}

注釈は、注釈モードでのみ表示されます。

1. 注釈モードは、ページの編集中にツールバー（右上）のアイコンを使用して開始できます。

   ![注釈ボタン](/help/sites-cloud/authoring/assets/annotations.png)

   既存の注釈を表示できるようになりました。

   ![注釈の例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 注釈を選択して「注釈」ダイアログを開き、詳細を表示します。

   ![注釈の詳細](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. 「注釈」モードを終了して前のモードに戻るには、上部のツールバーの右側にある「x」ボタンを選択します。

## 注釈の追加と編集 {#annotating-a-component}

「注釈」モードでは注釈の表示に加えて、コンテンツに対する注釈の作成、編集、移動、削除を行うことができます

1. ページで[注釈モードを開始](#annotate-mode)します。

1. 注釈を追加するには、注釈の追加アイコン（ツールバーの左側にあるプラス記号）を選択します。

1. 注釈を追加するために必要なコンポーネント（注釈を追加できるコンポーネントは青い境界線で強調表示されます）を選択して、ダイアログを開きます。

   ![注釈の追加](/help/sites-cloud/authoring/assets/annotation-adding.png)

   このダイアログで適切なフィールドやアイコンを使用し、次の操作を実行できます。

   * 注釈テキストを入力します。
   * スケッチ（線と図形）を作成して、コンポーネントの特定の領域を強調表示します。

     ![注釈のスケッチボタン](/help/sites-cloud/authoring/assets/annotation-sketch.png)

     スケッチの作成中は、カーソルが十字型に変わります。複数の異なる線を描くことができます。スケッチ線は注釈と同じ色で、矢印、円、楕円のいずれかにすることができます。

   * 色を選択または変更します。

     ![注釈のカラースウォッチボタン](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. ダイアログの外側をクリックまたはタップして、注釈ダイアログを閉じることができます。注釈の一部の表示とスケッチが一緒に表示されます。

   ![注釈のスケッチ](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 特定の注釈の編集が完了した後は、次の操作を実行できます。

   * テキストマーカーを選択して注釈を開きます。注釈が開いたら、テキスト全体を表示して、注釈に変更を加えたり [ 削除 ](#deleting-annotations) することができます。
   * テキストマーカーの位置を変更します。
   * スケッチ線を選択してそのスケッチを選択し、必要な位置までドラッグします。
   * コンポーネントの移動またはコピー
      * 関連する注釈およびスケッチも移動またはコピーされますが、段落に対する位置は変わりません。


>[!NOTE]
>
>別のユーザーによってロックされているページには、注釈を追加できません。

>[!NOTE]
>
>個々のコンポーネントの種類の定義によって、そのコンポーネントのインスタンスに注釈を追加できるかどうかが決まります。

## 注釈とスケッチの削除 {#deleting-annotations}

注釈と関連するスケッチは削除できます。

1. ページで[注釈モードを開始](#annotate-mode)します。

1. テキストマーカーを選択して注釈を開きます。

1. 削除アイコンを選択します。

   ![注釈を削除](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 注釈と関連するスケッチがすべて削除されます。

>[!NOTE]
>
>コンポーネントを削除すると、そのリソースに添付されていた注釈およびスケッチが、ページ全体での位置に関係なく、すべて削除されます。

## スケッチのみを削除 {#deleting-sketches}

関連付けられたスケッチを含む注釈全体ではなく、特定のスケッチのみを削除できます。

1. ページで[注釈モードを開始](#annotate-mode)します。

1. スケッチを選択します。スケッチが紺色のボックスでハイライトされます。

   ![削除するスケッチを選択](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. キーボードの Delete キーを押します。

1. スケッチは削除されますが、注釈は残ります。

## その他のリソースへの注釈の追加 {#annotating-other-resources}

コンポーネント以外にも、様々なリソースに注釈を付けることができます。

* アセットへの注釈の追加[アセットへの注釈の追加](/help/assets/manage-digital-assets.md#annotating)
* ビデオアセットへの注釈の追加[ビデオアセットへの注釈の追加](/help/assets/manage-video-assets.md#annotate-video-assets)
