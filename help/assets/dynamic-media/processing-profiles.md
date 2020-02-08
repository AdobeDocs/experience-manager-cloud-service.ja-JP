---
title: メタデータ、画像およびビデオを処理するためのプロファイル
description: プロファイルは、フォルダーにアップロードされたアセットに適用されるオプションに関する一連のルールです。アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定します。画像アセットの場合は、適切に切り抜くために画像アセットに適用するイメージプロファイルを指定することもできます。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Profiles for processing metadata, images, and videos{#profiles-for-processing-metadata-images-and-videos}

プロファイルとは、フォルダーにアップロードされるアセットに適用するオプションを指定したファイルです。例えば、アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定できます。また、画像アセットを適切に切り抜くために画像アセットに適用するイメージプロファイルを指定できます。

ルールには、メタデータの追加、画像のスマート切り抜きまたはビデオエンコーディングプロファイルの構築などが含まれます。AEM では、3 種類のプロファイルを作成できます。次のリンク先では、それらのプロファイルについて詳しく説明しています。

* [メタデータプロファイル](/help/assets/metadata-profiles.md)
* [イメージプロファイル](/help/assets/dynamic-media/image-profiles.md)
* [ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成、編集および削除するには、管理者権限が必要です。

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成した後、新規にアップロードするアセットのアップロード先として使用する 1 つ以上のフォルダーにそのプロファイルを割り当てます。

[処理プロファイルを使用するためのデジタルアセットの編成のベストプラクティス](/help/assets/dynamic-media/best-practices-for-file-management.md)を参照してください。

>[!NOTE]
>
>あるフォルダーから別のフォルダーに移動するアセットは再処理されません。例えば、プロファイルAが割り当てられたフォルダ1と、プロファイルBが割り当てられたフォルダ2があるとします。 フォルダ1からフォルダ2にアセットを移動すると、移動したアセットはフォルダ1の元の処理を保持します。
>
>同じプロファイルが割り当てられている 2 つのフォルダー間でアセットを移動する場合にも、同じことが言えます。

## フォルダー内のアセットの再処理 {#reprocessing-assets}

後で変更した既存の処理プロファイルが既に存在するフォルダー内のアセットを再処理できます。

例えば、画像プロファイルを作成し、フォルダーに割り当てたとします。 フォルダーにアップロードした画像アセットには、画像プロファイルが自動的にアセットに適用されます。 ただし、後で、プロファイルに新しいスマート切り抜き率を追加することにします。 ここで、アセットを選択してフォルダに再度アップロードする代わりに、 *Scene7を実行します。アセットの再処理* ワークフロー。

処理が初めて失敗したアセットに対して再処理ワークフローを実行できます。 したがって、処理プロファイルを編集していない場合や処理プロファイルを適用していない場合でも、アセットのフォルダーに対して再処理ワークフローをいつでも実行できます。

オプションで、再処理ワークフローのバッチサイズをデフォルトの50アセットから最大1,000アセットまで調整できます。 _Scene7を実行する場合：フォルダー上のアセット_ ・ワークフローを再処理すると、アセットはバッチでグループ化され、処理のためにダイナミック・メディア・サーバーに送信されます。 処理の後、バッチセット全体の各アセットのメタデータがAEM上で更新されます。 バッチサイズが非常に大きい場合は、処理に遅延が生じる可能性があります。 また、バッチサイズが小さすぎると、ダイナミックメディアサーバーへのラウンドトリップが多すぎる場合があります。

詳しくは、 [再処理ワークフローのバッチサイズの調整を参照してください](#adjusting-load)。

>[!NOTE]
>
>Dynamic Media ClassicからAEMへのアセットの一括移行を実行する場合は、Dynamic Mediaサーバーで移行レプリケーションエージェントを有効にする必要があります。 移行が完了したら、エージェントを無効にします。
再処理ワークフローが期待どおりに動作するように、移行発行エージェントをダイナミックメディアサーバーで無効にする必要があります。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**フォルダ内のアセットを再処理するには**:
1. AEMのアセットページで、処理プロファイルが割り当てられ、 **Scene7を適用するアセットのフォルダに移動します。アセットの再処理** ワークフロー、

   処理プロファイルが既に割り当てられているフォルダーは、カード表示のフォルダー名のすぐ下にプロファイル名が表示されます。

1. フォルダを選択します。

   * ワークフローは、選択したフォルダー内のすべてのファイルを再帰的に考慮します。
   * メイン選択フォルダー内にアセットを含む1つ以上のサブフォルダーが存在する場合、ワークフローはフォルダー階層内のすべてのアセットを再処理します。
   * ベストプラクティスとして、1,000を超えるアセットを含むフォルダー階層では、このワークフローを実行しないでください。

1. Near the upper-left corner of the page, from the drop-down list, click **[!UICONTROL Timeline]**.
1. ページの左下隅近くの「コメント」フィールドの右側で、カラットアイコン( **^** )をクリックします。

   ![アセットの再処理ワークフロー1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 「**[!UICONTROL ワークフローを開始]**」をクリックします。
1. 「ワークフ **[!UICONTROL ローを開始]** 」ドロップダウンリストから「 **[!UICONTROL Scene7」を選択します。アセットの再処理]**。
1. （オプション）「ワークフ **ローのタイトルを入力** 」テキストフィールドに、ワークフローの名前を入力します。 必要に応じて、この名前を使用してワークフローインスタンスを参照できます。

   ![アセットの再処理2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 「開始」 **[!UICONTROL をクリックし]**、「確認」をクリ **[!UICONTROL ックします]**。

   ワークフローを監視したり、進行状況を確認したりするには、AEMのメインコンソールページでツール/ワークフ **[!UICONTROL ローをクリックします]**。 ワークフローインスタンスページで、ワークフローを選択します。 メニューバーで[履歴を開く]をク **[!UICONTROL リックします]**。 同じワークフローインスタンスページから、選択したワークフローを終了、休止、名前の変更を行うこともできます。

### 再処理ワークフローのバッチサイズの調整 {#adjusting-load}

（オプション）再処理ワークフローのデフォルトのバッチサイズは、ジョブあたり50アセットです。 この最適なバッチサイズは、再処理が実行されるアセットの平均アセットサイズとMIMEタイプによって制御されます。 値を大きくすると、1回の再処理ジョブに多数のファイルが含まれます。 したがって、処理バナーはAEMアセット上に長い時間残ります。 ただし、平均ファイルサイズが1 MB以下の場合は、値を数百個に増やし、1000以下にすることをお勧めします。 平均ファイルサイズが数百MBの場合は、バッチサイズを10まで小さくすることをお勧めします。

**オプションで再処理ワークフローのバッチサイズを調整するには**

1. Experience Managerで、 **[!UICONTROL Adobe Experience Managerをタップしてグローバルナビゲーションコンソールにアクセスし、ツール]** （ハンマー）アイコン/ワークフロー/モ **[!UICONTROL デルをタップします]******。
1. ワークフローモデルページのカード表示またはリスト表示で、「 **[!UICONTROL Scene7」を選択します。アセットの再処理]**。

   ![Scene7を含むワークフローモデルページ：カード表示で選択されたアセットの再処理ワークフロー](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. ツールバーで、「編集」をクリッ **[!UICONTROL クします]**。 新しいブラウザタブでScene7が開きます。アセットワークフローモデルページを再処理します。
1. Scene7の場合：アセットワークフローページを再処理します。右上隅近くにある「編集」を **[!UICONTROL タップし]** 、ワークフローを「ロック解除」します。
1. ワークフローで、Scene7バッチアップロードコンポーネントを選択してツールバーを開き、ツールバーの「 **[!UICONTROL 設定]** 」をタップします。

   ![Scene7バッチアップロードコンポーネント](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. Scene7へのバッ **[!UICONTROL チアップロード — ステップのプロパティ]** ダイアログボックスで、次の設定を行います。
   * 必要に応じて、 **[!UICONTROL 「タイ]** トル **** 」と「説明」テキストフィールドに、ジョブの新しいタイトルと説明を入力します。
   * ハンドラ **[!UICONTROL ーが次の手順に進む場合は]** 、「ハンドラー処理の詳細設定」を選択します。
   * 「 **[!UICONTROL Timeout]** 」フィールドに、外部プロセスのタイムアウト（秒）を入力します。
   * 「 **[!UICONTROL Period]** 」フィールドに、外部プロセスの完了をテストするポーリング間隔（秒）を入力します。
   * 「バッ **[!UICONTROL チ」フィールドに]**、ダイナミックメディアサーバーのバッチ処理アップロードジョブで処理するアセットの最大数(50 ～ 1000)を入力します。
   * タイム **[!UICONTROL アウトに達した後に進める場合は]** 、「タイムアウト時に進む」を選択します。 タイムアウトに達したときにインボックスに進む場合は、選択を解除します。
   ![プロパティダイアログボックス](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. Scene7へのバッチアップロード — ステップのプ **[!UICONTROL ロパティダイアログボックスの右上隅で]** 、「完了」をタップ **[!UICONTROL します]**。

1. Scene7の右上隅：アセットワークフローモデルページを再処理し、「同期」をタ **[!UICONTROL ップしま]**&#x200B;す。 「同期済み」と表示さ **[!UICONTROL れる場合]**、ワークフローランタイムモデルは正常に同期され、フォルダー内のアセットを再処理する準備が整います。

   ![ワークフローモデルの同期](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Scene7を表示するブラウザタブを閉じます。アセットワークフローモデルの再処理を参照してください。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
