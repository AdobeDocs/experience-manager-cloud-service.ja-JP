---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: d202b0543020b277de982e3965475074a71b286d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 33%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年のバージョンなど）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在の機能リリース (2023.2.0) は 2023 年 4 月 12 日です。 次回の機能リリース (2023.4.0) は、2023 年 5 月 25 日に予定されています。

## リリースビデオ {#release-video}

2023.2.0 リリースに追加された機能の概要については、 2023 年 2 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Experience Manager Sites] 予約 {#prerelease-sites}

* コンテンツフラグメントをAEM as a cloud service から JSON オファーとしてAdobeターゲットに書き出します。
* 複雑なGraphQLのクエリとフィルターを使用して大きなコンテンツセットをAEMから取得する際、GraphQLのページネーションと並べ替えおよび内部キャッシュの強化に加えて、切り離されたクライアントアプリケーションのパフォーマンスを改善しました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Dynamic Mediaビデオ配信でアダプティブストリーミング用に開始された新しいプロトコル (DASH - Dynamic Adaptive Streaming over HTTP) のサポート（CMAF を有効にした場合）:
   * アダプティブストリーミング (DASH/HLS) により、エンドユーザーがビデオを視聴する際の操作性が向上します
   * DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています
   * NA で利用可能で、サポートチケットを介して有効にできます。APAC、EMEA で近日公開

* メタデータの自動抽出、サムネールおよびカスタムレンディションの生成を行う WebP 画像のサポートが追加されました。 これらのファイルでスマートタグ機能もサポートされるようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[データキャプチャコアコンポーネントを使用したアダプティブフォームの構築](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)**: [アダプティブフォームエディターを使用](/help/forms/creating-adaptive-form-core-components.md)して、標準化されたデータキャプチャコンポーネント（コアコンポーネント）に基づいてフォームを作成します。これらのコンポーネントは、デジタル登録エクスペリエンスでのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。

* **[アダプティブFormsに基づくコアコンポーネントのスタイル設定のためのフロントエンドパイプラインのサポート](/help/forms/using-themes-in-core-components.md)**:コアコンポーネントベースのアダプティブFormsに標準化された BEM ベースのテーマを利用するには、フロントエンドデプロイメントパイプラインと共にデプロイして、フォームのルックアンドフィールを強化し、組織が承認したデザインガイドラインに合わせます。

* **[コアコンポーネントベースのアダプティブFormsに関するレコードのドキュメントを生成する](/help/forms/generate-document-of-record-core-components.md)**:エンドユーザーへのアーカイブや参照用のコアコンポーネントを使用して構築された、アダプティブForms用の送信済みデータを、印刷形式またはドキュメント形式で含むレコードのドキュメントを作成します。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[「アダプティブフォームをテンプレートとして保存」機能を使用した効率的なフォーム作成](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:既存の承認済みフォームをフォームテンプレートとして保存して、すばやく再利用できるようにすることで、フォームの開発を迅速に進め、標準化します。

* **[AEM Formsを JDBC-Supported データベースに接続する](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:JDBC プロトコルを使用してAEM Cloud Service から直接エンタープライズデータベースに接続できます。REST API で公開する必要はありません。

* **[Open API 3.0 を使用した REST エンドポイントとの統合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:Open API 3.0 をサポートするレコードシステムとシームレスに統合し、フォームデータモデルを使用してデータを保存および取得します。

* **[レビュー用にアダプティブフォームを共有](/help/forms/create-reviews-forms.md)**：アダプティブフォームのレビュー機能を使用する、1 人または複数のレビュー担当者がフォームをレビューできます。


### の機能 [!DNL Forms] プレリリース {#prerelease-features-forms}

* **[Microsoft SharePointとMicrosoft OneDrive にアダプティブFormsを送信する](/help/forms/configuring-submit-actions.md)**:ビジネスユーザーの俊敏性を向上させ、新しいフォームをすばやく起動し、送信されたデータをMicrosoft SharePointサイトや OneDrive フォルダーなどの毎日のツールに保存します。

![Microsoft SharePointとMicrosoft OneDrive にアダプティブFormsを送信する](/help/forms/assets/onedrive-and-sharepoint.jpg)


## ヘッドレスアダプティブFormsアーリーアダプタープログラム {#forms-early-adopter}

ヘッドレスアダプティブFormsを使用すると、開発者は、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できます。 ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用する
* Adobe Experience Manager Formsの力を活用する

アーリーアダプタープログラムに参加するため、公式メール ID からaem-forms-headless@adobe.comまでメールを送信できます。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、 [こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
