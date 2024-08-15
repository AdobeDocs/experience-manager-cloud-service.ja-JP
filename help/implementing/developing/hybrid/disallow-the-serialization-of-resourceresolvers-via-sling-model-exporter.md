---
title: Sling Model Exporter による ResourceResolvers のシリアル化を許可しない
description: Sling Model Exporter による ResourceResolvers のシリアル化を許可しない
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 96%

---

# Sling Model Exporter による ResourceResolvers のシリアル化を許可しない {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling Model Exporter 機能を使用すると、Sling Models オブジェクトを JSON 形式にシリアル化できます。この機能は、SPA（単一ページアプリケーション）が AEM からのデータに容易にアクセスできるようにするので、広く使用されています。実装では、Jacson Databind ライブラリを使用してこれらのオブジェクトをシリアル化します。

シリアル化は再帰的な操作です。「root object」から始まり、すべての対象オブジェクトを再帰的に反復し、それらとその子をシリアル化します。シリアル化されるフィールドの説明については、[Jackson - Decide What Fields Get Serialized/Deserialized](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not) を参照してください。

このアプローチは、すべてのタイプのオブジェクトを JSON にシリアル化し、当然ながら、シリアル化のルールの対象となる場合は、Sling `ResourceResolver` オブジェクトもシリアル化できます。`ResourceResolver` サービス（つまり、それを表すサービスオブジェクト）には、開示してはいけない、潜在的な機密情報が含まれているため、これは問題になります。次に例を示します。

* ユーザーID
* 相対パスを解決する検索パス
* `propertyMap`。

特に注意が必要なのは `propertyMap` で（[`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--) の API ドキュメントを参照）で、内部データ構造であり、多くの目的で使用できます。例えば、`ResourceResolver` として同じライフサイクルを共有するキャッシュオブジェクトなどがあります。これらをシリアル化すると、エンドユーザーが読み取ることができない、またはアクセスできないデータが公開されるので、実装の詳細が漏洩し、セキュリティに影響を与える可能性があります。その理由で `ResourceResolvers` を JSON にシリアル化しないでください。

アドビは、2 段階アプローチでの `ResourceResolvers` のシリアル化を無効にする予定です。

1. AEM as a Cloud Service 14697 のリリース以降、`ResourceResolver` がシリアル化された AEM では、警告メッセージがログに記録されます。どのお客様にも、アプリケーションログでこれらのログステートメントを確認し、それに応じてコードベースを調整することをお勧めします。
1. 後でアドビは JSON としての ResourceResolvers のシリアル化を無効にします。

## 実装 {#implementation}

WARN メッセージは、AEM as a Cloud Service とローカル AEM SDK の両方のインスタンスに記録され、次のようになります。

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

このログメッセージは、`/content/…/page` を JSON にシリアル化するプロセスの間に、`ResourceResolver` が既にシリアル化されていることを意味します。`/content/../page.model.json` をリクエストして、正確に `ResourceResolver` のフィールドがどこに表示されるのかを確認し、これを使用して、実際にこの動作をトリガーしている Sling Model クラスを識別できます。


>[!NOTE]
>
>AEM コアコンポーネントは、この問題の影響を受けないことが検証されました。

## 要求されたアクション {#requested-action}

アドビは、すべてのお客様に対し、アプリケーションログとコードベースがこの問題の影響を受けているかどうかを確認するように促し、必要に応じてカスタムアプリケーションを変更するように要求します。これにより、この WARN メッセージが表示されなくなります。

ほとんどの場合、これらの必要な変更はわかりやすく、JSON 出力では `ResourceResolver` オブジェクトはまったく必要ありません。含まれる情報は、通常、フロントエンドアプリケーションでは必要ありません。つまり、ほとんどの場合、Jackson によって考慮されないように `ResourceResolver` オブジェクト（[ルール](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)を参照）を除外するだけで十分です。

Sling モデルがこの問題の影響を受けても変更はされない場合、`ResourceResolver` オブジェクトのシリアル化を明示的に無効にする（2 番目の手順としてアドビが実行する）ことで、JSON 出力が強制的に変更されます。
