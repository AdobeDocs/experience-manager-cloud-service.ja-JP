---
title: アセットビューでのレポートの管理
description: アセットビューの「レポート」セクションのデータにアクセスして、製品と機能の使用状況を評価し、主要な成功指標に関するインサイトを導き出します。
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: 6e0cd465f8695c948ece4679e083d6b9b35dded4
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 78%

---

# レポートの管理 {#manage-reports}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

アセットレポートを使用すると、管理者は Adobe Experience Manager Assets ビュー環境のアクティビティを視覚的に確認できます。このデータは、ユーザーがコンテンツや製品とどのようにやり取りするかについての有用な情報を提供します。 すべてのユーザーが Insights ダッシュボードにアクセスでき、管理者の製品プロファイルに割り当てられたユーザーはユーザー定義レポートを作成できます。

## レポートへのアクセス {#access-reports}

AEM管理者製品プロファイルに割り当てられているユーザーはすべて、Assets ビューでインサイトダッシュボードにアクセスしたり、ユーザー定義のレポートを作成したりできます。

レポートにアクセスするには、**[!UICONTROL 設定]**&#x200B;の&#x200B;**[!UICONTROL レポート]**&#x200B;に移動します。

![レポート](assets/reports.png)

<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## レポートの作成 {#create-report}

AEM Assets ビュー環境では、レポートダッシュボードを通じて包括的なレポート機能が提供されます。この機能により、ユーザーは、指定された期間（1 回限りから、日別、週別、月別、年別の間隔まで）内のアセットのアップロードとダウンロードの詳細を示す CSV レポートを生成してダウンロードできます。

**レポートを作成するには：**

1. **レポート**&#x200B;に移動し、「**レポートを作成**」（右上から）をクリックします。 **レポートを作成**ダイアログボックスには、以下のフィールドが表示されます。
   ![create-report](/help/assets/assets/executed-reports1.svg)

   **「設定」タブ：**

   1. **レポートタイプ：**[!UICONTROL  アップロード ]、[!UICONTROL  ダウンロード ]、[Dynamic Media配信レポート ](#dynamic-media-delivery-reports) のいずれかのタイプを選択します。
   1. **タイトル：**&#x200B;レポートにタイトルを追加します。
   1. **説明：**&#x200B;レポートにオプションの説明を追加します。
   1. **フォルダーパスを選択：**&#x200B;フォルダーパスを選択すると、その特定のフォルダー内でアップロードおよびダウンロードされたアセットのレポートが生成されます。 例えば、フォルダーにアップロードされたアセットのレポートが必要な場合は、そのフォルダーへのパスを指定します。
   1. **日付間隔を選択：**&#x200B;フォルダー内のアップロードまたはダウンロードのアクティビティを表示するには、日付範囲を選択します。
   <br>

   >[!NOTE]
   >
   > アセットビューは、すべてのローカルタイムゾーンを協定世界時（UTC）に変換します。

   **「列」タブ：**&#x200B;レポートに表示する列名を選択します。 次の表に、すべての列の使用方法を示します。

   <table>
    <tbody>
     <tr>
      <th><strong>列名</strong></th>
      <th><strong>説明</strong></th>
      <th><strong>レポートタイプ</strong></th>
     </tr>
     <tr>
      <td>タイトル</td>
      <td>アセットのタイトル。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>パス</td>
      <td>アセットビューでアセットを使用できるフォルダーパス。</td>
      <td>アップロード、ダウンロード、Dynamic Media配信</td>
     </tr>
     <tr>
      <td>MIME タイプ</td>
      <td>アセットの MIME タイプ。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>サイズ</td>
      <td>アセットのサイズ（バイト単位）。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>ダウンロードしたユーザー</td>
      <td>アセットをダウンロードしたユーザーのメール ID。</td>
      <td>ダウンロード</td>
     </tr>
     <tr>
      <td>ダウンロード日</td>
      <td>アセットのダウンロードアクションが実行された日付。</td>
      <td>ダウンロード</td>
     </tr>
     <tr>
      <td>作成者</td>
      <td>アセットの作成者。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>作成日時</td>
      <td>アセットがアセットビューにアップロードされた日付。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>変更日</td>
      <td>アセットの最終変更日付。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>期限切れ</td>
      <td>アセットの有効期限切れステータス。</td>
      <td>アップロードとダウンロード</td>
     </tr>
     <tr>
      <td>ユーザー名によりダウンロード</td>
      <td>アセットをダウンロードしたユーザーの名前。</td>
      <td>ダウンロード</td>
     </tr> 
     <tr>
      <td>リファラー</td>
      <td>アセットが配信される、または含まれる URL</td>
      <td>Dynamic Media 配信</td>
     </tr>  
     <tr>
      <td>ヒット数</td>
      <td>アセットが配信された回数（配信数）</td>
      <td>Dynamic Media 配信</td>
     </tr>          
    </tbody>
   </table>

## Dynamic Media配信レポート {#dynamic-media-delivery-reports}

アセットレベルの配信数、リファラー情報、AEM Assets 内のアセットパス、一意のアセット ID など、Dynamic Media で配信されたアセットの配信インサイトを取得します。 レポートは、AEM AssetsのDynamic Media リポジトリを介して配信されたすべてのアセットについて、またはAEM Assetsの特定のフォルダー階層について生成できます。 さらに、Dynamic Media配信レポートのインサイトは、配信されたアセットの ROI の測定、チャネルのパフォーマンスの測定、情報に基づいたアセット管理タスクの実行に役立ちます。

>[!NOTE]
> 
>Dynamic Media アカウントのDynamic Media配信レポートに早期にアクセスするには、[Adobeのカスタマーサポートケースを作成して送信 ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) します。

### 前提条件 {#prereqs-dynamic-media-delivery-reports}

このレポートを作成して使用するには、Dynamic Media ライセンスが必要です。

>[!IMPORTANT]
> 
>* Dynamic Media 経由で配信されるアセットに関するレポートが提供されます。
>* レポートは、最初の 100 万行に対して生成されます。この制限内のすべてのファイルを取り込むには、小さいフォルダーのリファラー列を含めることを検討してください。
>* レポートは過去 3 か月間のみ生成できます。

### Dynamic Media配信レポートの作成{#create-dynamic-media-delivery-report}

1. [ レポートの作成 ](#create-report) で説明されている手順を使用して、Dynamic Media配信レポートを作成します。

1. ]**レポートタイプ**[!UICONTROL  ドロップダウンリストから「**[!UICONTROL Dynamic Media配信]**」を選択します。

   ![Dynamic Media配信レポートドロップダウン ](assets/dynamic-media-delivery-report-option.png)


1. 「**[!UICONTROL 列]**」タブで「**[!UICONTROL リファラー]**」列を選択すると、レポートに含めることができます。

   ![ リファラー ](assets/referrer.png)

   ダウンロードされたレポートのすべての列は、読み取り専用です。ただし、「リファラー **列は、レポートに含めたり除外したりするように変更できます**。<!--Choosing a referrer displays the number of visitors received from each referred report that directs traffic to the site. It offers insights into the sources of traffic and the origin of the visitors. Such insights help measure ROI of delivered assets, measure channel performance, and help take informed asset management tasks for assets.-->

### Dynamic Media配信レポートで実行されたアクション {#actions-performed-dynamic-media-delivery-reports}

レポートを作成した後、次の操作を実行できます。

* **[!UICONTROL 削除]**：選択したレポートを削除できます。
* **[!UICONTROL CSV をダウンロード]**：選択したレポートを CSV 形式でダウンロードできます。 ダウンロードされたレポートは、名前、パス、DynamicMediaID、リファラー、ヒットの各列で構成されます。
   * **リファラー** 列には、アセットが配信または含まれる URL がリストされます。

   * **ヒット数** 列には、アセットが配信された回数（配信数）がリストされます。

Dynamic Media配信レポートを CSV 形式で削除またはダウンロードするには、[ 既存のレポートの表示とダウンロード ](#View-and-download-existing-report) を参照してください。

![ ダウンロードした CSV のDynamic Media配信レポート ](assets/csv-dynamic-media-delivery-report.png)


## 既存のレポートの表示とダウンロード {#View-and-download-existing-report}

既存のレポートは、「**実行されたレポート**」タブの下に表示されます。 「**レポート**」をクリックし、「**実行されたレポート**」を選択すると、ステータスが&#x200B;**完了**&#x200B;となり、ダウンロードの準備が整ったことを示す、作成済みのすべてのレポートが表示されます。 レポートを CSV 形式でダウンロードすることや、レポートを削除するには、レポート行を選択します。 次に、「**CSV をダウンロード**」または「**削除**」を選択します。
![既存のレポートの表示とダウンロード](/help/assets/assets/view-download-existing-report.png)


## レポートのスケジュール {#schedule-report}

AEM Assets ビュー UI の「**レポートをスケジュール**」では、日別、週別、月別、年別など、指定された今後の間隔でレポートを自動的に生成するように設定します。この機能により、繰り返し発生するレポートのニーズが効率化され、タイムリーなデータ更新が確保されます。 一方、「**レポートを作成**」では、過去の日付のレポートが生成されます。 完了したレポートは「**実行されたレポート**」の下にリストされ、今後のレポートは「**スケジュールされたレポート**」の下に表示されます。

レポートをスケジュールするには、次の手順に従います。

1. 左側のパネルから「レポート」をクリックし、「レポートを作成」（右上から）をクリックします。
1. レポートダイアログボックスには、以下の情報が表示されます。
   1. **レポートタイプ：**&#x200B;アップロードとダウンロードのどちらかのタイプを選択します。
   1. **タイトル：**&#x200B;レポートにタイトルを追加します。
   1. **説明**：レポートにオプションの説明を追加します。
   1. **フォルダーパスを選択：**&#x200B;フォルダーパスを選択すると、今後のその特定のフォルダーにアップロードされるか、その特定のフォルダーからダウンロードされるアセットのレポートが生成されます。
   1. **「レポートをスケジュール」を切り替え：**レポートを後で実行するようにスケジュールするか、繰り返し実行するように切り替えます。
      ![レポートのスケジュール](/help/assets/assets/schedule-reports1.svg)

   1. **頻度を選択：**&#x200B;レポートを生成する間隔（例えば、日別、週別、月別、年別、1 回限り）を指定し、レポートを実行する日時と繰り返しの終了日を設定します。 1 回限りのレポートの場合は、AEM 環境で選択したアクティビティタイプに関するレポートの日付範囲を選択します。 例えば、特定の月の 10日から 29日（今後の日付）までにダウンロードされたアセットに関するレポートが必要な場合は、「**日付間隔を選択**」フィールドでこれらの日付を選択します。

   >[!NOTE]
   >
   > アセットビューは、すべてのローカルタイムゾーンを協定世界時（UTC）に変換します。

## スケジュールされたレポートの表示 {#view-scheduled-reports}

スケジュールされたレポートは、「**スケジュールされたレポート**」タブの下に体系的に整理されて表示されます。 スケジュールされた各レポートのすべての完了したレポートは、単一のレポートフォルダー内に保存されます。 完全なレポートを表示するには、「![折りたたみを展開](/help/assets/assets/expand-icon1.svg)」をクリックします。例えば、日別レポートをスケジュールした場合、完了したレポートはすべて 1 つのフォルダーにグループ化されます。 この構成により、レポートのナビゲーションと検出性が簡素化されます。 スケジュールされたレポートを表示するには、「**レポート**」をクリックし、「**スケジュールされたレポート**」をクリックします。 スケジュールされたすべてのレポートが、進行中または完了のステータスと共に表示されます。 完全なレポートをダウンロードする準備が整いました。\
![スケジュールされたレポート](/help/assets/assets/scheduled-reports-tab.png)

## スケジュールされたレポートの編集とキャンセル {#edit-cancel-scheduled-reports}

1. 「**スケジュールされたレポート**」タブに移動します。
1. レポート行を選択します。
1. 「**編集**」をクリックします。
1. 「**スケジュールをキャンセル**」、「**確認**」の順にクリックして、スケジュールされたレポートをキャンセルします。 キャンセルしたレポートについては、次回の実行時間は空になり、ステータスはキャンセルと表示されます。
   ![スケジュールされたレポートの編集とキャンセル](/help/assets/assets/cancel-edit-scheduled-reports.png)

### スケジュールを再開 {#resume-schedule}

キャンセルしたスケジュールを再開するには、レポート行を選択し、「**スケジュールを再開**」をクリックします。 再開すると、次回の実行時間のエントリが再び表示され、ステータスは進行中と表示されます。
![スケジュールを再開](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> キャンセルしたレポートを、スケジュールされた終了日より前に再開すると、キャンセル日から再開日までのレポートが自動的に生成されます。

## インサイトの表示 {#view-live-statistics}

アセットビューを使用すると、アセットビュー環境のリアルタイムデータをインサイトダッシュボードで表示できます。過去 30 日間または過去 12 か月間のリアルタイムイベント指標を表示できます。

<!--![Toolbar options when you select an asset](assets/assets-view-live-statistics.png)-->

左側のナビゲーションパネルにある「**[!UICONTROL インサイト]**」をクリックすると、自動生成された以下のグラフを表示できます。

* **ダウンロード**：過去 30 日間または 12 か月間に Assets ビュー環境からダウンロードされたアセットの数が、折れ線グラフで表されます。
  ![インサイトのダウンロード](/help/assets/assets/insights-downloads2341.svg)

* **アップロード**：過去 30 日間または 12 か月間に Assets ビュー環境にアップロードされたアセットの数が、折れ線グラフで表されます。
  ![インサイトのアップロード](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **ストレージ使用量**：Assets ビュー環境のストレージ使用量（バイト）が、棒グラフで表されます。
  ![インサイトのアップロード](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **上位の検索**：過去 30 日間または 12 か月間に Assets ビュー環境で使用された上位の検索用語とその検索回数が、表形式で表されます。
  ![インサイトのアップロード](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->
* **サイズ別のアセットカウント：**アセットビュー環境の合計アセット数を様々なサイズ範囲にセグメント化し、各サイズ範囲内のアセットの数と割合をハイライト表示し、ドーナツグラフで表します。
  ![insights-assets-count-by-size](/help/assets/assets/insights-assets-count-by-size.svg)
* **アセットタイプ別のアセットカウント：**アセットビュー環境の合計アセット数をセグメント化し、ファイルタイプに基づいてアセットの数と割合をハイライト表示し、ドーナツグラフで表します。
  ![insights-assets-count-by-size](/help/assets/assets/insights-assest-count-by-asset-type1.svg)