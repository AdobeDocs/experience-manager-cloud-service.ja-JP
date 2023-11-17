---
title: SLA レポート
description: 契約済みのサービスレベル契約 (SLA) に対する、実稼動AEM環境のパフォーマンスを確認する方法を説明します。
exl-id: 03932415-a029-4703-b44a-f86a87edb328
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 9%

---


# SLA レポート {#sla-reporting}

契約済みのサービスレベル契約 (SLA) に対する、実稼動AEM環境のパフォーマンスを確認する方法を説明します。

## はじめに {#introduction}

SLA レポートデータは、 **レポート** タブをクリックします。 次の手順に従ってにアクセスします。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **レポート** タブを **概要** ページに貼り付けます。

1. 目的の年をクリックして、グラフ化された SLA データを表示します。

![SLA グラフの例](assets/sla-reporting-1.png)

データポイントにカーソルを合わせると、そのポイントの特定の値が表示されます。

![詳細データの表示](assets/sla-reporting-b.png)

## SLA 指標 {#sla-metrics}

選択した年のグラフには、複数のデータセットが含まれます。

* **パブリッシュ層の契約**  — これは、パブリッシュ層のAdobeとの契約で定義される SLA です。

* **パブリッシュ層（実際）**  — これは、AdobeまたはAdobeのベンダーが原因となって発生したインシデントを組み込んだ、実稼動パブリッシュ層の測定稼動時間です。

* **オーサー層の契約**  — これは、Adobeとの契約で定義される作成者層用の SLA です。

* **オーサー層（実際）**  — これは、AdobeまたはAdobeのベンダーが原因となって発生したインシデントを組み込んだ、実稼動オーサー層の測定稼動時間です。

## イベント分析 {#event-analysis}

The **イベント分析** グラフの下のセクションには、選択した年にプログラムで発生した一連のインシデントが表示されます。

各インシデントには、時間範囲、原因、一連のコメントが含まれます。

![イベント分析の例](assets/sla-reporting-c.png)
