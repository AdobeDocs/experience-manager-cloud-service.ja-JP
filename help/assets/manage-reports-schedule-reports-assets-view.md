---
title: アセットビューでのレポートの管理
description: アセットビューの「レポート」セクションのデータにアクセスして、製品と機能の使用状況を評価し、主要な成功指標に関するインサイトを導き出します。
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: 1103ed766eb17aa984831b6213e7e15671ead536
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 38%

---

# レポートの管理 {#manage-reports}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

アセットレポートを使用すると、管理者は Adobe Experience Manager Assets ビュー環境のアクティビティを視覚的に確認できます。このデータは、ユーザーがコンテンツや製品とどのようにやり取りするかについての有用な情報を提供します。すべてのユーザーが Insights ダッシュボードにアクセスでき、管理者の製品プロファイルに割り当てられたユーザーはユーザー定義レポートを作成できます。

## レポートへのアクセス {#access-reports}

アセットビューの管理者の製品プロファイルに割り当てられているユーザーはすべて、アセットビューでインサイトダッシュボードにアクセスしたり、ユーザー定義のレポートを作成したりできます。

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

AEM Assets ビュー環境は、レポート ダッシュボードを通じて包括的なレポート機能を提供します。 この機能を使用すると、アセットのアップロードとダウンロードの詳細を示す CSV レポートを、一度限りの期間から毎日、毎週、毎月、毎年などの指定した期間内に生成およびダウンロードできます。

**レポートを作成するには：**

1. **レポート** に移動して、（右上の **レポートを作成** をクリックします。 **レポートを作成** ダイアログボックスには、以下のフィールドが表示されます。
   ![create-report](/help/assets/assets/executed-reports1.svg)

   **「設定」タブで：**

   1. **レポートタイプ：** アップロードタイプとダウンロードタイプのどちらかを選択します。
   1. **タイトル：** レポートにタイトルを追加します。
   1. **説明：** オプションの説明をレポートに追加します。
   1. **フォルダーパスを選択：** アップロードおよびダウンロードされたアセットのレポートを、その特定のフォルダー内に生成するフォルダーパスを選択します。 例えば、アセットのレポートをフォルダーにアップロードする必要がある場合は、そのフォルダーへのパスを指定します。
   1. **日付間隔を選択：** フォルダー内のアップロードまたはダウンロードアクティビティを表示する日付範囲を選択します。
   <br>

   >[!NOTE]
   >
   > アセットビューは、すべてのローカルタイムゾーンを協定世界時（UTC）に変換します。

   **「列」タブ：** レポートに表示する列名を選択します。 次の表に、すべての列の使用方法を示します。

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
      <td>アップロードとダウンロード</td>
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
    </tbody>
   </table>

## 既存のレポートの表示とダウンロード {#View-and-download-existing-report}

既存のレポートは、「**実行済みレポート** タブに表示されます。 「**レポート**」をクリックし、「**実行済みレポート**」を選択して、ステータスが「**完了**」の作成済みレポートをすべて表示し、ダウンロードする準備が整ったことを示します。 レポートを CSV 形式でダウンロードしたり、レポートを削除したりするには、レポート行を選択します。 次に、「**CSV をダウンロード** または **削除**」を選択します。
![ 既存のレポートの表示とダウンロード ](/help/assets/assets/view-download-existing-report.png)

## レポートのスケジュール設定 {#schedule-report}

AEM Assets ビュー UI で **レポートのスケジュール** を使用すると、毎日、毎週、毎月、毎年など、指定した将来の間隔でレポートが自動的に生成されるように設定できます。 この機能は、繰り返し発生するレポートニーズを合理化し、タイムリーにデータを更新するのに役立ちます。 一方 **レポートを作成** は、過去の日付のレポートを生成します。 完了したレポートは **実行済みレポート** の下に表示され、今後のレポートは **予定レポート** の下に表示されます。

レポートをスケジュールするには、次の手順に従います。

1. 左側のパネルから「レポート」をクリックし、右上の「レポートを作成」をクリックします。
1. レポートダイアログボックスには、次の情報が表示されます。
   1. **レポートタイプ：** アップロードタイプとダウンロードタイプのどちらかを選択します。
   1. **タイトル：** レポートにタイトルを追加します。
   1. **説明**：オプションの説明をレポートに追加します。
   1. **フォルダーパスを選択：** 今後その特定のフォルダーにアップロードされる、または特定のフォルダーからダウンロードされるアセットのレポートを生成するフォルダーパスを選択します。
   1. **レポートをスケジュール：** 後でレポートをスケジュールするか、繰り返し発生させるかを切り替えます。
      ![ スケジュール報告書 ](/help/assets/assets/schedule-reports1.svg)

   1. **頻度を選択：** レポートを生成する間隔（毎日、毎週、毎月、毎年、1 回など）を指定し、レポートを実行する日時と繰り返しの終了日を設定します。 1 回限りのレポートの場合は、AEM環境で選択したアクティビティタイプに関するレポートの日付範囲を選択します。 例えば、特定の月の 10 日から 29 日（未来の日付）の間にダウンロードされたアセットに関するレポートが必要な場合、「**日付範囲を選択**」フィールドでこれらの日付を選択します。

   >[!NOTE]
   >
   > アセットビューは、すべてのローカルタイムゾーンを協定世界時（UTC）に変換します。

## 予定レポートの表示 {#view-scheduled-reports}

予定レポートは、「**予定レポート** タブに系統的に表示されます。 各予定レポートの完了済みレポートはすべて、1 つのレポートフォルダー内に保存されます。 クリック ![ 展開 ](/help/assets/assets/expand-icon1.svg) 折りたたみをクリックすると、完了したレポートが表示されます。 例えば、日別レポートをスケジュールした場合、完了したすべてのレポートは 1 つのフォルダーにグループ化されます。 この組織により、レポートのナビゲーションと検出性の両方が簡素化されます。 予定レポートを表示するには、[ **レポート** ] をクリックし、[ **予定レポート** ] をクリックします。 すべての予定レポートが、ステータスが進行中または完了として表示されます。 完了したレポートをダウンロードできます。\
![ 予定レポート ](/help/assets/assets/scheduled-reports-tab.png)

## 予定レポートの編集およびキャンセル {#edit-cancel-scheduled-reports}

1. 「**予定レポート**」タブに移動します。
1. レポート行を選択します。
1. 「**編集**」をクリックします。
1. **スケジュールをキャンセル** をクリックし、**確認** をクリックして、スケジュール済みレポートをキャンセルします。 キャンセルされたレポートの場合、次回の実行時は空になり、ステータスはキャンセルと表示されます。
   ![ スケジュール済み報告書の編集およびキャンセル ](/help/assets/assets/cancel-edit-scheduled-reports.png)

### スケジュールを再開 {#resume-schedule}

キャンセルされたスケジュールを再開するには、レポート行を選択し、「**スケジュールを再開**」をクリックします。 再開すると、次の実行時エントリが再び表示され、ステータスが「進行中」になります。
![ 再開スケジュール ](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> 予定終了日より前に取り消されたレポートを再開すると、取消日から再開日までのレポートが自動的に生成されます。

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
* **アセットタイプ別のアセット数：** Assets ビュー環境で合計アセット数をセグメント化し、ファイルタイプに基づいてアセットの数と割合をハイライト表示します。ドーナツグラフで表示されます。
  ![insights-assets-count-by-size](/help/assets/assets/insights-assest-count-by-asset-type1.svg)