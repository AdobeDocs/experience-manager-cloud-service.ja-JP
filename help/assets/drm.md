---
title: Digital Rights Management [!DNL Adobe Experience Manager Assets] inas a Cloud Service」を参照してください。
description: Learn how to manage asset expiration states and information for licensed assets in [!DNL Experience Manager] as a Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31b8db4403dff1934033e1ed93651a076dba7a1a
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 63%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

デジタルアセットは多くの場合、利用条件と使用期間を指定するライセンスに関連付けられます。 Because [!DNL Adobe Experience Manager Assets] is fully integrated with the [!DNL Experience Manager] platform, you can efficiently manage asset expiration information and asset states. ライセンス情報をアセットに関連付けることもできます。

## アセットの有効期限 {#asset-expiration}

アセットの有効期限は、アセットのライセンス要件を適用するのに効果的な方法です。 公開済みアセットの有効期限が切れたらアセットを非公開にすることで、ライセンス違反が発生する可能性を回避します。管理者権限を持たないユーザーは、期限切れのアセットを編集、コピー、移動、発行およびダウンロードすることはできません。

次の場所で、アセットの有効期限切れのステータスを確認できます。

* **カード表示**：有効期限切れのアセットの場合、カードのフラグが有効期限切れを示します。
* **リスト表示**：有効期限切れのアセットの場合、「**[!UICONTROL スタータス]**」列に「**[!UICONTROL 期限切れ]**」のバナーが表示されます。
* **タイムライン**：アセットの有効期限切れのステータスを確認できます。アセットを選択し、「タイムライン」を選択します。
* **参照レール**：アセットの有効期限切れのステータスは、**[!UICONTROL 参照]**&#x200B;レールからも確認できます。ここではアセットの有効期限切れのステータスと、複合アセットと参照元のサブアセット、コレクションおよびプロジェクトの間の関係を管理します。

1. 参照先の Web ページと複合アセットを表示するアセットに移動します。
1. アセットを選択し、 [!DNL Experience Manager] ロゴをクリックします。
1. メニューで「**[!UICONTROL 参照]**」を選択します。
1. 有効期限切れのアセットの場合、参照レールの上部に有効期限切れのステータス「**[!UICONTROL アセットは期限切れです]**」が表示されます。アセットに有効期限切れのサブアセットがある場合、参照レールにステータス「**[!UICONTROL アセットに有効期限切れのサブアセットがあります]**」が表示されます。

### 有効期限切れのアセットの検索 {#search-expired-assets}

検索パネルで、有効期限切れのアセット（有効期限切れのサブアセットを含む）を検索できます。

1. In the [!DNL Assets] console, click the **[!UICONTROL Search]** in the toolbar to display the Omnisearch box.

1. オムニサーチボックスのカーソルで、Enter キーを押して検索結果ページを表示します。

1. グローバルナビゲーションアイコンをクリックして、検索パネルを表示します。

1. 「**[!UICONTROL 有効期限ステータス]**」オプションをクリックまたはタップしてそれを展開します。

1. 「**[!UICONTROL 期限切れ]**」を選択します。有効期限切れのアセットが検索結果に表示されます。

When you choose the **[!UICONTROL Expired]** option, the [!DNL Assets] console only displays the expired assets and subassets that are referenced by compound assets. 有効期限切れのサブアセットを参照する複合アセットは、サブアセットの有効期限切れの直後には表示されません。Instead, they are displayed after [!DNL Experience Manager] detects that they reference expired subassets the next time the scheduler runs.

公開済みアセットの有効期限をスケジューラーの現在のサイクルより前の日付に変更する場合、スケジューラーは次回の実行時にも引き続きこのアセットを有効期限切れのアセットとして検出し、ステータスにそれを反映させます。

さらに、何らかの誤作動やエラーによりスケジューラーが現在のサイクルの有効期限切れアセットを検出できない場合、スケジューラーはこれらのアセットを次回のサイクルで再確認し、有効期限切れのステータスを検出します。

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. Open [!DNL Experience Manager] Configuration Manager.
1. 「**[!UICONTROL Adobe CQ DAM Expiry Notification]**」を選択します。デフォルトでは、「**[!UICONTROL Time based Scheduler]**」が選択されており、指定の時間にアセットに有効期限切れのサブアセットがあるかどうかをチェックするジョブのスケジュールを設定します。ジョブが完了すると、有効期限切れのサブアセットを持つアセットと参照元のアセットが検索結果に有効期限切れと表示されます。

1. ジョブを定期的に実行するには、「**[!UICONTROL Time Based Scheduler Rule]**」フィールドをクリアして、「**[!UICONTROL Periodic Scheduler]**」フィールドの時間（秒数）を変更します。例えば、「0 0 0 &amp;ast; &amp;ast; ?」と指定するとジョブが 00 時間でトリガーされます。

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. 「**[!UICONTROL Prior notification in seconds]**」フィールドで、アセットの有効期限が切れる何秒前に有効期限切れに関する通知を受け取るかを指定します。管理者かアセットの作成者の場合、アセットの有効期限が切れる前に、指定の時間が経過した後にアセットの有効期限が切れることを知らせるメッセージを受け取ります。

   アセットの有効期限が切れると、有効期限が切れたことを知らせる別の通知を受け取ります。さらに、有効期限切れのアセットはアクティベートが解除されます。

1. 「**[!UICONTROL 保存]**」をクリックします。

## アセットの状態 {#asset-states}

コン [!DNL Assets] ソールには、アセットの様々な状態を表示できます。 特定のアセットの現在の状態により、カード表示にその状態について記述されたラベル（期限切れ、公開済み、承認済み、拒否など）が表示されます。

1. In the [!DNL Assets] user interface, select an asset.

1. Click **[!UICONTROL Publish]** from the toolbar. If you don&#39;t see **Publish** on the toolbar, click **[!UICONTROL More]** on the toolbar and locate **[!UICONTROL Publish]** option.

1. メニューの「**[!UICONTROL 公開]**」を選択して、確認ダイアログを閉じます。
1. 選択モードを終了します。アセットの公開ステータスは、カード表示のアセットのサムネールの下部に表示されます。リスト表示では、「公開」列にアセットが公開された時間が表示されます。

1. アセットの詳細ページを表示するには、インター [!DNL Assets] フェイスでアセットを選択し、「 **[!UICONTROL プロパティ]**」をクリックします。

1. In the [!UICONTROL Advanced] tab, set an expiration date for the asset from the **[!UICONTROL Expires]** field.

1. 「**[!UICONTROL 保存]**」をクリックし、次に「**[!UICONTROL 閉じる]**」をクリックしてアセットコンソールを表示します。
1. アセットの公開ステータスは、カード表示のアセットのサムネールの下部に、有効期限切れのステータスを示します。リスト表示では、アセットのステータスが「**[!UICONTROL 期限切れ]**」と表示されます。

1. In the [!DNL Assets] console, select a folder and create a review task on the folder.
1. レビュータスクでアセットを承認または拒否して、「**[!UICONTROL 完了]**」をクリックします。
1. レビュータスクを作成するフォルダーに移動します。承認または拒否したアセットのステータスがカード表示の下部に表示されます。リスト表示では、承認および有効期限のステータスが該当する列に表示されます。

1. To search for assets based on their status, click **[!UICONTROL Search]** to display the Omnisearch bar.

1. Returnキーを押し、をクリック [!DNL Experience Manager] して検索パネルを表示します。
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

1. 有効期限切れのステータスに基づいてアセットを検索するには、検索パネルで「**[!UICONTROL 有効期限ステータス]**」を選択して適切なオプションを選択します。

1. 各種検索ファセットで、ステータスの組み合わせに基づいてアセットを検索することもできます。検索ファセットで適切なオプションを選択することで、例えば、レビュータスクで承認されており、まだ有効期限が切れていない公開済みのアセットを検索することもできます。

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

This feature enforces the acceptance of the license agreement before you can download a licensed asset from [!DNL Adobe Experience Manager Assets].

If you select a protected asset and click **[!UICONTROL Download]**, you are redirected to a license page to accept the license agreement. If you do not accept the license agreement, the **[!UICONTROL Download]** option is not available.

選択した項目に保護されたアセットが複数含まれている場合、一度に 1 つずつアセットを選択し、使用許諾契約書に同意し、アセットのダウンロードに進みます。

アセットは、次のいずれかの条件が満たされた場合に保護されていると見なされます。

* アセットのメタデータプロパティ `xmpRights:WebStatement` が、そのアセットの使用許諾契約書を含む ページのパスを指している。
* アセットのメタデータプロパティ `adobe_dam:restrictions` の値が、使用許諾契約書を指定する生の HTML である。

>[!NOTE]
>
> の以前のリリースにライセンスを保存するために使用されていた場所 `/etc/dam/drm/licences` は非推奨（廃止予定）となりました。[!DNL Experience Manager]
>
>If you create or modify licence pages, or port them from previous [!DNL Experience Manager] releases, Adobe recommends that you store them under `/apps/settings/dam/drm/licenses` or `/conf/*/settings/dam/drm/licenses`.

### DRM保護されたアセットのダウンロード {#downloading-drm-assets}

1. In the card view, select the assets you want to download and click **[!UICONTROL Download]**.
1. **[!UICONTROL 著作権管理]**&#x200B;ページで、ダウンロードするアセットをリストから選択します。
1. [ [!UICONTROL License] ]ペインで、[ **[!UICONTROL Agree]**]を選択します。 アセットの横にチェックマークが表示されます。 Click the **[!UICONTROL Download]** option.

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. 保護された複数のアセットの使用許諾契約に同時に承諾するには、リストからアセットを選択して「**[!UICONTROL 同意する]**」を選択します。

1. In the dialog, click **[!UICONTROL Download]** to download the asset or its renditions.
