---
title: キャッシュとパフォーマンス
description: GraphQL とコンテンツキャッシュを有効にしてコマース実装のパフォーマンス最適化に利用できる様々な設定について説明します。
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 44%

---

# キャッシュとパフォーマンス {#caching}

## コンポーネントおよび GraphQL の応答キャッシュ {#graphql}

AEM CIF コアコンポーネントには、個々のコンポーネントの GraphQL 応答をキャッシュするための組み込みのサポートが既にあります。この機能は、GraphQL バックエンド呼び出しの数を大幅に減らすために使用できます。効果的なキャッシュは、特に、ナビゲーションコンポーネントのカテゴリツリーを取得したり、製品検索ページやカテゴリページに表示される利用可能なすべての集計／ファセット値を取得するなど、繰り返しクエリで実現できます。

AEM CIF コアコンポーネントの場合、キャッシュはコンポーネント単位で設定されるので、各コンポーネントに対して GraphQL 要求／応答をキャッシュするかどうか（およびその長さ）を制御できます。GraphQL クライアントを使用して、OSGi サービスのキャッシュ動作を定義することもできます。

### 設定 {#configuration}

特定のコンポーネントに対して設定が完了すると、各キャッシュ設定エントリで定義された GraphQL クエリと応答の格納が開始されます。キャッシュのサイズと各エントリのキャッシュ期間は、例えば次のように、プロジェクト単位で定義されます。

* カタログデータの変更頻度。
* コンポーネントが常に最新のデータを表示することの重要性など。

キャッシュの無効化はおこなわれないので、キャッシュの期間を設定する際は注意が必要です。

コンポーネントのキャッシュを設定する場合、キャッシュ名は、プロジェクトで定義する&#x200B;**プロキシ**&#x200B;コンポーネントの名前にする必要があります。

クライアントがGraphQLリクエストを送信する前に、それが **正確** 同じGraphQLリクエストが既にキャッシュされており、キャッシュされた応答を返す場合があります。 照合するには、GraphQLリクエスト _必須_ 完全に一致します。つまり、クエリ、操作名（存在する場合）、変数（存在する場合） _必須_ は、キャッシュされたリクエストと等しくなります。 また、設定可能なすべてのカスタム HTTP ヘッダー _必須_ 同じです。 例えば、Adobe Commerce `Store` ヘッダー _必須_ 一致

### 例 {#examples}

Adobeでは、製品の検索ページおよびカテゴリページに表示される使用可能なすべての集計/ファセット値を取得する検索サービスに対して、キャッシュを設定することをお勧めします。 これらの値は、通常、例えば新しい属性が製品に追加された場合にのみ変更されます。 したがって、製品属性のセットが頻繁に変更されない場合、このキャッシュエントリの期間は「長い」可能性があります。 このエントリはプロジェクト固有ですが、Adobeでは、安定した実稼動システムで、プロジェクト開発フェーズで数分、数時間の値を推奨しています。

この設定は、通常、次のキャッシュエントリを使用して設定します。

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQl キャッシュ機能の使用を推奨する別のシナリオの例として、ナビゲーションコンポーネントがあります。 これは、すべてのページで同じGraphQLクエリが送信されるからです。 この場合、キャッシュエントリは通常次の値に設定されます。

```
venia/components/structure/navigation:true:10:600
```

これを考えると [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia) が使用されます。 CIF ナビゲーションコンポーネント名（`core/cif/components/structure/navigation/v1/navigation`）では&#x200B;**なく**、コンポーネントプロキシ名（`venia/components/structure/navigation`）が使用されることに注意してください。

他のコンポーネントのキャッシュは、通常は Dispatcher レベルで設定されたキャッシュと連携して、プロジェクト単位で定義する必要があります。これらのキャッシュはアクティブに無効化されないので、キャッシュ期間は慎重に設定する必要があります。 すべての可能なプロジェクトや使用例に一致する「1 つのサイズ」の値はありません。 プロジェクトの要件に最も適したプロジェクトレベルでキャッシュ方法を定義してください。

## Dispatcher のキャッシュ {#dispatcher}

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) 内の AEM ページまたはフラグメントのキャッシュは、どの AEM プロジェクトに対してもベストプラクティスです。通常、AEM で変更されたコンテンツの Dispatcher での適切なアップデートは、無効化の手法に依存します。この機能は、AEM Dispatcher のキャッシュ戦略の中核となります。

純粋なAEMで管理されるコンテンツ CIF に加えて、通常、ページには、GraphQLを介してAdobe Commerceから動的に取得されたコマースデータを表示できます。 ページ構造自体は変更されない場合がありますが、コマースのコンテンツは変更される場合があります。 例えば、名前や価格などの製品データがAdobe Commerceで変更された場合、

AEM Dispatcher で CIF ページが限られた時間キャッシュされるように、Adobeは、 [時間に基づくキャッシュの無効化](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#configuring-time-based-cache-invalidation-enablettl) AEM Dispatcher で CIF ページをキャッシュする場合は（TTL ベースのキャッシュと呼ばれます）、 この機能は、追加の [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) パッケージを使用して AEM で設定できます。

TTL ベースのキャッシュを使用する場合、デベロッパーは通常、選択した AEM ページに対して 1 つまたは複数のキャッシュ期間を定義します。この期間を設定すると、CIF ページは設定された期間までAEM Dispatcher にのみキャッシュされ、コンテンツは頻繁に更新されます。

>[!NOTE]
>
>サーバーサイドのデータはAEM Dispatcher によってキャッシュされる場合がありますが、CIF の一部のコンポーネント ( `product`, `productlist`、および `searchresults` コンポーネントは、通常、ページが読み込まれる際に、クライアント側のブラウザーリクエストで製品価格を再取得します。 これにより、ページの読み込み時に重要な動的コンテンツが常に取得されます。

## その他のリソース {#additional}

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [GraphQL キャッシュの設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)
