---
title: カスタムコード品質ルール
description: このページでは、コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Adobe Experience Manager Engineering のベストプラクティスに基づいています。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 2935338b847f7e852dfd31c93a61e737e8a3ec80
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 46%

---

# カスタムコード品質ルール {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="カスタムコード品質ルール"
>abstract="このページでは、コード品質テストの一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Adobe Experience Manager Engineering のベストプラクティスに基づいています。"

このページでは、[コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md)の一環として Cloud Manager で実行されるカスタムコード品質ルールについて説明します。これらは、Experience Manager・エンジニアリングのベスト・プラクティスに基づいています。

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

Experience Managerアプリケーション内から HTTP 要求を実行する場合、不要なスレッドの使用を避けるために、適切なタイムアウトが設定されていることを確認することが重要です。 残念ながら、Java™のデフォルト HTTP クライアント (`java.net.HttpUrlConnection`) と一般的に使用される Apache HTTP Components クライアントはタイムアウトしないので、タイムアウトを明示的に設定する必要があります。 また、ベストプラクティスとして、これらのタイムアウトは 60 秒以内にする必要があります。

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

### 常に ResourceResolver オブジェクトを閉じる {#resourceresolver-objects-should-always-be-closed}

* **キー**：CQRules:CQBP-72
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

`ResourceResolverFactory` から取得された `ResourceResolver` オブジェクトは、システムリソースを使用します。`ResourceResolver` が使用されなくなった場合に、これらのリソースを再利用する指標がありますが、`close()` メソッドを呼び出し、開いている `ResourceResolver` オブジェクトを明示的に閉じるほうが効率的です。

一つの比較的一般的な誤解は `ResourceResolver` 既存の JCR セッションを使用して作成したオブジェクトは、明示的に閉じたり、基になる JCR セッションを閉じたりしないでください。 これは該当しません。どの方法で `ResourceResolver` を開いても、使用しなくなったら閉じる必要があります。`ResourceResolver` は閉じることのできる `Closeable` インターフェイスを実装するので、`close()` を明示的に呼び出す代わりに、`try-with-resources` 構文を使用することもできます。

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

### サーブレットの登録に Sling サーブレットパスを使用しない {#do-not-use-sling-servlet-paths-to-register-servlets}

* **キー**：CQRules:CQBP-75
* **タイプ**：コードスメル
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2018.4.0

[Sling ドキュメント](https://sling.apache.org/documentation/the-sling-engine/servlets.html)で説明されているように、パスによってサーブレットをバインドすることは推奨されません。パスバインドサーブレットでは、標準 JCR アクセス制御を使用できないので、追加のセキュリティをより厳格にする必要があります。パスバインドサーブレットを使用する代わりに、リポジトリにノードを作成し、リソースタイプによってサーブレットを登録することをお勧めします。

#### 準拠していないコード {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### キャッチされた例外は、両方ではなく、ログまたはスローする必要があります {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

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

### ログ文の直後にスロー文が続くのを避ける {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **キー**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

もうひとつの避けるべき一般的なパターンは、メッセージをログに記録してからすぐに例外をスローすることです。この方法は、通常、例外メッセージがログファイルに複製されることを示します。

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

### GET または HEAD 要求の処理時に INFO でログに記録しない {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **キー**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **タイプ**：コードスメル
* **深刻度**：軽度

一般に、INFO ログレベルは重要なアクションを区切るために使用し、デフォルトでは、Experience Managerは INFO レベル以上をログに記録するように設定されています。 GET および HEAD メソッドは読み取り専用操作に過ぎず、重要なアクションを構成しません。GETやHEADの要求に応じて INFO レベルでログに記録すると、大量のログノイズが発生する可能性が高く、ログファイル内の有用な情報を特定しにくくなります。 GET または HEAD 要求処理時のログへの記録は、WARN または ERROR レベル（問題が発生した場合）、または、DEBUG または TRACE レベル（詳細なトラブルシューティング情報が役立つ可能性がある場合）で行います。

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

### Exception.getMessage() をログステートメントの最初のパラメーターとして使用しない {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **キー**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

ベストプラクティスとして、ログメッセージは、アプリケーション内での問題の発生場所に関するコンテキスト情報を提供する必要があります。コンテキストはスタックトレースを使用して決定することもできますが、一般に、ログメッセージは読みやすく、理解しやすくなります。 その結果、例外をログに記録する場合、例外のメッセージをログメッセージとして使用するのは悪い方法です。 例外メッセージには、何が起こったかが含まれますが、ログメッセージは、例外が発生したときにアプリケーションが何を実行していたかをログリーダーに伝えるために使用する必要があります。 例外メッセージはログに記録されます。 独自のメッセージを指定すると、ログがわかりやすくなります。

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

### catch ブロックのログは、WARN または ERROR レベルにする必要がある {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **キー**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

名前が示すように、Java™例外は常に例外的な状況で使用する必要があります。 結果として、例外が検出されたときには、ログメッセージが適切なレベル（WARN または ERROR）で記録されるようにすることが重要です。これにより、これらのメッセージがログに正しく表示されます。

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

### コンソールにスタックトレースをプリントしない {#do-not-print-stack-traces-to-the-console}

* **キー**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

既に述べたように、コンテキストはログメッセージを理解する場合に重要です。使用 `Exception.printStackTrace()` は、スタックトレースのみを標準エラーストリームに出力し、すべてのコンテキストを失います。 さらに、Experience Managerなどのマルチスレッドアプリケーションでは、このメソッドを同時に使用して複数の例外が印刷される場合、スタックトレースが重なり、大きな混乱を招く可能性があります。 例外は、ログフレームワークによってのみ記録される必要があります。

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

ログインExperience Managerは、常にログフレームワーク (SLF4J) を通じておこなう必要があります。 標準出力または標準エラーストリームに直接出力すると、ログフレームワークによって提供される構造およびコンテキスト情報が失われます。 場合によっては、パフォーマンスの問題が発生することがあります。

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

### /apps および/libs パスをハードコードしない {#avoid-hardcoded-apps-and-libs-paths}

* **キー**：CQRules:CQBP-71
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2018.4.0

一般に、`/libs` および `/apps` で始まるパスは、参照元としてハードコーディングせず、Sling 検索パス（デフォルトで `/libs,/apps` に設定されている）に対する相対パスで格納する必要があります。絶対パスを使用すると、プロジェクトライフサイクルの後になって初めて現れる、わかりにくい不具合が生じる可能性があります。

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

### Sling スケジューラーを使用しない {#sonarqube-sling-scheduler}

* **キー**：CQRules:AMSCORE-554
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

確実な実行を必要とするタスクには、 Sling スケジューラーを使用しないでください。 Sling スケジュールジョブは実行を保証し、クラスター化ジョブと非クラスター化環境の両方に適しています。

参照： [Apache Sling Eventing and Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) を参照して、Sling ジョブがクラスター環境で処理される方法について確認してください。

### Experience Managerの非推奨 API は使用しない {#sonarqube-aem-deprecated}

* **キー**：AMSCORE-553
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Experience ManagerAPI の表面は、使用が推奨されず非推奨と見なされた API を識別するために、継続的に改訂されています。

多くの場合、これらの API は標準の Java™を使用して非推奨（廃止予定）になっています `@Deprecated` 注釈と、 `squid:CallToDeprecatedMethod`.

ただし、API がExperience Managerのコンテキストで非推奨となるが、他のコンテキストでは非推奨とならない場合があります。 このルールは、この 2 番目のクラスを識別します。


## OakPAL コンテンツルール {#oakpal-rules}

以下の節では、Cloud Manager が実行する OakPAL チェックについて説明します。

>[!NOTE]
>
>OakPAL は、スタンドアロンの Oak リポジトリを使用してコンテンツパッケージを検証するフレームワークです。2019 年Experience Manager・ロックスター・ノース・アメリカ賞を受賞したExperience Manager・パートナーによって開発されました。

### @ProviderType の注釈が付いた製品 API は、お客様による実装または拡張はできない  {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **キー**：CQBP-84
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2018.7.0

Experience ManagerAPI には、カスタムコードで使用する（ただし実装しない）ための Java™インターフェイスとクラスが含まれています。 例えば、インターフェイス `com.day.cq.wcm.api.Page` は、Experience Managerのみで実装する必要があります。

新しいメソッドがこれらのインターフェイスに追加された場合、これらのインターフェイスを使用する既存のコードには、これらの追加のメソッドは影響しません。 その結果、これらのインターフェイスに新しいメソッドが追加された場合、後方互換性があると見なされます。 ただし、カスタムコードがこれらのインターフェイスのいずれかを実装する場合、そのカスタムコードによってお客様に後方互換性のリスクがもたらされます。

インターフェイスとクラスは、Experience Managerが実装したように、 `org.osgi.annotation.versioning.ProviderType` または同様の従来の注釈 `aQute.bnd.annotation.ProviderType`. このルールは、カスタムコードによってこのようなインターフェイスが実装されている（またはクラスが拡張されている）場合を特定します。

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

標準搭載の複数のExperience ManagerOak インデックスには Tika 設定が含まれ、これらのインデックスのカスタマイズには Tika 設定が含まれている必要があります。 このルールは、 `damAssetLucene`、 `lucene`、`graphqlConfig` インデックスのカスタマイズを確認し、 `tika` ノードがない場合、または `tika` ノードに `config.xml` という名前の子ノードがない場合には問題を報告します。

インデックス定義のカスタマイズについて詳しくは、[インデックス作成に関するドキュメント](/help/operations/indexing.md#preparing-the-new-index-definition)を参照してください。

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

### カスタム Lucene Oak インデックスは同期してはいけない {#oakpal-indexasync}

* **キー**：IndexAsyncProperty
* **タイプ**：バグ
* **重大度**：ブロッカー
* **開始バージョン**：2021.8.0

`lucene` タイプの Oak インデックスは常に非同期でインデックスを作成する必要があります。これに従わないと、システムが不安定になる可能性があります。Lucene インデックスの構造について詳しくは、 [Oak ドキュメント。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

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

Experience Manager Assetsでアセット検索が正しく機能するように、 `damAssetLucene` Oak インデックスは、このインデックスに固有の一連のガイドラインに従う必要があります。 このルールは、インデックス定義に `tags` という複数の値を持つプロパティがあり `visualSimilaritySearch` という値を含むかどうかを確認します。

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

### 顧客パッケージでは、/libs の下のノードを作成または変更しないでください {#oakpal-customer-package}

* **キー**：BannedPath
* **タイプ**：バグ
* **深刻度**：致命的
* **最初の対象バージョン**：バージョン 2019.6.0

これは長い間のベストプラクティスでした `/libs` Experience Managerコンテンツリポジトリーのコンテンツツリーは、顧客は読み取り専用と見なす必要があります。 `/libs` 下のノードやプロパティを変更すると、メジャーアップデートおよびマイナーアップデートの際に重大な問題が発生する可能性があります。変更先 `/libs` は、公式チャネルを通じてAdobeがおこなう必要があります。

### パッケージには重複する OSGi 設定を含めないでください {#oakpal-package-osgi}

* **キー**：DuplicateOsgiConfigurations
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

複雑なプロジェクトでよく発生する問題は、同じ OSGi コンポーネントが複数回設定されることです。この問題は、どの設定が適用できるかをあいまいにします。 このルールは「実行モード対応」です。つまり、同じ実行モードまたは実行モードの組み合わせで同じコンポーネントが複数回設定される問題のみを識別します。

>[!NOTE]
>
>このルールでは、同じ設定が同じパスで複数のパッケージで定義される場合、ビルドパッケージの全体的なリストで同じパッケージが複製される場合など、問題が発生します。
>
>例えば、ビルドで、という名前のパッケージが生成される場合、 `com.myco:com.myco.ui.apps` および `com.myco:com.myco.all` 場所 `com.myco:com.myco.all` 埋め込み `com.myco:com.myco.ui.apps`の場合、 `com.myco:com.myco.ui.apps` は、重複としてレポートされます。
>
>これは、通常、 [コンテンツパッケージ構造のガイドライン](/help/implementing/developing/introduction/aem-project-content-package-structure.md).この例では、パッケージ `com.myco:com.myco.ui.apps` が見つからない `<cloudManagerTarget>none</cloudManagerTarget>` プロパティ。

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

### config および install フォルダーには OSGi ノードのみを含める必要があります {#oakpal-config-install}

* **キー**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2019.6.0

セキュリティ上の理由から、パスには `/config/` および `/install/` は、管理者ユーザーのみがExperience Managerで読み取り可能で、OSGi 設定と OSGi バンドルにのみ使用してください。 これらのセグメントを含むパスの下に他のタイプのコンテンツを配置すると、アプリケーションの動作が管理者ユーザーと非管理者ユーザーとで意図せず異なることになります。

よくある問題としては、コンポーネントダイアログ内や、インライン編集にリッチテキストエディター設定を指定する際に、`config` というノードを使用するケースがあります。この問題を解決するには、問題のあるノードの名前を、準拠した名前に変更する必要があります。 リッチテキストエディターの設定には、 `configPath` プロパティ `cq:inplaceEditing` 新しい場所を指定するノード。

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

[パッケージには重複する OSGi 設定を含めない](#oakpal-package-osgi)と同様に、これも複雑なプロジェクトでよく発生する問題です。複数の異なるコンテンツパッケージに同じノードパスが書き込まれるケースです。コンテンツパッケージの依存関係を使用すると、一貫性のある結果を得ることができますが、その際には、パッケージがまったく重複しないようにすることをお勧めします。

### デフォルトのオーサリングモードをクラシック UI にしない {#oakpal-default-authoring}

* **キー**：ClassicUIAuthoringMode
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` は、デフォルトのオーサリングモードをExperience Manager内で定義します。 理由： [クラシック UI は、Experience Manager6.4 以降、非推奨（廃止予定）となりました。](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=ja)の場合、デフォルトのオーサリングモードがクラシック UI に設定されていると問題が発生するようになりました。

### タッチ UI ダイアログが必要なダイアログを持つコンポーネント {#oakpal-components-dialogs}

* **キー**：ComponentWithOnlyClassicUIDialog
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

クラシック UI ダイアログを持つExperience Managerコンポーネントには、対応するタッチ UI ダイアログが常に存在する必要があります。 どちらも、最適なオーサリングエクスペリエンスを提供し、クラシック UI がサポートされていないCloud Serviceデプロイメントモデルとの互換性を持たせます。 このルールは、次のシナリオを検証します。

* クラシック UI ダイアログ（`dialog` 子ノード）を持つコンポーネントには、対応するタッチ UI ダイアログ（`cq:dialog` 子ノード）が必要です。
* クラシック UI デザインダイアログ（`design_dialog` ノード）を使用しているコンポーネントには、対応するタッチ UI デザインダイアログ（`cq:design_dialog` 子ノード）が必要です。
* クラシック UI ダイアログとクラシック UI デザインダイアログの両方を持つコンポーネントには、対応するタッチ UI ダイアログと対応するタッチ UI デザインダイアログの両方が必要です。

Experience Manager最新化ツールのドキュメントには、コンポーネントをクラシック UI からタッチ UI に変換する方法に関するドキュメントとツールが記載されています。 詳しくは、 [Experience Manager最新化ツールのドキュメント](https://opensource.adobe.com/aem-modernize-tools/) を参照してください。

### 可変コンテンツと不変コンテンツをパッケージに混在させない {#oakpal-packages-immutable}

* **キー**：ImmutableMutableMixedPackage
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

Cloud Serviceデプロイメントモデルとの互換性を保つには、個々のコンテンツパッケージに、リポジトリの不変領域 (`/apps` および `/libs`) または可変領域 ( `/apps` または `/libs`) ですが、両方ではありません。 例えば、両方を含むパッケージ `/apps/myco/components/text` および `/etc/clientlibs/myco` はCloud Serviceと互換性がないので、問題が報告されます。

>[!NOTE]
>
>[顧客パッケージでは /libs 下のノードを作成／変更しない](#oakpal-customer-package)のルールが常に適用されます。

参照： [Experience Managerプロジェクト構造](/help/implementing/developing/introduction/aem-project-content-package-structure.md) を参照してください。

### リバースレプリケーションエージェントを使用しない {#oakpal-reverse-replication}

* **キー**：ReverseReplication
* **タイプ**：コードスメル／Cloud Service との互換性
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2020.5.0

リバースレプリケーションのサポートは、Cloud Serviceのas a Cloud Serviceの一部として説明されているように、Experience Managerのデプロイメントでは利用できません。 [リリースノート。](/help/release-notes/aem-cloud-changes.md#replication-agents)

リバースレプリケーションを使用するお客様は、アドビに問い合わせて、代替ソリューションをご利用ください。

### プロキシが有効なクライアントライブラリに含まれるリソースは、resources という名前のフォルダーに格納する必要があります {#oakpal-resources-proxy}

* **キー**：ClientlibProxyResource
* **タイプ**：バグ
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Managerのクライアントライブラリには、画像やフォントなどの静的リソースが含まれる場合があります。 [プリプロセッサーの使用](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)のドキュメントで説明しているように、プロキシ化されたクライアントライブラリを使用する場合、パブリッシュインスタンスで効果的に参照するために、これらの静的リソースを という名前の子フォルダーに格納する必要があります。`resources`

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

### 互換性のないCloud Serviceプロセスの使用 {#oakpal-usage-cloud-service}

* **キー**：CloudServiceIncompatibleWorkflowProcess
* **タイプ**：バグ
* **深刻度**：重大
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manager上でのアセット処理に対するアセットマイクロサービスへの移行に伴い、Experience Managerのオンプレミス版と AMS 版で使用されていたいくつかのワークフロープロセスは、サポートされなくなったか不要になりました。

移行ツール ( [Experience Managerのas a Cloud ServiceAssets GitHub リポジトリ](https://github.com/adobe/aem-cloud-migration) を使用して、Experience Manageras a Cloud Serviceへの移行中にワークフローモデルを更新できます。

### 静的テンプレートの使用は、編集可能なテンプレートのためにお勧めしません {#oakpal-static-template}

* **キー**：StaticTemplateUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

静的テンプレートの使用は、Experience Managerプロジェクトでは従来より一般的ですが、静的テンプレートでは、編集可能なテンプレートを推奨します。これは、静的テンプレートにはない追加機能を最大限に柔軟に提供し、サポートするからです。 詳しくは、[ページテンプレート](/help/implementing/developing/components/templates.md)のドキュメントを参照してください。

静的テンプレートから編集可能テンプレートへの移行は、 [Experience Manager最新化ツール。](https://opensource.adobe.com/aem-modernize-tools/)

### 従来の基盤コンポーネントは使用しないでください {#oakpal-usage-legacy}

* **キー**：LegacyFoundationComponentUsage
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

従来の基盤コンポーネント（例：下のコンポーネント） `/libs/foundation`) は [いくつかのExperience Managerリリースで非推奨](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=ja) コアコンポーネントに優先して 使用する方法がオーバーレイであろうと継承であろうと、基盤コンポーネントに基づいてカスタムコンポーネントを作成することは、お勧めしません。対応するコアコンポーネントに移行してください。

この変換は、 [Experience Manager最新化ツール。](https://opensource.adobe.com/aem-modernize-tools/)

### サポートされている実行モード名と順序のみを使用 {#oakpal-supported-runmodes}

* **キー**：SupportedRunmode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceでは、実行モード名に対して厳密な命名ポリシーを適用し、それらの実行モードに対して厳密な順序を指定します。 サポートされている実行モードのリストは、ドキュメントに記載されています [Experience Managerへのデプロイas a Cloud Service](/help/implementing/deploying/overview.md#runmodes) これから逸脱した場合は、問題と見なされます。

### カスタム検索インデックス定義ノードは、/oak:index の直接の子である必要があります {#oakpal-custom-search}

* **キー**：OakIndexLocation
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceには、カスタム検索インデックスの定義（つまり、タイプのノード）が必要です `oak:QueryIndexDefinition`) の直接の子ノード `/oak:index`. 他の場所のインデックスは、as a Cloud ServiceのExperience Managerとの互換性を保つために移動する必要があります。 検索インデックスの詳細については、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)のドキュメントを参照してください。

### カスタム検索インデックス定義ノードの compatVersion は 2 である必要があります {#oakpal-custom-search-compatVersion}

* **キー**：IndexCompatVersion
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceには、カスタム検索インデックスの定義（タイプのノードなど）が必要です `oak:QueryIndexDefinition`) には、 `compatVersion` プロパティを `2`. その他の値は、as a Cloud ServiceExperience Managerではサポートされません。 検索インデックスの詳細については、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)を参照してください。

### カスタム検索インデックス定義ノードの子孫ノードは、nt:unstructured 型である必要があります {#oakpal-descendent-nodes}

* **キー**：IndexDescendantNodeType
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

カスタム検索インデックス定義ノードに順序が指定されていない子ノードがある場合、問題のトラブルシューティングが困難になることがあります。 この状況を回避するには、 `oak:QueryIndexDefinition` ノードのタイプは `nt:unstructured`.

### カスタム検索インデックス定義ノードには、子を持つ indexRules という名前の子ノードが含まれている必要があります {#oakpal-custom-search-index}

* **キー**：IndexRulesNode
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

適切に定義されたカスタム検索インデックス定義ノードには、`indexRules` という名前の子ノードが含まれている必要があり、今度は、この子ノードに少なくとも 1 つの子が必要です。詳しくは、[Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html)を参照してください。

### カスタム検索インデックス定義ノードは、命名規則に従う必要があります {#oakpal-custom-search-definitions}

* **キー**：IndexName
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceには、カスタム検索インデックスの定義（つまり、タイプのノード）が必要です `oak:QueryIndexDefinition`) には、ドキュメントで説明されている特定のパターンに従って名前を付ける必要があります [コンテンツの検索とインデックス作成。](/help/operations/indexing.md)

### カスタム検索インデックス定義ノードは、インデックスタイプ Lucene を使用する必要があります  {#oakpal-index-type-lucene}

* **キー**：IndexType
* **タイプ**：バグ
* **重大度**：ブロッカー
* **最初の対象バージョン**：バージョン2021.2.0（2021.8.0でタイプと重大度が変更されました）

Experience Manageras a Cloud Serviceには、カスタム検索インデックスの定義（つまり、タイプのノード）が必要です `oak:QueryIndexDefinition`) が `type` プロパティの値を次に設定 `lucene`. 従来のインデックスタイプを使用するインデックス作成は、Experience Manageras a Cloud Serviceに移行する前に更新する必要があります。 詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)を参照してください。

### カスタム検索インデックス定義ノードに seed という名前のプロパティを含めることはできません {#oakpal-property-name-seed}

* **キー**：IndexSeedProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceは、カスタム検索インデックスの定義（つまり、タイプのノード）を禁止します `oak:QueryIndexDefinition`) に、 `seed`. このプロパティを使用するインデックス作成は、Experience Manageras a Cloud Serviceに移行する前に更新する必要があります。 詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)のドキュメントを参照してください。

### カスタム検索インデックス定義ノードに reindex という名前のプロパティを含めることはできません {#oakpal-reindex-property}

* **キー**：IndexReindexProperty
* **タイプ**：コードスメル
* **深刻度**：軽度
* **最初の対象バージョン**：バージョン 2021.2.0

Experience Manageras a Cloud Serviceは、カスタム検索インデックスの定義（つまり、タイプのノード）を禁止します `oak:QueryIndexDefinition`) に、 `reindex`. このプロパティを使用するインデックス作成は、Experience Manageras a Cloud Serviceに移行する前に更新する必要があります。 詳しくは、[コンテンツの検索とインデックス作成](/help/operations/indexing.md#how-to-use)のドキュメントを参照してください。
