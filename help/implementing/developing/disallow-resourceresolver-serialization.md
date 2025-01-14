---
title: Sling Model Exporter による ResourceResolvers のシリアル化を許可しない
description: Sling Model Exporter による ResourceResolvers のシリアル化を許可しない
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a64c17943332782814bdacd7484e056cd445d3a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 35%

---

# Sling Model Exporter による ResourceResolvers のシリアル化を許可しない {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling Model Exporter 機能を使用すると、Sling モデルオブジェクトを JSON 形式にシリアル化できます。 この機能は、SPA（単一ページアプリケーション）が AEM からのデータに容易にアクセスできるようにするので、広く使用されています。実装側では、Jackson Databind ライブラリを使用して、これらのオブジェクトをシリアル化します。

シリアル化は再帰的な操作です。「ルートオブジェクト」から始めて、すべての適格なオブジェクトを再帰的に反復処理し、それらのオブジェクトとその子をシリアル化します。 シリアル化されるフィールドの説明については、記事 [Jackson - Decide What Fields Get Serialized/Deserialized.](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not) を参照してください。

このアプローチは、すべてのタイプのオブジェクトを JSON にシリアル化します。 当然、シリアル化ルールの対象である場合は、Sling `ResourceResolver` オブジェクトもシリアル化できます。 `ResourceResolver` サービス（つまり、それを表すサービスオブジェクト）には、開示してはいけない、潜在的な機密情報が含まれているため、これは問題になります。例：

* ユーザーID
* 相対パスを解決する検索パス
* `propertyMap`

特に機密性が高いのは `propertyMap` （[`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--) の API ドキュメントを参照）です。これは内部データ構造であり、`ResourceResolver` と同じライフサイクルを共有するオブジェクトのキャッシュなど、多くの目的で使用できます。 シリアル化すると、実装の詳細がリークされる可能性があり、エンドユーザーが読み取りおよびアクセスできないデータが公開されるので、セキュリティに影響を与える可能性があります。 その理由で `ResourceResolvers` を JSON にシリアル化しないでください。

Adobeは、`ResourceResolvers` のシリアル化を次の 2 つの手順で無効にする予定です。

1. AEM as a Cloud Service リリース 14697 以降、`ResourceResolver` ールがシリアル化されるたびに、AEMは警告メッセージをログに記録します。 どのお客様にも、アプリケーションログでこれらのログステートメントを確認し、それに応じてコードベースを調整することをお勧めします。
1. 後で、Adobeによって `ResourceResolver` の JSON としてのシリアル化が無効になります。

## 実装 {#implementation}

WARN メッセージは、AEM as a Cloud Service とローカル AEM SDK の両方のインスタンスに記録され、次のようになります。

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

このログメッセージは、`/content/…/page` を JSON にシリアル化するプロセスの間に、`ResourceResolver` が既にシリアル化されていることを意味します。`/content/../page.model.json` をリクエストして、正確に `ResourceResolver` のフィールドがどこに表示されるのかを確認し、これを使用して、実際にこの動作をトリガーしている Sling Model クラスを識別できます。


>[!NOTE]
>
>[AEM コアコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction) は、この問題の影響を受けないことが検証されています。

## 要求されたアクション {#requested-action}

Adobeは、すべてのお客様に対して、アプリケーションログおよびコードベースをチェックしてこの問題の影響を受けているかどうかを確認し、必要に応じてカスタムアプリケーションを変更して、この警告メッセージがログに表示されないようにします。

ほとんどの場合、これらの必要な変更は簡単であると想定されています。 `ResourceResolver` オブジェクトは JSON 出力にはまったく必要ありません。そこに含まれる情報は、通常フロントエンドアプリケーションでは必要ないからです。つまり、ほとんどの場合、`ResourceResolver` オブジェクトが Jackson によって考慮されないように除外すれば十分です（[rules.](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not) を参照）。

Sling モデルがこの問題の影響を受けながらも変更されていない場合、`ResourceResolver` オブジェクトのシリアル化を明示的に無効にすると（2 番目の手順としてAdobeで実行する）、JSON 出力に変更が適用されます。
