---
title: ログ
description: 一元的なログサービスのグローバルパラメーターの設定、個々のサービスに特有の設定、またはデータのログ記録の要求をおこなう方法を学習します。
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# ログ{#logging}

AEMをクラウドサービスオファーとして設定できます。

* 中央のログサービスのグローバルパラメーター
* 要求データのログ（要求情報用の特殊なログ設定）
* 個々のサービスに特有の設定（個々のログファイルおよびログメッセージの書式など）

For local development, logs entries are written to local files in the `/crx-quickstart/logs` folder.

クラウド環境では、開発者は Cloud Manager を使用してログをダウンロードするか、コマンドラインツールを使用してログを追跡することができます。

>[!NOTE]
>
>AEMにクラウドサービスとしてログインする方法は、Slingの原則に基づいています。 詳しくは [Sling Logging](https://sling.apache.org/site/logging.html) を参照してください。

## グローバルログ {#global-logging}

[Apache Sling Logging Configurationは](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) 、ルートロガーの設定に使用します。 これは、AEMにクラウドサービスとしてログインするためのグローバル設定を定義します。

* ログレベル
* 主要なログファイルの場所
* 保存するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式

## 個々のサービス用のロガーとライター {#loggers-and-writers-for-individual-services}

グローバルログの設定に加え、AEMをクラウドサービスとして使用すると、個々のサービスに対して次のような特定の設定を行うことができます。

* 具体的なログレベル
* 個々のログファイルの場所
* 保存するバージョンの数
* バージョンのローテーション（最大サイズまたは期間）
* ログメッセージを書き込むときに使用する形式
* ロガー（ログメッセージを提供する OSGi サービス）

これにより、単一のサービスに関するログメッセージを別個のファイルに送ることができます。これは、開発やテストの際、例えば特定のサービスのログレベルを上げる必要がある場合などに特に便利です。

クラウドサービスとしてのAEMでは、次の情報を使用してログメッセージをファイルに書き込みます。

1. **OSGi サービス**（ロガー）がログメッセージを書き込みます。
1. **Logging Logger** がこのメッセージを受け取り、仕様に従って書式設定します。
1. **Logging Writer** が、これらすべてのメッセージを、定義済みの物理ファイルに書き込みます。

これらの要素は、該当する要素の次のパラメーターによってリンクされます。

* **Logger(Logging Logger)**

   メッセージを生成するサービスを定義します。

* **ログファイル(Logging Logger)**

   ログメッセージを保存する物理ファイルを定義します。

   これは、ロギング・ロガーとロギング・ライターをリンクするために使用されます。 接続を行うには、ログライター設定の同じパラメータと値が同じである必要があります。

* **ログファイル（ログライター）**

   ログメッセージの書き込み先の物理ファイルを定義します。

   これは、ログ・ライター構成の同じパラメータと同じである必要があります。同じでない場合、一致は行われません。 一致がない場合は、暗黙的なWriterがデフォルト設定（日次ログローテーション）で作成されます。

### 標準のロガーおよびライター {#standard-loggers-and-writers}

一部のロガーおよびライターは、クラウドサービスの標準インストールとしてAEMに含まれています。

1 つ目は特殊なケースで、`request.log` ファイルと `access.log` ファイルの両方を制御します。

* ロガー：

   * Apache Sling Customizable Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 要求コンテンツに関するメッセージを `request.log` に書き込みます。

* リンク先：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Writes the messages to either `request.log` or `access.log`.

これらは必要に応じてカスタマイズできますが、ほとんどのインストールには標準設定が適しています。

その他のペアは、標準設定に従います。

* ロガー：

   * Apache Sling Logging Loggerの設定

      (org.apache.sling.commons.log.LogManager.factory.config)

   * にメッセージ `Information` を書き込みま `logs/error.log`す。

* リンク先のライター：

   * Apache Slingログライターの設定

      (org.apache.sling.commons.log.LogManager.factory.writer)

* ロガー：

   * Apache Sling Logging Logger Configuration（org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7）

   * サービス `Warning` のメッセージ `../logs/error.log` をに書き込みま `org.apache.pdfbox`す。

* 特定のライターにリンクしないので、デフォルト設定で暗黙のライターを作成して使用します（毎日のログローテーション）。

## ログレベルの設定 {#setting-the-log-level}

クラウド環境のログレベルを変更するには、Sling Logging OSGi 設定を変更した後、完全に再デプロイする必要があります。これは即座にはおこなわれないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にする場合は注意が必要です。今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
> 以下に示す設定の変更を実行するには、ローカルの開発環境で設定の変更を作成し、それらをクラウドサービスインスタンスとしてAEMにプッシュする必要があります。 この方法について詳しくは、「クラウドサービスとしてのAEM [へのデプロイ」を参照してください](/help/implementing/deploying/overview.md)。

### デバッグログレベルのアクティベート {#activating-the-debug-log-level}

>[!WARNING]
>
> DEBUGログレベルをグローバルにアクティブ化すると、大量の情報が生成され、情報の切り替えが難しくなります。 デバッグが必要なサービスに対してのみ有効にすることをお勧めします。 詳しくは、個々のサービスのロ [ガーとライターを参照してください](logging.md#loggers-and-writers-for-individual-services)。

デフォルトのログレベルは情報（INFO）なので、デバッグ（DEBUG）メッセージはログに記録されません。DEBUGログレベルをアクティブにするには、

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

   1. ログファイルを指定します。
   1. ロガーを指定します。
   1. 必要に応じてその他のパラメーターを設定します。

1. ファクトリ設定の [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) の新しいインスタンスを作成します。

   1. ログファイルを指定します。ロガーに指定したものと同じファイルを指定する必要があります。
   1. 必要に応じてその他のパラメーターを設定します。

### カスタムログファイルの作成 {#create-a-custom-log-file}

>[!NOTE]
>
>Adobe Experience Managerを使用する場合、このようなサービスの設定を管理する方法がいくつかあります。

状況によっては、別のログレベルでカスタムログファイルを作成する必要があります。これをおこなうには、リポジトリで次の手順を実行します。

1. If not already existing, create a new configuration folder ( `sling:Folder`) for your project `/apps/<*project-name*>/config`.
1. Under `/apps/<*project-name*>/config`, create a node for the new Apache Sling Logging Logger Configuration:

   * 名前： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` （ロガーの場合）

      Where `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information).

      例：`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * タイプ: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

1. このノードで次のプロパティを設定します。

   * 名前: `org.apache.sling.commons.log.file`

      タイプ：String

      値：ログファイルの指定例えば、 `logs/myLogFile.log`

   * 名前: `org.apache.sling.commons.log.names`

      タイプ：文字列[] （文字列+複数）

      値：ロガーがメッセージをログに記録するOSGiサービスを指定する。例えば、次のすべての例を示します。

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名前: `org.apache.sling.commons.log.level`

      タイプ：String

      値：必要なログレベル(、、ま `debug`たは `info``warn` )を指 `error`定します。例えば `debug`

   * 必要に応じてその他のパラメーターを設定します。

      * 名前: `org.apache.sling.commons.log.pattern`

         タイプ: `String`

         値：必要に応じて、ログメッセージのパターンを指定します。例えば、

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` では、最大 6 個の引数がサポートされています。

   >{0}タイプのタイムスタンプ `java.util.Date`
   >
   >ログマーカー{1}{2}現在のスレッドの名前{3}ログレベル{4}のロガー名{5}ログメッセージ

   >ログ呼び出しに `Throwable` が含まれている場合は、スタックトレースがメッセージに付加されます。

   >[!CAUTION]
   org.apache.sling.commons.log.names には値が必要です。

   >[!NOTE]
   ログライターのパスは、`crx-quickstart` の場所と相対的です。
   したがって、ログファイルが
   `logs/thelog.log`

   >と指定されている場合、書き込み先は以下となります。
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   また、ログファイルが
   `../logs/thelog.log`

   >と指定されている場合、書き込み先は以下のディレクトリとなります。
   ` <*cq-installation-dir*>/logs/`
&quot;(例： ` `&lt;*cq-installation-dir*>/の横`crx-quickstart/`)

1. この手順は、新しいライターが必要な場合（つまり、デフォルトのライターとは異なる設定の場合）にのみ必要です。

   >[!CAUTION]
   新しい Logging Writer Configuration は、既存のデフォルトが適切でない場合にのみ必要です。

   >明示的なライターが設定されていない場合は、デフォルトに基づいて暗黙のライターが自動的に生成されます。

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

   * 名前：(こ `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` れは作家なので)

      ロガーと同様、は、イン `<*identifier*>` スタンスを識別するために（必須の）入力する自由なテキストに置き換えられます（この情報は省略できません）。 例：`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * タイプ: `sling:OsgiConfig`
   >[!NOTE]
   Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   このノードで次のプロパティを設定します。

   * 名前: `org.apache.sling.commons.log.file`

      タイプ: `String`

      値：ログファイルを指定して、ロガーで指定されたファイルと一致するようにします。

      例えば、 `../logs/myLogFile.log`「

   * 必要に応じてその他のパラメーターを設定します。

      * 名前: `org.apache.sling.commons.log.file.number`

         タイプ: `Long`

         Value: specify the number of log files you want kept; for example, `5`

      * 名前: `org.apache.sling.commons.log.file.size`

         タイプ: `String`

         Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` は、次のいずれかを設定することによって、ログファイルのローテーションを制御します。
   * 最大ファイルサイズ
   * 時刻／日付のスケジュール
   これにより、新しいファイルを作成する（また、名前のパターンに従って既存のファイルを名前変更する）条件を示します。
   * サイズ制限は数値で指定できます。 サイズインジケーターを指定しない場合は、バイト数と見なされるか、サイズインジケーター(、、または、大文字と小文字の区別な `KB`し) `MB`の1つ `GB` を追加できます。
   * 日時スケジュールは、パターンとして指定で `java.util.SimpleDateFormat` きます。 これは、ファイルの回転が終わるまでの期間を定義します。また、回転されたファイルに追加されるサフィックスも表します（識別用）。
   デフォルトは「。」です。yyyy-MM-dd（日別ログのローテーション用）。
   例えば、2010年1月20日の真夜中（またはこの後の最初のログメッセージが正確である場合）、../logs/error.logの名前は../logs/error.log.2010-01-20に変更されます。 1月21日のログは、次の日の変更時にロールオーバーされるまで、（新しい空の）../logs/error.logに出力されます。
       | `&#39;.&#39;yyyy-MM` |Rotation at the beginning of each month |
       |---|---|
       | `&#39;.&#39;yyyy-ww`|各週の最初の日のローテーション（ロケールによって異なります）。 |
       | `&#39;.&#39;yyyy-MM-dd`|毎日午前0時にローテーション。 |
       | `&#39;.&#39;yyyy-MM-dd-a`|毎日午前0時と午後のローテーション。 |
       | `&#39;.&#39;yyyy-MM-dd-HH`|毎時の最初のローテーション。 |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`|毎分の最初の回転。 |
    
    注意：日時を指定する場合：
      1.一重引用符(&#39; &#39;)のペア内で、リテラルテキストを「エスケープ」する必要があります。
  これは、     特定の文字がパターン文字として解釈されるのを防ぐためです。
       1. オプションの任意の場所で、有効なファイル名に使用できる文字のみを使用します。
   

1. 任意のツールで新しいログファイルを読み取ります。

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`.

The Felix Console also provides information about Sling Log Support at `../system/console/slinglog`; for example `https://localhost:4502/system/console/slinglog`.draf