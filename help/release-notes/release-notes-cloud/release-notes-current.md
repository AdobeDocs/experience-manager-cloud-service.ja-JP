---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 270e6623c764466f05b25c18faf724a7250309dd
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 67%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.9.0）の公開日は 2024年9月26日（PT）です。次回の機能リリース（2024.10.0）は、2024年10月31日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.9.0 リリースで追加された機能の概要については、2024 年 9 月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-feature-sites}

#### 翻訳管理 {#translation-management}

AEM翻訳ワークフローおよび API アクションで、翻訳ジョブの状態の変化に関するインサイトを提供するトリガーイベントが追加されました。 ユーザーは、Adobe Developer Consoleを通じてこれらのイベントを購読できます。 AEM Translation Management API について詳しくは、[ こちら ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/) を参照してください。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

### アセットセレクターの新機能 {#asset-selector-new-features}

アセットセレクターで、コレクションを参照して目的のアセットを見つけることができるようになりました。
![ アセットセレクターコレクション ](/help/assets/assets/collections-rail-modal-view.png)

### Content Hubの新機能 {#content-hub-new-features}

管理者は、期限切れのアセットをContent Hubに表示する必要があるかどうかを制御できるようになりました。 期限切れのアセットを表示可能にすると、ユーザーがダウンロードできるかどうかを定義することもできます。

![Content Hubの期限切れアセット ](/help/assets/assets/view-download-expired-assets.png)

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

### 機能改善 {#improvements-fixes-cif}

* カテゴリ制限をカスタマイズ可能にします。

### バグ修正 {#bug-fixes-cif}

* Commerce フィールドが、Assets メタデータスキーマエディターと正しく統合されません。
* カルーセル製品のマルチフィールドでドラッグ&amp;ドロップが発生する問題。
* カルーセルカテゴリのマルチフィールドでドラッグ&amp;ドロップが発生する問題。
* カテゴリおよび製品エディターページのページ情報のメニューで、クリックが機能しません。
* 注文確認ページに注文番号が表示されません。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 動的コンテンツを読み込むためのEdge サイドインクルード（ESI） {#esi}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含めることで、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。この機能は徐々に展開されます。

### CDN での基本認証 {#basicauth-cdn}

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する包括的なソリューションとして機能するのではなく、主にビジネス関係者によるコンテンツのレビューなど、簡易な認証ユースケースを対象としています。ユーザー名とパスワードのリストは、設定パイプラインを介してデプロイされた Git の設定ファイルを通じて、秘密鍵タイプのCloud Manager環境変数への参照を使用して管理されます。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

### クライアントサイドリダイレクト {#client-side-redirects}

CDN にデプロイされ CDN で評価される設定ファイル Git で [ ブラウザーリダイレクト ](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) を宣言する。 これは、ページの削除、変更されたサイト構造、SEO の最適化などのシナリオで役立ちます。

### 新しいAEM Developer Console（パブリック Beta） {#aem-developer-console-beta}

クラウド環境でコードをデバッグするためのよりインタラクティブなエクスペリエンスを提供する、刷新された ](/help/implementing/developing/introduction/aem-developer-console.md)0}AEM Developer Console} をお試しください。[

現在のAEM Developer Consoleで「*新しいコンソールを利用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。 Adobeから **<aemcs-new-devconsole-ui-beta@adobe.com>** にメールで送信できるフィードバックを歓迎します。

![AEM Developer Consoleの OSGi バンドル画面 ](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### ビジネスユーザーが Git 外部でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache/Dispatcher は、パブリッシュリポジトリーの特定の場所に配置された書き換えマップを取り込み、web 層パイプラインを実行しなくても読み込みます。 このアプローチを使用すると、ビジネスユーザーはスプレッドシートや UI （ACS Commons リダイレクトマップマネージャーやカスタムアプリケーションなど）を使用してリダイレクトを宣言できます。 **<aemcs-cdn-config-adopter@adobe.com>** に電子メールを送信して、早期導入プログラムに参加します。

### RDE の設定パイプライン（早期導入プログラム） {#config-pipeline-rdes-early-adopter}

[ 設定パイプライン ](/help/operations/config-pipeline.md) は、CDN オプション（トラフィックフィルタールール、リクエスト/応答の変換など）を含む yaml ファイル設定をデプロイするために使用します。 これらの同じ設定を CLI を使用する RDE （迅速な開発環境）にデプロイするように **<aemcs-cdn-config-adopter@adobe.com>** にメールを送信して、早期導入プログラムに参加してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0)を参照してください。

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
