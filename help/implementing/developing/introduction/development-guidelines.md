---
title: AEM as a Cloud Service の開発ガイドライン
description: 作成中
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# AEM as a Cloud Service の開発ガイドライン {#aem-as-a-cloud-service-development-guidelines}

AEMでクラウドサービスとして実行するコードは、常にクラスター内で実行されていることを認識している必要があります。 つまり、常に複数のインスタンスが実行されています。 コードは、特にインスタンスがいつでも停止する可能性があるので、回復力が必要です。

AEMをクラウドサービスとして更新する際に、古いコードと新しいコードが並行して実行されるインスタンスが発生します。 したがって、古いコードは新しいコードで作成されたコンテンツと区別できず、新しいコードは古いコンテンツを処理できる必要があります。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

クラスター内のマスターを識別する必要がある場合は、Apache Sling Discovery APIを使用して検出できます。

## メモリ内の状態 {#state-in-memory}

状態はメモリ内に保持せず、リポジトリ内に保持する必要があります。 そうしないと、インスタンスが停止した場合に、この状態が失われる可能性があります。

## ファイル・システムの状態 {#state-on-the-filesystem}

インスタンスのファイルシステムは、AEMでクラウドサービスとして使用しないでください。 ディスクは一時的で、インスタンスが再利用されると破棄されます。 単一の要求の処理に関する一時的なストレージのために、ファイルシステムの使用を制限することは可能ですが、大量のファイルに対しては悪用しないでください。 これは、リソースの使用割り当てに悪影響を与え、ディスクの制限が生じる可能性があるためです。

ファイルシステムの使用がサポートされていない例として、発行層では、永続化する必要のあるデータが、長期的なストレージのために外部サービスに出荷されることを確認する必要があります。

## 監視 {#observation}

同様に、観察イベントに作用するように非同期的に起こっているものすべてについては、ローカルで実行することを保証できず、注意深く使用する必要があります。 これは、JCRリソースとSlingイベントの両方に当てはまります。 変更が発生した時点で、インスタンスがダウンされ、別のインスタンスに置き換えられる場合があります。 その時点でアクティブなトポロジ内の他のインスタンスは、そのインスタンスに反応できます。イベント しかし、この場合、これは地元のイベントではなく、イベントの発行時には現役のリーダーがいない可能性もある。

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
* [OK Http](https://square.github.io/okhttp/) （AEMでは提供されません）

## クラシックUIのカスタマイズなし {#no-classic-ui-customizations}

クラウドサービスとしてのAEMは、サードパーティの顧客コードのタッチUIのみをサポートします。 クラシックUIはカスタマイズには使用できません。

## ネイティブバイナリの回避 {#avoid-native-binaries}

コードは、実行時にバイナリをダウンロードしたり、変更したりすることはできません。 例えば、ファイルを解凍できなくな `jar` りま `tar` す。

## AEMをクラウドサービスとして使用したストリーミングバイナリの使用なし {#no-streaming-binaries}

バイナリはCDNを通じてアクセスし、コアAEMサービスの外部でバイナリを提供します。

例えば、AEMサービスのEphemeralディスクへ `asset.getOriginal().getStream()`のバイナリのダウンロードをトリガーするバイナリを使用しないでください。

## 逆複製エージェントなし {#no-reverse-replication-agents}

「発行」から「作成者」への逆複製は、AEMでクラウドサービスとしてサポートされていません。 このような方法が必要な場合は、発行インスタンスのファームと、場合によっては作成者クラスターで共有される外部の永続化ストアを使用できます。

## 転送レプリケーションエージェントの移植が必要 {#forward-replication-agents}

コンテンツは、pub-subメカニズムを使用して作成者から発行に複製されます。 カスタムレプリケーションエージェントはサポートされていません。

## 監視とデバッグ {#monitoring-and-debugging}

### ログ {#logs}

ローカル開発の場合、ログエントリはローカルファイルに書き込まれます。 をフォルダーに追 `/crx-quickstart/logs` 加します。

クラウド環境では、開発者は Cloud Manager を使用してログをダウンロードするか、コマンドラインツールを使用してログを追跡することができます。<!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**ログレベルの設定**

クラウド環境のログレベルを変更するには、Sling Logging OSGi 設定を変更した後、完全に再デプロイする必要があります。これは即座にはおこなわれないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にする場合は注意が必要です。今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
>以下に示す設定の変更を実行するには、ローカルの開発環境で設定の変更を作成し、それらをクラウドサービスインスタンスとしてAEMにプッシュする必要があります。 この方法について詳しくは、「クラウドサービスとしてのAEM [へのデプロイ」を参照してください](/help/implementing/deploying/overview.md)。

**デバッグログレベルのアクティベート**

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

### スレッドダンプ {#thread-dumps}

クラウド環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。しばらくの間は、問題のデバッグ用にスレッドダンプが必要な場合は、AEM サポートに連絡して、正確な時間枠を指定してください。

## CRXDE Lite とシステムコンソール {#crxde-lite-and-system-console}

### ローカル開発 {#local-development}

ローカル開発の場合、開発者は CRXDE Lite（`/crx/de`）と AEM Web コンソール（`/system/console`）に完全にアクセスできます。

（クラウド対応クイックスタートを使用する）ローカル開発では、`/apps` と `/libs` に直接書き込むことができます。この点が、最上位フォルダーが不変なクラウド環境とは異なります。

### AEM as a Cloud Service の開発ツール {#aem-as-a-cloud-service-development-tools}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージ環境や実稼動環境ではアクセスできません。不変リポジトリ（`/libs`、`/apps`）に実行時に書き込むことはできないので、書き込もうとするとエラーが発生します。

AEM as a Cloud Service 開発者環境でデバッグするためのツールセットが開発環境、ステージ環境、実稼動環境の開発者コンソールで利用できます。URLは、次のようにAuthorサービスURLまたはPublishサービスURLを調整することで判別できます。

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

### AEM のステージング環境および実稼動環境用サービス {#aem-staging-and-production-service}

ユーザーは、ステージング環境と実稼動環境用の開発者ツールにはアクセスできません。

### パフォーマンスの監視 {#performance-monitoring}

アドビはアプリケーションのパフォーマンスを監視し、劣化が観察された場合に対処します。 現時点では、アプリの指標を確認できません。