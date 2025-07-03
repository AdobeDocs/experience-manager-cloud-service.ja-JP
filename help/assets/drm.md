---
title: ' [!DNL Assets] のデジタル著作権管理'
description: ' [!DNL Experience Manager]  as a  [!DNL Cloud Service] でライセンスされているアセットの有効期限の状態と情報を管理する方法について説明します。'
contentOwner: AG
feature: Asset Management,DRM
role: User, Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '1368'
ht-degree: 100%

---

# デジタルアセットのデジタル著作権管理 {#digital-rights-management-in-assets}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

多くの場合、デジタルアセットは、利用の条件と期間を明記したライセンスに関連付けられています。[!DNL Experience Manager] プラットフォームを使用すると、アセットの有効期限に関する情報とライセンス情報を効率的に管理できます。

## アセットの有効期限 {#asset-expiration}

アセットにライセンス要件を適用するには、アセットの有効期限に関する情報を使用します。有効期限の情報に基づいて、公開済みアセットの有効期限が切れたときにアセットを非公開にすることで、ライセンス違反を防ぐことができます。管理者権限のないユーザーは、有効期限切れのアセットを編集、コピー、移動、公開、ダウンロードできません。

次の場所で、アセットの有効期限切れのステータスを確認できます。

* **カード表示**：有効期限切れのアセットの場合、カードのフラグが有効期限切れを示します。
* **リスト表示**：有効期限切れのアセットの場合、「**[!UICONTROL ステータス]**」列に「**[!UICONTROL 期限切れ]**」のバナーが表示されます。
* **タイムライン**：アセットの有効期限切れのステータスを確認できます。アセットを選択し、「タイムライン」を選択します。
* **参照レール**：アセットの有効期限切れのステータスは、**[!UICONTROL 参照]**&#x200B;レールからも確認できます。ここではアセットの有効期限切れのステータスと、複合アセットと参照元のサブアセット、コレクションおよびプロジェクトの間の関係を管理します。

参照元の Web ページとアセットの複合アセットを表示するには、次の手順に従います。

1. アセットに移動して選択し、![左パネルのコンテンツ参照アイコン](assets/do-not-localize/content-rail-icon.png) アイコンをクリックします。左パネルが開きます。
1. 左パネルの「**[!UICONTROL 参照]**」を選択します。
1. 期限切れアセットの場合、[!UICONTROL 参照]には有効期限ステータスが「**[!UICONTROL アセットは期限切れです]**」と表示されます。アセットに有効期限切れのサブアセットがある場合、[!UICONTROL 参照]レールにステータス「**[!UICONTROL アセットに有効期限切れのサブアセットがあります]**」が表示されます。

### 有効期限切れのアセットの検索 {#search-expired-assets}

有効期限切れのサブアセットなど、有効期限切れのアセットを検索するには、次の手順に従います。

1. [!DNL Assets] コンソールで、ツールバーの「**[!UICONTROL 検索]**」をクリックし、`Enter` キーを押します。

1. グローバルナビゲーションアイコンをクリックし、「**[!UICONTROL 有効期限ステータス]**」オプションを選択します。

1. 「**[!UICONTROL 期限切れ]**」を選択します。検索結果に、有効期限切れのアセットが表示されます。

「**[!UICONTROL 期限切れ]**」オプションを選択すると、[!DNL Assets] コンソールに複合アセットによって参照されている有効期限切れのアセットとサブセットのみが表示されます。有効期限切れのサブアセットを参照する複合アセットは、サブアセットの有効期限切れの直後には表示されません。代わりに、次回スケジューラーが実行されたときに、それらのアセットが有効期限切れのサブアセットを参照していることを [!DNL Experience Manager] が検出した後で表示されます。

公開済みアセットの有効期限を、現在のスケジューラーサイクルより前の日付に変更できます。ただし、次回実行時には、スケジュールがそうしたアセットを期限切れアセットとして検出し、[!DNL Experience Manager] はレポートにそのステータスを反映します。アセットの有効期限の表示はタイムゾーンごとに異なります。

また、エラーによりスケジューラーが現在のサイクルの有効期限切れアセットを検出できない場合、スケジューラーはこれらのアセットを次回のサイクルで再確認し、有効期限切れのステータスを検出します。

[!DNL Assets] コンソールに有効期限切れのサブアセットと共に参照先の複合アセットを表示するには、[!DNL Experience Manager] で **[!UICONTROL Adobe CQ DAM Expiry Notification]** ワークフローを設定します。時間ベースのスケジューラーは、アセットに有効期限切れのサブアセットがあるかどうかを特定の時刻に確認するように、ジョブのスケジュールを設定します。ジョブが完了すると、有効期限切れのサブアセットを持つアセットと参照元のアセットが検索結果に有効期限切れと表示されます。

1. 環境に関連付けられた [!DNL Cloud Manager] Git リポジトリーにアクセスします。
1. Git リポジトリーにある、`com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` という名前のファイルを、次の内容でコミットします。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 詳しくは、[ [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md) 内で OSGi 設定を行う方法を参照してください。

以下のプロパティを使用して、スケジューラーを設定できます。

* `cq.dam.expiry.notification.scheduler.istimebased` プロパティの値が `true` の場合、スケジューラーが開始されます。* `cq.dam.expiry.notification.scheduler.timebased.rule` プロパティの値は、時間を定義する正規表現です。上記の例では、00 時にスケジューラージョブを開始します。
* `send_email` を `true` に設定した場合、アセットの有効期限が切れると、アセットの作成者（[!DNL Assets] に特定のアセットをアップロードしたユーザー）のみがメールを受け取ります。
* スケジューラーの 1 回の繰り返しで期限切れになるアセットの最大数は、`asset_expired_limit` プロパティの値です。
* ジョブを定期的に実行するには、`cq.dam.expiry.notification.scheduler.istimebased` プロパティの値を `false` に設定し、`cq.dam.expiry.notification.scheduler.period.rule` プロパティの値を秒単位の時間で設定します。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## アセットの状態 {#asset-states}

[!DNL Assets] コンソールには、アセットの様々な状態を表示できます。特定のアセットの現在の状態により、カード表示にその状態について記述されたラベル（期限切れ、公開済み、承認済み、拒否など）が表示されます。

1. [!DNL Assets] ユーザーインターフェイスでアセットを選択します。

1. ツールバーの「**[!UICONTROL 公開]**」を選択します。ツールバーに「[!UICONTROL 公開]」オプションが表示されていない場合は、ツールバーの「**[!UICONTROL 詳細]**」をクリックして「**[!UICONTROL 公開]**」オプションを見つけます。

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

1. 「`Return`」を選択し、「[!DNL Experience Manager]」をクリックします。

1. 検索パネルで、「**[!UICONTROL 公開ステータス]**」をクリックして「**[!UICONTROL 公開済み]**」を選択し、[!DNL Assets] で公開済みのアセットを検索します。

1. 承認済みまたは却下されたアセットを検索するには、「**[!UICONTROL 承認ステータス]**」を選択し、適切なオプションを選択します。

1. 有効期限切れのステータスに基づいてアセットを検索するには、検索パネルで「**[!UICONTROL 有効期限ステータス]**」を選択して適切なオプションを選択します。

1. 各種検索ファセットで、ステータスの組み合わせに基づいてアセットを検索することもできます。例えば、レビュータスクで承認された、期限切れでない公開済みアセットを検索できます。このようなアセットを検索するには、検索ファセットで適切なオプションを選択します。

## [!DNL Assets] のデジタル著作権管理 {#digital-rights-management-in-assets-1}

DRM 機能は、[!DNL Assets] からライセンスの必要なアセットをダウンロードする前に、使用許諾契約書への同意を求めます。

保護されたアセットを選択して「**[!UICONTROL ダウンロード]**」をクリックすると、ライセンスページが表示されるので、このページで使用許諾契約書に同意します。使用許諾契約に同意しない場合、「**[!UICONTROL ダウンロード]**」オプションは使用できません。

選択した項目に保護されたアセットが複数含まれている場合、一度に 1 つずつアセットを選択し、使用許諾契約書に同意し、アセットのダウンロードに進みます。

アセットは、次のいずれかの条件が満たされた場合に保護されていると見なされます。

* アセットのメタデータプロパティ `xmpRights:WebStatement` が、そのアセットの使用許諾契約書を含むページのパスを指している。
* アセットのメタデータプロパティ `adobe_dam:restrictions` の値が、使用許諾契約書を指定する生の HTML である。

>[!NOTE]
>
>場所 `/etc/dam/drm/licences` は、[!DNL Experience Manager] の以前のリリースでライセンスの保存に使用されていました。現在、この場所は非推奨（廃止予定）となっています。ライセンスページを作成または変更する場合、または [!DNL Experience Manager] の以前のリリースからページを移植する場合は、そうしたアセットを `/apps/settings/dam/drm/licenses` または `/conf/*/settings/dam/drm/licenses` の場所に保存することをお勧めします。

### DRM で保護されたアセットのダウンロード {#downloading-drm-assets}

1. カード表示で、ダウンロードするアセットを選択し、「**[!UICONTROL ダウンロード]**」を選択します。
1. **[!UICONTROL 著作権管理]**&#x200B;ページで、ダウンロードするアセットをリストから選択します。
1. [!UICONTROL ライセンス]パネルで、「**[!UICONTROL 同意する]**」を選択します。アセットの横にチェックマークが表示されます。「**[!UICONTROL ダウンロード]**」オプションを選択します。

   >[!NOTE]
   >
   >「**[!UICONTROL ダウンロード]**」オプションは、保護されたアセットの使用許諾契約に同意した場合にのみ有効になります。ただし、選択範囲が保護されたアセットと保護されていないアセットの両方で構成されている場合は、保護されたアセットのみがパネルに表示され、「**[!UICONTROL ダウンロード]**」オプションを使用して、保護されていないアセットをダウンロードできます。保護された複数のアセットの使用許諾契約に同時に承諾するには、リストからアセットを選択して「**[!UICONTROL 同意する]**」を選択します。

1. アセットまたはそのレンディションをダウンロードするには、ダイアログで「**[!UICONTROL ダウンロード]**」を選択します。

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
