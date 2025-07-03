---
title: キャッシュとパフォーマンス
description: GraphQL とコンテンツキャッシュを有効にしてコマース実装のパフォーマンス最適化に利用できる様々な設定について説明します。
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 100%

---

# キャッシュとパフォーマンス {#caching}

## コンポーネントおよび GraphQL の応答キャッシュ {#graphql}

AEM CIF コアコンポーネントには、個々のコンポーネントの GraphQL 応答をキャッシュするための組み込みのサポートが既にあります。この機能は、GraphQL バックエンド呼び出しの数を大幅に減らすために使用できます。効果的なキャッシュは、特に、ナビゲーションコンポーネントのカテゴリツリーを取得したり、製品検索ページやカテゴリページに表示される利用可能なすべての集計／ファセット値を取得するなど、繰り返しクエリで実現できます。

AEM CIF コアコンポーネントの場合、キャッシュはコンポーネント単位で設定されるので、各コンポーネントに対して GraphQL 要求／応答をキャッシュするかどうか（およびその長さ）を制御できます。GraphQL クライアントを使用して、OSGi サービスのキャッシュ動作を定義することもできます。

### 設定 {#configuration}

特定のコンポーネントに対して設定が完了すると、各キャッシュ設定エントリで定義された GraphQL クエリと応答の格納が開始されます。キャッシュのサイズと各エントリのキャッシュ期間は、例えば以下に応じて、プロジェクト単位で定義されます。

* カタログデータの変更頻度。
* コンポーネントでの最新データの常時表示の重要性など。

キャッシュは無効化されないので、キャッシュの期間を設定する際は注意が必要です。

コンポーネントのキャッシュを設定する場合、キャッシュ名は、プロジェクトで定義する&#x200B;**プロキシ**&#x200B;コンポーネントの名前にする必要があります。

クライアントは、GraphQL リクエストを送信する前に、**全く同じ** GraphQL リクエストが既にキャッシュされているかどうかをチェックし、キャッシュされている応答を返す場合があります。一致させるには、GraphQL リクエストが完全に一致する&#x200B;_必要があります_。つまり、クエリ、操作名（存在する場合）、変数（存在する場合）すべてがキャッシュされたリクエストと一致する&#x200B;_必要があります_。また、設定可能なすべてのカスタム HTTP ヘッダーも同一である&#x200B;_必要があります_。例えば、Adobe Commerce `Store` ヘッダーは一致する&#x200B;_必要があります_。

### 例 {#examples}

アドビでは、製品の検索ページおよびカテゴリページに表示される入手可能なすべての集計／ファセット値を取得する、検索サービスのキャッシュを設定することをお勧めします。通常、これらの値は、新しい属性が製品に追加された場合などにのみ変更されます。したがって、製品属性のセットが頻繁に変更されない場合、このキャッシュエントリの期間は「長くなる」可能性があります。このエントリはプロジェクトに固有のものですが、アドビではプロジェクト開発段階では数分の値を使用し、安定した実稼働システムでは数時間の値を使用することをお勧めします。

この設定は通常、次のキャッシュエントリを使用して設定します。

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQL キャッシュ機能の使用を推奨する別のシナリオの例として、ナビゲーションコンポーネントがあります。これは、すべてのページで同じ GraphQL クエリが送信されるからです。この場合、キャッシュエントリは通常次の値に設定されます。

```
venia/components/structure/navigation:true:10:600
```

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)を使用することを検討してください。CIF ナビゲーションコンポーネント名（`core/cif/components/structure/navigation/v1/navigation`）では&#x200B;**なく**、コンポーネントプロキシ名（`venia/components/structure/navigation`）が使用されることに注意してください。

他のコンポーネントのキャッシュは、通常は Dispatcher レベルで設定されたキャッシュと連携して、プロジェクト単位で定義する必要があります。これらのキャッシュはアクティブに無効化されないので、キャッシュ期間を慎重に設定する必要があります。考えられるすべてのプロジェクトやユースケースに適合する「万能の」値はありません。プロジェクトの要件に最も適したプロジェクトレベルでキャッシュ方法を定義してください。

## Dispatcher のキャッシュ {#dispatcher}

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) 内の AEM ページまたはフラグメントのキャッシュは、どの AEM プロジェクトに対してもベストプラクティスです。通常、AEM で変更されたコンテンツの Dispatcher での適切なアップデートは、無効化の手法に依存します。この機能は、AEM Dispatcher のキャッシュ戦略の中核となります。

純粋な AEM 管理コンテンツ CIF に加えて、通常、ページには、GraphQL 経由で Adobe Commerce から動的に取り込まれたコマースデータを表示できます。ページ構造自体は変更されませんが、コマースのコンテンツは変更される場合があります。例えば、名前や価格などの製品データが Adobe Commerce で変更された場合です。

AEM Dispatcher で CIF ページを限られた時間だけキャッシュできるようにするため、アドビでは AEM Dispatcher で CIF ページをキャッシュする場合は、[時間に基づくキャッシュの無効化](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#configuring-time-based-cache-invalidation-enablettl)（TTL ベースのキャッシュとも呼ばれる）を使用することをお勧めします。この機能は、追加の [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) パッケージを使用して AEM で設定できます。

TTL ベースのキャッシュを使用する場合、デベロッパーは通常、選択した AEM ページに対して 1 つまたは複数のキャッシュ期間を定義します。この期間により、CIF ページは設定された期間を上限として AEM Dispatcher にキャッシュされ、コンテンツは頻繁に更新されます。

>[!NOTE]
>
>サーバーサイドのデータは AEM Dispatcher によってキャッシュされる場合がありますが、`product`、`productlist`、`searchresults` などの CIF コンポーネントは、通常、ページの読み込み時にクライアントサイドのブラウザーリクエストで製品の価格を再取得します。これにより、ページの読み込み時に重要な動的コンテンツが常に取得されます。

## その他のリソース {#additional}

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL キャッシュの設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)
