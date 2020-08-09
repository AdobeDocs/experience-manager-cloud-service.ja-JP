---
title: デジタルアセットの使用および共有に関するレポートです。
description: デジタルアセットの使用状況、アクティビティ、共有 [!DNL Adobe Experience Manager Assets] を理解するのに役立つ、アセットに関するレポートです。
contentOwner: AG
translation-type: tm+mt
source-git-commit: ab9a3bfa3536e25243e9752f9f034e31a57e136c
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 51%

---


# アセットレポート {#asset-reports}

アセットレポートを使用すると、 [!DNL Adobe Experience Manager Assets] 導入のユーティリティを評価できます。 を使用 [!DNL Assets]すると、デジタルアセットに関する様々なレポートを生成できます。 レポートでは、システムの使用状況、ユーザーによるアセットの操作方法、ダウンロードされたアセットや共有されているアセットなどに関する有用な情報が提供されます。

Use the information in the reports to derive key success metrics to measure the adoption of [!DNL Assets] within your enterprise and by customers.

The [!DNL Assets] reporting framework uses [!DNL Sling] jobs to asynchronously process report requests in an ordered manner. このフレームワークは大規模なリポジトリに合わせて拡張することができます。レポートの非同期処理により、レポートを生成する際の効率性とスピードが向上します。

直観的なレポート管理インターフェイスに備わっているきめ細かなオプションやコントロールを使用すれば、アーカイブされたレポートにアクセスしたり、レポートの実行ステータス（成功、失敗および待機中）を表示したりすることができます。

レポートが生成されると、インボックス通知<!-- through an email (optional) and -->で通知されます。それまでに生成されたすべてのレポートが示されるレポートリストページで、レポートの表示、ダウンロードまたは削除をおこなうことができます。

## レポートの生成 {#generate-reports}

[!DNL Experience Manager Assets] は、次の標準レポートを生成します。

* アップロード
* ダウンロード
* 有効期限
* 変更
* 公開
* [!DNL Brand Portal] publish
* ディスク使用量
* ファイル
* リンク共有

[!DNL Adobe Experience Manager] 管理者は、これらのレポートを手軽に生成し、実装に合わせて容易にカスタマイズできます。レポートを生成するには、以下の手順に従います。

1. インター [!DNL Experience Manager] フェイスで、 **[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL レポートをクリックします]**。

   ![アセットレポートに移動するツールページ](assets/navigation.png)

1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.
1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.

   ![レポートタイプの選択](assets/choose_report.png)

   >[!NOTE]
   >
   >「**[!UICONTROL ダウンロードされたアセット]**」レポートを生成する前に、Asset Download サービスが有効になっていることを確認してください。Web コンソール（`https://[aem_server]:[port]/system/console/configMgr`）で、「**[!UICONTROL Day CQ DAM Event Recorder]**」設定を開き、「イベントタイプ」で「**[!UICONTROL ダウンロードされたアセット（ダウンロード済み）]**」オプションを選択します（まだ選択されていない場合）。

   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the Asset [!UICONTROL Download] report. 適切なオプションを選択して、リンク共有のレポートを作成するか、ダウンロードレポートからコンテンツフラグメントを除外します。

   >[!NOTE]
   >
   >[!UICONTROL ダウンロード] レポートには、個別に選択した後、またはクイックアクションを使用してダウンロードされたアセットの詳細のみが表示されます。 ただし、ダウンロードしたフォルダー内のアセットの詳細は含まれません。

1. タイトル、説明、サムネール、CRX リポジトリ内のフォルダーパス（レポートの保存場所）など、レポートの詳細を設定します。By default, the folder path is `/content/dam`. 別のパスを指定することもできます。

   ![レポートの詳細を追加するページ](assets/report_configuration.png)

   レポートの日付範囲を選択します。

   レポートを今すぐ生成するか、将来の日時に生成するかを選択できます。

   >[!NOTE]
   >
   >レポートを後でスケジュールする場合は、「日付と時間」フィールドで日時を必ず指定してください。 値を指定しなかった場合、レポートエンジンはそのレポートをすぐに生成するものとして取り扱います。

   設定フィールドは、作成するレポートのタイプによって異なることがあります。例えば、「**[!UICONTROL ディスク使用量]**」レポートには、アセットが使用しているディスク領域を計算する際にアセットレンディションを含めるオプションが用意されています。ディスク使用量を計算するために、サブフォルダー内のアセットを含めるか、除外するかを選択できます。

   >[!NOTE]
   >
   >「**[!UICONTROL ディスク使用量]**」レポートには、現在のディスク領域使用量のみが示されます。そのため、日付範囲のフィールドはありません。

   ![ディスク使用量レポートの詳細ページ](assets/disk_usage_configuration.png)

   When you create the **[!UICONTROL Files]** report, you can include/exclude sub-folders. ただし、このレポートの場合、アセットレンディションを含めることはできません。

   ![ファイルレポートの詳細ページ](assets/files_report.png)

   The **[!UICONTROL Link Share]** report displays URLs to assets that are shared with external users from within [!DNL Assets]. <!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. -->列をカスタマイズすることはできません。

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![リンク共有レポートの詳細ページ](assets/link_share.png)

1. Click **[!UICONTROL Next]** from the toolbar.

1. **[!UICONTROL 列を構成]**&#x200B;ページでは、いくつかの列がデフォルトでレポートに表示されるように選択されています。さらに列を選択できます。 選択されている列の選択を解除すると、その列はレポートから除外されます。

   ![レポート列の選択または選択解除](assets/configure_columns.png)

   To display a custom column name or property path, configure the properties for the asset binary under the `jcr:content` node in CRX. または、プロパティパスピッカーを使用してパスを追加します。

   ![レポート列の選択または選択解除](assets/custom_columns.png)

1. Click **[!UICONTROL Create]** from the toolbar. レポートの生成が開始されたことを通知するメッセージが表示されます。
1. On the [!UICONTROL Asset Reports] page, the report generation status is based on the current state of the report job, for example [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued], or [!UICONTROL Scheduled]. 通知インボックスにも同じステータスが表示されます。レポートページを表示するには、レポートのリンクをクリックします。 Alternatively, select the report, and click **[!UICONTROL View]** from the toolbar.

   ![生成されたレポート](assets/report_page.png)

   Click **[!UICONTROL Download]** from the toolbar to download the report in CSV format.

## カスタム列の追加 {#add-custom-columns}

次のレポートにカスタム列を追加し、独自の要件に応じてさらに多くのデータを表示することができます。

* アップロード
* ダウンロード
* 有効期限
* 変更
* 公開
* [!DNL Brand Portal] publish
* ファイル

これらのレポートにカスタム列を追加するには、次の手順に従います。

1. で、 [!DNL Manager interface]ツール **[!UICONTROL /]** アセット **[!UICONTROL /]** レポートをクリックします ****。
1. On the [!UICONTROL Asset Reports] page, click **[!UICONTROL Create]** from the toolbar.

1. From the **[!UICONTROL Create Report]** page, choose the report you want to create and click **[!UICONTROL Next]**.
1. 必要に応じて、タイトル、説明、サムネール、フォルダーパス、日付範囲などのレポートの詳細を設定します。

1. カスタム列を表示するには、「**[!UICONTROL カスタム列]**」で列の名前を指定します。

   ![レポートのカスタム列の名前を指定](assets/custom_columns-1.png)

1. プロパティパスピッカーを使用して、CRXDE の `jcr:content` ノード下にプロパティパスを追加します。または、プロパティパスフィールドにパスを入力します。

   ![jcr:content内のパスからプロパティパスをマップします。](assets/property_picker.png)

   To add more custom columns, click **[!UICONTROL Add]** and repeat steps 5 and 6.

1. Click **[!UICONTROL Create]** from the toolbar. レポートの生成が開始されたことを通知するメッセージが表示されます。

## パージサービスの設定 {#configure-purging-service}

不要になったレポートを削除するには、数量や経過日数に基づいて既存のレポートをパージするように、Web コンソールで DAM レポートパージサービスを設定します。

1. `https://[aem_server]:[port]/system/console/configMgr` で Web コンソール（設定マネージャー）にアクセスします。
1. 「**[!UICONTROL DAM Report Purge Service]**」設定を開きます。
1. `scheduler.expression.name` フィールドでパージサービスの頻度（時間間隔）を指定します。レポートの経過日数および数量のしきい値を設定することもできます。
1. 変更内容を保存します。
