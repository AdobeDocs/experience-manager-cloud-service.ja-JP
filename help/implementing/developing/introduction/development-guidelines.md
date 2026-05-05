---
title: AEM as a Cloud Service の開発ガイドライン
description: AEM as a Cloud Service での開発に関するガイドラインと、オンプレミスでの AEM および AMS での AEM との重要な違いについて説明します。
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
feature: Developing
role: Admin, Developer
source-git-commit: 925ed3687b17108b8d42a4a25d1f2b87edaaf76f
workflow-type: tm+mt
source-wordcount: '2890'
ht-degree: 69%

---


# AEM as a Cloud Service の開発ガイドライン {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service の開発ガイドライン"
>abstract="AEM as a Cloud Service での開発に関するガイドラインと、オンプレミスでの AEM および AMS での AEM との重要な違いについて説明します。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="パッケージ構造のデモ"

このドキュメントでは、AEM as a Cloud Service での開発に関するガイドラインと、オンプレミスおよび AMS の AEM とは異なる重要な方法について説明します。

## コードはクラスター対応である必要があります {#cluster-aware}

AEM as a Cloud Service で実行するコードは、常にクラスター内で実行されていることを認識している必要があります。 つまり、常に複数のインスタンスが実行されています。 インスタンスがいつでも停止する可能性があるため、コードは回復力を持つ必要があります。

AEM as a Cloud Service を更新する間、古いコードと新しいコードが並行して実行されるインスタンスが存在します。 したがって、古いコードが新しいコードによって作成されたコンテンツで壊れてはならず、新しいコードが古いコンテンツを処理できるようにする必要があります。

クラスター内のプライマリを識別する必要がある場合は、Apache Sling Discovery APIを使用して検出できます。

## メモリ内の状態 {#state-in-memory}

状態はメモリ内ではなく、リポジトリー内に保持する必要があります。 そうしないと、インスタンスが停止した場合に、状態が失われる可能性があります。

## ファイルシステムの状態 {#state-on-the-filesystem}

AEM as a Cloud Service でインスタンスのファイルシステムを使用しないでください。 ディスクは一時的なもので、インスタンスがリサイクルされると破棄されます。 単一の要求の処理に関する一時的なストレージのために、ファイルシステムの使用を制限することは可能ですが、大量のファイルに対して濫用しないでください。 リソースの使用割り当てに悪影響を与え、ディスクの制限が生じる可能性があるためです。

ファイルシステムの使用がサポートされていない場合の例として、パブリッシュ層では、永続化する必要があるデータが外部サービスに送信され、長期的に保存されるようにする必要があります。

## 監視 {#observation}

同様に、観察イベントに作用するように、非同期に起こっているすべてのものでは、ローカルで実行されることを保証できないので、慎重に使用する必要があります。 これは、JCR リソースと Sling イベントの両方に当てはまります。 変更が発生した時点で、インスタンスは削除され、別のインスタンスに置き換えられます。 その時点でアクティブなトポロジ内の他のインスタンスは、このイベントに反応できます。 ただし、この場合、これはローカルのイベントではなく、イベントが発行されたときに進行中のリーダー選挙の場合には、アクティブなリーダーがいない可能性があります。

## バックグラウンドタスクと長時間実行ジョブ {#background-tasks-and-long-running-jobs}

バックグラウンドタスクとして実行されるコードは、実行中のインスタンスがいつでもダウンできるものと仮定する必要があります。 したがって、コードは回復力があり、最も重要なのは再利用可能である必要があります。 つまり、コードが再実行された場合、最初から再び開始するのではなく、中断した場所に近い状態で開始する必要があります。 これは、この種のコードに対する新しい要件ではありませんが、AEM as a Cloud Serviceでは、インスタンスのテイクダウンが発生する可能性が高くなります。

トラブルを最小限に抑えるためには、可能であれば長時間稼働する作業を避け、少なくとも再開する必要があります。 このようなジョブを実行するには、少なくとも 1 回は実行されることが保証されている Sling ジョブを使用します。したがって、ジョブが中断された場合、ジョブはできるだけ早く再実行されます。 ただし、最初からやり直すべきではないでしょう。 このようなジョブをスケジュールする場合は、 [Sling ジョブ](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) スケジューラーを使用することをお勧めします。やはり、少なくとも 1 回は実行されることが保証されているからです。

実行は保証できないため、Sling Commons Schedulerをスケジュールに使用しないでください。 スケジュール設定されている可能性が高いです。

同様に、観測イベント（JCR イベントまたはSling リソースイベント）に対してアクションを実行するなど、非同期に発生するあらゆるイベントでは、実行が保証されないため、慎重に使用する必要があります。 これは、現在の AEM デプロイメントに既に当てはまります。

## 送信 HTTP 接続 {#outgoing-http-connections}

送信HTTP接続では、接続と読み取りのタイムアウトを合理的に設定することを強くお勧めします。推奨される値は、接続タイムアウトで1秒、読み取りタイムアウトで5秒です。 正確な数値は、これらのリクエストを処理するバックエンドシステムのパフォーマンスに基づいて決定する必要があります。

これらのタイムアウトを適用しないコードの場合、AEM as a Cloud Service上で動作するAEM インスタンスは、グローバルタイムアウトを適用します。 接続の場合、これらのタイムアウト値は、接続呼び出しについては 10 秒、読み取り呼び出しについては 60 秒です。

HTTP 接続を行う場合は、提供されている [Apache HttpComponents Client 4.x ライブラリ](https://hc.apache.org/httpcomponents-client-ga/)を使用することをお勧めします。

次の代替手段は、動作することはわかっていますが、依存関係を自分で指定しなければならない可能性があります。

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) と [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html)（AEM で提供）のいずれか一方または両方
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/)（古くなり、バージョン 4.x に代わっているので、お勧めしません）
* [OK Http](https://square.github.io/okhttp/)（AEM では提供されません）

タイムアウトの指定の次に、そのようなタイムアウトと予期しない HTTP ステータスコードの適切な処理も実装する必要があります。

## リクエストレート制限の処理 {#rate-limit-handling}

AEM への受信リクエストのレートが正常なレベルを超えると、AEM は HTTP エラーコード 429 を使用して新しい要求に応答します。 AEM に対してプログラムによる呼び出しを行うアプリケーションでは、コーディングを慎重に検討し、指数バックオフ戦略を使用して、数秒後に再試行することができます。 2023年8月中旬以前は、AEM は HTTP エラーコード 503 で同じ条件に応答していました。

## クラシック UI のカスタマイズがない {#no-classic-ui-customizations}

AEM as a Cloud Service は、サードパーティの顧客コードのタッチ UI のみをサポートします。 クラシック UI はカスタマイズには使用できません。

## ネイティブバイナリまたはネイティブライブラリがありません {#avoid-native-binaries}

ネイティブバイナリおよびライブラリを、クラウド環境にデプロイしたり、インストールしたりしないでください。

さらに、コードは、実行時にネイティブバイナリまたはネイティブ Java拡張機能（JNIなど）をダウンロードしようとしないでください。

## AEM as a Cloud Service を使用したストリーミングバイナリがない {#no-streaming-binaries}

バイナリは CDN を通じてアクセスし、コア AEM サービスの外部でバイナリを提供します。

例えば、AEM サービスの揮発性ディスクへのバイナリのダウンロードをトリガーする `asset.getOriginal().getStream()` を使用しないでください。

## リバースレプリケーションエージェントがない {#no-reverse-replication-agents}

パブリッシュからオーサーへのリバースレプリケーションは、AEM as a Cloud Service ではサポートされていません。 このような方法が必要な場合は、パブリッシュインスタンスのファームと、場合によってはオーサークラスターで共有される外部の永続化ストアを使用できます。

## 転送レプリケーションエージェントの移植が必要 {#forward-replication-agents}

コンテンツは、pub-sub メカニズムを使用してオーサーからパブリッシュにレプリケートされます。 カスタムレプリケーションエージェントはサポートされていません。

## 開発環境の過負荷防止 {#overloading-dev-envs}

本番環境のサイズが拡大され、安定した動作が保証される一方で、ステージング環境は本番環境同様のサイズとなり、本番条件下での現実的なテストを行えます。

開発環境と高速開発環境は、開発、エラー分析、および機能テストに限定する必要があり、高いワークロードや大量のコンテンツを処理するように設計されていません。

例えば、開発環境上の大規模なコンテンツリポジトリーでインデックス定義を変更すると、インデックスを再作成して処理が過剰になる可能性があります。 充実したコンテンツを必要とするテストは、ステージング環境で実施する必要があります。

## 監視とデバッグ {#monitoring-and-debugging}

### ログ {#logs}

ローカル開発の場合、ログ エントリは`/crx-quickstart/logs` フォルダー内のローカル ファイルに書き込まれます。

Cloud環境では、開発者はCloud Managerを通じてログをダウンロードするか、コマンドラインツールを使用してログをテールできます。<!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Custom logs are not supported and so all logs should be output to the error log. -->

**ログレベルの設定**

クラウド環境のログレベルを変更するには、Sling Logging OSGi設定を変更し、その後に完全に再デプロイメントする必要があります。 これは瞬時に行われるものではないので、大量のトラフィックを受け取る実稼動環境で詳細なログを有効にすることに注意してください。 今後、ログレベルをより迅速に変更するメカニズムが提供される可能性があります。

>[!NOTE]
>
>以下に示す設定の変更を実行するには、ローカル開発環境で設定変更を作成し、それらを AEM as a Cloud Service インスタンスにプッシュします。 この方法について詳しくは、[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。

**デバッグログレベルのアクティベート**

デフォルトのログレベルは情報（INFO）なので、デバッグ（DEBUG）メッセージはログに記録されません。 DEBUG ログレベルをアクティブにするには、次のプロパティをデバッグモードに更新します。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例えば、`/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` に次の値を設定します。

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

この結果、多くのエントリが生成されるので、ログを不必要に長くデバッグログレベルのままにしないでください。

開発時に常に `DEBUG` レベルでログを記録するのが望ましい場合は、実行モードベースの OSGi 設定ターゲティングを使用して、AEM 環境ごとに個別にログレベルを設定できます。 例：

| 環境 | 実行モード別の OSGi 設定の場所 | `org.apache.sling.commons.log.level` プロパティ値 |
| - | - | - |
| 開発 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | DEBUG |
| ステージ | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | WARN |
| 実稼動 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | ERROR |

デバッグファイル内の行は通常DEBUGで始まり、ログレベル、インストーラーアクション、ログメッセージを提供します。 例：

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 重大なエラー | アクションが失敗し、インストーラーの処理を続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。 インストールは続行しますが、CRX の一部が正常にインストールされなかったので、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。 CRX は正常に機能する場合と機能しない場合があります。 |
| 3 | 情報 | アクションが成功しました。 |

### スレッドダンプ {#thread-dumps}

クラウド環境のスレッドダンプは継続的に収集されますが、現時点ではセルフサービス方式でダウンロードすることはできません。 また、問題のデバッグにスレッドダンプが必要な場合は、正確な時間ウィンドウを指定して、AEM サポートにお問い合わせください。

## CRX/DE Lite と AEM as a Cloud Service Developer Console {#crxde-lite-and-developer-console}

### ローカル開発 {#local-development}

ローカル開発のために、開発者は[CRXDE Lite](/help/implementing/developing/tools/crxde.md) （`/crx/de`）および[Web コンソール &#x200B;](/help/implementing/developing/tools/web-console.md) （`/system/console`）に完全にアクセスできます。

（SDKを使用して）ローカル開発の場合、`/apps`と`/libs`は直接に書き込むことができます。これは、最上位のフォルダーが不変であるクラウド環境とは異なります。

### AEM as a Cloud Service の開発ツール {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>
>* 一部のお客様は、AEM Cloud Service Developer Console の刷新されたエクスペリエンスを試してみることもできます。 詳しくは、[こちらの記事](/help/implementing/developing/introduction/aem-developer-console.md)を参照してください。
>* AEM as a Cloud Service Developer Console を、同様の名前の [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) と混同しないでください。

オーサー層の開発環境でCRXDE liteにアクセスできますが、ステージングや実稼動環境にはアクセスできません。 不変リポジトリー（`/libs`、`/apps`）に実行時に書き込むことはできないので、書き込もうとするとエラーが発生します。

代わりに、AEM as a Cloud Service Developer Console からリポジトリブラウザーを起動して、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対してリポジトリへの読み取り専用ビューを提供できます。 詳しくは、[&#x200B; リポジトリブラウザー](/help/implementing/developing/tools/repository-browser.md)を参照してください。

AEM as a Cloud Service開発者向け環境をデバッグするための一連のツールは、RDE、開発、ステージ、実稼動環境用の[AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/aem-developer-console.md)で利用できます。 URLは、オーサーまたはパブリッシュサービスのURLを次のように調整することで決定できます。

`https://dev-console-<namespace>.<cluster>.dev.adobeaemcloud.com`

ショートカットとして、次の Cloud Manager CLI コマンドを使用して、下記の環境パラメーターに基づいて AEM as a Cloud Service Developer Console を起動できます。

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

詳しくは、[リリース情報](/help/release-notes/home.md)を参照してください。

開発者は、ステータス情報を生成し、様々なリソースを解決できます。

以下に示すように、使用可能なステータス情報には、バンドル、コンポーネント、OSGi設定、オーク インデックス、OSGi サービス、およびSling ジョブの状態が含まれます。

![開発者コンソール 1](/help/implementing/developing/introduction/assets/devconsole1.png)

下図に示すように、開発者はパッケージの依存関係とサーブレットを解決できます。

![開発者コンソール 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![開発者コンソール 3](/help/implementing/developing/introduction/assets/devconsole3.png)

また、デバッグにも便利な、AEM as a Cloud Service Developer Console には、次のようにクエリの説明を実行ツールへのリンクがあります。

![開発者コンソール 4](/help/implementing/developing/introduction/assets/devconsole4.png)

実稼働プログラムの場合、AEM as a Cloud Service Developer Console へのアクセスは Adobe Admin Console の「Cloud Manager - 開発者の役割」で定義されます。一方、サンドボックスプログラムの場合、AEM as a Cloud Service Developer Console は、AEM as a Cloud Service へのアクセス権を付与する製品プロファイルを持つすべてのユーザーが利用できます。 すべてのプログラムで、ステータスダンプとリポジトリブラウザーには「Cloud Manager - デベロッパーの役割」が必要です。また、オーサーサービスとパブリッシュサービスの両方のサービスからデータを表示するには、両方のサービスで AEM ユーザーまたはAEM 管理者製品プロファイルでもユーザーが定義されている必要があります。 ユーザー権限の設定について詳しくは、 [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja) を参照してください。

### パフォーマンスの監視 {#performance-monitoring}

Adobeは、アプリケーションのパフォーマンスを監視し、低下が発生した場合に対処するための対策を講じます。 現在、アプリケーションの指標は観察できません。

## メールの送信 {#sending-email}

以下の節では、メールのリクエスト、設定、送信の方法について説明します。

>[!NOTE]
>
>メールサービスは、OAuth2 サポートを使用して設定できます。 詳しくは、[メールサービスの OAuth2 サポート](/help/security/oauth2-support-for-mail-service.md)を参照してください。

### 送信メールの有効化 {#enabling-outbound-email}

メールの送信に使用されるポートは、デフォルトでは無効になっています。 ポートをアクティブにするには、[高度なネットワーク](/help/security/configuring-advanced-networking.md)を設定して、対象となるポート（465 や 587 など）をプロキシポートにマッピングするエンドポイントのポート転送ルールを、必要な環境ごとに設定するようにします（`PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`）。

Adobeはフレキシブルポートエグレスのトラフィックのパフォーマンスを最適化できるため、`kind` パラメーターを`flexiblePortEgress`に設定して高度なネットワークを設定することをお勧めします。 一意のエグレス IP アドレスが必要な場合は、`kind` パラメーターを `dedicatedEgressIp` に設定します。 他の理由で既に VPN を設定してある場合は、その高度なネットワークバリエーションから提供される一意の IP アドレスも使用できます。

メールクライアントに直接メールを送信するのではなく、メールサーバーを通じてメールを送信する必要があります。 そうしないと、メールがブロックされる可能性があります。

### メールの送信 {#sending-emails}

[Day CQ メールサービス OSGI サービス &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=ja#configuring-the-mail-service)を使用する必要があり、メールは受信者に直接送信するのではなく、サポート要求に示されているメールサーバーに送信する必要があります。

### 設定 {#email-configuration}

AEMの電子メールは、[Day CQ Mail Service OSGI サービス &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=ja#configuring-the-mail-service)を使用して送信する必要があります。

メールの設定について詳しくは、 [AEM 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html?lang=ja) を参照してください。 AEM as a Cloud Serviceの場合は、`com.day.cq.mailer.DefaultMailService` OSGi サービスに次の必要な調整を行います。

* SMTP サーバーホスト名は$[env:AEM_PROXY_HOST;default=proxy.tunnel]に設定する必要があります
* SMTP サーバーポートは、高度なネットワーク機能を設定する際に、API 呼び出しで使用される portForwards パラメーターに設定された元のプロキシポートの値に設定してください。 例えば、（465 ではなく）30465 などとします。

SMTP サーバーポートは、高度なネットワークを設定する際にAPI呼び出しで使用されるportForwards パラメーターで設定される`portDest`値として設定する必要があり、`portOrig`値は必要な30000 ～ 30999の範囲内の有意義な値である必要があります。 例えば、SMTP サーバーポートが 465 の場合、ポート 30465 を `portOrig` の値として使用します。

この例で、SSL を有効にする必要がある場合、**Day CQ Mail Service OSGI** サービスの設定は次のとおりです。

* `smtp.port` を `30465` に設定
* `smtp.ssl` を `true` に設定

または、宛先ポートが 587 の場合、`portOrig` 値の 30587 を使用する必要があります。 また、SSL を無効にする必要がある場合、Day CQ Mail Service OSGi サービスの設定は次のとおりです。

* `smtp.port` を `30587` に設定
* `smtp.ssl` を `false` に設定

`smtp.starttls` プロパティは、実行時に AEM as a Cloud Service によって適切な値に自動的に設定されます。 したがって、`smtp.ssl` が true に設定されている場合、`smtp.startls` は無視されます。 `smtp.ssl` が false に設定されている場合、`smtp.starttls` は true に設定されます。 これは、OSGI 構成で設定されている `smtp.starttls` 値には関係ありません。


オプションで、メールサービスに OAuth2 サポートを設定できます。 詳しくは、[メールサービスの OAuth2 サポート](/help/security/oauth2-support-for-mail-service.md)を参照してください。

### 従来のメール設定 {#legacy-email-configuration}

2021.9.0 リリースより前は、カスタマーサポートへの依頼を通じてメールが設定されていました。 `com.day.cq.mailer.DefaultMailService` OSGi サービスに必要な次の調整に注意してください。

AEM as a Cloud Service では、ポート 465 を通じてメールを送信する必要があります。 TLS オプションが有効になっている限り、メールサーバーがポート 465 をサポートしていない場合は、ポート 587 を使用できます。

ポート 465 がリクエストされた場合：

* `smtp.port` を `465` に設定
* `smtp.ssl` を `true` に設定

さらに、ポート 587 がリクエストされた場合は、

* `smtp.port` を `587` に設定
* `smtp.ssl` を `false` に設定

`smtp.starttls` プロパティは、実行時に AEM as a Cloud Service によって適切な値に自動的に設定されます。 したがって、`smtp.ssl` が true に設定されている場合、`smtp.startls` は無視されます。 `smtp.ssl` が false に設定されている場合、`smtp.starttls` は true に設定されます。 これは、OSGi設定で設定された`smtp.starttls`値に関係なく行われます。

SMTP サーバーホストは、メールサーバーのホストに設定してください。

## 複数値の大きなプロパティの回避 {#avoid-large-mvps}

AEM as a Cloud Service の基盤となる Oak コンテンツリポジトリは、複数値プロパティ（MVP）の数が非常に多い状況での使用を意図していません。 経験則として、MVP を 1000 未満に保ってください。 しかし、実際の成果は、さまざまな要因に左右されます。

警告は、1000 件を超えるとデフォルトでログに記録されます。 次のようになります。

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

大規模な MVP では、16 MB を超える MongoDB ドキュメントが原因で、次のようなエラーが発生する可能性があります。

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

詳しくは、[Apache Oak のドキュメント](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property)を参照してください。

## [!DNL Assets] 開発のガイドラインとユースケース {#use-cases-assets}

Assets as a Cloud Service の開発ユースケース、推奨事項、参考資料については、[Assets の開発者向けリファレンス](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis)を参照してください。
