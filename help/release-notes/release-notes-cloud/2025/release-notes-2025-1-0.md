---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2025.1.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: 085629bf-fb24-4511-af6c-bbbeedcb6b98
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 92%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2025.1.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2025.1.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.1.0）のリリース日は、2025年1月30日（PT）です。次回の機能リリース（2025.2.0）は 2025年3月4日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2025.1.0 リリースで追加された機能の概要については、2025年1月のリリースに関する概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3456072?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**コンテンツフラグメントエディターのコメント機能が一般公開されました**

AEM コンテンツフラグメントエディターの最新化された新しいコメントサービスを使用して、AEM コンテンツフラグメントをオーサリングする際に、同僚と簡単に共同作業できます。
[詳細情報](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment)。

**コンテンツフラグメントエディターと管理ユーザーインターフェイスで、AEM as a Cloud Service バージョンのサポートが更新されました**

新しいコンテンツフラグメント管理およびエディターのユーザーインターフェイスでサポートされる AEM as a Cloud Service の最小バージョンが、2023.8.13099 になりました。新しいユーザーインターフェイスの一般提供リリース前のバージョンは、サポートされなくなりました

### 早期導入プログラム {#sites-early-adopter}

**コンテンツフラグメントの強化**

[一意の ID ベースの参照を用いたコンテンツフラグメント参照](/help/headless/graphql-api/uuid-reference-upgrade.md)の強化は、フラグメントを別の場所に移動した場合でも、個々のコンテンツフラグメントに対する GraphQL クエリが安定した状態を確保するのに役立ちます。これを、「ByID」クエリで実現できるようになりました。パスは変更され、「ByPath」クエリが壊れる可能性がありますが、UUID は安定します。また、新しい ID を、任意のクエリやその他の適用可能な API リクエストのプロパティとして返すこともできます。現在の制限事項（2025.1）：ページ参照は、一意の ID ではまだサポートされていません。コンテンツフラグメントでページが参照されている場合は、この機能を使用しないでください。この制限は、次回の AEM as a Cloud Service リリースで削除される予定です。

**コンテンツフラグメント配信用の AEM REST OpenAPI**

[コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) を、AEM as a Cloud Service で使用できるようになりました。

### 廃止される機能 {#sites-deprecated}

#### SPA エディター {#spa-editor}

[SPA エディター](/help/implementing/developing/hybrid/introduction.md)は、リリース 2025.1.0 以降の新しいプロジェクトでは廃止されました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のようになりました。

* ビジュアル編集用の[ユニバーサルエディター](https://www.aem.live/docs/aem-authoring)。
* フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。

#### PWA の機能 {#pwa-features}

AEM Sitesの [ プログレッシブ web アプリ（PWA）機能 ](/help/sites-cloud/authoring/sites-console/enable-pwa.md) は、リリース 2025.1.0 以降の新しいプロジェクトで非推奨（廃止予定）になりました。この機能は、既存のプロジェクトでは引き続きサポートされますが、新規プロジェクトでは使用しないでください

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### AEM Assets の新機能 {#new-features-assets}

**Dynamic Media 配信レポート**

アセットレベルの配信数、リファラーの詳細、AEM Assets 内のアセットパス、一意のアセット ID など、Dynamic Media を通じて配信されたアセットの配信インサイトを取得します。AEM Assets リポジトリまたは特定のフォルダー階層内のすべてのアセットに対するレポートを生成します。これらのインサイトにより、配信されたアセットの ROI を測定、チャネルのパフォーマンスを評価し、アセット管理に関する情報に基づいた決定を行うことができます。

![動的レンディション](/help/assets/assets/referrer.png)

**Dynamic Media のマルチオーディオとキャプション**

[Dynamic Media のビデオに対するマルチキャプションとマルチオーディオトラックのサポート](/help/assets/dynamic-media/video.md#about-msma) - プライマリビデオに複数のキャプションと複数のオーディオトラックを容易に追加できるようになりました。この機能により、グローバルなオーディエンスがビデオにアクセスできるようになります。1 つの公開済みプライマリビデオを複数の言語でグローバルオーディエンスに向けてカスタマイズし、様々な地理的地域のアクセシビリティガイドラインに従うことができます。また、作成者は、ユーザーインターフェイスの 1 つのタブからキャプションとオーディオトラックを管理することもできます。

**HTTP 経由の動的アダプティブストリーミングのサポート**

CMAF が有効になっている Dynamic Media ビデオ配信で、アダプティブストリーミング向けの新しいプロトコル（DASH：HTTP 経由の動的アダプティブストリーミング）のサポートが開始しました。

* アダプティブストリーミング（DASH／HLS）により、ユーザーがビデオを視聴する際の操作性が向上します。

* DASH はアダプティブビデオストリーミング用の国際標準プロトコルで、業界で広く採用されています。


**アセットの再処理**

アセットビューでは、フォルダー内で使用可能なアセットの再処理がサポートされるようになりました。「**フルプロセス**」オプションと詳細オプション（デフォルトのプレビューレンディション、メタデータ、後処理ワークフロー、処理プロファイルなど）のどちらを使用するかを選択できます。

### AEM Assets の早期アクセス機能 {#early-access-features-assets}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 キャプションは、元のオーディオ、追加のオーディオトラック、またはビデオプロパティページの「キャプションとオーディオ」タブで提供される追加のキャプションから生成されます。60 を超える言語がサポートされているので、ビデオを公開する前にキャプションを確認およびプレビューできます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新機能 {#forms-new-features}

* **公開を管理**: [ 公開を管理 ](/help/forms/manage-publication.md#publish-forms-using-the-manage-publication-option)）ワークフローを使用して、通常はオーサーインスタンスからパブリッシュインスタンスとプレビューインスタンスに向けて、複数の環境にわたってフォームを公開または非公開にすることができます。 これにより、ユーザーは効率的な方法でコンテンツの公開、非公開、または公開のスケジュールを設定できます。

* **[コアコンポーネントベースアダプティブフォームのドラフトの自動保存](/help/forms/save-core-component-based-form-as-draft.md)**：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。 後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。 この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

* **[ルールエディターの機能強化](/help/forms/invoke-service-enhancements-rule-editor.md)**：コアコンポーネントに基づくアダプティブFormsの場合、サービスの呼び出しの出力を使用してドロップダウンオプションを入力し、繰り返し可能なパネルまたは個々のパネルを設定できます。 さらに、この出力は、他のフィールドを検証するためにも使用できます。

* **[パネルレイアウトのナビゲーションボタンを使用したユーザーエクスペリエンスの向上](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**：水平タブ、垂直タブ、アコーディオン、ウィザードなどのナビゲーションボタンをパネルレイアウトに追加できるようになりました。 これらのボタンを使用すると、選択したパネルに焦点を当てて、パネル間の切り替えを簡素化し、ユーザーエクスペリエンスを向上させることができます。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### [ アダプティブFormsのHTML メールテンプレート ](/help/forms/html-email-templates-in-adaptive-forms.md)

アダプティブFormsでは、HTMLのメールテンプレートを使用できます。 HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

#### クラウドストレージのサポートの強化：Azure Blob Storage への直接 PDF アップロード

AEM Forms Document Generation API では、生成されたPDF ドキュメントの Azure Blob Storage への直接アップロードをサポートするようになりました。 この機能強化により、ストレージと取得が合理化され、効率の向上やクラウドワークフローとの統合が促進されます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Java 21 サポート {#java21}

Java 21 を使用してコードをビルドできるようになりました。これには、新機能（switch ステートメントのパターンマッチング、sealed クラスなど）とパフォーマンスの向上が含まれ、Java 17 ビルドも新たにサポートされます。Maven プロジェクトとライブラリのバージョンのアップデートを含む設定手順について詳しくは、[ビルド環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)の記事を参照してください。

Java 17 または 21 ビルドが検出されると、より高パフォーマンスの Java 21 **ランタイム**&#x200B;が自動的にデプロイされます。ただし、Java 11 でビルドされた環境については、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) にメールを送信して Java 21 ランタイムをオプトインすることをお勧めします。[Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> Java 21 **ランタイム**&#x200B;は、2 月にサンドボックスと dev/RDE を開始し、4 月にステージング／実稼動を開始して、**すべて**&#x200B;の環境に徐々にデプロイされます（Java 17 または 21 で既にビルドされ、Java 21 ランタイムが存在する環境は除く）。

### サンドボックスプログラムは、設定パイプラインをサポートします {#sandbox-config-pipelines}

サンドボックスプログラムで設定パイプラインがサポートされるようになりました。このパイプラインは、Git 内で保持される yaml ファイルをデプロイするように Cloud Manager で設定できます。

CDN、ログ転送、バージョンパージ／監査ログのパージメンテナンスタスクを設定できる設定パイプラインについて詳しくは、[こちら](/help/operations/config-pipeline.md)を参照してください。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を、自分たちのアプリケーションやツールに深く統合できます。新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成されます。

詳しくは、[OpenAPI ベースの AEM API](/help/implementing/developing/open-api-based-apis.md) を参照し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)を試してください。

具体的には、以下に示す API エンドポイントが早期導入プログラムの一部として使用可能です。 興味がある場合は、どのように活用する予定かを記載したメールを [aem-apis@adobe.com](mailto:aem-apis@adobe.com) まで送信してください。

* [Sites Content Fragments API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* Sites およびAssets Folders API
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかについて、ぜひお聞かせください。さらに、製品ロードマップへのインプットとして、お客様が何を想定されるかをお教えください。ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。 アドビでは、フィードバックを大切にしています。[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com) までメールで送信してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2412-release/fixed-issues-2024-12-0)を参照してください。

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
