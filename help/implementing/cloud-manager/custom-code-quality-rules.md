---
title: カスタムコード品質ルール
description: このページでは、[ コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。 これらは、AEM Engineering のベストプラクティスに基づいています。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: ee45ba3a03f9ab5461a09188888694ca22a11b20
workflow-type: tm+mt
source-wordcount: '3495'
ht-degree: 50%

---

# カスタムコード品質ルール {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="カスタムコード品質ルール"
>abstract="このページでは、コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。 これらは、AEM Engineering のベストプラクティスに基づいています。"

このページでは、Cloud Manager が [コード品質テスト。](/help/implementing/cloud-manager/code-quality-testing.md) これらは、AEM Engineering のベストプラクティスに基づいています。

>[!NOTE]
>
>ここで提供されるコードサンプルは、例としてのみ使用されています。SonarQube を参照してください。 [概念ドキュメント](https://docs.sonarqube.org/7.4/user-guide/concepts/) を参照して、SonarQube の概念と品質ルールについて学んでください。

## SonarQube ルール {#sonarqube-rules}

以下の節では、Cloud Manager で実行される SonarQube ルールについて説明します。

### 問題が発生する可能性がある関数は使用しない {#do-not-use-potentially-dangerous-functions}

* **キー**：CQRules:CWE-676
* **タイプ**：脆弱性
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

メソッド `Thread.stop()` および `Thread.interrupt()` は再現が困難な問題を引き起こし、場合によってはセキュリティの脆弱性を引き起こす可能性があります。 その使用状況は、厳密に監視および検証する必要があります。一般的に、似た目標を達成するにはメッセージを渡すとより安全です。

#### 準拠していないコード {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### 準拠しているコード {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### 外部で制御できる可能性のある書式指定文字列を使用しない {#do-not-use-format-strings-which-may-be-externally-controlled}

* **キー**：CQRules:CWE-134
* **タイプ**：脆弱性
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

外部ソース（リクエストパラメーターやユーザー生成コンテンツなど）の書式指定文字列を使用すると、アプリケーションが DoS 攻撃にさらされる可能性があります。書式指定文字列は外部で制御できる場合がありますが、信頼できるソースからのみ許可されます。

#### 準拠していないコード {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP 要求には常にソケットおよび接続タイムアウトが必要 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **キー**：CQRules:ConnectionTimeoutMechanism
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2018.6.0

AEM アプリケーション内から HTTP 要求を実行する場合、不要なスレッドの使用を防ぐために、適切なタイムアウトが設定されていることを確認することが重要です。残念ながら、Java のデフォルト HTTP クライアント (`java.net.HttpUrlConnection`) と一般的に使用される Apache HTTP Components クライアントはタイムアウトしないので、タイムアウトを明示的に設定する必要があります。 また、ベストプラクティスとして、これらのタイムアウトは 60 秒以内にする必要があります。

#### 準拠していないコード {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### 準拠しているコード {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### ResourceResolver オブジェクトを常に閉じる必要がある {#resourceresolver-objects-should-always-be-closed}

* **キー**：CQRules:CQBP-72
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

`ResourceResolver` ～から得られる物体 `ResourceResolverFactory` システムリソースを消費します。 ただし、 `ResourceResolver` は使用されなくなったので、開いているすべてのを明示的に閉じるほうが効率的です `ResourceResolver` オブジェクトを `close()` メソッド。

一つの比較的一般的な誤解は `ResourceResolver` 既存の JCR セッションを使用して作成されたオブジェクトは、明示的に閉じないでください。閉じると、基になる JCR セッションが閉じられます。 そうではありません。 どのように `ResourceResolver` が開いている場合は、使用されなくなったら閉じる必要があります。 次以降 `ResourceResolver` を実装する `Closeable` インターフェイス、 `try-with-resources` 明示的にを呼び出す代わりの構文 `close()`.

#### 準拠していないコード {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 準拠しているコード {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Sling サーブレットパスを使用してサーブレットを登録しない {#do-not-use-sling-servlet-paths-to-register-servlets}

* **キー**：CQRules:CQBP-75
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

[Sling ドキュメント](http://sling.apache.org/documentation/the-sling-engine/servlets.html)で説明されているように、パスによってサーブレットをバインドすることは推奨されません。パスバインドサーブレットでは、標準 JCR アクセス制御を使用できないので、追加のセキュリティをより厳格にする必要があります。パスバインドサーブレットを使用する代わりに、リポジトリーにノードを作成し、リソースタイプによってサーブレットを登録することをお勧めします。

#### 準拠していないコード {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### キャッチされた例外は、ログまたはスローする必要がある（両方ではない） {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **キー**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

一般に、例外は 1 回だけログに記録する必要があります。複数回ログに記録すると、例外が発生した回数がわからなくなるので、混乱が生じる可能性があります。最も一般的なパターンは、キャッチされた例外をログに記録してスローすることです。

#### 準拠していないコード {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### 準拠しているコード {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### ログステートメントの直後にスローステートメントを使用しない {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **キー**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

もうひとつの避けるべき一般的なパターンは、メッセージをログに記録してからすぐに例外をスローすることです。これは一般に、ログファイルで例外メッセージが重複することを示します。

#### 準拠していないコード {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 準拠しているコード {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### GETまたはHEAD要求を処理する際の INFO でのログの回避 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **キー**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **タイプ**：コードスメル
* **深刻度**：軽度

一般的に、INFO ログレベルは重要なアクションを区切るために使用し、デフォルトでは、AEM は INFO レベル以上をログに記録するように設定されています。GET および HEAD メソッドは読み取り専用操作に過ぎず、重要なアクションを構成しません。GET または HEAD 要求に応答して INFO レベルでログに記録すると、大量のログノイズが作成されるので、ログファイル内の有用な情報を特定するのが難しくなります。GET または HEAD 要求処理時のログへの記録は、WARN または ERROR レベル（問題が発生した場合）、または、DEBUG または TRACE レベル（詳細なトラブルシューティング情報が役立つ可能性がある場合）で行います。

>[!NOTE]
>
>これは、 `access.log`各リクエストの —type ログ。

#### 準拠していないコード {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 準拠しているコード {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Logging ステートメントの最初のパラメーターとして Exception.getMessage() を使用しない {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **キー**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

ベストプラクティスとして、ログメッセージは、アプリケーション内での問題の発生場所に関するコンテキスト情報を提供する必要があります。また、スタックトレースを使用してコンテキストを判断することもできます。これにより、一般的にログメッセージが読みやすく、わかりやすくなります。その結果、例外をログに記録する場合、例外のメッセージをログメッセージとして使用するのは悪い方法です。例外メッセージには、何が起こったかが含まれますが、ログメッセージは、例外が発生したときにアプリケーションが何を実行したかをログリーダーに伝えるために使用する必要があります。 例外メッセージは、引き続きログに記録されます。独自のメッセージを指定すると、ログがわかりやすくなります。

#### 準拠していないコード {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 準拠しているコード {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Catch ブロックのログは WARN または ERROR レベルにする {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **キー**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

名前が示すように、Java の例外は常に例外的な状況で使用する必要があります。その結果、例外がキャッチされた場合、ログメッセージが適切なレベル（WARN または ERROR）で記録されるようにすることが重要です。 これにより、これらのメッセージがログに正しく表示されます。

#### 準拠していないコード {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 準拠しているコード {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### コンソールにスタックトレースを印刷しない {#do-not-print-stack-traces-to-the-console}

* **キー**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

既に述べたように、コンテキストはログメッセージを理解する場合に重要です。使用 `Exception.printStackTrace()` を指定すると、スタックトレースのみが標準エラーストリームに出力されるので、すべてのコンテキストが失われます。 さらに、AEMのようなマルチスレッドアプリケーションでは、このメソッドを同時に使用して複数の例外が印刷される場合、スタックトレースが重なり、大きな混乱を招く可能性があります。 例外は、ログフレームワークによってのみ記録される必要があります。

#### 準拠していないコード {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 準拠しているコード {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 標準出力または標準エラーに出力しない {#do-not-output-to-standard-output-or-standard-error}

* **キー**：CQRules:CQBP-44—LogLevelConsolePrinters
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

AEM にログインする場合は、常にログフレームワーク（SLF4J）を使用してログインする必要があります。標準出力または標準エラーストリームに直接出力すると、ログフレームワークによって提供される構造およびコンテキスト情報が失われ、場合によってはパフォーマンスの問題が発生することがあります。

#### 準拠していないコード {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 準拠しているコード {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### /apps および /libs パスをハードコーディングしない  {#avoid-hardcoded-apps-and-libs-paths}

* **キー**：CQRules:CQBP-71
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

一般に、 `/libs` および `/apps` を参照するパスは、Sling 検索パスに対する相対パスとして最も一般的に保存されるので、ハードコードしないでください。このパスは、次のように設定されます。 `/libs,/apps` デフォルトでは。 絶対パスを使用すると、プロジェクトライフサイクルの後になって初めて現れるわかりにくい不具合が生じる可能性があります。

#### 準拠していないコード {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 準拠しているコード {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Sling スケジューラーは使用しない {#sonarqube-sling-scheduler}

* **キー**：CQRules:AMSCORE-554
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Sling スケジューラーは、確実な実行を必要とするタスクには使用しないでください。Sling スケジュールジョブは実行を保証し、クラスター化ジョブと非クラスター化環境の両方に適しています。

Sling ジョブがクラスター環境で処理される方法について詳しくは、[Apache Sling Eventing and Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) を参照してください。

### AEMの非推奨 API は使用しない {#sonarqube-aem-deprecated}

* **キー**：AMSCORE-553
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

AEM API の表面は、使用が推奨されず非推奨と見なされる API を識別するために継続的に見直しされます。

多くの場合、これらの API は、標準の Java を使用して非推奨（廃止予定）となっています `@Deprecated` 注釈と、 `squid:CallToDeprecatedMethod`.

ただし、API が AEM のコンテキストで非推奨となるものの、他のコンテキストでは非推奨とならない場合があります。このルールは、この 2 番目のクラスを識別します。


## OakPAL コンテンツルール {#oakpal-rules}

以下の節では、Cloud Manager で実行される OakPAL チェックについて詳しく説明します。

>[!NOTE]
>
>OakPAL は、スタンドアロンの Oak リポジトリを使用してコンテンツパッケージを検証するフレームワークです。 2019 AEM Rockstar North America 賞を受賞したAEM Partner が開発しました。

### @ProviderTypeの注釈が付いた製品 API は、お客様による実装または拡張はできない {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **キー**：CQBP-84
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2018.7.0

AEM API には、カスタムコードによる使用のみ（ただし実装はしない）を意図した Java インターフェイスおよびクラスが含まれています。例えば、インターフェイス `com.day.cq.wcm.api.Page` は、AEM のみによって実装されるように設計されています。

これらのインターフェイスに新しいメソッドが追加される場合、それらの追加メソッドは、これらのインターフェイスを使用する既存のコードには影響しません。その結果、これらのインターフェイスへの新しいメソッドの追加は、後方互換性があると見なされます。ただし、カスタムコードがこれらのインターフェイスのいずれかを実装する場合、そのカスタムコードによってお客様に後方互換性のリスクがもたらされます。

AEMでの実装のみを意図したインターフェイスおよびクラスには、 `org.osgi.annotation.versioning.ProviderType` または、場合によっては、従来の注釈と同様の注釈 `aQute.bnd.annotation.ProviderType`. このルールは、このようなインターフェイスが実装されている場合、またはクラスがカスタムコードで拡張されている場合を識別します。

#### 準拠していないコード {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### カスタム Lucene Oak インデックスには Tika 設定が必要 {#oakpal-indextikanode}

* **キー**：IndexTikaNode
* **タイプ**：バグ
* **重大度**：ブロッカー
* **開始バージョン**：2021.8.0

標準搭載の複数のAEM Oak インデックスには tika 設定が含まれ、これらのインデックスのカスタマイズには tika 設定が含まれている必要があります。 このルールは、 `damAssetLucene`、 `lucene`、`graphqlConfig` インデックスのカスタマイズを確認し、 `tika` ノードがない場合、または `tika` ノードに `config.xml` という名前の子ノードがない場合には問題を報告します。

詳しくは、 [インデックス作成ドキュメント](/help/operations/indexing.md#preparing-the-new-index-definition) インデックス定義のカスタマイズの詳細については、を参照してください。

#### 準拠していないコード {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 準拠しているコード {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### カスタム Lucene Oak インデックスは同期にできません {#oakpal-indexasync}

* **キー**：IndexAsyncProperty
* **タイプ**：バグ
* **重大度**：ブロッカー
* **開始バージョン**：2021.8.0

タイプの Oak インデックス `lucene` は常に非同期でインデックスを作成する必要があります。 これに従わないと、システムが不安定になる可能性があります。Lucene インデックスの構造について詳しくは、 [Oak ドキュメント。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### 準拠していないコード {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

#### 準拠しているコード {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### カスタム DAM Asset Lucene Oak インデックスが正しく構造化されている  {#oakpal-damAssetLucene-sanity-check}

* **キー**：IndexDamAssetLucene
* **タイプ**：バグ
* **重大度**：ブロッカー
* **開始バージョン**：2021.6.0

AEM Assets でアセット検索が正しく機能するようにするには、`damAssetLucene` Oak インデックスのカスタマイズはこのインデックスに固有の一連のガイドラインに従う必要があります。このルールは、インデックス定義に、という名前の複数の値を持つプロパティが必要かどうかをチェックします。 `tags` 値を含む `visualSimilaritySearch`.

#### 準拠していないコード {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      + tika
        + config.xml
```

#### 準拠しているコード {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 顧客パッケージでは /libs 下のノードを作成／変更しない {#oakpal-customer-package}

* **キー**:BannedPath
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2019.6.0

これは長い間のベストプラクティスでした `/libs` AEMコンテンツリポジトリーのコンテンツツリーは、顧客は読み取り専用と見なす必要があります。 以下のノードおよびプロパティの変更 `/libs` は、メジャーアップデートとマイナーアップデートの際に重大なリスクを引き起こします。 変更先 `/libs` は、公式チャネルを通じてのみAdobeによって作成される必要があります。

### パッケージには重複する OSGi 設定を含めない {#oakpal-package-osgi}

* **キー**：DuplicateOsgiConfigurations
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

複雑なプロジェクトでよく発生する問題は、同じ OSGi コンポーネントが複数回設定されることです。これにより、どの設定が適用されるかがあいまいになります。 このルールは「実行モード対応」です。つまり、同じ実行モードまたは実行モードの組み合わせで同じコンポーネントが複数回設定される問題のみを識別します。

>[!NOTE]
>
>このルールの結果、ビルド済みパッケージのリスト全体で同じパッケージが重複する場合など、同じパスの同じ設定が複数のパッケージで定義される問題が発生します。
>
>例えば、ビルドで `com.myco:com.myco.ui.apps` と `com.myco:com.myco.all` というパッケージが生成され、`com.myco:com.myco.ui.apps` が `com.myco:com.myco.all` に組み込まれている場合、`com.myco:com.myco.ui.apps` 内のすべての設定が重複としてレポートされます。
>
>これは、通常、 [コンテンツパッケージ構造のガイドライン](/help/implementing/developing/introduction/aem-project-content-package-structure.md)」を選択します。この例では、パッケージ `com.myco:com.myco.ui.apps` が見つからない `<cloudManagerTarget>none</cloudManagerTarget>` プロパティ。

#### 準拠していないコード {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 準拠しているコード {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### /config および /install フォルダーには OSGi ノードのみ含める  {#oakpal-config-install}

* **キー**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

セキュリティ上の理由から、パスには `/config/` および `/install/` は、AEMの管理者ユーザーのみが読み取り可能で、OSGi 設定および OSGi バンドルにのみ使用してください。 これらのセグメントを含むパスの下に他のタイプのコンテンツを配置すると、アプリケーションの動作が管理者ユーザーと非管理者ユーザーとで意図せず異なることになります。

よくある問題としては、コンポーネントダイアログ内や、インライン編集にリッチテキストエディター設定を指定する際に、`config` というノードを使用するケースがあります。これを解決するには、問題のあるノードを適切な名前に変更する必要があります。リッチテキストエディター設定については、`cq:inplaceEditing` ノードの `configPath` プロパティを使用して新しい場所を指定します。

#### 準拠していないコード {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 準拠しているコード {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### パッケージは重複しない {#oakpal-no-overlap}

* **キー**：PackageOverlaps
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

次に類似 [パッケージには重複する OSGi 設定ルールを含めない、](#oakpal-package-osgi) これは、同じノードパスが複数の個別のコンテンツパッケージによって書き込まれる複雑なプロジェクトでの一般的な問題です。 コンテンツパッケージの依存関係を使用すると、一貫性のある結果を得ることができますが、その際には、パッケージがまったく重複しないようにすることをお勧めします。

### デフォルトのオーサリングモードをクラシック UI にしない {#oakpal-default-authoring}

* **キー**：ClassicUIAuthoringMode
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` は、AEM 内でデフォルトのオーサリングモードを定義します。理由： [クラシック UI は、AEM 6.4 以降、非推奨（廃止予定）となりました。](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) デフォルトのオーサリングモードがクラシック UI に設定されている場合、問題が発生するようになりました。

### タッチ UI ダイアログが必要なダイアログを持つコンポーネント {#oakpal-components-dialogs}

* **キー**：ComponentWithOnlyClassicUIDialog
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

最適なオーサリングエクスペリエンスを提供し、クラシック UI がサポートされていないCloud Serviceデプロイメントモデルとの互換性を保つために、クラシック UI ダイアログを持つAEMコンポーネントには常に対応するタッチ UI ダイアログを持つ必要があります。 このルールは、次のシナリオを検証します。

* クラシック UI ダイアログ ( `dialog` 子ノード ) には、対応するタッチ UI ダイアログ ( つまり、 `cq:dialog` 子ノード ) です。
* クラシック UI デザインダイアログを含むコンポーネント ( `design_dialog` ノード ) には、対応するタッチ UI デザインダイアログ ( つまり、 `cq:design_dialog` 子ノード ) です。
* クラシック UI ダイアログとクラシック UI デザインダイアログの両方を持つコンポーネントには、対応するタッチ UI ダイアログと対応するタッチ UI デザインダイアログの両方が必要です。

AEM 最新化ツールのドキュメントには、コンポーネントをクラシック UI からタッチ UI に変換する方法に関するドキュメントとツールが記載されています。詳しくは、 [AEM Modernization Tools ドキュメント](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) を参照してください。

### 可変コンテンツと不変コンテンツをパッケージに混在させない {#oakpal-packages-immutable}

* **キー**：ImmutableMutableMixedPackage
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Cloud Serviceデプロイメントモデルとの互換性を保つには、個々のコンテンツパッケージに、リポジトリの不変領域 ( つまり、 `/apps` および `/libs`) または可変領域 ( つまり、 `/apps` または `/libs`) ですが、両方ではありません。 例えば、`/apps/myco/components/text and /etc/clientlibs/myco` の両方を含むパッケージは Cloud Service と互換性がなく、問題が報告されます。

>[!NOTE]
>
>ルール [顧客パッケージでは/libs 下のノードを作成または変更しない](#oakpal-customer-package) 常に適用されます。

詳しくは、[AEM プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)を参照してください。

### リバースレプリケーションエージェントは使用しない {#oakpal-reverse-replication}

* **キー**：ReverseReplication
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

AEM as a Cloud Serviceの [リリースノート。](/help/release-notes/aem-cloud-changes.md#replication-agents)

リバースレプリケーションを使用するお客様は、アドビに問い合わせて、代替ソリューションをご利用ください。

### プロキシが有効なクライアントライブラリに含まれるリソースは、 Resources という名前のフォルダーに格納する必要があります {#oakpal-resources-proxy}

* **キー**：ClientlibProxyResource
* **タイプ**：バグ
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEM クライアントライブラリには、画像やフォントなどの静的なリソースが含まれる場合があります。このドキュメントの説明に従って [プリプロセッサの使用](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) プロキシ化されたクライアントライブラリを使用する場合、これらの静的リソースは、 `resources` パブリッシュインスタンスで効果的に参照するために。

#### 準拠していないコード {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 準拠しているコード {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Cloud Service と互換性のないワークフロープロセスの使用 {#oakpal-usage-cloud-service}

* **キー**：CloudServiceIncompatibleWorkflowProcess
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2021.2.0

AEM as a Cloud Service上でのアセット処理用のアセットマイクロサービスに移行すると、オンプレミスおよび AMS バージョンのAEMで使用されていたいくつかのワークフロープロセスが、サポート対象外または不要になります。

移行ツール ( [AEM Assetsas a Cloud ServiceGitHub リポジトリ](https://github.com/adobe/aem-cloud-migration) は、AEM as a Cloud Serviceへの移行中にワークフローモデルを更新するために使用できます。

### 静的なテンプレートより編集可能なテンプレートを使用する {#oakpal-static-template}

* **キー**：StaticTemplateUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

従来、AEM プロジェクトは静的テンプレートを使用することが一般的でしたが、編集可能なテンプレートは最も柔軟性が高く、静的なテンプレートにはない追加機能をサポートしているため、このテンプレートの使用を強くお勧めします。詳しくは、 [ページテンプレート。](/help/implementing/developing/components/templates.md)

静的テンプレートから編集可能テンプレートへの移行は、 [AEM Modernization Tools.](https://opensource.adobe.com/aem-modernize-tools/)

### 従来の基盤コンポーネントの使用は推奨されない {#oakpal-usage-legacy}

* **キー**：LegacyFoundationComponentUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

従来の基盤コンポーネント（例：下のコンポーネント） `/libs/foundation`) は [一部のAEMリリースで非推奨（廃止予定）](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) コアコンポーネントに優先して カスタムコンポーネントの基礎としての基盤コンポーネントの使用（オーバーレイによる場合も継承による場合も）は推奨されず、対応するコアコンポーネントに変換する必要があります。

この変換は、 [AEM Modernization Tools.](https://opensource.adobe.com/aem-modernize-tools/)

### サポートされている実行モード名および順序のみを使用する {#oakpal-supported-runmodes}

* **キー**：SupportedRunmode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEM as a Cloud Serviceでは、実行モード名に対して厳密な命名ポリシーを適用し、それらの実行モードに対して厳密な順序を指定します。 サポートされている実行モードのリストは、このドキュメントに記載されています [AEMへのデプロイ (as a Cloud Service)](/help/implementing/deploying/overview.md#runmodes) これから逸脱した場合は、問題として識別されます。

### カスタム検索インデックス定義ノードは、/oak:index の直接の子にする {#oakpal-custom-search}

* **キー**：OakIndexLocation
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEM as a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプのノード）が必要です。 `oak:QueryIndexDefinition`) の直接の子ノード `/oak:index`. 他の場所のインデックスは、AEM as a Cloud Serviceとの互換性を保つために移動する必要があります。 検索インデックスの詳細については、ドキュメントを参照してください。 [コンテンツの検索とインデックス作成。](/help/operations/indexing.md)

### カスタム検索インデックス定義ノードの compatVersion は 2 にする {#oakpal-custom-search-compatVersion}

* **キー**：IndexCompatVersion
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEM as a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプのノード）が必要です。 `oak:QueryIndexDefinition`) には、 `compatVersion` プロパティを `2`. その他の値は、AEM as a Cloud Serviceではサポートされません。 検索インデックスの詳細については、 [コンテンツの検索とインデックス作成。](/help/operations/indexing.md)

### カスタム検索インデックス定義ノードの子孫ノードのタイプは、nt:unstructured にする {#oakpal-descendent-nodes}

* **キー**：IndexDescendantNodeType
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

カスタムの検索インデックス定義ノードに、順序が指定されていない子ノードがある場合、問題のトラブルシューティングが難しくなる可能性があります。この状況を回避するには、 `oak:QueryIndexDefinition` ノードのタイプは `nt:unstructured`.

### カスタム検索インデックス定義ノードには、子を持つ indexRules という名前の子ノードが含まれている必要があります {#oakpal-custom-search-index}

* **キー**：IndexRulesNode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

適切に定義されたカスタム検索インデックス定義ノードには、という名前の子ノードが含まれている必要があります。 `indexRules` その子は、次に少なくとも一人の子を持つ必要がある。 詳しくは、 [Oak ドキュメント。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### カスタム検索インデックス定義ノードは命名規則に従う {#oakpal-custom-search-definitions}

* **キー**：IndexName
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEM as a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプのノード）が必要です。 `oak:QueryIndexDefinition`) には、ドキュメントで説明されている特定のパターンに従って名前を付ける必要があります [コンテンツの検索とインデックス作成。](/help/operations/indexing.md)

### カスタム検索インデックス定義ノードは、インデックスタイプ lucene を使用する必要があります  {#oakpal-index-type-lucene}

* **キー**：IndexType
* **タイプ**：バグ
* **重大度**：ブロッカー
* **最初の対象バージョン**：バージョン2021.2.0（2021.8.0でタイプと重大度が変更されました）

AEM as a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプのノード）が必要です。 `oak:QueryIndexDefinition`) が `type` プロパティの値を次に設定 `lucene`. 従来のインデックスタイプを使用するインデックス作成は、AEM as a Cloud Serviceに移行する前に更新する必要があります。 ドキュメントを参照 [コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use) を参照してください。

### カスタム検索インデックス定義ノードに seed という名前のプロパティを含めない {#oakpal-property-name-seed}

* **キー**：IndexSeedProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEMas a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプがのノード）は禁止されています `oak:QueryIndexDefinition`) に、 `seed`. AEM as a Cloud Serviceに移行する前に、このプロパティを使用するインデックス作成を更新する必要があります。 ドキュメントを参照 [コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use) を参照してください。

### カスタム検索インデックス定義ノードに reindex という名前のプロパティを含めない {#oakpal-reindex-property}

* **キー**：IndexReindexProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

AEMas a Cloud Serviceでは、カスタム検索インデックス定義（つまり、タイプがのノード）は禁止されています `oak:QueryIndexDefinition`) に、 `reindex`. AEM as a Cloud Serviceに移行する前に、このプロパティを使用するインデックス作成を更新する必要があります。 ドキュメントを参照 [コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use) を参照してください。
