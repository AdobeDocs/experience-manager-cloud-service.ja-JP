---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 8008bd1076b2f2170f2c95685017854f8bf09646
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 23%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.8.0) は 2022 年 9 月 1 日です。
次回のリリース (2022.10.0) は 2022 年 11 月 10 日に予定されています。

## リリースビデオ {#release-video}

2022.8.0 リリースに追加された機能の概要については、 2022 年 8 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* 電子メールコンポーネントを使用すると、AEMでコンテンツを作成し、Campaign Classic経由で電子メールとして配信できます。 コア電子メールコンポーネント：
   * は [コア WCM コンポーネント](https://github.com/adobe/aem-core-wcm-components) は、編集可能テンプレートとスタイルシステムをサポートしています。
   * では、電子メールで最適化された 10 個の実稼動用コンポーネント（ページ、コンテナ、タイトル、テキスト、画像、ボタン、ティーザー、エクスペリエンスフラグメント、コンテンツフラグメント、セグメント化）を提供しています。
   * は、 [キャンペーン変数の挿入](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) ほとんどのダイアログフィールドで、また柔軟な [セグメント化コンポーネント](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * は、 [CSS スタイルインライナー](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、 [HTML属性インライナー](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、および [HTML消毒剤](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * どこでも E メールを作成できます。

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* この [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) には、コンテンツフラグメントに関連付けられている言語コピーの合計数を表示するオプションが用意されています。 すべての言語コピーを表示するための 1 回のクリックアクセスが提供されました。 また、ユーザーは、対象のロケールに基づいてテーブル表示をフィルタリングすることもできます。

![コンテンツフラグメントの言語](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#features-assets}

* Adobe Experience Manager Assets を [MIME タイプに基づいてユーザーがアップロードできるアセットのタイプを制限します](/help/assets/configure-asset-upload-restrictions.md).

   ![アセットのアップロード制限](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* [アダプティブFormsウィザード](/help/forms/creating-adaptive-form.md):AEM Formsは、アダプティブFormsをすばやくオーサリングするための、ビジネスユーザーにとってわかりやすいウィザードを提供します。 このウィザードでは、事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択して、アダプティブフォームを作成するためのクイックタブナビゲーションが用意されています。 このリリースでは、ウィザードが次のように改善されました。

   * フィールドを選択または選択解除します。ウィザードでは、JSON およびフォームデータモデルスキーマに基づくアダプティブフォームを作成できます。 スキーマ内のフィールドのサブセットを選択して、アダプティブフォームに含めることができるようになりました。 選択したフィールドは、対応するアダプティブフォームのデータキャプチャコンポーネントに変換され、目的のアダプティブフォームをすばやく作成できます。

   * 静的テンプレートを使用：既存のレガシー静的テンプレートへの投資をお持ちのお客様は、ウィザードで静的テンプレートを使用してアダプティブフォームを作成することで、クラウドの採用プロセスを継続的に進めることができます。 これにより、古い静的テンプレートを最新の編集可能なテンプレートに移行する時間が増えます。

* [サーバーサイドの処理中にレコードのドキュメント (DoR) から非表示のフィールドを削除する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md):データ取得エクスペリエンスで表示されたフィールドのみを含むエンドユーザーのレコードのドキュメントPDFを生成できます。 フォームの送信時に、サーバーは送信されたデータに基づいてエンドユーザーに対して非表示にされたフィールドを検証し、レコードのドキュメントから一貫性を保つために除外します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* AEMページのプロパティを介した製品およびカテゴリへのAEMページの関連付けと、製品コックピットでの概要
   ![製品コックピットページ協会](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
