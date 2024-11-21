---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 5d2c09a3e1c67e6c2435d84112546107d284259f
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 41%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2022年、2023年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.11.0）のリリース日は、2024年11月21日（PT）です。次回の機能リリース（2024.12.0）は 2024年12月12日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

ユニバーサルエディターのオーサリングを使用したページテンプレートの **[!DNL Edge Delivery Services]成**

任意のEdge Delivery ページをすばやくページテンプレートに変換します。 これにより、空白のページの代わりに、事前に定義された構造とコンテンツで新しいページを開始できます。 [詳細情報](/help/sites-cloud/authoring/universal-editor/templates.md)。

AEM インスタンス **[!DNL Edge Delivery Services]介して公開するための CSV インポーター**

お気に入りのスプレッドシートツールでEdge Delivery スプレッドシートデータ（リダイレクトなど）を効率的に管理し、新しい CSV インポーターを使用してAEMにアップロードします。 [詳細情報](/help/edge/wysiwyg-authoring/tabular-data.md#importing)。

### AEM Sitesのプレリリース機能

一意の ID ベースの参照を使用したコンテンツフラグメント参照が強化され、アセットやフラグメントが移動された場合でも安定したリンクが維持されるようになり、更新や再公開が不要になりました。 現在の制限事項：一意の ID では、ページ参照はまだサポートされていません。 コンテンツフラグメントでページが参照されている場合は、この機能を使用しないでください。

### 早期導入プログラム {#sites-early-adopter}

**コンテンツフラグメント配信用の AEM REST OpenAPI**

[コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) が AEM as a Cloud Service で使用できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Mediaの早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

**Dynamic Media配信レポート**

アセットレベルの配信数、リファラー情報、AEM Assetsのアセットパス、一意のアセット ID など、Dynamic Mediaで配信されるアセットの配信に関するインサイトを取得します。 レポートは、AEM Assets リポジトリーのDynamic Mediaを介して配信されるすべてのアセットに対して、またはAEM Assetsの特定のフォルダー階層に対して生成できます。 インサイトは、配信されたアセットの ROI の測定、チャネルパフォーマンスの測定、情報に基づいたアセット管理タスクの実行に役立ちます。

Dynamic Media アカウントのDynamic Media配信レポートに早期にアクセスするには、[Adobeのカスタマーサポートケースを作成して送信 ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) します。

### アセットビューの新機能 {#assets-view-new-features}

**Dynamic Mediaパネル**

Assets ビューで、使用可能になった別のパネルから、OpenAPI レンディションを使用してDynamic MediaおよびDynamic Mediaにアクセスできるようになりました。 配信 URL をコピーするか、アセットとレンディションタイプに基づいてレンディションをダウンロードするかを選択できます。 詳しくは、[Dynamic Media レンディション ](/help/assets/renditions.md#dynamic-media-renditions) および [OpenAPI 機能レンディションのDynamic Media](/help/assets/renditions.md#dm-with-openapi-renditions) を参照してください。

![ 動的レンディション ](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-features}

* **[Adobe Sign スコープを簡単に更新](/help/forms/adobe-sign-integration-adaptive-forms.md)**：AEM クラウド設定ページから Adobe Sign 設定のスコープを直接変更できるので、既存の設定をよりすばやく簡単に更新できます。

* **[アダプティブフォームの非同期関数のサポート](/help/forms/using-async-funct-in-rule-editor.md)**：アダプティブフォームで外部プロセスの待機やデータの取得などの非同期操作が必要な際は、カスタム関数を使用してこれらの操作を実装し、ルールエディターで設定できます。

### AEM Formsのプレリリース機能 {#forms-new-prerelease-features}

* **公開を管理**：公開を管理ワークフローを使用して、通常はオーサーインスタンスからパブリッシュおよびプレビューインスタンスに、複数の環境にわたってフォームを公開または非公開にできます。 これにより、ユーザーは、合理化された方法でコンテンツの公開、非公開または公開スケジュールを設定できます。

* **[コアコンポーネントベースアダプティブフォームのドラフトの自動保存](/help/forms/save-core-component-based-form-as-draft.md)**：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

* **[ルールエディターの機能強化](/help/forms/invoke-service-enhancements-rule-editor.md)**：コアコンポーネントに基づくアダプティブFormsの場合、呼び出しサービスの出力を使用したドロップダウンオプションの入力、呼び出しサービスの出力を使用した繰り返し可能なパネルの設定、呼び出しサービスの出力を使用した個々のパネルの設定および呼び出しサービスの出力パラメーターの使用をして、他のフィールドを検証できるようになりました。

* **[パネルレイアウトのナビゲーションボタンを使用したユーザーエクスペリエンスの向上](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：水平タブ、垂直タブ、アコーディオン、ウィザードなどのナビゲーションボタンをパネルレイアウトに追加できるようになりました。これらのボタンを使用すると、選択したパネルに焦点を当てて、パネル間の切り替えを簡素化し、ユーザーエクスペリエンスを向上させることができます。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### 統合

* **[アダプティブFormsとAdobe Marketo Engageの統合](/help/forms/integrate-form-to-marketo-engage.md)**:AEM Formsas a Cloud Serviceには、アダプティブFormsとAdobe Marketo Engageを接続するための使いやすいオプションが含まれるようになりました。 この統合により、Marketo Engageのリードキャプチャおよび関連するカスタムオブジェクトを使用してアダプティブFormsを直接作成できます。 フォームフィールドにMarketo Engageからのデータを事前入力し、データを送信してスマートキャンペーンやメールの自動処理などのワークフローを自動化できるようになりました。 また、アダプティブフォームをMunchkin ライブラリに接続して、訪問数、クリック数、フォーム送信数をトラッキングすることもできます。

#### アダプティブFormsとHTML 5 Forms

* **[既存の XFA テンプレートに基づくアダプティブFormsの作成](/help/forms/create-adaptive-form-using-xfa-templates.md)**:XFA フォームテンプレート（*.XDP ファイル）を使用して、コアコンポーネントベースのアダプティブFormsを作成できるようになりました。 この機能により、XFA テクノロジーに既に投資しているAEM Forms オンプレミスのお客様は、AEM Formsas a Cloud Serviceを導入しやすくなります。

* **HTML 5 Forms（XFA ベースの Web フォーム）**：現在は、XFA テクノロジを使用しているAEM Forms オンプレミスのお客様は、HTML 5 Forms（XFA ベースの Web フォーム）での既存のユーザーエクスペリエンスを維持しながら、AEM Formsのas a Cloud Serviceな機能を簡単に利用できます。 この機能を使用すると、XFA フォームテンプレートをHTML5 形式でレンダリングし、XFA ベースのPDF formsをサポートしていないデバイスでフォームにアクセスできるようになります。

  ![HTMLForms（XFA ベースの web フォーム） ](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[添付ファイルの Base64 エンコードされた文字列のサポート ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：コアコンポーネントに基づくアダプティブ Formsの添付ファイルコンポーネントに、添付ファイルを Base64 でエンコードされた文字列として送信するオプションが含まれるようになりました。

#### インタラクティブ通信および通信 API

* **インタラクティブ通信エディター**：インタラクティブ通信エディターは、使いやすいグラフィカルな通信デザインツールで、パーソナライズされたデータ駆動型通信の作成を簡単にし、最新の任意のブラウザーで実行できます。 シームレスなデータ統合、複雑なロジック定義、リッチメディア統合をサポートし、様々なビジネスニーズに対応するプロフェッショナルで準拠したドキュメント、コミュニケーション、テンプレートの生成を保証します。

  ![ インタラクティブ通信エディター ](/help/forms/assets/ic-editor.png)


* **[PDF/A コンプライアンスの強化](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：通信 API を使用して、PDFドキュメントをPDF/A 形式（1a、2a、3a）に変換し、アーカイブしながら、アクセシビリティを確保し、これらの標準への準拠を検証できるようになりました。


* **[Signature API （Document Assurance）](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**:PDFAPI の新しい RESTful API を使用すると、通信の署名を簡単に管理できます。 次のような操作をサポートしています。
   * 署名をクリア：指定したフィールドから署名を削除します。
   * 署名フィールドを削除：指定した署名フィールドを削除します。


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自動フォーム変換サービス

* **[PDF formsをコアコンポーネントベースのアダプティブFormsに変換 ](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**:Automated forms conversionサービスを使用して、PDF forms、AcroForms または XFA ベースのフォームをコアコンポーネントベースのアダプティブFormsに変換できるようになりました。


>[!IMPORTANT]
>
> Forms のイノベーションの早期アクセスプログラムへの参加に興味がありますか？興味のある機能のリストを添えて、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。## CIF アドオン {#cloud-services-cif}

## CIF アドオン {#cif}

### バグ修正 {#bug-fixes-cif}

* コア CIF コンポーネントで正しく動作するように UI テストを修正しました。
* カテゴリ URL 形式がクラウドインスタンスで期待どおりに機能しない問題を解決しました。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### ツリーレプリケーションのパフォーマンスの向上（Publish コンテンツツリーワークフローは廃止されます） {#tree-replication-performance}

[ ツリーのアクティベーションワークフローステップ ](/help/operations/replication.md#tree-activation) は、深いコンテンツ階層のレプリケーションに推奨される新しいワークフローモデル手順です。 なお、処理中のツリーレプリケーションワークフローと並行して、独立したレプリケーション（クイック公開や公開管理などを通じて）を続行できます。 これは、一括レプリケーションの処理中に時間の影響を受けるコンテンツを公開する必要がある場合に特に便利です。 ツリーレプリケーション手順は、現在非推奨（廃止予定）となっているPublish コンテンツツリーワークフローとその関連するワークフロー手順に代わるものです。

### OpenAPI ベースの API – 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEMをCloud Service機能として独自のアプリケーションやツールに深く組み込むことができます。 新しいAEM as a Cloud Service API は、一貫性があり、十分にドキュメント化され、使いやすいことを目標として、OpenAPI 仕様に従います。 認証が必要なエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することで生成されます。

[OpenAPI ベースのAEM API](/help/implementing/developing/open-api-based-apis.md) について詳しくは、設定と使用方法を説明した [ エンドツーエンドのチュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) を試してください。

具体的には、以下に示す API エンドポイントは、早期導入プログラムの一部として利用できます。 興味があれば、それらの使用方法を説明して [aem-apis@adobe.com](mailto:aem-apis@adobe.com) に電子メールを送信してください。
* [Sites コンテンツフラグメント API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites とAssets Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms通信 API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge コンピューティング – フィードバックのリクエスト {#edge-computing-feedback}

Edgeコンピューティングは、データ処理をブラウザーに近づけます。これにより、待ち時間の短縮などのメリットがあります。 ロードマップのインプットとして、このテクノロジーがAEM Publishの配信およびEdge Delivery Servicesプロジェクトに役立つかどうか、そしてそれを使用して何を実現しようとしているのかをお聞かせください。 ご質問やご意見を含む電子メール [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) をお送りください。

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。Adobeでは、[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com) 宛てにメールで送信できるフィードバックを歓迎しています。

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
