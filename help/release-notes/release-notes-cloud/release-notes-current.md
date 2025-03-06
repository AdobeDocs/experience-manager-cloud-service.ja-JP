---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: edfec41a9e33fbe818cb19f878ac42d435d62419
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 48%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.2.0）のリリース日は、2025年3月4日（PT）です。次回の機能リリース（2025.3.0）は 2025年3月27日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### AEM Sitesの新機能 {#new-features-sites}

** コンテンツフラグメントの自動タグ付け**

コンテンツフラグメントの作成時に、コンテンツモデルに割り当てられたタグを自動的に継承できるようになりました。 これにより、コンテンツフラグメントに保存されたコンテンツを強力に自動分類できます。

** コンテンツフラグメント UUID のサポート **

コンテンツフラグメント UUID のサポートが一般提供（GA）されるようになりました。 この新しい機能は、AEM内のパスに基づく操作（移動、名前を変更、ロールアウトなど）の動作は変わりませんが、コンテンツフラグメントの外部使用をより簡単かつ安定させることができます。特に、ByPath クエリで個々のフラグメントを直接ターゲットにするGraphQL クエリを使用する場合に便利です。 このようなクエリは、フラグメントパスが変更されると壊れる可能性があります。 新しい ById クエリタイプを使用する場合、パスが変更されてもフラグメントの UUID は変化しないので、クエリは安定したままになります。

コンテンツフラグメントエディターおよびGraphQL **で OpenAPI をサポートする** Dynamic Media

コンテンツフラグメントとは異なるAEM as a Cloud Service プログラムに保存され、OpenAPI 機能を備えた新しい Dynamic Media で有効になっているAssetsを、コンテンツフラグメントで使用できるようになりました。 新しいコンテンツフラグメントエディターの画像セレクターで、フラグメントで参照する画像アセットのソースとして「リモート」リポジトリーを選択できるようになりました。 さらに、AEM GraphQLを使用してこのようなコンテンツフラグメントを配信する際に、リモートアセット（assetId、repositoryId）の必須プロパティが JSON 応答に含まれるようになりました。これにより、クライアントアプリケーションは、画像を取得する OpenAPI の URL で各 Dynamic Media を作成できます。

** Translation HTTP API **

しばらくの間アーリーアダプターモードであったAEM翻訳 HTTP REST API が一般提供（GA）されるようになりました。 ドキュメントは [ こちら ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) で参照できます。 API を使用すると、AEM内のコンテンツの翻訳管理プロセスで必要な手順を自動化できます。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets の新機能 {#new-features-assets}

**Dynamic Media の新しいパッケージ構造**

Dynamic Media のパッケージ構造を刷新し、市場の期待に応え、追跡をサポートできるようになりました。 新しいパッケージ構造は、次の要素で構成されます。

* Dynamic Media Prime（OpenAPI およびビデオを備えた Dynamic Media を含み、配信を強化）。

* Dynamic Media Ultimateは、より厳しい使用要件に対応するために、配信および変換機能を追加します。

新しいパッケージ構造のメリットを得るには、Assets as a Cloud Service PrimeまたはUltimateが必要です。

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なキャプションを提供することでアクセシビリティを向上し、ユーザーエクスペリエンスを強化するように設計されています。 キャプションは、元のオーディオ、追加のオーディオトラック、または追加のキャプションから生成され、ビデオのプロパティページの「キャプションとオーディオ」タブで提供されます。 60 を超える言語がサポートされているので、ビデオを公開する前にキャプションを確認およびプレビューできます。

**検索フィルターのカスタマイズ**

カスタム検索フィルターを使用すると、関連情報の検索の精度と効率が向上します。 これにより、ブランド、製品、カテゴリ、その他のキー識別子などの特定の属性に従ってデータをフィルタリングし、よりカスタマイズされた検索を行うことができます。 これにより、組織が改善され、無関係な結果の選別に費やす時間が短縮され、意思決定をより迅速に行うことができます。 また、大きなデータセットの移動や分析が容易になるので、スケーラビリティもサポートします。

![ 検索フィルターのカスタマイズ ](/help/assets/assets/custom-search-filters.png)


### Content Hubの早期アクセス機能 {#early-access-content-hub}

Content Hubでは、既存の静的レンディションに加え、動的レンディションとスマート切り抜きレンディションを表示およびダウンロードできるようになりました。 Content Hub管理者は、設定ユーザーインターフェイスを使用してレンディションの可用性を設定することもできます。

![動的レンディション](/help/assets/assets/download-single-asset-renditions-dynamic.png)



## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### アダプティブFormsのHTML メールテンプレート

アダプティブFormsでは、[HTMLのメールテンプレート ](/help/forms/html-email-templates-in-adaptive-forms.md) を使用できます。 HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

#### クラウドストレージのサポートの強化：Azure Blob Storage への直接 PDF アップロード

AEM Forms Document Generation API で、Azure Blob ストレージに [ 生成されたPDF ドキュメントを直接アップロード ](/help/forms/early-access-ea-features.md#doc-generation-api) できるようになりました。 この機能強化により、ストレージと取得が合理化され、効率の向上やクラウドワークフローとの統合が促進されます。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Java 21 サポート {#java21}

1 月のリリースノートに記載されているように、Java 21 を使用してコードをビルドできるようになりました。この中には、新機能（スイッチステートメントのパターン照合、シールされたクラスなど）とパフォーマンスの向上が含まれています。Java 17 ビルドも新たにサポートされます。 Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)の記事を参照してください。

Java 17 または 21 ビルドが検出されると、より高パフォーマンスの Java 21 **ランタイム**&#x200B;が自動的にデプロイされます。ただし、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信して Java 21 ランタイムをオプトインすることをお勧めします。[Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> 2 月に、Java 21 **runtime** が開発/RDE 環境にデプロイされました（既に Java 17 または 21 でビルドされており、既に Java 21 ランタイムが含まれている環境は除く）。 Java 21 は、4 月にステージ/実稼動環境に適用されます。

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 Adobeは、このテクノロジーがAEMの公開配信プロジェクトとEdge Delivery Services プロジェクトに役立つかどうかを聞きたいと考えています。 さらに、製品ロードマップへの入力として使用すると想定される内容をお知らせください。

考えられるユースケースは次のとおりです。
* コンテンツへのアクセスをゲートする IdP を使用した認証
* 位置情報、デバイスタイプ、ユーザー属性などに基づく動的（パーソナライズされ、ローカライズされた）コンテンツのレンダリング
* 高度な画像操作
* CDN とオリジンの間のミドルウェア
* ブラウザーとサードパーティ API の間のレイヤー（API 応答の再フォーマット用など）
* 複数のオリジンからのデータを集計して、クライアントブラウザーでレンダリングしやすくする。

ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を独自のアプリケーションやツールに深く統合できます。 新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成されます。

詳しくは、[OpenAPI ベースの AEM API](/help/implementing/developing/open-api-based-apis.md) を参照し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)を試してください。

具体的には、以下に示す API エンドポイントが早期導入プログラムの一部として使用可能です。 興味がある場合は、どのように活用する予定かを記載したメールを [aem-apis@adobe.com](mailto:aem-apis@adobe.com) まで送信してください。

* [Sites Content Fragments API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites and Assets Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。 アドビでは、フィードバックを大切にしています。[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com) までメールで送信してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターのリリースの完全なリストは、[こちら](/help/release-notes/universal-editor/current.md)で確認できます。

## バリエーションの生成 {#generate-variations}

バリエーションの生成のリリースの完全なリストは、[こちら](/help/generative-ai/release-notes-generate-variations.md)で確認できます。

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
