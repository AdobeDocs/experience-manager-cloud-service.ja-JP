---
title: カスタムコード品質ルール - Cloud Services
description: カスタムコード品質ルール - Cloud Services
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 0217e39ddc8fdaa2aa204568be291d608aef3d0e
workflow-type: ht
source-wordcount: '3520'
ht-degree: 100%

---

# カスタムコード品質ルール {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="カスタムコード品質ルール"
>abstract="このページでは、AEM エンジニアリングチームのベストプラクティスに基づいて作成され Cloud Manager で実行されるカスタムコード品質ルールについて説明します。"

このページでは、AEM エンジニアリングチームのベストプラクティスに基づいて作成され Cloud Manager で実行されるカスタムコード品質ルールについて説明します。

>[!NOTE]
>ここで提供されるコードサンプルは、例としてのみ使用されています。SonarQube の概念と品質ルールについて詳しくは、[概念](https://docs.sonarqube.org/7.4/user-guide/concepts/)（英語のみ）を参照してください。

## SonarQube ルール {#sonarqube-rules}

以下の節では、SonarQube ルールについて説明します。

### 問題が発生する可能性がある関数は使用しない {#do-not-use-potentially-dangerous-functions}

**キー**：CQRules:CWE-676

**タイプ**：脆弱性

**深刻度**：重大

**最初の対象バージョン**：バージョン 2018.4.0

***Thread.stop()*** および ***Thread.interrupt()*** メソッドを使用すると再現の困難な問題が発生する可能性があり、場合によってはセキュリティの脆弱性につながることもあります。その使用状況は、厳密に監視および検証する必要があります。一般的に、似た目標を達成するにはメッセージを渡すとより安全です。

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

**キー**：CQRules:CWE-134

**タイプ**：脆弱性

**深刻度**：重大

**最初の対象バージョン**：バージョン 2018.4.0

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

**キー**：CQRules:ConnectionTimeoutMechanism

**タイプ**：バグ

**深刻度**：致命的

**最初の対象バージョン**：バージョン 2018.6.0

AEM アプリケーション内から HTTP 要求を実行する場合、不要なスレッドの使用を防ぐために、適切なタイムアウトが設定されていることを確認することが重要です。ただし、Java のデフォルト HTTP クライアント（java.net.HttpUrlConnection）および一般的に使用される Apache HTTP コンポーネントクライアントのデフォルトの動作はタイムアウトしないので、タイムアウトを明示的に設定する必要があります。また、ベストプラクティスとして、これらのタイムアウトは 60 秒以内にする必要があります。

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

### ResourceResolver オブジェクトは常に閉じる必要がある {#resourceresolver-objects-should-always-be-closed}

**キー**：CQRules:CQBP-72

**タイプ**：コードスメル

**深刻度**：重大

**最初の対象バージョン**：バージョン 2018.4.0

ResourceResolverFactory から取得された ResourceResolver オブジェクトは、システムリソースを使用します。ResourceResolver が使用されなくなった場合に、これらのリソースを再利用する指標がありますが、close() メソッドを呼び出すことで開いている ResourceResolver オブジェクトを明示的に閉じるほうが効率的です。

比較的一般的な誤解として、既存の JCR セッションを使用して作成された ResourceResolver オブジェクトは、明示的に閉じると、基になる JCR セッションを閉じてしまうというものがあります。これは間違いで、ResourceResolver を開く方法に関係なく、使用されなくなったら閉じる必要があります。ResourceResolver は閉じることのできるインターフェイスを実装するので、close() を明示的に呼び出す代わりに、try-with-resources 構文を使用することもできます。

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

**キー**：CQRules:CQBP-75

**タイプ**：コードスメル

**深刻度**：重大

**最初の対象バージョン**：バージョン 2018.4.0

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

### キャッチされた例外は、ログまたはスローする必要があるが、両方は行わない {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**キー**：CQRules:CQBP-44---CatchAndEitherLogOrThrow

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

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

### ログステートメントの直後にスローステートメントを使用するのを避ける {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**キー**：CQRules:CQBP-44---ConsecutivelyLogAndThrow

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

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

### GET または HEAD 要求の処理時に INFO でログに記録しない {#avoid-logging-at-info-when-handling-get-or-head-requests}

**キー**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests

**タイプ**：コードスメル

**深刻度**：軽度

一般的に、INFO ログレベルは重要なアクションを区切るために使用し、デフォルトでは、AEM は INFO レベル以上をログに記録するように設定されています。GET および HEAD メソッドは読み取り専用操作に過ぎず、重要なアクションを構成しません。GET または HEAD 要求に応答して INFO レベルでログに記録すると、大量のログノイズが作成されるので、ログファイル内の有用な情報を特定するのが難しくなります。GET または HEAD 要求処理時のログへの記録は、WARN または ERROR レベル（問題が発生した場合）、または、DEBUG または TRACE レベル（詳細なトラブルシューティング情報が役立つ可能性がある場合）で行います。

>[!CAUTION]
>
>これは、各要求の access.log-type ログには適用されません。

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

**キー**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

ベストプラクティスとして、ログメッセージは、アプリケーション内での問題の発生場所に関するコンテキスト情報を提供する必要があります。また、スタックトレースを使用してコンテキストを判断することもできます。これにより、一般的にログメッセージが読みやすく、わかりやすくなります。結果として、例外をログに記録する場合、例外のメッセージをログメッセージとして使用するのは望ましくありません。例外メッセージには発生した問題の説明を含めるのに対して、ログメッセージでは、例外が発生したときにアプリケーションが何を実行していたかを示す必要があります。例外メッセージは、引き続きログに記録されます。独自のメッセージを指定すると、ログがわかりやすくなります。

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

**キー**：CQRules:CQBP-44---WrongLogLevelInCatchBlock

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

名前が示すように、Java の例外は常に&#x200B;*例外的な*&#x200B;状況で使用する必要があります。結果として、例外がキャッチされる際に、ログメッセージが適切なレベル（WARN または ERROR）で記録されるようにすることが重要です。これにより、これらのメッセージがログに正しく表示されます。

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

**キー**：CQRules:CQBP-44---ExceptionPrintStackTrace

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

既に述べたように、コンテキストはログメッセージを理解する場合に重要です。Exception.printStackTrace() を使用すると、スタックトレース&#x200B;**のみ**&#x200B;が標準エラーストリームに出力されるので、すべてのコンテキストが失われます。さらに、AEM などのマルチスレッドアプリケーションで、このメソッドを同時に使用して複数の例外がプリントされる場合、スタックトレースが重なって大きな混乱を招くことがあります。例外は、ログフレームワークによってのみ記録される必要があります。

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

**キー**：CQRules:CQBP-44—LogLevelConsolePrinters

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

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

**キー**：CQRules:CQBP-71

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2018.4.0

一般に、/libs および /apps で始まるパスは、参照元としてハードコーディングせず、Sling 検索パス（デフォルトで /libs、/apps に設定されている）に対する相対パスで格納する必要があります。絶対パスを使用すると、プロジェクトライフサイクルの後になって初めて現れるわかりにくい不具合が生じる可能性があります。

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

**キー**：CQRules:AMSCORE-554

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

Sling スケジューラーは、確実な実行を必要とするタスクには使用しないでください。Sling スケジュールジョブは実行を保証し、クラスター化ジョブと非クラスター化環境の両方に適しています。

Sling ジョブがクラスター環境で処理される方法について詳しくは、[Apache Sling Eventing and Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) を参照してください。

### AEM の非推奨 API は使用しない {#sonarqube-aem-deprecated}

**キー**：AMSCORE-553

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

AEM API の表面は、使用が推奨されず非推奨と見なされる API を識別するために継続的に見直しされます。

多くの場合、これらの API は、標準の Java *@Deprecated* 注釈を使用して非推奨とされ、その結果、`squid:CallToDeprecatedMethod` によって識別されます。

ただし、API が AEM のコンテキストで非推奨となるものの、他のコンテキストでは非推奨とならない場合があります。このルールは、この 2 番目のクラスを識別します。


## OakPAL コンテンツルール {#oakpal-rules}

Cloud Manager で実行される OakPAL 関連チェックについて、以下に説明します。

>[!NOTE]
>OakPAL は AEM パートナー（2019 年の AEM Rockstar North America の優勝者）により開発されたフレームワークで、スタンドアロンの Oak リポジトリーを使用してコンテンツパッケージを検証します。

### @ProviderType の注釈が付いた製品 API は、お客様による実装または拡張はできない  {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**キー**：CQBP-84

**タイプ**：バグ

**深刻度**：致命的

**最初の対象バージョン**：バージョン 2018.7.0

AEM API には、カスタムコードによる使用のみ（ただし実装はしない）を意図した Java インターフェイスおよびクラスが含まれています。例えば、インターフェイス *com.day.cq.wcm.api.Page* は、***AEM のみ***&#x200B;によって実装されるように設計されています。

これらのインターフェイスに新しいメソッドが追加される場合、それらの追加メソッドは、これらのインターフェイスを使用する既存のコードには影響しません。その結果、これらのインターフェイスへの新しいメソッドの追加は、後方互換性があると見なされます。ただし、カスタムコードがこれらのインターフェイスのいずれかを&#x200B;***実装***&#x200B;する場合、そのカスタムコードによってお客様に後方互換性のリスクがもたらされます。

AEM によってのみ実装されることを意図されたインターフェイス（およびクラス）は、*org.osgi.annotation.versioning.ProviderType*（場合によっては、従来の類似の注釈の *aQute.bnd.annotation.ProviderType*）で注釈が付けられます。このルールは、カスタムコードによってこのようなインターフェイスが実装されている（またはクラスが拡張されている）場合を特定します。

#### 準拠していないコード {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### カスタム Lucene Oak インデックスには tika 設定が必要 {#oakpal-indextikanode}

**キー**：IndexTikaNode

**タイプ**：バグ

**重大度**：ブロッカー

**開始バージョン**：2021.8.0

複数の標準提供の AEM Oak インデックスには tika 設定が含まれており、これらのインデックスをカスタマイズする場合は tika 設定を含める&#x200B;**必要があります**。このルールは、 `damAssetLucene`、 `lucene`、`graphqlConfig` インデックスのカスタマイズを確認し、 `tika` ノードがない場合、または `tika` ノードに `config.xml` という名前の子ノードがない場合には問題を報告します。

インデックス定義のカスタマイズの詳細については、[インデックス作成に関するドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#preparing-the-new-index-definition)を参照してください。

#### 準拠していないコード {#non-compliant-code-indextikanode}

```+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 準拠しているコード {#compliant-code-indextikanode}

```+ oak:index
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

**キー**：IndexAsyncProperty

**タイプ**：バグ

**重大度**：ブロッカー

**開始バージョン**：2021.8.0

Lucene タイプの Oak インデックスは常に非同期でインデックスを作成する必要があります。これに従わないと、システムが不安定になる可能性があります。Lucene インデックスの構造に関する詳細は、[Oak のドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)を参照してください。

#### 準拠していないコード {#non-compliant-code-indexasync}

```+ oak:index
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

```+ oak:index
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

**キー**：IndexDamAssetLucene

**タイプ**：バグ

**重大度**：ブロッカー

**開始バージョン**：2021.6.0

AEM Assets でアセット検索が正しく機能するようにするには、`damAssetLucene` Oak インデックスのカスタマイズはこのインデックスに固有の一連のガイドラインに従う必要があります。このルールは、インデックス定義に `tags` という複数の値を持つプロパティがあって `visualSimilaritySearch` という値を含むかどうかを確認します。

#### 準拠していないコード {#non-compliant-code-damAssetLucene}

```+ oak:index
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

```+ oak:index
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

**キー**：BannedPaths

**タイプ**：バグ

**重大度**：ブロッカー

**最初の対象バージョン**：バージョン 2019.6.0

AEM コンテンツリポジトリー内の /libs コンテンツツリーを読み取り専用と見なすことは長年のベストプラクティスとなっています。*/libs* 下のノードやプロパティを変更すると、メジャーアップデートおよびマイナーアップデートの際に重大な問題が発生する可能性があります。*/libs* への変更は、アドビの公式チャネルを通じてのみ行うことができます。

### パッケージには重複する OSGi 設定を含めない {#oakpal-package-osgi}

**キー**：DuplicateOsgiConfigurations

**タイプ**：バグ

**深刻度**：重大

**最初の対象バージョン**：バージョン 2019.6.0

複雑なプロジェクトでよく発生する問題は、同じ OSGi コンポーネントが複数回設定されることです。その結果、どの設定が使用可能かがあいまいになります。このルールは「実行モード対応」です。つまり、同じコンポーネントが同じ実行モード（または実行モードの組み合わせ）で複数回設定されている問題のみを特定します。

>[!NOTE]
>このルールの結果、ビルド済みパッケージのリスト全体で同じパッケージが重複する場合など、同じパスの同じ設定が複数のパッケージで定義される問題が発生します。例えば、ビルドで `com.myco:com.myco.ui.apps` と `com.myco:com.myco.all` というパッケージが生成され、`com.myco:com.myco.ui.apps` が `com.myco:com.myco.all` に組み込まれている場合、`com.myco:com.myco.ui.apps` 内のすべての設定が重複としてレポートされます。これは一般に、[コンテンツパッケージ構造ガイドライン](/help/implementing/developing/introduction/aem-project-content-package-structure.md)に従っていない場合に発生します。この例では、パッケージ `com.myco:com.myco.ui.apps` に `<cloudManagerTarget>none</cloudManagerTarget>` プロパティがありません。

#### 準拠していないコード {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 準拠しているコード {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### /config および /install フォルダーには OSGi ノードのみ含める  {#oakpal-config-install}

**キー**：ConfigAndInstallShouldOnlyContainOsgiNodes

**タイプ**：バグ

**深刻度**：重大

**最初の対象バージョン**：バージョン 2019.6.0

セキュリティ上の理由から、*/config/ と /install/* を含むパスは、AEM の管理者ユーザーだけが読み取り可能です。また、OSGi 設定と OSGi バンドルにのみ使用してください。これらのセグメントを含むパスの下に他のタイプのコンテンツを配置すると、アプリケーションの動作が管理者ユーザーと非管理者ユーザーとで意図せず異なることになります。

よくある問題としては、コンポーネントダイアログ内や、インライン編集にリッチテキストエディター設定を指定する際に、`config` というノードを使用するケースがあります。これを解決するには、問題のあるノードを適切な名前に変更する必要があります。リッチテキストエディター設定については、`cq:inplaceEditing` ノードの `configPath` プロパティを使用して新しい場所を指定します。

#### 準拠していないコード {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 準拠しているコード {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### パッケージは重複しない {#oakpal-no-overlap}

**キー**：PackageOverlaps

**タイプ**：バグ

**深刻度**：重大

**最初の対象バージョン**：バージョン 2019.6.0

*パッケージには重複する OSGi 設定を含めない*&#x200B;と同様に、これも複雑なプロジェクトでよく発生する問題です。複数の異なるコンテンツパッケージに同じノードパスが書き込まれるケースです。コンテンツパッケージの依存関係を使用すると、一貫性のある結果を得ることができますが、その際には、パッケージがまったく重複しないようにすることをお勧めします。

### デフォルトのオーサリングモードをクラシック UI にしない {#oakpal-default-authoring}

**キー**：ClassicUIAuthoringMode

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` は、AEM 内でデフォルトのオーサリングモードを定義します。AEM 6.4 以降、クラシック UI は非推奨となったため、デフォルトのオーサリングモードがクラシック UI に設定されている場合、問題が発生するようになりました。

### タッチ UI ダイアログが必要なダイアログを持つコンポーネント {#oakpal-components-dialogs}

**キー**：ComponentWithOnlyClassicUIDialog

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

最適なオーサリングエクスペリエンスを提供し、クラシック UI がサポートされない Cloud Service デプロイメントモデルとの互換性を維持するために、クラシック UI ダイアログを含む AEM コンポーネントには、常にタッチ UI ダイアログが必要です。このルールは、次のシナリオを検証します。

* クラシック UI ダイアログ（ダイアログの子ノード）を持つコンポーネントには、対応するタッチ UI ダイアログ（`cq:dialog` 子ノード）が必要です。
* クラシック UI デザインダイアログ（design_dialog ノード）を含むコンポーネントには、対応するタッチ（`cq:design_dialog` 子ノード）が必要です。
* クラシック UI ダイアログとクラシック UI デザインダイアログの両方を持つコンポーネントには、対応するタッチ UI ダイアログと対応するタッチ UI デザインダイアログの両方が必要です。

AEM 最新化ツールのドキュメントには、コンポーネントをクラシック UI からタッチ UI に変換する方法に関するドキュメントとツールが記載されています。詳しくは、[AEM 最新化ツール](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html)を参照してください。

### 可変コンテンツと不変コンテンツをパッケージに混在させない {#oakpal-packages-immutable}

**キー**：ImmutableMutableMixedPackage

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

Cloud Service のデプロイメントモデルとの互換性を維持するために、個々のコンテンツパッケージには、リポジトリーの不変領域のコンテンツ（つまり、`/apps and /libs, although /libs` を顧客コードで変更すると、別の違反を引き起こします）または可変領域（その他すべて）のいずれかを含める必要があります。例えば、`/apps/myco/components/text and /etc/clientlibs/myco` の両方を含むパッケージは Cloud Service と互換性がなく、問題が報告されます。

詳しくは、[AEM プロジェクト構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)を参照してください。

### リバースレプリケーションエージェントは使用しない {#oakpal-reverse-replication}

**キー**：ReverseReplication

**タイプ**：コードスメル／Cloud Service との互換性

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2020.5.0

[リリースノート：レプリケーションエージェントの削除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=ja#replication-agents)で説明されているように、リバースレプリケーションのサポートは Cloud Service のデプロイメントでは利用できません。

リバースレプリケーションを使用するお客様は、アドビに問い合わせて、代替ソリューションをご利用ください。

### OakPAL - プロキシ対応のクライアントライブラリに含まれるリソースは、「resources」という名前のフォルダー内に存在する必要がある {#oakpal-resources-proxy}

**キー**：ClientlibProxyResource

**タイプ**：バグ

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM クライアントライブラリには、画像やフォントなどの静的なリソースが含まれる場合があります。[プリプロセッサーの使用](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)で説明しているように、プロキシ化されたクライアントライブラリを使用する場合、パブリッシュインスタンスで効果的に参照するために、これらの静的リソースを resources という名前の子フォルダーに格納する必要があります。

#### 準拠していないコード {#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 準拠しているコード {#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL - Cloud Service と互換性のないワークフロープロセスの使用 {#oakpal-usage-cloud-service}

**キー**：CloudServiceIncompatibleWorkflowProcess

**タイプ**：バグ

**深刻度**：重大

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service 上でアセット処理をおこなうためにアセットマイクロサービスに移行すると、AEM のオンプレミスバージョンと AMS バージョンで使用されていたワークフロープロセスが、サポートされなくなる、または不要になります。[aem-cloud-migration](https://github.com/adobe/aem-cloud-migration) にある移行ツールを使用して、AEM Cloud Service の移行中にワークフローモデルを更新できます。

### OakPAL - 静的なテンプレートより編集可能なテンプレートを使用する {#oakpal-static-template}

**キー**：StaticTemplateUsage

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

従来、AEM プロジェクトは静的テンプレートを使用することが一般的でしたが、編集可能なテンプレートは最も柔軟性が高く、静的なテンプレートにはない追加機能をサポートしているため、このテンプレートの使用を強くお勧めします。詳しくは、[ページテンプレートを参照してください。](/help/implementing/developing/components/templates.md)静的なテンプレートから編集可能なテンプレートへの移行は、[AEM Modernization Tools](https://opensource.adobe.com/aem-modernize-tools/) を使用して、ほとんど自動化することができます。

### OakPAL - 従来の基盤コンポーネントの使用は推奨されない {#oakpal-usage-legacy}

**キー**：LegacyFoundationComponentUsage

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

一部の AEM リリースでは、従来の基盤コンポーネント（`/libs/foundation` 配下のコンポーネントなど）は廃止され、WCM コアコンポーネントに置き換わりました。カスタムコンポーネントの基盤として従来の基盤コンポーネントを使用することは（オーバーレイか継承かに関わらず）お勧めしません。対応するコアコンポーネントに変換する必要があります。この変換は、[AEM 最新化ツール](https://opensource.adobe.com/aem-modernize-tools/)で容易におこなうことができます。

### OakPAL - サポートされている実行モード名および順序のみを使用する {#oakpal-supported-runmodes}

**キー**：SupportedRunmode

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、実行モード名には厳密な命名ポリシーと実行モードな厳密な順序が適用されます。サポートされている実行モードのリストは[実行モード](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#runmodes)で確認でき、これから逸脱した場合は問題と見なされます。

### OakPAL - カスタム検索インデックス定義ノードは、/oak:index の直接の子にする {#oakpal-custom-search}

**キー**：OakIndexLocation

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが oak:QueryIndexDefinition など）が `/oak:index` の直接の子ノードである必要があります。AEM Cloud Service と互換性を持たせるため、他の場所にあるインデックスは移動する必要があります。検索インデックスの詳細については、[コンテンツ検索とインデックス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja)を参照してください。

### OakPAL - カスタム検索インデックス定義ノードの compatVersion は 2 にする {#oakpal-custom-search-compatVersion}

**キー**：IndexCompatVersion

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが oak:QueryIndexDefinition など）の compatVersion プロパティを 2 に設定する必要があります。その他の値は、AEM Cloud Service ではサポートされていません。検索インデックスの詳細については、[コンテンツ検索とインデックス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja)を参照してください。

### OakPAL - カスタム検索インデックス定義ノードの子孫ノードのタイプは、nt:unstructured にする {#oakpal-descendent-nodes}

**キー**：IndexDescendantNodeType

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

カスタムの検索インデックス定義ノードに、順序が指定されていない子ノードがある場合、問題のトラブルシューティングが難しくなる可能性があります。これを避けるために、`oak:QueryIndexDefinition` ノードのすべての子孫ノードは、タイプを nt:unstructured にすることをお勧めします。

### OakPAL - カスタム検索インデックス定義ノードには、子を持つ indexRules という名前の子ノードを含める {#oakpal-custom-search-index}

**キー**：IndexRulesNode

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

適切に定義されたカスタム検索インデックス定義ノードには、indexRules という名前の子ノードが含まれている必要があります。このノードには、少なくとも 1 つの子が必要です。詳細については、[Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/lucene.html)を参照してください。

### OakPAL - カスタム検索インデックス定義ノードは命名規則に従う {#oakpal-custom-search-definitions}

**キー**：IndexName

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが `oak:QueryIndexDefinition`）に、[コンテンツ検索とインデックス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#how-to-use)に記載されているパターンに従った名前を付ける必要があります。

### OakPAL - カスタム検索インデックス定義ノードはインデックスタイプ lucene を使用する   {#oakpal-index-type-lucene}

**キー**：IndexType

**タイプ**：バグ

**重大度**：ブロッカー

**最初の対象バージョン**：バージョン2021.2.0（2021.8.0でタイプと重大度が変更されました）

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが oak:QueryIndexDefinition など）に、値が **lucene** に設定された type プロパティが必要です。AEM Cloud Service に移行する前に、従来のインデックスタイプを使用したインデックス作成を更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#how-to-use)を参照してください。

### OakPAL - カスタム検索インデックス定義ノードに seed という名前のプロパティを含めない {#oakpal-property-name-seed}

**キー**：IndexSeedProperty

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが `oak:QueryIndexDefinition`）に seed という名前のプロパティを含めるこが禁止されています。AEM Cloud Service に移行する前に、このプロパティを使用しているインデックスを更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#how-to-use)を参照してください。

### OakPAL - カスタム検索インデックス定義ノードに reindex という名前のプロパティを含めない {#oakpal-reindex-property}

**キー**：IndexReindexProperty

**タイプ**：コードスメル

**深刻度**：軽度

**最初の対象バージョン**：バージョン 2021.2.0

AEM Cloud Service では、カスタム検索インデックス定義（ノードのタイプが `oak:QueryIndexDefinition`）に reindex という名前のプロパティを含めることが禁止されています。AEM Cloud Service に移行する前に、このプロパティを使用しているインデックスを更新する必要があります。詳しくは、[コンテンツの検索とインデックス作成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#how-to-use)を参照してください。
