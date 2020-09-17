---
title: Cloud Readiness Analyzer の使用
description: Cloud Readiness Analyzer の使用
translation-type: tm+mt
source-git-commit: b0ea504fe9b1f2d8eadb9fd263c983dae090cd1a
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 71%

---


# Cloud Readiness Analyzer の使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzer を使用する際の重要な考慮事項 {#imp-considerations}

Cloud Readiness Analyzer（CRA）を実行するには、次の重要事項を考慮してください。

* CRA レポートは、Adobe Experience Manager（AEM）[パターン検出](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/deploying/upgrading/pattern-detector.translate.html)の出力を使用して作成されます。CRA で使用するパターン検出のバージョンは、CRA インストールパッケージに含まれています。

* CRA は、**管理者ユーザー**&#x200B;または&#x200B;**管理者**&#x200B;グループのユーザーのみが実行できます。

* CRA は、バージョン 6.1 以降を含む AEM インスタンスでサポートされます。

   >[!NOTE]
   > AEM 6.1 に CRA をインストールするための特別な要件については、[AEM 6.1 へのインストール](#installing-on-aem61)を参照してください。

* CRA はどの環境でも実行できますが、*ステージング*&#x200B;環境で実行することをお勧めします。

   >[!NOTE]
   >ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、*実稼動*&#x200B;環境にできる限り近い&#x200B;*オーサー*&#x200B;環境で CRA を実行することをお勧めします。または、実稼動版の&#x200B;*オーサー*&#x200B;環境のクローンで実行することもできます。

* CRA レポートのコンテンツの生成には、数分から数時間まで、相当な時間がかかる場合があります。必要な時間は、AEM リポジトリコンテンツのサイズと特性、AEM バージョン、その他の要因に大きく左右されます。

* レポートのコンテンツの生成に非常に時間がかかる場合があるため、コンテンツはバックグラウンドプロセスで生成され、キャッシュに保持されます。レポートの表示とダウンロードは、期限が切れるか、レポートが明示的に更新されるまでコンテンツキャッシュを利用するので、比較的高速でおこなわれます。レポートコンテンツの生成中にブラウザータブを閉じても、キャッシュでレポートのコンテンツが使用可能になったら戻って表示できます。

## 入手方法 {#availability}

Cloud Readiness Analyzer は、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)ポータルから Cloud Readiness Analyzer をダウンロードします。

## Cloud Readiness Analyzer レポートの表示 {#viewing-report}

### Adobe Experience Manager 6.3.0 以降 {#aem-later-versions}

Cloud Readiness Analyzer の表示方法を学ぶには、次のセクションに従います。

1. Adobe Experience Manager を選択し、ツール／**操作**／**Cloud Readiness Analyzer** に移動します。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 「 **レポートの** 生成」をクリックして、Cloud Readiness Analyzerを実行します。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-generate-report.png)

1. CRAがレポートを生成中に、ツールが行った進行状況を画面で確認できます。 分析された項目の数と、見つかった結果の数が表示されます。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-generate-report-1.png)


1. CRAレポートが生成されると、検索のタイプと重要度レベル別に整理された表形式で、結果の概要と数が表示されます。 特定の検索の詳細を表示するには、表内の検索のタイプに対応する番号をクリックします。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-summary-table.png)

上記のアクションは、レポート内のその検索場所まで自動的にスクロールします。

![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-summary-table-1.png)

1. You have the option of downloading the report in a comma-separated values (CSV) format by clicking on **CSV**, as shown in the figure below.

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-download-csv.png)

   >[!NOTE]
   >CRA に対して「**レポートの更新**」をクリックしてキャッシュをクリアし、レポートを再生成させることができます。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-refresh.png)

   >[!NOTE]
   >レポートが再生成される間、完了率の観点での進行状況が次の画像のように表示されます。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-refresh-1.png)


### Adobe Experience Manager 6.2 および 6.1 {#aem-specific-versions}

Adobe Experience Manager 6.2 では、Cloud Readiness Analyzer ツールの CSV レポートを生成およびダウンロードするリンクのみに制限されています。

Adobe Experience Manager 6.1 では、このツールは機能せず、HTTP インターフェイスのみを使用できます。

>[!NOTE]
>すべてのバージョンで、付属のパターン検出は独立して実行できます。

## Cloud Readiness Analyzer レポートの解釈 {#cra-report}

Cloud Readiness Analyzer ツールを AEM インスタンスで実行すると、結果としてレポートがツールウィンドウに表示されます。

レポートの形式は次のとおりです。

* **レポートの概要**：次の情報を含む、レポート自体に関する情報。
   * **レポート時間**：レポートの内容が生成され、最初に使用可能になった時間。
   * **有効期限**：レポートコンテンツのキャッシュが期限切れになる時期。
   * **生成期間**：レポートコンテンツ生成プロセスに費やされた時間。
   * **結果数**：レポートに含まれる結果の合計数。
* **システム概要**：CRA が実行された AEM システムに関する情報です。
* **発見カテゴリ**：各セクションが同じカテゴリの 1 つ以上の発見に対応する複数セクション。各セクションには次の内容が含まれます。カテゴリ名、サブタイプ、発見数と重要度、概要、カテゴリドキュメントへのリンク、個々の発見情報。

アクションの大まかな優先度を示すために、各発見に重要度レベルが割り当てられます。各検索カテゴリの詳細については、「 [パターン検出カテゴリ」を参照してください。](https://docs.adobe.com/content/help/en/experience-manager-pattern-detection/table-of-contents/aso.html)

次の表に、重要度レベルを示します。

| 重要度 | 説明 |
|--- |--- |
| INFO | 情報提供の目的で提供されます。 |
| ADVISORY | アップグレードに関する問題の可能性があります。さらに調査をおこなうことをお勧めします。 |
| MAJOR | 対処する必要があるアップグレードに関する問題の可能性があります。 |
| CRITICAL | アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |


## Cloud Readiness Analyzer の CSV レポートの解釈 {#cra-csv-report}

AEM インスタンスから **CSV** オプションをクリックすると、Cloud Readiness Analyzer レポートの CSV 形式がコンテンツキャッシュから作成され、ブラウザーに返されます。ブラウザーの設定に応じて、このレポートは、デフォルト名が `results.csv` のファイルとして自動的にダウンロードされます。

キャッシュの有効期限が切れた場合は、CSV ファイルを作成してダウンロードする前にレポートが再生成されます。

レポートの CSV 形式には、パターン検出の出力から生成され、カテゴリタイプ、サブタイプ、重要度レベルで並べ替え、整理された情報が含まれます。この形式は、Microsoft Excel などのアプリケーションでの表示や編集に適しています。これは、進行状況を測定するために時間の経過と共にレポートを比較する際に役立つ、繰り返し可能な形式で発見情報をすべて提供することを目的としています。

CSV 形式レポートの列は次のとおりです。

* **コード**：カテゴリコード
* **タイプ**：カテゴリ名
* **サブタイプ**：カテゴリのサブタイプ
* **重要度**：重要レベル
* **識別子**：発見の主な識別子
* **その他**：発見に関する追加情報
* **メッセージ**：発見のために提供されたメッセージ
* **詳細情報**：カテゴリに関するオンラインヘルプにアクセスするために使用できるリンク
* **コンテキスト**：発見データの JSON 文字列

個々の発見の列の値「\N」は、データが提供されなかったことを示します。

## HTTP インターフェイス {#http-interface}

CRA は HTTP インターフェイスを提供し、AEM 内でのユーザーインターフェイスの代替として使用できます。このインタフェースは、HEAD コマンドと GET コマンドの両方をサポートしています。CRA レポートを生成し、JSON、CSV、タブ区切り値（TSV）の 3 つの形式のいずれかで返す場合に使用します。

CRA がインストールされているサーバーの HTTP アクセスには、次の URL を使用できます。`<host>` は、ホスト名と必要に応じてポートを示します。
* `http://<host>/apps/readiness-analyzer/analysis/result.json` JSON 形式の場合
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` CSV 形式の場合
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` TSV 形式の場合

### HTTP リクエストの実行 {#executing-http-request}

HTTP インターフェイスは、様々な方法で使用できます。

簡単な方法の 1 つは、管理者として AEM に既にサインインしているブラウザーと同じブラウザーで、「ブラウザー」タブを開くことです。「ブラウザー」タブに URL を入力して、結果をブラウザーで表示またはダウンロードすることができます。

また、`curl` や `wget` などのコマンドラインツールや、HTTP クライアントアプリケーションを使用することもできます。認証済みのセッションで「ブラウザー」タブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

これをおこなう方法の例を次に示します。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`

### ヘッダーとパラメーター {#http-headers-and-parameters}

このインターフェイスでは、次の HTTP ヘッダーが使用されます。

* `Cache-Control: max-age=<seconds>`:キャッシュフレッシュネスの有効期間を秒単位で指定します。 （[RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8) を参照）
* `Prefer: respond-async`:サーバーが非同期で応答する必要があることを指定します。 （[RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1) を参照）
* `Prefer: return=minimal`:サーバーが最小限の応答を返すように指定します。 （[RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2) を参照）

次の HTTP クエリパラメーターは、HTTP ヘッダーが容易に使用できない場合の便宜を図るために使用できます。

* `max-age` （数値、オプション）:キャッシュフレッシュネスの有効期間を秒単位で指定します。 この数値は 0 以上にする必要があります。デフォルトのフレッシュ時間は86400秒です。 このパラメーターまたは対応するヘッダーがない場合は、24時間の要求を処理するために新規キャッシュが使用され、その時点でキャッシュを再生成する必要があります。 を使用 `max-age=0` すると、新しく生成されたキャッシュのゼロ以外の有効期間を使用して、キャッシュが強制的にクリアされ、レポートの再生成が開始されます。
* `respond-async` （ブール値、オプション）:応答を非同期で提供する必要があることを指定します。 Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. キャッシュが新規の場合、このパラメーターは無効です。The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` （ブール値、オプション）:現在のキャッシュが空、古い、または古くなる前にキャッシュが古い場合に、要求に応じてサーバーがキャッシュを更新する可能性があることを指定します。 指定し `may-refresh-cache=true`た場合、または指定しなかった場合、サーバーはバックグラウンドタスクを開始し、パターンディテクターを呼び出してキャッシュを更新します。 この場合、キャッシュ `may-refresh-cache=false` が空または古い場合に行われた更新タスクがサーバーで開始されないと、レポートは空になります。 既に処理中の更新タスクは、このパラメータの影響を受けません。
* `return-minimal` （ブール値、オプション）:サーバーからの応答に、進行状況の指示とキャッシュの状態を含む状態のみをJSON形式で含めるように指定します。 の場合 `return-minimal=true`、応答本文はステータスオブジェクトに制限されます。 指定し `return-minimal=false`た場合、または指定しなかった場合は、完全な応答が返されます。
* `log-findings` （ブール値、オプション）:サーバが最初にキャッシュを構築または更新したときに、キャッシュの内容をログに記録する必要があることを指定します。 キャッシュからの検索はそれぞれJSON文字列として記録されます。 このログは、要求で新しいキャッシュが生成さ `log-findings=true` れた場合にのみ発生します。

HTTP ヘッダーと対応するクエリパラメーターの両方が存在する場合は、クエリパラメーターが優先されます。

HTTP インターフェイスを使用してレポートの生成を開始する簡単な方法は、次のコマンドを使用することです。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`

リクエストがおこなわれた後、クライアントはレポートを生成するのにアクティブである必要はありません。HTTPGETリクエストを使用して1つのクライアントでレポートの生成を開始し、レポートが生成されたら別のクライアントでキャッシュから、またはAEMユーザーインターフェイスのCRAツールを使用して表示できます。

### 応答 {#http-responses}

次の応答値を指定できます。

* `200 OK`:キャッシュのフレッシュネス有効期間内に生成された、パターンディテクターからの結果が応答に含まれていることを示します。
* `202 Accepted`:キャッシュが古いことを示すために使用します。 と `respond-async=true` この応答 `may-refresh-cache=true` が更新タスクの進行中であることを示す場合。 この応答 `may-refresh-cache=false` が単にキャッシュが古いことを示す場合。
* `400 Bad Request`：リクエストでエラーが発生したことを示します。詳細については、問題詳細形式のメッセージ（[RFC 7807](https://tools.ietf.org/html/rfc7807) を参照）を参照してください。
* `401 Unauthorized`:要求が承認されなかったことを示します。
* `500 Internal Server Error`：内部サーバーエラーが発生したことを示します。詳細については、問題詳細形式のメッセージを参照してください。
* `503 Service Unavailable`：サーバーが別の応答でビジー状態であり、このリクエストをタイムリーに処理できないことを示します。これは、同期リクエストがおこなわれた場合にのみ発生する可能性があります。詳細については、問題詳細形式のメッセージを参照してください。

## 管理者情報

### キャッシュ有効期間の調整 {#cache-adjustment}

CRA キャッシュのデフォルトの有効期間は 24 時間です。レポートを更新し、キャッシュを再生成するオプションを使用する場合、AEM インスタンスと HTTP インターフェイスの両方で、このデフォルト値はほとんどの CRA の使用に適していると考えられます。AEM インスタンスに対してレポート生成時間が特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュのライフタイム値は、次のリポジトリノードの `maxCacheAge` プロパティとして保存されます。`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

このプロパティの値は、キャッシュの有効期間（秒）です。管理者は、CRX／DE Lite を使用してキャッシュの有効期間を調整できます。

### AEM 6.1 へのインストール {#installing-on-aem61}

CRA は、パターンディテクターの実行に `repository-reader-service` と名付けられたシステムサービスユーザーアカウントを使用します。このアカウントは、AEM 6.2 以降で使用できます。AEM 6.1 では、CRA をインストールする&#x200B;*前に*、次の手順でこのアカウントを作成する必要があります。

1. [新しいサービスユーザーの作成](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/security/security-service-users.translate.html#creating-a-new-service-user)の手順に従って、ユーザーを作成します。UserID を `repository-reader-service` に設定し、中間パスを空のままにして、緑のチェックマークをクリックします。

2. [ユーザーとグループの管理の手順](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/security/security.translate.html#managing-users-and-groups)に従います。特に、`repository-reader-service` ユーザーを `administrators` グループに追加する手順については、ユーザーをグループに追加の手順を参照してください。

3. パッケージマネージャーを介して CRA パッケージをソース AEM インスタンスにインストールします。（これにより、`repository-reader-service` システムサービスユーザーの ServiceUserMapper 構成に必要な構成の修正が追加されます）
