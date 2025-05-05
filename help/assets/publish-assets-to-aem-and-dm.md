---
title: クイック公開先  [!DNL AEM and Dynamic Media]
description: ' [!DNL Assets view]  クイック公開」を使用すると、アセットを同時に、または個別に公開  [!DNL AEM and Dynamic Media]  きます。 アセットとフォルダーを選択し、公開先  [!DNL Dynamic Media]  または  [!DNL AEM] を選択できます。'
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: 138f7ef2023399ce5da9fe80447ac45fd9542064
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 38%

---

# [!DNL AEM and Dynamic Media] へのAssetsの公開{#Publish-Assets-to-AEM-and-Dynamic-Media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

[!DNL Experience Manager Assets] を使用すると、[!DNL Assets view] を使用してアセットを [!DNL Experience Manager] および [!DNL Dynamic Media] にすばやく公開できます。 これにより、アセットを管理し、を使用して [[!DNL Assets view]  に切り替えることなく  [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences) アセットを公開できます。

[!DNL Experience Manager Assets view] では、アセットを [!DNL AEM] または [!DNL Dynamic Media] に同時に公開することができます。 アセットのアップロード、参照および検索時に、アセットを公開できます。アセットを公開するこれらのすべてのオプションについて詳しくは、この記事を参照してください。

## 始める前に {#before-you-begin}

[!DNL AEM and Dynamic Media] の公開オプションを表示するには、以下の設定を行います。

* [!DNL Dynamic Media] の公開オプションを表示するには、管理者表示を使用して次の設定を指定します。

   * [ クラウド設定  [!DNL Dynamic Media]  作成 ](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) します。
   * フォルダーレベルで [!DNL Dynamic Media] 公開モードを設定します。 これらの設定は、[!DNL Dynamic Media] Cloud 設定を作成する際にも指定できます。 これらの設定をフォルダーレベルで上書きするには、[ のフォルダーレベルでの選択的公開の設定  [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md) を参照してください。

* [!DNL AEM] の公開オプションを表示するには、ご利用の環境に [!DNL AEM] パブリッシュエンドポイントを設定する必要があります。

## アップロード中のアセットの公開 {#piblish-assets-during-upload}

アセットをフォルダーにアップロードする際に、アセットを [!DNL AEM and Dynamic Media] に公開できます。 表示される公開オプションは、アセットがアップロードされているフォルダーの [!DNL Dynamic Media] 公開モード設定によって異なります。 公開モード [!DNL Dynamic Media] 次のように設定することができます。

* **[!UICONTROL アクティベーション時 &#x200B;]:** アセットがこのフォルダーにアップロードされる場合、URL/埋め込みリンクの提供の前に、最初にアセットを明示的に公開する必要があります。

* **[!UICONTROL 即時 &#x200B;]:** アセットがこのフォルダーにアップロードされると、アセットがExperience Managerに取り込まれ、URL/埋め込みがすぐに提供されます。
* **[!UICONTROL 選択的公開 &#x200B;]:** Assetsは、[!DNL Experience Manager] または [!DNL Dynamic Media] のいずれかを選択して公開され、パブリックドメインで配信されます。

### [!UICONTROL Dynamic Media 公開モード &#x200B;] アクティベーション時 [!UICONTROL &#x200B; に設定される &#x200B;] {#dynamic-media-publish-mode-set-to-upon-activation}

[!DNL Dynamic Media Publish Mode] が **[!UICONTROL アクティベーション時]** に設定されているフォルダーにアセットをアップロードする際にアセットを公開するには：

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL アクティベーション時]**&#x200B;として表示されます。
   ![アクティベーション時のアップロード画像](/help/assets/assets/upload-uactivation.svg)
2. 「**[!UICONTROL AEM および Dynamic Media に公開]**」を選択し、「**[!UICONTROL アップロード]**」をクリックします。アセットは [!DNL AEM and Dynamic Media] に同時に公開されます。 これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### [!UICONTROL Dynamic Media 公開モード &#x200B;] を [!UICONTROL &#x200B; 即時 &#x200B;] に設定 {#dynamic-media-publish-mode-set-to-immediate}

[!UICONTROL Dynamic Media 公開モード &#x200B;] が **[!UICONTROL 即時]** に設定されているフォルダーにアセットをアップロードしながら公開するには：

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL 即時]**&#x200B;として表示されます。
   ![ ファイルのアップロード画像 – 即時モード ](/help/assets/assets/resized-image-pdf-svg-new.svg)
[!UICONTROL Dynamic Media 公開モード &#x200B;] が **[!UICONTROL 即時]** の場合、アップロードされたアセットは、「**[!UICONTROL アップロード]**」をクリックすると自動的に [!DNL Dynamic Media] に公開されます。

2. **AEMに公開** を選択して、アップロードしたアセットを [!DNL AEM] に公開し、**[!UICONTROL アップロード]** をクリックします。

   **AEMに公開** を選択した場合、アセットは [!DNL AEM and Dynamic Media] に公開され、選択しなかった場合は [!DNL Dynamic Media] に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### [!UICONTROL Dynamic Media 公開モード &#x200B;] を [!UICONTROL &#x200B; 選択的公開 &#x200B;] に設定 {#dynamic-media-publish-mode-set-to-selective-publish}

[!UICONTROL Dynamic Media 公開モード &#x200B;] を「選択的公開 **[!UICONTROL に設定したフォルダーにアップロードする際にアセットを公開するには]**:

1. **[!UICONTROL アセットを追加]**／**[!UICONTROL 参照]**／**[!UICONTROL ファイルを参照]**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**[!UICONTROL 公開オプション]**」セクションには、**[!UICONTROL DM 公開モード]**&#x200B;が&#x200B;**[!UICONTROL 選択的公開]**&#x200B;として表示されます。
   ![アップロード画像 - 選択的公開モード](/help/assets/assets/upload-selective.svg)

2. 要件に応じて「**[!UICONTROL AEM に公開]**」、「**[!UICONTROL Dynamic Media に公開]**」、またはその両方を選択し、「**アップロード**」をクリックします。

   選択した内容に基づいて、アセットが [!DNL AEM and Dynamic Media] に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

## アセットの参照ページを使用したアセットの公開 {#publish-assets-using-asset-browse-page}

アセットの参照ページを使用してアセットを公開するには：

1. 左側のパネルにある「**[!UICONTROL アセット管理]**」セクションで「**[!UICONTROL アセット]**」をクリックします。
2. 公開する必要があるアセットまたはフォルダーを 1 つ以上選択し、「**[!UICONTROL 公開]**」をクリックします。
3. **[!UICONTROL AEM]** を選択し、「**[!UICONTROL 公開]**」をクリックして、アセットを [!DNL AEM and Dynamic Media] に公開します。
   ![ アセットの参照 ](/help/assets/assets/browse-uactivation-immediate.svg)
[!DNL Dynamic Media] 公開モードが **[!UICONTROL 選択的公開]** に設定されているフォルダーは公開できません。 選択した他のすべてのフォルダーやアセットは、選択した後に [!DNL AEM and Dynamic Media] に公開さ [!DNL AEM] ます。
   ![アセットの参照](/help/assets/assets/browse-selective123.svg)

## 検索結果ページを使用したアセットの公開 {#publish-assets-using-search-results-page}

アセットの検索結果ページを使用してアセットを公開するには：

1. 検索バーで条件を指定し、検索アイコンをクリックして結果を表示します。
2. 公開するアセットを選択し、「**[!UICONTROL 公開 &#x200B;].** をクリックします。
3. 必要に応じて [!DNL AEM, Dynamic Media] または両方を選択し、「**[!UICONTROL 公開]**」をクリックします。
   ![ 検索画像 ](/help/assets/assets/search-mode.svg)
検索結果ページで [!DNL Dynamic Media] に公開するオプションは、アセットがリポジトリで使用可能なフォルダーで設定された [!DNL Dynamic Media] 公開モードによって異なります。
   >[!NOTE]
   >
   >フォルダーを選択し、検索結果ページで「**[!UICONTROL 公開]**」をクリックすると、[!DNL Experience Manager Assets] はフォルダーの [!DNL Dynamic Media] 公開モード設定に関係な [!DNL Dynamic Media]、[!DNL AEM] にアセットを公開するオプションを表示します。

## 公開ステータスの確認 {#check-publish-status}

アセットまたはフォルダーの公開ステータスを確認するには：

1. 左側のパネルにある「**[!UICONTROL アセット管理]**」セクションで「**[!UICONTROL アセット]**」をクリックします。
2. 表示切り替えを使用してリスト表示に切り替えます。[!UICONTROL AEM公開 &#x200B;]、[!UICONTROL Dynamic Media 公開 &#x200B;]、[!UICONTROL &#x200B; タイトル &#x200B;]、[!UICONTROL &#x200B; サイズ &#x200B;]、[!UICONTROL &#x200B; ディメンション &#x200B;] などのアセットプロパティを表示できます。\
   アセットまたはフォルダーが公開されていない場合、列 **[!UICONTROL AEM公開]** および **[!UICONTROL Dynamic Media 公開]** のステータスは **[!UICONTROL なし]** と表示されます。
   ![ 公開ステータスの確認 1](/help/assets/assets/check-publish-status1.png)
リスト表示で「[!DNL AEM] 公開」列と「[!DNL Dynamic Media] 公開」列を表示できない場合は、次のようにします。
   1. ![設定](/help/assets/assets/settings-icon.svg) をクリックし、**[!UICONTROL 設定可能な列]**&#x200B;ダイアログから **[!UICONTROL AEM パブリッシュ]**&#x200B;列と **[!UICONTROL Dynamic Media 公開]**&#x200B;列を選択します。
   2. 「**[!UICONTROL 確認]**」をクリックします。選択した列 [!DNL Experience Manager Assets] リスト表示に追加されます。

      ![公開ステータスの確認 2](/help/assets/assets/check-publish-status2.png)

また、アセットを選択して「**[!UICONTROL 詳細]**」をクリックすると、アセットの公開ステータスを確認できます。 詳細は、右側のパネルにある「**[!UICONTROL 公開]**」セクションで確認できます。 **[!UICONTROL 公開]** セクションには、アセットが [!DNL Dynamic Media] および [!DNL AEM] に公開された日付が一覧表示されます。 アセットが公開された時間を確認する必要がある場合は、リスト表示に移動して詳細を表示できます。

![公開ステータスの確認 3](/help/assets/assets/check-publish-status3.png)

## 制限事項 {#limitations}

アセットを [!DNL AEM and Dynamic Media] に公開する際に、以下の機能は現時点では範囲外です。

* [!DNL Asset details page] から [!DNL AEM and Dynamic Media] にアセットを公開します。
* クイック公開ウィザードを使用して、アセットが公開されるエンドポイントを視覚化。
* クイック公開ウィザードでアセットをさらに追加または削除。
* 公開されたアセットを表示するページ。
* アセットレベルで URL をコピーまたは貼り付け [!DNL Dynamic Media] 機能（アセットが [!DNL Dynamic Media] に公開されている場合）。
* [!DNL AEM] への公開中に参照（アセット、タグなど）を公開する機能。
* フォルダーレベルで同期ステ [!DNL Dynamic Media] タスを上書きする機能。
* フォルダーレベルで公開モード [!DNL Dynamic Media] 上書きする機能
* 公開を管理は、まだサポートされていません。
