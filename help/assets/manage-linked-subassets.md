---
title: 複合アセットの管理
description: InDesign、Adobe Illustrator および Photoshop のファイルから AEM Assets への参照を作成する方法について説明します。また、ページビューア機能を使用して、複数ページファイル（PDF、INDD、PPT、PPTX、AI ファイルなど）の個々のページを表示する方法についても説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 複合アセットの管理 {#managing-compound-assets}

Adobe Experience Manager（AEM） Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに AEM アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

Adobe Creative Cloud アプリケーションで AEM アセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

AEM Assets supports **bidirectional referencing**. 参照されたアセットは、アップロードされたファイルのアセットの詳細ページで検索できます。 さらに、AEM アセットの参照元のファイルは、参照先のアセットのアセットの詳細ページで確認できます。

参照は、参照先のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator 内で AEM アセットを参照として追加 {#refai}

既存の AEM アセットを、Adobe Illustrator ファイル内から参照できます。

1. Using [AEM desktop app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html), mount AEM Assets repository as a drive on your local machine. マウントしたドライブ内で、参照するアセットの場所に移動します。
1. マウントしたドライブから Illustrator ファイルにアセットをドラッグします。
1. Save the Illustrator file to the mounted drive, or [upload](/help/assets/manage-digital-assets.md#uploading-assets) to the AEM repository.
1. ワークフローが完了したら、アセットのアセットの詳細ページに移動します。 既存の AEM アセットへの参照は、「**参照**」列の「**依存関係**」に一覧表示されます。

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. The referenced assets that appear under **Dependencies** can also be referenced by files other than the current one. 参照元のファイルのリストを表示するには、「**依存関係**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Click the **View Properties** icon from the toolbar. プロパティページで、現在のアセットを参照しているファイルのリストが「**基本**」タブの「**参照**」列に表示されます。

   ![chlimage_1-86](assets/chlimage_1-86.png)

## Adobe InDesign 内で AEM アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

InDesignファイル内からAEMアセットを参照するには、AEMアセットをInDesignファイルにドラッグするか、InDesignファイルをZIPファイルとして書き出します。

参照先のアセットは AEM Assets に既に存在します。<!-- You can extract subassets by [configuring InDesign server](/help/assets/indesign.md). Embedded assets in an InDesign file are extracted as subassets. -->

>[!NOTE]
>
>InDesign サーバーにプロキシが設定されている場合、InDesign のファイルのプレビューが XMP メタデータ内に組み込まれています。この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesign にプロキシが設定されていない場合、InDesign のファイルでサムネールを明示的に抽出する必要があります。

### AEM アセットをドラッグして参照を作成 {#create-references-by-dragging-aem-assets}

この手順は、[Adobe Illustrator で AEM アセットを参照として追加する](#refai)場合の手順と同様です。

### ZIP ファイルに書き出して AEM アセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 新しいワークフローモデルを作成します。
1. Adobe InDesign のパッケージ機能を使用して、ドキュメントを書き出します。
Adobe InDesign ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、書き出されたフォルダーには、InDesign ファイル内のサブアセットを格納するための Links フォルダーが含まれます。
1. ZIP ファイルを作成し、このファイルを AEM リポジトリにアップロードします。
1. 解凍ワークフローを開始します。
1. When the workflow completes, the references in the Links folder are automatically referenced as subassets. To view a list of referred assets, navigate to the asset details page of the InDesign asset and close the [Rail](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

## Adobe Photoshop 内で AEM アセットを参照として追加 {#refps}

1. WebDav クライアントを使用して、AEM Assets をドライブとしてマウントします。
1. Photoshop ファイルに AEM アセットへの参照を作成するには、Photoshop のリンクを配置機能を使用して、マウントしたドライブで対応するアセットに移動します。

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Save in Photoshop file to the mounted drive or or [upload](/help/assets/manage-digital-assets.md#uploading-assets) to the AEM repository.
1. ワークフローが完了したら、既存の AEM アセットへの参照がアセットの詳細ページに一覧表示されます。

   To view the referenced assets, close the [Rail](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector) in the asset details page.

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [Rail](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合アセット内のアセットは、ドキュメントIDとインスタンスIDに基づいて参照することもできます。 この機能は、Adobe Illustrator と Adobe Photoshop のバージョンでのみ使用できます。その他の場合、AEM の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

AEM Assets のページビューア機能を使用すると、複数ページファイルの個々のページ（PDF、INDD、PPT、PPTX、Ai ファイルなど）を表示できます。InDesign では、InDesign サーバーを使用してページを抽出できます。InDesign ファイルの作成中にページのプレビューが保存されている場合は、ページを抽出するために InDesign サーバーを使用する必要はありません。

アセットページからファイルの個々のページを閲覧できます。ツールバーのオプションを使用してファイルの個々のページに注釈を追加できます。You can also use the **Page Overview** option to view all the pages simultaneously.

1. 複数ページファイルが含まれる AEM Assets のフォルダーに移動します。
1. アセットをクリックして、そのアセットのページを開きます。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. グローバルナビゲーションアイコンをクリックし、メニューから「**ページ**」を選択します。

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. 画像の下の左右アイコンをクリックしてファイルの個々のページに移動します。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. To annotate a page, click the **Annotate** icon from the toolbar and add a comment.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. To download the file, click the **Download** icon.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. To view all pages of the file simultaneously, click the **Page Overview** icon.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. To view the activity stream for the file, including annotations and downloads, click the Global Nav ico and then choose **Timeline** from the menu.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. To view and edit the metadata properties of the page, click the **View Properties** icon from the toolbar.

   ![chlimage_1-95](assets/chlimage_1-95.png)
