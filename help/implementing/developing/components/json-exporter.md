---
title: コンテンツサービス用の JSON エクスポーター
description: AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 7d09cafc4f8518fee185d3f9efc76c33ec20f9a3
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 92%

---

# コンテンツサービス用の JSON エクスポーター {#json-exporter-for-content-services}

AEM コンテンツサービスは、Web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

構造化コンテンツを使用するコンテンツフラグメントでは、JSON エクスポーターを使用して、任意の AEM ページのコンテンツを JSON データモデル形式で配信することで、コンテンツサービスを提供できます。その後、独自のアプリケーションでコンテンツを使用できるようになります。

## JSON エクスポーターとコンテンツフラグメントコアコンポーネント {#json-exporter-with-content-fragment-core-components}

AEM JSON エクスポーターを使用して、任意のAEMページのコンテンツを JSON データモデル形式で配信できます。 その後、独自のアプリケーションでコンテンツを使用できるようになります。

AEM 内では、セレクター `model` と `.json` 拡張機能を使用して配信をおこないます。

`.model.json`

1. 例えば、次のような URL があります。

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 次のようなコンテンツを配信します。

   ![WKND コンテンツの JSON モデル](assets/json-model-wknd.png)

代わりに、構造化コンテンツフラグメントのコンテンツを、ターゲット設定して配信することもできます。

これをおこなうには、（`jcr:content` を介して）フラグメントへのパス全体を使用します。例えば、次のようなサフィックスを付けます。

`.../jcr:content/root/container/container/contentfragment.model.json`

ページには、単一のコンテンツフラグメントまたは様々なタイプの複数のコンポーネントを含めることができます。また、リストコンポーネントなどのメカニズムを使用して、関連するコンテンツを自動的に検索することもできます。

* 例えば、次のような URL があります。

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* 次のようなコンテンツを配信します。

  ![WKND コンテンツフラグメントの JSON モデル](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >このデータにアクセスして使用するように[独自のコンポーネントを変更する](enabling-json-exporter.md)ことができます。

  >[!NOTE]
  >
  >標準的な実装ではありませんが、[複数のセレクターがサポートされています](enabling-json-exporter.md#multiple-selectors)。ただし、`model` セレクターを最初に指定する必要があります。

### その他の情報 {#further-information}

関連トピック：

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling モデル：
   * [Sling モデル - 1.3.0 以降のモデルクラスとリソースタイプの関連付け](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM と JSON：
   * [コンポーネントの JSON 書き出しの有効化](enabling-json-exporter.md)

## 関連ドキュメント {#related-documentation}

詳しくは、以下を参照してください。

* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)
