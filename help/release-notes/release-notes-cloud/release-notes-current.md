---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d424b6f2e0a2ec40ab607dcbdcba3120c7f45a58
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 100%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.11.0）のリリース日は、2024年11月21日（PT）です。 次回の機能リリース（2025.1.0）は 2024年1月30日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

ユニバーサルエディターオーサリングを使用した **[!DNL Edge Delivery Services]ページテンプレート**

任意の Edge Delivery ページをすばやくページテンプレートに変換します。 これにより、空白ページの代わりに、事前に定義された構造とコンテンツを持つ新しいページを開始できます。 [詳細情報](/help/sites-cloud/authoring/universal-editor/templates.md)。

AEM インスタンス経由で公開するための **[!DNL Edge Delivery Services]CSV インポーター**

お気に入りのスプレッドシートツールで Edge Delivery スプレッドシートデータ（リダイレクトなど）を効率的に管理し、新しい CSV インポーターを使用して AEM にアップロードします。 [詳細情報](/help/edge/wysiwyg-authoring/tabular-data.md#importing)。

### AEM Sites のプレリリース機能

強化された[一意の ID ベースの参照によるコンテンツフラグメント参照](/help/headless/graphql-api/uuid-reference-upgrade.md)により、アセットまたはフラグメントを移動した場合でも有効な安定したリンクが確保され、更新や再公開の必要がなくなります。 現在の制限事項：ページ参照は、一意の ID ではまだサポートされていません。 コンテンツフラグメントでページを参照する場合は、この機能を使用しないでください。

### 早期導入プログラム {#sites-early-adopter}

**コンテンツフラグメント配信用の AEM REST OpenAPI**

[コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) が AEM as a Cloud Service で使用できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。 これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

**Dynamic Media 配信レポート**

アセットレベルの配信数、リファラー情報、AEM Assets 内のアセットパス、一意のアセット ID など、Dynamic Media で配信されたアセットの配信インサイトを取得します。 AEM Assets リポジトリの Dynamic Media 経由で配信されるすべてのアセットに対するレポートや、AEM Assets の特定のフォルダー階層に対するレポートを生成できます。 インサイトは、配信されたアセットの ROI の測定、チャネルのパフォーマンスの測定、アセットの情報に基づいたアセット管理タスクの実行に役立ちます。

自身の Dynamic Media アカウントで Dynamic Media 配信レポートへの早期アクセスを利用するには、[アドビカスタマーサポートケースを作成して送信](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)してください。

### アセットビューの新機能 {#assets-view-new-features}

**Dynamic Media パネル**

アセットビューでは、使用可能な別のパネルから Dynamic Media レンディションと、OpenAPI を備えた Dynamic Media レンディションにアクセスできるようになりました。 アセットとレンディションのタイプに基づいて、配信 URL をコピーするか、レンディションをダウンロードするかを選択できます。 詳しくは、[Dynamic Media レンディション](/help/assets/renditions.md#dynamic-media-renditions)および [OpenAPI 機能を備えた Dynamic Media レンディション](/help/assets/renditions.md#dm-with-openapi-renditions)を参照してください。

![動的レンディション](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-features}

* **[Adobe Sign スコープを簡単に更新](/help/forms/adobe-sign-integration-adaptive-forms.md)**：AEM クラウド設定ページから Adobe Sign 設定のスコープを直接変更できるので、既存の設定をよりすばやく簡単に更新できます。

* **[アダプティブフォームの非同期関数のサポート](/help/forms/using-async-funct-in-rule-editor.md)**：アダプティブフォームで外部プロセスの待機やデータの取得などの非同期操作が必要な際は、カスタム関数を使用してこれらの操作を実装し、ルールエディターで設定できます。

### AEM Forms のプレリリース機能 {#forms-new-prerelease-features}

* **公開を管理**：公開を管理ワークフローを使用すると、通常はオーサーインスタンスからパブリッシュインスタンスおよびプレビューインスタンスまで、環境間でフォームを公開または非公開にすることができます。 これにより、ユーザーは効率的な方法でコンテンツの公開、非公開、または公開のスケジュールを設定できます。

* **[コアコンポーネントベースアダプティブフォームのドラフトの自動保存](/help/forms/save-core-component-based-form-as-draft.md)**：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。 後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。 この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

* **[ルールエディターの機能強化](/help/forms/invoke-service-enhancements-rule-editor.md)**：コアコンポーネントに基づくアダプティブフォームでは、呼び出しサービスの出力を使用したドロップダウンオプションの入力、呼び出しサービスの出力を使用した繰り返し可能なパネルの設定、呼び出しサービスの出力を使用した個々のパネルの設定、呼び出しサービスの出力パラメーターを使用した他のフィールドの検証を行うことができるようになりました。

* **[パネルレイアウトのナビゲーションボタンを使用したユーザーエクスペリエンスの向上](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：水平タブ、垂直タブ、アコーディオン、ウィザードなどのナビゲーションボタンをパネルレイアウトに追加できるようになりました。 これらのボタンを使用すると、選択したパネルに焦点を当てて、パネル間の切り替えを簡素化し、ユーザーエクスペリエンスを向上させることができます。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### 統合

* **[アダプティブフォームと Adobe Marketo Engage の統合](/help/forms/integrate-form-to-marketo-engage.md)**：AEM Forms as a Cloud Service に、アダプティブフォームと Adobe Marketo Engage を接続できる使いやすいオプションが追加されました。 この統合により、Marketo Engage のリードキャプチャおよび関連するカスタムオブジェクトを使用して直接アダプティブフォームを作成できます。 Marketo Engage のデータを使用してフォームフィールドに事前入力し、データを送信してスマートキャンペーンやメール自動処理などのワークフローを自動化できるようになりました。 また、アダプティブフォームを Munchkin ライブラリに接続して、訪問数、クリック数、フォーム送信数を追跡することもできます。

#### アダプティブフォームと HTML5 フォーム

* **[既存の XFA テンプレートに基づくアダプティブフォームの作成](/help/forms/create-adaptive-form-using-xfa-templates.md)**：XFA フォームテンプレート（*.XDP ファイル）を使用して、コアコンポーネントベースのアダプティブフォームを作成できるようになりました。 この機能により、XFA テクノロジーに既存の投資を行っている AEM Forms オンプレミスのお客様が AEM Forms as a Cloud Servic を導入することが容易になります。

* **HTML5 フォーム（XFA ベースの web フォーム）**：現在、XFA テクノロジーを使用している AEM Forms オンプレミスのお客様は、HTML5 フォーム（XFA ベースの web フォーム）での既存のユーザーエクスペリエンスを保持しながら、AEM Forms as a Cloud Service に簡単に移行できます。 この機能により、HTML5 形式での XFA フォームテンプレートのレンダリングを有効にし、XFA ベースの PDF フォームをサポートしていないデバイスでフォームにアクセスできます。

  ![HTML フォーム（XFA ベースの web フォーム）](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[ファイル添付の Base64 エンコード文字列のサポート](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**：コアコンポーネントに基づくアダプティブフォームのファイル添付コンポーネントに、添付ファイルを Base64 エンコード文字列として送信するオプションが含まれるようになりました。

#### インタラクティブ通信および通信 API

* **インタラクティブ通信エディター**：インタラクティブ通信エディターは、使いやすいグラフィカルな通信デザインツールで、パーソナライズされたデータ駆動型通信の作成を簡単にし、最新の任意のブラウザーで実行できます。 シームレスなデータ統合、複雑なロジック定義、リッチメディア統合をサポートし、様々なビジネスニーズに対応するプロフェッショナルで準拠したドキュメント、通信、テンプレートの生成を確保します。

  ![インタラクティブ通信エディター](/help/forms/assets/ic-editor.png)


* **[PDF/A 準拠の機能強化](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**：通信 API を使用して、アクセシビリティを確保し、これらの標準への準拠を検証しながら、アーカイブ目的で PDF ドキュメントを PDF/A 形式（1a、2a、3a）に変換できるようになりました。


* **[署名 API（ドキュメント保証）](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**：通信 API の新しい RESTful API により、PDF 署名を簡単に管理できます。 次のような操作をサポートします。
   * 署名をクリア：指定したフィールドから署名を削除します。
   * 署名フィールドを削除：指定した署名フィールドを削除します。


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## 自動フォーム変換サービス

* **[コアコンポーネントベースのアダプティブフォームへの PDF フォームの変換](https://experienceleague.adobe.com/ja/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**：自動フォーム変換サービスを使用して、PDF フォーム、AcroForms、または XFA ベースのフォームをコアコンポーネントベースのアダプティブフォームに変換できるようになりました。


>[!IMPORTANT]
>
> Forms のイノベーションの早期アクセスプログラムへの参加に興味がありますか？ 興味のある機能のリストを添えて、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。## CIF アドオン {#cloud-services-cif}

## CIF アドオン {#cif}

### バグ修正 {#bug-fixes-cif}

* コア CIF コンポーネントで正しく動作するように UI テストを修正しました。
* カテゴリ URL 形式がクラウドインスタンスで期待どおりに機能しない問題を解決しました。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### ツリーレプリケーションのパフォーマンスの向上（およびコンテンツツリーを公開ワークフローの廃止） {#tree-replication-performance}

[ツリーアクティベーションワークフローステップ](/help/operations/replication.md#tree-activation)は、深いコンテンツ階層をレプリケートするために推奨される新しいワークフローモデルステップです。 処理中のツリーレプリケーションワークフローと並行して、独立したレプリケーション（クイック公開や公開の管理など）を実行できます。 これは、一括レプリケーションの処理中に、時間制限があるコンテンツを公開する必要がある場合に特に役立ちます。 ツリーレプリケーションステップは、現在非推奨（廃止予定）となっているコンテンツツリーを公開ワークフローと、関連するワークフローステップに代わるものです。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を独自のアプリケーションやツールに深く統合できます。 新しい AEM as a Cloud Service API は、一貫性があり、明確に文書化され、使いやすいことを目標として、OpenAPI 仕様に従います。 認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成されます。

詳しくは、[OpenAPI ベースの AEM API](/help/implementing/developing/open-api-based-apis.md) を参照し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)を試してください。

具体的には、以下に示す API エンドポイントが早期導入プログラムの一部として使用可能です。 興味がある場合は、どのように活用する予定かを記載したメールを [aem-apis@adobe.com](mailto:aem-apis@adobe.com) まで送信してください。
* [Sites Content Fragments API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites and Assets Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 ロードマップへのインプットとして、このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかや、どのような用途での使用を考えているかについて、ぜひお聞かせください。 ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

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
