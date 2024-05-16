---
title: AEMとDynamic Mediaへのクイック公開
description: アセットビューのクイック公開を使用すると、アセットをAEMと Dynamic Media に同時に、または個別に公開できます。 アセットとフォルダーを選択し、Dynamic MediaまたはAEMに公開することを選択できます。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: cb8a5e5e8ecec2884c061d60f2519ba3e0208f81
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# AEM および Dynamic Media へのアセットの公開{#Publish-Assets-to-AEM-and-Dynamic-Media}

Experience Manager Assetsでは、アセット ビューを使用して、アセットをExperience ManagerおよびDynamic Mediaにすばやく公開できます。 これにより、アセットを管理し、次を使用して公開することができます [管理者表示に切り替えない場合の Assets 表示](/help/assets/overview.md##persona-based-experiences).

Experience Manager Assets表示では、アセットをAEMまたはDynamic Media（あるいはその両方）に同時に柔軟に公開できます。 アセットのアップロード、参照および検索時に、アセットを公開できます。 アセットを公開するためのこれらのオプションについて、この記事で詳しく説明します。

## 事前準備 {#before-you-begin}

次の設定を指定して、AEMおよびDynamic Mediaの公開オプションを表示します。

* Dynamic Mediaの公開オプションを表示するには、管理者ビューを使用して次の設定を行います。

   * [Dynamic Media クラウド設定の作成](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * フォルダーレベルでDynamic Media公開モードを設定します。 これらの設定は、Dynamic Media クラウド設定を作成する際にも指定できます。 これらの設定をフォルダーレベルで上書きするには、を参照してください。 [Dynamic Mediaのフォルダーレベルでの選択的公開の設定](/help/assets/dynamic-media/selective-publishing.md).

* AEMの公開オプションを表示するには、ご利用の環境にAEM パブリッシュエンドポイントを設定する必要があります。

## アップロード時のアセットの公開 {#piblish-assets-during-upload}

アセットをフォルダーにアップロードしながら、アセットをAEMおよびDynamic Mediaに公開できます。 表示されるパブリッシュオプションは、アセットのアップロード先のフォルダーに設定されたDynamic Media パブリッシュモードによって異なります。 Dynamic Mediaの公開モードは次のように設定することができます。

* **アクティベート時：** アセットがこのフォルダーにアップロードされる場合は、URL/埋め込みリンクを指定する前に、まずアセットを明示的に公開する必要があります。

* **即時：** アセットがこのフォルダーにアップロードされると、アセットがExperience Managerーに取り込まれ、URL/埋め込みがすぐに提供されます。
* **選択的公開：** アセットは、Experience ManagerまたはDynamic Mediaのいずれかを選択して公開され、パブリックドメインで配信されます。

### アクティベーション時にDynamic Media公開モードをに設定 {#dynamic-media-publish-mode-set-to-upon-activation}

Dynamic Media公開モードをに設定したフォルダーにアップロードする際にアセットを公開するには **アクティベーション時**:

1. クリック **アセットを追加** > **参照** > **ファイルの参照** に移動してアセットをアップロードするフォルダーに移動します。 この **公開オプション** 「」セクションには、 **DM 公開モード** as **アクティベーション時**.
   ![アクティベーション時に画像をアップロード](/help/assets/assets/upload-uactivation.svg)
2. を選択 **AEMとDynamic Mediaへの公開** をクリックして、 **Upload**. アセットはAEMとDynamic Mediaに同時に公開されます。 これらのアセットの更新された公開ステータスを確認するには、 [公開ステータスの確認](#check-publish-status).

### Dynamic Media公開モードを「即時」に設定 {#dynamic-media-publish-mode-set-to-immediate}

Dynamic Media公開モードをに設定したフォルダーにアップロードする際にアセットを公開するには **即時**:

1. クリック **アセットを追加** > **参照** > **ファイルの参照** に移動してアセットをアップロードするフォルダーに移動します。 [ パブリッシュ オプション ] セクションには、 **DM 公開モード** as **即時**.
   ![ファイルのアップロード画像 – 即時モード](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Dynamic Mediaのパブリッシュモードは **即時**&#x200B;をクリックすると、アップロードされたアセットがDynamic Mediaに自動公開されます **Upload**.

2. 「公開先」を選択します **公開するAEM** アップロードされたアセットをAEMに送信し、「アップロード」をクリックします。

   を選択する場合 **AEMに公開**&#x200B;を選択すると、アセットがAEMとDynamic Mediaに公開されます。選択していない場合は、アセットがDynamic Mediaに公開されます。

   これらのアセットの更新された公開ステータスを確認するには、 [公開ステータスの確認](#check-publish-status).

### Dynamic Media公開モードを「選択的公開」に設定する {#dynamic-media-publish-mode-set-to-selective-publish}

Dynamic Media公開モードをに設定したフォルダーにアップロードする際にアセットを公開するには **選択的公開**:

1. クリック **アセットを追加** > **参照** > **ファイルの参照** に移動してアセットをアップロードするフォルダーに移動します。 公開オプション セクションには、が表示されます **DM 公開モード** as **選択的公開**.
   ![画像選択ピブリッシュモードのアップロード](/help/assets/assets/upload-selective.svg)

2. を選択 **AEMに公開**, **Dynamic Mediaに公開**&#x200B;必要に応じてまたは両方を選択し、 **Upload**.

   アセットは、選択内容に基づいてAEMおよびDynamic Mediaに公開されます。

   これらのアセットの更新された公開ステータスを確認するには、 [公開ステータスの確認](#check-publish-status).

## アセットの参照ページを使用したアセットの公開 {#publish-assets-using-asset-browse-page}

アセットの参照ページを使用してアセットを公開するには：

1. クリック **アセット** が含まれる **アセット管理** セクションは左側のウィンドウで使用できます。
2. 公開する必要があるアセットまたはフォルダーを選択し、 **公開**.
3. を選択 **AEM** をクリックして、 **公開** をクリックして、AEMとDynamic Mediaにアセットを公開します。
   ![アセットの参照](/help/assets/assets/browse-uactivation-immediate.svg)
Dynamic Media公開モードがに設定されているフォルダーは公開できません **選択的公開。** 他の選択したフォルダーやアセットはすべて、AEMを選択した後、AEMとDynamic Mediaに公開されます。
   ![アセットの参照](/help/assets/assets/browse-selective123.svg)

## 検索結果ページを使用したアセットの公開 {#publish-assets-using-search-results-page}

アセット検索結果ページを使用してアセットを公開するには：

1. 検索バーで条件を指定し、検索アイコンをクリックして結果を表示します。
2. 公開するアセットを選択し、 **公開。**
3. 必要に応じてAEM、Dynamic Mediaまたはその両方を選択し、をクリックします。 **公開。**
   ![検索画像](/help/assets/assets/search-mode.svg)
検索結果ページでDynamic Mediaに公開するオプションは、アセットがリポジトリーで使用可能なフォルダーに設定されている「Dynamic Media公開モード」によって異なります。

   >[!NOTE]
   >
   >フォルダーを選択し、 **公開** 検索結果ページに、フォルダーの「Dynamic Media公開モード」設定に関係なく、Experience Manager Assetsはアセットを「Dynamic MediaではなくAEMに公開」するオプションを表示します。

## 公開ステータスの確認 {#check-publish-status}

アセットまたはフォルダーの公開ステータスを確認するには：

1. クリック **[!UICONTROL アセット]** が含まれる **[!UICONTROL アセット管理]** セクションは左側のウィンドウで使用できます。
2. 表示スイッチャーを使用してリスト表示に切り替えます。 AEM パブリッシュ、Dynamic Media パブリッシュ、タイトル、サイズ、寸法などのアセットプロパティを表示できます。\
   アセットまたはフォルダーが公開されていない場合、ステータスは **AEM公開** および **Dynamic Media公開** 列の表示方法 **なし**
   ![公開ステータス 1 を確認](/help/assets/assets/check-publish-status1.png)
リスト表示で「AEM公開」列と「Dynamic Media公開」列を表示できない場合は、次のようにします。
   1. クリック ![設定](/help/assets/assets/settings-icon.svg) を選択して、 **AEM公開** および **Dynamic Media公開** からの列 **設定可能な列** ダイアログ。
   2. クリック **確認して。** Experience Manager Assetsは、選択された列をリスト表示に追加します。

      ![公開ステータスの確認 2](/help/assets/assets/check-publish-status2.png)

また、アセットを選択してをクリックすることで、アセットの公開ステータスを確認することもできます **詳細。** 詳しくは、以下を参照してください **公開** セクションは右側のパネルで使用できます。 この **公開** 「」セクションには、アセットがDynamic MediaとAEMに公開された日付が一覧表示されます。 アセットが公開された時間を確認する必要がある場合は、リスト表示に移動して、それらの詳細を確認できます。

![公開ステータス 3 を確認](/help/assets/assets/check-publish-status3.png)

## 制限事項 {#limitations}

AEMとDynamic Mediaにアセットを公開する際に、現時点では次の機能が利用できません。

* アセットの詳細ページからAEMおよびDynamic Mediaにアセットを公開する。
* クイック公開ウィザードを使用して、アセットが公開されるエンドポイントを視覚化します。
* クイック公開ウィザードで、アセットをさらに追加または削除します。
* 公開済みアセットを表示するページ。
* アセットレベルでDynamic Media URL をコピーまたは貼り付ける機能（アセットがDynamic Mediaに公開されている場合）。
* AEMへの公開中に参照（アセット、タグなど）を公開する機能。
* フォルダーレベルでDynamic Media同期ステータスを上書きする機能。
* フォルダーレベルでDynamic Media公開モードを上書きする機能
* 公開を管理は、まだサポートされていません。
