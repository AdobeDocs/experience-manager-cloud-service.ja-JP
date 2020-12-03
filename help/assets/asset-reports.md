---
title: 使用状況および共有に関するレポート
description: デジタルアセットの使用状況、アクティビティ、共有を理解するのに役立つ、 [!DNL Adobe Experience Manager Assets]  でのアセットに関するレポートです。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3ee2e53268ea77949057ac18fcb4a8f8b1e01cb2
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 96%

---


# アセットレポート {#asset-reports}

アセットレポートを使用すると、 [!DNL Adobe Experience Manager Assets] デプロイメントのユーティリティを評価できます。[!DNL Assets] を使用すると、デジタルアセットに関する様々なレポートを生成できます。レポートでは、システムの使用状況、ユーザーによるアセットの操作方法、ダウンロードされたアセットや共有されているアセットなどに関する有用な情報が提供されます。

レポートの情報を使用して重要な成功指標を導き出し、企業やお客様における [!DNL Assets] の採用状況を測定することができます。

[!DNL Assets] のレポートフレームワークでは、[!DNL Sling] ジョブを利用して、レポートの要求が順序立てて非同期的に処理されます。このフレームワークは大規模なリポジトリに合わせて拡張することができます。レポートの非同期処理により、レポートを生成する際の効率性とスピードが向上します。

直観的なレポート管理インターフェイスに備わっているきめ細かなオプションやコントロールを使用すれば、アーカイブされたレポートにアクセスしたり、レポートの実行ステータス（成功、失敗および待機中）を表示したりすることができます。

レポートが生成されると、インボックス通知<!-- through an email (optional) and -->で通知されます。それまでに生成されたすべてのレポートが示されるレポートリストページで、レポートの表示、ダウンロードまたは削除をおこなうことができます。

## レポートの生成 {#generate-reports}

[!DNL Experience Manager Assets] では、次の標準レポートが生成されます。

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

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;をクリックします。

   ![アセットレポートに移動するツールページ](assets/navigation.png)

1. アセットレポートページで、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL レポートを作成]**&#x200B;ページで、作成するレポートを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![レポートタイプの選択](assets/choose_report.png)

<!-- TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

>[!NOTE]
>
>デフォルトで、アセットの[!UICONTROL ダウンロード]レポートにはコンテンツフラグメントとリンク共有が含まれています。適切なオプションを選択して、リンク共有のレポートを作成するか、ダウンロードレポートからコンテンツフラグメントを除外します。

>[!NOTE]
>
>[!UICONTROL ダウンロード]レポートには、個別に選択した後、またはクイックアクションを使用してダウンロードされたアセットの詳細のみが表示されます。ただし、ダウンロードされたフォルダー内のアセットの詳細は含まれません。

1. タイトル、説明、サムネール、CRX リポジトリ内のフォルダーパス（レポートの保存場所）など、レポートの詳細を設定します。デフォルトでは、フォルダーパスは `/content/dam` です。別のパスを指定することもできます。

   ![レポートの詳細を追加するページ](assets/report_configuration.png)

   レポートの日付範囲を選択します。

   レポートを今すぐ生成するか、将来の日時に生成するかを選択できます。

   >[!NOTE]
   >
   >レポートを後で生成するようにスケジュールする場合は必ず、「日付」フィールドと「時間」フィールドで日時を指定してください。値を指定しなかった場合、レポートエンジンはそのレポートをすぐに生成するものとして取り扱います。

   設定フィールドは、作成するレポートのタイプによって異なることがあります。例えば、「**[!UICONTROL ディスク使用量]**」レポートには、アセットが使用しているディスク領域を計算する際にアセットレンディションを含めるオプションが用意されています。ディスク使用量を計算する際にサブフォルダー内のアセットを含めるか除外するかを選択することもできます。

   >[!NOTE]
   >
   >「**[!UICONTROL ディスク使用量]**」レポートには、現在のディスク領域使用量のみが示されます。そのため、日付範囲のフィールドはありません。

   ![ディスク使用量レポートの詳細ページ](assets/disk_usage_configuration.png)

   「**[!UICONTROL ファイル]**」レポートを作成する場合は、サブフォルダーを含めるか除外するかを選択できます。ただし、このレポートの場合、アセットレンディションを含めることはできません。

   ![ファイルレポートの詳細ページ](assets/files_report.png)

   「**[!UICONTROL リンク共有]**」レポートには、[!DNL Assets] 内から外部ユーザーと共有されているアセットへの URL が表示されます。<!-- It includes email ids of the user who shared the assets, emails ids of users with which the assets are shared, share date, and expiration date for the link. -->列をカスタマイズすることはできません。

   「**[!UICONTROL リンク共有]**」レポートでは、`/var/dam/share` に表示される共有 URL が公開されるだけです。そのため、サブフォルダーやレンディションに関するオプションは用意されていません。

   ![リンク共有レポートの詳細ページ](assets/link_share.png)

1. ツールバーから「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 列を構成]**&#x200B;ページでは、いくつかの列がデフォルトでレポートに表示されるように選択されています。追加の列を選択できます。選択されている列の選択を解除すると、その列はレポートから除外されます。

   ![レポート列の選択または選択解除](assets/configure_columns.png)

   カスタムの列名やプロパティパスを表示するには、CRX のノード下のアセットバイナリのプロパティを設定します。`jcr:content`または、プロパティパスピッカーを使用してパスを追加します。

   ![レポート列の選択または選択解除](assets/custom_columns.png)

1. ツールバーから「**[!UICONTROL 作成]**」をクリックします。レポートの生成が開始されたことを通知するメッセージが表示されます。
1. [!UICONTROL アセットレポート]ページのレポート生成ステータスはジョブの現在の状態（「[!UICONTROL 成功]」「[!UICONTROL 失敗]」「[!UICONTROL キューに追加済み]」、「[!UICONTROL スケジュール済み]」など）に基づきます。通知インボックスにも同じステータスが表示されます。レポートページを表示するには、レポートのリンクをクリックします。または、レポートを選択し、ツールバーの「**[!UICONTROL 表示]**」をクリックします。

   ![生成されたレポート](assets/report_page.png)

   ツールバーの「**[!UICONTROL ダウンロード]**」をクリックすると、レポートを CSV 形式でダウンロードできます。

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

1. [!DNL Manager interface] で、 **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;をクリックします 。
1. アセットレポートページで、ツールバーの「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL レポートを作成]**&#x200B;ページで、作成するレポートを選択し、「**[!UICONTROL 次へ]**」をクリックします。
1. タイトル、説明、サムネール、フォルダーパス、期間など、該当するレポートの詳細を設定します。

1. カスタム列を表示するには、「**[!UICONTROL カスタム列]**」で列の名前を指定します。

   ![レポートのカスタム列の名前を指定](assets/custom_columns-1.png)

1. プロパティパスピッカーを使用して、CRXDE の `jcr:content` ノード下にプロパティパスを追加します。または、プロパティパスフィールドにパスを入力します。

   ![jcr:content 内のパスからプロパティパスをマップします。](assets/property_picker.png)

   カスタム列をさらに追加するには、「**[!UICONTROL 追加]**」をクリックし、手順 5 および 6 を繰り返します。

1. ツールバーから「**[!UICONTROL 作成]**」をクリックします。レポートの生成が開始されたことを通知するメッセージが表示されます。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## トラブルシューティング情報、ヒント、制限事項{#best-practices-and-limitations}

* ディスク使用量レポートが生成されず、[!DNL Dynamic Media]を使用している場合は、すべてのアセットが正しく処理されることを確認します。 解決するには、アセットを再処理し、レポートを再生成します。
