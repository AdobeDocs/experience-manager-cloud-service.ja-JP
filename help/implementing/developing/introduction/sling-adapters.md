---
title: Sling アダプターの使用
description: Sling には、Adaptable インターフェイスを実装するオブジェクトを適切に変換するアダプターパターンが用意されています
translation-type: tm+mt
source-git-commit: 639bf1add463c0e62982a44ecdca834e2c7c53fe
workflow-type: tm+mt
source-wordcount: '2234'
ht-degree: 72%

---


# Sling アダプターの使用 {#using-sling-adapters}

[Sling](https://sling.apache.org) は、[Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) インターフェイスを実装するオブジェクトを簡単に変換するための [Adapter パターン](https://sling.apache.org/site/adapters.html)を提供します。このインターフェイスは、汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供しており、このメソッドによってオブジェクトは引数として渡されるクラス型に変換されます。

例えば、次のように実行するだけで、Resource オブジェクトを対応する Node オブジェクトに変換できます。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装用のオブジェクトの取得

   例えば、汎用の [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) インターフェイスの JCR ベース実装では、基盤の JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) にアクセスできます。

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

   例えば、JCR ベースの [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) では、要求の [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) への参照を保持しています。この JCR セッションは、その要求セッションに基づいて動作する多くのオブジェクト（[`PageManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) や [`UserManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html) など）を取得するために必要になります。

* サービスへのショートカット。

   稀なケース - `sling.getService()` も簡単に使用できます。

### 戻り値 Null {#null-return-value}

`adaptTo()` は null を返す場合があります。

これには様々な理由がありますが、その一部は次のとおりです。

* 実装がターゲットタイプをサポートしていない
* このケースを処理するアダプターファクトリがアクティブでない（サービスの参照が見つからないなどの理由で）
* 内部的な条件が合わなかった
* サービスを利用できない

null のケースを問題なく処理することが重要です。JSP レンダリングでは、JSP の問題によってコンテンツの一部が空になる場合に、その問題が受容されることもあります。

### キャッシュ {#caching}

パフォーマンスを改善する目的で、各実装では `obj.adaptTo()` 呼び出しから返されたオブジェクトを自由にキャッシュできます。`obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、汎用的なルールは存在せず、オブジェクトが新しいインスタンスである場合も既存のインスタンスである場合もあります。したがって、いずれの動作にも依存することはできません。重要なのは、特に `AdapterFactory` 内部において、このシナリオでオブジェクトが再利用可能であるということです。

### 仕組み {#how-it-works}

`Adaptable.adaptTo()` の実装には、様々な方法があります。

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html) を使用。これは、任意のオブジェクトをマッピングできます。

   オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、[`SlingAdaptable`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/adapter/SlingAdaptable.html) を拡張する必要があります（これは、Central Adapter Manager の `adaptTo` 呼び出しを渡します）。

   これにより、`Resource` などの既存クラスの `adaptTo` メカニズムにフックを組み込むことができます。

* これら 2 つの組み合わせ。

最初の例では、javadocs に何の `adaptTo-targets` が可能かが示されます。ただし、JCR ベースのリソースなどの特定のサブクラスでは、多くの場合、これは不可能です。後者の場合、`AdapterFactory` の実装は通常、バンドルのプライベートクラスの一部なので、クライアント API で公開されず、Javadoc にも表示されません。理論的には、[OSGi](/help/implementing/deploying/configuring-osgi.md) サービスランタイムからすべての `AdapterFactory` 実装にアクセスし、「アダプタブル」（ソースとターゲット）の設定を調べることは可能ですが、相互にマッピングすることはできません。最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。従って、参照はこちらです。

## リファレンス {#reference}

### Sling {#sling}

[**Resource**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>このリソースが JCR ノードベースのリソースまたはノードを参照する JCR プロパティの場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Property</a></td>
   <td>このリソースが JCR プロパティベースのリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td>
   <td>このリソースが JCR ベースのリソース（ノードまたはプロパティ）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Map</a></td>
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティのマップを返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティの使用しやすいマップを返します。また、<br /> <code><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> を使用（null ケースを処理するなど）して達成することもできます。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> の拡張。プロパティを探すときにリソースの階層を考慮することができます。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> の拡張です。そのノードのプロパティを変更できます。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>ファイルリソースのバイナリコンテンツ（このリソースが JCR ノードベースのリソースでありノードタイプが <code>nt:file</code> または <code>nt:resource</code> の場合。このリソースがバンドルリソースの場合。このリソースがファイルシステムリソースの場合はファイルコンテンツ）
またはバイナリ JCR プロパティリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>リソースの URL を返します（このリソースが JCR ノードベースのリソースの場合は、このノードのリポジトリ URL。このリソースがバンドルリソースの場合は JAR バンドル URL。このリソースがファイルシステムリソースの場合はファイル URL）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">File</a></td>
   <td>このリソースがファイルシステムリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（JSP ファイルなど）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（JSP ファイルなど）である場合、またはこのリソースがサーブレットリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">String</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">
Boolean</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">
Long</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html">
Double</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">
Calendar</a><br /><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">
Value</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">
String[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">
Boolean[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">
Long[]</a><br /><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">
Calendar[]</a><br /><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">
Value[]</a></td>
   <td>このリソースが JCR プロパティベースのリソースである（および値が適合する）場合、その値を返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html">ページ</a></td>
   <td>このリソースが JCR ノードベースのリソースであり、ノードが <code>cq:Page</code>（または <code>cq:PseudoPage</code>）である場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html">コンポーネント</a></td>
   <td>このリソースが <code>cq:Component</code> ノードリソースである場合。</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Design.html">デザイン</a></td>
   <td>このノードが設計ノード（<code>cq:Page</code>）である場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html">テンプレート</a></td>
   <td>このリソースが <code>cq:Template</code> ノードリソースである場合。</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/msm/api/Blueprint.html">ブループリント</a></td>
   <td>このリソースが <code>cq:Template</code> ノードリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Asset.html">Asset</a></td>
   <td>このリソースが dam:Asset ノードリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td>このリソースが dam:Asset レンディション（dam:Assert の rendition フォルダー以下にある nt:file）である場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/Tag.html">タグ</a></td>
   <td>このリソースが <code>cq:Tag</code> ノードリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>このリソースが JCR ベースのリソースであり、ユーザーが UserManager へのアクセス権限を持っている場合の、JCR セッションに基づいたもの。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a></td>
   <td>Authorizable は、User と Group の共通の基本インターフェイスです。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>User は、認証済みであり、偽装可能な特別な Authorizable です。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>このリソースが JCR ベースのリソースである場合、このリソース以下で検索します（または setSearchIn() を使用します）。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>特定のページまたはワークフローのペイロードノード用のワークフローステータス。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>特定のリソースまたはその jcr:content サブノード（最初にチェックされたもの）のレプリケーションステータス。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合、特定のタイプに対する適応後のコネクタリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>このリソースが <code>cq:ContentSyncConfig</code> ノードリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>このリソースが <code>cq:ContentSyncConfig</code> ノードリソース以下にある場合。</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceResolver.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバー（デフォルト）である場合の、要求の JCR セッション。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Designer.html">デザイナー</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づいたもの。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づいたもの。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager は、承認可能なオブジェクト（ユーザーやグループ）へのアクセス権と手段を提供します。UserManager は特定のセッションにバインドされています。
   </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a><br /> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>要求オブジェクトがない場合でも、絶対 URL を外部化するためのもの。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletRequest.html) は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletResponse.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />
（XML）</td>
   <td>この応答が Sling リライター応答である場合。</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Page](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>ページのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソース（== this）。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>ページのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>ページのリソースが適応可能なすべての項目。</td>
  </tr>
 </tbody>
</table>

**[Component](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html)** は次の項目に適応します。

| [Resource](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース。 |
|---|---|
| [LabeledResource](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソース（== this）。 |
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード。 |
| ... | コンポーネントのリソースが適応可能なすべての項目。 |

**[Template](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>テンプレートのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソース（== this）。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>このテンプレートのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>テンプレートのリソースが適応可能なすべての項目。</td>
  </tr>
 </tbody>
</table>

#### セキュリティ {#security}

**Authorizable**、**User** および **Group** は以下に適応します。

| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | ユーザーまたはグループのホームノードを返します。 |
|---|---|
| [ReplicationStatus](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザーまたはホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

**Asset** は次の項目に適応します。

| [Resource](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応可能なすべての項目。 |

#### タグ付け {#tagging}

**Tag** は次の項目に適応します。

| [Resource](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応可能なすべての項目。 |

#### その他 {#other}

さらに、Sling、JCR、OCM では、カスタム OCM（[`AdapterFactory`](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)Object Content Mapping）オブジェクト用の [](https://jackrabbit.apache.org/object-content-mapping.html) も提供しています。
