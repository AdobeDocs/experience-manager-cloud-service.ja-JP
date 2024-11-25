---
title: コンテンツハブからのアセットのダウンロード
description: コンテンツハブポータルからアセットをダウンロードする方法について説明します。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 94%

---

# コンテンツハブからのアセットのダウンロード {#download-assets}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![アセットのダウンロード](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コンテンツハブでは、アセットをダウンロードして共有できます。これらのアセットには、画像、ビデオ、またはその他のデジタルコンテンツが含まれる場合があります。コンテンツハブでは、効果的なアセット配布用のアクセシビリティと適応性が強化されます。

コンテンツハブを使用して、1 つまたは複数のアセットをダウンロードできます。アセットの元のバージョンがダウンロードされます。

## 1 つのライセンス済みアセットのダウンロード {#single-download-asset}

アセットを選択し、上部のパネルから ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックします。アセットをダウンロードダイアログボックスにアセットのライセンスが表示されます。ライセンスの利用条件に同意し、「**ダウンロード**」をクリックします。
または、アセットカードの ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックして、アセットをダウンロードします。

### アセットから 1 つのライセンス済みアセットをダウンロードダイアログボックス {#single-download-from-asset-dialog-box}

1. アセットのサムネールをクリックします。アセットダイアログボックスが表示されます。
1. 右端のツールバーから ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックします。ダウンロードパネルには、アセットのレンディションとライセンスの利用条件の同意チェックボックスが表示されます。
   ![1 つのダウンロードダイアログボックス](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * 利用条件リンクをクリックすると、左側のパネルにライセンス条件が表示されます。

     >[!NOTE]
     >
     利用条件チェックボックスは、ライセンス済みアセットに対してのみ表示されます。また、アセットダイアログボックスには、ライセンスが承認されたアセットのみのライセンス利用条件のプレビューが表示されます。ダウンロードする前に[アセットのライセンスを承認](/help/assets/approve-assets-content-hub.md)すると、アセットダイアログボックスでライセンス条件のプレビューが有効になります。

   * 「**元のレンディションボックス**」をクリックすると、左側のパネルの元のアセットレンディションに戻ります。
1. ライセンスの利用条件（ライセンス済みアセットの場合）に同意し、「**ダウンロード**」をクリックして、アセットをダウンロードします。

## 複数のライセンス済みアセットのダウンロード{#multi-download}

1. アセットを選択し、上部のパネルから ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックします。表示されるダイアログボックスは、ダウンロードリストに有効期限切れのアセットが含まれているか、有効期限切れでないアセットのみが含まれているかによって異なります。<br/>
   **有効期限切れのアセットをダウンロードダイアログボックス**：このダイアログボックスでは、有効期限切れのアセットのプレビューと有効期限の日付が左側のパネルに表示されます。選択した合計のうちの有効期限切れのアセットの数が右側のパネルに表示されます。有効期限切れのアセットを他のアセット（存在する場合）と共にダウンロードするには、「**すべてのアセットで続行**」をクリックします。アセットをダウンロードダイアログボックスが表示されます。詳しくは、[アセットをダウンロードダイアログボックス](#Download-asset-dialog-box)を参照してください。

   >[!NOTE]
   >
   [有効期限切れのアセットをダウンロードするには、ダウンロードオプションを有効](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub)にします。ダウンロードが有効になっている有効期限切れのアセットのみダウンロードできます。

   <a id="Download-asset-dialog-box"></a> **アセットをダウンロードダイアログボックス：**&#x200B;このダイアログボックスには、左側のパネルに選択したアセットに関連付けられているライセンスのリストが表示されます。ライセンスを選択すると、中央のパネルでその利用条件（PDF 形式）がプレビューされ、右側のパネルに関連付けられたアセットのプレビューとその数が表示されます。レビュー済みのライセンスは明るい青色でハイライト表示されます。

   >[!NOTE]
   >
   **アセットをダウンロードダイアログボックス**&#x200B;では、承認済みライセンスのライセンス利用条件のみがプレビューされます。アセットをダウンロードする前に[アセットのライセンスを承認](/help/assets/approve-assets-content-hub.md)し、**アセットをダウンロードダイアログボックス**&#x200B;でライセンス条件をプレビューします。

1. ![remove-icon](/help/assets/assets/remove-icon.svg) をクリックして、ダウンロードダイアログボックスからライセンスを削除します。

1. 利用条件に同意し、「**ダウンロード**」をクリックして、左側のパネルで使用可能なライセンスに関連付けられたアセットをダウンロードします。
   ![複数ライセンスをダウンロード](/help/assets/assets/download-multiple-license.png)

### ライセンスのないアセットのダウンロード {#download-non-licensed-assets}

ライセンスのないアセットアセットをダウンロードするには、アセットを選択し、上部のパネルから ![ダウンロード](/help/assets/assets/download-icon.svg) をクリックします。







