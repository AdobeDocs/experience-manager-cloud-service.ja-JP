---
title: CDN パフォーマンスダッシュボード
description: Cloud Manager がコンテンツ配信ネットワーク（CDN）のパフォーマンスを評価する方法およびダッシュボードから学習できる内容について説明します。
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 95%

---

# CDN パフォーマンスダッシュボード {#cdn-performance}

Cloud Manager がコンテンツ配信ネットワーク（CDN）のパフォーマンスを評価する方法およびダッシュボードから学習できる内容について説明します。

## 概要 {#overview}

すべての Cloud Manager プログラムには、CDN パフォーマンスダッシュボードがあります。このダッシュボードには、CDN パフォーマンスの全体的なスコアと、必要に応じて、改善のトレンド、アラート、提案が表示されます。

![CDN パフォーマンスダッシュボード](assets/cdn-performance-dashboard.png)

## ダッシュボードへのアクセス {#accessing}

CDN ダッシュボードは、すべてのプログラムの概要ページで利用できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、表示する CDN ダッシュボードのプログラムをクリックします。

   ![マイプログラムページ](assets/my-programs.png)

1. プログラムの&#x200B;**プログラムの概要**&#x200B;ページで、**環境**&#x200B;および&#x200B;**パイプライン**&#x200B;カードで下にスクロールし、**パフォーマンス**&#x200B;カードを表示します。

   ![パフォーマンス](assets/cdn-performance-overview.png)

## ダッシュボードの使用 {#using}

ダッシュボードには、CDN パフォーマンスの全体的なスコアと、必要に応じて、改善のトレンド、アラート、提案が表示されます。

![CDN パフォーマンスダッシュボード](assets/cdn-performance-dashboard.png)

CDN パフォーマンスとその改善方法についての推奨事項について詳しくは、「**トレンドを表示**」をクリックしてください。

![パフォーマンスのトレンド](assets/cdn-performance-trend.png)

グラフの下で「**表示**」をクリックして、グラフの期間を変更します。

CDN のパフォーマンスを向上させる方法の提案については、「**レコメンデーション**」タブを選択します。

![CDN のレコメンデーション](assets/cdn-performance-recommendations.png)

リスト内のレコメンデーションの横にある山形記号をクリックすると、改善を行う手順と問題の原因に関する詳細が表示されます。

## キャッシュヒットの定義 {#cache-hit}

キャッシュヒット率は、受け取るリクエスト数と比較して、キャッシュが正常に記入できるコンテンツリクエスト数を示します。キャッシュヒット率が高いほど、CDN のパフォーマンスが向上します。

>[!TIP]
>
>Adobe では、ユーザーが 99％のキャッシュヒット率を目指すことをお勧めします。

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **ヒット** - データがキャッシュからリクエストされ、見つかりました。
* **ミス** - データがキャッシュからリクエストされましたが、見つかりません。
* **パス** - データはキャッシュからリクエストされますが、どのような場合でも、このデータをキャッシュしないように設定されています。
* **その他** - キャッシュからのすべてのデータリクエストで、他の大文字と小文字がいずれも一致しません。

キャッシュ指標は 24 時間ごとに更新されます。

>[!TIP]
>
>Cloud Manager と CDN が Dispatcher とやり取りする方法について詳しくは、[AEM as a Cloud Service でのキャッシュ](/help/implementing/dispatcher/caching.md)を参照してください。
