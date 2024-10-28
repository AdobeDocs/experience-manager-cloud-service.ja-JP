---
title: Content Hubからのアセットのダウンロード
description: Content Hub ポータルからアセットをダウンロードする方法を学ぶ
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 96b7b7fe32aefc81a9fde15d79e9089f71cb5d31
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# Content Hubからのアセットのダウンロード {#download-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![アセットのダウンロード](assets/download-asset-genstudio.jpeg)

Content Hubでは、アセットをダウンロードして共有できます。 これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。 Content Hubは、効果的なアセット配布のためにアクセシビリティと適応性を強化します。

Content Hubでは、1 つまたは複数のアセットをダウンロードできます。 アセットの元のバージョンがダウンロードされます。

## 前提条件 {#prerequisites}

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) は、この記事で説明されるアクションを実行できます。

## アセットをダウンロード {#download-single-asset}

ダウンロードする前に、[ アセットのライセンスを承認 ](/help/assets/approve-assets-content-hub.md) してください。

### 単一ダウンロード {#single-download-asset}

アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 アセットをダウンロード ダイアログボックスに、アセットのライセンスが表示されます。 ライセンス条項に同意し、「**ダウンロード**」をクリックします。
または、アセットカードの ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックして、アセットをダウンロードします。

#### アセットからの単一アセットのダウンロード ダイアログボックス {#single-download-from-asset-dialog-box}

1. アセットのサムネールをクリックします。 アセット ダイアログボックスが表示されます。
1. 右端のツールバーから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 ダウンロードペインには、アセットレンディションと、ライセンス契約条件の承認チェックボックスが表示されます。
   ![single-download-dialog-box](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * 利用条件リンクをクリックして、左側のウィンドウにライセンス条件を表示します。

     >[!NOTE]
     >
     >利用条件チェックボックスは、ライセンスされたアセットに対してのみ表示されます。 また、アセットダイアログボックスには、ライセンスが承認されたアセットのライセンス条件のプレビューのみが表示されます。 ダウンロードする前に [ アセットのライセンスを承認 ](/help/assets/approve-assets-content-hub.md) し、アセットダイアログボックスでライセンス条件のプレビューを有効にします。

   * 左側のペインの元のアセットレンディションに戻るには、「**元のレンディション」ボックス** をクリックします。
1. （ライセンスが付与されたアセットの）ライセンス条件に同意し、「**ダウンロード**」をクリックしてアセットをダウンロードします。

### マルチダウンロード {#multi-download}

1. アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 表示されるダイアログボックスは、ダウンロードリストに期限切れのアセットが含まれているか、期限切れでないアセットのみが含まれているかによって異なります。<br/>
   **期限切れアセットをダウンロード** ダイアログボックス：このダイアログボックスでは、期限切れアセットのプレビューと有効期限が左側のペインに表示されます。 選択した合計のうち期限切れのアセットのカウントが右側のパネルに表示されます。 **すべてのアセットで続行** をクリックして、有効期限が切れたアセットを他のアセット（存在する場合）と共にダウンロードします。 アセットをダウンロード ダイアログボックスが表示されます。 詳しくは、[ アセットをダウンロード ](#Download-asset-dialog-box) ダイアログボックスを参照してください。

   >[!NOTE]
   >
   >[ 有効期限切れのアセットのダウンロードオプションを有効にする ](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) と、アセットをダウンロードできます。 ダウンロードが有効になっている期限切れアセットのみをダウンロードできます。

   <a id="Download-asset-dialog-box"></a> **アセットをダウンロードダイアログボックス：** このダイアログボックスには、選択したアセットに関連付けられているライセンスのリストが左側のペインに表示されます。 ライセンスを選択すると、契約条件（PDF 形式）が中央のウィンドウにプレビューされ、関連するアセットのプレビューとカウントが右側のウィンドウに表示されます。 レビュー済みのライセンスは水色でハイライト表示されます。

   >[!NOTE]
   >
   > **アセットをダウンロード」ダイアログボックス** は、承認されたライセンスに関するライセンス条件のみをプレビューします。 [ アセットのダウンロード ](/help/assets/approve-assets-content-hub.md) ダイアログボックスでライセンス条件をプレビューするには、アセットをダウンロードする前に **アセットのライセンスを承認** します。

1. ![remove-icon](/help/assets/assets/remove-icon.svg) をクリックして、ダウンロードダイアログボックスからライセンスを削除します。

1. 利用条件に同意し、「**ダウンロード**」をクリックして、使用可能なライセンスに関連付けられたアセットを左側のパネルでダウンロードします。
   ![download-multiple-license](/help/assets/assets/download-multiple-license.png)

### ライセンスのないアセットのダウンロード {#download-non-licensed-assets}

ライセンスのないアセットをダウンロードするには、アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。







