---
title: アセットレポート
description: この記事では、AEM Assets 内のアセットに関する様々なレポートとレポートの生成方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# アセットレポート {#asset-reports}

アセットレポートは、Adobe Experience Manager（AEM）Assets デプロイメントのユーティリティを評価するための重要なツールです。AEM Assets では、デジタルアセットに関する様々なレポートを生成できます。レポートでは、システムの使用状況、ユーザーによるアセットの操作方法、ダウンロードされたアセットや共有されているアセットなどに関する有用な情報が提供されます。

レポート内の情報を使用して主要な成功指標を導き出し、企業内および顧客によるAEM Assetの採用を測定します。

AEM Assets のレポートフレームワークでは、Sling ジョブを利用して、レポートの要求が順序立てて非同期的に処理されます。このフレームワークは大規模なリポジトリに合わせて拡張することができます。レポートの非同期処理により、レポートを生成する際の効率性とスピードが向上します。

直観的なレポート管理インターフェイスに備わっているきめ細かなオプションやコントロールを使用すれば、アーカイブされたレポートにアクセスしたり、レポートの実行ステータス（成功、失敗および待機中）を表示したりすることができます。

レポートが生成されると、電子メール（オプション）とインボックスで通知を受け取ります。それまでに生成されたすべてのレポートが示されるレポートリストページで、レポートの表示、ダウンロードまたは削除をおこなうことができます。

## レポートの生成 {#generate-reports}

AEM Assets では、次の標準レポートが生成されます。

* アップロード
* ダウンロード
* 有効期限
* 変更
* 公開
* Brand Portal 公開
* ディスク使用量
* ファイル
* リンク共有

AEM 管理者は、これらのレポートを手軽に生成し、実装に合わせて容易にカスタマイズできます。レポートを生成するには、以下の手順に従います。

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.

   ![ナビゲーション](assets/navigation.png)

1. In the Asset Reports page, tap/click **[!UICONTROL Create]** from the toolbar.
1. **[!UICONTROL レポートを作成]**&#x200B;ページで、作成するレポートを選択し、「**[!UICONTROL 次へ]**」をタップまたはクリックします。

   ![choose_report](assets/choose_report.png)

   >[!NOTE]
   >
   >「**[!UICONTROL ダウンロードされたアセット]**」レポートを生成する前に、Asset Download サービスが有効になっていることを確認してください。From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.

   >[!NOTE]
   >
   >デフォルトで、「ダウンロードされたアセット」レポートにはコンテンツフラグメントとリンク共有が含まれています。適切なオプションを選択して、リンク共有のレポートを作成するか、ダウンロードレポートからコンテンツフラグメントを除外します。

1. タイトル、説明、サムネール、CRX リポジトリ内のフォルダーパス（レポートの保存場所）など、レポートの詳細を設定します。By default, the folder path is */content/dam*. 別のパスを指定することもできます。

   ![report_configuration](assets/report_configuration.png)

   レポートの日付範囲を選択します。

   レポートを今すぐ生成するか、将来の日時に生成するかを選択できます。

   >[!NOTE]
   >
   >レポートを後で生成するようにスケジュールする場合は必ず、「日時」フィールドで日付と時刻を指定してください。値を指定しなかった場合、レポートエンジンはそのレポートをすぐに生成するものとして取り扱います。

   設定フィールドは、作成するレポートのタイプによって異なることがあります。

   例えば、「**[!UICONTROL ディスク使用量]**」レポートには、アセットが使用しているディスク領域を計算する際にアセットレンディションを含めるオプションが用意されています。ディスク使用量を計算するために、サブフォルダー内のアセットを含めるか除外するかを選択できます。

   >[!NOTE]
   >
   >「**[!UICONTROL ディスク使用量]**」レポートには、現在のディスク領域使用量のみが示されます。そのため、日付範囲のフィールドはありません。

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   「**[!UICONTROL ファイル]**」レポートを作成する場合は、サブフォルダーを含めるか除外するかを選択できます。ただし、このレポートの場合、アセットレンディションを含めることはできません。

   ![files_report](assets/files_report.png)

   「**[!UICONTROL リンク共有]**」レポートには、AEM Assets 内から外部ユーザーと共有されているアセットへの URL が表示されます。アセットを共有したユーザーの電子メール ID、アセットを共有しているユーザーの電子メール ID、共有の日付、リンクの有効期限なども表示されます。列をカスタマイズすることはできません。

   The **[!UICONTROL Link Share]** report, does not include options for subfolders and renditions because it merely publishes the shared URLs that appear under */var/dam/share*.

   ![link_share](assets/link_share.png)

1. ツールバーの「**[!UICONTROL 次へ]**」をタップまたはクリックします。

1. **[!UICONTROL 列を構成]**&#x200B;ページでは、いくつかの列がデフォルトでレポートに表示されるように選択されています。追加の列を選択できます。選択されている列の選択を解除すると、その列はレポートから除外されます。

   ![configure_columns](assets/configure_columns.png)

   カスタム列名またはプロパティパスを表示するには、CRXのjcr:contentノードの下にアセットバイナリのプロパティを設定します。 または、プロパティパスピッカーを使用して追加します。

   ![custom_columns](assets/custom_columns.png)

1. Tap/click **[!UICONTROL Create]** from the toolbar. レポートの生成が開始されたことを通知するメッセージが表示されます。
1. アセットレポートページでは、レポート生成ステータスは、成功、失敗、キュー、スケジュール済みなど、レポートジョブの現在の状態に基づきます。 同じステータスが通知インボックスにも表示されます。

   レポートページを表示するには、レポートのリンクをタップまたはクリックします。または、レポートを選択し、ツールバーの「表示」アイコンをタップまたはクリックします。

   ![report_page](assets/report_page.png)

   ツールバーの「ダウンロード」アイコンをタップまたはクリックすると、レポートを CSV 形式でダウンロードできます。

## カスタム列の追加 {#add-custom-columns}

次のレポートにカスタム列を追加し、独自の要件に応じてさらに多くのデータを表示することができます。

* アップロード
* ダウンロード
* 有効期限
* 変更
* 公開
* Brand Portal 公開
* ファイル

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Reports]**.
1. In the Asset Reports page, tap/click **[!UICONTROL Create]** from the toolbar.

1. **[!UICONTROL レポートを作成]**&#x200B;ページで、作成するレポートを選択し、「**[!UICONTROL 次へ]**」をタップまたはクリックします。
1. タイトル、説明、サムネール、フォルダーパス、日付範囲など、該当するレポートの詳細を設定します。

1. To display a custom column, specify the name of the column in under **[!UICONTROL Custom Columns]**.

   ![custom_columns-1](assets/custom_columns-1.png)

1. Add the property path under the `jcr:content` node in CRXDE using the property path picker.

   ![property_picker](assets/property_picker.png)

   または、プロパティパスフィールドにパスを入力します。

   ![property_path](assets/property_path.png)

   カスタム列をさらに追加するには、「**[!UICONTROL 追加]**」をタップまたはクリックし、手順 5 および 6 を繰り返します。

1. Tap/click **[!UICONTROL Create]** from the toolbar. レポートの生成が開始されたことを通知するメッセージが表示されます。

## パージサービスの設定 {#configure-purging-service}

不要になったレポートを削除するには、数量や経過日数に基づいて既存のレポートをパージするように、Web コンソールで DAM レポートパージサービスを設定します。

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. レポートの経過日数および数量のしきい値を設定することもできます。
1. 変更内容を保存します。
