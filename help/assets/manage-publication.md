---
title: 公開を管理
description: Experience Manager Assets、Dynamic MediaおよびBrand Portalへのアセットの公開または非公開
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: ca01102673211f17e58af36ef2a59d0e964022d5
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 15%

---

# Experience Manager Assetsで公開を管理 {#manage-publication-in-aem}

As a [!DNL Adobe Experience Manager Assets] 管理者は、アセットやアセットを含むフォルダーをオーサーインスタンスからに公開できます [!DNL Experience Manager Assets], [!DNL Dynamic Media]、および [!DNL Brand Portal]. また、アセットまたはフォルダーの公開ワークフローを後の日時にスケジューリングすることもできます。公開すると、ユーザーはアセットにアクセスし、さらに他のユーザーに配布できます。 デフォルトでは、にアセットおよびフォルダーを公開できます。 [!DNL Experience Manager Assets]. ただし、 [!DNL Experience Manager Assets] 公開を有効にする [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) および [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

次のいずれかを使用して、アセットレベルまたはフォルダーレベルでアセットを公開または非公開にできます。 **[!UICONTROL クイック公開]** または **[!UICONTROL 公開を管理]** オプションは [!DNL Experience Manager Assets] インターフェイス。 その後、 [!DNL Experience Manager Assets]から再公開するまで、変更はパブリッシュインスタンスに反映されません。 [!DNL Experience Manager Assets]. これにより、作業中の変更がパブリッシュインスタンスで使用できなくなります。 パブリッシュインスタンスでは、管理者が公開した承認済みの変更のみを使用できます。

* [クイック公開を使用したアセットの公開](#quick-publish)
* [「公開を管理」を使用したアセットの公開](#manage-publication)
* [アセットを後で公開](#publish-assets-later)
* [Dynamic Mediaへのアセットの公開](#publish-assets-to-dynamic-media)
* [Brand Portal へのアセットの公開](#publish-assets-to-brand-portal)
* [制限事項とヒント](#limitations-and-tips)

## クイック公開を使用したアセットの公開 {#quick-publish}

クイック公開を使用すると、選択した宛先にコンテンツを直ちに公開できます。 次の [!DNL Experience Manager Assets] コンソールで、親フォルダーに移動し、公開するすべてのアセットまたはフォルダーを選択します。 クリック **[!UICONTROL クイック公開]** オプションを選択し、ドロップダウンリストからアセットを公開する宛先を選択します。

![クイック公開](assets/quick-publish-to-aem.png)

## 「公開を管理」を使用したアセットの公開 {#manage-publication}

「公開を管理」を使用すると、選択した宛先に対して、またはその宛先からコンテンツを公開または非公開にできます。 [コンテンツを追加](#add-content) を DAM リポジトリー全体の発行リストに追加する [フォルダ設定を含める](#include-folder-settings) 選択したフォルダーのコンテンツを公開し、フィルターを適用するには、次の手順に従います。 [公開をスケジュール](#publish-assets-later) を後の日時に変更する必要があります。

次の [!DNL Experience Manager Assets] コンソールで、親フォルダーに移動し、公開するすべてのアセットまたはフォルダーを選択します。 クリック **[!UICONTROL 公開を管理]** 」オプションを使用します。 次の条件を満たしていない場合、 [!DNL Dynamic Media] および [!DNL Brand Portal] で [!DNL Experience Manager Assets] インスタンスは、アセットおよびフォルダーのみをに公開できます。 [!DNL Experience Manager Assets].

![公開を管理](assets/manage-publication-aem.png)

以下のオプションを [!UICONTROL 公開を管理] インターフェイス：

* [!UICONTROL アクション]
   * `Publish`:選択した宛先へのアセットおよびフォルダーの公開
   * `Unpublish`:アセットおよびフォルダーを宛先から非公開にする

* [!UICONTROL 移動先]
   * `Publish`:へのアセットおよびフォルダーの公開 [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`:へのアセットの公開 [!DNL Dynamic Media]
   * `Brand Portal`:へのアセットおよびフォルダーの公開 [!DNL Brand Portal]

* [!UICONTROL スケジュール設定]
   * `Now`:アセットを直ちに公開する
   * `Later`:に基づいてアセットを公開する `Activation` 日時

続行するには、 **[!UICONTROL 次へ]**. 選択に基づいて、 **[!UICONTROL 範囲]** 「 」タブには、様々なオプションが表示されます。 次のオプションがあります。 **[!UICONTROL コンテンツを追加]** および **[!UICONTROL フォルダ設定を含める]** は、アセットとフォルダーを [!DNL Experience Manager Assets] (`Destination: Publish`) をクリックします。

![公開を管理での範囲](assets/manage-publication-aem-scope.png)

### コンテンツの追加 {#add-content}

への公開 [!DNL Experience Manager Assets] 発行リストにコンテンツ（アセットやフォルダー）をさらに追加できます。 dam リポジトリー全体で、リストにさらにアセットやフォルダーを追加できます。 クリック **[!UICONTROL コンテンツを追加]** ボタンをクリックして、コンテンツを追加します。

1 つのフォルダーから複数のアセットを追加したり、一度に複数のフォルダーを追加したりできます。 ただし、一度に複数のフォルダーからアセットを追加することはできません。

![コンテンツの追加](assets/manage-publication-add-content.png)

### フォルダー設定を含む {#include-folder-settings}

デフォルトでは、へのフォルダーの公開 [!DNL Experience Manager Assets] は、すべてのアセット、サブフォルダーおよびその参照を公開します。

公開するフォルダーコンテンツをフィルターするには、 **[!UICONTROL フォルダ設定を含める]**:

* `Include folder contents`

   * 有効：選択したフォルダーのすべてのアセット、サブフォルダー（サブフォルダーのすべてのアセットを含む）、および参照が公開されます。
   * 無効：選択したフォルダー（空）と参照のみが公開されます。 選択したフォルダーのアセットは公開されていません。

* `Include folder contents` および `Include only immediate folder contents`

   両方のオプションを選択した場合、選択したフォルダー、サブフォルダー（空）、参照のすべてのアセットが公開されます。 サブフォルダーのアセットは公開されません。

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![フォルダー設定を含む](assets/manage-publication-include-folder-settings.png)

フィルターを適用したら、 **[!UICONTROL OK]**&#x200B;をクリックし、 **[!UICONTROL 公開]**. 「公開」ボタンをクリックすると、確認メッセージが表示されます `Resource(s) have been scheduled for publication` が表示されます。 また、選択したアセットと（または）フォルダーは、スケジューラー (`Now` または `Later`) をクリックします。 パブリッシュインスタンスにログインして、アセットと（または）フォルダーが正常に公開されたことを確認します。

![AEM に公開](assets/manage-publication-publish-aem.png)

上の図では、 **[!UICONTROL 公開ターゲット]** 属性。 ～への投稿を選択したという事実を思い出してみましょう。 [!DNL Experience Manager Assets] (`Destination: Publish`) をクリックします。 次に、フォルダーとアセットのみがに公開されていることを示すのはなぜですか？ `AEM`」と入力し、他の 2 つのアセットは両方に公開されます `AEM` および `Dynamic Media`?

ここでは、フォルダープロパティの役割を理解する必要があります。 フォルダーの **[!UICONTROL Dynamic Media Publishing Mode]** プロパティは、パブリッシュに重要な役割を果たします。 フォルダーのプロパティを表示するには、フォルダーを選択し、 **[!UICONTROL プロパティ]** をクリックします。 アセットの親フォルダーのプロパティを表示する。

次の表で、定義した **[!UICONTROL 宛先]** および **[!UICONTROL Dynamic Media公開モード]**:

| [!UICONTROL 移動先] | [!UICONTROL Dynamic Media 公開モード] | [!UICONTROL 公開ターゲット] | 許可されたコンテンツ |
| --- | --- | --- | --- |
| 公開 | 選択的公開 | `AEM` | アセットおよびフォルダー |
| 公開 | 即時 | `AEM` および `Dynamic Media` | アセットおよびフォルダー |
| 公開 | アクティベーション時 | `AEM` および `Dynamic Media` | アセットおよびフォルダー |
| Dynamic Media | 選択的公開 | `Dynamic Media` | アセット |
| Dynamic Media | 即時 | `None` | アセットを公開できません |
| Dynamic Media | アクティベーション時 | `None` | アセットを公開できません |

>[!NOTE]
>
>に公開されるのはアセットのみ [!DNL Dynamic Media].
>
>へのフォルダーの公開 [!DNL Dynamic Media] はサポートされていません。
>
>フォルダー (`Selective Publish`) をクリックし、 [!DNL Dynamic Media] 宛先、 [!UICONTROL 公開ターゲット] 属性の反映 `None`.


次に、 **[!UICONTROL 宛先]** 上記の使用例では、 **[!UICONTROL Dynamic Media]** 結果を確認します。 これにより、 `Selective Publish` フォルダーが [!DNL Dynamic Media]. のアセット `Immediate` および `Upon Activation` フォルダは公開されず、を反映します。 `None`.

![Dynamic Media に公開](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>If [!DNL Dynamic Media] は、 [!DNL Experience Manager Assets] インスタンスと **[!UICONTROL 宛先]** が **[!UICONTROL 公開]**&#x200B;を使用すると、アセットとフォルダーは常にに公開されます。 `AEM`.
>
>への公開 [!DNL Brand Portal] は、フォルダーのプロパティとは無関係です。 すべてのアセット、フォルダーおよびコレクションをBrand Portalに公開できます。 詳しくは、 [Brand Portalへのアセットの公開](#publish-assets-to-brand-portal).

>[!NOTE]
>
>既に [!DNL Manage Publication] ウィザードを使用すると、カスタマイズは既存の機能で引き続き動作します。
>
>ただし、既存のカスタマイズを削除して新しい [!DNL Manager Publication] 機能。


## アセットを後で公開 {#publish-assets-later}

アセットの公開ワークフローを後の日時にスケジュールするには、次の手順を実行します。

1. 次の [!UICONTROL Experience Manager Assets] コンソールで、親フォルダーに移動し、公開のスケジュールを設定するすべてのアセットまたはフォルダーを選択します。
1. クリック **[!UICONTROL 公開を管理]** 」オプションを使用します。
1. クリック **[!UICONTROL 公開]** から **[!UICONTROL アクション]**&#x200B;をクリックし、 **[!UICONTROL 宛先]** コンテンツの公開先。
1. 「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 後で]**」を選択します。
1. を選択します。 **[!UICONTROL 有効化日]** 日時を指定します。 「**[!UICONTROL 次へ]**」をクリックします。

   ![公開を管理ワークフロー](assets/manage-publication-workflow.png)

1. 内 **[!UICONTROL 範囲]** タブ、 **[!UICONTROL コンテンツを追加]** （必要に応じて）。 「**[!UICONTROL 次へ]**」をクリックします。
1. 内 **[!UICONTROL ワークフロー]** 「 」タブで、「ワークフロータイトル」を指定します。 「**[!UICONTROL 後で公開する]**」をクリックします。

   ![ワークフロータイトル](assets/manage-publication-workflow-title.png)

   宛先インスタンスにログインして、公開されたアセットを検証します（スケジュールされた日時に応じて異なります）。

## Dynamic Mediaへのアセットの公開 {#publish-assets-to-dynamic-media}

に公開されるのはアセットのみ [!DNL Dynamic Media]. ただし、公開動作はフォルダーのプロパティによって異なります。 フォルダーには **[!UICONTROL Dynamic Media公開モード]** 次のいずれかを選択的公開用に設定されます。

* `Selective Publish`
* `Immediate`
* `Upon Activation`

の公開プロセス **[!UICONTROL 即時]** および **[!UICONTROL アクティベーション時]** モードは一貫していますが、次の場合は異なります： **[!UICONTROL 選択的公開]**. 詳しくは、 [Dynamic Mediaのフォルダーレベルでの選択的公開の設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). フォルダーで選択的公開を設定した後、次の操作を行うことができます。

* [「公開を管理」を使用して、Dynamic MediaまたはExperience Managerにアセットを選択的に公開する](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [「公開を管理」を使用した、Dynamic Media または Experience Manager からのアセットの選択的非公開 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [「クイック公開」を使用した、Dynamic Media または Experience Manager へのアセットの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [検索結果を使用して、アセットを選択的に公開または非公開にする](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

アセット、フォルダーおよびコレクションを [!DNL Experience Manager Assets Brand Portal] インスタンス。

* [Brand Portal へのアセットの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Brand Portal へのフォルダーの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Brand Portal へのコレクションの公開](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## 制限事項とヒント {#limitations-and-tips}

* 「[!UICONTROL 公開を管理]」のオプションは、レプリケーション権限を持つユーザーアカウントでのみ使用できます。
* 空のフォルダーは公開されません。
* 処理中のアセットを公開した場合は、オリジナルのコンテンツのみが公開されます。処理中のレンディションは失われます。処理が完了するのを待ち、処理が完了したら、アセットを公開または再公開します。
* 複雑なアセットを非公開にする場合は、アセットだけを非公開にします。参照は他の公開済みアセットによって参照される可能性があるので、非公開にしないでください。
