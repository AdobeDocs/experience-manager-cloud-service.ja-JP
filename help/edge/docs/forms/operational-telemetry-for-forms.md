---
title: AEM Forms as a Cloud Service 向け Edge Delivery Services の運用テレメトリ
description: AEM Forms as a Cloud Service 向け Edge Delivery Services の運用テレメトリは、フォームでのユーザーインタラクションの継続的なトラッキングと分析を行います。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: ht
source-wordcount: '789'
ht-degree: 100%

---

# AEM Forms as a Cloud Service 向け Edge Delivery Services の運用テレメトリ

運用テレメトリを使用すると、訪問者が Adobe Experience Manager（AEM）の web サイトでどのようなインタラクションを行っているかについて、現実的なインサイトを得ることができます。この組み込みツールには、ユーザーの行動を理解し、パフォーマンスの問題を診断し、web サイトの実験の効果を測定するための貴重なデータが用意されています。運用テレメトリは、実際の使用のインタラクションを取り込み、サイトのパフォーマンスをより正確に把握することによって、合成テストよりも優れた性能を発揮します。

ただし、運用テレメトリは訪問者のプライバシーを優先します。サンプリング技術を利用してユーザーの代表的なサブセットからデータを収集し、個人を特定できる情報（PII）が一切取り込まれないようにします。また、運用テレメトリはデータの最小化を念頭に設計されているため、パフォーマンス分析に必須の重要な指標のみを収集します。このアプローチにより、ユーザーの信頼を維持しながら AEM サイトを最適化できます。


## 前提条件

次の URL にアクセスすると、AEM Forms as a Cloud Service の Edge Delivery Services のモニタリングダッシュボードを表示できます。

https://data.aem.live/?ext=forms

![Forms 向け Edge Delivery Service の運用テレメトリログイン画面](/help/edge/assets/rum-login-screen.png)

AEM Forms as a Cloud Service の Edge Delivery のモニタリングダッシュボードにログインするには、以下を入力します。

* **URL**：URL はユーザーのサイトまたはドメインに固有です。ユーザーは、サイトまたはドメインをフィルタリングして、要件に応じてダッシュボードを表示することもできます。

* **ドメインキー**：ユーザーが手動でドメインキーを生成します。フォームのドメインキーを取得するには、アドビ担当者にお問い合わせください。

### AEM Forms as a Cloud Service 向け Edge Delivery Services のモニタリングダッシュボード

ログイン画面に URL とドメインキーを入力すると、AEM Forms as a Cloud Service の Edge Delivery Services のモニタリングダッシュボードにアクセスできます。

AEM Forms as a Cloud Service の Edge Delivery Services のダッシュボードを次の図に示します。

![運用テレメトリ Forms のダッシュボード](/help/edge/assets/rum-forms-dashboard.png)

### Forms のダッシュボードの様々な主要指標 {#different-metrics-operational-telemetry-dashboard-forms}

このダッシュボードでは、訪問者が Adobe Experience Manager（AEM）web サイト上のフォームを操作する方法に関する重要なインサイトを得ることができます。これらの指標を監視することで、改善すべき領域を特定し、ユーザーエクスペリエンスとコンバージョン率を向上させるためにフォームを最適化できます。

* **フォームビュー**：フォームが表示された合計回数を追跡します
* **フォーム送信**：完了した送信の合計数を追跡します

* **最大コンテンツペイント**：URL の読み込み速度を示します。ユーザーが URL をリクエストした時点から、ビューポートに表示される最大のコンテンツ要素をレンダリングするまでに要した時間を示します。この最大のコンテンツ要素となるのは、画像、ビデオまたは実質的なブロックレベルテキスト要素などです。URL 読み込み速度のパフォーマンス評価は、次のように分類されます。
   * **良**：読み込み時間が 2.5 秒以下の場合
   * **可**：読み込み時間が 2.5 秒より長く 4 秒以下の場合
   * **不可**：読み込み時間が 4 秒を超える場合

* **累積レイアウトシフト**：ページの全期間を通じて発生する予期しないレイアウトシフトごとの、個々のレイアウトシフトスコアの合計を測定します。これは、ページのパフォーマンスを特定するうえで非常に重要な役割を果たします。ユーザーがページ要素を操作しようとしているのにページ要素がシフトすると、ユーザーエクスペリエンスの低下につながるからです。このスコアの範囲は、0 から任意の正の数です。0 はシフトがないことを示し、大きい数はページ上により多くのレイアウトシフトがあることを示します。レイアウトシフトスコアの評価に使用されるパフォーマンス指標は、次のように分類されます。

   * **良**：レイアウトシフトスコアが 0.1 以下の場合
   * **可**：レイアウトシフトスコアが 0.1 より大きく 0.25 以下の場合
   * **不可**：レイアウトシフトスコアが0.25 を超える場合

* **次のペイントまでのインタラクション**：ページへのユーザーの訪問中にクリック、タップおよびキーボード入力にページが応答するまでの時間を考慮して、ページがユーザーインタラクションにどれだけ速く反応するかを評価します。異常を無視して、観測された最長のインタラクションが最終的な値になります。「次のペイントまでのインタラクション」のパフォーマンス指標は、次のように分類されます。
   * **良**：ユーザーアクション間の時間が 200 ミリ秒（ms）以下の場合
   * **可**：上記の時間が 200 ms より長く 500 ms 以下の場合
   * **不可**：上記の時間が 500 ms を超える場合

## 実用的なインサイト

これらの指標を分析することで、次の機会を特定できます。

* フォームを簡素化し、フィールド数を減らす。
* 明確な指示とラベルにより、フォームの明瞭さが向上する。
* モバイルの応答性を高めるためにフォームのレイアウトを最適化する。
* フォームの読み込みを遅らせる技術的な問題に対処する。

これらの領域に焦点を当てることで、より使いやすいフォームを作成し、訪問者にフォームへの入力を促すことができ、最終的にはコンバージョン率の向上につながります。

## 関連トピック

{{see-more-forms-eds}}
