---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.2.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: b893663d-35f1-43ae-a029-4c249b117f2d
source-git-commit: 3e0afac8f2f81f9ceae1cbfa456f1e747f2bdb06
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.2.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.2.0 バージョンの機能リリースノートの概要について説明します。

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

## リリースビデオ {#release-video}

2025.2.0 リリースで追加された機能の概要については、2025年2月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3458080?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### AEM Sites の新機能 {#new-features-sites}

**コンテンツフラグメントの自動タグ付け**

コンテンツフラグメントを作成する際に、コンテンツモデルに割り当てられたタグを自動的に継承できるようになりました。これにより、コンテンツフラグメントに保存されたコンテンツを強力に自動分類できます。

**コンテンツフラグメントの UUID サポート**

コンテンツフラグメントの UUID サポートが一般提供（GA）されるようになりました。この新しい機能は、移動、名前変更、ロールアウトなど、パスが自動的に調整される AEM 内の操作のパスベースの動作を変更するものではありませんが、特に ByPath クエリで個々のフラグメントを直接ターゲットにする GraphQL クエリを使用する場合に、コンテンツフラグメントの外部での使用をより簡単で安定させることができます。フラグメントパスを変更すると、このようなクエリが破損する場合があります。新しい ById クエリタイプを使用する際、パスを変更してもフラグメントの UUID は変更されないので、クエリは安定したままになります。

**コンテンツフラグメントエディターと GraphQL での OpenAPI を備えた Dynamic Media のサポート**

コンテンツフラグメントとは異なる AEM as a Cloud Service プログラムに保存され、新しい OpenAPI 機能を備えた Dynamic Media が有効になっているアセットを、コンテンツフラグメントで使用できるようになりました。新しいコンテンツフラグメントエディターの画像セレクターでは、フラグメントで参照される画像アセットのソースとして「リモート」リポジトリを選択できるようになりました。さらに、AEM GraphQL を使用してこのようなコンテンツフラグメントを配信すると、JSON 応答にリモートアセットの必須プロパティ（assetId、repositoryId）が含まれるようになったので、クライアントアプリケーションでは OpenAPI を備えた Dynamic Media の各 URL を作成し、画像を取得できるようになりました。

**コンテンツフラグメントエディターのロールアウト**

AEM as a Cloud Service では、新しい Spectrum UI ベースのコンテンツフラグメントエディターが引き続き有効になります。2024年11月にすべての Cloud Service 開発環境のデフォルトになった後、2025年4月1日（PT）にはすべてのステージング環境のデフォルト、2025年5月1日（PT）にはすべての実稼動環境のデフォルトとして設定される予定です。すべてのケースで、ユーザーは AEM タッチ UI で従来のコンテンツフラグメントエディターに戻すオプションを引き続き利用できます。

**Translation HTTP API**

しばらくの間、早期導入モードであった AEM Translation HTTP REST API が一般提供（GA）されるようになりました。ドキュメントについて詳しくは、[こちら](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/)を参照してください。API を使用すると、AEM 内のコンテンツの翻訳管理プロセスで必要な手順を自動化できます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets の新機能 {#new-features-assets}

**Dynamic Media の新しいパッケージ構造**

市場の期待に応え、トラッキングをサポートするために、更新された Dynamic Media のパッケージ構造が使用可能になりました。新しいパッケージ構造は、以下で構成されています。

* Dynamic Media Prime：配信を強化する OpenAPI を備えた Dynamic Media とビデオが含まれます。

* Dynamic Media Ultimate：より厳しい使用要件を満たすために配信機能と変換機能を追加します。

新しいパッケージ構造のメリットを得るには、Assets as a Cloud Service Prime または Ultimate が必要です。

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。キャプションは、元のオーディオ、追加のオーディオトラック、またはビデオプロパティページの「キャプションとオーディオ」タブで提供される追加のキャプションから生成されます。60 を超える言語がサポートされているので、ビデオを公開する前にキャプションを確認およびプレビューできます。

**検索フィルターのカスタマイズ**

カスタム検索フィルターを使用すると、関連情報の検索の精度と効率が向上します。ブランド、製品、カテゴリ、その他の主要な識別子などの特定の属性に従ってデータをフィルタリングし、よりカスタマイズされた検索が可能になります。これにより、組織が改善され、無関係な結果の選別に費やす時間が短縮され、より迅速な意思決定を行うことができます。また、大規模なデータセットの移動や分析が簡単になるので、スケーラビリティもサポートされます。

![検索フィルターのカスタマイズ](/help/assets/assets/custom-search-filters.png)

### コンテンツハブの早期アクセス機能 {#early-access-content-hub}

コンテンツハブでは、既存の静的レンディションに加えて、動的レンディションとスマート切り抜きレンディションを表示およびダウンロードできるようになりました。コンテンツハブ管理者は、設定ユーザーインターフェイスを使用して、これらのレンディションをユーザーが使用できるように設定することもできます。

![動的レンディション](/help/assets/assets/download-single-asset-renditions-dynamic.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### アダプティブフォームの HTML メールテンプレート

アダプティブフォームでは、[HTML メールテンプレート](/help/forms/html-email-templates-in-adaptive-forms.md)を使用できます。HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

#### クラウドストレージのサポートの強化：Azure Blob Storage への直接 PDF アップロード

AEM Forms ドキュメント生成 API で、[生成された PDF ドキュメントを Azure Blob Storage に直接アップロード](/help/forms/early-access-ea-features.md#doc-generation-api)できるようになりました。この機能強化により、ストレージと取得が合理化され、効率の向上やクラウドワークフローとの統合が促進されます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Java 21 サポート {#java21}

1 月のリリースノートで説明したように、Java 21 を使用してコードをビルドできるようになりました。これには、新機能（switch ステートメントのパターンマッチング、sealed クラスなど）とパフォーマンスの向上が含まれ、Java 17 ビルドも新たにサポートされます。Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)の記事を参照してください。

Java 17 または 21 ビルドが検出されると、より高パフォーマンスの Java 21 **ランタイム**&#x200B;が自動的にデプロイされます。ただし、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信して Java 21 ランタイムをオプトインすることをお勧めします。[Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> 2 月に、Java 21 **ランタイム**&#x200B;が dev/RDE 環境にデプロイされました（Java 17 または 21 で既にビルドされ、Java 21 ランタイムが存在する環境は除く）。Java 21 は、4 月にステージング／実稼動環境に適用されます。

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかについて、ぜひお聞かせください。さらに、製品ロードマップへのインプットとして、お客様が何を想定されるかをお教えください。

いくつかの考えられるユースケース：
* コンテンツへのアクセスをゲートする IdP を使用した認証
* 位置情報、デバイスタイプ、ユーザー属性などに基づく動的（パーソナライズされ、ローカライズされた）コンテンツのレンダリング。
* 高度な画像操作
* CDN とオリジンの間のミドルウェア
* ブラウザーとサードパーティ API の間のレイヤー（API 応答の再フォーマット用など）
* クライアントブラウザーでレンダリングしやすくする、複数のオリジンからのデータの集計

ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を、自分たちのアプリケーションやツールに深く統合できます。新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成されます。

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
