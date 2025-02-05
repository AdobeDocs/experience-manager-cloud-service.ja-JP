---
title: コンテンツサービス用の JSON エクスポーター
description: AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 96%

---

# コンテンツサービス用の JSON エクスポーター {#json-exporter-for-content-services}

AEM コンテンツサービスは、Web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* 単一ページアプリケーション
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

構造化コンテンツを使用するコンテンツフラグメントでは、JSON エクスポーターを使用して、任意の AEM ページのコンテンツを JSON データモデル形式で配信することで、コンテンツサービスを提供できます。その後、独自のアプリケーションでコンテンツを使用できるようになります。

## JSON エクスポーターとコンテンツフラグメントコアコンポーネント {#json-exporter-with-content-fragment-core-components}

AEM JSON エクスポーターを使用すると、任意の AEM ページのコンテンツを JSON データモデル形式で配信できます。その後、独自のアプリケーションでコンテンツを使用できるようになります。

AEM 内では、セレクター `model` と `.json` 拡張機能を使用して配信をおこないます。

`.model.json`

1. 例えば、次のような URL があります。

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 次のようなコンテンツが配信されます。

   ![WKND コンテンツの JSON モデル](assets/json-model-wknd.png)

代わりに、構造化コンテンツフラグメントのコンテンツを、ターゲット設定して配信することもできます。

これを行うには、（`jcr:content` を介して）フラグメントへのパス全体を使用します。例えば、次のようなサフィックスを付けます。

`.../jcr:content/root/container/container/contentfragment.model.json`

ページには、単一のコンテンツフラグメントまたは様々なタイプの複数のコンポーネントを含めることができます。また、リストコンポーネントなどのメカニズムを使用して、関連するコンテンツを自動的に検索することもできます。

* 例えば、次のような URL があります。

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* 次のようなコンテンツが配信されます。

  ![WKND コンテンツフラグメントの JSON モデル](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >このデータにアクセスして使用するように[独自のコンポーネントを変更する](enabling-json-exporter.md)ことができます。

  >[!NOTE]
  >
  >標準実装ではありませんが、[ 複数のセレクターがサポートされています ](enabling-json-exporter.md#multiple-selectors) が、`model` を最初にする必要があります。

### その他の情報 {#further-information}

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling モデル：
   * [Sling モデル - 1.3.0 以降のモデルクラスとリソースタイプの関連付け](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM と JSON：
   * [コンポーネントの JSON 書き出しの有効化](enabling-json-exporter.md)

## 関連ドキュメント {#related-documentation}

* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)
