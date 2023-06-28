---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.10.0 リリースのリリースノート。'
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 84%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.10.0 リリースノート {#release-notes}

以下の節では、の2022.10.0版の機能リリースノートの概要を説明します。 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の月間リリース（2022.10.0）のリリース日は 2022 年11月10日です。次の毎月のリリース (2023.1.0) は、2023 年 2 月 9 日に予定されています。

## リリースビデオ {#release-video}

2022.10.0 リリースで追加された機能の概要については、2022年10月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### の新機能[!DNL Sites] {#sites-features}

* この [エクスペリエンスフラグメントの「パーソナライゼーション」タブ](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) では、エクスペリエンスフラグメントエディターに対してセグメント化の仕様機能を使用でき、ネストされたエクスペリエンスフラグメントを柔軟に作成できるので、複数のセグメントに対してヘッダーとフッターのバリエーションを作成できます。 この機能を開始する前は、AEM が提供するパーソナライゼーションはサイトのページでのみ使用できますが、エクスペリエンスフラグメントでは使用できません

* この[コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)では、ユーザーが翻訳されたコンテンツフラグメントを効率的に管理できるようになりました。 すべての言語コピーを表示するための 1 回のクリックアクセスが提供されています。 また、ユーザーは、関心があるロケールに基づいてテーブル表示をフィルタリングすることもできます。

![コンテンツフラグメントの言語](/help/release-notes/assets/cfconsole-languages.png)

* テンプレートの画像サイズ設定を最適化することで、訪問者のページ読み込み時間をさらに短縮します。 画像コンポーネントの詳細については、[コア WCM コンポーネント](https://github.com/adobe/aem-core-wcm-components)を参照してください

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Experience Manager Assets で、他のサポートされている形式のドキュメントをアップロードし、[付属の Document Cloud ビューアを使用してプレビューができるようになりました](/help/assets/manage-pdf-documents.md)。サポートされる形式の種類には、TXT、RTF、DOC、DOCX、PPT、PPTX、XLS、XLSX が含まれます。

  ![他の形式向けの PDF レンディション](/help/release-notes/assets/multi-page-other-formats.png)


### [!DNL Assets] プレリリースの新機能 {#prerelease-features-assets}

* Experience Manager Assets は、画像スマートタグ用に改善された人工知能フレームワークを使用するようになりました。 このコンテンツインテリジェンスにより、取り込み時にすべての画像アセットで使用できるスマートタグの関連性と精度が向上します。 さらに、向き情報が`cq:tags`に取り込まれ、向きフィルターを使用してより良い検索結果が得られます。

  ベータ版への参加を希望される場合は、11月14日までに [このフォームに入力](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) してください。

* Experience Manager Assets now は、Azure Blob ストレージデータ ソースに接続し、一括インポート ツールを使用してアセットを取り込む際に、認証用のアクセス キーに加えて [SAS Token](/help/assets/add-assets.md#asset-bulk-ingestor) をサポートするようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブフォームテンプレートエディター**：テンプレートエディターを使用すると、組織のアダプティブフォームの基本構造と外観を事前に定義することができます。このリリースでは、テンプレートエディターが次のように改善されました：
   * **[テンプレートエディターのフォームデータモデル](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**：テンプレートエディター内で、フォームデータモデルスキーマをアダプティブフォームテンプレートに関連付けることができます。 これにより、アダプティブフォームの作成に要する時間を短縮します。 このオプションはアダプティブ フォームエディターにも追加され、ユーザーは既存のフォームのフォームデータモデルを選択または変更することができます。
   * **[テンプレートエディターでのレコードのドキュメント](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**：テンプレートを使用して作成されたすべてのフォームのレコードのドキュメント生成を標準化できるようになりました。これにより、組織の要件に対するコンプライアンスと標準化が強化されます。

* **[AEM Sites ページからアダプティブフォームウィザードを起動](/help/forms/embed-adaptive-form-aem-sites.md)**：AEM Sites ページでは、アダプティブフォームのサポートが拡張されました。AEM Sites ページを表示したまま、新しいアダプティブフォームを作成したり、既存のアダプティブフォームを埋め込んだりすることができるようになりました。
* **[DoR でチェックボックスとラジオボタンの表示の配置を変更](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**：レコードのドキュメントのチェックボックスおよびラジオボタンに対して、配置（水平、垂直、アダプティブフォームと同じ）を設定できるようになりました。このオプションは、レコードのドキュメント内でのチェックボックスおよびラジオボタンの位置を決定します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 作成者は、エクスペリエンスフラグメントを使用して、製品リストを動的にエンリッチメントできます（例：製品リスト間にバナーを配置）。
* リストコンポーネントは、関連する製品／カテゴリーページをサポートして、関連ページを動的に表示するようになりました。
* Peregrine 12.5 コンポーネントのサポートが追加されました。
* 製品ティーザーおよびカルーセルでのクライアントサイドの価格読み込みサポートが追加されました。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* AEM as a Cloud Service（オーサーサービス）が統合シェルと統合され、ユーザーエクスペリエンスが向上し、他のすべての Experience Cloud アプリケーションと統合されました。AEM as a [統合シェルのCloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) を参照してください。

* リリースノートで前述したように、10 MB を超えるコンテンツパッケージ（バイナリを含まないプロパティを持つノード）を配布するためのレプリケーションエージェント管理画面またはレプリケーション API を使用する方法は、非推奨（廃止予定）となりました。 詳しくは、 [公開を管理](/help/operations/replication.md#manage-publication) または [コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow) を参照してください。

* Dispatcher 設定で、一般的なマーケティングキャンペーンのクエリパラメーターをリストするファイルが参照されるようになりました。顧客が関連するパラメーターのコメント解除を選択できるので、キャッシュが改善されました。詳しくは、 [マーケティングキャンペーンパラメーター](/help/implementing/dispatcher/caching.md#marketing-parameters) を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
