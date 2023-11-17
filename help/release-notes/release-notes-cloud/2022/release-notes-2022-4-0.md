---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 リリースのリリースノート。'
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 86%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.4.0 リリースノート {#release-notes}

以下の節では、の 2022.4.0 バージョンの機能リリースノートの概要を説明します [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新リリース（2022.4.0）のリリース日は 2022年05月5日（PT）です。次回のリリース（2022.5.0）は 2022年6月9日（PT）に予定されています。

## リリースビデオ {#release-video}

2022.4.0 リリースで追加された機能の概要については、[2022年4月リリースの概要](https://video.tv.adobe.com/v/342612?quality=12)ビデオをご覧ください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#sites-features}

* コンテンツモデルのデータ型が、コンテンツモデルエディターで簡単なチェックボックスを使用して[翻訳可能](/help/assets/content-fragments/content-fragments-models.md#properties)として定義できるようになりました。また、AEM翻訳ルールと設定は自動的に更新されます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* タグピッカーウィンドウで、タグ名、作成日、変更日を基準に、[タグの並べ替え](/help/assets/organize-assets.md#use-tags-to-organize-assets)を昇順または降順に実行できるようになりました。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **通信 - Forms as a Cloud Service SDK でのドキュメント操作 API のサポート**：[ドキュメント操作 API](/help/forms/aem-forms-cloud-service-communications.md) は、PDF 文書の結合、並べ替え、検証に役立ちます。AEM Forms as a Cloud Service SDK を利用して、ローカル開発環境で通信 - ドキュメント生成 API を使用できるようになりました。

* **レコードのドキュメントの生成にカスタム XCI を使用**：[レコードのドキュメントの様々なプロパティを設定するために、カスタム XCI ファイルを使用](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file)できるようになりました。カスタムの変更でマスター XCI を上書きします。レコードのドキュメントの生成をより詳細に制御し、パーソナライゼーションやカスタマイズの機会を増やします。

* **アダプティブフォーム内で非表示の CAPTCHA を使用**：[非表示の CAPTCHA を使用して、疑わしいアクティビティの場合にのみ CAPTCHA チャレンジを表示](/help/forms/captcha-adaptive-forms.md)させることができます。疑わしいアクティビティが検出されない場合、CAPTCHA チャレンジは表示されません。これにより、チェックボックス要件を使わずに人間がフォームを完成させたかどうかを評価し、カスタマイズ作業を軽減し、エンドユーザーエクスペリエンスを向上させることができます。

* **フォームデータモデルの設定**：[複数の環境でフォームデータモデルの設定を再利用する](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)を使用して、データ統合をシンプル化し、IT コストを削減できるようになりました。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### SDK ビルドアナライザー {#sdk-build-analyzers}

AEM as a Cloud Service の SDK ビルドアナライザー Maven プラグインでは、依存関係の欠落など、Maven プロジェクトの問題を検出します。これを使用すると、ローカル開発中に、Cloud Manager でクラウド環境にデプロイする前に開発者が問題を見つけることができます。

新しいアナライザーが最近追加されました。

* `content-packages-validation`  — デプロイメント中にインストールされるパッケージの適切な形式のコンテンツ構文および構造を検証します。

まだ行っていない場合は、アナライザーの最新バージョンで Maven プロジェクトを更新するか、アナライザーを含めることを強くお勧めします。詳しくは、[こちらのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=ja)を参照してください。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基盤セキュリティ {#foundation-security}

### TLS 1.0、1.1 の廃止

2022 年 6 月 30 日以降、Experience Manageras a Cloud Serviceは、より安全なネットワーク通信とユーザーシステムとのデータ交換を必要とします。 AEMは、TLS(Transport Layer Security)1.2 プロトコルのみを使用する予定です。 古い TLS バージョン 1.0 および 1.1 は非推奨（廃止予定）となりました。

古いバージョンの TLS 1.0 および 1.1 を引き続き使用する場合、Experience Manager as a Cloud Service のへのアクセス権が失われる可能性があります。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
