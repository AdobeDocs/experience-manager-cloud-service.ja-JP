---
title: AEMとDynamic MediaのクイックPublish
description: Assets ビューのクイックPublishを使用すると、AEMと Dynamic Media にアセットを同時に、または個別に公開できます。 アセットとフォルダーを選択し、Dynamic MediaまたはAEMに公開することを選択できます。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# AEM および Dynamic Media へのアセットの公開{#Publish-Assets-to-AEM-and-Dynamic-Media}

Experience Manager Assetsでは、Assets ビューを使用して、アセットをExperience ManagerおよびDynamic Mediaにすばやく公開できます。 これにより、管理者ビューに切り替えることなく、[Assets ビューを使用してアセットを管理し ](/help/assets/overview.md##persona-based-experiences) 公開できます。

Experience Manager Assets表示では、アセットをAEMまたはDynamic Media（あるいはその両方）に同時に柔軟に公開できます。 アセットのアップロード、参照および検索時に、アセットを公開できます。 アセットを公開するためのこれらのオプションについて、この記事で詳しく説明します。

## 事前準備 {#before-you-begin}

次の設定を指定して、AEMおよびDynamic Mediaの公開オプションを表示します。

* Dynamic Mediaの公開オプションを表示するには、管理者ビューを使用して次の設定を行います。

   * [Dynamic Media クラウド設定を作成 ](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) します。
   * フォルダーレベルでDynamic Media Publish モードを設定します。 これらの設定は、Dynamic Media クラウド設定を作成する際にも指定できます。 これらの設定をフォルダーレベルで上書きするには、[Dynamic Mediaのフォルダーレベルでの選択したPublishの設定 ](/help/assets/dynamic-media/selective-publishing.md) を参照してください。

* AEMの公開オプションを表示するには、ご利用の環境にAEM パブリッシュエンドポイントを設定する必要があります。

## アップロード中のPublish Assets {#piblish-assets-during-upload}

アセットをフォルダーにアップロードしながら、アセットをAEMおよびDynamic Mediaに公開できます。 表示されるパブリッシュオプションは、アセットのアップロード先のフォルダーに設定されたDynamic Media パブリッシュモードによって異なります。 Dynamic Mediaの公開モードは次のように設定することができます。

* **アクティベーション時：** アセットがこのフォルダーにアップロードされる場合、URL/埋め込みリンクの提供の前に、最初にアセットを明示的に公開する必要があります。

* **即時：** アセットがこのフォルダーにアップロードされると、アセットがExperience Managerーに取り込まれ、URL/埋め込みがすぐに提供されます。
* **Publishを選択：** Assetsは、Experience ManagerまたはDynamic Mediaのいずれかを選択して公開され、パブリックドメインで配信されます。

### アクティベーション時にDynamic Media Publish モードを「」に設定 {#dynamic-media-publish-mode-set-to-upon-activation}

Dynamic Media Publish モードを **アクティベーション時** に設定したフォルダーにアップロードする際にアセットを公開するには：

1. **Assetsを追加**/**参照**/**ファイルを参照** をクリックして、アセットをアップロードするフォルダーに移動します。 「**Publishオプション**」セクションには、「**アクティベーション時** として **DM Publishモード** が表示されます。
   ![ アクティベーション時に画像をアップロード ](/help/assets/assets/upload-uactivation.svg)
2. **PublishからAEMおよびDynamic Mediaへ** を選択し、「**アップロード**」をクリックします。 アセットはAEMとDynamic Mediaに同時に公開されます。 これらのアセットの更新された公開ステータスを確認するには、[Publish ステータスの確認 ](#check-publish-status) を参照してください。

### Dynamic Media Publish モードを即時に設定 {#dynamic-media-publish-mode-set-to-immediate}

Dynamic Media Publish モードを **即時** に設定したフォルダーにアップロードする際にアセットを公開するには：

1. **Assetsを追加**/**参照**/**ファイルを参照** をクリックして、アセットをアップロードするフォルダーに移動します。 「Publishオプション」セクションには、「**DM Publishモード** が **即時** と表示されます。
   ![ ファイルのアップロード画像 – 即時モード ](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Dynamic Media Publishモードが **即時** なので、「アップロード **をクリックすると、アップロードされたアセットがDynamic Mediaに自動的に公開され** す。

2. 公開する **AEMにPublishを選択し** アップロードしたアセットをAEMに送信して、「アップロード」をクリックします。

   **AEMにPublish** を選択した場合、アセットはAEMおよびDynamic Mediaに公開され、選択していない場合は、Dynamic Mediaに公開されます。

   これらのアセットの更新された公開ステータスを確認するには、[Publish ステータスの確認 ](#check-publish-status) を参照してください。

### Dynamic Media Publish モードが「選択Publish」に設定されている {#dynamic-media-publish-mode-set-to-selective-publish}

Dynamic Media Publish モードを **Publishを選択** に設定して、フォルダーにアップロードする際にアセットを公開するには：

1. **Assetsを追加**/**参照**/**ファイルを参照** をクリックして、アセットをアップロードするフォルダーに移動します。 「Publish オプション」セクションには、「**DM Publish モード** が **選択Publish** として表示されます。
   ![ 画像選択ピブリッシュモードのアップロード ](/help/assets/assets/upload-selective.svg)

2. 必要に応じて、**PublishからAEM**、**PublishからDynamic Media**、またはその両方を選択し、「**アップロード**」をクリックします。

   アセットは、選択内容に基づいてAEMおよびDynamic Mediaに公開されます。

   これらのアセットの更新された公開ステータスを確認するには、[Publish ステータスの確認 ](#check-publish-status) を参照してください。

## アセットの参照ページを使用したPublish アセット {#publish-assets-using-asset-browse-page}

アセットの参照ページを使用してアセットを公開するには：

1. 左側のウィンドウで使用可能な **2}Assets Management}** セクションの **Assets} をクリックします。**
2. 公開する必要があるアセットまたはフォルダーを選択し、**Publish** をクリックします。
3. 「**AEM**」を選択し、「**Publish**」をクリックして、AEMとDynamic Mediaにアセットを公開します。
   ![ アセットの参照 ](/help/assets/assets/browse-uactivation-immediate.svg)
Dynamic Media Publish モードが **選択的公開」に設定されているフォルダーは公開できません。** 選択した他のすべてのフォルダーまたはアセットは、AEMを選択した後、AEMおよびDynamic Mediaに公開されます。
   ![ アセットの参照 ](/help/assets/assets/browse-selective123.svg)

## 検索結果ページを使用したPublish assets {#publish-assets-using-search-results-page}

アセット検索結果ページを使用してアセットを公開するには：

1. 検索バーで条件を指定し、検索アイコンをクリックして結果を表示します。
2. 公開するアセットを選択し、**Publish.** をクリックします。
3. 必要に応じてAEM、Dynamic Mediaまたはその両方を選択し、**Publish** をクリックします。
   ![ 検索画像 ](/help/assets/assets/search-mode.svg)
検索結果ページでDynamic Mediaに公開するオプションは、アセットがリポジトリーで使用可能なフォルダーに設定されているDynamic Media Publish モードによって異なります。

   >[!NOTE]
   >
   >フォルダーを選択し、検索結果ページで **Publish** をクリックすると、Experience Manager Assetsには、フォルダーのDynamic Media Publish モード設定に関係なく、Dynamic MediaではなくAEMにアセットを公開するオプションが表示されます。

## Publishのステータスの確認 {#check-publish-status}

アセットまたはフォルダーの公開ステータスを確認するには：

1. 左側のウィンドウで使用可能な ]**2}Assets Management}]** セクションの **[!UICONTROL Assets} をクリックします。**[!UICONTROL 
2. 表示スイッチャーを使用してリスト表示に切り替えます。 AEM Publish、Dynamic Media Publish、タイトル、サイズ、寸法などのアセットプロパティを表示できます。\
   アセットまたはフォルダーが公開されていない場合、**AEM Publish** および **Dynamic Media Publish** 列のステータスは **該当なし** と表示されます。
   ![ 公開ステータスの確認 1](/help/assets/assets/check-publish-status1.png)
リスト表示でAEM Publish列とDynamic Media Publish列を表示できない場合は、次のようにします。
   1. ![ 設定 ](/help/assets/assets/settings-icon.svg) をクリックし、{ 設定可能な列 **ダイアログで** AEM Publish **列と** 4}Dynamic Media Publish **列を選択します。**
   2. **確認」をクリックします。Experience Manager Assets**、選択した列をリスト表示に追加します。

      ![ 公開ステータスの確認 2](/help/assets/assets/check-publish-status2.png)

また、アセットを選択して「**詳細」をクリックすると、アセットの公開ステータスを確認できます。** 詳細は、右側のパネルにある「**Publish**」セクションで確認できます。 「**Publish**」セクションには、アセットがDynamic MediaおよびAEMに公開された日付が一覧表示されます。 アセットが公開された時間を確認する必要がある場合は、リスト表示に移動して、それらの詳細を確認できます。

![ 公開ステータス 3 を確認 ](/help/assets/assets/check-publish-status3.png)

## 制限事項 {#limitations}

AEMとDynamic Mediaにアセットを公開する際に、現時点では次の機能が利用できません。

* アセットの詳細ページからAEMおよびDynamic MediaにアセットをPublishします。
* クイックPublishウィザードを使用して、アセットが公開されるエンドポイントを視覚化します。
* クイックPublishウィザードで、さらにアセットを追加または削除する。
* 公開済みアセットを表示するページ。
* アセットレベルでDynamic Media URL をコピーまたは貼り付ける機能（アセットがDynamic Mediaに公開されている場合）。
* AEMへの公開中に参照（アセット、タグなど）を公開する機能。
* フォルダーレベルでDynamic Media同期ステータスを上書きする機能。
* フォルダーレベルでDynamic Media Publish モードを上書きする機能
* 公開を管理は、まだサポートされていません。
