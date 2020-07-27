---
title: AEM as a Cloud Service の開発ガイドライン
description: 作成中
translation-type: tm+mt
source-git-commit: 0a2ae4e40cd342056fec9065d226ec064f8b2d1f
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 84%

---


# AEM as a Cloud Service の開発ガイドライン {#aem-as-a-cloud-service-development-guidelines}

AEM as a Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。インスタンスはいつ停止するかわからないので、コードには特に回復力が必要です。

AEM as a Cloud Service を更新する間、古いコードと新しいコードが並行して実行されるインスタンスが存在します。したがって、新しいコードで作成されたコンテンツが古いコードによって中断されず、新しいコードが古いコンテンツを処理できる必要があります。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

クラスター内のプライマリを識別する必要がある場合は、Apache Sling Discovery API を使用して検出できます。

## メモリ内の状態 {#state-in-memory}

状態はメモリ内ではなく、リポジトリ内に保持する必要があります。そうしないと、インスタンスが停止した場合に、状態が失われる可能性があります。

## ファイルシステムの状態 {#state-on-the-filesystem}

インスタンスのファイルシステムは、AEM as a Cloud Service で使用しないでください。ディスクは揮発性で、インスタンスが再利用されると破棄されます。単一の要求の処理に関する一時的なストレージのために、ファイルシステムの使用を制限することは可能ですが、大量のファイルに対して濫用しないでください。リソースの使用割り当てに悪影響を与え、ディスクの制限が生じる可能性があるためです。

ファイルシステムの使用がサポートされていない例として、パブリッシュ層では、永続化する必要のあるデータが、長期ストレージのために外部サービスに送り出されることを確認する必要があります。

## 監視 {#observation}

同様に、観察イベントに作用するように非同期的に起こっているものすべてに対して、ローカルで実行することを保証できないことから、注意深く使用する必要があります。これは、JCR リソースと Sling イベントの両方に当てはまります。変更が発生した時点で、インスタンスが停止し、別のインスタンスに置き換えられる場合があります。その時点でアクティブなトポロジ内の他のインスタンスは、このイベントに反応できます。しかし、この場合、ローカルのイベントではなく、イベントの発行時にアクティブなリーダーがいない可能性もあります。

## バックグラウンドタスクと長時間実行ジョブ {#background-tasks-and-long-running-jobs}

バックグラウンドタスクとして実行するコードでは、コードを実行しているインスタンスが突然機能しなくなる可能性があることを前提にする必要があります。したがって、コードは耐障害性が高く、再開可能でなければなりません。つまり、コードが再実行された場合は、再び最初から始めるのではなく、実行が中断された箇所に近い位置から始める必要があります。これはこの種のコードにとって新しい要件ではありませんが、AEM as a Cloud Service では、インスタンスの停止が起こる可能性が高くなります。

トラブルを最小限に抑えるために、長時間実行ジョブは可能な限り避け、少なくとも再開可能な状態になっている必要があります。このようなジョブを実行するには、少なくとも 1 回は実行されることが保証されている Sling ジョブを使用します。したがって、ジョブが中断された場合、ジョブはできるだけ早く再実行されます。ただし、最初からやり直すべきではないでしょう。このようなジョブをスケジュールする場合は、[Sling ジョブ](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing)スケジューラーを使用することをお勧めします。やはり、少なくとも 1 回は実行されることが保証されているからです。

Sling Commons Scheduler は実行を保証できないので、スケジュール設定には使用しないでください（スケジュール設定される可能性のほうが高いというだけで、保証されるものではありません）。

同様に、監視イベント（例：JCR イベントや Sling リソースイベント）に対する動作など、非同期的に発生するあらゆる動作は、必ずしも実行が保証されないので、慎重に使用する必要があります。これは、現在の AEM デプロイメントに既に当てはまります。

## 送信 HTTP 接続 {#outgoing-http-connections}

送信 HTTP 接続では、接続および読み取りの妥当なタイムアウトを設定することを強くお勧めします。これらのタイムアウトを適用しないコードの場合、AEM as a Cloud Service 上で動作している AEM インスタンスは、グローバルタイムアウトを強制的に適用します。一般的な次の Java ライブラリで使用される接続の場合、これらのタイムアウト値は、接続呼び出しについては 10 秒、読み取り呼び出しについては 60 秒です。

HTTP 接続をおこなう場合は、提供されている [Apache HttpComponents Client 4.x ライブラリ](https://hc.apache.org/httpcomponents-client-ga/)を使用することをお勧めします。

次の代替手段は、動作することはわかっていますが、依存関係を自分で指定しなければならない可能性があります。

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) と [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html)（AEM で提供）のいずれか一方または両方
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)（古くなり、バージョン 4.x に代わっているので、お勧めしません）
* [OK Http](https://square.github.io/okhttp/)（AEM では提供されません）

## クラシック UI のカスタマイズがない {#no-classic-ui-customizations}

AEM as a Cloud Service は、サードパーティの顧客コードのタッチ UI のみをサポートします。クラシック UI はカスタマイズには使用できません。

## ネイティブバイナリの回避 {#avoid-native-binaries}

コードは、実行時にバイナリをダウンロードしたり、変更したりすることはできません。例えば、`jar` や `tar` ファイルは解凍できません。

## AEM as a Cloud Service を使用したストリーミングバイナリがない {#no-streaming-binaries}

バイナリは CDN を通じてアクセスし、コア AEM サービスの外部でバイナリを提供します。

例えば、AEM サービスの揮発性ディスクへのバイナリのダウンロードをトリガーする `asset.getOriginal().getStream()` を使用しないでください。

## リバースレプリケーションエージェントがない {#no-reverse-replication-agents}

パブリッシュからオーサーへのリバースレプリケーションは、AEM as a Cloud Service ではサポートされていません。このような方法が必要な場合は、パブリッシュインスタンスのファームと、場合によってはオーサークラスターで共有される外部の永続化ストアを使用できます。

## 転送レプリケーションエージェントの移植が必要 {#forward-replication-agents}

コンテンツは、pub-sub メカニズムを使用してオーサーからパブリッシュにレプリケートされます。カスタムレプリケーションエージェントはサポートされていません。

## 監視とデバッグ {#monitoring-and-debugging}

### ログ {#logs}

ローカル開発の場合、ログエントリは`/crx-quickstart/logs` フォルダーのローカルファイルに書き込まれます。

クラウド環境では、開発者は Cloud Manager を使用してログをダウンロードするか、コマンドラインツールを使用してログを追跡することができます。<!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**ログレベルの設定**

クラウド環境のログレベルを変更するには、Sling Logging OSGi 設定を変更した後、完全に再デプロイする必要があります。これは即座にはおこなわれないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にする場合は注意が必要です。今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
>以下に示す設定の変更を実行するには、ローカルの開発環境で設定の変更を作成し、それらを AEM as a Cloud Service インスタンスにプッシュする必要があります。この方法について詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。

**デバッグログレベルのアクティベート**

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

### スレッドダンプ {#thread-dumps}

クラウド環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。しばらくの間は、問題のデバッグ用にスレッドダンプが必要な場合は、AEM サポートに連絡して、正確な時間枠を指定してください。

## CRXDE Lite とシステムコンソール {#crxde-lite-and-system-console}

### ローカル開発 {#local-development}

ローカル開発の場合、開発者は CRXDE Lite（`/crx/de`）と AEM Web コンソール（`/system/console`）に完全にアクセスできます。

（クラウド対応クイックスタートを使用する）ローカル開発では、`/apps` と `/libs` に直接書き込むことができます。この点が、最上位フォルダーが不変なクラウド環境とは異なります。

### AEM as a Cloud Service の開発ツール {#aem-as-a-cloud-service-development-tools}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージ環境や実稼動環境ではアクセスできません。不変リポジトリ（`/libs`、`/apps`）に実行時に書き込むことはできないので、書き込もうとするとエラーが発生します。

AEM as a Cloud Service 開発者環境でデバッグするためのツールセットが開発環境、ステージ環境、実稼動環境の開発者コンソールで利用できます。URL は、次のようにオーサーサービス URL またはパブリッシュサービス URL を調整して決定できます。

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

ショートカットとして、次の Cloud Manager CLI コマンドを使用して、下記の環境パラメーターに基づいて開発者コンソールを起動できます。

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

詳しくは、[こちらのページ](/help/release-notes/home.md)を参照してください。

開発者は、ステータス情報を生成し、様々なリソースを解決できます。

下図に示すように、使用可能なステータス情報には、バンドルの状態、コンポーネント、OSGi 設定、Oak インデックス、OSGi サービス、Sling ジョブなどがあります。

![開発者コンソール 1](/help/implementing/developing/introduction/assets/devconsole1.png)

下図に示すように、開発者はパッケージの依存関係とサーブレットを解決できます。

![開発者コンソール 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開発者コンソール 3](/help/implementing/developing/introduction/assets/devconsole3.png)

また、デバッグにも便利です。開発者コンソールには、次のように「クエリの説明を実行」ツールへのリンクがあります。

![開発者コンソール 4](/help/implementing/developing/introduction/assets/devconsole4.png)

通常のプログラムの場合、開発者コンソールへのアクセスは Admin Console の「Cloud Manager - デベロッパーロール」で定義されます。一方、サンドボックスプログラムの場合、開発者コンソールは、AEM as a Cloud Service へのアクセスを可能にする製品プロファイルを持つすべてのユーザーが使用できます。すべてのプログラムで、ステータスダンプには「Cloud Manager - デベロッパーロール」が必要です。また、オーサーサービスとパブリッシュサービスの両方のステータスダンプデータを表示するには、ユーザーがそれら両方のサービスで製品の AEM ユーザープロファイルまたは AEM 管理者プロファイルにも定義されている必要があります。ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)を参照してください。


### AEM のステージング環境および実稼動環境用サービス {#aem-staging-and-production-service}

ユーザーは、ステージング環境と実稼動環境用の開発者ツールにはアクセスできません。

### パフォーマンスの監視 {#performance-monitoring}

アドビはアプリケーションのパフォーマンスを監視し、劣化が観察された場合に対処します。現時点では、アプリケーションの指標を確認できません。

## 専用出力IPアドレス

AEMは要求に応じて、Cloud Serviceとして、JavaコードでプログラムされたHTTP（ポート80）およびHTTPS（ポート443）送信トラフィック用の静的な専用のIPアドレスを提供します。

### メリット

この専用IPアドレスは、SaaSベンダー（CRMベンダーなど）や、AEM以外の統合をIPアドレスの許可リストをオファーするCloud Serviceとして統合する場合のセキュリティを強化します。 専用のIPアドレスを許可リストに追加することで、顧客のAEMCloud Serviceからのトラフィックのみが外部サービスに送信できるようにします。 これは、他のIPからのトラフィックに加えて、許可されているものです。

専用のIPアドレス機能を有効にしないと、Cloud ServiceとしてAEMから出てくるトラフィックは、他の顧客と共有される一連のIPを通って流れます。

### 設定

専用のIPアドレスを有効にするには、IPアドレス情報を提供するカスタマーサポートにリクエストを送信します。 リクエストは、環境ごとに行う必要があります。この中には、最初のリクエストの後に作成される新しい環境が含まれます。

### 機能の使用

この機能は、プロキシ設定に標準のJavaシステムプロパティを使用する場合、送信トラフィックの原因となるJavaコードまたはライブラリと互換性があります。 実際には、これには最も一般的なライブラリが含まれる必要があります。

次にコード例を示します。

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

同じ専用IPが、アドビの組織内のすべてのお客様のプログラムと、各プログラム内のすべての環境に適用されます。 作成者サービスと発行サービスの両方に適用されます。

HTTPポートとHTTPSポートのみがサポートされます。 これには、HTTP/1.1と、暗号化時のHTTP/2が含まれます。

### デバッグの考慮事項

予想される専用IPアドレスでトラフィックが実際に送信されていることを検証するには、目的のサービスでログインする（可能な場合）ことを確認します。 それ以外の場合は、 [https://ifconfig.me/ipなどのデバッグサービスを呼び出すと、呼び出し元のIPアドレスが返されるので便利です](https://ifconfig.me/ip)。
