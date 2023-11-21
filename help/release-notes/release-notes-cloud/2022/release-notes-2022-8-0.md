---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.8.0 リリースのリリースノート。'
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 55%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.8.0 リリースノート {#release-notes}

以下の節では、の 2022.8.0 バージョンの機能リリースノートの概要を説明します [!DNL Experience Manager] as a Cloud Service。

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
   * は、 [コア WCM コンポーネント](https://github.com/adobe/aem-core-wcm-components) は、編集可能テンプレートとスタイルシステムをサポートしています。
   * では、電子メールで最適化された 10 個の実稼動用コンポーネント（ページ、コンテナ、タイトル、テキスト、画像、ボタン、ティーザー、エクスペリエンスフラグメント、コンテンツフラグメント、セグメント化）を提供しています。
   * は、 [キャンペーン変数の挿入](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) ほとんどのダイアログフィールドで、また柔軟な [セグメント化コンポーネント](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * は、 [CSS スタイルインライナー](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、 [HTML属性インライナー](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、および [HTML消毒剤](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * どこでも E メールを作成できます。

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* The [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) には、コンテンツフラグメントに関連付けられている言語コピーの合計数を表示するオプションが用意されています。 すべての言語コピーを表示するための 1 回のクリックアクセスが提供されています。 また、ユーザーは、関心があるロケールに基づいてテーブル表示をフィルタリングすることもできます。

![コンテンツフラグメントの言語](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#features-assets}

* これで、Adobe Experience Manager Assetsを [MIME タイプに基づいてユーザーがアップロードできるアセットのタイプを制限します](/help/assets/configure-asset-upload-restrictions.md).

  ![アセットアップロードの制限](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* [アダプティブフォームウィザード](/help/forms/creating-adaptive-form.md)：AEM Forms は、ビジネスユーザー向けの使いやすいウィザードで、アダプティブフォームをすばやく作成することができます。このウィザードはクイックタブナビゲーション機能を備えており、アダプティブフォームを作成するための事前設定済みのテンプレート、スタイル設定、フィールド、送信オプションを簡単に選択することができます。このリリースでは、ウィザードが次のように改善されました：

   * フィールドの選択または選択解除：ウィザードを使用して、JSON およびフォームデータモデルスキーマに基づくアダプティブフォームを作成できます。 スキーマ内のフィールドのサブセットを選択して、アダプティブフォームに含めることができるようになりました。 選択したフィールドは、対応するアダプティブフォームのデータキャプチャコンポーネントに変換され、目的のアダプティブフォームをすばやく作成することができます。

   * 静的テンプレートを使用：従来の静的テンプレートにすでに投資している顧客は、ウィザードで静的テンプレートを使用してアダプティブ フォームを作成することにより、クラウド導入のジャーナリストを続けることができます。これにより、顧客にとっての、古い静的テンプレートを最新の編集可能なテンプレートに移行する時間が増加します。

* [サーバーサイドの処理中にレコードのドキュメント（DoR）から非表示のフィールドを削除する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)：データキャプチャエクスペリエンス中にエンドユーザーに表示されたフィールドのみを含む、エンド ユーザー用のレコード PDF ドキュメントを生成することができます。フォームの送信時に、サーバーは、送信されたデータに基づいてユーザーに対して非表示にされたフィールドを検証し、レコードのドキュメントとの一貫性を保つために除外します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* AEM ページのプロパティと製品コックピットの概要を介した、製品およびカテゴリに対する AEM ページの関連付け
  ![製品コックピットページの関連付け](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
