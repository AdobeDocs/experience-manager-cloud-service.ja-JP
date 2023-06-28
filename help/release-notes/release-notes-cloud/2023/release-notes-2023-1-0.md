---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.1.0 リリースのリリースノート。'
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 97%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.1.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.1.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年のバージョンなど）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の 2023.1.0 機能リリースのリリース日は、2023年2月9日（PT）です。次回の機能リリース（2023.2.0）は 2023年4月12日（PT）に予定されています。

## リリースビデオ {#release-video}

2023.1.0 リリースで追加された機能の概要については、2023年1月 のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースの新機能 {#prerelease-features-sites}

* AEM GraphQL コンテンツ配信 API で GraphQL [ページング](/help/headless/graphql-api/content-fragments.md#paging) および [並べ替え](/help/headless/graphql-api/content-fragments.md#sorting)がサポートされるようになり、大きなコンテンツセットの取得とレンダリングの効率が向上します。GraphQL のページネーションを使用すると、すべてを一度に返すのではなく、サブセットで結果を返すことで、クエリの応答時間を短縮できます。GraphQL での並べ替えでは、コンテンツセットを最適な順序で配置できるので、クライアントアプリケーションでのコンテンツの処理が容易になります。AEM GraphQL エンジンのハイブリッドフィルタリングにより、クエリの応答時間がさらに短縮されました。コンテンツは、クエリフィルターに対応する小さなセットで JCR から読み取られるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* 管理者はアセットレポートで Experience Manager Assetsas a Cloud Service デプロイメントから[アセットダウンロードレポートを生成](/help/assets/asset-reports.md)できるようになりました。このデータにより、管理者はさらに、主要な成功指標から洞察を得て、企業やお客様での Assets の採用状況を測定できます。

  ![他の形式向けの PDF レンディション](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets now は、Azure Blob ストレージデータ ソースに接続し、一括インポート ツールを使用してアセットを取り込む際に、認証用のアクセス キーに加えて [SAS Token](/help/assets/add-assets.md#asset-bulk-ingestor) をサポートするようになりました。

* Asset Compute での CMYK 画像の管理が改善され、CMYK 画像用のスマート切り抜きとスマートタグを生成できるようになりました。

### [!DNL Assets] プレリリースの新機能 {#prerelease-features-assets}

* Experience Manager Assets は、[Google Cloud Platform からの一括読み込みツールを使用した大規模なアセットの取り込み](/help/assets/add-assets.md#asset-bulk-ingestor) をサポートするようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[非インタラクティブ PDF ワークフロードキュメントと印刷可能な出力を生成するためのワークフローステップ](/help/forms/aem-forms-workflow-step-reference.md)**：AEM ワークフローステップを使用して、ビジネスプロセス向けの非インタラクティブ PDF ドキュメントと印刷可能な出力の作成を自動化することで、ドキュメント生成プロセスを合理化して時間を節約します。
* **[脚注を使用してアダプティブフォームで引用文や追加情報を提供](/help/forms/footnotes-richtextsupport.md)**：フォーム内の脚注を使用して、フォームの入力方法や使用方法に関する情報を表示します。また、括弧で囲まれた情報や著作権に関する権限、その他の役に立つ情報を提供する場合にも使用できます。

### [!DNL Forms] プレリリースの新機能 {#prerelease-features-forms}

* **[データキャプチャコアコンポーネントを使用したアダプティブフォームの構築](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)**: [アダプティブフォームエディターを使用](/help/forms/creating-adaptive-form-core-components.md)して、標準化されたデータキャプチャコンポーネント（コアコンポーネント）に基づいてフォームを作成します。これらのコンポーネントは、デジタル登録エクスペリエンスでのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。
* **[アダプティブフォームに基づくコアコンポーネントのスタイル設定のためのフロントエンドパイプラインのサポート](/help/forms/using-themes-in-core-components.md)**：コアコンポーネントベースのアダプティブフォームに対して、容易にカスタマイズできる BEM ベースのテーマを利用し、フロントエンドデプロイメントパイプラインと共にデプロイして、フォームのルックアンドフィールを向上させます。
* **[コアコンポーネントベースのアダプティブフォームに関するレコードのドキュメントを生成](/help/forms/generate-document-of-record-core-components.md)**：長期保存用、印刷またはドキュメント形式での送信時に、コアコンポーネントベースのアダプティブフォームのレコードを作成します。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Microsoft SharePoint と Microsoft OneDrive にアダプティブフォームを送信](/help/forms/configuring-submit-actions.md)**：Microsoft SharePoint と Microsoft OneDrive の両方にアダプティブフォームのデータを直接送信できるので、データ送信が効率化されます。スキーマベースのデータとスキーマレスのデータの両方を送信できます。これらの送信アクションは、既に使用可能な送信アクションに加えて実行されます。
* **[「アダプティブフォームをテンプレートとして保存」機能を使用した効率的なフォーム作成](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：アダプティブフォームをテンプレートとして保存し、そのテンプレートを次のフォームで再利用することで、フォームの作成プロセスを合理化します。
* **[AEM Formsを JDBC対応データベースに接続](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：JDBC をサポートするデータベースに AEM Forms データモデルを簡単に接続して、データの読み取りと書き込みをシームレスに行うことができます。
* **[Open API 3.0 を使用した REST エンドポイントとの統合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：Open API 仕様バージョン 3.0 をサポートする REST エンドポイントに AEM Formsas a Cloud Service のフォームデータモデルを接続することで、簡単にデータを送受信できます。
* **[レビュー用にアダプティブフォームを共有](/help/forms/create-reviews-forms.md)**：アダプティブフォームのレビュー機能を使用する、1 人または複数のレビュー担当者がフォームをレビューできます。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* [迅速な開発環境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE を使用すると、デベロッパーは問題を迅速にトラブルシューティングして、AEM as a Cloud Service に新しい機能をデプロイできます。

  迅速な開発環境とは、迅速で一貫性のある拡張可能な方法として設計された新しいタイプのクラウド環境であり、ローカルで動作するコードの検証もクラウドで期待通りに機能します。コマンドラインツールを使用して、コンテンツパッケージ、バンドル、コンテンツファイル、OSGi 設定、Dispatcher 設定をすばやく「同期」します。以下のビデオで、実際の動作を確認してください。

  >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

  RDE でコードを正常に検証した後、実稼動パイプラインを介してステージおよび実稼動環境にデプロイする前に、クラウド開発環境にデプロイして Cloud Manager の品質ゲートを実行することをお勧めします。

  各プログラムには 1 つの RDE が含まれ、オプションでさらにライセンスを取得できます。

  >[!NOTE]
  >
  >RDE は今後数週間で徐々に展開される予定です。メールを aemcs-rde-support@adobe.com に送信すると、行の先頭にスキップすることができます。

* [サーバーサイド API アクセストークンの拡張サポート](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - 複数の資格情報を生成できるようになりました。これは、API の特性が異なるシナリオで役立ちます。また、セルフサービス方式で資格情報を失効させることもできるようになりました。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
