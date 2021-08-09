---
title: ページ注釈の追加
description: 注釈モードを使用して、注釈やスケッチをページに残し、コンテンツレビュープロセスを支援するノート注釈を使用する場合と同じようにします
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: feee00bf5adae0821fe770c8882641994cee2dbf
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 35%

---

# ページ注釈の追加 {#adding-page-annotations}

デジタルエクスペリエンス向けにコンテンツを作成するには、多くの場合、公開前にディスカッションとフィードバックが必要です。 このフィードバックプロセスを支援するために、AEMではコンテンツに注釈を追加できます。

注釈を付けると、単純なスケッチやメモ（実際の付箋）がページに配置されます。 注釈を使用すると、他の作成者やレビュー担当者に対してコメントや質問を残すことができます。

>[!TIP]
>
>ページでフィードバックを提供するために、[コメント](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)も使用できます。

注釈の作成と表示には、特別な[モード](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)が使用されます。

>[!TIP]
>
>要件に応じて、注釈が追加、更新または削除されたときに通知を送信する[ワークフロー](/help/sites-cloud/authoring/workflows/overview.md)を開発することもできます。

## 注釈インジケーター {#annotation-indicator}

注釈は編集モードでは表示されませんが、ツールバーの右上にあるバッジに、現在のページに存在する注釈の数が示されます。このバッジは、デフォルトの注釈アイコンに代わるものですが、注釈モードと切り替えるクイックリンクとしても動作します。

![注釈インジケーター](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## 注釈モード {#annotate-mode}

注釈は、注釈モードでのみ表示されます。

1. ページの編集時に、ツールバー（右上）のアイコンを使用して注釈モードに入ります。

   ![注釈ボタン](/help/sites-cloud/authoring/assets/annotations.png)

   既存の注釈を表示できるようになりました。

   ![注釈の例](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 注釈をクリックまたはタップして注釈ダイアログを開き、詳細を表示します。

   ![注釈の詳細](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. 注釈モードを終了して以前に使用したモードに戻るには、上部のツールバーの右側にある「x」ボタンをタップまたはクリックします。

## 注釈の追加と編集 {#annotating-a-component}

注釈モードでは、注釈の表示に加えて、コンテンツに対する注釈の作成、編集、移動または削除をおこなうことができます

1. [ページで注釈](#annotate-mode) モードを開始します。

1. 注釈の追加を開始するには、注釈を追加アイコン（ツールバーの左側にあるプラス記号）をクリックまたはタップします。

1. 必要なコンポーネント（注釈を付けることができるコンポーネントは、青い境界線でハイライト表示されます）をクリックまたはタップして注釈を追加し、ダイアログを開きます。

   ![注釈の追加](/help/sites-cloud/authoring/assets/annotation-adding.png)

   このダイアログで適切なフィールドやアイコンを使用し、次の操作を実行できます。

   * 注釈テキストを入力します。
   * スケッチ（線と図形）を作成して、コンポーネントの特定の領域を強調表示します。

      ![注釈のスケッチボタン](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      スケッチの作成中は、カーソルが十字型に変わります。複数の異なる線を描くことができます。スケッチ線は注釈と同じ色で、矢印、円、楕円のいずれかにすることができます。

   * 色を選択または変更します。

      ![注釈のカラースウォッチボタン](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. ダイアログの外側をクリックまたはタップして、注釈ダイアログを閉じることができます。 注釈の一部がスケッチと共に表示されます。

   ![注釈のスケッチ](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. 特定の注釈の編集が完了した後は、次の操作を実行できます。

   * テキストマーカーをクリックまたはタップして注釈を開きます。 開いたら、全文を表示したり、変更を加えたり、[注釈を削除したりできます。](#deleting-annotations)
   * テキストマーカーの位置を変更します。
   * スケッチ線をクリックまたはタップしてそのスケッチを選択し、目的の位置までドラッグします。
   * コンポーネントの移動またはコピー
      * 関連する注釈とスケッチも移動またはコピーされますが、段落に対する位置は変わりません。


>[!NOTE]
>
>別のユーザーによってロックされているページには、注釈を追加できません。

>[!NOTE]
>
>個々のコンポーネントの種類の定義によって、そのコンポーネントのインスタンスに注釈を追加できるかどうかが決まります。

## 注釈とスケッチの削除 {#deleting-annotations}

注釈と関連するスケッチは削除できます。

1. [ページで注釈](#annotate-mode) モードを開始します。

1. テキストマーカーをクリックまたはタップして注釈を開きます。

1. 「削除」アイコンをクリックまたはタップします。

   ![注釈を削除](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. 注釈と関連するスケッチがすべて削除されます。

>[!NOTE]
>
>コンポーネントを削除すると、そのリソースに添付された注釈およびスケッチが、ページ全体での位置に関係なく、すべて削除されます。

## スケッチのみを削除する {#deleting-sketches}

関連付けられたスケッチを含む注釈全体ではなく、特定のスケッチのみを削除できます。

1. [ページで注釈](#annotate-mode) モードを開始します。

1. スケッチをクリックまたはタップします。 AEMでは、暗い青いボックスでハイライト表示されます。

   ![削除するスケッチを選択](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. キーボードのDeleteキーを押します。

1. スケッチは削除されますが、注釈は残ります。

## その他のリソースへの注釈の追加 {#annotating-other-resources}

コンポーネント以外にも、様々なリソースに注釈を付けることができます。

* アセットへの注釈の追加[アセットへの注釈の追加](/help/assets/manage-digital-assets.md#annotating)
* ビデオアセットへの注釈の追加[ビデオアセットへの注釈の追加](/help/assets/manage-video-assets.md#annotate-video-assets)
