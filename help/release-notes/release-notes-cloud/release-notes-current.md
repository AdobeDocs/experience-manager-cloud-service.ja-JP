---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 400e9fa0263b3e9bdae10dc80d524b291f99496d
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 21%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下の節では、の現在（最新）バージョンの機能リリースノートの概要を説明します [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021 年、2022 年のバージョンなど）のリリースノートに移動できます。
>
>以下をご覧ください： [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) の今後の機能のアクティベーションについて [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.1.0) は 2023 年 2 月 10 日です。 次の機能リリース (2023.2.0) は、2023 年 3 月 3 日に予定されています。

## リリースビデオ {#release-video}

2023.1.0 リリースに追加された機能の概要については、 2023 年 1 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースの新機能 {#prerelease-features-sites}

* AEM GraphQLコンテンツ配信 API でGraphQLがサポートされるようになりました [ページング](/help/headless/graphql-api/content-fragments.md#paging) および [並べ替え](/help/headless/graphql-api/content-fragments.md#sorting)を使用して、大きなコンテンツセットの取得とレンダリングをより効率的におこなうことができます。 GraphQLのページネーションを使用すると、すべてを一度に返すのではなく、サブセットで結果を返すことで、クエリの応答時間を短縮できます。 GraphQLでの並べ替えでは、コンテンツセットを目的の順序で配置できるので、クライアントアプリケーションでのコンテンツの処理が容易になります。  AEM GraphQLエンジンのハイブリッドフィルタリングにより、クエリの応答時間がさらに短縮されました。 コンテンツは、クエリフィルターに対応する小さなセットで JCR から読み取られるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* アセットレポートに、管理者が次の操作を実行できるようになりました。 [アセットダウンロードレポートを生成](/help/assets/asset-reports.md) Experience Manager Assetsas a Cloud Serviceデプロイメントから。 このデータにより、管理者はさらに、企業やお客様での Assets の採用状況を測定するために、主要な成功指標から洞察を得ることができます。

   ![他の形式向けの PDF レンディション](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets now は、Azure Blob ストレージデータ ソースに接続し、一括インポート ツールを使用してアセットを取り込む際に、認証用のアクセス キーに加えて [SAS Token](/help/assets/add-assets.md#asset-bulk-ingestor) をサポートするようになりました。

* asset computeでの CMYK 画像の管理が改善され、CMYK 画像用のスマート切り抜きとスマートタグを生成できるようになりました。

### [!DNL Assets] プレリリースの新機能 {#prerelease-features-assets}

* Experience Manager Assetsは、 [Google Cloud Platform からの大規模なアセットの取り込み](/help/assets/add-assets.md#asset-bulk-ingestor) 一括読み込みツールを使用して読み込みます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[非インタラクティブワークフロードキュメントと印刷可能なPDF出力を生成するためのワークフローステップ](/help/forms/aem-forms-workflow-step-reference.md)**:AEM Workflow ステップを使用して、非インタラクティブPDFドキュメントの作成とビジネスプロセスの印刷可能な出力の自動化を行い、ドキュメント生成プロセスを合理化し、時間を節約します。
* **[脚注を使用して、アダプティブFormsで引用文や追加情報を提供する](/help/forms/footnotes-richtextsupport.md)**:アダプティブフォーム内の脚注を使用して、フォームの入力方法や使用方法に関する情報を表示します。 また、括弧で囲まれた情報や著作権に関する権限、その他の役に立つ情報を提供する場合にも使用できます。

### [!DNL Forms] プレリリースの新機能 {#prerelease-features-forms}

* **[データキャプチャコアコンポーネントを使用したアダプティブFormsの構築](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [アダプティブFormsエディターを使用](/help/forms/creating-adaptive-form-core-components.md) 標準化されたデータキャプチャコンポーネント（コアコンポーネント）に基づいてフォームを作成する場合。 これらのコンポーネントは、カスタマイズ機能を提供し、開発時間を短縮し、デジタル登録エクスペリエンスのメンテナンスコストを削減します。
* **[アダプティブFormsに基づくコアコンポーネントのスタイル設定のためのフロントエンドパイプラインのサポート](/help/forms/using-themes-in-core-components.md)**:コアコンポーネントベースのアダプティブFormsに対して、容易にカスタマイズ可能な BEM ベースのテーマを利用し、フロントエンドデプロイメントパイプラインと共にデプロイして、フォームのルックアンドフィールを強化します。
* **[コアコンポーネントベースのアダプティブFormsに関するレコードのドキュメントを生成する](/help/forms/generate-document-of-record-core-components.md)**:長期保存用、印刷またはドキュメント形式での送信時に、コアコンポーネントベースのアダプティブフォームのレコードを作成します。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Microsoft SharePointとMicrosoft OneDrive にアダプティブFormsを送信する](/help/forms/configuring-submit-actions.md)**:Microsoft SharePointとMicrosoft OneDrive の両方にアダプティブフォームのデータを直接送信できるので、データ送信を効率化します。 スキーマベースのデータとスキーマレスのデータの両方を送信できます。 これらの送信アクションは、既に使用可能な送信アクションに加えて実行されます。
* **[「アダプティブフォームをテンプレートとして保存」機能を使用した効率的なフォーム作成](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:アダプティブフォームをテンプレートとして保存し、そのテンプレートを次のアダプティブフォーム用に再利用することで、フォームの作成プロセスを合理化します。
* **[AEM Formsを JDBC-Supported データベースに接続する](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:AEM Formsデータモデルを JDBC をサポートするデータベースに簡単に接続でき、データの読み取りと書き込みをシームレスに行うことができます。
* **[Open API 3.0 を使用した REST エンドポイントとの統合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:Open API 仕様バージョン 3.0 をサポートする REST エンドポイントにAEM Formsas a Cloud Serviceのフォームデータモデルを接続すると、簡単にデータを送受信できます。
* **[レビュー用にアダプティブフォームを共有する](/help/forms/create-reviews-forms.md)**:アダプティブFormsのレビューメカニズムを使用して、1 人または複数のレビュー担当者がフォームをレビューできるようにします。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* 作成者は、エクスペリエンスフラグメントを使用して、製品リストを動的にエンリッチメントできます（例：製品リスト間にバナーを配置）。
* リストコンポーネントは、関連する製品／カテゴリーページをサポートして、関連ページを動的に表示するようになりました。
* Peregrine 12.5 コンポーネントのサポートが追加されました。
* 製品ティーザーおよびカルーセルでのクライアントサイドの価格読み込みサポートが追加されました。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* [迅速な開発環境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE を使用すると、開発者は問題を迅速にトラブルシューティングし、AEM as a Cloud Serviceに新しい機能をデプロイできます。

   迅速な開発環境は、迅速で一貫性のある、拡張可能な方法として設計された新しいタイプのクラウド環境で、ローカルで動作するコードを検証する方法も、クラウド内での期待どおりに機能します。 コマンドラインツールを使用して、コンテンツパッケージ、バンドル、コンテンツファイル、OSGi 設定、Dispatcher 設定をすばやく「同期」します。 以下のビデオで、実際の動作でこれを確認してください。

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   RDE でコードを正常に検証した後、実稼動パイプラインを介してステージおよび実稼動環境にデプロイする前に、Cloud Dev Environment にデプロイして Cloud Manager の品質ゲートを使用することをお勧めします。

   各プログラムには 1 つの RDE が含まれ、オプションで、さらにライセンスを取得できます。

   >[!NOTE]
   >
   >RDE は、今後数週間で徐々に展開される予定です。メールをaemcs-rde-support@adobe.comに送信して、スキップして行の先頭に進むことができます。

* [サーバー側 API アクセストークンの拡張サポート](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)  — 複数の資格情報を生成できるようになりました。これは、API の特性が異なるシナリオで役立ちます。 また、セルフサービス方式で資格情報を失効させることもできるようになりました。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートがあります [ここ](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
