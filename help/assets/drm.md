---
title: ' [!DNL Assets] のデジタル著作権管理'
description: ' [!DNL Experience Manager]  as a  [!DNL Cloud Service] でライセンスされているアセットの有効期限の状態と情報を管理する方法について説明します。'
contentOwner: AG
feature: アセット管理、DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 49%

---

# デジタルアセットのDigital Rights Management {#digital-rights-management-in-assets}

デジタルアセットは、多くの場合、利用条件と使用期間を指定したライセンスに関連付けられています。 [!DNL Experience Manager]プラットフォームを使用すると、アセットの有効期限に関する情報とライセンス情報を効率的に管理できます。

## アセットの有効期限 {#asset-expiration}

アセットのライセンス要件を適用するには、アセットの有効期限に関する情報を使用します。 有効期限情報により、公開済みアセットの有効期限が切れたときに非公開になり、ライセンス違反を防ぎます。 管理者権限のないユーザーは、有効期限切れのアセットを編集、コピー、移動、公開、ダウンロードできません。

次の場所で、アセットの有効期限切れのステータスを確認できます。

* **カード表示**：有効期限切れのアセットの場合、カードのフラグが有効期限切れを示します。
* **リスト表示**:有効期限切れのアセットの場合、「ステータ **** ス」列に「有効期限切れ」のバナーが **** 表示されます。
* **タイムライン**：アセットの有効期限切れのステータスを確認できます。アセットを選択し、「タイムライン」を選択します。
* **参照レール**：アセットの有効期限切れのステータスは、**[!UICONTROL 参照]**&#x200B;レールからも確認できます。ここではアセットの有効期限切れのステータスと、複合アセットと参照元のサブアセット、コレクションおよびプロジェクトの間の関係を管理します。

アセットの参照元のWebページと複合アセットを表示するには、次の手順に従います。

1. アセットに移動し、アセットを選択し、![左側のレールのコンテンツ参照アイコン](assets/do-not-localize/content-rail-icon.png)をクリックします。 左側のレールが開きます。
1. 左側のレールから「**[!UICONTROL 参照]**」を選択します。
1. 有効期限切れのアセットの場合、「[!UICONTROL 参照]」に有効期限切れのステータスが「**[!UICONTROL アセットは期限切れです]**」と表示されます。 アセットに有効期限切れのサブアセットがある場合、[!UICONTROL 参照]レールにステータス&#x200B;**[!UICONTROL アセットに有効期限切れのサブアセットがあります]**&#x200B;と表示されます。

### 有効期限切れのアセットの検索 {#search-expired-assets}

有効期限切れのサブアセットを含む有効期限切れのアセットを検索するには、次の手順に従います。

1. [!DNL Assets]コンソールで、ツールバーの「**[!UICONTROL 検索]**」をクリックし、`Enter`を押します。

1. グローバルナビゲーションアイコンをクリックし、「**[!UICONTROL 有効期限ステータス]**」オプションを選択します。

1. 「**[!UICONTROL 期限切れ]**」を選択します。検索結果に、有効期限切れのアセットが表示されます。

「**[!UICONTROL 期限切れ]**」オプションを選択すると、[!DNL Assets] コンソールに複合アセットによって参照されている有効期限切れのアセットとサブセットのみが表示されます。有効期限切れのサブアセットを参照する複合アセットは、サブアセットの有効期限切れの直後には表示されません。代わりに、[!DNL Experience Manager]が次回スケジューラーを実行したときに、それらのアセットが有効期限切れのサブアセットを参照していることを検出した後に表示されます。

公開済みアセットの有効期限を、現在のスケジューラーサイクルより前の日付に変更できます。 ただし、スケジュールは次回実行時に期限切れアセットとして検出し、[!DNL Experience Manager]はレポートにステータスを反映します。 アセットの有効期限の表示方法は、タイムゾーンごとに異なります。

さらに、エラーが発生し、スケジューラーが現在のサイクルの期限切れアセットを検出できない場合、スケジューラーは次のサイクルでこれらのアセットを再調べ、期限切れのステータスを検出します。

[!DNL Assets]コンソールに有効期限切れのサブアセットと共に参照元の複合アセットを表示するには、[!DNL Experience Manager]で&#x200B;**[!UICONTROL Adobe CQ DAM Expiry Notification]**&#x200B;ワークフローを設定します。 時間ベースのスケジューラーは、特定の時間にアセットに有効期限切れのサブアセットがあるかどうかをチェックするジョブのスケジュールを設定します。 ジョブが完了すると、有効期限切れのサブアセットを持つアセットと参照元のアセットが検索結果に有効期限切れと表示されます。

1. 環境に関連付けられた [!DNL Cloud Manager] Git リポジトリーにアクセスします。
1. Git リポジトリーにある、`com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` という名前のファイルを、次の内容でコミットします。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. [as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)のOSGi設定の実行方法に従います。 [!DNL Experience Manager] 

スケジューラーは、次のプロパティを使用して設定できます。

* プロパティ`cq.dam.expiry.notification.scheduler.istimebased`の`true`値がスケジューラーを開始します。 *プロパティ`cq.dam.expiry.notification.scheduler.timebased.rule`の値は、時間を定義する正規表現です。 上記の例では、00時間にスケジューラージョブが開始されます。
* `send_email`を`true`に設定すると、アセットの有効期限が切れたときに、アセットの作成者（特定のアセットを[!DNL Assets]にアップロードした人）に電子メールが送信されます。
* スケジューラーの1回の繰り返しで期限切れになるアセットの最大数は、プロパティ`asset_expired_limit`の値です。
* ジョブを定期的に実行するには、プロパティ`cq.dam.expiry.notification.scheduler.istimebased`の値を`false`に設定し、時間（秒）を指定してプロパティ`cq.dam.expiry.notification.scheduler.period.rule`の値を設定します。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## アセットの状態 {#asset-states}

[!DNL Assets] コンソールには、アセットの様々な状態を表示できます。特定のアセットの現在の状態により、カード表示にその状態について記述されたラベル（期限切れ、公開済み、承認済み、拒否など）が表示されます。

1. [!DNL Assets] ユーザーインターフェイスでアセットを選択します。

1. ツールバーの「**[!UICONTROL 公開]**」を選択します。 ツールバーに「[!UICONTROL 公開]」オプションが表示されない場合は、ツールバーの「**[!UICONTROL 詳細]**」をクリックして「**[!UICONTROL 公開]**」オプションを見つけます。

1. メニューの「**[!UICONTROL 公開]**」を選択して、確認ダイアログを閉じます。

1. 選択モードを終了します。アセットの公開ステータスは、カード表示のアセットのサムネールの下部に表示されます。リスト表示では、「公開」列にアセットが公開された時間が表示されます。

1. アセットの詳細ページを表示するには、[!DNL Assets] インターフェイスでアセットを選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「[!UICONTROL 詳細]」タブの「**[!UICONTROL 期限切れ]**」フィールドで、アセットの有効期限日を設定します。

1. 「**[!UICONTROL 保存]**」をクリックし、次に「**[!UICONTROL 閉じる]**」をクリックしてアセットコンソールを表示します。

1. アセットの公開ステータスは、カード表示のアセットのサムネールの下部に、有効期限切れのステータスを示します。リスト表示では、アセットのステータスが「**[!UICONTROL 期限切れ]**」と表示されます。

1. [!DNL Assets] コンソールで、フォルダーを選択してフォルダーにレビュータスクを作成します。

1. レビュータスクでアセットを承認または拒否して、「**[!UICONTROL 完了]**」をクリックします。

1. レビュータスクを作成するフォルダーに移動します。承認または拒否したアセットのステータスがカード表示の下部に表示されます。リスト表示では、承認および有効期限のステータスが該当する列に表示されます。

1. アセットをステータスに基づいて検索するには、「**[!UICONTROL 検索]**」をクリックして検索バーを表示します。

1. `Return`を選択し、[!DNL Experience Manager]をクリックします。

1. 検索パネルで、「**[!UICONTROL 公開ステータス]**」をクリックして「**[!UICONTROL 公開済み]**」を選択し、[!DNL Assets] で公開済みのアセットを検索します。

1. 承認済みまたは却下されたアセットを検索するには、「**[!UICONTROL 承認ステータス]**」を選択し、適切なオプションを選択します。

1. 有効期限切れのステータスに基づいてアセットを検索するには、検索パネルで「**[!UICONTROL 有効期限ステータス]**」を選択し、適切なオプションを選択します。

1. 各種検索ファセットで、ステータスの組み合わせに基づいてアセットを検索することもできます。例えば、レビュータスクで承認され、期限切れでない発行済みアセットを検索できます。 このようなアセットを検索するには、検索ファセットで適切なオプションを選択します。

## [!DNL Assets] のデジタル著作権管理 {#digital-rights-management-in-assets-1}

DRM機能は、[!DNL Assets]からライセンスの必要なアセットをダウンロードする前に、使用許諾契約への同意を強制します。

保護されたアセットを選択して「**[!UICONTROL ダウンロード]**」をクリックすると、ライセンスページが表示されるので、このページで使用許諾契約書に同意します。使用許諾契約に同意しない場合、「**[!UICONTROL ダウンロード]**」オプションは使用できません。

選択した項目に保護されたアセットが複数含まれている場合、一度に 1 つずつアセットを選択し、使用許諾契約書に同意し、アセットのダウンロードに進みます。

アセットは、次のいずれかの条件が満たされた場合に保護されていると見なされます。

* アセットのメタデータプロパティ `xmpRights:WebStatement` が、そのアセットの使用許諾契約書を含むページのパスを指している。
* アセットのメタデータプロパティ `adobe_dam:restrictions` の値が、使用許諾契約書を指定する生の HTML である。

>[!NOTE]
>
>`/etc/dam/drm/licences`は、以前のリリースの[!DNL Experience Manager]にライセンスを保存するために使用されていました。 場所は現在非推奨（廃止予定）となっています。 ライセンスページを作成または変更する場合、または以前の[!DNL Experience Manager]リリースのページを移植する場合は、Adobeでは、そのようなアセットを`/apps/settings/dam/drm/licenses`または`/conf/*/settings/dam/drm/licenses`の場所に保存することをお勧めします。

### DRM で保護されたアセットのダウンロード {#downloading-drm-assets}

1. カード表示で、ダウンロードするアセットを選択し、「**[!UICONTROL ダウンロード]**」を選択します。
1. **[!UICONTROL 著作権管理]**&#x200B;ページで、ダウンロードするアセットをリストから選択します。
1. [!UICONTROL ライセンス]パネルで、「**[!UICONTROL 同意する]**」を選択します。アセットの横にチェックマークが表示されます。「**[!UICONTROL ダウンロード]**」オプションを選択します。

   >[!NOTE]
   >
   >「**[!UICONTROL ダウンロード]**」オプションは、保護されたアセットの使用許諾契約に同意した場合にのみ有効になります。ただし、保護されたアセットと保護されていないアセットの両方を選択した場合は、保護されたアセットのみがウィンドウに表示され、「**[!UICONTROL ダウンロード]**」オプションを使用して保護されていないアセットをダウンロードできます。 保護された複数のアセットの使用許諾契約に同時に承諾するには、リストからアセットを選択して「**[!UICONTROL 同意する]**」を選択します。

1. アセットまたはそのレンディションをダウンロードするには、ダイアログで「**[!UICONTROL ダウンロード]**」を選択します。
