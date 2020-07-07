---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 100%

---


# ログ{#logging}

AEM as a Cloud Service は、カスタムコードを含めて、顧客ベースに独自のエクスペリエンスを作成する顧客のためのプラットフォームです。このことを念頭に置いた上で、ログは、クラウド環境のカスタムコードをデバッグするため、特にローカル開発環境向けの重要な機能です。


<!-- ## Global Logging {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. This defines the global settings for logging in AEM as a Cloud Service:

* the logging level
* the location of the central log file
* the number of versions to be kept
* version rotation; either maximum size or a time interval
* the format to be used when writing the log messages
-->

## AEM as a Cloud Service のログ {#aem-as-a-cloud-service-logging}

AEM as a Cloud Service は設定の可能性を提供します。

* 中央のログサービスのグローバルパラメーター
* 要求データのログ（要求情報用の特殊なログ設定）
* 個々のサービス固有の設定

ローカル開発の場合、ログエントリは `/crx-quickstart/logs` フォルダーのローカルファイルに書き込まれます。

クラウド環境では、開発者は Cloud Manager を使用してログをダウンロードするか、コマンドラインツールを使用してログを追跡することができます。

>[!NOTE]
>
>AEM as a Cloud Service にログインする方法は、Sling プリンシパルに基づいています。詳しくは [Sling の Logging](https://sling.apache.org/site/logging.html) を参照してください。

## AEM as a Cloud Service の Java のログ {#aem-as-a-cloud-service-java-logging}

### 標準のロガーおよびライター {#standard-loggers-and-writers}

>[!IMPORTANT]
>
>これらは必要に応じてカスタマイズできますが、ほとんどのインストールには標準設定が適しています。ただし、標準のログ設定をカスタマイズする必要がある場合は、必ず `dev` 環境でおこないます。

一部のロガーとライターは、AEM as a Cloud Service の標準インストールとして含まれています。

1 つ目は特殊なケースで、`request` と `access` ログの両方を制御します。

* ロガー：

   * Apache Sling Customizable Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 要求コンテンツに関するメッセージを `request.log` に書き込みます。

* リンク先：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * メッセージを `request.log` または `access.log` に書き込みます。

その他のペアは、標準設定に従います。

* ロガー：

   * Apache Sling Logging Logger Configuration

      (org.apache.sling.commons.log.LogManager.factory.config)

   * `logs/error.log` にメッセージ `Information` を書き込みます。

* リンク先のライター：

   * Apache Sling Logging Writer Configuration

      (org.apache.sling.commons.log.LogManager.factory.writer)

* ロガー：

   * Apache Sling Logging Logger Configuration（org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7）

   * サービス `org.apache.pdfbox` のメッセージ `Warning` を `../logs/error.log` に書き込みます。

* 特定のライターにリンクしないので、デフォルト設定で暗黙のライターを作成して使用します。

**AEM as a Cloud Service の HTTP リクエストのログ**


AEM WCM およびリポジトリに対するアクセス要求はすべてここに登録されます。

出力例：

**AEM as a Cloud Service の HTTP リクエスト／レスポンシブアクセスログ**


各アクセス要求が、応答と共にここに登録されます。

出力例：

**Apache Web サーバー／Dispatcher ログ**

Dispatcher 問題のデバッグに使用するログです。詳しくは、[Apache および Dispatcher 設定のデバッグ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/)を参照してください。

<!-- Besides the three types of logs present on an AEM as a Cloud Service instance (`request`, `access` and `error` logs) there is another dispatcher/overview.html#debugging-apache-and-dispatcher-configuration.

leftover text from the last breakaway chunk (re dispatcher) -->

基本的な実践に関しては、現在 AEM as a Cloud Service の Maven アーキタイプとして存在する設定に合わせて調整することをお勧めします。これらは、特定の環境タイプに対して異なるログ設定とレベルを設定します。

* `local dev` と `dev` 環境の場合、`error.log` に対し、ロガーを **DEBUG** レベルに設定
* `stage`の場合、`error.log` に対し、ロガーを **WARN** レベルに設定
* `prod` の場合、`error.log` に対し、ロガーを **ERROR** レベルに設定

各設定の例を以下に示します。

* `dev` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="debug"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```


* `stage` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="warn"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

* `prod` 環境：

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="error"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

### 個々のサービス用のロガーとライター {#loggers-and-writers-for-individual-services}

グローバルログ設定に加えて、AEM as a Cloud Service では個々のサービス用に具体的な設定をおこなうことができます。

* 具体的なログレベル
* ロガー（ログメッセージを提供する OSGi サービス）

これにより、単一のサービスに関するログメッセージを別個のファイルに送ることができます。これは、開発やテストの際、例えば特定のサービスのログレベルを上げる必要がある場合などに特に便利です。

AEM as a Cloud Service では、次の情報を使用してログメッセージをファイルに書き込みます。

1. **OSGi サービス**（ロガー）がログメッセージを書き込みます。
1. **Logging Logger** がこのメッセージを受け取り、仕様に従って書式設定します。
1. **Logging Writer** が、これらすべてのメッセージを、定義済みの物理ファイルに書き込みます。

これらの要素は、該当する要素の次のパラメーターによってリンクされます。

* **ロガー（Logging Logger）**

   メッセージを生成するサービスを定義します。

<!-- * **Log File (Logging Logger)**

  Define the physical file for storing the log messages.

  This is used to link a Logging Logger with a Logging Writer. The value must be identical to the same parameter in the Logging Writer configuration for the connection to be made.

* **Log File (Logging Writer)**

  Define the physical file that the log messages will be written to.

  This must be identical to the same parameter in the Logging Writer configuration, or the match will not be made. If there is no match then an implicit Writer will be created with default configuration (daily log rotation).
-->

### ログレベルの設定 {#setting-the-log-level}

クラウド環境のログレベルを変更するには、Sling Logging OSGi 設定を変更した後、完全に再デプロイする必要があります。これは即座にはおこなわれないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にする場合は注意が必要です。今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
>以下に示す設定の変更を実行するには、ローカルの開発環境で設定の変更を作成し、それらを AEM as a Cloud Service インスタンスにプッシュする必要があります。この方法について詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。

**デバッグログレベルのアクティベート**

>[!WARNING]
>
>DEBUG ログレベルをグローバルにアクティベートすると、大量の情報が生成され、情報の切り分けが難しくなります。デバッグが必要なサービスに対してのみ有効にすることをお勧めします。詳しくは、[個々のサービス用のロガーとライター](logging.md#loggers-and-writers-for-individual-services)を参照してください。

デフォルトのログレベルは情報（INFO）なので、デバッグ（DEBUG）メッセージはログに記録されません。DEBUG ログレベルをアクティブにするには、

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

このプロパティを debug に設定してください。多くのログが生成されるので、デバッグログレベルのログを不必要に長く残さないでください。デバッグファイルの行は、通常は DEBUG で始まり、その後にログレベル、インストーラーのアクション、ログメッセージが示されます。次に例を示します。

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

ログレベルは次のとおりです。

| 0 | 重大なエラー | アクションが失敗し、インストーラーの処理を続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。インストールは続行しますが、CRX の一部が正常にインストールされなかったので、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。CRX が正常に機能するかどうかは不明です。 |
| 3 | 情報 | アクションが成功しました。 |

### 独自のロガーおよびライターの作成 {#creating-your-own-loggers-and-writers}

次の手順で、独自のロガーとライターのペアを定義できます。

1. ファクトリ設定の [Apache Sling Logging Logger Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) の新しいインスタンスを作成します。

   1. ロガーを指定します。

<!-- 1. Create a new instance of the Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

    1. Specify the Log File - this must match that specified for the Logger.
    1. Configure the other parameters as required. -->

### ログの設定 {#configure-logging}

>[!NOTE]
>
>Adobe Experience Manager で作業をする際にはいくつかの方法でそのようなサービスの設定を管理できます。

状況によっては、異なるログレベルでカスタムログを作成する必要があります。リポジトリでは、次の方法で実行できます。

1. 既存のものがない場合は、新しい設定フォルダー（`sling:Folder`）を、プロジェクト（`/apps/<*project-name*>/config`）用に作成します。
1. `/apps/<*project-name*>/config` の下に、新しい Apache Sling Logging Logger Configuration 用のノードを作成します。

   * 名前：`org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>`（ロガーの場合）

      `<*identifier*>` の部分は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。

      例：`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * タイプ：`sling:OsgiConfig`
   >[!NOTE]
   >
   >技術的に必須ではありませんが、`<*identifier*>` は一意にすることをお勧めします。

<!-- 1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: String

      Value: specify the Log File; for example, `logs/myLogFile.log`

    * Name: `org.apache.sling.commons.log.names`

      Type: String[] (String + Multi)

      Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`
        * `org.apache.felix`
        * `com.day`

    * Name: `org.apache.sling.commons.log.level`

      Type: String

      Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern`

          Type: `String`

          Value: specify the pattern of the log message as required; for example,

          `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supports up to six arguments.

   >
   >
   >{0} The timestamp of type `java.util.Date`
   >{1} the log marker
   >{2} the name of the current thread
   >{3} the name of the logger
   >{4} the log level
   >{5} the log message

   >
   >
   >If the log call includes a `Throwable` the stacktrace is appended to the message.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names must have a value.

   >[!NOTE]
   >
   >Log writer paths are relative to the `crx-quickstart` location.
   >
   >
   >Therefore, a log file specified as:
   >
   >
   >`logs/thelog.log`

   >
   >
   >writes to:
   >
   >
   >`` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   >
   >
   >And a log file specified as:
   >
   >
   >`../logs/thelog.log`

   >
   >
   >writes to a directory:
   >
   >
   >` <*cq-installation-dir*>/logs/`
   >``(i.e. next to ` `<*cq-installation-dir*>/`crx-quickstart/`)
 -->

<!-- open question: see if we need to leave the above warning note in place, but adjust it so that it doesn't mention filenames -->

<!-- 1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer).

   >[!CAUTION]
   >
   >A new Logging Writer Configuration is only required when the existing default is not suitable.

   >
   >
   >If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer)

      As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: `String`

      Value: specify the Log File so that it matches the file specified in the Logger;

      for this example, `../logs/myLogFile.log`.

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number`

          Type: `Long`

          Value: specify the number of log files you want kept; for example, `5`

        * Name: `org.apache.sling.commons.log.file.size`

          Type: `String`

          Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controls the rotation of the log file by setting either:
   >
   >* a maximum file size
   >* a time/date schedule
   >
   >to indicate when a new file will be created (and the existing file renamed according to the name pattern).
   >
   >* A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - `KB`, `MB`, or `GB` (case is ignored).
   >* A time/date schedule can be specified as a `java.util.SimpleDateFormat` pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).
   >
   >The default is '.'yyyy-MM-dd (for daily log rotation).
   >
   >So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.
   >
   >      | `'.'yyyy-MM` |Rotation at the beginning of each month |
   >      |---|---|
   >      | `'.'yyyy-ww` |Rotation at the first day of each week (depends on the locale). |
   >      | `'.'yyyy-MM-dd` |Rotation at midnight each day. |
   >      | `'.'yyyy-MM-dd-a` |Rotation at midnight and midday of each day. |
   >      | `'.'yyyy-MM-dd-HH` |Rotation at the top of every hour. |
   >      | `'.'yyyy-MM-dd-HH-mm` |Rotation at the beginning of every minute. |
   >
   >      Note: When specifying a time/date:
   >      1. You should "escape" literal text within a pair of single quotes (' ');
   >      this is to avoid certain characters being interpreted as pattern letters.
   >      1. Only use characters allowed for a valid file name anywhere in the option.

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`. -->

Felix コンソールでは、`../system/console/slinglog` の Sling Log Support に関する情報も提供されます。例えば、`https://localhost:4502/system/console/slinglog`.draf です。

## ログへのアクセスと管理 {#manage-logs}

ログにアクセスして管理する方法について詳しくは、[Cloud Manager のドキュメントを参照してください](/help/implementing/cloud-manager/manage-logs.md)。