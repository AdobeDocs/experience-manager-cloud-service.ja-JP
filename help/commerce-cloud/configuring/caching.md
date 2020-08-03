---
title: キャッシュとパフォーマンス
description: キャッシュとパフォーマンス
translation-type: tm+mt
source-git-commit: 2997a28e79b51e88ececbd46c81dbc6a6c443e68
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# キャッシュとパフォーマンス {#caching}

## コンポーネントおよびGraphQLの応答キャッシュ {#graphql}

AEM CIFコアコンポーネントには、個々のコンポーネント用のGraphQL応答のキャッシュに対する組み込みのサポートが既にあります。 この機能は、GraphQLバックエンド呼び出しの数を大幅に減らすために使用できます。 効果的なキャッシュは、特にナビゲーションコンポーネントのカテゴリツリーを取得したり、製品検索ページやカテゴリページに表示される利用可能なすべての集計/ファセット値を取得するなど、繰り返しクエリで実現できます。

AEM CIFコアコンポーネントの場合、キャッシュはコンポーネント単位で設定されるので、各コンポーネントに対してGraphQLリクエスト/応答をキャッシュするかどうか（およびその長さ）を制御できます。 GraphQLクライアントを使用して、OSGiサービスのキャッシュ動作を定義することもできます。

### 設定

特定のコンポーネントに対して設定が完了すると、各キャッシュ設定エントリで定義されたとおりに、GraphQLクエリと応答を格納するキャッシュ開始が格納されます。 カタログデータが変更される頻度や、コンポーネントが常に最新の可能なデータを表示する重要度などに応じて、キャッシュのサイズと各エントリのキャッシュ期間はプロジェクト単位で定義します。 キャッシュの無効化は行われないので、キャッシュの期間を設定する際は注意が必要です。

コンポーネントのキャッシュを設定する場合、キャッシュ名は、プロジェクトで定義する **プロキシ** コンポーネントの名前にする必要があります。

クライアントがGraphQL要求を送信する前に、 **完全に同一のGraphQL要求が既にキャッシュされているかどうかがチェックされ** 、キャッシュされた応答が返される場合があります。 一致させるには、GraphQLリクエストが完全に一致する必要があります。つまり、クエリ、操作名（存在する場合）、変数（存在する場合）はすべてキャッシュされたリクエストと等しく、また、設定されるカスタムHTTPヘッダも同じでなければなりません。 例えば、Magento `Store` ヘッダーが一致する必要があります。

### 例

製品の検索ページおよびカテゴリページに表示される利用可能なすべての集計/ファセット値を取得するSearchサービスのキャッシュを設定することをお勧めします。 これらの値は通常、例えば新しい属性が製品に追加された場合にのみ変更されるので、製品属性のセットが頻繁に変更されない場合、このキャッシュエントリの期間は「大」になる可能性があります。 これはプロジェクトに固有のものですが、プロジェクト開発段階では数分の値を使用し、安定した実稼働システムでは数時間の値を使用することをお勧めします。

これは通常、次のキャッシュエントリを使用して設定します。

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

GraphQlキャッシュ機能の使用を推奨する別のシナリオの例として、ナビゲーションコンポーネントが挙げられます。これは、すべてのページで同じGraphQLクエリが送信されるからです。 この場合、キャッシュエントリは通常次の値に設定されます。

```
venia/components/structure/navigation:true:10:600
```

を使用する場合は、 [ベニアリファレンスストア](https://github.com/adobe/aem-cif-guides-venia) (Venia Reference Store)を考慮してください。 CIFナビゲーションコンポーネント( `venia/components/structure/navigation`)の名前で **はなく**`core/cif/components/structure/navigation/v1/navigation`、コンポーネントプロキシ名を使用することに注意してください。

他のコンポーネントのキャッシュは、通常、Dispatcherレベルで構成されるキャッシュと連携して、プロジェクト単位で定義する必要があります。 これらのキャッシュはアクティブに無効になっていないので、キャッシュ期間は慎重に設定する必要があります。 すべての可能なプロジェクトや使用例に一致する「1つのサイズですべてを満たす」値はありません。 プロジェクトの要件に最も適したプロジェクトレベルでキャッシュ方法を定義してください。

## ディスパッチャーのキャッシング {#dispatcher}

AEMページまたはAEM [Dispatcher内のフラグメントのキャッシュは](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html) 、どのAEMプロジェクトでもベストプラクティスです。 通常、AEMで変更されたコンテンツがDispatcher内で適切に更新されるように、無効化手法に依存します。 これは、AEMDispatcherのキャッシュ方法の中核機能です。

純粋なAEMで管理されるコンテンツCIFに加えて、通常、ページには、GraphQLを介してMagentoから動的に取り込まれたコマースデータを表示できます。 ページ構造自体は変更されない場合がありますが、コマースのコンテンツは変更されることがあります。例えば、商品データ（名前、価格など）のMagentoが変更される場合などです。

AEMディスパッチャーでCIFページを限られた時間だけキャッシュできるようにするため、AEMDispatcherでCIFページをキャッシュする場合は、 [時間ベースのキャッシュの無効化](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) （TTLベースのキャッシュとも呼ばれます）を使用することをお勧めします。 この機能は、追加の [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) パッケージを使用してAEMで設定できます。

TTLベースのキャッシュを使用する場合、開発者は通常、選択したAEMページの1つまたは複数のキャッシュ期間を定義します。 これにより、CIFページは設定された期間までAEMディスパッチャーにのみキャッシュされ、コンテンツは頻繁に更新されます。

>[!NOTE]
>
>サーバー側のデータはAEMディスパッチャーによってキャッシュされる場合がありますが、 `product`、 `productlist``searchresults` 、コンポーネントなどの一部のCIFコンポーネントは、通常、ページが読み込まれる際に、クライアント側のブラウザーリクエストで製品価格を再取得します。 これにより、ページの読み込み時に重要な動的コンテンツが常に取得されます。

## その他のリソース

- [ベニアリファレンスストア](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQLキャッシュの設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html)