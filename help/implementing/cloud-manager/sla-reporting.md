---
title: SLA レポート
description: 契約されたサービスレベル契約に対する AEM の実稼動環境のパフォーマンスを確認する方法について説明します。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e6f5414454f79f46421593440587e81941a8f4c2
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 100%

---


# SLA レポート {#sla-reporting}

SLA（契約されたサービスレベル契約）に対する AEM の実稼動環境のパフォーマンスを確認する方法について説明します。

## SLA レポートの表示 {#introduction}

SLA レポートデータでは、オーサー層とパブリッシュ層という 2 つの実稼動層のパフォーマンス指標を追跡します。

選択した年の折れ線グラフには、1～12月の各月のデータポイントが含まれます。次の指標が追跡されます。

| 追跡対象となった指標 | 線の色 | 説明 |
| --- | --- | --- |
| オーサー階層 (実際) | ライトグリーン | アドビまたはアドビのベンダーが原因となって発生したインシデントを組み込んだ、実稼動オーサー層の測定稼動時間です。 |
| オーサー階層（契約） | ダークブルー | アドビとの契約で定義されるオーサー層用の SLA です。 |
| パブリッシュ階層（実際） | オレンジ | アドビまたはアドビのベンダーが原因となって発生したインシデントを組み込んだ、実稼動パブリッシュ層の測定稼動時間です。 |
| パブリッシュ階層（契約） | レッド | アドビとの契約で定義されるパブリッシュ層用の SLA です。 |

**SLA レポートを表示するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページの左側のサイドメニューで、「**レポート**」をクリックします。

1. 「**SLA レポート**」をクリックします。

   ![SLA レポートの折れ線グラフ](/help/implementing/cloud-manager/assets/cm-sla-report2.png)

1. 目的の年をクリックして、SLA データの折れ線グラフを表示します。

1. （オプション）次のいずれかの操作を行います。

   * そのポイントの特定の値を表示するには、折れ線グラフのデータポイントにカーソルを合わせます。
   * 折れ線グラフの PNG 画像ファイルを保存するには、折れ線グラフの年の下にあるダウンロードアイコンをクリックします。
   * 指標のデータのみを表示するには、その指標名をクリックします。または、1 つ以上の指標名を選択または選択解除しながら、キーボードの `Shift` キーを押します。

## イベント分析 {#event-analysis}

このグラフの「**イベント分析**」セクションには、選択年度中にプログラムに発生した一連のインシデントが表示されます。

インシデントごとに、時間範囲、原因および一連のコメントが記載されています。

![イベント分析の例](assets/sla-reporting-c.png)

## SLA レポートの更新間隔 {#refresh}

SLA レポートには、AEM 実稼動環境のパフォーマンスに関するインサイトが表示されます。このインサイトは、最新ですが、即時ではありません。SLA レポートは、`Production previous month` としてマークされた新しいプログラムに対して毎月生成されます。これは、即時ではありません。この遅延により、SLA レポートを確認する際は、次の点に注意してください。

* レポートされる SLA は、その月の間に SLA が変更された場合でも、月の初めに存在した SLA になります。
* 月の初めにプログラムが存在せず、そのために SLA が存在しなかった場合は、プログラムの作成日に存在していた SLA が適用されます。

## プレビュー環境 {#preview}

プレビュー環境は、コンテンツ作成者が公開前にコンテンツの最終的なエクスペリエンスを検証するためのツールとして設計されています。この機能により、プレビュー環境は高可用性を備えた設計ではなく、SLA が関連付けられていません。

