---
title: キャッシュとパフォーマンス
description: GraphQLとコンテンツのキャッシュを有効にしてコマース実装のパフォーマンスを最適化するために利用できる様々な設定について説明します。
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 97%

---


# キャッシュとパフォーマンス{#caching}

## コンポーネントおよび GraphQL の応答キャッシュ {#graphql}

AEM CIF コアコンポーネントには、個々のコンポーネントの GraphQL 応答をキャッシュするための組み込みのサポートが既にあります。この機能は、GraphQL バックエンド呼び出しの数を大幅に減らすために使用できます。効果的なキャッシュは、特に、ナビゲーションコンポーネントのカテゴリツリーを取得したり、製品検索ページやカテゴリページに表示される利用可能なすべての集計／ファセット値を取得するなど、繰り返しクエリで実現できます。

AEM CIF コアコンポーネントの場合、キャッシュはコンポーネント単位で設定されるので、各コンポーネントに対して GraphQL 要求／応答をキャッシュするかどうか（およびその長さ）を制御できます。GraphQL クライアントを使用して、OSGi サービスのキャッシュ動作を定義することもできます。

### 設定

特定のコンポーネントに対して設定が完了すると、各キャッシュ設定エントリで定義された GraphQL クエリと応答の格納が開始されます。キャッシュのサイズと各エントリのキャッシュ期間は、カタログデータが変更される頻度や、コンポーネントが常に最新データを表示することの重要度などに応じて、プロジェクト単位で定義します。キャッシュの無効化はおこなわれないので、キャッシュの期間を設定する際は注意が必要です。

コンポーネントのキャッシュを設定する場合、キャッシュ名は、プロジェクトで定義する&#x200B;**プロキシ**&#x200B;コンポーネントの名前にする必要があります。

クライアントが GraphQL 要求を送信する前に、**完全に**&#x200B;同一の GraphQL 要求が既にキャッシュされているかどうかがチェックされ、キャッシュされた応答が返される場合があります。GraphQL リクエストは完全に一致する必要があります。つまり、クエリ、操作名（存在する場合）、変数（存在する場合）はすべてキャッシュされたリクエストと等しく、また、設定されているカスタム HTTP ヘッダーも同じでなければなりません。例えば、Magento `Store` ヘッダーは一致する必要があります。

### 例

製品の検索ページおよびカテゴリページに表示される利用可能なすべての集計／ファセット値を取得する検索サービスのキャッシュを設定することをお勧めします。これらの値は通常、例えば新しい属性が製品に追加された場合にのみ変更されるので、製品属性のセットが頻繁に変更されない場合、このキャッシュエントリの期間は「長く」なる可能性があります。これはプロジェクトに固有のものですが、プロジェクト開発段階では数分の値を使用し、安定した実稼働システムでは数時間の値を使用することをお勧めします。

これは通常、次のキャッシュエントリを使用して設定します。

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQl キャッシュ機能の使用を推奨する別のシナリオの例として、ナビゲーションコンポーネントが挙げられます。これは、すべてのページで同じ GraphQL クエリが送信されるからです。この場合、キャッシュエントリは通常次の値に設定されます。

```
venia/components/structure/navigation:true:10:600
```

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)を使用する場合。CIF ナビゲーションコンポーネント名（ `core/cif/components/structure/navigation/v1/navigation`）では&#x200B;**なく**、コンポーネントプロキシ名（`venia/components/structure/navigation`）が使用されることに注意してください。

他のコンポーネントのキャッシュは、通常は Dispatcher レベルで設定されたキャッシュと連携して、プロジェクト単位で定義する必要があります。これらのキャッシュはアクティブに無効化されないので、キャッシュ期間は慎重に設定する必要があります。すべての可能なプロジェクトや使用例に適切である「フリーサイズ」の値はありません。プロジェクトの要件に最も適したプロジェクトレベルでキャッシュ方法を定義してください。

## Dispatcher のキャッシング {#dispatcher}

[AEM Dispatcher](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html) 内の AEM ページまたはフラグメントのキャッシュは、どの AEM プロジェクトに対してもベストプラクティスです。通常、AEM で変更されたコンテンツの Dispatcher での適切なアップデートは、無効化の手法に依存します。これは、AEM Dispatcher のキャッシュ方法の中心となる機能です。

純粋な AEM で管理されるコンテンツ CIF に加えて、通常、ページには、GraphQL を介して Magento から動的に取り込まれたコマースデータを表示できます。ページ構造自体は変更されない場合がありますが、コマースのコンテンツは変更されることがあります。例は、製品データ（名前、価格など）が Magento で変更された場合です。

AEM Dispatcher で CIF ページを限られた時間だけキャッシュできるようにするため、AEM Dispatcher で CIF ページをキャッシュする場合は、[時間ベースのキャッシュの無効化](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/configuring/dispatcher-configuration.translate.html#configuring-time-based-cache-invalidation-enablettl)（TTL ベースのキャッシュとも呼ばれます）を使用することをお勧めします。この機能は、追加の [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) パッケージを使用して AEM で設定できます。

TTL ベースのキャッシュを使用する場合、デベロッパーは通常、選択した AEM ページに対して 1 つまたは複数のキャッシュ期間を定義します。これにより、CIF ページは設定された期間まで AEM Dispatcher にのみキャッシュされ、コンテンツは頻繁にアップデートされます。

>[!NOTE]
>
>サーバーサイドのデータは AEM Dispatcher によってキャッシュされる場合がありますが、`product`、 `productlist`、`searchresults` などの CIF コンポーネントは、通常、ページの読み込み時にクライアントサイドのブラウザーリクエストで製品の価格を再取得します。これにより、ページの読み込み時に重要な動的コンテンツが常に取得されます。

## その他のリソース

- [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL キャッシュの設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)