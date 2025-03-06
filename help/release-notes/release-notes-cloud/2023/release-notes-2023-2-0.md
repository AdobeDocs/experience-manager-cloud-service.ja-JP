---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.2.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2023.2.0 リリースのリリースノート。'
exl-id: 671056e6-84cc-4c2c-bca3-fde68d5cc835
feature: Release Information
role: Admin
source-git-commit: b4ffcddddfcd990c359380071f19b5442dee9eb2
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2023.2.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2023.2.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年のバージョンなど）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2023.2.0）のリリース日は、2023年4月12日（PT）です。次回の機能リリース（2023.4.0）は 2023年6月7日（PT）に予定されています。

## リリースビデオ {#release-video}

2023.2.0 リリースで追加された機能の概要については、2023年2月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] プレリリースの新機能 {#prerelease-sites}

* AEM as a Cloud Service からコンテンツフラグメントを JSON オファーとして Adobe Target に書き出します。
* 複雑な GraphQL のクエリとフィルターを使用して大きなコンテンツセットを AEM から取得する際、GraphQL のページネーションと並べ替えのサポートに加え、内部キャッシュの強化によって、切り離されたクライアントアプリケーションのパフォーマンスの向上を支援するようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Dynamic Media ビデオ配信でアダプティブストリーミング用に開始された新しいプロトコル（DASH - Dynamic Adaptive Streaming over HTTP）のサポート（CMAF を有効にした場合）:
   * アダプティブストリーミング（DASH／HLS）により、ユーザーがビデオを視聴する際の操作性が向上します
   * DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています

* メタデータの自動抽出、サムネールおよびカスタムレンディションの生成を行う WebP 画像のサポートが追加されました。これらのファイルで、スマートタグおよびスマート切り抜き機能もサポートされるようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] で利用できる新機能 {#new-features-available-in-channel}

* **[データキャプチャコアコンポーネントを使用したアダプティブフォームの構築](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)**: [アダプティブフォームエディターを使用](/help/forms/creating-adaptive-form-core-components.md)して、標準化されたデータキャプチャコンポーネント（コアコンポーネント）に基づいてフォームを作成します。これらのコンポーネントは、デジタル登録エクスペリエンスでのカスタマイズ機能を提供し、開発時間を短縮し、メンテナンスコストを削減します。

* **[アダプティブフォームに基づくコアコンポーネントのスタイル設定のためのフロントエンドパイプラインのサポート](/help/forms/using-themes-in-core-components.md)**：コアコンポーネントベースのアダプティブフォームに対して、容易にカスタマイズできる AEM ベースのテーマを利用し、フロントエンドデプロイメントパイプラインと共にデプロイして、フォームのルックアンドフィールを向上させ、組織のブランド承認済みのデザインガイドラインに沿うことができます。

* **[コアコンポーネントベースのアダプティブフォーム用のレコードのドキュメントを生成](/help/forms/generate-document-of-record-core-components.md)**：コアコンポーネントを使用して構築されたアダプティブフォームの送信データを含むレコードのドキュメントを、印刷物またはドキュメント形式で、エンドユーザーへのアーカイブまたは参照用に作成します。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[アダプティブフォームをテンプレートとして保存機能を使用した効率的なフォーム作成](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：既存の承認済みフォームをフォームテンプレートとして保存して、素早く再利用できるようにすることで、フォームの開発を迅速に進め、標準化します。

* **[AEM Forms を JDBC対応データベースに接続](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：JDBC プロトコルを使用して AEM Cloud Service から直接エンタープライズデータベースに接続できます。REST API で公開する必要はありません。

* **[Open API 3.0 を使用した REST エンドポイントとの統合](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：Open API 3.0 をサポートするレコードのシステムとシームレスに統合し、フォームデータモデルを使用してデータを保存および取得します。

* **[レビュー用にアダプティブフォームを共有](/help/forms/create-reviews-forms.md)**：アダプティブフォームのレビュー機能を使用する、1 人または複数のレビュー担当者がフォームをレビューできます。


### [!DNL Forms] の機能プレリリース {#prerelease-features-forms}

* **[Microsoft SharePoint と Microsoft OneDrive にアダプティブフォームを送信](/help/forms/configuring-submit-actions.md)**：ビジネスユーザーの俊敏性を向上させ、新しいフォームを素早く起動し、送信されたデータを Microsoft SharePoint サイトや OneDrive フォルダーなどの毎日使用するツールに保存します。

![Microsoft SharePoint と Microsoft OneDrive にアダプティブフォームを送信](/help/forms/assets/onedrive-and-sharepoint.jpg)


## ヘッドレスアダプティブフォーム早期導入者プログラム {#forms-early-adopter}

ヘッドレスアダプティブフォームを使用すると、開発者は、従来のグラフィカルユーザーインターフェイスではなく、API を介してアクセスおよび操作できるインタラクティブなフォームを作成、公開、管理できます。ヘッドレスアダプティブフォームは以下の場合に役立ちます。

* 高品質のマルチチャネルフォームを好みのプログラミング言語で作成
* デスクトップおよびモバイルアプリ、web サイト、チャットアプリケーションにフォームをネイティブに統合
* フォームアプリケーションで独自の UI コンポーネントを再利用
* Adobe Experience Manager Forms の機能を活用

ご自身の公式メール ID から aem-forms-headless@adobe.com にメールを送信して、早期導入者プログラムにご参加ください。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
