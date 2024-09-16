---
title: カスタムコード品質ルール
description: このページでは、コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Adobe Experience Manager Engineering のベストプラクティスに基づいています。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: ht
source-wordcount: '4513'
ht-degree: 100%

---

# カスタムコード品質ルール {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="カスタムコード品質ルール"
>abstract="このページでは、コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Adobe Experience Manager Engineering のベストプラクティスに基づいています。"

このページでは、[コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)の一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Experience Manager Engineering のベストプラクティスに基づいています。

>[!NOTE]
>
>完全な SonarQube ルールは、アドビ独自の情報が原因でダウンロードできません。ルールの完全なリストをダウンロードするには、[このリンクを使用](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)します。ルールの説明と例については、このドキュメントを引き続き参照してください。

>[!NOTE]
>
>ここで提供されるコードサンプルは、例としてのみ使用されています。SonarQube の概念と品質ルールについて詳しくは、SonarQube の[概念に関するドキュメント](https://docs.sonarqube.org/latest/)を参照してください。

## SonarQube ルール {#sonarqube-rules}

以下の節では、Cloud Manager で実行される SonarQube ルールについて説明します。

### 問題が発生する可能性がある関数は使用しない {#do-not-use-potentially-dangerous-functions}

* **キー**：CQRules:CWE-676
* **タイプ**：脆弱性
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

`Thread.stop()` と `Thread.interrupt()` のメソッドは、再現が困難な問題を引き起こし、場合によってはセキュリティの脆弱性を生み出す可能性があります。その使用状況は、厳密に監視および検証する必要があります。一般的に、似た目標を達成するにはメッセージを渡すとより安全です。

#### 非準拠コード {#non-compliant-code}

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

#### 準拠コード {#compliant-code}

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

#### 非準拠コード {#non-compliant-code-1}

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

Experience Manager アプリケーション内から HTTP 要求を実行する場合、不要なスレッドの消費を防ぐために、適切なタイムアウトが設定されていることを確認することが重要です。ただし、Java™ のデフォルト HTTP クライアント（`java.net.HttpUrlConnection`）および一般的に使用される Apache HTTP コンポーネントクライアントのデフォルトの動作はタイムアウトしないので、タイムアウトを明示的に設定する必要があります。また、ベストプラクティスとして、これらのタイムアウトは 60 秒以内にする必要があります。

#### 非準拠コード {#non-compliant-code-2}

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

#### 準拠コード {#compliant-code-1}

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

public void orDoThis () {
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

### 常に ResourceResolver オブジェクトを閉じる {#resourceresolver-objects-should-always-be-closed}

* **キー**：CQRules:CQBP-72
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

`ResourceResolverFactory` から取得された `ResourceResolver` オブジェクトは、システムリソースを使用します。`ResourceResolver` が使用されなくなった場合に、これらのリソースを再利用する指標がありますが、`close()` メソッドを呼び出し、開いている `ResourceResolver` オブジェクトを明示的に閉じるほうが効率的です。

比較的一般的な誤解として、既存の JCR セッションを使用して作成された `ResourceResolver` オブジェクトは明示的に閉じることはできず、そうすると基になる JCR セッションを閉じてしまうというものがあります。これは該当しません。どの方法で `ResourceResolver` を開いても、使用しなくなったら閉じる必要があります。`ResourceResolver` は閉じることのできる `Closeable` インターフェイスを実装するので、`close()` を明示的に呼び出す代わりに、`try-with-resources` 構文を使用することもできます。

#### 非準拠コード {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 準拠コード {#compliant-code-2}

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

### サーブレットの登録に Sling サーブレットパスを使用しない {#do-not-use-sling-servlet-paths-to-register-servlets}

* **キー**：CQRules:CQBP-75
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

[Sling ドキュメント](https://sling.apache.org/documentation/the-sling-engine/servlets.html)で説明されているように、パスによってサーブレットをバインドすることは推奨されません。パスバインドサーブレットでは、標準 JCR アクセス制御を使用できないので、追加のセキュリティをより厳格にする必要があります。パスバインドサーブレットを使用する代わりに、リポジトリにノードを作成し、リソースタイプによってサーブレットを登録することをお勧めします。

#### 非準拠コード {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### キャッチされた例外は、ログに記録またはスローする必要があるが、両方は行わない {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **キー**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

一般に、例外は 1 回だけログに記録する必要があります。複数回ログに記録すると、例外が発生した回数がわからなくなるので、混乱が生じる可能性があります。最も一般的なパターンは、キャッチされた例外をログに記録してスローすることです。

#### 非準拠コード {#non-compliant-code-6}

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

#### 準拠コード {#compliant-code-3}

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

#### 非準拠コード {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 準拠コード {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### GET または HEAD 要求の処理時に INFO でログに記録しない {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **キー**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **タイプ**：コードスメル
* **深刻度**：軽度

一般的に、INFO ログレベルは重要なアクションを区切るために使用し、デフォルトでは、Experience Manager は INFO レベル以上をログに記録するように設定されています。GET および HEAD メソッドは読み取り専用操作に過ぎず、重要なアクションを構成しません。GET または HEAD 要求に応答して INFO レベルでログに記録すると、大量のログノイズが作成されるので、ログファイル内の有用な情報を特定するのが難しくなります。GET または HEAD 要求処理時のログへの記録は、WARN または ERROR レベル（問題が発生した場合）、または、DEBUG または TRACE レベル（詳細なトラブルシューティング情報が役立つ可能性がある場合）で行います。

>[!NOTE]
>
>これは、各リクエストの `access.log`-type ログには適用されません。

#### 非準拠コード {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 準拠コード {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Exception.getMessage() をログステートメントの最初のパラメーターとして使用しない {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **キー**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

ベストプラクティスとして、ログメッセージは、アプリケーション内での問題の発生場所に関するコンテキスト情報を提供する必要があります。また、スタックトレースを使用してコンテキストを判断することもできます。これにより、一般的にログメッセージが読みやすく、わかりやすくなります。その結果、例外をログに記録する際に、例外のメッセージをログメッセージとして使用するのは適切ではありません。例外メッセージには、何が起こったかが含まれますが、ログメッセージは、例外が発生したときにアプリケーションが何を実行していたかをログリーダーに伝えるために使用する必要があります。例外メッセージはログに記録されます。独自のメッセージを指定すると、ログがわかりやすくなります。

#### 非準拠コード {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 準拠コード {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### catch ブロックのログは、WARN または ERROR レベルにする必要がある {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **キー**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

名前が示すように、Java™ の例外は常に例外的な状況で使用する必要があります。結果として、例外が検出されたときには、ログメッセージが適切なレベル（WARN または ERROR）で記録されるようにすることが重要です。これにより、これらのメッセージがログに正しく表示されます。

#### 非準拠コード {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 準拠コード {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### コンソールにスタックトレースをプリントしない {#do-not-print-stack-traces-to-the-console}

* **キー**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

既に述べたように、コンテキストはログメッセージを理解する場合に重要です。`Exception.printStackTrace()` を使用すると、スタックトレースのみが標準エラーストリームに出力されるので、すべてのコンテキストが失われます。さらに、Experience Manager などのマルチスレッドアプリケーションで、このメソッドを同時に使用して複数の例外が出力される場合、スタックトレースが重なって大きな混乱を招くことがあります。例外は、ログフレームワークによってのみ記録される必要があります。

#### 非準拠コード {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 準拠コード {#compliant-code-8}

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

Experience Manager にログインする場合は、常にログフレームワーク（SLF4J）を使用してログインする必要があります。標準出力または標準エラーストリームに直接出力すると、ログフレームワークによって提供される構造およびコンテキスト情報が失われます。場合によっては、パフォーマンスの問題が発生することがあります。

#### 非準拠コード {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 準拠コード {#compliant-code-9}

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

一般に、`/libs` および `/apps` で始まるパスは、参照元としてハードコーディングせず、Sling 検索パス（デフォルトで `/libs,/apps` に設定されている）に対する相対パスで格納する必要があります。絶対パスを使用すると、プロジェクトライフサイクルで後になってから初めて現れる、細かい不具合が生じる可能性があります。

#### 非準拠コード {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 準拠コード {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Sling スケジューラーを使用しない {#sonarqube-sling-scheduler}

* **キー**：CQRules:AMSCORE-554
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

確実な実行を必要とするタスクには、 Sling スケジューラーを使用しないでください。Sling スケジュールジョブは実行を保証し、クラスター化環境と非クラスター化環境の両方に適しています。

Sling ジョブがクラスター環境で処理される方法について詳しくは、[Apache Sling のイベントとジョブの取り扱い](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)を参照してください。

### Experience Manager の非推奨 API は使用しない {#sonarqube-aem-deprecated}

* **キー**：AMSCORE-553
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Experience Manager API のサーフェスは、使用が勧められず、非推奨と見なされる API を識別するため、継続的に改訂されます。

多くの場合、これらの API は、標準の Java™ `@Deprecated` 注釈を使用して非推奨とされ、その結果、`squid:CallToDeprecatedMethod` によって識別されます。

ただし、API が Experience Manager のコンテキストで非推奨となるものの、他のコンテキストでは非推奨とならない場合があります。このルールは、この 2 番目のクラスを識別します。

### Sling モデルで @Inject 注釈を @Optional と共に使用しない {#sonarqube-slingmodels-inject-optional}

* **キー**：InjectAnnotationWithOptionalInjectionCheck
* **タイプ**：ソフトウェアの品質
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.11

Apache Sling プロジェクトでは、Sling モデルのコンテキストでの `@Inject` 注釈の使用を推薦しません。`DefaultInjectionStrategy.OPTIONAL` と組み合わされた場合（フィールドまたはクラスレベルで）、パフォーマンスが悪くなるからです。代わりに、より具体的なインジェクション（`@ValueMapValue` または `@OsgiInjector` 注釈など）を使用する必要があります。

推薦される注釈に関して、そして、そもそもなぜこのような推薦がされたのかに関しての詳細は、[Apache Sling ドキュメント](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1)を参照してください。


### HTTPClient のインスタンスを再利用 {#sonarqube-reuse-httpclient}

* **キー**：AEMSRE-870
* **タイプ**：ソフトウェアの品質
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.11

AEM アプリケーションは 、HTTP プロトコルを使用している他のアプリケーションに接続することが多く、Apache HttpClient はこれを実現するためによく使用されるライブラリです。しかし、このような HttpClient オブジェクトを作成する際にはオーバーヘッドが発生するので、これらのオブジェクトはできる限り再利用する必要があります。

このルールは、HttpClient オブジェクトがメソッド内でプライベートではなく、クラスレベルでグローバルであることを確認するので、再利用できます。この場合、httpClient フィールドは、クラスのコンストラクターか `activate()` メソッド（このクラスが OSGi コンポーネント／サービスの場合）で設定される必要があります。

HttpClient の使用に関するベストプラクティスに関しては、HttpClient の[最適化ガイド](https://hc.apache.org/httpclient-legacy/performance.html)を確認してください。

#### 非準拠コード {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### 準拠コード {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## OakPAL コンテンツルール {#oakpal-rules}

以下の節では、Cloud Manager が実行する OakPAL チェックについて説明します。

>[!NOTE]
>
>OakPAL は、スタンドアロンの Oak リポジトリを使用してコンテンツパッケージを検証するフレームワークです。2019 Experience Manager Rockstar North America 賞を受賞した Experience Manager Partner が開発しました。

### @ProviderType の注釈が付いた製品 API は、お客様による実装または拡張はできない  {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **キー**：CQBP-84
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2018.7.0

Experience Manager API には、カスタムコードで使用するけれど実装できない Java™ インターフェイスとクラスが含まれています。例えば、インターフェイス `com.day.cq.wcm.api.Page` は、Experience Manager のみで実装する必要があります。

新しいメソッドがこれらのインターフェイスに追加された場合、これらのインターフェイスを使用する既存のコードには、これらの追加のメソッドは影響しません。その結果、これらのインターフェイスに新しいメソッドが追加された場合、後方互換性があると見なされます。ただし、カスタムコードがこれらのインターフェイスのいずれかを実装する場合、そのカスタムコードによってお客様に後方互換性のリスクがもたらされます。

インターフェイスとクラス（Experience Manager によって実装される）には、`org.osgi.annotation.versioning.ProviderType` または場合によっては従来の類似の注釈 `aQute.bnd.annotation.ProviderType` が付けられます。このルールは、カスタムコードによってこのようなインターフェイスが実装されている（またはクラスが拡張されている）場合を特定します。

#### 非準拠コード {#non-compliant-code-3}

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

標準提供の複数の Experience Manager Oak インデックスには Tika 設定が含まれており、これらのインデックスをカスタマイズする場合は Tika 設定を含める必要があります。このルールは、`damAssetLucene`、`lucene`、`graphqlConfig` インデックスのカスタマイズを確認し、`tika` ノードがない場合、または `tika` ノードに `config.xml` という名前の子ノードがない場合には問題を報告します。

インデックス定義のカスタマイズについて詳しくは、[インデックス作成に関するドキュメント](/help/operations/indexing.md#preparing-the-new-index-definition)を参照してください。

#### 非準拠コード {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 準拠コード {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### カスタム Lucene Oak インデックスは同期してはいけない {#oakpal-indexasync}

* **キー**：IndexAsyncProperty
* **タイプ**：バグ
* **重大度**：ブロッカー
* **開始バージョン**：2021.8.0

`lucene` タイプの Oak インデックスは常に非同期でインデックスを作成する必要があります。これに従わないと、システムが不安定になる可能性があります。Lucene インデックスの構造について詳しくは、[Oak のドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)を参照してください。

#### 非準拠コード {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### 準拠コード {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
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

Experience Manager Assets でアセット検索が正しく機能するようにするには、`damAssetLucene` Oak インデックスのカスタマイズはこのインデックスに固有の一連のガイドラインに従う必要があります。このルールは、インデックス定義に `tags` という複数の値を持つプロパティ（`visualSimilaritySearch` という値を含む）があるかどうかを確認します。

#### 非準拠コード {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### 準拠コード {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 顧客パッケージでは /libs 下のノードを作成／変更しない {#oakpal-customer-package}

* **キー**：BannedPath
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2019.6.0

Experience Manager コンテンツリポジトリ内の `/libs` コンテンツツリーを読み取り専用と見なすことは、長年のベストプラクティスとなっています。`/libs` の下のノードやプロパティを変更すると、メジャーアップデートやマイナーアップデートの際に重大な問題が発生する可能性があります。`/libs` への変更は、アドビの公式チャネルを通じて行う必要があります。

### パッケージには重複する OSGi 設定を含めない {#oakpal-package-osgi}

* **キー**：DuplicateOsgiConfigurations
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

複雑なプロジェクトでよく発生する問題は、同じ OSGi コンポーネントが複数回設定されることです。この問題により、どの設定が適用可能かがあいまいになります。このルールは「実行モード対応」です。つまり、同じコンポーネントが同じ実行モード（または実行モードの組み合わせ）で複数回設定されている問題のみを特定します。

>[!NOTE]
>
>このルールの結果、ビルド済みパッケージのリスト全体で同じパッケージが重複する場合など、同じパスの同じ設定が複数のパッケージで定義される問題が発生します。
>
>例えば、ビルドで `com.myco:com.myco.ui.apps` と `com.myco:com.myco.all` というパッケージが生成され、`com.myco:com.myco.all` に `com.myco:com.myco.ui.apps` が組み込まれている場合、`com.myco:com.myco.ui.apps` 内のすべての設定が重複としてレポートされます。
>
>これは一般に、[コンテンツパッケージ構造ガイドライン](/help/implementing/developing/introduction/aem-project-content-package-structure.md)に従っていない場合です。この例では、パッケージ `com.myco:com.myco.ui.apps` に `<cloudManagerTarget>none</cloudManagerTarget>` プロパティがありません。

#### 非準拠コード {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 準拠コード {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### config および install フォルダーには OSGi ノードのみを含める {#oakpal-config-install}

* **キー**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

セキュリティ上の理由から、`/config/` と `/install/` を含むパスを判読できるのは Experience Manager の管理者ユーザーのみとなっており、これらのパスは OSGi 設定と OSGi バンドルにのみ使用する必要があります。これらのセグメントを含むパスの下に他のタイプのコンテンツを配置すると、アプリケーションの動作が管理者ユーザーと非管理者ユーザーとで意図せず異なることになります。

よくある問題としては、コンポーネントダイアログ内や、インライン編集にリッチテキストエディター設定を指定する際に、`config` というノードを使用するケースがあります。この問題を解決するには、問題のノードを準拠した名前に変更する必要があります。リッチテキストエディター設定については、`cq:inplaceEditing` ノードの `configPath` プロパティを使用して新しい場所を指定します。

#### 非準拠コード {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 準拠コード {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### パッケージは重複させない {#oakpal-no-overlap}

* **キー**：PackageOverlaps
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

[パッケージには重複する OSGi 設定を含めない](#oakpal-package-osgi)と同様に、これも複雑なプロジェクトでよく発生する問題です。複数の異なるコンテンツパッケージに同じノードパスが書き込まれるケースです。コンテンツパッケージの依存関係を使用すると、一貫性のある結果を得ることができますが、その際には、パッケージがまったく重複しないようにすることをお勧めします。

### デフォルトのオーサリングモードをクラシック UI にしない {#oakpal-default-authoring}

* **キー**：ClassicUIAuthoringMode
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` は、Experience Manager 内でデフォルトのオーサリングモードを定義します。Experience Manager 6.4 以降、クラシック UI は非推奨となったため、デフォルトのオーサリングモードがクラシック UI に設定されている場合、問題が発生するようになりました。

### ダイアログを持つコンポーネントはタッチ UI ダイアログが必要 {#oakpal-components-dialogs}

* **キー**：ComponentWithOnlyClassicUIDialog
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

クラシック UI ダイアログを持つ Experience Manager コンポーネントには、対応するタッチ UI ダイアログが常に存在する必要があります。どちらも、最適なオーサリングエクスペリエンスを提供し、クラシック UI がサポートされていない Cloud Service デプロイメントモデルとの互換性を持たせます。このルールは、次のシナリオを検証します。

* クラシック UI ダイアログ（`dialog` 子ノード）を持つコンポーネントには、対応するタッチ UI ダイアログ（`cq:dialog` 子ノード）が必要です。
* クラシック UI デザインダイアログ（`design_dialog` ノード）を使用しているコンポーネントには、対応するタッチ UI デザインダイアログ（`cq:design_dialog` 子ノード）が必要です。
* クラシック UI ダイアログとクラシック UI デザインダイアログの両方を持つコンポーネントには、対応するタッチ UI ダイアログと対応するタッチ UI デザインダイアログの両方が必要です。

Experience Manager 最新化ツールのドキュメントには、コンポーネントをクラシック UI からタッチ UI に変換する方法に関するドキュメントとツールが記載されています。詳しくは、[Experience Manager 最新化ツールのドキュメント](https://opensource.adobe.com/aem-modernize-tools/)を参照してください。

### 可変コンテンツと不変コンテンツがパッケージ内に混在してはならない {#oakpal-packages-immutable}

* **キー**：ImmutableMutableMixedPackage
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Cloud Service デプロイメントモデルとの互換性を保つには、個々のコンテンツパッケージに、リポジトリの不変領域（`/apps` および `/libs`）または可変領域（`/apps` または `/libs`）のいずれか（ただし両方ではない）のコンテンツが含まれている必要があります。例えば、`/apps/myco/components/text` と `/etc/clientlibs/myco` の両方を含むパッケージは Cloud Service と互換性がなく、問題が報告されます。

>[!NOTE]
>
>[顧客パッケージでは /libs 下のノードを作成／変更しない](#oakpal-customer-package)のルールが常に適用されます。

詳しくは、[Experience Manager プロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md)を参照してください。

### リバースレプリケーションエージェントを使用しない {#oakpal-reverse-replication}

* **キー**：ReverseReplication
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

リバースレプリケーションのサポートは、Experience Manager as a Cloud Service の[リリースノート](/help/release-notes/aem-cloud-changes.md#replication-agents)で説明しているように、Cloud Service のデプロイメントでは利用できません。

リバースレプリケーションを使用するお客様は、アドビに問い合わせて、代替ソリューションをご利用ください。

### プロキシ対応のクライアントライブラリに含まれるリソースは resources という名前のフォルダーに格納する {#oakpal-resources-proxy}

* **キー**：ClientlibProxyResource
* **タイプ**：バグ
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager クライアントライブラリには、画像やフォントなどの静的リソースが含まれている場合があります。[プリプロセッサーの使用](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)のドキュメントで説明しているように、プロキシ化されたクライアントライブラリを使用する場合、パブリッシュインスタンスで効果的に参照するために、これらの静的リソースを `resources` という名前の子フォルダーに格納する必要があります。

#### 非準拠コード {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 準拠コード {#compliant-proxy-enabled}

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

Experience Manager as a Cloud Service 上でのアセット処理をアセットマイクロサービスに移行するのに伴い、Experience Manager のオンプレミスバージョンと AMS バージョンで使用されていたワークフロープロセスが、サポートされなくなる、または不要になります。

[Experience Manager as a Cloud Service Assets GitHub リポジトリ](https://github.com/adobe/aem-cloud-migration)の移行ツールを使用すると、Experience Manager as a Cloud Service への移行中にワークフローモデルを更新できます。

### 静的なテンプレートより編集可能なテンプレートの使用を推奨 {#oakpal-static-template}

* **キー**：StaticTemplateUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

従来、Experience Manager プロジェクトでは静的テンプレートを使用するのが一般的でしたが、アドビでは、最も柔軟性が高く、静的テンプレートにはない追加機能をサポートしている編集可能なテンプレートをお勧めします。詳しくは、[ページテンプレート](/help/implementing/developing/components/templates.md)のドキュメントを参照してください。

静的なテンプレートから編集可能なテンプレートへの移行は、[Experience Manager 最新化ツール](https://opensource.adobe.com/aem-modernize-tools/)を使用して、ほとんど自動化することができます。

### 従来の基盤コンポーネントの使用は推奨されない {#oakpal-usage-legacy}

* **キー**：LegacyFoundationComponentUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

従来の基盤コンポーネント（`/libs/foundation` 下のコンポーネントなど）は、一部の Experience Manager リリースでは廃止され、コアコンポーネントが採用されています。使用する方法がオーバーレイであろうと継承であろうと、カスタムコンポーネントの基礎として基盤コンポーネントを使用することは、お勧めしません。対応するコアコンポーネントに変換する必要があります。

この変換は、[Experience Manager 最新化ツール](https://opensource.adobe.com/aem-modernize-tools/)で容易に行うことができます。

### サポートされている実行モード名と順序のみを使用 {#oakpal-supported-runmodes}

* **キー**：SupportedRunmode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、実行モード名に対して厳密な命名ポリシーを適用し、それらの実行モードに対して厳密な順序を指定します。サポートされている実行モードのリストは、[Experience Manager as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md#runmodes)のドキュメントで確認でき、このリストからの逸脱は問題として特定されます。

### カスタム検索インデックス定義ノードは、/oak:index の直接の子にする必要がある {#oakpal-custom-search}

* **キー**：OakIndexLocation
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、カスタム検索インデックス定義（`oak:QueryIndexDefinition` タイプのノード）が `/oak:index` の直接の子ノードである必要があります。Experience Manager as a Cloud Service と互換性を持たせるため、他の場所にあるインデックスは移動する必要があります。検索インデックスについて詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)のドキュメントを参照してください。

### カスタム検索インデックス定義ノードの compatVersion は 2 にする {#oakpal-custom-search-compatVersion}

* **キー**：IndexCompatVersion
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、カスタム検索インデックス定義（`oak:QueryIndexDefinition` タイプのノード）の `compatVersion` プロパティを `2` に設定する必要があります。その他の値は、Experience Manager as a Cloud Service ではサポートされていません。検索インデックスの詳細については、[コンテンツ検索とインデックス](/help/operations/indexing.md)を参照してください。

### カスタム検索インデックス定義ノードの子孫ノードのタイプは、nt:unstructured にする {#oakpal-descendent-nodes}

* **キー**：IndexDescendantNodeType
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

カスタム検索インデックス定義ノードに順序なしの子ノードがある場合、トラブルシューティングしにくい問題が発生するおそれがあります。このような状況を避けるために、`oak:QueryIndexDefinition` ノードのすべての子孫ノードは、タイプを `nt:unstructured` にすることをお勧めします。

### カスタム検索インデックス定義ノードには、子を持つ indexRules という名前の子ノードを含める {#oakpal-custom-search-index}

* **キー**：IndexRulesNode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

適切に定義されたカスタム検索インデックス定義ノードには、`indexRules` という名前の子ノードが含まれている必要があり、今度は、この子ノードに少なくとも 1 つの子が必要です。詳しくは、[Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html)を参照してください。

### カスタム検索インデックス定義ノードは命名規則に従う {#oakpal-custom-search-definitions}

* **キー**：IndexName
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)のドキュメントで説明されている特定のパターンに従ってカスタム検索インデックス定義（`oak:QueryIndexDefinition` タイプのノード）に名前を付ける必要があります。

### カスタム検索インデックス定義ノードでは lucene 型のインデックスを使用する  {#oakpal-index-type-lucene}

* **キー**：IndexType
* **タイプ**：バグ
* **重大度**：ブロッカー
* **最初の対象バージョン**：バージョン2021.2.0（2021.8.0でタイプと重大度が変更されました）

Experience Manager as a Cloud Service では、カスタム検索インデックス定義（`oak:QueryIndexDefinition` タイプのノード）に、値が `lucene` に設定された `type` プロパティが必要です。Experience Manager as a Cloud Service に移行する前に、従来のインデックスタイプを使用したインデックス作成を更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)を参照してください。

### カスタム検索インデックス定義ノードに seed という名前のプロパティを含めない {#oakpal-property-name-seed}

* **キー**：IndexSeedProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、カスタム検索インデックス定義（ノードのタイプが `oak:QueryIndexDefinition`）に `seed` という名前のプロパティを含めることが禁止されています。Experience Manager as a Cloud Service に移行する前に、このプロパティを使用しているインデックスを更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)のドキュメントを参照してください。

### カスタム検索インデックス定義ノードに reindex というプロパティを含めない {#oakpal-reindex-property}

* **キー**：IndexReindexProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager as a Cloud Service では、カスタム検索インデックス定義（ノードのタイプが `oak:QueryIndexDefinition`）に `reindex` という名前のプロパティを含めることが禁止されています。Experience Manager as a
Cloud Service に移行する前に、このプロパティを使用しているインデックスを更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)のドキュメントを参照してください。

### カスタム DAM Asset Lucene ノードで「queryPaths」を指定することはできません {#oakpal-damAssetLucene-queryPaths}

* **キー**：IndexDamAssetLucene
* **タイプ**：バグ
* **重大度**：ブロッカー
* **最初の対象バージョン**：バージョン 2022.1.0

#### 非準拠コード {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### 準拠コード {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### カスタム検索のインデックス定義に compatVersion が含まれる場合は、2 に設定する必要があります。 {#oakpal-compatVersion}

* **キー**：IndexCompatVersion
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2022.1.0


### 「includedPaths」を指定するインデックスノードでは、同じ値を持つ「queryPaths」も指定する必要があります {#oakpal-included-paths-without-query-paths}

* **キー**：IndexIncludedPathsWithoutQueryPaths
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

カスタムインデックスの場合、`includedPaths` および `queryPaths` は同じ値で設定する必要があります。いずれかを指定した場合は、もう 1 つが一致する必要があります。ただし、`damAssetLucene` のインデックスには特別なケースがあります（カスタムバージョンを含む）。これらの場合、`includedPaths` のみを提供する必要があります。

### 汎用ノードタイプの nodeScopeIndex を指定するインデックスノードでも includedPaths と queryPaths を指定する必要があります。 {#oakpal-full-text-on-generic-node-type}

* **キー**：IndexFulltextOnGenericType
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

`nt:unstructured` または `nt:base` のような「汎用」ノードタイプで `nodeScopeIndex` プロパティを設定する場合、`includedPaths` および `queryPaths` プロパティも指定する必要があります。
`nt:base` は「汎用」と見なすことができます。これは、すべてのノードタイプがそのタイプを継承するからです。したがって、`nt:base` に `nodeScopeIndex` を設定すると、リポジトリ内のすべてのノードのインデックスが作成されます。同様に、このタイプのリポジトリには多数のノードがあるので、`nt:unstructured` も「汎用」と見なされます。

#### 非準拠コード {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### 準拠コード {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### クエリエンジンの queryLimitReads プロパティは上書きしないでください {#oakpal-query-limit-reads}

* **キー**：OverrideOfQueryLimitReads
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

デフォルト値を上書きすると、特にコンテンツが追加された場合に、ページの読み取りが非常に遅くなる可能性があります。

### 同じインデックスの複数のアクティブバージョン {#oakpal-multiple-active-versions}

* **キー**：IndexDetectMultipleActiveVersionsOfSameIndex
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

#### 非準拠コード {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### 準拠コード {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### 完全なカスタムインデックス定義の名前は、公式のガイドラインに従う必要があります {#oakpal-fully-custom-index-name}

* **キー**：IndexValidFullyCustomName
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

完全なカスタムインデックス名に必要なパターンは `[prefix].[indexName]-custom-[version]` です。詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)のドキュメントを参照してください。

### 同じインデックス定義内で異なる分析値を持つ同じプロパティ {#oakpal-same-property-different-analyzed-values}

#### 非準拠コード {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### 準拠コード {#compliant-code-same-property-different-analyzed-values}

例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

分析対象のプロパティが明示的に設定されていない場合、そのデフォルト値は false になります。

### タグプロパティ {#tags-property}

* **キー**：IndexHasValidTagsProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2023.1.0

個別のインデックスでは、タグプロパティとその現在の値を必ず保持してください。タグプロパティに新しい値を追加することもできますが、既存の値を削除（またはプロパティを完全に削除）すると、予期しない結果が生じる場合があります。

### UI コンテンツパッケージではインデックス定義ノードをデプロイしない {#oakpal-ui-content-package}

* **キー**：IndexNotUnderUIContent
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.6.0

AEM Cloud Service では、UI コンテンツパッケージでカスタム検索インデックス定義（タイプ `oak:QueryIndexDefinition` のノード）をデプロイすることは禁止されています。

>[!WARNING]
>
>[Cloud Manager 2024年8月リリース](/help/implementing/cloud-manager/release-notes/current.md)以降、パイプラインでエラーが発生する可能性があるので、できるだけ早く対処することをお勧めします。

### damAssetLucene タイプのカスタムフルテキストインデックス定義には、「damAssetLucene」というプレフィックスを正しく付ける {#oakpal-dam-asset-lucene}

* **キー**：CustomFulltextIndexesOfTheDamAssetCheck
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.6.0

AEM Cloud Service では、`damAssetLucene` タイプのカスタムフルテキストインデックス定義に `damAssetLucene` 以外のプレフィックスを付けることが禁止されています。

>[!WARNING]
>
>[Cloud Manager 2024年8月リリース](/help/implementing/cloud-manager/release-notes/current.md)以降、パイプラインでエラーが発生する可能性があるので、できるだけ早く対処することをお勧めします。

### インデックス定義ノードに同じ名前のプロパティを含めない {#oakpal-index-property-name}

* **キー**：DuplicateNameProperty
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.6.0

AEM Cloud Service では、カスタム検索インデックス定義（つまり、タイプ `oak:QueryIndexDefinition` のノード）に同じ名前のプロパティを含めることが禁止されています。

>[!WARNING]
>
>[Cloud Manager 2024年8月リリース](/help/implementing/cloud-manager/release-notes/current.md)以降、パイプラインでエラーが発生する可能性があるので、できるだけ早く対処することをお勧めします。

### 特定の OOTB インデックス定義のカスタマイズは禁止されている {#oakpal-customizing-ootb-index}

* **キー**：RestrictIndexCustomization
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.6.0

AEM Cloud Service では、次の OOTB インデックスの許可されていない変更が禁止されています。

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>[Cloud Manager 2024年8月リリース](/help/implementing/cloud-manager/release-notes/current.md)以降、パイプラインでエラーが発生する可能性があるので、できるだけ早く対処することをお勧めします。

### アナライザーのトークナイザーの設定は、「tokenizer」という名前で作成する {#oakpal-tokenizer}

* **キー**：AnalyzerTokenizerConfigCheck
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.6.0

AEM Cloud Service では、アナライザーで誤った名前のトークナイザーを作成することが禁止されています。トークナイザーは、常に `tokenizer` として定義する必要があります。

>[!WARNING]
>
>[Cloud Manager 2024年8月リリース](/help/implementing/cloud-manager/release-notes/current.md)以降、パイプラインでエラーが発生する可能性があるので、できるだけ早く対処することをお勧めします。

### インデックス作成定義の設定にスペースを含めることはできない {#oakpal-indexing-definitions-spaces}

* **キー**：PathSpacesCheck
* **タイプ**：改善点
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2024.7.0

AEM Cloud Service では、プロパティにスペースを使用したインデックス作成定義の作成が禁止されています。
