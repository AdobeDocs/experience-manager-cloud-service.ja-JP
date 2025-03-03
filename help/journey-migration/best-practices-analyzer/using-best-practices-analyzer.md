---
title: ベストプラクティスアナライザーの使用
description: ベストプラクティスアナライザーを使用してアップグレードの準備状況を理解する方法について説明します。
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: 951f7fb56d1d8a3285973fda945cbc21f310925f
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 97%

---

# ベストプラクティスアナライザーの使用 {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="ベストプラクティスアナライザーの使用"
>abstract="ベストプラクティスアナライザー（旧称 Cloud Readiness Analyzer）と生成されたレポートの使用に関するドキュメントを確認します。ベストプラクティスアナライザーレポートは、アップグレードの全般的な準備状況を大まかに理解するために使用します。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="［ウェビナー］Adobe Experience Manager as a Cloud Service へのジャーニーを加速するツールの紹介"

## ベストプラクティスアナライザーを使用する際の重要な検討事項 {#imp-considerations}

ベストプラクティスアナライザー（BPA）を実行するには、次の重要事項を考慮してください。

* BPA レポートは、Adobe Experience Manager（AEM）[パターン検出](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=ja)の出力を使用して作成されます。BPA で使用するパターン検出のバージョンは、BPA インストールパッケージに含まれています。

* BPA は、**管理者**&#x200B;ユーザーまたは&#x200B;**管理者**&#x200B;グループのユーザーのみが実行できます。

* BPA は、バージョン 6.1 以降の AEM インスタンスでサポートされます。

  >[!NOTE]
  >AEM 6.1 に BPA をインストールするための特別な要件について詳しくは、[AEM 6.1 へのインストール](#installing-on-aem61)を参照してください。

* BPA はどの環境でも実行できますが、*ステージング*&#x200B;環境で実行することをお勧めします。

  >[!NOTE]
  >ビジネスクリティカルなインスタンスへの影響を避けるために、カスタマイズ、設定、コンテンツおよびユーザーアプリケーションの領域で、*実稼動*&#x200B;環境にできるだけ近い&#x200B;*ステージング*&#x200B;環境で BPA を実行することをお勧めします。または、実稼動版の&#x200B;*オーサー*&#x200B;環境のクローンで実行することもできます。

* BPA レポートのコンテンツの生成には、数分から数時間まで、相当な時間がかかる場合があります。必要な時間は、AEM リポジトリーコンテンツのサイズと特性、AEM バージョン、その他の要因に大きく左右されます。

* レポートのコンテンツの生成に非常に時間がかかる場合があるため、コンテンツはバックグラウンドプロセスで生成され、キャッシュに保持されます。レポートの表示とダウンロードは、期限が切れるか、レポートが明示的に更新されるまでコンテンツキャッシュを利用するので、比較的高速で行われます。レポートコンテンツの生成中にブラウザータブを閉じても、キャッシュでレポートのコンテンツが使用可能になったら戻って表示できます。

## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="ベストプラクティスアナライザーのダウンロード"
>abstract="ベストプラクティスアナライザーは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。"

ベストプラクティスアナライザーは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md) を使用して、このパッケージを AEM（Adobe Experience Manager）ソースインスタンスにインストールできます。

>[!NOTE]
>[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)ポータルからベストプラクティスアナライザーをダウンロードします。

## ソース環境の接続性 {#source-environment-connectivity}

ソース AEM インスタンスがファイアウォールの内側で動作していて、許可リストに追加された特定のホストにしか到達できない場合があります。BPA で生成したレポートを Cloud Acceleration Manager に正常に自動アップロードするには、AEM を実行しているインスタンスから次のエンドポイントにアクセスできる必要があります。

* Azure BLOB ストレージサービス：`casstorageprod.blob.core.windows.net`


## ベストプラクティスアナライザーレポートの表示 {#viewing-report}

### Adobe Experience Manager 6.3.0 以降 {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="ベストプラクティスアナライザーレポートを CAM に自動的にアップロード"
>abstract="BPA アップロードキーを指定して、生成した BPA レポートを Cloud Acceleration Manager（CAM）に自動的にアップロードします。"

ベストプラクティスアナライザーレポートを表示するには、このセクションの手順に従います。

1. Adobe Experience Manager を選択し、ツール／**操作**／**ベストプラクティスアナライザー**&#x200B;に移動します。

   ![ベストプラクティスアナライザー](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 「**レポートの生成**」をクリックして、ベストプラクティスアナライザーを実行します。

   ![レポートを生成](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> BPA バージョン 2.1.54 以降、Lighthouse スコアを取得するための新機能が導入されました。


1. **レポートを生成** をクリックすると、ポップアップが表示され、Lighthouse スコアのAEM公開サイト URL を要求します。 ユーザーは、指定されたフィールドに有効な URL を入力する必要があります。

   ![画像](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. URL が有効な場合は、成功メッセージが表示されます。

      ![画像](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. URL が無効な場合は、エラーメッセージが表示されます。

      ![画像](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. BPA アップロードキーを指定して、生成した BPA レポートを [Cloud Acceleration Manager（CAM）](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md)に自動的にアップロードします。アップロードキーを取得するには、[CAM のベストプラクティス分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)に移動します。

   ![BPA アップロードキーを設定](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>「**CAM へのレポートの自動アップロードをスキップ**」を選択すると、CAM への自動アップロードをスキップできます。スキップすることを選択した場合は、BPA レポートをコンマ区切り値ファイルとして手動でダウンロードし、そのファイルを CAM にアップロードする必要があります。操作を効率化するため、アップロードキーオプションを使用することをお勧めします。

>[!IMPORTANT]
>CAM に手動でアップロードする際、レポートのサイズは約 200 MB に制限されます。より大きなレポートの場合は、自動アップロードを活用する必要があります。

1. 有効なキーを指定すると、「**生成**」ボタンがアクティブになります。「**生成**」をクリックして、レポートの生成を開始します。

   ![レポートを生成](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. BPA がレポートを生成している間は、ツールの進行状況を画面で確認できます。進行状況が完了率で表示されます。また、分析された項目の数と、見つかった結果の数が表示されます。

   ![レポートの生成](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>BPA アップロードキーの有効期限のタイムスタンプが右上隅に表示されます。BPA アップロードキーの有効期限が近づいたら、更新する必要があります。キーを更新するには、「**更新**」をクリックして CAM に移動し、キーを更新します。

1. BPA レポートが生成された後は、概要と結果の数が、結果のタイプと重要度レベル別に整理された表形式で表示されます。特定の結果の詳細を取得するには、表で結果のタイプに対応する番号をクリックします。

   ![レポートの概要](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. 「**CSV に書き出し**」をクリックすると、レポートをコンマ区切り値（CSV）形式でダウンロードできます。また、「**CAM に移動**」をクリックして、CAM でレポートを表示することもできます。これにより、CAM の[ベストプラクティス分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)ページが表示されます。

BPA に対して「**レポートの更新**」をクリックしてキャッシュをクリアし、レポートを再生成させることができます。

![レポートを更新](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. キャッシュの有効期限が切れた場合は、「**CAM で最後に生成されたレポートを表示**」をクリックして CAM で最後に生成されたレポートを表示するか、「**新しいレポートを生成**」をクリックして新しいレポートの生成を開始することができます。

![レポートなし](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### ベストプラクティスアナライザーレポートでのフィルターの使用 {#bpa-filters}

[ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) に関連する結果を除外するには、次の手順に従います。

1. ページの左側にある左レールアイコンをクリックします。**ACS Commons フィルター**&#x200B;が表示されます。**ACS Commonsフィルター**&#x200B;をクリックして、下の画像に示すインタラクティブチェックボックスを表示します。

   ![ACS Commons フィルター](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >左レールアイコンは、BPA が ACS Commons の使用を検出した場合にのみ表示されます。

1. このボックスの選択を解除すると、ACS Commons に関連するすべての結果が除外されます。次の画像に示すように、**フィルター適用済みの結果数**&#x200B;がレポートに表示されます。このフィルターは、レポートがコンマ区切り値（CSV）形式で書き出される場合にも適用されます。

   ![フィルター適用済みの結果数](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >ACS Commons の結果は無視しないでください。AEM as a Cloud Service との互換性を確認するには、[ドキュメント](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility)を参照してください。

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## ベストプラクティスアナライザーレポートの説明 {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="ベストプラクティスアナライザーレポートの説明"
>abstract="BPA レポート出力は UI と CSV の 2 つのオプションで表示できます。ベストプラクティスアナライザーツールを AEM インスタンスで実行すると、結果として UI レポートがツールウィンドウに表示されます。レポートの CSV 形式には、パターン検出の出力から生成され、カテゴリタイプ、サブタイプ、重要度レベルで並べ替え、整理された情報が含まれます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=ja#analysis-report" text="ベストプラクティス分析レポートの確認"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=ja" text="ベストプラクティスアナライザーレポートのカテゴリについて"

ベストプラクティスアナライザーツールを AEM インスタンスで実行すると、結果としてレポートがツールウィンドウに表示されます。

レポートの形式は次のとおりです。

* **レポートの概要**：次の情報を含む、レポート自体に関する情報。
   * **レポート時間**：レポートの内容が生成され、最初に使用可能になった時間。
   * **有効期限**：レポートコンテンツのキャッシュが期限切れになる時期。
   * **生成期間**：レポートコンテンツ生成プロセスに費やされた時間。
   * **結果数**：レポートに含まれる結果の合計数。
* **システム概要**：BPA が実行された AEM システムに関する情報です。
* **発見カテゴリ**：各セクションが同じカテゴリの 1 つ以上の発見に対応する複数セクション。各セクションには次の内容が含まれます。カテゴリ名、サブタイプ、発見数と重要度、概要、カテゴリドキュメントへのリンク、個々の発見情報。

アクションの大まかな優先度を示すために、各発見に重要度レベルが割り当てられます。

>[!NOTE]
>各カテゴリの検索について詳しくは、[パターン検出のカテゴリ](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=ja)を参照してください。

次の表に、重要度レベルを示します。

| 重要度 | 説明 |
|--- |--- |
| INFO | 情報提供の目的で提供されます。 |
| ADVISORY | アップグレードに関する問題の可能性があります。さらに調査を行うことをお勧めします。 |
| MAJOR | 対処する必要があるアップグレードに関する問題の可能性があります。 |
| CRITICAL | アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |

## ベストプラクティスアナライザーの CSV レポートの説明 {#cra-csv-report}

AEM インスタンスから「**CSV**」オプションをクリックすると、ベストプラクティスアナライザーレポートが CSV 形式でコンテンツキャッシュから作成され、ブラウザーに返されます。ブラウザーの設定に応じて、このレポートは、デフォルト名が `results.csv` のファイルとして自動的にダウンロードされます。

キャッシュの有効期限が切れている場合、CSV ファイルが作成されダウンロードされる前にレポートが再生成されます。

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

BPA は HTTP インターフェイスを提供し、AEM 内でのユーザーインターフェイスの代替として使用できます。このインターフェイスは、HEAD コマンドと GET コマンドの両方をサポートしています。BPA レポートを生成し、JSON、CSV、タブ区切り値（TSV）の 3 つの形式のいずれかで返す場合に使用します。

BPA がインストールされているサーバーの HTTP アクセスには、次の URL を使用できます。`<host>` は、ホスト名と必要に応じてポートを示します。
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` JSON 形式の場合
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` CSV 形式の場合
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` TSV 形式の場合

### HTTP リクエストの実行 {#executing-http-request}

HTTP インターフェイスは、様々な方法で使用できます。

簡単な方法の 1 つは、管理者として AEM に既にサインインしているブラウザーと同じブラウザーで、「ブラウザー」タブを開くことです。「ブラウザー」タブに URL を入力して、結果をブラウザーで表示またはダウンロードすることができます。

また、`curl` または `wget` などのコマンドラインツールおよび HTTP クライアントアプリケーションも使用できます。認証済みのセッションで「ブラウザー」タブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

これを行う方法の例を次に示します。
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`

### ヘッダーとパラメーター {#http-headers-and-parameters}

このインターフェイスでは、次の HTTP ヘッダーが使用されます。

* `Cache-Control: max-age=<seconds>`：キャッシュフレッシュネスの有効期間を秒単位で指定します。（[RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8) を参照）
* `Prefer: respond-async`：サーバーが非同期で応答する必要があることを指定します。（[RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1) を参照）
* `Prefer: return=minimal`：サーバーが最小限の応答を返すように指定します。（[RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2) を参照）

次の HTTP クエリパラメーターは、HTTP ヘッダーが容易に使用できない場合の便宜を図るために使用できます。

* `max-age`（数値、オプション）：キャッシュフレッシュネスの有効期間を秒単位で指定します。この数値は 0 以上にする必要があります。デフォルトのフレッシュ有効期間は 86400 秒です。このパラメーターまたは対応するヘッダーがない場合、24 時間リクエストを処理するために新しいキャッシュが使用され、その時点でキャッシュを再生成する必要があります。`max-age=0` を使用すると、新しく生成されたキャッシュのゼロ以外の有効期間を使用して、キャッシュが強制的にクリアされ、レポートの再生成が開始されます。
* `respond-async`（ブール値、オプション）：応答を非同期で提供する必要があることを指定します。キャッシュが古い場合に `respond-async=true` を使用すると、キャッシュの更新とレポートの生成を待たずに、サーバーは `202 Accepted` 応答を返します。キャッシュが新規の場合、このパラメーターは無効です。デフォルト値は `false` です。このパラメーターや対応するヘッダーがない場合、サーバーは同期して応答します。これには非常に長い時間がかかり、HTTP クライアントの最大応答時間の調整が必要になる場合があります。
* `may-refresh-cache`（ブール値、オプション）：現在のキャッシュが空、古い、または古くなる場合、要求に応じてサーバーがキャッシュを更新することを指定します。`may-refresh-cache=true` の場合、または指定されていない場合、サーバーはバックグラウンドタスクを開始し、パターンディテクターを呼び出してキャッシュを更新します。`may-refresh-cache=false` の場合、キャッシュが空または古い場合に実行されるはずの更新タスクがサーバーで開始されないため、レポートは空になります。既に処理中の更新タスクは、このパラメーターの影響を受けません。
* `return-minimal`（ブール値、オプション）：サーバーからの応答に、進行状況の指示とキャッシュの状態を含む状態のみを JSON 形式で含めるように指定します。`return-minimal=true` の場合、応答本文はステータスオブジェクトに制限されます。`return-minimal=false` の場合または指定されていない場合、完全な応答が返されます。
* `log-findings`（ブール値、オプション）：サーバーが最初にキャッシュを構築または更新したときに、キャッシュの内容をログに記録するかどうかを指定します。キャッシュからの結果はそれぞれ JSON 文字列として記録されます。このログは、`log-findings=true` で、要求で新しいキャッシュが生成された場合にのみ発生します。

HTTP ヘッダーと対応するクエリパラメーターの両方が存在する場合は、クエリパラメーターが優先されます。

HTTP インターフェイスを使用してレポートの生成を開始する簡単な方法は、次のコマンドを使用することです。
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`

リクエストが行われた後、クライアントはレポートを生成するのにアクティブである必要はありません。HTTP GET リクエストを使用して 1 つのクライアントでレポートの生成を開始し、レポートが生成された後は、別のクライアントのキャッシュや、 AEM ユーザーインターフェイスの BPA ツールから表示できます。

### 応答 {#http-responses}

次の応答値を指定できます。

* `200 OK`：応答にキャッシュのフレッシュネス有効期間内に生成されたパターン検出の結果が含まれることを示します。
* `202 Accepted`：キャッシュが古いことを示すために使用します。`respond-async=true` および `may-refresh-cache=true` の場合、この応答は更新タスクが進行中であることを示します。`may-refresh-cache=false` の場合、この応答は単にキャッシュが古いことを示します。
* `400 Bad Request`：リクエストでエラーが発生したことを示します。詳細については、問題詳細形式のメッセージ（[RFC 7807](https://tools.ietf.org/html/rfc7807) を参照）を参照してください。
* `401 Unauthorized`：要求が承認されなかったことを示します。
* `500 Internal Server Error`：内部サーバーエラーが発生したことを示します。詳細については、問題詳細形式のメッセージを参照してください。
* `503 Service Unavailable`：サーバーが別の応答でビジー状態であり、このリクエストをタイムリーに処理できないことを示します。これは、同期リクエストが行われた場合にのみ発生する可能性があります。詳細については、問題詳細形式のメッセージを参照してください。

## 管理者情報

### キャッシュ有効期間の調整 {#cache-adjustment}

BPA キャッシュのデフォルトの有効期間は 24 時間です。レポートを更新し、キャッシュを再生成するオプションを使用する場合、AEM インスタンスと HTTP インターフェイスの両方で、このデフォルト値は BPA のほとんどの用途に適しています。AEM インスタンスに対してレポート生成時間が特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュのライフタイム値は、次のリポジトリーノードの `maxCacheAge` プロパティとして保存されます。`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

このプロパティの値は、キャッシュの有効期間（秒）です。管理者は、CRX／DE Lite を使用してキャッシュの有効期間を調整できます。

### AEM 6.1 へのインストール {#installing-on-aem61}

BPA は、パターンディテクターの実行に `repository-reader-service` と名付けられたシステムサービスユーザーアカウントを使用します。このアカウントは、AEM 6.2 以降で使用できます。AEM 6.1 では、BPA をインストールする&#x200B;*前に*、次の手順でこのアカウントを作成する必要があります。

1. [新しいサービスユーザーの作成](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html?lang=ja#creating-a-new-service-user) の手順に従って、ユーザーを作成します。UserID を `repository-reader-service` に設定し、中間パスを空のままにして、緑のチェックマークをクリックします。

2. [ユーザーとグループの管理の手順](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ja#managing-users-and-groups)に従います。特に、`repository-reader-service` ユーザーを `administrators` グループに追加する手順については、ユーザーをグループに追加の手順を参照してください。

3. パッケージマネージャーを介して BPA パッケージをソース AEM インスタンスにインストールします。（これにより、`repository-reader-service` システムサービスユーザーの ServiceUserMapper 構成に必要な構成の修正が追加されます）
