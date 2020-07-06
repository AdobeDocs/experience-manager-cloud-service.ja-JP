---
title: Cloud Readiness Analyzer の使用
description: Cloud Readiness Analyzer の使用
translation-type: tm+mt
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: tm+mt
source-wordcount: '1871'
ht-degree: 75%

---


# Cloud Readiness Analyzer の使用 {#using-cloud-readiness-analyzer}

## Cloud Readiness Analyzer を使用する際の重要な考慮事項 {#imp-considerations}

次の節に従って、Cloud Readiness Analyzer(CRA)を実行する際の重要な考慮事項を理解してください。

* CRA レポートは、Adobe Experience Manager（AEM）[パターン検出](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/deploying/upgrading/pattern-detector.translate.html)の出力を使用して作成されます。CRA で使用するパターン検出のバージョンは、CRA インストールパッケージに含まれています。

* CRA may only be run by the **admin** user or a user in the **administrators** group.

* CRA は、バージョン 6.1 以降を含む AEM インスタンスでサポートされます。

   >[!NOTE]
   > AEM 6.1にCRAをインストールするための特別な要件については、 [AEM 6.1へのインストールを参照してください](#installing-on-aem61) 。

* CRA はどの環境でも実行できますが、*ステージング*&#x200B;環境で実行することをお勧めします。

   >[!NOTE]
   >In order to avoid an impact on business critical instances, it is recommended that you run CRA on an *Author* environment that is as close as possible to the *Production* environment in the areas of customizations, configurations, content and user applications. または、実稼働版の&#x200B;*オーサー*&#x200B;環境のクローンで実行することもできます。

* CRA レポートのコンテンツの生成には、数分から数時間まで、相当な時間がかかる場合があります。必要な時間は、AEM リポジトリコンテンツのサイズと特性、AEM バージョン、その他の要因に大きく左右されます。

* レポートのコンテンツの生成に非常に時間がかかる場合があるため、コンテンツはバックグラウンドプロセスで生成され、キャッシュに保持されます。レポートの表示とダウンロードは、期限が切れるか、レポートが明示的に更新されるまでコンテンツキャッシュを利用するので、比較的高速でおこなわれます。レポートコンテンツの生成中にブラウザータブを閉じても、キャッシュでレポートのコンテンツが使用可能になったら戻って表示できます。

## 入手方法 {#availability}

Cloud Readiness Analyzerは、Software Distribution Portalからzipファイルとしてダウンロードできます。 パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。

>[!NOTE]
>Download the Cloud Readiness Analyzer from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html) portal.

## Viewing the Cloud Readiness Analyzer Report {#viewing-report}

### Adobe Experience Manager 6.3.0 以降 {#aem-later-versions}

Cloud Readiness Analyzerレポートの表示方法を学ぶには、次のセクションに従います。

1. Adobe Experience Manager を選択し、ツール／**操作**／**Cloud Readiness Analyzer に移動します**。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 「**Cloud Readiness Analyzer**」をクリックすると、レポート生成が開始され、使用可能になると表示されます。

   >[!NOTE]
   >レポート全文を表示するには、ページを下にスクロールする必要があります。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. CRAレポートが生成され、表示されたら、下の図に示すように、「 **CSV**」をクリックして、レポートをコンマ区切り値(CSV)形式でダウンロードするオプションがあります。

   ![画像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >CRA に対して「**レポートの更新**」をクリックしてキャッシュをクリアし、レポートを再生成させることができます。

### Adobe Experience Manager 6.2 および 6.1 {#aem-specific-versions}

Cloud Readiness Analyzerツールは、Adobe Experience Manager6.2ではCSVレポートを生成およびダウンロードするリンクに限定されています。

Adobe Experience Manager 6.1 では、このツールは機能せず、HTTP インターフェイスのみを使用できます。

>[!NOTE]
>すべてのバージョンで、付属のパターン検出は独立して実行できます。

## Cloud Readiness Analyzer レポートの解釈 {#cra-report}

Cloud Readiness AnalyzerツールをAEMインスタンスで実行すると、結果としてレポートがツールウィンドウに表示されます。

レポートの形式は次のとおりです。

* **レポートの概要**: 次の情報を含む、レポート自体に関する情報です。
   * **レポート時間**: レポートの内容が生成され、最初に使用可能になった時。
   * **有効期限**: レポートコンテンツのキャッシュが期限切れになる時期。
   * **生成期間**: レポートコンテンツ生成プロセスに費やされた時間。
   * **検索数**: レポートに含まれる結果の合計数。
* **システム概要**：CRA が実行された AEM システムに関する情報です。
* **発見カテゴリ**：各セクションが同じカテゴリの 1 つ以上の発見に対応する複数セクション。各セクションには次の内容が含まれます。カテゴリ名、サブタイプ、発見数と重要度、概要、カテゴリドキュメントへのリンク、個々の発見情報。

アクションの大まかな優先度を示すために、各発見に重要度レベルが割り当てられます。

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

また、`curl` や `wget` などのコマンドラインツールや、HTTP クライアントアプリケーションを使用することもできます。認証済みのセッションでブラウザータブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

これをおこなう方法の例を次に示します。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`

### ヘッダーとパラメーター {#http-headers-and-parameters}

このインターフェイスでは、次の HTTP ヘッダーが使用されます。

* `Cache-Control: max-age=<seconds>`：キャッシュフレッシュネスの有効期間を秒単位で指定します。（[RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8) を参照）
* `Prefer: respond-async`：サーバーが非同期で応答する必要があることを示します。（[RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1) を参照）

次の HTTP クエリパラメーターは、HTTP ヘッダーが容易に使用できない場合の便宜を図るために使用できます。

* `max-age`（数値、オプション）：キャッシュフレッシュネスの有効期間を秒単位で指定します。この数値は 0 以上にする必要があります。デフォルトのフレッシュネス有効期間は 86400 秒です。つまり、このパラメーターまたは対応するヘッダーがない場合、レポートを再生成する 24 時間前に、新しいキャッシュが使用されてリクエストを処理します。`max-age=0` を使用すると、キャッシュが強制的にクリアされ、レポートの再生成が開始されます。このリクエストの直後に、フレッシュネスの有効期間は、前のゼロ以外の値にリセットされます。
* `respond-async`（ブール値、オプション）：応答を非同期で提供する必要があることを指定します。キャッシュが古い場合に `respond-async=true` を使用すると、レポートの生成とキャッシュの更新を待たずに、サーバーは `202 Accepted, processing cache` 応答を返します。キャッシュが新規の場合、このパラメーターは無効です。デフォルト値は `false` です。つまり、このパラメーターや対応するヘッダーがない場合、サーバーは同期して応答します。これには非常に長い時間がかかり、HTTP クライアントの最大応答時間の調整が必要になる場合があります。

HTTP ヘッダーと対応するクエリパラメーターの両方が存在する場合は、クエリパラメーターが優先されます。

HTTP インターフェイスを使用してレポートの生成を開始する簡単な方法は、次のコマンドを使用することです。
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

リクエストがおこなわれた後、クライアントはレポートを生成するのにアクティブである必要はありません。HTTP GET リクエストを使用して 1 つのクライアントでレポートの生成を開始し、レポートが生成された後は、別のクライアントのキャッシュや、AEM 内のユーザーインターフェイスの CSV ツールから表示できます。

### 回答 {#http-responses}

次の応答値を指定できます。

* `200 OK`：応答には、キャッシュのフレッシュネス有効期間内に生成されたパターン検出の結果が含まれます。
* `202 Accepted, processing cache`：キャッシュが古く、更新が進行中であることを示す非同期応答用に提供されます。
* `400 Bad Request`：リクエストでエラーが発生したことを示します。A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) for more details.
* `401 Unauthorized`：リクエストは承認されませんでした。
* `500 Internal Server Error`：内部サーバーエラーが発生したことを示します。詳細については、問題詳細形式のメッセージを参照してください。
* `503 Service Unavailable`：サーバーが別の応答でビジー状態であり、このリクエストをタイムリーに処理できないことを示します。これは、同期要求が行われた場合にのみ発生する可能性があります。 詳細については、問題詳細形式のメッセージを参照してください。

## 管理者情報

### キャッシュ有効期間の調整 {#cache-adjustment}

CRA キャッシュのデフォルトの有効期間は 24 時間です。レポートを更新し、キャッシュを再生成するオプションを使用する場合、AEM インスタンスと HTTP インターフェイスの両方で、このデフォルト値はほとんどの CRA の使用に適していると考えられます。AEM インスタンスに対してレポート生成時間が特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュのライフタイム値は、次のリポジトリノードの `maxCacheAge` プロパティとして保存されます。`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

このプロパティの値は、キャッシュの有効期間（秒）です。管理者は、CRX/DE Liteを使用してキャッシュの有効期間を調整できます。

### AEM 6.1へのインストール {#installing-on-aem61}

CRAは、パターンディテクターの実行に名前付けられたシステムサービスユーザーアカウント `repository-reader-service` を使用します。 このアカウントは、AEM 6.2以降で使用できます。 AEM 6.1では、CRAをインストールする *前に* 、次の手順でこのアカウントを作成する必要があります。

1. 「新しいサービスユーザーの [作成](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) 」の手順に従って、ユーザーを作成します。 UserIDをに設定し、中間パスを空のままにし `repository-reader-service` て、緑のチェックマークをクリックします。

2. 「ユーザーとグループの [管理」の手順に従います](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups)。特に、ユーザーをグループに追加する手順については、ユー `repository-reader-service` ザーを `administrators` グループに追加します。

3. Package Managerを介してCRAパッケージをソースAEMインスタンスにインストールします。 (これにより、 `repository-reader-service` システムサービスユーザーのServiceUserMapper構成に必要な構成の修正が追加されます)。
