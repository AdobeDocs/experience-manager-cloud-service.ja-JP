---
title: コンテンツサービス用の JSON エクスポーター
description: AEM コンテンツサービスは、Web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM Web ページとは異なるチャネルにコンテンツを配信できます。
translation-type: tm+mt
source-git-commit: 02d95b7c45cb4d6d2fbfd9699690ecc1b80e1202
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 75%

---


# コンテンツサービス用の JSON エクスポーター {#json-exporter-for-content-services}

AEM Content Servicesは、Webページに重点を置くことなく、AEM内またはからコンテンツの説明と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM Web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM外部のその他のチャネルおよびタッチポイント

構造化コンテンツを使用するコンテンツフラグメントでは、JSONエクスポーターを使用してAEMページのコンテンツをJSONデータモデル形式で配信することで、コンテンツサービスを提供できます。 その後、コンテンツを独自のアプリケーションで使用することができます。

## JSON エクスポーターとコンテンツフラグメントコアコンポーネント {#json-exporter-with-content-fragment-core-components}

AEM JSON エクスポーターを使用すると、任意の AEM ページのコンテンツを JSON データモデル形式で配信できます。その後、コンテンツを独自のアプリケーションで使用することができます。

AEM内では、セレクター `model` と拡張子を使用して配信を行い `.json` ます。

`.model.json`

1. 例えば、次の URL では

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 次のようなコンテンツが配信されます。

   ![WKNDコンテンツのJSONモデル](/help/implementing/developing/introduction/assets/json-model-wknd.png)

代わりに、構造化コンテンツフラグメントのコンテンツを、ターゲット設定して配信することもできます。

これをおこなうには、（`jcr:content` を介して）フラグメントへのパス全体を使用します。例えば、次のようなサフィックスを付けます。

`.../jcr:content/root/container/container/contentfragment.model.json`

ページには、単一のコンテンツフラグメントまたはタイプが異なる複数のコンポーネントを含めることができます。また、リストコンポーネントなどのメカニズムを使用して、関連するコンテンツを自動的に検索することもできます。

* 例えば、次の URL では

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* 次のようなコンテンツが配信されます。

   ![WKNDコンテンツフラグメントのJSONモデル](/help/implementing/developing/introduction/assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >このデータにアクセスして使用するように[独自のコンポーネントを変更する](enabling-json-exporter.md)ことができます。

   >[!NOTE]
   >
   >標準的な実装ではありませんが、 [複数のセレクターがサポートされます](enabling-json-exporter.md#multiple-selectors) が、最初 `model` にセレクターを指定する必要があります。

### その他の情報 {#further-information}

関連トピック：

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling Model:
   * [Sling モデル - 130 以降のモデルクラスとリソースタイプの関連付け](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM と JSON：
   * [コンポーネントの JSON 書き出しの有効化](enabling-json-exporter.md)

## 関連ドキュメント {#related-documentation}

詳しくは、以下を参照してください。

* [アセットユーザーガイドのコンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)および[コンテンツフラグメントコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/content-fragment-component.html)
