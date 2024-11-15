---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 2b34b23c05ff125a24fb0969d0239a384e773011
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 98%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.10.0）のリリース日は、2024年10月31日（PT）です。次回の機能リリース（2024.11.0）は 2024年11月21日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**最新化されたページイベント**

次の AEM Sites ページイベントは、AEM as a Cloud Service イベンティングプラットフォームに基づく外部で消費可能なイベントとして使用できるようになりました。イベントは Adobe I/O を介して処理され、外部プロセスとやり取りできます。
* ページが公開されました
* ページが非公開にされました
* ページが削除されました

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメント配信用の AEM REST OpenAPI**

[コンテンツフラグメント配信用の AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) が AEM as a Cloud Service で使用できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

### アセットビューの新機能 {#assets-view-new-features}

**スケジュールされたレポート**

繰り返しスケジュールまたは今後の日付で、アセットビューでレポートを自動的に生成できるようになったので、データに基づくインサイトの発見が容易になりました。

![スケジュールされたレポート](/help/assets/assets/scheduled-reports-tab.png)

### コンテンツハブの新機能 {#content-hub-new-features}

**ライセンス済みアセットの Digital Rights Management**

組織は、コンテンツハブのユーザー向けにライセンス済みアセットに DRM を活用し、ライセンス済みアセットのダウンロードを開始する前にユーザーにライセンス条件の確認と同意を要求することで、ライセンスコンプライアンスを強化し、ライセンス条件付きのアセットを共有するリスクを最小限に抑えることができるようになりました。詳しくは、[コンテンツハブのライセンス済みアセットの管理](/help/assets/manage-licensed-assets-on-content-hub.md)を参照してください。

![複数ライセンスをダウンロード](/help/assets/assets/download-multiple-license.png)

**アセットカードのメタデータ設定**

コンテンツハブでは、アセットカードに表示する必要がある主なメタデータフィールドを最大 6 個まで設定できるようになりました。詳しくは、[コンテンツハブの設定](/help/assets/configure-content-hub-ui-options.md#asset-card)のアセットカードの節を参照してください。

![アセットカードの主なメタデータ](/help/assets/assets/asset-card-key-metadata.png)

**有効期限切れのアセットの表示とダウンロードの設定**

管理者は、有効期限切れのアセットをコンテンツハブに表示する必要があるかどうかを制御できるようになりました。有効期限切れのアセットを表示する場合は、ユーザーがこれらをダウンロードできるかどうかも定義できます。詳しくは、[コンテンツハブの設定](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub)の有効期限切れのアセットの節を参照してください。

![コンテンツハブの有効期限切れのアセット](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Formsの新機能 {#forms-new-features}

* [パネルレイアウトのナビゲーションボタンを使用したユーザーエクスペリエンスの向上](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)：水平タブ、垂直タブ、アコーディオン、ウィザードなどのナビゲーションボタンをパネルレイアウトに追加できるようになりました。これらのボタンを使用すると、選択したパネルに焦点を当てて、パネル間の切り替えを簡素化し、ユーザーエクスペリエンスを向上させることができます。

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### AEM Forms の新しいプレリリース機能 {#forms-new-prerelease-features}

* [コアコンポーネントベースアダプティブフォームのドラフトの自動保存](/help/forms/save-core-component-based-form-as-draft.md)：一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

* [Adobe Sign スコープを簡単に更新](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms)：AEM クラウド設定ページから Adobe Sign 設定のスコープを直接変更できるので、既存の設定をよりすばやく簡単に更新できます。

* [アダプティブフォームの非同期関数のサポート](/help/forms/using-async-funct-in-rule-editor.md)：アダプティブフォームで外部プロセスの待機やデータの取得などの非同期操作が必要な際は、カスタム関数を使用してこれらの操作を実装し、ルールエディターで設定できます。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### AEM Forms AI アシスタント

[ アダプティブForms用のジェネレーティブ AI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) は、まったく新しいレベルの機能を提供し、Forms 開発プロセスを簡単にします。 かつてないほど短時間で、より優れたフォームを作成できるようになります。

![生成 AI アシスタント、アダプティブフォーム](/help/forms/assets/generative-ai-assistant.png)

オファー上の生成 AI 機能は次のとおりです。

* **製品クエリ用 AI アシスタント**：AEM フォーム関連の質問に対する回答をすぐに得られます。AI アシスタントは、ユーザー自身のナレッジベースとして機能し、プラットフォーム内で直接、インサイトに満ちたガイダンスとレコメンデーションを提供します。

* **アダプティブフォームの生成**：生成 AI プロンプトを使用して、本格的なフォームを簡単に作成します。アドビの生成 AI は、離脱を減らし、エクスペリエンスをパーソナライズする使いやすいフォームを自動的に生成します。

* **Forms のパネル生成**：特定のデータ収集ニーズに合わせてフォームセクションを生成します。例えば、支払い情報、顧客の環境設定、旅行の詳細を収集するためのセクションを生成します。

* **フォームレイアウトの変更**：生成 AI プロンプトを使用して、様々なレイアウトやデザインを試します。ウィザードやタブ付きビューなどの様々なレイアウトを試して、自身のフォームに最適なスタイルを見つけます。生成 AI プロンプトを使用してモバイル機器のレスポンシブデザイン向けにフォームを最適化し、ユーザーが好む魅力的な外観のフォームを作成します。

* **送信アクションの設定**：生成 AI プロンプトを使用して、フォームの送信アクションを簡単に設定します。事前定義済みの送信アクションのライブラリ、または自社開発チームによって作成およびデプロイされたカスタム送信アクションから選択します。

>[!IMPORTANT]
>
> Forms のイノベーションの早期アクセスプログラムへの参加に興味がありますか？興味のある機能のリストを添えて、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。

## CIF アドオン {#cloud-services-cif}

### バグ修正 {#bug-fixes-cif}

* コア CIF コンポーネントで正しく動作するように UI テストを修正しました。
* カテゴリ URL 形式がクラウドインスタンスで期待どおりに機能しない問題を解決しました。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### フォーム送信を制御する設定 {#configuration-submissions}

特定の場所での Coral フォームまたは Foundation フォームのフォーム送信を制御することを目的に、AEM では新しい設定 `com.adobe.granite.ui.components.FormRestrict` が導入されました。この設定は、次の 2 つのフィールドで構成されます。

1. **許可されているパスを追加**：フォームアクションが許可されているパスを指定します。
1. **動作を制限**：制限されているパス（許可リストに含まれていないパス）の動作を決定します。次の 2 つのオプションのどちらかを選択できます。
   * **ポップアップ**（デフォルト）：ポップアップ通知を表示します。
   * **防止**：フォームの送信をブロックします。

>[!NOTE]
>
>この設定は、`/apps`、`/libs`、`/mnt/overlay`、`/mnt/override` にあるすべての Coral フォームまたは Foundation フォームでサポートされているわけではありません。

### 高度なネットワークオプションを備えたセルフサービスログ転送 {#log-forwarding}

AEM（Apache／Dispatcher を含む）および CDN ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリーミングすることが有益であると考えられています。AEM では、Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch）、Splunk への[ログ転送](/help/implementing/developing/introduction/log-forwarding.md)がサポートされるようになりました。AEM ログは、オプションで、専用 IP アドレスを使用するなどの高度なネットワーク設定を介して転送できます。

この機能は、ユーザーがセルフサービス方式で設定し、[設定パイプライン](/help/operations/config-pipeline.md)を使用してデプロイします。

### ビジネスユーザー向けのパイプライン不要の URL リダイレクト {#pipeline-free-redirects}

ブラウザーサイドのリダイレクトは、web ページの削除や移動があった場合など、様々なシナリオで役立ちます。[パイプライン不要の URL リダイレクト](/help/implementing/dispatcher/pipeline-free-url-redirects.md)を使用すると、Apache 書き換えマップファイルを AEM パブリッシュの場所に配置して、自動的に読み込むことができます。ファイルをソース管理にコミットしたり、Cloud Manager パイプラインを開始したりする必要はありません。

書き換えファイルを公開するオプションには、アセットとしてアップロードする、ACS Commons 書き換えマップマネージャーを使用する、カスタムユーザーインターフェイスを操作するなどがあります。

### RDE の設定パイプライン {#config-pipeline-rdes}

迅速な開発環境は、クラウド環境でコードと設定を迅速にデプロイおよびテストするための強力なツールです。RDE では、トラフィックフィルタールールやリクエスト／応答変換などの CDN 設定、ログ転送、その他の設定オプションを含む[設定 YAML ファイルの同期](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)がサポートされるようになりました。詳しくは、サポートされている設定オプションの[完全なリストを参照](/help/operations/config-pipeline.md)してください。

### 新しい製品プロファイル {#new-product-profiles}

新しい AEM 環境を作成すると、製品プロファイルが Adobe Admin Console に自動的に表示され、管理者はライセンス済みソリューションと機能へのアクセスを割り当てることができます。

新しい環境に更新済み製品プロファイルのセットが含まれるようになり、Adobe Developer Console での API 認証情報の生成などの今後の機能と互換性を持つようになりました。既存の環境では、今後のリリースで製品プロファイルを更新できるようになります。[詳細情報](/help/onboarding/aem-cs-team-product-profiles.md)。

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。アドビでは、フィードバックを大切にしています。**<aemcs-new-devconsole-ui-beta@adobe.com>** までメールで送信してください。

![AEM Developer Console の OSGi バンドル画面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-0-release/whats-new-2024-10-0)を参照してください。

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
