---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: a8d632818dd0514d63a5cb544e4b64301819483f
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 16%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

>[!CAUTION]
>
>**ブラックフライデーおよびクリスマスメンテナンスの除外期間**
>
> AEMaaCS の自動メンテナンスは、次の期間 ( 午前 0 時(00:00) CET から開始し、終了 ) には実行されません。
>
>* 11 月 21 日（月）～12 月 5 日（月）
>* 12 月 19 日（月）～1 月 3 日（火）
>
> この期間は、ブラックフライデー、サイバーマンデー、クリスマス、お正月を対象としています。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の月別リリース (2022.10.0) は 2022 年 11 月 10 日です。 次の毎月のリリース (2023.1.0) は、2022 年 1 月 26 日に予定されています。

## リリースビデオ {#release-video}

2022.10.0リリースで追加された機能の概要については、 2022 年 10 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### の新機能[!DNL Sites] {#sites-features}

* この [エクスペリエンスフラグメントの「パーソナライゼーション」タブ](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) では、エクスペリエンスフラグメントエディターに対してセグメント化の仕様機能を使用できるほか、ネストされたエクスペリエンスフラグメントを柔軟に作成できるので、複数のセグメントに対してヘッダーとフッターのバリエーションを作成できます。 この機能を開始する前は、AEMが提供するパーソナライゼーションはサイトのページでのみ使用できますが、エクスペリエンスフラグメントでは使用できません

* この [コンテンツフラグメントコンソール](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) では、翻訳されたコンテンツフラグメントを効率的に管理できるようになりました。 すべての言語コピーを表示するための 1 回のクリックアクセスが提供されました。 また、ユーザーは、対象のロケールに基づいてテーブル表示をフィルタリングすることもできます。

![コンテンツフラグメントの言語](/help/release-notes/assets/cfconsole-languages.png)

* テンプレートの画像サイズ設定を最適化することで、訪問者のページ読み込み時間をさらに短縮します。 画像コンポーネントの詳細については、 [コア WCM コンポーネント](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Experience Manager Assetsで、他のサポートされている形式のドキュメントをアップロードし、[ 付属のDocument Cloudビューアを使用してプレビュー](/help/assets/manage-pdf-documents.md). サポートされる形式の種類には、TXT、RTF、DOC、DOCX、PPT、PPTX、XLS、XLSX が含まれます。

   ![他の形式のPDFレンディション](/help/release-notes/assets/multi-page-other-formats.png)


### の新機能 [!DNL Assets] プレリリース {#prerelease-features-assets}

* Experience Manager Assetsは、画像スマートタグに改善された人工知能フレームワークを使用するようになりました。 このコンテンツインテリジェンスにより、取り込み時にすべての画像アセットで使用できるスマートタグの関連性と精度が向上します。 さらに、向き情報は `cq:tags`を使用すると、向きフィルターによる検索結果の改善が可能になります。

   ベータ版への参加を希望される場合は、 [このフォームを入力](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) 11 月 14 日までに

* Experience Manager Assets now [は、SAS トークンをサポートします](/help/assets/add-assets.md#asset-bulk-ingestor) さらに、一括読み込みツールを使用してアセットを取り込むための Azure Blob ストレージデータソースに接続する際の認証用アクセスキーに加えて、

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **アダプティブFormsテンプレートエディター**:テンプレートエディターでは、組織のアダプティブFormsの基本的な構造と外観を事前に定義できます。 このリリースでは、テンプレートエディターが次のように改善されました。
   * **[テンプレートエディターのフォームデータモデル](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**:テンプレートエディターで、フォームデータモデルスキーマをアダプティブフォームテンプレートに関連付けることができます。 これにより、アダプティブフォームの作成に要する時間を短縮できます。 また、このオプションはアダプティブFormsエディターに追加され、既存のフォームのフォームデータモデルを選択または変更することができます。
   * **[テンプレートエディターでのレコードのドキュメント](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**:テンプレートを使用して作成されるすべてのフォームに対して、レコードのドキュメントの生成を標準化できるようになりました。 これにより、組織要件のコンプライアンスおよび標準化を強化できます。

* **[AEM Sitesページからアダプティブフォームウィザードを起動します。](/help/forms/embed-adaptive-form-aem-sites.md)**:AEM Sitesページでは、アダプティブFormsのサポートが拡張されました。 これで、新しいアダプティブフォームを作成したり、既存のアダプティブフォームを埋め込んだりできます。これは、AEM Sitesページに留まったままです。
* **[DoR でチェックボックスとラジオボタンの表示の配置を変更する](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**:レコードのドキュメントのチェックボックスおよびラジオボタンに対して、目的の配置 ( 水平、垂直、アダプティブFormsと同じ ) を設定できるようになりました。 このオプションは、レコードのドキュメント内でのチェックボックスおよびラジオボタンの位置を決定します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 作成者は、エクスペリエンスフラグメントを使用して製品リストを動的にエンリッチメントできます ( 例：製品リスト間にバナーを配置 )。
* リストコンポーネントで、関連する製品/カテゴリページをサポートし、関連するページを動的に表示できるようになりました。
* Peregrine 12.5 コンポーネントのサポートが追加されました。
* 製品ティーザーおよびカルーセルでのクライアント側の価格の読み込みのサポートが追加されました。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* AEMas a Cloud Service（オーサーサービス）が統合シェルと統合され、ユーザーエクスペリエンスが向上し、他のすべてのExperience Cloudアプリケーションと統合されました。 AEM as a を参照してください。 [統合シェルのCloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) を参照してください。

* リリースノートで前述したように、10 MB（バイナリを含まないプロパティを持つノード）を超えるコンテンツパッケージを配布するためのレプリケーションエージェント管理画面またはレプリケーション API を使用することは非推奨となり、近日中に適用されます。 詳しくは、 [公開を管理](/help/operations/replication.md#manage-publication) または [コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow) を参照してください。

* Dispatcher 設定で、一般的なマーケティングキャンペーンクエリパラメーターをリストするファイルを参照するようになりました。 お客様は、関連するパラメーターのコメントを解除することを選択できるので、キャッシュが改善されました。 参照： [マーケティングキャンペーンパラメーター](/help/implementing/dispatcher/caching.md#marketing-parameters) を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
