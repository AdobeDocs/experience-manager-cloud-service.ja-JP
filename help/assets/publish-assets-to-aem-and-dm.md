---
title: AEM および Dynamic Media へのクイック公開
description: Assets ビューのクイックPublishを使用すると、AEMとDynamic Mediaにアセットを同時に、または個別に公開できます。 アセットとフォルダーを選択し、Dynamic Media または AEM に公開することを選択できます。
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: 8ab19fe82fc390d28d33b17222177fd8486c8fc7
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 70%

---

# AEM および Dynamic Media へのアセットの公開{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets では、アセットビューを使用して、Experience Manager および Dynamic Media にアセットをすばやく公開できます。これにより、管理者ビューに切り替えることなく、[Assets ビューを使用してアセットを管理し ](/help/assets/overview.md##persona-based-experiences) 公開できます。

Experience Manager Assets ビューでは、アセットを AEM や Dynamic Media に、またはその両方に同時に公開できる柔軟性が提供されます。アセットのアップロード、参照および検索時に、アセットを公開できます。アセットを公開するためのこれらのオプションについて、この記事で詳しく説明します。

## 事前準備 {#before-you-begin}

これらの設定を構成して、AEMおよびDynamic Mediaの公開オプションを表示します。

* Dynamic Mediaの公開オプションを表示するには、管理者ビューを使用して次の設定を行います。

   * [Dynamic Media Cloud 設定を作成 ](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) します。
   * フォルダーレベルで Dynamic Media 公開モードを設定します。これらの設定は、Dynamic Media Cloud 設定を作成する際にも指定できます。 これらの設定をフォルダーレベルで上書きするには、[Dynamic Mediaのフォルダーレベルでの選択的Publishの設定 ](/help/assets/dynamic-media/selective-publishing.md) を参照してください。

* AEMの公開オプションを表示するには、ご利用の環境にAEM パブリッシュエンドポイントを設定する必要があります。

## アップロード中のアセットの公開 {#piblish-assets-during-upload}

アセットをフォルダーにアップロードしながら、AEM および Dynamic Media にアセットを公開できます。表示される公開オプションは、アセットのアップロード先のフォルダーに設定されたDynamic Media公開モードによって異なります。 Dynamic Media 公開モードは、次のように設定できます。

* **アクティベーション時：** アセットがこのフォルダーにアップロードされる場合、URL/埋め込みリンクの提供の前に、最初にアセットを明示的に公開する必要があります。

* **即時：**&#x200B;アセットをこのフォルダーにアップロードする際は、システムがアセットを Experience Manager に取り込み、URL／埋め込みを即時に提供します。
* **選択的公開：**&#x200B;パブリックドメインでの配信用に、Experience Manager または Dynamic Media のいずれかにアセットを公開します。

### アクティベーション時への Dynamic Media 公開モードの設定 {#dynamic-media-publish-mode-set-to-upon-activation}

**アクティベーション時**&#x200B;に Dynamic Media 公開モードを設定したフォルダーへのアップロード中にアセットを公開するには：

1. **アセットを追加**／**参照**／**ファイルを参照**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「**Publishオプション**」セクションには、「**アクティベーション時** として **DM Publishモード** が表示されます。
   ![アクティベーション時のアップロード画像](/help/assets/assets/upload-uactivation.svg)
2. 「**AEM および Dynamic Media に公開**」を選択し、「**アップロード**」をクリックします。アセットは、AEM と Dynamic Media に同時に公開されます。これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### Dynamic Media 公開モードを即時に設定 {#dynamic-media-publish-mode-set-to-immediate}

Dynamic Media 公開モードを&#x200B;**即時**&#x200B;に設定したフォルダーへのアップロード中にアセットを公開するには：

1. **アセットを追加**／**参照**／**ファイルを参照**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「Publishオプション」セクションには、「**DM Publishモード** が **即時** と表示されます。
   ![ファイルのアップロード画像 - 即時モード](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Dynamic Media 公開モードは&#x200B;**即時**&#x200B;なので、「**アップロード**」をクリックすると、アップロードしたアセットは自動的に Dynamic Media に公開されます。

2. アップロードしたアセットを AEM に公開するには、「**AEM に公開**」を選択し、「アップロード」をクリックします。

   「**AEM に公開**」を選択した場合、アセットは AEM と Dynamic Media に公開され、それ以外の場合はアセットは Dynamic Media に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

### Dynamic Media 公開モードを選択的公開に設定 {#dynamic-media-publish-mode-set-to-selective-publish}

Dynamic Media 公開モードを&#x200B;**選択的公開**&#x200B;に設定したフォルダーへのアップロード中にアセットを公開するには：

1. **アセットを追加**／**参照**／**ファイルを参照**&#x200B;をクリックして、アセットをアップロードする適切なフォルダーに移動します。「公開オプション」セクションには、**DM 公開モード**&#x200B;が&#x200B;**選択的公開**として表示されます。
   ![アップロード画像 - 選択的公開モード](/help/assets/assets/upload-selective.svg)

2. 要件に応じて「**AEM に公開**」、「**Dynamic Media に公開**」、またはその両方を選択し、「**アップロード**」をクリックします。

   アセットは、選択に基づいて AEM および Dynamic Media に公開されます。

   これらのアセットの更新された公開ステータスを確認する方法について詳しくは、[公開ステータスの確認](#check-publish-status)を参照してください。

## アセットの参照ページを使用したアセットの公開 {#publish-assets-using-asset-browse-page}

アセットの参照ページを使用してアセットを公開するには：

1. 左側のパネルにある「**アセット管理**」セクションで「**アセット**」をクリックします。
2. 公開する必要があるアセットまたはフォルダーを 1 つ以上選択して、**Publish** をクリックします。
3. 「**AEM**」を選択し、「**公開**」をクリックして、アセットを AEM および Dynamic Media に公開します。
   ![アセットの参照](/help/assets/assets/browse-uactivation-immediate.svg)
Dynamic Media 公開モードが選択的公開に設定されているフォルダーを公開できません。****AEM を選択すると、選択した他のすべてのフォルダーまたはアセットが AEM および Dynamic Media に公開されます。
   ![アセットの参照](/help/assets/assets/browse-selective123.svg)

## 検索結果ページを使用したアセットの公開 {#publish-assets-using-search-results-page}

アセットの検索結果ページを使用してアセットを公開するには：

1. 検索バーで条件を指定し、検索アイコンをクリックして結果を表示します。
2. 公開する必要があるアセットを選択し、「**公開**」をクリックします。
3. 要件に応じて、AEM、Dynamic Media、またはその両方を選択し、「**公開**」をクリックします。
   ![検索画像](/help/assets/assets/search-mode.svg)
検索結果ページで Dynamic Media に公開するオプションは、リポジトリ内でアセットが使用可能なフォルダーに設定されている Dynamic Media 公開モードによって異なります。

   >[!NOTE]
   >
   >フォルダーを選択し、検索結果ページで **Publish** をクリックすると、Experience Manager Assetsには、フォルダーのDynamic Media Publish モード設定に関係なく、Dynamic MediaではなくAEMにアセットを公開するオプションが表示されます。

## 公開ステータスの確認 {#check-publish-status}

アセットまたはフォルダーの公開済みステータスを確認するには：

1. 左側のパネルにある「**[!UICONTROL アセット管理]**」セクションで「**[!UICONTROL アセット]**」をクリックします。
2. 表示スイッチャーを使用してリスト表示に切り替えます。 AEM パブリッシュ、Dynamic Media Publish、タイトル、サイズ、寸法などのアセットプロパティを表示できます。\
   アセットまたはフォルダーが公開されていない場合、列 **AEM Publish** および **Dynamic Media Publish** のステータスは **該当なし** と表示されます。
   ![公開ステータスの確認 1](/help/assets/assets/check-publish-status1.png)
リスト表示に AEM パブリッシュ列とDynamic Media 公開列が表示されない場合は、次の操作を行います。
   1. ![設定](/help/assets/assets/settings-icon.svg) をクリックし、**設定可能な列**&#x200B;ダイアログから **AEM パブリッシュ**&#x200B;列と **Dynamic Media 公開**&#x200B;列を選択します。
   2. 「確認」をクリックします。**** Experience Manager Assets は、選択した列をリスト表示に追加します。

      ![公開ステータスの確認 2](/help/assets/assets/check-publish-status2.png)

また、アセットを選択して「詳細」をクリックすると、アセットの公開ステータスを確認することもできます。****&#x200B;詳細は、右側のパネルにある「**公開**」セクションで確認できます。「**公開**」セクションには、アセットが Dynamic Media および AEM に公開された日付がリストされます。アセットが公開された時間を確認する必要がある場合は、リスト表示に移動して詳細を表示できます。

![公開ステータスの確認 3](/help/assets/assets/check-publish-status3.png)

## 制限事項 {#limitations}

アセットを AEM および Dynamic Media に公開する場合、次の機能は現時点では範囲外です。

* アセットの詳細ページからAEMおよびDynamic MediaへのPublish アセット。
* クイックPublishウィザードを使用して、アセットが公開されるエンドポイントを視覚化します。
* クイックPublishウィザードで、アセットを追加または削除します。
* 公開されたアセットを表示するページ。
* アセットレベルで Dynamic Media URL をコピーまたはペーストする機能（アセットが Dynamic Media に公開されている場合）。
* AEM への公開中に参照（アセット、タグなど）を公開する機能。
* フォルダーレベルで Dynamic Media 同期ステータスを上書きする機能。
* フォルダーレベルで Dynamic Media 公開モードを上書きする機能。
* 公開を管理は、まだサポートされていません。
