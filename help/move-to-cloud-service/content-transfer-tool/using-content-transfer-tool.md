---
title: コンテンツ転送ツールの使用
description: コンテンツ転送ツールの使用
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 2f811c5c6ccbb1d05aa1825dd110e0c9d5e6b219
workflow-type: tm+mt
source-wordcount: '3063'
ht-degree: 86%

---

# コンテンツ転送ツールの使用 {#using-content-transfer-tool}

## コンテンツ転送ツール使用時の重要な考慮事項 {#pre-reqs}

コンテンツ転送ツールを実行する際には、次の重要事項を考慮してください。

* コンテンツ転送ツールに必要なシステム構成は、AEM 6.3 以降と Java 8 です。使用している AEM のバージョンがこれより古い場合、コンテンツ転送ツールを使用するには、コンテンツリポジトリーを AEM 6.5 にアップグレードする必要があります。

* AEM を開始するユーザーが `java` コマンドを実行できるように、AEM 環境上で Java を設定する必要があります。

* バージョン 1.3.0 のインストール時には、コンテンツ転送ツールのアーキテクチャが大きく変更されているため、旧バージョンのツールをアンインストールすることをお勧めします。また、1.3.0 では、新しい移行セットを作成し、その新しい移行セットで抽出と取り込みを再実行してください。

* コンテンツ転送ツールは、ファイルデータストア、S3 データストア、共有 S3 データストア、Azure Blob Store データストアと共に使用できます。

* *サンドボックス環境*&#x200B;を使用している場合は、環境が最新で最新のリリースにアップグレードされていることを確認してください。*実稼動環境*&#x200B;を使用している場合、環境は自動的に更新されます。

* コンテンツ転送ツールを使用するユーザーは、ソースインスタンスの管理者で、かつ、コンテンツ転送先の Cloud Service インスタンスのローカルの AEM **administrators** グループに属している必要があります。権限のないユーザーは、コンテンツ転送ツールを使用するアクセストークンを取得できません。

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。CTT のアクセストークンを取得するには、ユーザーを **administrators** グループに再度追加する必要があります。

* アクセストークンは、特定の期間の後、または Cloud Service 環境のアップグレード後に、定期的に期限切れになる場合があります。アクセストークンの有効期限が切れると、Cloud Service インスタンスに接続できなくなり、新しいアクセストークンを取得する必要があります。既存の移行セットに関連付けられているステータスアイコンが赤の雲アイコンに変わり、その上にカーソルを置くとメッセージが表示されます。

* コンテンツ転送ツール（CTT）は、ソースインスタンスからターゲットインスタンスにコンテンツを転送する前に、どのような種類のコンテンツ分析も実行しません。例えば、CTT では、コンテンツをパブリッシュ環境に取り込む際に、公開済みコンテンツと非公開コンテンツを区別しません。移行セットで指定されているコンテンツは何であれ、選択したターゲットインスタンスに取り込まれます。オーサーインスタンスとパブリッシュインスタンスのどちらか一方または両方に移行セットを取り込むことができます。コンテンツを実稼動インスタンスに移動する際は、ソースオーサーインスタンスに CTT をインストールしてコンテンツをターゲットオーサーインスタンスに移動し、同様に、ソースパブリッシュインスタンスに CTT をインストールしてコンテンツをターゲットパブリッシュインスタンスに移動することをお勧めします。

* コンテンツ転送ツールによって転送されるユーザーとグループは、権限を満たすためにコンテンツで必要なものに限られます。*抽出*&#x200B;プロセスでは、`/home` 全体を移行セットにコピーし、*取り込み*&#x200B;プロセスでは、移行されたコンテンツ ACL で参照されているすべてのユーザーおよびグループをコピーします。既存のユーザーやグループを IMS ID に自動的にマッピングする場合は、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#cloud-migration)を参照してください。

* 抽出段階では、コンテンツ転送ツールはアクティブな AEM ソースインスタンスで実行されます。

* コンテンツ転送プロセスの&#x200B;*抽出*&#x200B;段階が完了したら、*取り込み段階*&#x200B;を開始してコンテンツを AEM as a Cloud Service の&#x200B;*ステージング*&#x200B;インスタンスまたは&#x200B;*実稼働*&#x200B;インスタンスに取り込む前に、サポートチケットを申請して、*取り込み*&#x200B;を実行する意図をアドビに知らせる必要があります。それにより、アドビは、*取り込み*&#x200B;プロセス中に中断が発生しないようにすることができます。予定している&#x200B;*取り込み*&#x200B;日の 1 週間前にサポートチケットを申請する必要があります。サポートチケットを申請したら、サポートチームから、次の手順に関するガイダンスが提供されます。次の詳細を含むサポートチケットをログに記録できます。

   * *取り込み*&#x200B;段階の開始を予定している正確な日付と大体の時刻（およびタイムゾーン）
   * データの取り込み先として予定している環境のタイプ（ステージングまたは実稼働）
   * プログラム ID

* オーサーの&#x200B;*取得段階*&#x200B;では、オーサーのデプロイメント全体がスケールダウンされます。つまり、オーサー AEM インスタンスは、インジェストプロセス全体で使用できなくなります。また、*取り込み*&#x200B;段階の実行中に Cloud Manager パイプラインが実行されないようにしてください。

* ソース AEM システム上のデータストアとして `Amazon S3` または `Azure` を使用する場合は、保存された BLOB を削除（ガベージコレクション）できないように、データストアを設定する必要があります。これにより、インデックスデータの整合性が確保されます。このように設定しないと、このインデックスデータの整合性が欠落しているために抽出が失敗する可能性があります。

* カスタムインデックスを使用する場合は、コンテンツ転送ツールを実行する前に、`tika` ノードでカスタムインデックスを設定する必要があります。詳細は、「[新しいインデックス定義の準備](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#preparing-the-new-index-definition)」を参照してください。

* 追加を行う場合は、最初の抽出を実行した時点からに対して、既存のコンテンツのコンテンツ構造を変更しないことが重要です。 最初の抽出以降に構造が変更されたコンテンツに対しては、追加は実行できません。 移行プロセス中は、必ずこの制限をおこなってください。

## 入手方法 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="ダウンロード"
>abstract="コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="リリースノート"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="ソフトウェア配布ポータル"

コンテンツ転送ツールは、ソフトウェア配布ポータルから zip ファイルとしてダウンロードできます。パッケージマネージャーを使用して、このパッケージをソース AEM（Adobe Experience Manager）インスタンスにインストールできます。最新バージョンをダウンロードしてください。最新バージョンの詳細については、「[リリースノート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)」を参照してください。

>[!NOTE]
>[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からコンテンツ転送ツールをダウンロードします。

## コンテンツ転送ツールの実行 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="コンテンツ転送ツールの実行"
>abstract="この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" デモを見る"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=ja#migration" text="チュートリアル - コンテンツ転送ツールの使用"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


この節では、コンテンツ転送ツールを使用してコンテンツを AEM as a Cloud Service（オーサー／パブリッシュ）に移行する方法について説明します。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ移行**&#x200B;に移動します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. **コンテンツ移行**&#x200B;ウィザードから「**コンテンツ転送**」オプションを選択します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. 最初の移行セットを作成すると、次のコンソールが表示されます。「**移行セットを作成**」をクリックして、新しい移行セットを作成します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >既存の移行セットがある場合、コンソールには既存の移行セットのリストが表示され、現在のステータスが表示されます

   さらに、「**ユーザーマッピング設定を作成**」をクリックして、[ユーザーマッピングツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool)にアクセスします。

1. **移行セットを作成**&#x200B;画面の各フィールドに、以下のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **名前**：移行セットの名前を入力します。
      >[!NOTE]
      >移行セット名には特殊文字を使用できません。

   1. **クラウドサービス設定**：移行先の AEM as a Cloud Service オーサーの URL を入力します。

      >[!NOTE]
      >コンテンツ転送をおこなう際は、一度に最大 10 個の移行セットを作成し維持管理できます。
      >さらに、特定の環境（*ステージング*、*開発*、*実稼動*&#x200B;のいずれか）ごとに個別に移行セットを作成する必要があります。

   1. **アクセストークン**：アクセストークンを入力します。

      >[!NOTE]
      >「**アクセストークンを開く**」ボタンを使用してアクセストークンを取得できます。ターゲット Cloud Service インスタンスの AEM 管理者グループに属していることを確認する必要があります。

   1. **パラメーター**：移行セットを作成するには、次のパラメータを選択します。

      1. **バージョンを含める**：必要に応じて選択します。

      1. **IMS ユーザーおよびグループからのマッピングを含める**：IMS ユーザーおよびグループからのマッピングを含める場合は、このオプションを選択します。
詳しくは、[ユーザーマッピングツール](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja)を参照してください。

      1. **含めるパス**：パスブラウザーを使用して、移行する必要があるパスを選択します。パスピッカーは、キーボード入力または選択による入力を受け付けます。

         >[!IMPORTANT]
         >移行セットの作成時には、次のパスは制限されます。
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`（`/etc` の一部のパスは CTT で選択できます）


1. **移行セットを作成**&#x200B;画面のすべてのフィールドに値を入力したら、「**保存**」をクリックします。

1. 移行セットが&#x200B;*概要*&#x200B;ページに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   既存のすべての移行セットが、現在のステータスなどのステータス情報と共に&#x200B;*概要*&#x200B;ページに表示されます。以下に示すアイコンの一部が表示されます。

   * *赤い雲*&#x200B;は、抽出プロセスを完了できないことを示しています。
   * *緑色の雲*&#x200B;は、抽出プロセスを完了できることを示しています。
   * *黄色のアイコン*&#x200B;は、その既存の移行セットが同じインスタンス内の他のユーザーによって作成されたことを示しています。

1. 概要ページで移行セットを選択し、「**プロパティ**」をクリックして、移行セットのプロパティを表示または編集します。プロパティの編集中は、コンテナ名またはサービス URL を変更できません。


### コンテンツ転送の抽出プロセス {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="コンテンツの抽出"
>abstract="抽出とは、ソース AEM インスタンスから、移行セットと呼ばれる一時領域にコンテンツを抽出することです。移行セットは、アドビが提供するクラウドストレージ領域で、ソース AEM インスタンスと AEM as a Cloud Service インスタンスの間で転送されるコンテンツを一時的に保存するためのものです。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="追加抽出"

コンテンツ転送ツールで移行セットを抽出するには、次の手順に従います。
>[!NOTE]
>Amazon S3またはAzureデータストアをデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、抽出段階を大幅に高速化できます。 そのためには、抽出を実行する前に`azcopy.config`ファイルを設定する必要があります。 詳しくは、[大きなコンテンツリポジトリの処理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)を参照してください。

1. *概要*&#x200B;ページで移行セットを選択し、「**抽出**」をクリックして抽出を開始します。**移行セットの抽出**&#x200B;ダイアログボックスが表示されるので、「**抽出**」をクリックして抽出段階を完了します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >抽出段階では、ステージングコンテナを上書きするオプションがあります。


1. 「**抽出**」フィールドに「**実行中**」ステータスが表示され、抽出が進行中であることを示します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   抽出が完了すると、移行セットのステータスが&#x200B;**完了**&#x200B;に更新され、*緑で塗りつぶされた*&#x200B;雲のアイコンが「**情報**」フィールドに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI には自動リロード機能があり、30 秒ごとに概要ページをリロードします。
   >抽出フェーズが開始されると、書き込みロックが作成され、*60 秒*&#x200B;後に解放されます。したがって、抽出が停止した場合は、ロックが解除されるまで 1 分待ってから、抽出を再開する必要があります。

#### 追加抽出 {#top-up-extraction-process}

コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁に行って、Cloud Service での運用を開始する前に行う最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。
>また、追加抽出を実行する際に、最初の抽出を実行した時点からに変更しないで、既存のコンテンツのコンテンツ構造を変更する必要はありません。 最初の抽出以降に構造が変更されたコンテンツに対しては、追加は実行できません。 移行プロセス中は、必ずこの制限をおこなってください。

抽出プロセスが完了したら、追加抽出方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加抽出の実行対象となる移行セットを選択します。「**抽出**」をクリックして、追加抽出を開始します。**移行セットの抽出**&#x200B;ダイアログボックスが表示されます。

   >[!IMPORTANT]
   >
   >「**抽出時にステージングコンテナを上書き**」オプションを無効にしてください。
   >
   >![画像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### コンテンツ転送のインジェストプロセス {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="コンテンツの取得"
>abstract="取得とは、移行セットからターゲット Cloud Service インスタンスにコンテンツを取り込むことです。コンテンツ転送ツールには、差分コンテンツ追加をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="追加インジェスト"

コンテンツ転送ツールで移行セットを取り込むには、次の手順に従います。
>[!NOTE]
>Amazon S3またはAzureデータストアをデータストアのタイプとして使用する場合は、オプションのプリコピー手順を実行して、インジェスト段階を大幅に高速化できます。 詳細は、[AzCopyでの取り込み](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy)を参照してください。

1. *概要*&#x200B;ページで移行セットを選択し、「**取り込み**」をクリックして取り込みを開始します。 **移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。「**取得**」をクリックして、取得段階を完了します。コンテンツをオーサーとパブリッシュに同時に取り込むことができます。

   >[!IMPORTANT]
   >プリコピーを使用した取り込みを（S3またはAzureデータストアに対して）使用する場合は、最初にオーサーの取り込みを1つで実行することをお勧めします。 これにより、後で実行する際に、パブリッシュの取り込みが高速化されます。

   >[!IMPORTANT]
   >「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。詳しくは、[コンテンツ転送ツール使用時の重要な考慮事項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=ja#pre-reqs)も参照してください。

1. 取得が完了すると、「**取得を公開**」フィールドのステータスが「**完了**」に更新されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### 追加インジェスト {#top-up-ingestion-process}

コンテンツ転送ツールには、*差分コンテンツ追加*&#x200B;をサポートする機能があります。差分追加では、前回のコンテンツ転送アクティビティ以降に加えられた変更のみを転送できます。

>[!NOTE]
>
>最初のコンテンツ転送の後は、差分コンテンツ追加を頻繁におこなって、Cloud Service での運用を開始する前におこなう最後の差分コンテンツ転送に必要なコンテンツ凍結期間を短縮することをお勧めします。

インジェストプロセスが完了したら、追加インジェスト方式を使用して差分コンテンツを転送できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、追加取得の実行対象となる移行セットを選択します。「**取得**」をクリックして、追加取得を開始します。**移行セットのインジェスト**&#x200B;ダイアログボックスが表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   >[!IMPORTANT]
   >以前の取得アクティビティから既存のコンテンツを削除しないようにするには、「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションを無効にする必要があります。さらに、「**カスタマーケア**」をクリックしてチケットを発行します（上図を参照）。


### 移行セットのログの表示 {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="ログの表示"
>abstract="取得の抽出が完了したら、エラーや警告がないかログを確認します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="トラブルシューティング"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="アドビサポートのご案内"

各ステップ（抽出と取り込み）が完了したら、ログを確認してエラーを探します。エラーが発生した場合は、報告された問題を解決するかアドビサポートに連絡して、即座に対処してください。

既存の移行セットのログを&#x200B;*概要*&#x200B;ページから表示できます。それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、ログを表示する移行セットを選択し、アクションバーの「**ログを表示**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. **ログ**&#x200B;ダイアログボックスが表示されます。「**抽出ログ**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
または、

   *概要*&#x200B;画面から移行セットのログを直接表示することもできます。移行セットを選択し、「**抽出**」フィールド内のステータスをクリックします。下図の場合は、「**完了**」をクリックすると、ログが新しいタブに表示されます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. ユーザーインターフェイスを使用せずにログの末尾を表示するには、ソース AEM 環境に SSH で接続し、`crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`で tail コマンドを実行します。

### 移行セットの削除 {#deleting-migration-set}

*概要*ページで移行セットを削除できます。
それには、次の手順に従います。

1. *概要*&#x200B;ページに移動し、削除する移行セットを選択し、アクションバーの「**削除**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. **移行セットを削除**&#x200B;ダイアログボックスの「**削除**」をクリックして、削除を確定します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)


## パブリッシュインスタンスでのコンテンツ転送ツールの実行 {#running-ctt-on-publish}

コンテンツをパブリッシュインスタンスに移動する際に、CTTをソースパブリッシュインスタンスにインストールして、コンテンツをターゲットパブリッシュインスタンスに移動することをお勧めします。 次に説明する推奨されるアプローチに従います。

* オーサーインスタンスで使用したのと同じバージョンのCTTを使用します。

* 移行する必要があるのは、1つのパブリッシュノードのみです。 抽出を開始する前に、ロードバランサーから削除する必要があります。

* 移行セットを作成する場合は、オーサーAEMaCS環境のURLを使用します。

* パブリッシュへのインジェスト中、パブリッシュ層は（オーサーとは異なり）スケールダウンされません。 予防措置として、次のようなユーザーが開始する書き込み操作は避けてください。

   * AEMaCSオーサーからその環境のパブリッシュへのコンテンツの配布
   * パブリッシュインスタンス間のユーザー同期


## トラブルシューティング {#troubleshooting}

### 不明な BLOB ID {#missing-blobs}

以下に示すように、不明な BLOB ID が報告された場合は、既存のリポジトリーで整合性チェックを実行し、不明な BLOB を復元する必要があります。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

以下のコマンドを実行します。

>[!NOTE]
>
>`--verbose` フラグが必要なのは、BLOB の参照元ノードのパスを報告するためです。

**AEM 6.5（Oak 1.8 以前）のリポジトリーの場合**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Oak 1.10 以降のリポジトリーの場合**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

詳しくは、[Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)（Oak 実行可能 Jar）を参照してください。

整合性チェックのために上記で指定された *OUT_DIR* に作成されたファイルを調べて、不明なバイナリのパスや必要なアクション（バックアップからの復元、パスの削除、インデックスの再作成など）を確認できます。


### UI の動作 {#ui-behavior}

コンテンツ転送ツールのユーザーインターフェイス（UI）に次のような動作が見られることがあります。

* コンテンツ転送ツール UI のアイコンが、このガイドに示すスクリーンショットとは異なって表示される場合や、ソース AEM インスタンスのバージョンによっては表示されない場合があります。
