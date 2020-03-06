---
title: AEM as a Cloud Service の開発ガイドライン
description: '完了予定 '
translation-type: tm+mt
source-git-commit: 9777dd5772ab443b5b3dabbc74ed0d362e52df60

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

インスタンスのファイルシステムは、AEMでクラウドサービスとして使用しないでください。 ディスクは一時的で、インスタンスが再利用されると破棄されます。 単一の要求を処理する際に、一時的にファイルシステムを使用することは限られていますが、大量のファイルに対しては悪用しないでください。 これは、リソースの使用割り当てに悪影響を与え、ディスクの制限が生じる可能性があるためです。

ファイルシステムの使用がサポートされていない場合は、発行層で、永続化する必要のあるデータを外部サービスに確実に送り出し、長期保存する必要があります。

## 監視 {#observation}

同様に、観察イベントに作用するように非同期的に起こっているものすべてについては、ローカルで実行することを保証できず、注意して使用する必要があります。 これは、JCRイベントとSlingリソースイベントの両方に当てはまります。 変更が発生した時点で、インスタンスがダウンされ、別のインスタンスに置き換えられる場合があります。 その時点でアクティブなトポロジ内の他のインスタンスは、そのイベントに対して反応できます。 しかし、この場合は地元のイベントではなく、引き続きリーダー選挙が行われた場合には、引き続きリーダーがいない可能性もあります。

## バックグラウンドタスクと長時間実行中のジョブ {#background-tasks-and-long-running-jobs}

バックグラウンドタスクとして実行されるコードは、実行中のインスタンスをいつでもダウンできると想定する必要があります。 したがって、コードは回復力があり、最も多くのインポートを再開できる必要があります。 つまり、コードが再実行された場合は、最初から始めるのではなく、コードが終了した場所から近い位置から始める必要があります。 この種のコードに対する新しい要件ではありませんが、AEMのクラウドサービスでは、インスタンスの停止が発生する可能性が高くなります。

トラブルを最小限に抑えるために、長時間実行するジョブは可能な限り避ける必要があり、少なくとも再開できる必要があります。 このようなジョブを実行するには、少なくとも1回の保証を持つSlingジョブを使用します。したがって、ジョブが中断された場合は、できるだけ早く再実行されます。 でも最初からやり直すべきではない。 このようなジョブをスケジュールする場合は、 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) （スリングジョブ）スケジューラを再度、少なくとも1回は実行するのに最適です。

Sling Commons Schedulerは、実行を保証できないので、スケジュールに使用しないでください。 それは予定される可能性が高い。

同様に、監視イベント（JCRイベントやSlingリソースイベント）に基づくなど、非同期的な処理が行われている場合は、実行が保証されないので注意して使用する必要があります。 これは、現在のAEMデプロイメントでは既に同じです。

## 送信HTTP接続 {#outgoing-http-connections}

発信HTTP接続では、適切な接続と読み取りのタイムアウトを設定することを強くお勧めします。 これらのタイムアウトを適用しないコードの場合、AEM上でクラウドサービスとして実行されるAEMインスタンスは、グローバルタイムアウトを強制します。 これらのタイムアウト値は、接続呼び出しの場合は10秒、次の一般的なJavaライブラリで使用される接続の場合は60秒です。

HTTP接続を行う場合は、提供されている [Apache HttpComponents Client 4.xライブラリを使用する](https://hc.apache.org/httpcomponents-client-ga/) ことをお勧めします。

動作はわかっているが、依存関係を自分で提供する必要がある可能性のある代替手段は、次のとおりです。

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) / [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （AEMによって提供）
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （古くなり、バージョン4.xに置き換えられているので推奨されません）
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

* ローカル開発の場合、ログエントリはローカルファイルに書き込まれます
   * `./crx-quickstart/logs`
* Cloud環境では、開発者はCloud Managerを使用してログをダウンロードするか、コマンドラインツールを使用してログの末尾に配置することができます。 <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Cloud環境のログレベルを変更するには、Sling Logging OSGIの設定を変更し、その後完全な再デプロイを行う必要があります。 これは即座に行われるわけではないので、大量のトラフィックを受け取る実稼働環境で詳細なログを有効にする場合は注意が必要です。 今後、ログレベルをより迅速に変更するメカニズムが生じる可能性があります。

### Thread Dumps {#thread-dumps}

Cloud環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。 その間、問題のデバッグにスレッドダンプが必要な場合は、正確な時間枠を指定して、AEMサポートにお問い合わせください。

## CRX/DE Liteとシステムコンソール {#crxde-lite-and-system-console}

### 地域開発 {#local-development}

ローカル開発の場合、開発者はCRXDE Lite(`/crx/de`)とAEM Web Console(`/system/console`)に完全にアクセスできます。

ローカル開発（クラウド対応クイックスタートを使用）では、直接書き込むことができます。 `/apps``/libs` これは、これらの最上位フォルダーが不変のCloud環境とは異なります。

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

お客様は、ステージや実稼働環境ではなく、開発環境でCRXDE Liteにアクセスできます。 不変リポジトリ(`/libs`、 `/apps`)は実行時に書き込むことができず、書き込もうとするとエラーが発生します。

AEMをクラウドサービス開発環境としてデバッグするためのツールのセットは、開発、ステージ、実稼働環境に関して、デベロッパーコンソールで利用できます。 URLは、次のようにAuthorサービスURLまたはPublishサービスURLを調整することで判別できます。

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

ショートカットとして、次のCloud Manager CLIコマンドを使用して、以下に説明する環境パラメーターに基づいて開発者コンソールを起動できます。

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

See [this page](/help/release-notes/home.md) for more information.

開発者は、ステータス情報を生成し、様々なリソースを解決できます。

以下の図に示すように、使用可能なステータス情報には、バンドル、コンポーネント、OSGI設定、oakインデックス、OSGIサービス、Slingジョブの状態が含まれます。

![開発コンソール1](/help/implementing/developing/introduction/assets/devconsole1.png)

次の図に示すように、開発者はパッケージの依存関係とサーブレットを解決できます。

![開発コンソール2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開発コンソール3](/help/implementing/developing/introduction/assets/devconsole3.png)

また、デバッグに役立つ開発者コンソールには、次のExplain Queryツールへのリンクがあります。

![開発コンソール4](/help/implementing/developing/introduction/assets/devconsole4.png)

### AEMのステージングと実稼働サービス {#aem-staging-and-production-service}

お客様は、ステージング環境と実稼働環境用の開発者ツールにアクセスできません。

### パフォーマンスの監視 {#performance-monitoring}

アドビはアプリケーションのパフォーマンスを監視し、劣化が観察された場合に対処します。 現時点では、アプリの指標を確認できません。