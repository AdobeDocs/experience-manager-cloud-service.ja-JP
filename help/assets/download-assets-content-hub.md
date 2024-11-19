---
title: Content Hubからのアセットのダウンロード
description: Content Hub ポータルからアセットをダウンロードする方法を学ぶ
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# Content Hubからのアセットのダウンロード {#download-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![アセットのダウンロード](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hubでは、アセットをダウンロードして共有できます。 これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。 Content Hubは、効果的なアセット配布のためにアクセシビリティと適応性を強化します。

Content Hubでは、1 つまたは複数のアセットをダウンロードできます。 アセットの元のバージョンがダウンロードされます。

## ライセンス取得済みアセットを 1 つダウンロード {#single-download-asset}

アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 アセットをダウンロード ダイアログボックスに、アセットのライセンスが表示されます。 ライセンス条項に同意し、「**ダウンロード**」をクリックします。
または、アセットカードの ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックして、アセットをダウンロードします。

### アセットから 1 つのライセンス済みアセットをダウンロード ダイアログボックス {#single-download-from-asset-dialog-box}

1. アセットのサムネールをクリックします。 アセット ダイアログボックスが表示されます。
1. 右端のツールバーから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 ダウンロードペインには、アセットレンディションと、ライセンス契約条件の承認チェックボックスが表示されます。
   ![single-download-dialog-box](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * 利用条件リンクをクリックして、左側のウィンドウにライセンス条件を表示します。

     >[!NOTE]
     >
     利用条件チェックボックスは、ライセンスされたアセットに対してのみ表示されます。 また、アセットダイアログボックスには、ライセンスが承認されたアセットのライセンス条件のプレビューのみが表示されます。 ダウンロードする前に [ アセットのライセンスを承認 ](/help/assets/approve-assets-content-hub.md) し、アセットダイアログボックスでライセンス条件のプレビューを有効にします。

   * 左側のペインの元のアセットレンディションに戻るには、「**元のレンディション」ボックス** をクリックします。
1. （ライセンスが付与されたアセットの）ライセンス条件に同意し、「**ダウンロード**」をクリックしてアセットをダウンロードします。

## 複数のライセンス済みAssetsのダウンロード{#multi-download}

1. アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。 表示されるダイアログボックスは、ダウンロードリストに期限切れのアセットが含まれているか、期限切れでないアセットのみが含まれているかによって異なります。<br/>
   **期限切れアセットをダウンロード** ダイアログボックス：このダイアログボックスでは、期限切れアセットのプレビューと有効期限が左側のペインに表示されます。 選択した合計のうち期限切れのアセットのカウントが右側のパネルに表示されます。 **すべてのアセットで続行** をクリックして、有効期限が切れたアセットを他のアセット（存在する場合）と共にダウンロードします。 アセットをダウンロード ダイアログボックスが表示されます。 詳しくは、[ アセットをダウンロード ](#Download-asset-dialog-box) ダイアログボックスを参照してください。

   >[!NOTE]
   >
   [ 有効期限切れのアセットのダウンロードオプションを有効にする ](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) と、アセットをダウンロードできます。 ダウンロードが有効になっている期限切れアセットのみをダウンロードできます。

   <a id="Download-asset-dialog-box"></a> **アセットをダウンロードダイアログボックス：** このダイアログボックスには、選択したアセットに関連付けられているライセンスのリストが左側のペインに表示されます。 ライセンスを選択すると、契約条件（PDF 形式）が中央のウィンドウにプレビューされ、関連するアセットのプレビューとカウントが右側のウィンドウに表示されます。 レビュー済みのライセンスは水色でハイライト表示されます。

   >[!NOTE]
   >
   **アセットをダウンロード」ダイアログボックス** は、承認されたライセンスに関するライセンス条件のみをプレビューします。 [ アセットのダウンロード ](/help/assets/approve-assets-content-hub.md) ダイアログボックスでライセンス条件をプレビューするには、アセットをダウンロードする前に **アセットのライセンスを承認** します。

1. ![remove-icon](/help/assets/assets/remove-icon.svg) をクリックして、ダウンロードダイアログボックスからライセンスを削除します。

1. 利用条件に同意し、「**ダウンロード**」をクリックして、使用可能なライセンスに関連付けられたアセットを左側のパネルでダウンロードします。
   ![複数ライセンスをダウンロード](/help/assets/assets/download-multiple-license.png)

### ライセンスのないAssetsのダウンロード {#download-non-licensed-assets}

ライセンスのないアセットをダウンロードするには、アセットを選択し、上部のパネルから ![ ダウンロード ](/help/assets/assets/download-icon.svg) をクリックします。







