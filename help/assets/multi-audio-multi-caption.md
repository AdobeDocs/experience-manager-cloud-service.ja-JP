---
title: OpenAPI機能を備えたDynamic Mediaのマルチオーディオとマルチキャプション ビデオ
description: Adobe Experience Manager Assets内でOpenAPI機能を使用して、Dynamic Mediaでビデオアセットの複数のオーディオトラックとキャプションを追加および管理する方法について説明します。
role: User
badgeSaas: label="AEM Assets" type="Positive"
source-git-commit: 80a32672ec018274b0410abfa14fdd761fdb5aba
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 15%

---


# OpenAPI機能を備えたDynamic Mediaのマルチオーディオとマルチキャプション ビデオ {#multi-audio-captions-dynamic-media-with-openapi-capabilities}

OpenAPI機能を備えた[!DNL Adobe Experience Manager Assets] Dynamic Mediaを使用すると、複数のオーディオトラックとキャプションファイルをビデオアセットに追加できます。 これにより、アクセシビリティの向上、ローカライズされた再生エクスペリエンスのサポート、世界中のオーディエンスへの動画配信の強化を実現できます。

これらの機能は、ビデオアセットのプロパティページの「**キャプションとオーディオトラック**」タブから直接管理されます。

>[!NOTE]
>
>OpenAPI機能を備えたDynamic Mediaのマルチオーディオおよびマルチキャプションのサポートは、限定的な可用性機能です。 [ サポートチケット ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)を作成して有効にできます。

サポートされているすべてのDynamic MediaとOpenAPI機能ビデオ形式は、複数のキャプションとオーディオトラックをサポートしています。

## 開始する前に {#before-you-begin}

以下を確認してください。

* ビデオアセットは[!DNL AEM Assets]で利用できます
* サポートされているオーディオ形式：`.mp3`
* サポートされているキャプション形式：`.vtt`

>[!NOTE]
>
>OpenAPI機能を備えたDynamic Mediaには、ビデオプロファイルは必要ありません。 デフォルトでは、**キャプションとオーディオトラック** タブはすべてのビデオアセットで使用できます。

## 複数のオーディオトラックを追加 {#add-audio-tracks}

![ キャプションとオーディオトラックのタブ ](/help/assets/assets/caption-audio-tracks1.png)

ビデオにオーディオトラックを追加するには：

1. アップロードされたビデオアセットに移動します。
1. アセットを選択し、「**プロパティ**」をクリックします。
1. 「**キャプションとオーディオトラック**」タブを開きます。
1. 「**オーディオトラックをアップロード**」をクリックします。
1. 1つ以上の`.mp3` ファイルを選択してください。
1. オーディオトラックファイル名の横にある&#x200B;**Draw** アイコンをクリックします。

**オーディオトラックを編集** ダイアログボックスで、次の操作を行います。

* **ファイル名** - アップロードされたファイルから派生したデフォルトのファイル名。
* **言語** - オーディオ言語を選択します。
* **Type** – 元の説明、標準の説明、または音声の説明。
* **ラベル** - プレーヤーのオーディオセレクターに表示される表示名。

![ オーディオトラックダイアログ ](/help/assets/assets/edit-audio1.png)

1. 「**保存**」をクリックします。
1. 必要に応じて、追加のオーディオトラックに対してこれを繰り返します。
1. 「**保存して閉じる**」をクリックします。

>[!NOTE]
>
>オーディオトラックラベルは一意である必要があります。

## 複数のキャプションを追加 {#add-captions}

![ キャプションとオーディオトラックのタブ ](/help/assets/assets/caption-audio-tracks1.png)

キャプションを追加するには：

1. ビデオ **プロパティ** ページを開きます。
1. 「**キャプションとオーディオトラック**」タブを開きます。
1. **キャプションを作成**/**ファイルをアップロード**&#x200B;をクリックします。
1. 1つ以上の`.vtt` ファイルを選択してください。
1. キャプションファイルの横にある&#x200B;**Draw** アイコンをクリックします。

![ キャプションダイアログのアップロード ](/help/assets/assets/upload-caption.png)

**キャプションを編集** ダイアログボックスで、次の操作を行います。

* **ファイル名** - デフォルトのアップロード済みファイル名。
* **言語** - キャプション言語。
* **種類** – 字幕またはキャプション。
* **ラベル** - プレーヤーのキャプションセレクターに表示される表示名。

![ キャプションを編集ダイアログ ](/help/assets/assets/edit-captions.png)

1. 「**保存**」をクリックします。
2. 「**保存して閉じる**」をクリックします。

>[!NOTE]
>
>字幕テキストの編集はサポートされていません。 ファイルを外部で更新し、再アップロードします。

## 承認行動 {#approval-behavior}

承認は、親ビデオアセットによって異なります。

* **Approved**&#x200B;の場合、新しいファイルは処理後に自動承認されます。
* 承認されていない場合は、親ライフサイクルに従います。

## ファイルライフサイクルのステータスの表示 {#status}

* **承認済み** – 再生準備完了
* **却下** - ファイルが拒否されました

## デフォルトのオーディオトラックを設定 {#set-default-audio}

デフォルトでは、元のオーディオが使用されます。

1. **キャプションとオーディオトラック**&#x200B;を開きます。
1. オーディオトラックを選択します。
1. 「**デフォルトとして設定**」をクリックします。

   ![既定のアクションとして設定](/help/assets/assets/set-default.png)

1. 「**OK**」をクリックします。
1. 「**保存して閉じる**」をクリックします。

## オーディオとキャプションのプレビュー {#preview-audio-captions}

処理後：

1. ビデオプレビューを開きます。

   ![ ビデオプレビュープレーヤー](/help/assets/assets/preview-caption-audio.png)

1. プレーヤーのコントロールの使用：

   * オーディオトラックの切り替え
   * キャプションを有効にする

## キャプションファイルまたはオーディオファイルのダウンロード {#download-tracks}

1. キャプションファイルまたはオーディオファイルを選択します。
1. 「**ダウンロード**」をクリックします。

   ![ トラックアクションのダウンロード ](/help/assets/assets/download-caption.png)

1. 「**ダウンロード**」をクリックします。

選択したファイルがローカルシステムにダウンロードされます。

## キャプションファイルまたはオーディオファイルの削除 {#delete-tracks}

1. キャプションファイルまたはオーディオファイルを選択します。
1. 「**削除**」をクリックします。

   ![ トラックアクションを削除](/help/assets/assets/delete-caption.png)

1. 「**OK**」をクリックします。

ビデオから抽出された元のオーディオは削除できません。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
