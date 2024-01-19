---
title: Sling Model Exporter を使用した ResourceResolvers のシリアル化を許可しない
description: Sling Model Exporter を使用した ResourceResolvers のシリアル化を許可しない
source-git-commit: 4543a4646719f8433df7589b21344433c43ab432
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Sling Model Exporter を使用した ResourceResolvers のシリアル化を許可しない {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling Model Exporter 機能を使用すると、Sling Models オブジェクトを JSON 形式にシリアライズできます。 この機能は、SPA（シングルページアプリケーション）がAEMからのデータに簡単にアクセスできるようにするので、広く使用されています。 実装側では、Jacson Databind ライブラリを使用してこれらのオブジェクトをシリアライズします。

シリアル化は再帰的な操作です。 &quot;root object&quot;から始まり、すべての対象オブジェクトを再帰的に反復し、それらとその子をシリアル化します。 シリアル化されるフィールドの説明を検索できます [この記事](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

このアプローチは、すべてのタイプのオブジェクトを JSON にシリアル化します。当然、Sling をシリアル化することもできます `ResourceResolver` オブジェクトを返します。 これは問題がある。 `ResourceResolver` サービス（したがって、それを表すサービスオブジェクト）には、開示すべきでない、潜在的に機密情報が含まれています。 次に例を示します。

* ユーザー ID
* 相対パスを解決する検索パス
* The `propertyMap`.

特に、 `propertyMap` （ API ドキュメントを参照） [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)) は内部データ構造なので、多くの目的で使用できます。例えば、 `ResourceResolver`. これらをシリアル化すると、読み取りやエンドユーザーにアクセスできないデータが公開されるので、実装の詳細が漏洩し、セキュリティに影響を与える可能性があります。 その理由で `ResourceResolvers` は JSON にシリアル化しないでください。

Adobeは、のシリアル化を無効にする予定です `ResourceResolvers` 2 段階アプローチ：

1. AEMas a Cloud Serviceリリース14697以降 ( `ResourceResolver` がシリアル化されたAEMでは、警告メッセージがログに記録されます。 すべてのお客様は、アプリケーションログでこれらのログ文を確認し、それに応じてコードベースを調整することをお勧めします。
1. 後でAdobeすると、ResourceResolvers のシリアル化が JSON として無効になります。

## 実装 {#implementation}

WARN メッセージは、AEM as a Cloud ServiceとローカルAEM SDK の両方のインスタンスに記録され、次のようになります。

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

このログメッセージは、 `/content/…/page` を JSON a に `ResourceResolver` は既にシリアル化されています。 次をリクエストして `/content/../page.model.json` 正確に `ResourceResolver` が表示され、これを使用して、実際にこの動作をトリガーしている Sling Model クラスを識別します。


>[!NOTE]
>
>AEMコアコンポーネントは、この問題の影響を受けないことが検証されました。

## 要求されたアクション {#requested-action}

Adobeは、すべてのお客様に対し、この問題の影響を受けているかどうかを確認し、必要に応じてカスタムアプリケーションを変更するよう要求します。これにより、この WARN メッセージが表示されなくなります。

ほとんどの場合、これらの必要な変更は、 `ResourceResolver` オブジェクトは、JSON 出力ではまったく必要ありません。含まれる情報は通常、フロントエンドアプリケーションでは必要ありません。 つまり、ほとんどの場合、 `ResourceResolver` ジャクソンによって考慮されない対象 ( [ルール](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)) をクリックします。

Sling モデルがこの問題の影響を受けるが変更されない場合、 `ResourceResolver` オブジェクト (2 番目の手順としてAdobeが実行 ) は、JSON 出力に変更を加えます。



