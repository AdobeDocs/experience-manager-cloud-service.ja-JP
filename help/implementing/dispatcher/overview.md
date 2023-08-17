---
title: コンテンツ配信フローの概要
description: コンテンツ配信データフローとコンテンツの公開方法の詳細を説明します
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: d1da8559da856e028a5dcad1d0c0b2c00176af0c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 45%

---

# コンテンツ配信フロー {#content-delivery}

このページは、AEM as a Cloud Service のパブリッシュサービスコンテンツ配信の詳細です。パブリッシュサービスコンテンツ配信には、次のものが含まれます。

* CDN
* AEM Dispatcher
* AEM publisher

データフローは次のとおりです。

1. URL がブラウザーに追加される
1. そのドメインへの DNS にマッピングされた CDN に対してリクエストが行われる
1. コンテンツが CDN 上で完全にキャッシュされている場合、CDN はコンテンツをブラウザーに提供する
1. コンテンツが完全にキャッシュされていない場合、CDN は Dispatcher を呼び出す（リバースプロキシ）
1. コンテンツが Dispatcher 上で完全にキャッシュされている場合、Dispatcher はそのコンテンツを CDN に提供する
1. コンテンツが完全にキャッシュされていない場合、Dispatcher はAEMパブリッシュを呼び出す（リバースプロキシ）
1. コンテンツはブラウザーによってレンダリングされ、ヘッダーに応じてキャッシュされる場合もあります

デフォルトでは、コンテンツタイプのHTML/テキストは、Dispatcher レイヤーで 300 秒（5 分）後に期限切れになるように設定されています。この期限は、Dispatcher キャッシュと CDN の両方が考慮するしきい値です。 パブリッシュサービスの再デプロイメント中に、Dispatcher のキャッシュがクリアされ、新しいパブリッシュノードがトラフィックを受け入れる前にウォームアップされます。

以下の節では、コンテンツ配信に関する詳細情報を提供します。
* [CDN 設定](/help/implementing/dispatcher/cdn.md)
* [キャッシュ](/help/implementing/dispatcher/caching.md)


オーサーサービスからパブリッシュサービスへのレプリケーションに関する情報は、[こちら](/help/operations/replication.md)を参照してください。
