---
title: コンポーネントの JSON 書き出しの有効化
description: モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 07327f80b23e1e6fdbb3fb49d861221877724d39
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 100%

---

# コンポーネントの JSON 書き出しの有効化 {#enabling-json-export-for-a-component}

モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。

## 概要 {#overview}

JSON 書き出しは、[Sling Model](https://sling.apache.org/documentation/bundles/models.html) と [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) フレームワーク（それ自体が [Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)に依存）に基づいています。

つまり、JSON を書き出す必要がある場合、コンポーネントには Sling Model が必要です。したがって、次の 2 つの手順に従って、任意のコンポーネントで JSON 書き出しを有効にします。

* [コンポーネントに Sling Model を定義する](#define-a-sling-model-for-the-component)
* [Sling Model インターフェイスに注釈を付ける](#annotate-the-sling-model-interface)

## コンポーネントに Sling Model を定義する {#define-a-sling-model-for-the-component}

まず、コンポーネントに Sling モデルを定義する必要があります。

>[!NOTE]
>
>Sling Model の使用例については、[AEM での Sling Model Exporter の開発](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=ja)の記事を参照してください。

Sling Model の実装クラスに次のような注釈を付ける必要があります。

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

これにより、`.model` セレクターと `.json` 拡張子を使用して、コンポーネントをそれ自体に書き出すことができます。

さらに、Sling Model クラスが `ComponentExporter` インターフェイスに適応できるように指定されます。

>[!NOTE]
>
>Jackson 注釈は通常 Slingモデルクラスレベルではなく、モデルインターフェイスレベルで指定されます。これは、JSON 書き出しがコンポーネント API の一部とみなされるようにするためです。

>[!NOTE]
>
>`ExporterConstants` クラスと `ComponentExporter` クラスは `com.adobe.cq.export.json` バンドルから取得されます。

### 複数のセレクターの使用 {#multiple-selectors}

標準的なユースケースではありませんが、`model` セレクターに加えて複数のセレクターを設定することができます。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

ただし、その場合は、`model` セレクターを最初のセレクターにし、拡張子を `.json` にする必要があります。

## Sling Model インターフェイスに注釈を付ける {#annotate-the-sling-model-interface}

JSON エクスポーターフレームワークで認識されるようにするには、モデルインターフェイスに `ComponentExporter` インターフェイス（またはコンテナコンポーネントの場合は `ContainerExporter`）を実装する必要があります。

対応する Sling Model インターフェイス（`MyComponent`）には、[Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)を使用して注釈が付けられ、どのように書き出し（シリアル化）が行われるかが定義されます。

シリアル化されるメソッドを定義するためには、モデルインターフェイスに適切に注釈を付ける必要があります。デフォルトでは、getter の通常の命名規則に準拠するすべてのメソッドがシリアル化され、JSON プロパティ名が getter 名から派生されます。これを回避または上書きするには、`@JsonIgnore` または `@JsonProperty` を使用して JSON プロパティの名前を変更します。

## 例 {#example}

[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) は、JSON 形式での書き出しをサポートしており、参考にすることができます。

例えば、画像コアコンポーネントの Sling Model 実装とその注釈されたインターフェイスを参照してください。

## 関連ドキュメント {#related-documentation}

* [コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)
