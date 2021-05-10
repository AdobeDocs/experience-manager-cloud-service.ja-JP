---
title: Dynamic Media のイメージプロファイルとビデオプロファイルについて
description: イメージプロファイルまたはビデオプロファイルは、フォルダーにアップロードするアセットに適用するオプションの手法です。例えば、アップロードする Dynamic Media のビデオアセットに適用するビデオエンコーディングを指定できます。また、画像アセットを適切に切り抜くために Dynamic Media 画像アセットに適用するイメージプロファイルを指定できます。
feature: アセット管理，画像プロファイル，ビデオプロファイル
role: Administrator,Business Practitioner
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
translation-type: tm+mt
source-git-commit: 1fe6ce1259972c1805d934327aa2f24cdcdc0bc8
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 67%

---

# Dynamic Media のイメージプロファイルとビデオプロファイルについて {#about-dm-image-video-profiles}

イメージプロファイルまたはビデオプロファイルは、フォルダーにアップロードするアセットに適用するオプションの手法です。例えば、アップロードする Dynamic Media のビデオアセットに適用するビデオエンコーディングを指定できます。また、画像アセットを適切に切り抜くために Dynamic Media 画像アセットに適用するイメージプロファイルを指定できます。

Dynamic Media では、2 種類のプロファイルを作成できます。次のリンク先では、それらのプロファイルについて詳しく説明しています。

* [Dynamic Media イメージプロファイル](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)

[メタデータプロファイル](/help/assets/metadata-profiles.md)も参照してください。

Dynamic Media イメージプロファイルまたは Dynamic Media ビデオプロファイルを作成、編集および削除するには、管理者権限が必要です。

画像プロファイルまたはビデオプロファイルを作成したら、新しくアップロードしたDynamic Mediaアセットに使用する1つ以上のフォルダにその画像フォルダを割り当てます。

[イメージプロファイルまたはビデオプロファイルを使用するためのデジタルアセット編成のベストプラクティス](/help/assets/dynamic-media/best-practices-for-file-management.md)も参照してください。

>[!NOTE]
>
>あるフォルダーから別のフォルダーに移動するアセットは再処理されません。例えば、フォルダー 1 にプロファイル A が割り当てられ、フォルダー 2 にプロファイル B が割り当てられているとします。アセットをフォルダー 1 からフォルダー 2 に移動しても、そのアセットには、元の処理がフォルダー 1 から引き継がれます。
>
>同じプロファイルが割り当てられている 2 つのフォルダー間でアセットを移動する場合にも、同じことが言えます。

## フォルダー内の Dynamic Media アセットの再処理 {#reprocessing-assets}

後で変更した既存の Dynamic Media イメージプロファイルまたは Dynamic Media ビデオプロファイルが存在するフォルダー内のアセットを再処理できます。

例えば、Dynamic Media イメージプロファイルを作成してフォルダーに割り当てたとします。フォルダーにアップロードした画像アセットには、イメージプロファイルが自動的にアセットに適用されます。ただし、後でイメージプロファイルに新しいスマート切り抜き率を追加することにします。その場合は、もう一度アセットを選択してフォルダーに再度アップロードするのではなく、「*Scene7：アセットを再処理*」ワークフローを実行するだけです。

処理が初めて失敗したアセットに対して、再処理ワークフローを実行できます。画像プロファイルやビデオプロファイルを編集していない場合や、画像プロファイルやビデオプロファイルを既に適用している場合でも、アセットのフォルダに対して再処理ワークフローを実行できます。

オプションで、再処理ワークフローのバッチサイズを、デフォルトの 50 アセットから最大 1,000 アセットまで調整できます。_Scene7を実行する場合：フォルダー上のアセット_&#x200B;ワークフローを再処理し、アセットをバッチでグループ化して、処理のためにDynamic Mediaサーバーに送信します。 処理の後、バッチセット全体の各アセットのメタデータがAdobe Experience Managerで更新されます。 バッチサイズが大きい場合は、処理に遅延が生じる可能性があります。 また、バッチサイズが小さすぎる場合、Dynamic Mediaサーバーへのラウンドトリップが多すぎる可能性があります。

詳しくは、[再処理ワークフローのバッチサイズの調整](#adjusting-load)を参照してください。

>[!NOTE]
>
>アセットをDynamic MediaクラシックからExperience Managerに一括移行する場合は、Dynamic Mediaサーバーで移行レプリケーションエージェントを有効にします。 移行が完了したら、このエージェントを必ず無効にします。

>
>再処理ワークフローが期待どおりに動作するように、Dynamic Media サーバー上で移行公開エージェントを無効にする必要があります。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**フォルダー内のDynamic Mediaアセットを再処理するには：**
1. Experience Managerで、アセットページから、画像プロファイルーまたはビデオプロファイルーが割り当てられていて、**Scene7を適用するアセットーに移動します。アセット**&#x200B;ワークフローを再処理します。

   画像プロファイルまたはビデオプロファイルが割り当てられているプロファイルにそのフォルダの名前が割り当てられている場合は、カード表示のフォルダ名のすぐ下に表示されます。

1. フォルダーを選択します。

   * 選択したフォルダー内のすべてのファイルがワークフローで再帰的に考慮されます。
   * メイン選択フォルダー内にアセットが含まれるサブフォルダーが1つ以上ある場合、ワークフローはフォルダー階層内のすべてのアセットを再処理します。
   * ベストプラクティスとして、1000を超えるアセットを含むフォルダー階層では、このワークフローを実行しないでください。

1. ページの左上隅付近にあるドロップダウンリストで「**[!UICONTROL タイムライン]**」をクリックします。
1. ページの左下隅近くの、「[!UICONTROL コメント]」フィールドの右側にある、カラトアイコン(**^**)をタップします。

   ![アセット再処理ワークフロー（その 1）](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 「**[!UICONTROL ワークフローを開始]**」をクリックします。
1. 「**[!UICONTROL ワークフローを開始]**」ドロップダウンリストから「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。
1. （オプション）「**ワークフローのタイトルを入力**」テキストフィールドに、ワークフローの名前を入力します。必要に応じて、ワークフローインスタンスを参照する名前を使用できます。

   ![アセット再処理ワークフロー（その 2）](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 「**[!UICONTROL 開始]**」をクリックした後、「**[!UICONTROL 確認]**」をクリックします。

   ワークフローを監視したり、進行状況を確認したりするには、Experience Manager のメインコンソールページで&#x200B;**[!UICONTROL ツール／ワークフロー]**&#x200B;をクリックします。ワークフローインスタンスページで、ワークフローを選択します。メニューバーの「**[!UICONTROL 履歴を開く]**」をクリックします。同じワークフローインスタンスページで、選択したワークフローの終了、休止、名前変更をおこなうこともできます。

### 再処理ワークフローのバッチサイズの調整 {#adjusting-load}

（オプション）再処理ワークフローのデフォルトのバッチサイズは、1 ジョブあたり 50 アセットです。この最適なバッチサイズは、平均アセットサイズと、再処理が実行されるアセットのMIMEタイプによって制御されます。 値を大きくすると、1回の再処理ジョブに多数のファイルが含まれます。 したがって、処理用バナーはExperience Managerアセット上に長い時間残ります。 ただし、平均ファイルサイズが1 MB以下の場合は、値を100個まで増やすことを推奨しますが、Adobeは1000個以下にすることをお勧めします。 平均ファイルサイズが数百MBの場合は、Adobeでは、バッチサイズを10まで下げることを推奨します。

**必要に応じて、再処理ワークフローのバッチ・サイズを調整する手順は**、次のとおりです。

1. Adobe Experience Manager で、「**[!UICONTROL Adobe Experience Manager]**」をタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**（ハンマーアイコン）／**[!UICONTROL ワークフロー／モデル]**&#x200B;をタップします。
1. ワークフローモデルページのカード表示またはリスト表示で、「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。

   ![カード表示で「Scene7：アセットを再処理」ワークフローが選択されたワークフローモデルページ](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. ツールバーで、**[!UICONTROL 編集]**&#x200B;をクリックします。 新しいブラウザータブに、「Scene7：アセットを再処理」ワークフローモデルページが開きます。
1. 「Scene7：アセットを再処理」ワークフローページで、右上隅付近の「**[!UICONTROL 編集]**」をタップして、ワークフローを「ロック解除」します。
1. ワークフローで、Scene7バッチアップロードコンポーネントを選択してツールバーを開き、ツールバーの&#x200B;**[!UICONTROL 設定]**&#x200B;をタップします。

   ![Scene7 バッチアップロードコンポーネント](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. **[!UICONTROL Scene7 へのバッチアップロード - ステップのプロパティ]**&#x200B;ダイアログボックスで、以下の設定をおこないます。
   * 「**[!UICONTROL タイトル]**」および「**[!UICONTROL 説明]**」テキストフィールドに、必要に応じて、ジョブの新しいタイトルと説明を入力します。
   * ハンドラーが次のステップに進む場合は、「**[!UICONTROL ハンドラー処理の設定]**」を選択します。
   * 「**[!UICONTROL タイムアウト]**」フィールドに、外部プロセスのタイムアウト（秒）を入力します。
   * 「**[!UICONTROL 期間]**」フィールドに、外部プロセスが完了したかどうかを確認するポーリング間隔（秒）を入力します。
   * 「**[!UICONTROL バッチ]**」フィールドに、Dynamic Media サーバーのアップロードジョブのバッチ処理で処理するアセットの最大数（50～1,000）を入力します。
   * タイムアウトに達したときに先に進む場合は、「**[!UICONTROL タイムアウトで先に進む]**」を選択します。タイムアウトに達したときにインボックスまで進む場合は、選択を解除します。

   ![プロパティダイアログボックス](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. **[!UICONTROL Scene7 へのバッチアップロード - ステップのプロパティ]**&#x200B;ダイアログボックスの右上隅にある「**[!UICONTROL 完了]**」をタップします。

1. 「Scene7：アセットを再処理」ワークフローモデルページの右上隅にある「**[!UICONTROL 同期]**」をタップします。「**[!UICONTROL 同期済み]**」と表示された場合、ワークフローランタイムモデルは正常に同期されており、フォルダー内のアセットを再処理する準備が整います。

   ![ワークフローモデルの同期](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 「Scene7：アセットを再処理」ワークフローモデルを表示しているブラウザータブを閉じます。

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
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
