---
title: 複合アセットの管理
description: Adobe Indesign、Adobe IllustratorおよびAdobe Photoshopファイル内からAEMアセットへの参照を作成する方法を説明します。 また、ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなど、複数ページのファイルの個々のページを表示する方法についても説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 複合アセットの管理 {#managing-compound-assets}

Adobe Experience Manager（AEM） Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに AEM アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

Adobe Creative Cloud アプリケーションで AEM アセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

AEM Assets supports **bidirectional referencing**. 参照されたアセットは、アップロードされたファイルのアセットの詳細ページで検索できます。 さらに、AEM アセットの参照元のファイルは、参照先のアセットのアセットの詳細ページで確認できます。

参照は、参照先のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator 内で AEM アセットを参照として追加 {#refai}

既存の AEM アセットを、Adobe Illustrator ファイル内から参照できます。

デジタルアセットを追加するには、 [AEMデスクトップアプリを使用するか](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 、AEM [](/help/assets/manage-digital-assets.md#uploading-assets) ユーザーインターフェイスを使用してアップロードします。

ワークフローが完了したら、アセットのアセットの詳細ページに移動します。 既存の AEM アセットへの参照は、「**参照**」列の「**依存関係**」に一覧表示されます。The referenced assets that appear under **Dependencies** can also be referenced by files other than the current one.

参照元のファイルのリストを表示するには、「**依存関係**」にあるアセットをクリックします。Click the **View Properties** icon from the toolbar. プロパティページで、現在のアセットを参照しているファイルのリストが「**基本**」タブの「**参照**」列に表示されます。

## Adobe InDesign 内で AEM アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

InDesignファイル内からAEMアセットを参照するには、AEMアセットをInDesignファイルにドラッグするか、InDesignファイルをZIPファイルとして書き出します。

参照先のアセットは AEM Assets に既に存在します。サブアセットは、Adobe inDesignサーバーを設定して抽出できます。 InDesignファイルに埋め込まれたアセットは、サブアセットとして抽出されます。

>[!NOTE]
>
>InDesign サーバーにプロキシが設定されている場合、InDesign のファイルのプレビューが XMP メタデータ内に組み込まれています。この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesign にプロキシが設定されていない場合、InDesign のファイルでサムネールを明示的に抽出する必要があります。

### Create references by dragging AEM assets {#create-references-by-dragging-aem-assets}

The procedure is similar to [Adding AEM assets as references in Adobe Illustrator](#refai).

### ZIP ファイルに書き出して アセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 新しいワークフローを作成します。
1. Adobe InDesign のパッケージ機能を使用して、ドキュメントを書き出します。
Adobe InDesign ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、書き出されたフォルダーには、InDesign ファイル内のサブアセットを格納するための Links フォルダーが含まれます。
1. ZIP ファイルを作成し、このファイルを AEM リポジトリにアップロードします。
1. 解凍ワークフローを開始します。
1. ワークフローが完了すると、Linksフォルダー内の参照が自動的にサブアセットとして参照されます。参照されたアセットのリストを表示するには、アセットの詳細ページに移動します。

## Adobe Photoshop 内で AEM アセットを参照として追加 {#refps}

デジタルアセットを追加するには、 [AEMデスクトップアプリを使用するか](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 、AEM [](/help/assets/manage-digital-assets.md#uploading-assets) ユーザーインターフェイスを使用してアップロードします。

ワークフローが完了すると、既存のAEMアセットへの参照がアセットの詳細ページに表示されます。 参照先のアセットには、参照元のアセットのリストも含まれます。参照されているアセットのリストを表示するには、アセットの詳細ページに移動します。

>[!NOTE]
>
>複合アセット内のアセットは、ドキュメントIDとインスタンスIDに基づいて参照することもできます。 この機能は、Adobe Illustrator と Adobe Photoshop のバージョンでのみ使用できます。その他の場合、AEM の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

AEM Assets のページビューア機能を使用すると、複数ページファイルの個々のページ（PDF、INDD、PPT、PPTX、Ai ファイルなど）を表示できます。InDesign では、InDesign サーバーを使用してページを抽出できます。InDesign ファイルの作成中にページのプレビューが保存されている場合は、ページを抽出するために InDesign サーバーを使用する必要はありません。

アセットページからファイルの個々のページを閲覧できます。ツールバーのオプションを使用してファイルの個々のページに注釈を追加できます。You can also use the **Page Overview** option to view all the pages simultaneously.

1. 複数ページファイルが含まれる AEM Assets のフォルダーに移動します。
1. アセットをクリックして、そのアセットのページを開きます。
1. グローバルナビゲーションアイコンをクリックし、メニューから「**ページ**」を選択します。
1. 画像の下の左右アイコンをクリックしてファイルの個々のページに移動します。
1. To annotate a page, click the **Annotate** icon from the toolbar and add a comment.
1. To download the file, click the **Download** icon.
1. To view all pages of the file simultaneously, click the **Page Overview** icon.
1. To view the activity stream for the file, including annotations and downloads, click the AEM icon and then choose **Timeline** from the menu.
1. To view and edit the metadata properties of the page, click the **View Properties** icon from the toolbar.
