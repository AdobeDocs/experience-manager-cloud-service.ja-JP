---
title: Cloud Readiness Analyzerの使用
description: Cloud Readiness Analyzerの使用
translation-type: tm+mt
source-git-commit: 1ca9b2091befbafad0878d83fc7963c779146b2a
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 1%

---


# Cloud Readiness Analyzerの使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzerを使用する際の重要な考慮事項 {#imp-considerations}

Cloud Readiness Analyzer(CRA)の実行中の重要な考慮事項を理解するには、次の節に従ってください。

* CRAレポートは、Adobe Experience Manager(AEM) [パターンディテクターの出力を使用して作成されます](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)。 CRAが使用するパターンディテクターのバージョンは、CRAインストールパッケージに含まれています。

* CRAは、 *管理者ユーザーまたは* Administrators **** グループ内のユーザーのみが実行できます。

* CRAは、バージョン6.1以降を含むAEMインスタンスでサポートされます。

* CRAはどの環境でも実行できますが、 *Stage* 環境で実行することをお勧めします。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの各領域で、実稼働環境にできる限り近い *作成者* ステージング環境に対してCRAを実行することをお勧めします。 または、実稼働版の *作成者* 環境のクローンで実行することもできます。

* CRAレポートの生成には、数分から数時間の間に相当な時間がかかる場合があります。 必要な時間は、AEMリポジトリコンテンツのサイズと特性、AEMバージョン、その他の要因に大きく左右されます。

* レポートの生成に非常に長い時間がかかるので、結果はキャッシュに保持され、キャッシュの期限が切れるか、レポートが明示的に更新されるまで、以降の表示やダウンロードに使用できます。

## 入手方法 {#availability}

Cloud Readiness Analyzerは、Software Distribution Portalからzipファイルとしてダウンロードできます。 パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>Software Distribution Portal *保留中のCloud Readiness AnalyzerからCloud Readiness Analyzerをダウンロードします*。

## Cloud Readiness Analyzerの実行 {#running-tool}

Cloud Readiness Analyzerの実行方法を学ぶには、次のセクションに従います。

1. Select the Adobe Experience Manager and navigate to tools -> **Operations** -> **Cloud Readiness Analyzer**.

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Cloud Readiness Analyzerをクリックすると ****、レポートを生成するツール開始が発生し、数分後にはAEMインスタンスでサマリレポートが使用できるようになります。

   >[!NOTE]
   >完全なレポートを表示するには、ページを下にスクロールする必要があります。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### AEM 6.3以降 {#aem-older-version}

AEM 6.3以降では、Cloud Readiness Analyzerを実行する主な方法は次のとおりです。

1. Adobe Experience Managerインスタンスを選択し、ツール/ **操作** / **Cloud Readiness Analyzerに移動します**。

   >[!NOTE]
   >CRAは、ツールが開かれ次第、レポートを生成するバックグラウンドプロセスを開始します。 レポートの準備が整うまで、レポートの生成が進行中であることを示すメッセージが表示されます。 ブラウザーのタブを閉じてから、後でレポートの完了時に表示に戻ることができます。

1. CRAレポートが生成され、表示されたら、コンマ区切り値(CSV)でレポートをダウンロードするオプションがあります。 下の図に示すように、「 **CSV** 」をクリックして、完全なサマリレポートをコンマ区切り値(CSV)形式でダウンロードします。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

   >[!NOTE]
   >CRAのキャッシュをクリアし、左上隅の「レポートの **更新** 」ボタンをクリックしてレポートを再生成するように強制できます。

### AEM 6.2および6.1 {#aem-specific-versions}

Cloud Readiness Analyzerのユーザーインターフェイスは、AEM 6.2ではCSVレポートを生成およびダウンロードするためのリンクに制限されています。 AEM 6.1では、ユーザーインターフェイスは機能せず、HTTPインターフェイスのみを使用できます。

すべてのバージョンで、付属のパターンディテクターは独立して実行できます。

次の手順に従って、Adobe Experience Manager (AEM) 6.1および6.2用のCSVレポートをダウンロードします。

1.Navigate to **Adobe Experience Manager Web Console
Configuration** using `https://serveraddress:serverport/system/console/configMgr`.

1. 次の図に示すように、「 **Status** 」タブを選択し、ドロップダウンリストから「 **Pattern Detector** 」を検索します。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. サマリレポートはzipフォルダーまたはJSON形式でダウンロードできます。

## CRAサマリレポート {#cra-summary-report}

Cloud Readiness AnalyzerをAEMユーザーインターフェイスで実行すると、結果としてレポートがツールウィンドウに表示されます。

レポートの形式は次のとおりです。

* *レポートの概要*: レポートがいつ生成されたかなど、レポート自体に関する情報です。
* *システム概要*: CRAが実行されたAEMシステムに関する情報です。
* *検索カテゴリ*: 各セクションが同じカテゴリの1つ以上の結果に対応する複数のセクション。 各セクションには、次の内容が含まれます。 カテゴリ名、サブタイプ、検索数と重要度、概要、カテゴリドキュメントへのリンク、個々の検索情報。

行動の大まかな優先度を示すために、各発見に重要度レベルを割り当てる。

次の表に、重要度レベルを示します。

| Importance | 説明 |
|--- |--- |
| INFO | この検索結果は、情報を提供する目的で提供されます。 |
| 助言 | この結果、アップグレードに関する問題が発生する可能性があります。 さらに調査を行うことをお勧めします。 |
| メジャー | この結果、アップグレードに関する問題に対処する必要がある可能性があります。 |
| 重要 | この結果、アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |

## CRA CSVレポート {#crs-csv-report}

AEMインスタンスから **CSV** (CSV)オプションをクリックすると、Cloud Readiness AnalyzerレポートのCSV形式が結果キャッシュから作成され、ブラウザーに返されます。 ブラウザの設定に応じて、このレポートは、デフォルト名がのファイルとして自動的にダウンロードされ `results.csv`ます。 キャッシュの有効期限が切れた場合は、CSVファイルを作成してダウンロードする前にレポートが再生成されます。

レポートのCSV形式には、パターンディテクターの出力から生成され、カテゴリタイプ、サブタイプ、重要度レベルで並べ替え、整理された情報が含まれます。 この形式は、Microsoft Excelなどのアプリケーションでの表示や編集に適しています。 これは、進行状況を測定するために時間の経過と共にレポートを比較する際に役立つ、繰り返し可能な形式で検索情報をすべて提供することを目的としています。

CSV形式レポートの列は次のとおりです。

* **code**: カテゴリコード
* **type**: カテゴリ名
* **subtype**: カテゴリのサブタイプ
* **importance**: 重要度
* **identifier**: その発見の主な識別子
* **other**: 発見に関する追加情報
* **message**: 発見のために提供されたメッセージ
* **moreInfo**: カテゴリに関するオンラインヘルプにアクセスするために使用できるリンク
* **context**: 検索データのJSON文字列

個々の検索結果の列の値「\N」は、データが提供されなかったことを示します。

## HTTPインターフェイス {#http-interface}

CRAはHTTPインターフェイスを提供し、AEMユーザーインターフェイスの代替として使用できます。 このインタフェースは、HEAD[ヘッド]コマンドとGET[GET]コマンドの両方をサポートしています。 CRAレポートを生成し、次の3つの形式のいずれかで返す場合に使用します。 JSON、CSV、タブ区切り値(TSV)。

CRAがインストールされているサーバーのHTTPアクセスには、次のURLを使用できます。 `<host>` は、ホスト名、必要に応じてポートです。
* `http://<host>/apps/readiness-analyzer/analysis/result.json` JSON形式の場合
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` CSV形式の場合
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` TSV形式の場合

### HTTPリクエストの実行 {#executing-http-request}

HTTPインターフェイスは、様々な方法で使用できます。

簡単な方法の1つは、管理者としてAEMに既にサインインしているブラウザーと同じブラウザーでブラウザータブを開くことです。 ブラウザータブにURLを入力して、結果をブラウザーで表示またはダウンロードすることができます。

また、 `curl` やなどのコマンドラインツールや、HTTPクライアントアプリケーションを使用す `wget` ることもできます。 認証済みのセッションでブラウザータブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

これを行う方法の例を次に示します。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### ヘッダーとパラメーター {#http-headers-and-parameters}

このインターフェイスでは、次のHTTPヘッダーが使用されます。

* `Cache-Control: max-age=<seconds>`: キャッシュフレッシュネスの有効期間を秒単位で指定します。 ( [RFC 7234を参照](https://tools.ietf.org/html/rfc7234#section-5.2.2.8))。
* `Prefer: respond-async`: サーバーが非同期で応答する必要があることを示します。 ( [RFC 7240を参照](https://tools.ietf.org/html/rfc7240#section-4.1))。

次のHTTPクエリパラメーターは、HTTPヘッダーが容易に使用できない場合の便宜を図るために使用できます。

* `max-age` （数値、オプション）: キャッシュフレッシュネスの有効期間を秒単位で指定します。 この数値は0以上にする必要があります。 デフォルトのフレッシュネス有効期間は86400秒です。つまり、このパラメーターまたは対応するヘッダーがない場合、レポートを再生成する24時間前に、新しいキャッシュが使用されてリクエストが提供されます。 を使用 `max-age=0` すると、キャッシュが強制的にクリアされ、レポートの再生成が開始されます。 このリクエストの直後に、フレッシュネスの有効期間は、前のゼロ以外の値にリセットされます。
* `respond-async` （ブール値、オプション）: 応答を非同期で提供する必要があることを指定します。 キャッシュが古い `respond-async=true` 場合にを使用すると、レポートが生成されキャッシュが更新されるのを待たずに、サーバは応答を返 `202 Accepted, processing cache` します。 キャッシュが新規の場合、このパラメーターは無効です。 デフォルト値は `false`です。つまり、このパラメーターや対応するヘッダーがない場合、サーバーは同期的に応答します。これには非常に長い時間がかかり、HTTPクライアントの最大応答時間の調整が必要になる場合があります。

HTTPヘッダーと対応するクエリパラメーターの両方が存在する場合は、クエリパラメーターが優先されます。

HTTPインターフェイスを使用してレポートの生成を開始する簡単な方法は、次のコマンドを使用することです。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

リクエストが行われた後は、クライアントはアクティブなままでレポートを生成する必要はありません。 レポートの生成は、HTTP GETリクエストを使用してあるクライアントで開始でき、レポートが生成されたら、別のクライアントのキャッシュまたはAEMユーザーインターフェイスのCSVツールから表示できます。

### 応答(#http-responses)

次の応答値を指定できます。

* `200 OK`: 応答には、キャッシュのフレッシュネス有効期間内に生成されたパターンディテクターからの結果が含まれます。
* `202 Accepted, processing cache`: キャッシュが古く、更新が進行中であることを示す非同期応答用に提供されます。
* `400 Bad Request`: 要求でエラーが発生したことを示します。 詳細については、Problem Details形式のメッセージ( [RFC 7807を参照](https://tools.ietf.org/html/rfc7807))を参照してください。
* `401 Unauthorized`: 要求は承認されませんでした。
* `500 Internal Server Error`: 内部サーバーエラーが発生したことを示します。 詳細については、「問題の詳細」の形式のメッセージを参照してください。
* `503 Service Unavailable`: サーバーが別の応答でビジー状態であり、この要求をタイムリーに処理できないことを示します。 これは、同期要求が行われた場合にのみ発生します。 詳細については、「問題の詳細」の形式のメッセージを参照してください。

## キャッシュのライフタイム調整 {#cache-adjustment}

CRAキャッシュのデフォルトの有効期間は24時間です。 レポートを更新し、キャッシュを再生成するオプションを使用する場合、ユーザーインターフェイスとHTTPインターフェイスの両方で、このデフォルト値はCRAのほとんどの使用に適していると考えられます。 レポート生成時間がAEMインスタンスに特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュのライフタイム値は、次のリポジトリノードの `maxCacheAge` プロパティとして保存されます。
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

このプロパティの値は、キャッシュの有効期間（秒）です。 管理者は、AEMへのCRX/DE Liteインターフェイスを使用してキャッシュの有効期間を調整できます。





