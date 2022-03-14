---
title: AEM as a Cloud Service の開発ガイドライン
description: AEM as a Cloud Service の開発ガイドライン
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 925f451b11e599691ad7dcec27c88913ca6efcdd
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 89%

---

# AEM as a Cloud Service の開発ガイドライン {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service の開発ガイドライン"
>abstract="このタブでは、AEM as a Cloud Serviceでのコーディングに関して推奨されるベストプラクティスを確認できます。 コーディングは、AMS やオンプレミスデプロイメントとは大きく異なる場合があります。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="パッケージ構造のデモ"

AEM as a Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。つまり、常に複数のインスタンスが実行されています。インスタンスはいつ停止するかわからないので、コードには特に回復力が必要です。

AEM as a Cloud Service を更新する間、古いコードと新しいコードが並行して実行されるインスタンスが存在します。したがって、新しいコードで作成されたコンテンツが古いコードによって中断されず、新しいコードが古いコンテンツを処理できる必要があります。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

クラスター内のプライマリを識別する必要がある場合は、Apache Sling Discovery API を使用して検出できます。

## メモリ内の状態 {#state-in-memory}

状態はメモリ内ではなく、リポジトリー内に保持する必要があります。そうしないと、インスタンスが停止した場合に、状態が失われる可能性があります。

## ファイルシステムの状態 {#state-on-the-filesystem}

インスタンスのファイルシステムは、AEM as a Cloud Service で使用しないでください。ディスクは揮発性で、インスタンスが再利用されると破棄されます。単一の要求の処理に関する一時的なストレージのために、ファイルシステムの使用を制限することは可能ですが、大量のファイルに対して濫用しないでください。リソースの使用割り当てに悪影響を与え、ディスクの制限が生じる可能性があるためです。

ファイルシステムの使用がサポートされていない例として、パブリッシュ層では、永続化する必要のあるデータが、長期ストレージのために外部サービスに送り出されることを確認する必要があります。

## 監視 {#observation}

同様に、観察イベントに作用するように非同期的に起こっているものすべてに対して、ローカルで実行することを保証できないことから、注意深く使用する必要があります。これは、JCR リソースと Sling イベントの両方に当てはまります。変更が発生した時点で、インスタンスが停止し、別のインスタンスに置き換えられる場合があります。その時点でアクティブなトポロジ内の他のインスタンスは、このイベントに反応できます。しかし、この場合、ローカルのイベントではなく、イベントの発行時にアクティブなリーダーがいない可能性もあります。

## バックグラウンドタスクと長時間実行ジョブ {#background-tasks-and-long-running-jobs}

バックグラウンドタスクとして実行するコードでは、コードを実行しているインスタンスが突然機能しなくなる可能性があることを前提にする必要があります。したがって、コードは回復力が高く、最も重要な点として再開可能である必要があります。 つまり、コードが再実行された場合は、再び最初から始めるのではなく、実行が中断された箇所に近い位置から始める必要があります。これはこの種のコードにとって新しい要件ではありませんが、AEM as a Cloud Service では、インスタンスの停止が起こる可能性が高くなります。

トラブルを最小限に抑えるために、長時間実行ジョブは可能な限り避け、少なくとも再開可能な状態になっている必要があります。このようなジョブを実行するには、少なくとも 1 回は実行されることが保証されている Sling ジョブを使用します。したがって、ジョブが中断された場合、ジョブはできるだけ早く再実行されます。ただし、最初からやり直すべきではないでしょう。このようなジョブをスケジュールする場合は、 [Sling ジョブ](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) スケジューラーを再度使用すると、少なくとも 1 回は実行されるようになります。

Sling Commons Scheduler は実行を保証できないので、スケジュール設定には使用しないでください（スケジュール設定される可能性のほうが高いというだけで、保証されるものではありません）。

同様に、監視イベント（例：JCR イベントや Sling リソースイベント）に対する動作など、非同期的に発生するあらゆる動作は、必ずしも実行が保証されないので、慎重に使用する必要があります。これは、現在の AEM デプロイメントに既に当てはまります。

## 送信 HTTP 接続 {#outgoing-http-connections}

送信 HTTP 接続では、接続および読み取りの妥当なタイムアウトを設定することを強くお勧めします。これらのタイムアウトを適用しないコードの場合、AEM as a Cloud Service 上で動作している AEM インスタンスは、グローバルタイムアウトを強制的に適用します。一般的な次の Java ライブラリで使用される接続の場合、これらのタイムアウト値は、接続呼び出しについては 10 秒、読み取り呼び出しについては 60 秒です。

HTTP 接続を行う場合は、提供されている [Apache HttpComponents Client 4.x ライブラリ](https://hc.apache.org/httpcomponents-client-ga/)を使用することをお勧めします。

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

ローカル開発の場合、ログエントリは `/crx-quickstart/logs` フォルダーのローカルファイルに書き込まれます。

クラウド環境では、開発者は Cloud Manager を使用してログをダウンロードするか、コマンドラインツールを使用してログを追跡することができます。<!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**ログレベルの設定**

クラウド環境のログレベルを変更するには、Sling Logging OSGi 設定を変更した後、完全に再デプロイする必要があります。これは即座には行われないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にする場合は注意が必要です。今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
>以下に示す設定の変更を実行するには、ローカルの開発環境で設定の変更を作成し、それらを AEM as a Cloud Service インスタンスにプッシュする必要があります。この方法について詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。

**デバッグログレベルのアクティベート**

デフォルトのログレベルは情報（INFO）なので、デバッグ（DEBUG）メッセージはログに記録されません。DEBUG ログレベルをアクティブにするには、次のプロパティを debug モードに更新します。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例えば、 `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` を次の値に設定します。

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

DEBUG ログレベルのログを必要以上に長く残さないでください。この場合、多数のエントリが生成されます。

常に次の場所にログを記録するのが望ましい場合は、実行モードベースの OSGi 設定ターゲティングを使用して、異なるAEM環境に個別のログレベルを設定できます。 `DEBUG` 開発中に 次に例を示します。

|環境 |実行モード別の OSGi 設定の場所 | `org.apache.sling.commons.log.level` プロパティ値 | | - | - | - | |開発 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEBUG | |ステージ | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | WARN | |実稼動 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config～example.cfg.json | ERROR |

デバッグファイルの行は、通常は DEBUG で始まり、その後にログレベル、インストーラーのアクション、ログメッセージが示されます。次に例を示します。

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 重大なエラー | アクションが失敗し、インストーラーの処理を続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。インストールは続行しますが、CRX の一部が正常にインストールされなかったので、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。CRX が正常に機能するかどうかは不明です。 |
| 3 | 情報 | アクションが成功しました。 |

### スレッドダンプ {#thread-dumps}

クラウド環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。しばらくの間は、問題のデバッグ用にスレッドダンプが必要な場合は、AEM サポートに連絡して、正確な時間枠を指定してください。

## CRXDE Lite とデベロッパーコンソール {#crxde-lite-and-developer-console}

### ローカル開発 {#local-development}

ローカル開発の場合、開発者は CRXDE Lite（`/crx/de`）と AEM Web コンソール（`/system/console`）に完全にアクセスできます。

（SDK を使用する）ローカル開発では、`/apps` と `/libs` に直接書き込むことができます。この点が、最上位フォルダーが不変なクラウド環境とは異なります。

### AEM as a Cloud Service の開発ツール {#aem-as-a-cloud-service-development-tools}

ユーザーはオーサー層の開発環境では CRXDE Lite にアクセスできますが、ステージ環境や実稼動環境ではアクセスできません。不変リポジトリー（`/libs`、`/apps`）に実行時に書き込むことはできないので、書き込もうとするとエラーが発生します。

代わりに、開発者コンソールからリポジトリブラウザーを起動して、オーサー層、パブリッシュ層、プレビュー層のすべての環境のリポジトリに対する読み取り専用ビューを提供できます。 リポジトリブラウザの詳細を表示 [ここ](/help/implementing/developing/tools/repository-browser.md).

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

実稼動プログラムの場合、開発者コンソールへのアクセスは Admin Console の「Cloud Manager - デベロッパーロール」で定義されます。一方、サンドボックスプログラムの場合、開発者コンソールは、AEM as a Cloud Service へのアクセスを可能にする製品プロファイルを持つすべてのユーザーが使用できます。すべてのプログラムで、ステータスダンプに「Cloud Manager - Developer Role」が必要で、両方のサービスのデータを表示するには、オーサーサービスとパブリッシュサービスのAEM Users またはAEM Administrators Product Profile でもユーザーを定義する必要があります。 ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja)を参照してください。

### パフォーマンスの監視 {#performance-monitoring}

アドビはアプリケーションのパフォーマンスを監視し、劣化が観察された場合に対処します。現時点では、アプリケーションの指標を確認できません。

## 電子メールの送信 {#sending-email}

以下の節では、電子メールのリクエスト、設定、送信の方法について説明します。

>[!NOTE]
>
>メールサービスは、OAuth2 サポートを使用して設定できます。詳しくは、[メールサービスの OAuth2 サポート](/help/security/oauth2-support-for-mail-service.md)を参照してください。

### 送信電子メールの有効化 {#enabling-outbound-email}

電子メールの送信に使用されるポートは、デフォルトでは無効になっています。ポートをアクティブにするには、[高度なネットワーク機能](/help/security/configuring-advanced-networking.md)を設定して、必要な環境ごとに `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` エンドポイントのポート転送ルールを必ず設定します。これは、対象となるポート（465 や 587 など）をプロキシポートにマッピングします。

`kind` パラメータを `flexiblePortEgress` に設定して高度なネットワーク機能を設定することをお勧めします。アドビがフレキシブルポートエグレストラフィックのパフォーマンスを最適化できるからです。一意のエグレス IP アドレスが必要な場合は、`kind` パラメーターを `dedicatedEgressIp` に設定します。他の理由で既に VPN を設定してある場合は、その高度なネットワークバリエーションから提供される一意の IP アドレスも使用できます。

電子メールクライアントに直接送信するのではなく、メールサーバーを通じて電子メールを送信する必要があります。そうしないと、電子メールがブロックされる可能性があります。

### 電子メールの送信 {#sending-emails}

[Day CQ Mail Service OSGi サービス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=ja#configuring-the-mail-service)を使用してください。また、受信者に直接送信するのではなく、サポートリクエストに明示されたメールサーバーに電子メールを送信する必要があります。

### 設定 {#email-configuration}

AEM 内の電子メールは、[Day CQ Mail Service OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) サービスを使用して送信する必要があります。

電子メールの設定について詳しくは、[AEM 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=ja)を参照してください。AEM as a Cloud Service の場合は、`com.day.cq.mailer.DefaultMailService OSGI` サービスへの次のような調整が必要になります。

* SMTP サーバーのホスト名は$に設定する必要があります[env:AEM_PROXY_HOST;default=proxy.tunnel]
* SMTP サーバーポートは、高度なネットワーク機能を設定する際に、API 呼び出しで使用される portForwards パラメーターに設定された元のプロキシポートの値に設定してください。例えば、（465 ではなく）30465 などとします。

また、ポート 465 がリクエストされた場合は、次のことをお勧めします。

* `smtp.port` を `465` に設定
* `smtp.ssl` を `true` に設定

さらに、ポート 587 がリクエストされた場合は、

* `smtp.port` を `587` に設定
* `smtp.ssl` を `false` に設定

`smtp.starttls` プロパティは、実行時に AEM as a Cloud Service によって適切な値に自動的に設定されます。したがって、`smtp.ssl` が true に設定されている場合、`smtp.startls` は無視されます。`smtp.ssl` が false に設定されている場合、`smtp.starttls` は true に設定されます。これは、OSGI 構成で設定されている `smtp.starttls` 値には関係ありません。


オプションで、メールサービスに OAuth2 サポートを設定できます。詳しくは、[メールサービスの OAuth2 サポート](/help/security/oauth2-support-for-mail-service.md)を参照してください。

### 従来の電子メール設定 {#legacy-email-configuration}

2021.9.0 リリースより前は、カスタマーサポートへの依頼を通じて電子メールが設定されていました。`com.day.cq.mailer.DefaultMailService OSGI` サービスへの次のような調整が必要になります。

AEM as a Cloud Service では、ポート 465 を通じてメールを送信する必要があります。TLS オプションが有効になっている限り、メールサーバーがポート 465 をサポートしていない場合は、ポート 587 を使用できます。

ポート 465 がリクエストされた場合：

* `smtp.port` を `465` に設定
* `smtp.ssl` を `true` に設定

さらに、ポート 587 がリクエストされた場合は、

* `smtp.port` を `587` に設定
* `smtp.ssl` を `false` に設定

`smtp.starttls` プロパティは、実行時に AEM as a Cloud Service によって適切な値に自動的に設定されます。したがって、`smtp.ssl` が true に設定されている場合、`smtp.startls` は無視されます。`smtp.ssl` が false に設定されている場合、`smtp.starttls` は true に設定されます。これは、OSGI 構成で設定されている `smtp.starttls` 値には関係ありません。

SMTP サーバーホストは、メールサーバーのホストに設定してください。


## [!DNL Assets] 開発のガイドラインとユースケース {#use-cases-assets}

AEM Assets as a Cloud Service の開発のユースケース、推奨事項、参考資料については、[Assets の開発者向けリファレンス](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)を参照してください。
