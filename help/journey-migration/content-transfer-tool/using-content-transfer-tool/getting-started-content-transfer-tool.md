---
title: コンテンツ転送ツールの基本を学ぶ
description: コンテンツ転送ツールの基本を学ぶ
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: f84806c1579f8ef163dd9454fcae4a57bf22a452
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 43%

---

# コンテンツ転送ツールの基本を学ぶ {#getting-started-content-transfer-tool}


## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="ダウンロード"
>abstract="コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="リリースノート"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="ソフトウェア配布ポータル"

コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md) を使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。最新バージョンの詳細については、「[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)」を参照してください。

>[!NOTE]
>[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からコンテンツ転送ツールをダウンロードします。

## ソース環境の接続性 {#source-environment-connectivity}

>[!NOTE]
>
>移行セットが Cloud Acceleration Manager から削除されている場合も、接続エラーが発生する可能性があります。

ソース AEM インスタンスがファイアウォールの内側で動作していて、許可リストに追加された特定のホストにしか到達できない場合があります。抽出を正常に実行するには、AEM を実行しているインスタンスから、次のエンドポイントにアクセスできる必要があります。

* ターゲット AEM as a Cloud Service 環境：`author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure BLOB ストレージサービス：`*.blob.core.windows.net`
* ユーザーマッピング IO エンドポイント：`usermanagement.adobe.io`

ターゲット AEM as a Cloud Service 環境への接続をテストするには、ソースインスタンスのシェルから次の cURL コマンドを発行します（`program_id`、`environment_id` および `migration_token` を実際の値に置き換えてください）。

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>`HTTP/2 200` を受け取った場合は、AEM as a Cloud Service への接続に成功しました。

## コンテンツ転送ツールの実行 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="コンテンツ転送ツールの実行"
>abstract="この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" デモを見る"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration" text="チュートリアル - コンテンツ転送ツールの使用"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)
<!-- Need to remove the video -->

次の節は、コンテンツ転送ツールの新しいバージョンに適用されます。 この節では、コンテンツ転送ツールを使用してコンテンツをAEM as a Cloud Serviceに移行する方法について説明します。

### 抽出設定フェーズ {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="抽出設定フェーズ"
>abstract="移行セットを作成し、抽出キーをコピーする方法を説明します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="チュートリアル - コンテンツ転送ツールの使用"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. Cloud Acceleration Manager(CAM) にログインし、以前に作成した CAM プロジェクトをクリックして、AEM as a Cloud Serviceへの移行に対する準備状況を評価します。 CAM プロジェクトをまだ作成していない場合は、「CAM でのプロジェクトの作成と管理」を参照してください。

1. をクリックします。 **コンテンツ転送** カード。 これにより、移行セットのリストビューが表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 「 」をクリックして移行セットを作成 **移行セットを作成**.

   >[!NOTE]
   >
   >Cloud Acceleration Manager では、プロジェクトごとに最大 5 つの移行セットを作成できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. これで、リスト表示に移行リストが表示されます。 3 つのドット記号 (**...**) をクリックしてドロップダウンを開き、 **抽出キーをコピー**. このキーは、抽出段階で必要になります。 この抽出キーをコピーします。

   >[!NOTE]
   >
   >抽出キーを使用すると、ソースAEM環境から移行セットに安全に接続できます。 この鍵は、パスワードと同じ注意を払って扱ってください。また、電子メールのような安全でないメディアでは、鍵を共有しないでください。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 移行セットへの入力 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="移行セットの入力 abstract=&quot;移行セットを作成した後、AEMas a Cloud Service環境に移動する必要があるソースインスタンスのコンテンツを入力する必要があります。 これをおこなうには、コンテンツ転送ツールをソースインスタンスにインストールする必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="コンテンツの抽出"

Cloud Acceleration Manager で作成した移行セットを入力するには、最新バージョンのコンテンツ転送ツールをソースAdobe Experience Manager(AEM) インスタンスにインストールする必要があります。 移行セットの入力方法については、この節を参照してください。

1. ソースAdobe Experience Managerインスタンスに最新バージョン (Vxxx) のコンテンツ転送ツールをインストールしたら、に移動します。 **運用 — コンテンツ移行**

1. クリック **移行セットを作成**

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 前の CAM からコピーした抽出キーを、の抽出キー入力フィールドに貼り付けます。 **移行セットを作成** フォーム。 その後、移行セット名と Cloud Acceleration Manager(CAM) プロジェクト名フィールドが自動的に入力されます。 これらは、CAM の移行セット名と、作成した CAM プロジェクト名に一致する必要があります。 コンテンツのパスを追加できるようになりました。 コンテンツのパスを追加したら、移行セットを保存できます。 抽出は、含めるバージョンまたは除外するバージョンで実行できます。

   >[!NOTE]
   >
   >抽出キーが有効で、有効期限に近づいていないことを確認します。 この情報は、 **移行セットを作成** ダイアログを開き、抽出キーを貼り付けた後に表示されます。 接続エラーが発生した場合は、 [ソース環境の接続](#source-environment-connectivity) を参照してください。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 次に、次のパラメータを選択して移行セットを作成します。

   1. **バージョンを含める**： 必要に応じて選択します。バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

      ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツ転送ツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。


   1. **含めるパス**： パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、キーボード入力または選択による入力を受け付けます。

      >[!IMPORTANT]
      >移行セットの作成時には、次のパスは制限されます。
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc`（`/etc` の一部のパスは CTT で選択できます）


1. **移行セットを作成**&#x200B;画面のすべてのフィールドに値を入力したら、「**保存**」をクリックします。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 移行セットのサイズの決定 {#migration-set-size}

移行セットを作成した後、抽出プロセスを開始する前に、移行セットに対してサイズチェックを実行することを強くお勧めします。
移行セットでサイズチェックを実行すると、次の操作を実行できます。
* に十分なディスク容量があるかどうかを確認します。 `crx-quickstart` サブディレクトリの抽出が正常に完了しました。
* 移行セットのサイズがサポート対象の製品の制限内に収まるかどうかを判断し、コンテンツの取り込みに失敗しないようにします。

サイズチェックを実行するには、次の手順に従います。

1. 移行セットを選択し、「 」をクリックします。 **サイズを確認**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. これにより、 **サイズを確認** ダイアログ。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. クリック **サイズを確認** をクリックしてプロセスを開始します。 移行セットのリストビューに戻り、次のことを示すメッセージが表示されます。 **サイズを確認** が実行中です。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 1 回 **サイズを確認** 処理が完了した場合、ステータスは **完了**. 同じ移行セットを選択し、「 」をクリックします。 **サイズを確認** をクリックして結果を表示します。 以下は **サイズを確認** の結果は警告を含みません。

   ![画像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. この **サイズを確認** 結果は、ディスク容量が不足しているか、移行セットが製品の制限を超えているかを示します。 **警告** ステータスが表示されます。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 次の手順 {#whats-next}

移行セットの作成方法を理解したら、コンテンツ転送ツールでの抽出プロセスと取り込みプロセスについて学ぶ準備が整います。これらのプロセスを学ぶ前に、コンテンツを AEM as a Cloud Service に移行するコンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に短縮する[大規模なコンテンツリポジトリーの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)を参照する必要があります。
