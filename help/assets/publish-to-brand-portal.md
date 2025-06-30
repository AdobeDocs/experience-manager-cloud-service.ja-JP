---
title: Brand Portal へのアセット、フォルダーおよびコレクションの公開
description: アセット、フォルダーおよびコレクションを Brand Portal に公開します。
contentOwner: Adobe
feature: Brand Portal, Asset Distribution, Configuration
role: User
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 100%

---

# Brand Portal へアセットを公開 {#publish-assets-to-brand-portal}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/brandportal/brand-portal-publish-assets) |
| AEM as a Cloud Service | この記事 |

Adobe Experience Manager（AEM）Assets 管理者の場合、アセット、フォルダー、およびコレクションを AEM Assets Brand Portal インスタンスに公開できます。また、アセットまたはフォルダーの公開ワークフローを後の日時にスケジューリングすることもできます。公開すると、Brand Portal ユーザーはアセット、フォルダーおよびコレクションにアクセスでき、さらに他のユーザーに配布できます。

ただし、最初に AEM Assets を Brand Portal と連携するように設定する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

その後、AEM Assets でオリジナルのアセット、フォルダー、コレクションに変更を加えても、AEM Assets から再び公開しない限り、変更内容は Brand Portal に反映されません。このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

* [Brand Portal へのアセットの公開](#publish-assets-to-bp)
* [Brand Portal へのフォルダーの公開](#publish-folders-to-brand-portal)
* [Brand Portal へのコレクションの公開](#publish-collections-to-brand-portal)

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。
>>アセットは、バッチで公開する必要があります。 バッチサイズの推奨は 15K です。
>> の場合 [!DNL Experience Manager Assets] as a [!DNL Cloud Service]の場合、ラボ条件で観察される転送率は、1 時間あたり 1,000 アセットです。 この率は、平均サイズが 10 MB のアセットで測定されます。

## Brand Portal へのアセットの公開 {#publish-assets-to-bp}

AEM Assets から Brand Portal にアセットを公開する手順を次に示します。

1. アセットコンソールで、親フォルダーを開き、公開するすべてのアセットを選択し、ツールバーの「**[!UICONTROL クイック公開]**」オプションをクリックします。

   ![publish2bp-2](assets/publish2bp.png)

1. アセットを公開する方法は次の 2 つです。
   * [今すぐ公開](#publish-to-bp-now)（アセットをただちに公開）
   * [後で公開](#publish-to-bp-later)（アセットの公開をスケジュール）

### アセットを今すぐ公開 {#publish-to-bp-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL Brand Portal に公開]**」を選択します。

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal に公開]**」を選択します。

      「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。

      「**[!UICONTROL 次へ]**」をクリックします。

   2. 「**[!UICONTROL 範囲]**」の選択を確認し、「**[!UICONTROL Brand Portal に公開]**」をクリックします。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

### アセットを後で公開 {#publish-to-bp-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. 公開のスケジュールを設定するアセットを選択し、上部のツールバーの「**[!UICONTROL 公開を管理]**」をクリックします。

1. **[!UICONTROL 公開を管理]**&#x200B;ページで、「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal に公開]**」を選択します。

   「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 後で]**」を選択します。

   <!--![publishlaterbp-1](assets/publishlaterbp-1.png)-->

   ![後で公開する](assets/publish-later.png)

1. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**アクティベート日**」を選択して時刻を指定します。「**次へ**」をクリックします。

1. 「**[!UICONTROL ワークフロー]**」で&#x200B;**[!UICONTROL ワークフロータイトル]**&#x200B;を指定します。「**[!UICONTROL 後で公開する]**」をクリックします。

   <!--![publishworkflow](assets/publishworkflow.png)-->

   ![公開ワークフロー](assets/publish-workflow.png)

>[!NOTE]
>
> * DAM-Users グループの既存のユーザーは、パス「/conf/global/settings/cloudconfigs/mediaportal」に対する読み取りアクセス権を持ちます。
> * 新しいユーザー（または管理者以外のユーザー）は、brand portal に公開するために、次の権限が必要です。
>   > パス：
>   > `"/conf/global/settings/cloudconfigs/mediaportal" : jcr:read `
>   >`/libs : jcr:read`
>   >`/conf : jcr:read`
>   >`/content : jcr:read, crx:replicate`
>   >`/content/dam/ : jcr:read,modify, crx:replicate`

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal}

アセットフォルダーは、直ちに公開または非公開にしたり、後の日付や時間にスケジュールを設定したりできます。

### Brand Portal へのフォルダーの公開 {#publish-folders-to-bp}

1. アセットコンソールで、公開するフォルダーを選択し、ツールバーの「**[!UICONTROL クイック公開]**」オプションをクリックします。

   ![publish2bp](assets/publish2bp.png)

1. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * ツールバーで「**[!UICONTROL クイック公開]**」を選択します。

     メニューから「**[!UICONTROL Brand Portal に公開]**」を選択します。

   * ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

      1. 「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal に公開]**」を選択します。

         「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。

         「**次へ**」をクリックします。

      1. 「**[!UICONTROL 範囲]**」の選択を確認し、「**[!UICONTROL Brand Portal に公開]**」をクリックします。

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

1. **フォルダーを後で公開**：
アセットフォルダーの公開を後の日時にスケジュールするには、次の手順に従います。

   1. 公開のスケジュールを設定するフォルダーを選択し、上部のツールバーから「**[!UICONTROL 公開を管理]**」を選択します。
   1. 「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal に公開]**」を選択します。

      「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 後で]**」を選択します。

   1. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をクリックします。

      <!--![publishlaterbp](assets/publishlaterbp.png)-->

   ![フォルダーを後で公開](assets/publish-later-folder.png)

   1. 「**[!UICONTROL 範囲]**」で選択内容を確認します。「**[!UICONTROL 次へ]**」をクリックします。

   1. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。「**[!UICONTROL 後で公開する]**」をクリックします。

      <!--![manageschedulepub](assets/manageschedulepub.png)-->

   ![ワークフローの公開](assets/publish-workflow.png)

### Brand Portal に公開されたファイルまたはフォルダーの表示 {#view-published-file-folder}

1. Brand Portal インターフェイスにログインして、公開されたアセットを確認します（スケジュールを設定した日時に応じて異なります）。

   ![bp_landingpage](assets/bp_landingpage.png)

1. リスト表示 ![リスト表示](assets/list-view.svg) に切り替えて、アセットの現在の公開ステータスを確認します。

<!--2. On the [Asset Reports page](#https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/asset-reports), you can see the current state of the report job, for example, Success, Failed, Queued, or Scheduled.-->

![生成されたレポートのステータス](assets/report-status.JPG)

### Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

AEM Assets インスタンスから非公開にすることで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

アセットフォルダーを Brand Portal から直ちに非公開にしたり、日時を指定してスケジュールを設定したりできます。

Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. アセットコンソールで、公開するアセットフォルダーを選択し、ツールバーの「**[!UICONTROL 公開を管理]**」オプションをクリックします。

   ![publish2bp-1](assets/publish2bp.png)

1. **アセットフォルダーの非公開**

   選択したアセットフォルダーを Brand Portal から直ちに非公開にするには、次の手順を実行します。

   1. ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal から非公開]**」を選択します。

      「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。

      「**[!UICONTROL 次へ]**」をクリックします。

   1. 「**[!UICONTROL 範囲]**」の選択を確認し、「**[!UICONTROL Brand Portal から非公開]**」をクリックします。

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **アセットフォルダーを後で非公開にする**

   アセットフォルダーを後で非公開にするようにスケジュールを設定するには、次の手順を実行します。

   1. ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portal から非公開]**」を選択します。

      「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 後で]**」を選択します。

   1. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をクリックします。

   1. 「**[!UICONTROL 範囲]**」で選択内容を確認し、「**[!UICONTROL 次へ]**」をクリックします。

   1. 「**[!UICONTROL ワークフロー]**」で&#x200B;**[!UICONTROL ワークフロータイトル]**&#x200B;を指定します。「**[!UICONTROL 後で非公開にする]**」をクリックします。

      ![unpublishworkflows](assets/unpublishworkflows.png)

## Brand Portal へのコレクションの公開 {#publish-collections-to-brand-portal}

AEM Assets クラウドインスタンスからコレクションを公開または非公開にできます。

>[!NOTE]
>
>コンテンツフラグメントは Brand Portal に公開できません。したがって、AEM Assets インスタンスでコンテンツフラグメントを選択している場合は、「**[!UICONTROL Brand Portal に公開]**」アクションを使用できません。
>
>コンテンツフラグメントを含むコレクションを AEM Assets インスタンスから Brand Portal へ公開した場合は、そのフォルダー内のコンテンツフラグメントを除く全コンテンツが Brand Portal インターフェイスにレプリケートされます。

### コレクションの公開 {#publish-collections}

AEM Assets から Brand Portal にコレクションを公開する手順を次に示します。

1. AEM Assets の UI で AEM のロゴをクリックします。

1. **ナビゲーション**&#x200B;ページで、**[!UICONTROL アセット]**／**[!UICONTROL コレクション]**&#x200B;に移動します。

1. **コレクション**&#x200B;コンソールで Brand Portal に公開するコレクションを選択します。

   ![select_collection](assets/select_collection.png)

1. ツールバーで「**[!UICONTROL Brand Portal に公開]**」をクリックします。

1. 確認ダイアログで「**[!UICONTROL 公開]**」をクリックします。

1. 確認メッセージを閉じます。

   管理者として Brand Portal にログインします。公開したコレクションがコレクションインターフェイスで利用できます。

   ![公開コレクション](assets/published_collection.png)

### コレクションを非公開にする {#unpublish-collections}

AEM Assets インスタンスから非公開にすることで、Brand Portal に公開されているコレクションを削除できます。元のコレクションを非公開にすると、Brand Portal のユーザーはそのコピーを使用できなくなります。

コレクションを非公開にする手順は次のとおりです。

1. AEM Assets インスタンスの&#x200B;**コレクション**&#x200B;コンソールから、非公開にしたいコレクションを選択します。

   ![select_collection](assets/select_collection-1.png)

1. ツールバーで「**[!UICONTROL Brand Portal から削除]**」アイコンをクリックします。
1. 確認ダイアログで「**[!UICONTROL 非公開]**」をクリックします。
1. 確認メッセージを閉じます。コレクションが Brand Portal インターフェイスから削除されます。

上記に加えて、AEM Assets のメタデータスキーマ、画像プリセット、検索ファセット、タグを Brand Portal に公開することもできます。

* [Brand Portal へのプリセット、スキーマ、ファセットの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=ja)
* [Brand Portal へのタグの公開](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=ja)


詳しくは、[Brand Portal ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja)を参照してください。


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

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