---
title: ' [!DNL AEM and Dynamic Media] へのクイック公開'
description: ' [!DNL Assets view]  のクイック公開を使用すると、アセットを  [!DNL AEM and Dynamic Media]  に同時または個別に公開できます。アセットとフォルダーを選択し、 [!DNL Dynamic Media]  または [!DNL AEM] に公開することを選択できます。'
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 92%

---

# [!DNL AEM and Dynamic Media] へのアセットの公開{#Publish-Assets-to-AEM-and-Dynamic-Media}

[!DNL Experience Manager Assets] を使用すると、[!DNL Assets view] を使用して [!DNL Experience Manager] と [!DNL Dynamic Media] にアセットをすばやく公開できます。これにより、 [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences) に切り替えることなく、[[!DNL Assets view]  を使用してアセットを管理し、公開できるようになります。

[!DNL Experience Manager Assets view] ビューでは、アセットを [!DNL AEM] や [!DNL Dynamic Media] に、またはその両方に同時に公開できる柔軟性が提供されます。アセットのアップロード、参照および検索時に、アセットを公開できます。アセットを公開するこれらのすべてのオプションについて詳しくは、この記事を参照してください。

## 開始する前に {#before-you-begin}

[!DNL AEM and Dynamic Media] の公開オプションを表示するには、次の設定を行います。

* [!DNL Dynamic Media] の公開オプションを表示するには、管理ビューを使用して、次の設定を行います。

   * [ [!DNL Dynamic Media] クラウド設定](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)を作成します。
   * フォルダーレベルで [!DNL Dynamic Media] 公開モードを設定します。これらの設定は、[!DNL Dynamic Media] クラウド設定の作成中にも設定できます。フォルダーレベルでこれらの設定を上書きする方法について詳しくは、[ [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md) のフォルダーレベルでの選択的公開の設定を参照してください。

* [!DNL AEM] の公開オプションを表示するには、環境に合わせて [!DNL AEM] パブリッシュエンドポイントを設定する必要があります。

## アップロード中のアセットの公開 {#piblish-assets-during-upload}

アセットをフォルダーにアップロードする際に、[!DNL AEM and Dynamic Media] にアセットを公開できます。表示される公開オプションは、アセットがアップロードされるフォルダーの [!DNL Dynamic Media] 公開モード設定によって異なります。[!DNL Dynamic Media]公開モードは、次のいずれかに設定できます。

* **[!UICONTROL アクティベーション時]：**&#x200B;アセットをこのフォルダーにアップロードする際は、URL／埋め込みリンクが提供される前に、まずアセットを明示的に公開する必要があります。

* **[!UICONTROL 即時]：**&#x200B;アセットをこのフォルダーにアップロードする際は、システムがアセットを Experience Manager に取り込み、URL／埋め込みを即時提供します。
* **[!UICONTROL 選択的公開]：**&#x200B;パブリックドメインでの配信用に、[!DNL Experience Manager] または [!DNL Dynamic Media] のいずれかにアセットを公開します。

### [!UICONTROL Dynamic Media 公開モード]を[!UICONTROL アクティベーション時]に設定 {#dynamic-media-publish-mode-set-to-upon-activation}

**[!UICONTROL アクティベーション時]**&#x200B;に [!DNL Dynamic Media Publish Mode] を設定したフォルダーへのアップロード中にアセットを公開するには、次のようにします。

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL アクティベーション時]**&#x200B;として表示されます。

   ![アクティベーション時のアップロード画像](/help/assets/assets/upload-uactivation.svg)

1. 「**[!UICONTROL AEM および Dynamic Media に公開]**」を選択し、「**[!UICONTROL アップロード]**」をクリックします。アセットは、[!DNL AEM and Dynamic Media] に同時に公開されます。これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### [!UICONTROL Dynamic Media 公開モード]を[!UICONTROL 即時]設定 {#dynamic-media-publish-mode-set-to-immediate}

[!UICONTROL Dynamic Media 公開モード]を&#x200B;**[!UICONTROL 即時]**&#x200B;設定したフォルダーへのアップロード中にアセットを公開するには、次のようにします。

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL 即時]**&#x200B;として表示されます。

   ![ファイルのアップロード画像 - 即時モード](/help/assets/assets/resized-image-pdf-svg-new.svg)

   [!UICONTROL Dynamic Media 公開モード ] が **[!UICONTROL 即時]** の場合、アップロードされたアセットは、「[!DNL Dynamic Media] アップロード **[!UICONTROL 」をクリックすると自動的に]** に公開されます。

1. アップロードしたアセットを [!DNL AEM] に公開するには、「**AEM に公開**」を選択し、「**[!UICONTROL アップロード]**」をクリックします。

   「**AEM に公開**」を選択した場合、アセットは [!DNL AEM and Dynamic Media] に公開され、それ以外の場合はアセットは [!DNL Dynamic Media] に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### [!UICONTROL Dynamic Media 公開モード]を[!UICONTROL 選択的公開]に設定 {#dynamic-media-publish-mode-set-to-selective-publish}

[!UICONTROL Dynamic Media 公開モード]を&#x200B;**[!UICONTROL 選択的公開]**&#x200B;に設定したフォルダーへのアップロード中にアセットを公開するには、次のようにうします。

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL 選択的公開]**&#x200B;として表示されます。

![アップロード画像 - 選択的公開モード](/help/assets/assets/upload-selective.svg)

1. 要件に応じて「**[!UICONTROL AEM に公開]**」、「**[!UICONTROL Dynamic Media に公開]**」、またはその両方を選択し、「**アップロード**」をクリックします。

   アセットは、選択に基づいて [!DNL AEM and Dynamic Media] に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

## アセットの参照ページを使用したアセットの公開 {#publish-assets-using-asset-browse-page}

アセットの参照ページを使用してアセットを公開するには：

1. 左側のパネルにある「**[!UICONTROL アセット管理]**」セクションで「**[!UICONTROL アセット]**」をクリックします。
1. 公開する必要があるアセットまたはフォルダーを 1 つ以上選択し、「**[!UICONTROL 公開]**」をクリックします。
1. 「**[!UICONTROL AEM]**」を選択し、「**[!UICONTROL 公開]**」をクリックして、アセットを [!DNL AEM and Dynamic Media] に公開します。

   ![アセットの参照](/help/assets/assets/browse-uactivation-immediate.svg)

   [!DNL Dynamic Media] 公開モードが **[!UICONTROL 選択的公開]** に設定されているフォルダーは公開できません。 [!DNL AEM] を選択すると、選択した他のすべてのフォルダーまたはアセットは [!DNL AEM and Dynamic Media] に公開されます。

   ![アセットの参照](/help/assets/assets/browse-selective123.svg)

## 検索結果ページを使用したアセットの公開 {#publish-assets-using-search-results-page}

アセットの検索結果ページを使用してアセットを公開するには：

1. 検索バーで条件を指定し、検索アイコンをクリックして結果を表示します。
1. 公開する必要があるアセットを選択し、「**[!UICONTROL 公開]」をクリックします。**
1. 要件に応じて、[!DNL AEM, Dynamic Media]、またはその両方を選択し、「**[!UICONTROL 公開]**」をクリックします。

   ![ 検索画像 ](/help/assets/assets/search-mode.svg)

   検索結果ページで [!DNL Dynamic Media] に公開するオプションは、アセットがリポジトリで使用可能なフォルダーで設定された [!DNL Dynamic Media] 公開モードによって異なります。

   >[!NOTE]
   >
   >フォルダーを選択し、検索結果ページで「**[!UICONTROL 公開]**」をクリックすると、[!DNL Experience Manager Assets] では、フォルダーの [!DNL Dynamic Media] 公開モードの設定に関係なく、アセットを [!DNL Dynamic Media] ではなく [!DNL AEM] に公開するオプションが表示されます。

## 公開ステータスの確認 {#check-publish-status}

アセットまたはフォルダーの公開ステータスを確認するには：

1. 左側のパネルにある「**[!UICONTROL アセット管理]**」セクションで「**[!UICONTROL アセット]**」をクリックします。
1. 表示切り替えを使用してリスト表示に切り替えます。[!UICONTROL AEM パブリッシュ]、[!UICONTROL Dynamic Media 公開]、[!UICONTROL タイトル]、[!UICONTROL サイズ]、[!UICONTROL ディメンション]などのアセットのプロパティを表示できます。

   アセットまたはフォルダーが公開されていない場合、**[!UICONTROL AEM パブリッシュ]**&#x200B;列と **[!UICONTROL Dynamic Media 公開]**&#x200B;列のステータスには&#x200B;**[!UICONTROL 該当なし]**&#x200B;と表示されます。

   ![公開ステータス 1 の確認](/help/assets/assets/check-publish-status1.png)

   リスト表示で「[!DNL AEM] 公開」列と「[!DNL Dynamic Media] 公開」列を表示できない場合は、次のようにします。

   1. ![設定](/help/assets/assets/settings-icon.svg) をクリックし、**[!UICONTROL 設定可能な列]**&#x200B;ダイアログから **[!UICONTROL AEM パブリッシュ]**&#x200B;列と **[!UICONTROL Dynamic Media 公開]**&#x200B;列を選択します。
   1. 「**[!UICONTROL 確認]**」をクリックします。[!DNL Experience Manager Assets] は、選択した列をリスト表示に追加します。

      ![公開ステータスの確認 2](/help/assets/assets/check-publish-status2.png)

また、アセットを選択して「**[!UICONTROL 詳細]**」をクリックすると、アセットの公開ステータスを確認することもできます。詳細は、右側のパネルにある「**[!UICONTROL 公開]**」セクションで確認できます。「**[!UICONTROL 公開]**」セクションには、アセットが [!DNL Dynamic Media] および [!DNL AEM] に公開された日付がリストされます。アセットが公開された時間を確認する必要がある場合は、リスト表示に移動して詳細を表示できます。

![公開ステータスの確認 3](/help/assets/assets/check-publish-status3.png)

## 制限事項 {#limitations}

アセットを [!DNL AEM and Dynamic Media] に公開する場合、次の機能は現時点では対象外です。

* [!DNL Asset details page] から [!DNL AEM and Dynamic Media] にアセットを公開。
* クイック公開ウィザードを使用して、アセットが公開されるエンドポイントを視覚化。
* クイック公開ウィザードでアセットをさらに追加または削除。
* 公開されたアセットを表示するページ。
* アセットレベルで [!DNL Dynamic Media] URL をコピーまたはペーストする機能（アセットが [!DNL Dynamic Media] に公開されている場合）。
* [!DNL AEM] への公開中に参照（アセット、タグなど）を公開する機能。
* フォルダーレベルで [!DNL Dynamic Media] 同期ステータスを上書きする機能。
* フォルダーレベルで [!DNL Dynamic Media] 公開モードを上書きする機能。
* 公開を管理は、まだサポートされていません。
