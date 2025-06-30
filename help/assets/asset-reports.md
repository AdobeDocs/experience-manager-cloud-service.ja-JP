---
title: 使用状況および共有に関するレポート
description: デジタルアセットの使用状況、アクティビティ、共有を理解するのに役立つ、 [!DNL Adobe Experience Manager Assets]  でのアセットに関するレポートです。
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: ef617b01-0019-4379-8d58-c03215d7e28f
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 100%

---

# アセットレポート {#asset-reports}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

アセットレポートを使用すると、 [!DNL Adobe Experience Manager Assets] デプロイメントのユーティリティを評価できます。[!DNL Assets] を使用すると、デジタルアセットに関する様々なレポートを生成できます。レポートでは、システムの使用状況、ユーザーによるアセットの操作方法、<!-- downloaded and --> 共有されるアセットなどに関する役に立つ情報が提供されます。

レポートの情報を使用して重要な成功指標を導き出し、企業やお客様における [!DNL Assets] の採用状況を測定することができます。

[!DNL Assets] のレポートフレームワークでは、[!DNL Sling] ジョブを利用して、レポートのリクエストが順序立てて非同期的に処理されます。このフレームワークは大規模なリポジトリーに合わせて拡張することができます。レポートの非同期処理により、レポートの生成速度と効率が向上します。

レポート管理インターフェイスは直感的で、アーカイブされたレポートにアクセスし、レポートの実行ステータス（成功、失敗、待機中）を表示する、詳細なオプションとコントロールが含まれます。

レポートが生成されると、インボックス通知<!-- through an email (optional) and -->で通知されます。それまでに生成されたすべてのレポートが示されるレポートリストページで、レポートの表示、ダウンロードまたは削除を行うことができます。

## レポートの生成 {#generate-reports}

[!DNL Experience Manager Assets] では、次の標準レポートが生成されます。

* アップロード
* ダウンロード
* 有効期限
* 変更
* 公開
* [!DNL Brand Portal] 公開
* ディスク使用量
* ファイル
* リンク共有

<!-- Removed download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Disk Usage
* Files
* Link Share
-->

[!DNL Adobe Experience Manager] 管理者は、これらのレポートを手軽に生成し、実装に合わせて容易にカスタマイズできます。レポートを生成するには、以下の手順に従います。

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;をクリックします。

   ![アセットレポートに移動するツールページ](assets/navigation.png)

1. [!UICONTROL アセットレポート]ページで、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL レポートを作成]**&#x200B;ページで、作成するレポートを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   >[!NOTE]
   >
   >**ダウンロード**&#x200B;レポートを作成するには、**AEM 管理者製品プロファイル**&#x200B;の資格を自分に付与します。AEM 管理者製品プロファイルの資格を自分に付与するには、[AEM 製品プロファイルの割り当て](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem)を参照してください。

   ![レポートタイプの選択](assets/choose_report.png)

1. タイトル、説明、サムネール、フォルダーパスなど、レポートの詳細を設定します。デフォルトでは、フォルダーパスは `/content/dam` です。別のパスを指定して、特定のフォルダーでレポートを実行できます。

   ![レポートの詳細を追加するページ](assets/report_configuration.png)

   レポートの日付範囲を選択します。レポートを今すぐ生成するか、将来の日時に生成するかを選択できます。

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

1. **[!UICONTROL 列を構成]**&#x200B;ページでは、いくつかの列がデフォルトでレポートに表示されるように選択されています。追加の列を選択できます。列の選択をキャンセルすると、その列はレポートから除外されます。

   ![レポート列の選択または選択のキャンセル](assets/configure_columns.png)

   カスタムの列名やプロパティパスを表示するには、CRX のノード下のアセットバイナリのプロパティを設定します。`jcr:content`または、プロパティパスピッカーを使用して追加します。

   ![レポート列の選択または選択のキャンセル](assets/custom_columns.png)

1. ツールバーから「**[!UICONTROL 作成]**」をクリックします。レポートの生成が開始されたことを通知するメッセージが表示されます。
1. [!UICONTROL アセットレポート]ページのレポート生成ステータスは、レポートジョブの現在の状態（「[!UICONTROL 成功]」、「[!UICONTROL 失敗]」、「[!UICONTROL 待機中]」、「[!UICONTROL スケジュール済み]」など）に基づきます。同じステータスが通知インボックスにも表示されます。レポートページを表示するには、レポートのリンクをクリックします。または、レポートを選択し、ツールバーの「**[!UICONTROL 表示]**」をクリックします。

   <!--![A generated report](assets/report_page.png)-->
   ![生成されたレポートのステータス](assets/report-status.JPG)

   ツールバーの「**[!UICONTROL ダウンロード]**」をクリックすると、レポートを CSV 形式でダウンロードできます。

   >[!NOTE]
   >
   >過去 360 日間に生成されたイベントに基づいて、レポートを生成できます。 Experience Manager はユーザー ID データを 30 日間保持します。

## レポートへのカスタム列の追加 {#add-custom-columns}

また、次のレポートにカスタム列を追加して、独自の要件に応じてさらに多くのデータを表示できます。

<!-- Remove download report.
* Upload
* Download
* Expiration
* Modification
* Publish
* [!DNL Brand Portal] publish
* Files
-->

* アップロード
* 有効期限
* 変更
* 公開
* [!DNL Brand Portal] 公開
* ファイル

これらのレポートにカスタム列を追加するには、次の手順に従います。

1. [!DNL Manager interface] で、 **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;をクリックします 。
1. [!UICONTROL アセットレポート]ページで、ツールバーの「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL レポートを作成]**&#x200B;ページから、作成するレポートを選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. タイトル、説明、サムネール、フォルダーパス、期間など、該当するレポートの詳細を設定します。「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL デフォルトの列]**&#x200B;のリストから、該当する情報を選択します。カスタム列を表示するには、「**[!UICONTROL カスタム列]**」で列の名前を指定します。

   ![レポートのカスタム列の名前を指定](assets/custom_columns-1.png)

1. プロパティパスピッカーを使用して、CRXDE の `jcr:content` ノード下にプロパティパスを追加します。または、プロパティパスフィールドにパスを入力します。

   ![jcr:content 内のパスからプロパティパスをマップします。](assets/property_picker.png)

   カスタム列をさらに追加するには、「**[!UICONTROL 追加]**」をクリックし、上記の手順を繰り返します。

1. ツールバーから「**[!UICONTROL 作成]**」をクリックします。レポートの生成が開始されたことを通知するメッセージが表示されます。

<!-- TBD: How to configure purge now? Is it using OSGi configurations?

## Configure purging service {#configure-purging-service}

To remove reports that you no longer require, configure the DAM Report Purge service from the web console to purge existing reports based on their quantity and age.

1. Access the web console (configuration manager) from `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL DAM Report Purge Service]** configuration.
1. Specify the frequency (time interval) for the purging service in the `scheduler.expression.name` field. You can also configure the age and the quantity threshold for reports.
1. Save the changes.
-->

## トラブルシューティング情報 {#tips-troubleshoot}

* [!DNL Dynamic Media] を使用していて、[!UICONTROL ディスク使用量レポート]が生成されない場合は、すべてのアセットが正しく処理されていることを確認します。問題を解決するには、アセットを再処理し、レポートを再度生成します。

<!-- These notes were present in generate report section above. Removing commented text from in between the instructions to preserve the numbering of the ordered list.

TBD: How do enable this in CS now? Is it done using some OSGi config now?
   >[!NOTE]
   >
   >Before you can generate an **[!UICONTROL Asset Downloaded]** report, ensure that the Asset Download service is enabled. From the web console (`https://[aem_server]:[port]/system/console/configMgr`), open the **[!UICONTROL Day CQ DAM Event Recorder]** configuration, and select the **[!UICONTROL Asset Downloaded (DOWNLOADED)]** option in Event Types if not already selected.
-->

<!-- Removed download report.
   >[!NOTE]
   >
   >By default, the Content Fragments and link shares are included in the asset [!UICONTROL Download] report. Select the appropriate option to create a report of link shares or to exclude Content Fragments from the download report.

   >[!NOTE]
   >
   >The [!UICONTROL Download] report displays details of only those assets which are downloaded after selecting individually or are downloaded using Quick Action. However, it does not include the details of the assets that are inside a downloaded folder.
-->

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
