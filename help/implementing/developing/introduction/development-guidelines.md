---
title: AEM as a Cloud Service Development Guidelines
description: '完了予定 '
translation-type: tm+mt
source-git-commit: 13c0a670330532f574c2b38823b8a924c609e8e4

---


# AEM as a Cloud Service Development Guidelines {#aem-as-a-cloud-service-development-guidelines}

## バックグラウンドタスクと長時間実行中のジョブ {#background-tasks-and-long-running-jobs}

バックグラウンドタスクとして実行するコードは、実行中のインスタンスをいつでもダウンできると想定する必要があります。 したがって、コードは回復力があり、最も多くのインポートを再開できる必要があります。 つまり、コードが再実行された場合は、最初から始めるのではなく、コードの実行が中止された場所から近い位置から始める必要があります。 この種のコードには新しい要件はありませんが、AEMのクラウドサービスでは、インスタンスの停止が発生する可能性が高くなります。

トラブルを最小限に抑えるために、長時間実行するジョブは可能な限り避け、少なくとも再開可能な状態にする必要があります。 このようなジョブを実行するには、少なくとも1回の保証を持つSlingジョブを使用します。したがって、ジョブが中断された場合は、できるだけ早く再実行されます。 でも最初からやり直すべきではないでしょう このようなジョブをスケジュールする場合は、 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) （スケジューラー）を再び少なくとも1回は実行するのに使用することをお勧めします。

実行を保証できないので、Sling Commons Schedulerはスケジュールに使用しないでください。 それは予定される可能性が高い。

同様に、監視イベントに対する動作（JCRイベントやSlingリソースイベント）など、非同期的に起こっているすべての動作では、必ずしも実行が保証されず、注意して使用する必要があります。 これは、現在のAEMデプロイメントでは既に同じです。

## 送信HTTP接続 {#outgoing-http-connections}

送信HTTP接続では、適切な接続と読み取りのタイムアウトを設定することを強くお勧めします。 これらのタイムアウトを適用しないコードの場合、AEM上でクラウドサービスとして実行されるAEMインスタンスは、グローバルタイムアウトを強制します。 これらのタイムアウト値は、接続呼び出しの場合は10秒、一般的な次のJavaライブラリで使用される接続の場合は60秒です。

HTTP接続を行う場合は、提供されている [Apache httpComponents Client 4.xライブラリを使用する](https://hc.apache.org/httpcomponents-client-ga/) ことをお勧めします。

動作は知られているが、依存関係を自分で提供する必要がある可能性のある代替手段は、次のとおりです。

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) /java.net.URLConnection [](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （AEMによって提供）
* [Apache Commons httpClient 3.x](https://hc.apache.org/httpclient-3.x/) （古くなり、バージョン4.xに置き換えられているので、推奨されません）
* [OK Http](OK Http（AEMでは提供されません）（AEMでは提供されません）

## 監視とデバッグ {#monitoring-and-debugging}

### ログ {#logs}

* ローカル開発の場合、ログエントリはローカルファイルに書き込まれます
   * `./crx-quickstart/logs`
* Cloud環境では、開発者はCloud Managerを使用してログをダウンロードするか、コマンドラインツールを使用してログの末尾に表示することができます。 <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Cloud環境のログレベルを変更するには、Sling Logging OSGIの設定を変更し、その後完全な再デプロイを行う必要があります。 これは即座に行われないので、大量のトラフィックを受け取る実稼働環境で詳細なログを有効にする場合は注意が必要です。 今後、ログレベルをより迅速に変更するメカニズムが存在する可能性があります。

### Thread Dumps {#thread-dumps}

Cloud環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。 その間、問題のデバッグにスレッドダンプが必要な場合は、AEMサポートに連絡し、正確な時間枠を指定してください。

### CRX/DE Liteとシステムコンソール {#crxde-lite-and-system-console}

## 地域開発 {#local-development}

ローカル開発の場合、開発者はCRXDE Lite (`/crx/de`)とAEM Web Console (`/system/console`)に完全にアクセスできます。

ローカル開発（クラウド対応クイックスタートを使用）では、直接書き込むことができます `/apps``/libs` 。これは、最上位フォルダーが不変のCloud環境とは異なります。

## クラウドサービス開発ツールとしてのAEM {#aem-as-a-cloud-service-development-tools}

お客様は開発環境でCRXDE Liteにアクセスできますが、ステージや実稼働環境にはアクセスできません。 不変リポジトリ(`/libs`, `/apps`)を実行時に書き込むことはできません。書き込もうとするとエラーが発生します。

AEMをクラウドサービス開発者環境としてデバッグするためのツールのセットは、開発、ステージ、実稼働環境について、デベロッパーコンソールで利用できます。 URLは、次のように作成者URLまたは発行サービスURLを調整することで決定できます。

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

ショートカットとして、以下に示す環境パラメーターに基づいて、Cloud Manager CLIの次のコマンドを使用して、デベロッパーコンソールを起動できます。

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

See [this page](/help/release-notes/home.md) for more information.

開発者は、ステータス情報を生成し、様々なリソースを解決できます。

以下の図に示すように、使用可能なステータス情報には、バンドルの状態、コンポーネント、OSGI設定、oakインデックス、OSGIサービス、Slingジョブが含まれます。

![開発コンソール1](/help/implementing/developing/introduction/assets/devconsole1.png)

次の図に示すように、開発者はパッケージの依存関係とサーブレットを解決できます。

![開発コンソール2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開発コンソール3](/help/implementing/developing/introduction/assets/devconsole3.png)

また、デバッグにも便利です。開発者コンソールには、次のExplain queryツールへのリンクがあります。

![開発コンソール4](/help/implementing/developing/introduction/assets/devconsole4.png)

**AEMステージングと実稼働サービス**

ステージング環境と実稼働環境用の開発者ツールにはアクセスできません。

### 診断 {#diagnostics}

開発環境では、システムコンソールを使用できます。 ただし、ステージングおよび実稼働用の診断ダンプは使用できません。