---
title: Sling アダプターの使用
description: Sling には、Adaptable インターフェイスを実装するオブジェクトを適切に変換するアダプターパターンが用意されています
translation-type: tm+mt
source-git-commit: 4d41f18fea1984f64e85df6b06602426c3602efa
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 43%

---


# Sling アダプターの使用 {#using-sling-adapters}

[Sling](https://sling.apache.org) オファーと [Adapterパターン](https://sling.apache.org/site/adapters.html) 。Adaptable [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) インターフェイスを実装するオブジェクトを簡単に変換します。 このインターフェイスは、オブジェクトを引数として渡されるクラス型に変換する汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供します。

例えば、次のように実行するだけで、Resource オブジェクトを対応する Node オブジェクトに変換できます。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装固有のオブジェクトを取得します。

   For example, a JCR-based implementation of the generic [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) interface provides access to the underlying JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

   例えば、JCR ベースの [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) では、要求の [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) への参照を保持しています。この JCR Session は、その要求セッションに基づいて動作する多くのオブジェクト（[`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) や [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html) など）を取得するために必要になります。

* サービスへのショートカット。

   A rare case - `sling.getService()` is simple as well.

### 戻り値 Null {#null-return-value}

`adaptTo()` はnullを返すことができます。

これには様々な理由がありますが、その一部は次のとおりです。

* 実装がターゲットタイプをサポートしていない
* このケースを処理するアダプターファクトリがアクティブでない（サービスの参照が見つからないなどの理由で）
* 内部的な条件が合わなかった
* サービスを利用できない

null のケースを問題なく処理することが重要です。JSP レンダリングでは、JSP の問題によってコンテンツの一部が空になる場合に、その問題が受容されることもあります。

### キャッシュ {#caching}

To improve performance, implementations are free to cache the object returned from a `obj.adaptTo()` call. `obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、汎用的なルールは存在せず、オブジェクトが新しいインスタンスである場合も既存のインスタンスである場合もあります。したがって、いずれの動作にも依存することはできません。重要なのは、特に `AdapterFactory` 内部において、このシナリオでオブジェクトが再利用可能であるということです。

### 仕組み {#how-it-works}

There are various ways that `Adaptable.adaptTo()` can be implemented:

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* を使用し [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)て、任意のオブジェクトをマッピングできます。

   オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、拡張する必要があります [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (これは、Central Adapter Managerへの `adaptTo` 呼び出しを渡します)。

   これにより、などの既存のクラスの `adaptTo` メカニズムにフックを組み込むことができ `Resource`ます。

* これら 2 つの組み合わせ。

最初の例では、javadocsに何が可能かが示され `adaptTo-targets` ます。 ただし、JCRベースのリソースなどの特定のサブクラスでは、多くの場合、これは不可能です。 後者の場合、の実装は通常、バンドルのプライベートクラスの一部 `AdapterFactory` なので、クライアントAPIで公開されず、javadocにも表示されません。 理論的には、 `AdapterFactory` OSGi [サービスランタイムからすべての](/help/implementing/deploying/configuring-osgi.md) 実装にアクセスし、「アダプティブテーブル」(ソースとターゲット)の設定を調べることは可能ですが、相互にマッピングすることはできません。 最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。 従って、この参照。

## リファレンス {#reference}

### Sling {#sling}

[**Resource **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>JCRノードベースのリソース、またはノードを参照するJCRプロパティの場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">プロパティ</a></td>
   <td>このリソースが JCR プロパティベースのリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>このリソースが JCR ベースのリソース（ノードまたはプロパティ）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">マップ</a></td>
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティのマップを返します。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCRノードベースのリソース（または他のリソースサポート値マップ）の場合、プロパティの使いやすいマップを返します。 また、<br /> (ヌルケースを処理するなど <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> )を使用して達成することもできます。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extension of <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> which allows the hierarchy of resources to be taken into account when looking for properties.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>ValueMapの拡張子です。 <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>では、そのノードのプロパティを変更できます。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Returns the binary content of a file resource (if this is a JCR-node-based resource and the node type is <code>nt:file</code> or <code>nt:resource</code>; if this is a bundle resource; file content if this is a file system resource) or the data of a binary JCR property resource.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>リソースの URL を返します（このリソースが JCR ノードベースのリソースの場合は、このノードのリポジトリ URL。このリソースがバンドルリソースの場合は JAR バンドル URL。このリソースがファイルシステムリソースの場合はファイル URL）。</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">ファイル</a></td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html">アセットの</a></td>
   <td>このリソースが dam:Asset ノードリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td>これがdam:Assetレンディションの場合（dam:Assertのレンディションフォルダーの下のnt:file）</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>このリソースが JCR ベースのリソースであり、ユーザーが UserManager へのアクセス権限を持っている場合の、JCR セッションに基づいたもの。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a></td>
   <td>Authorizableは、UserとGroupの共通の基本インターフェイスです。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a></td>
   <td>Userは、認証済みであり、偽装可能な特別なAuthorizableです。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>このリソースが JCR ベースのリソースである場合、このリソース以下で検索します（または setSearchIn() を使用します）。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>特定のページまたはワークフローのペイロードノード用のワークフローステータス。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>特定のリソースまたはその jcr:content サブノード（最初にチェックされたもの）のレプリケーションステータス。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>このリソースが JCR ノードベースのリソースである場合、特定のタイプに対する適応後のコネクタリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>If this is a <code>cq:ContentSyncConfig</code> node resource.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>If this is below a <code>cq:ContentSyncConfig</code> node resource.</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html):

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバー（デフォルト）である場合の、要求の JCR セッション。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づいたもの。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManagerは、承認可能なオブジェクト（ユーザーやグループ）へのアクセス権と手段を提供します。 UserManagerが特定のセッションにバインドされている。
   </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a><br /> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>要求オブジェクトがない場合でも、絶対 URL を外部化するためのもの。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)は次の項目に適応します。

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

**Page** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>ページのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
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

**Component** は次の項目に適応します。

| [Resource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソース（== this）。 |
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード。 |
| ... | コンポーネントのリソースが適応可能なすべての項目。 |

**Template** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>テンプレートのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
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
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザーまたはホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

**アセット** :

| [Resource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応可能なすべての項目。 |

#### タグ付け {#tagging}

**タグ** :

| [Resource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
|---|---|
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応可能なすべての項目。 |

#### その他 {#other}

さらに、Sling、JCR、OCM では、カスタム OCM（` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`Object Content Mapping）オブジェクト用の [](https://jackrabbit.apache.org/object-content-mapping.html) も提供しています。
