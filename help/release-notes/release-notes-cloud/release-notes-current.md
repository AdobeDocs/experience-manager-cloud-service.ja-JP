---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75a011ed952e1801f0988942d4501a52d348bb3f
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 47%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.1.0）のリリース日は、2025年1月30日（PT）です。次回の機能リリース（2025.2.0）は 2025年2月27日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**コンテンツフラグメントエディターのコメント機能が一般公開されました**

AEM コンテンツフラグメントエディターの新しい最新化されたコメントサービスを使用して、AEM コンテンツフラグメントをオーサリングする際に、同僚と簡単に共同作業ができます。
[詳細情報](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**コンテンツフラグメントエディターと管理ユーザーインターフェイスで、AEM as a Cloud Service バージョンのサポートが更新されました**

新しいコンテンツフラグメント管理およびエディターのユーザーインターフェイスでサポートされるAEM as a Cloud Serviceの最小バージョンは、2023.8.13099 になりました。一般提供リリース以前のバージョンの新しいユーザーインターフェイスは、サポートされなくなりました

### 早期導入プログラム {#sites-early-adopter}

**コンテンツフラグメントの強化機能**

強化 [ 一意の ID ベースの参照を使用したコンテンツフラグメント参照 ](/help/headless/graphql-api/uuid-reference-upgrade.md) により、アセットやフラグメントを移動した場合でも有効な安定したリンクが確保され、更新や再公開が不要になりました。 現在の制限事項：ページ参照は、一意の ID ではまだサポートされていません。 コンテンツフラグメントでページを参照する場合は、この機能を使用しないでください。

**コンテンツフラグメント配信用の AEM REST OpenAPI**

コンテンツフラグメント配信用の [AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) がAEM as a Cloud Serviceで使用できるようになりました。

### 非推奨（廃止予定）の機能 {#sites-deprecated}

#### SPA エディター {#spa-editor}

[SPA エディター ](/help/implementing/developing/hybrid/introduction.md) は、リリース 2025.1.0 以降の新しいプロジェクトでは廃止されました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEMでヘッドレスコンテンツを管理するために推奨されるエディターは、次のとおりです。

* ビジュアル編集用の [ ユニバーサルエディター ](/help/edge/wysiwyg-authoring/authoring.md)。
* フォームベースの編集用の [ コンテンツフラグメントエディター ](/help/assets/content-fragments/content-fragments-managing.md)。

#### PWAの機能 {#pwa-features}

AEM Sitesの [ プログレッシブ web アプリ（PWA）機能 ](/help/sites-cloud/authoring/sites-console/enable-pwa.md) は、リリース 2025.1.0 以降の新しいプロジェクトで非推奨（廃止予定）になりました。この機能は、既存のプロジェクトでは引き続きサポートされますが、新規プロジェクトでは使用しないでください

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assetsの新機能 {#new-features-assets}

**Dynamic Media テンプレート**

使いやすいWYSIWYG Dynamic Media テンプレートエディターを使用して画像バナーやテキストバナーをその場でパーソナライズし、ファーストパーティまたはサードパーティアプリケーションに URL を埋め込むことで、リアルタイムのバナーコンテンツ更新で非常に魅力的なエクスペリエンスを促進します。

![動的レンディション](/help/assets/assets/dm-templates-smart-text-resize.png)

**Dynamic Media配信レポート**

Dynamic Mediaを通じて配信されるアセットの配信インサイトを取得します。これには、アセットレベルの配信数、リファラーの詳細、AEM Assetsのアセットパス、一意のアセット ID などが含まれます。 AEM Assets リポジトリまたは特定のフォルダー階層内のすべてのアセットに関するレポートを生成します。 これらのインサイトを使用すると、配信されたアセットの ROI を測定し、チャネルのパフォーマンスを評価し、十分な情報に基づいてアセット管理の決定を行うことができます。

![動的レンディション](/help/assets/assets/referrer.png)

**Dynamic Mediaのマルチオーディオとキャプション**

[Dynamic Mediaでのビデオのマルチキャプションおよびマルチオーディオトラックのサポート ](/help/assets/dynamic-media/video.md#about-msma) – プライマリビデオに複数のキャプションと複数のオーディオトラックを簡単に追加できるようになりました。 この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからキャプションとオーディオトラックを管理することもできます。

**HTTP を使用した動的アダプティブストリーミングのサポート**

CMAF が有効な Dynamic Media ビデオ配信で、アダプティブストリーミングをサポートする新しいプロトコル（DASH - HTTP での動的アダプティブストリーミング）が開始しました。

* アダプティブストリーミング（DASH/HLS）により、ビデオの視聴エクスペリエンスが向上します。

* DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています

**アセット関係**

Assets ビューで、シンプルなアセットの詳細パネルでアセットの関係を表示および編集できるようになりました。 Sourceや派生などの関係をコンテンツに容易に追加して、ユーザーが関連するヒーローコンテンツをより効果的に見つけられるようにします。

**アセットの再処理**

Assets ビューで、フォルダー内の使用可能なアセットの再処理がサポートされるようになりました。 「**フルプロセス**」オプションを使用するか、デフォルトのプレビューレンディション、メタデータ、後処理ワークフロー、処理プロファイルなどの詳細オプションを使用するかを選択できます。

### AEM Assetsの早期アクセス機能 {#early-access-features-assets}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 キャプションは、元のオーディオ、追加のオーディオトラック、またはビデオのプロパティページの「キャプションとオーディオ」タブで提供される追加のキャプションから生成されます。 60 を超える言語がサポートされているので、ビデオを公開する前にキャプションをレビューおよびプレビューできます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-features}

* **公開を管理**:「公開を管理」ワークフローを使用して、通常はオーサーインスタンスからパブリッシュインスタンスとプレビューインスタンスに対して、複数の環境をまたいでフォームを公開または非公開にすることができます。 これにより、ユーザーは効率的な方法でコンテンツの公開、非公開、または公開のスケジュールを設定できます。

* **[コアコンポーネントベースアダプティブフォームのドラフトの自動保存](/help/forms/save-core-component-based-form-as-draft.md)**：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。 後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。 この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

* **[ルールエディターの機能強化](/help/forms/invoke-service-enhancements-rule-editor.md)**：コアコンポーネントに基づくアダプティブFormsの場合、サービスの呼び出しの出力を使用してドロップダウンオプションを入力し、繰り返し可能なパネルまたは個々のパネルを設定できます。 さらに、この出力は、他のフィールドの検証に使用できます。

* **[パネルレイアウトのナビゲーションボタンを使用したユーザーエクスペリエンスの向上](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：水平タブ、垂直タブ、アコーディオン、ウィザードなどのナビゲーションボタンをパネルレイアウトに追加できるようになりました。 これらのボタンを使用すると、選択したパネルに焦点を当てて、パネル間の切り替えを簡素化し、ユーザーエクスペリエンスを向上させることができます。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### [ アダプティブFormsのHTMLメールテンプレート ](/help/forms/html-email-templates-in-adaptive-forms.md)

アダプティブFormsでは、HTMLのメールテンプレートを使用できます。 HTML用のメールテンプレートを使用すると、フォームが送信される際に、リッチでパーソナライズされた、視覚的にアピールするメールを送信できます。 これらのメールは、フォームデータを使用してカスタマイズし、画像やリンクなどの様々なメールタグを使用して強化できます。 アダプティブFormsでは、HTMLテンプレートを含んだファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTMLのメールテンプレート ](/help/forms/assets/html-email.png)

#### クラウドストレージのサポートの強化：Azure Blob Storage への直接PDFアップロード

AEM Forms Document Generation API では、生成されたPDFドキュメントの Azure Blob Storage への直接アップロードをサポートするようになりました。 この機能強化により、ストレージと取得が合理化され、効率が向上し、クラウドワークフローとの統合が促進されます。

* **[ファイル添付の Base64 エンコード文字列のサポート](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：コアコンポーネントに基づくアダプティブフォームのファイル添付コンポーネントに、添付ファイルを Base64 エンコード文字列として送信するオプションが含まれるようになりました。

>[!IMPORTANT]
>
> Forms のイノベーションの早期アクセスプログラムへの参加に興味がありますか？ 興味のある機能のリストを添えて、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。## CIF アドオン {#cloud-services-cif}

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Java 21 サポート {#java21}

Java 21 を使用してコードをビルドできるようになりました。この機能には、新機能（switch ステートメントのパターン照合、sealed クラスなど）とパフォーマンスの向上が含まれ、Java 17 ビルドも新しくサポートされます。 Maven プロジェクトとライブラリのバージョンの更新など、設定手順については、[ ビルド環境 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) の記事を参照してください。

Java 17 または 21 ビルドが検出されると、よりパフォーマンスの高い Java 21 **runtime** が自動的にデプロイされます。 ただし、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) に電子メールを送信して Java 21 ランタイムをオプトインすることをお勧めします。 [Java 21 ランタイム要件 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) について説明します。

>[!IMPORTANT]
>
> Java 21 **runtime** は、2 月にサンドボックスと dev/RDE を開始し、4 月にステージング/実稼動を開始して、**すべて** の環境に徐々にデプロイされます（Java 17 または 21 で既にビルドされ、Java 21 ランタイムが存在する環境は除く）。

### サンドボックスプログラムは、設定パイプラインをサポートします {#sandbox-config-pipelines}

サンドボックスプログラムで設定パイプラインがサポートされるようになりました。このパイプラインは、Git に保存されている yaml ファイルをデプロイするようにCloud Managerで設定できます。

CDN、ログ転送、バージョンパージ/監査ログのパージメンテナンスタスクを設定できる設定パイプラインについて [ 詳細情報 ](/help/operations/config-pipeline.md) します。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を独自のアプリケーションやツールに深く統合できます。 新しいAEM as a Cloud Service API は、一貫性があり、適切にドキュメント化され、使いやすいことを目標として、OpenAPI 仕様に従っています。 認証が必要なエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成して生成されます。

詳しくは、[OpenAPI ベースの AEM API](/help/implementing/developing/open-api-based-apis.md) を参照し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)を試してください。

具体的には、以下に示す API エンドポイントが早期導入プログラムの一部として使用可能です。 興味がある場合は、どのように活用する予定かを記載したメールを [aem-apis@adobe.com](mailto:aem-apis@adobe.com) まで送信してください。

* [Sites Content Fragments API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites and Assets Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 Adobeは、このテクノロジーがAEM Publishの配信プロジェクトやEdge Delivery Servicesプロジェクトに役立つとお聞きしています。 さらに、製品ロードマップへの入力として使用すると想定される内容をお知らせください。 ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

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
