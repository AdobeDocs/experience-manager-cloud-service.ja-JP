---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a5159f2ff49b8e216087df4206c14a9ccd89f336
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 64%

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

次のAEM Sites ページイベントは、AEM as a Cloud Service Eventing Platform に基づく外部的に消費されるイベントとして使用できるようになりました。 イベントはAdobe I/Oを介して処理し、外部プロセスとやり取りできます。
* ページが公開されました
* ページが非公開にされました
* ページが削除されました

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメント配信用AEM REST OpenAPI**

コンテンツフラグメント配信用の [AEM REST OpenAPI](/help/headless/aem-rest-openapi-content-fragment-delivery.md) がAEM as a Cloud Serviceで使用できるようになりました。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

### アセットビューの新機能 {#assets-view-new-features}

**予定レポート**

Assets ビューで、繰り返しスケジュールまたは将来の日付にレポートを自動的に生成できるようになり、データ駆動型のインサイトを明らかにする労力を軽減できます。

![ 予定レポート – ](/help/assets/assets/scheduled-reports-tab.png)

### コンテンツハブの新機能 {#content-hub-new-features}

**ライセンス済みアセットのデジタル著作権管理**

Content Hubのユーザー向けライセンスアセットに DRM を活用することで、ライセンスのコンプライアンスを向上させ、ライセンス条項を含むアセットを共有するリスクを最小限に抑えることができるようになりました。このため、ユーザーは、ライセンス条項を確認して同意してから、ライセンス条項をダウンロードする必要があります。

![download-multiple-license](/help/assets/assets/download-multiple-license.png)

**アセットカードのメタデータ設定**

Content Hubでは、アセットカードに表示する必要がある主要なメタデータフィールドを、最大 6 つのフィールドまで設定できるようになりました。

![ アセットカード上の主要なメタデータ ](/help/assets/assets/asset-card-key-metadata.png)

**期限切れアセットの表示とダウンロードの設定**

管理者は、有効期限切れのアセットをコンテンツハブに表示する必要があるかどうかを制御できるようになりました。有効期限切れのアセットを表示する場合は、ユーザーがこれらをダウンロードできるかどうかも定義できます。

![コンテンツハブの有効期限切れのアセット](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースアダプティブフォームのドラフトの自動保存

一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### AEM Forms AI アシスタント

アダプティブフォーム用の生成 AI を使用すれば、まったく新しいレベルの機能により、フォーム開発プロセスが容易になります。かつてないほど短時間で、より優れたフォームを作成できるようになります。

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

### 高度なネットワークオプションを使用したセルフサービスログ転送 {#log-forwarding}

AEM（Apache/Dispatcherを含む）および CDN ログはCloud Managerからダウンロードできますが、多くの組織では、これらのログを優先されるログ先にストリーミングすると便利です。 AEMは、Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch](/help/implementing/developing/introduction/log-forwarding.md)、Splunk への [ ログ転送）をサポートするようになりました。 AEM ログは、オプションで、専用の IP アドレスを使用するなどの高度なネットワーク設定を介して転送できます。

この機能は、ユーザーがセルフサービス方式で設定し、[Config パイプライン ](/help/operations/config-pipeline.md) を使用してデプロイします。

### ビジネスユーザー向けのパイプラインを使用しない URL リダイレクト {#pipeline-free-redirects}

ブラウザーサイドのリダイレクトは、web ページが停止や移動などのシナリオに使用すると便利です。 [ パイプラインを使用しない URL リダイレクト ](/help/implementing/dispatcher/pipeline-free-url-redirects.md) を使用すると、Apache 書き換えマップファイルをAEMの公開場所に配置できます。そこでファイルが自動的に読み込まれるので、ファイルをソースコントロールにコミットしたり、Cloud Manager パイプラインを開始したりする必要はありません。

書き換えファイルを公開するオプションには、ファイルをアセットとしてアップロードする、ACS Commons 書き換えマップマネージャを使用する、カスタムユーザーインターフェイスを操作するなどがあります。

### RDE の設定パイプライン {#config-pipeline-rdes}

迅速な開発環境は、クラウド環境でコードと設定を迅速にデプロイおよびテストするための強力なツールです。 RDE では、トラフィックフィルタールールやリクエスト/応答変換などの CDN 設定、ログ転送およびその他の設定オプションなど、[ 設定 YAML ファイルの同期 ](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) をサポートするようになりました。 詳しくは、サポートされている設定オプションの [ 完全なリストを参照 ](/help/operations/config-pipeline.md) してください。

### 新製品プロファイル {#new-product-profiles}

新しいAEM環境が作成されると、製品プロファイルがAdobe Admin Consoleに自動的に表示され、管理者はライセンス取得済みのソリューションおよび機能へのアクセス権を割り当てることができます。

新しい環境に、更新された一連の製品プロファイルが含まれるようになりました。これにより、Adobe Developer Consoleでの API 認証情報の生成などの今後の機能と互換性を持つようになります。 既存の環境は、将来のリリースで製品プロファイルを更新できるようになります。 [詳細情報](/help/onboarding/aem-cs-team-product-profiles.md)。

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。アドビでは、フィードバックを大切にしています。**<aemcs-new-devconsole-ui-beta@adobe.com>** までメールで送信してください。

![AEM Developer Console の OSGi バンドル画面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0)を参照してください。

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
