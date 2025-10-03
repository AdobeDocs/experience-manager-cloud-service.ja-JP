---
title: コンテンツトランスファーツールの基本を学ぶ
description: コンテンツトランスファーツールの基本を学ぶ
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 100%

---


# コンテンツトランスファーツールの基本を学ぶ {#getting-started-content-transfer-tool}


## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="ダウンロード"
>abstract="コンテンツトランスファーツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=ja" text="リリースノート"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html" text="ソフトウェア配布ポータル"

コンテンツトランスファーツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)を使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。最新バージョンについて詳しくは、[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=ja)を参照してください。

サポートされるのはバージョン 2.0.0 以降のみで、最新バージョンを使用することをお勧めします。

>[!NOTE]
>[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)からコンテンツトランスファーツールをダウンロードします。

## ソース環境の接続性 {#source-environment-connectivity}

>[!NOTE]
>
>移行セットが Cloud Acceleration Manager から削除されている場合も、接続エラーが発生する可能性があります。

ソース AEM インスタンスがファイアウォールの内側で動作していて、許可リストに追加された特定のホストにしか到達できない場合があります。抽出を正常に実行するには、AEM を実行しているインスタンスから、次のエンドポイントにアクセスできる必要があります。

* Azure BLOB ストレージサービス：`casstorageprod.blob.core.windows.net`

>[!NOTE]
>エラー： 「javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX パスのビルドに失敗しました: sun.security.provider.certpath.SunCertPathBuilderException: リクエストされたターゲットへの有効な証明書パスが見つかりません」が原因で抽出に失敗した場合は、関連する CA 証明書を読み込むことで問題を解決できます。

### SSL ログを有効にする {#enable-ssl-logging}

SSL/TLS 接続の問題の理解は困難な場合があります。 抽出プロセス中に接続の問題をトラブルシューティングするには、次の手順に従って、ソース AEM 環境のシステムコンソールで SSL ログを有効にします。

1. **ツール／操作／Web コンソール**&#x200B;に移動するか、*https://serveraddress:serverport/system/console/configMgr* の URL に直接アクセスして、ソースインスタンスの Adobe Experience Manager web コンソールに移動します
1. **コンテンツトランスファーツール抽出サービスの設定**&#x200B;を検索します。
1. 鉛筆アイコンボタンを使用して、設定値を編集します。
1. を有効にします。 **抽出用の SSL ログを有効にする** 設定してから、 **保存**:

   ![画像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>
>このフラグは、SSL の問題のデバッグにのみ使用されます。抽出を実行する前に、フラグが無効になっていることを確認してください。これには大量のディスク領域が必要になる場合があります。これにより、ドライブ容量がいっぱいになり、抽出プロセスが失敗する可能性があります。

## コンテンツトランスファーツールの実行 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="コンテンツトランスファーツールの実行"
>abstract="この節では、コンテンツトランスファーツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。"
>additional-url="https://video.tv.adobe.com/v/327070/?quality=12&amp;learn=on&captions=jpn" text=" デモを見る"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration" text="チュートリアル - コンテンツトランスファーツールの使用"

次の節は、コンテンツトランスファーツールの新しいバージョンに適用されます。この節では、コンテンツトランスファーツールを使用してコンテンツを AEM as a Cloud Service に移行する方法について説明します。

### 抽出設定フェーズ {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="抽出設定フェーズ"
>abstract="移行セットを作成して管理し、抽出キーをコピーする方法を説明します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration" text="チュートリアル - コンテンツトランスファーツールの使用"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Cloud Acceleration Manager（CAM）にログインし、以前に作成した CAM プロジェクトをクリックして、AEM as a Cloud Service への移行に対する準備状況を評価します。CAM プロジェクトをまだ作成していない場合は、CAM でのプロジェクトの作成と管理を参照してください。

1. **コンテンツ転送**&#x200B;カードをクリックして、移行セットリスト表示を開きます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 「**移行セットを作成**」をクリックして移行セットを作成します。

   >[!NOTE]
   >
   >Cloud Acceleration Manager で、プロジェクトごとに最大 10 個（期限切れセットを含む）の移行セットを作成できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   次のダイアログボックスが表示されます。移行セットは、無操作状態が長時間続くと有効期限が切れます。警告がプロジェクトカードおよび移行ジョブテーブルの行に一定期間表示された後、移行セットは期限切れになり、そのデータは使用できなくなります。詳しくは、[移行セットの有効期限](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)を確認してください。

   移行セットの作成時に、一時的な移行データが保存される地域を選択できます。取り込み時に最適なパフォーマンスを確保するために、ターゲットクラウド環境に最も近い地域を選択することをお勧めします。移行セットの作成後に地域を変更することはできません。別の地域を使用するには、新しい移行セットを作成する必要があります。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >名前は AEM ノードと同じ規則に従う必要があるので、`. / : [ ] | * < > ^ ? { } % # ` の文字や、異常な記号または絵文字を含めることはできません。

1. これで、リスト表示に移行リストが表示されます。3 つのドット記号（**...**）をクリックして、ドロップダウンを開き、「**抽出キーをコピー**」を選択します。このキーは、抽出段階で必要になります。この抽出キーをコピーします。

   >[!NOTE]
   >
   >抽出キーを使用すると、移行元の AEM 環境から移行セットに安全に接続できます。この鍵は、パスワードと同じ注意を払って扱ってください。また、メールのような安全でないメディアでは、鍵を共有しないでください。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 移行セットへの入力 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="移行セットの追加"
>abstract="移行セットを作成したら、AEM as a Cloud Service 環境に移行する必要がある、ソースインスタンスのコンテンツを入力する必要があります。これを行うには、ソースインスタンスにコンテンツトランスファーツールをインストールする必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=ja" text="コンテンツの抽出"

Cloud Acceleration Manager で作成した移行セットを設定するには、最新バージョンのコンテンツトランスファーツールをソースの Adobe Experience Manager（AEM）インスタンスにインストールします。移行セットの設定方法については、この節に従ってください。

1. 移行元の Adobe Experience Manager インスタンスに最新バージョンのコンテンツトランスファーツールをインストールしたら、**運用 - コンテンツ移行**&#x200B;に移動します。

1. 「**移行セットを作成**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 先ほど CAM からコピーした抽出キーを、**移行セットを作成**&#x200B;フォームの抽出キー入力フィールドに貼り付けます。これを実行すると、「移行セット名」フィールドと「Cloud Acceleration Manager（CAM）プロジェクト名」フィールドに自動的に値が入力されます。これらは、CAM の移行セット名と、作成した CAM プロジェクト名に一致する必要があります。コンテンツのパスを追加できるようになりました。コンテンツのパスを追加したら、移行セットを保存します。抽出は、含めるバージョンまたは除外するバージョンで実行できます。

   >[!NOTE]
   >
   >抽出キーが有効で、有効期限に近づいていないことを確認します。抽出キーを貼り付けた後、この情報は、**移行セットを作成**&#x200B;ダイアログに表示されます。接続エラーが発生した場合は、[ソース環境の接続性](#source-environment-connectivity)を参照してください。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. 次に、移行セットを作成するには、次のパラメータを選択します。

   1. **バージョンを含める**： 必要に応じて選択します。バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

      ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツトランスファーツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。

      >[!NOTE]
      >CTT バージョン（3.0.24）以降、コンテンツトランスファーツールに新機能が含まれ、パスの包含および除外プロセスが強化されました。以前は、パスを 1 つずつ選択する必要があり、面倒で時間がかかっていました。現在は、ユーザーは環境設定に応じて、UI から直接パスを含めたり、CSV ファイルをアップロードしたりできます。CSV ファイルでは、行ごとに 1 つのパスを指定し、コンマを使用しないでください。

   1. **含めるパス**： パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、タイピングまたは選択による入力を受け付けます。ユーザーは、UI から、または CSV ファイルをアップロードすることによって、パスを含めるオプションを 1 つだけ選択できます。
      >[!IMPORTANT]
      >移行セットの作成時には、次のパスは制限されます。
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc`（`/etc` の一部のパスは CTT で選択できます）

      ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. パスの選択のみが許可され、1 つ以上のパスが存在する必要があります。パスを選択していない場合は、サーバーエラーが発生します。

         ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. **CSV アップロードオプション**&#x200B;を使用する場合、CSV ファイルに有効なパスが含まれている必要があります。

         ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. パスピッカーに戻すには、ユーザーはページを更新して最初からやり直す必要があります。

      1. アップロードした CSV に&#x200B;**無効なパス**&#x200B;が見つかった場合、別のダイアログに無効なパスが表示されます。

         ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. ユーザーは CSV ファイルを修正して再びアップロードするか、UI を更新して、パスピッカーでパスを選択する必要があります。

   1. **除外するパス**：新機能を使用すると、ユーザーは特定のパスを含めない場合に除外できます。例えば、include セクションのパスが /content/dam の場合、ユーザーは /content/dam/catalogs などのパスを除外できるようになりました。

      ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. **移行セットを作成**&#x200B;画面のすべてのフィールドを入力したら、「**保存**」をクリックします。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 移行セットのサイズの決定 {#migration-set-size}

移行セットを作成した後、抽出プロセスを開始する前に、移行セットに対してサイズ確認を実行することを強くお勧めします。
移行セットに対してサイズ確認を実行すると、以下が可能になります。

* 抽出を正常に完了できるだけの十分なディスク容量が `crx-quickstart` サブディレクトリにあるかどうかを確認します。
* 移行セットのサイズが製品の制限内に収まるかどうかを判断し、コンテンツの取り込みに失敗しないようにします。

サイズ確認を実行するには、次の手順に従います。

1. 移行セットを選択し、「**サイズを確認**」をクリックします。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. **サイズを確認**&#x200B;ダイアログが開きます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. 「**サイズを確認**」をクリックして、プロセスを開始します。移行セットリスト表示に戻り、**サイズ確認**&#x200B;が実行中であることを示すメッセージが表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. **サイズ確認**&#x200B;プロセスが完了したら、ステータスが&#x200B;**完了**&#x200B;に変わります。同じ移行セットを選択し、「**サイズを確認**」をクリックして結果を表示します。以下は、警告を含まない&#x200B;**サイズ確認**&#x200B;結果の例です。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. **サイズ確認**&#x200B;の結果、空きディスク容量が不足しているか、移行セットが製品の制限を超えていることがわかった場合は、**警告**&#x200B;ステータスが表示されます。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 次の手順 {#whats-next}

移行セットの作成方法を理解したら、コンテンツトランスファーツールでの抽出プロセスと取り込みプロセスについて学ぶ準備が整います。これらのプロセスを学ぶ前に、コンテンツを AEM as a Cloud Service に移行するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮する[大規模なコンテンツリポジトリの処理](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)を参照する必要があります。
