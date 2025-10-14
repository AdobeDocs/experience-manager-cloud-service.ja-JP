---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.9.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: 75ecd154-112a-4468-9962-de50bb1f4cd0
source-git-commit: 5db419e674ceb3c861f53a19e7b852c89ebd3702
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 90%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.9.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.9.0 バージョンの機能リリースノートの概要について説明します。

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

2024.9.0 リリースで追加された機能の概要については、2024年9月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-feature-sites}

#### 翻訳管理 {#translation-management}

AEM 翻訳ワークフローと API アクションが、翻訳ジョブの状態の変化に関するインサイトを提供するイベントをトリガーするようになりました。ユーザーは、Adobe Developer Consoleを通じてこれらのイベントを購読できます。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の早期アクセス機能 {#dm-early-access}

**AI 生成のビデオキャプション**

Adobe Dynamic Media の AI 生成のビデオキャプションは、人工知能を使用して、ビデオコンテンツのキャプションを自動的に生成します。 この機能は、正確なリアルタイムのキャプションを提供することで、アクセシビリティを向上させ、ユーザーエクスペリエンスを強化するように設計されています。 AI は、ビデオのオーディオトラックを分析し、音声を文字起こしして、キャプションを作成します。キャプションを編集して、精度を高めたりカスタマイズしたりできます。 これらのキャプションは、アクセシビリティ要件を満たし、テキストベースのビデオサポートに依存している、またはこれを好むオーディエンスのビデオエンゲージメントを向上させるのに役立ちます。

Dynamic Media アカウントで AI 生成のキャプションサポートに早期アクセスするには、[アドビカスタマーサポートケースを作成して送信](/help/assets/dynamic-media/video.md##enable-dash)してください。

### アセットセレクターの新機能 {#asset-selector-new-features}

アセットセレクターでは、コレクションを参照して目的のアセットを検索できるようになりました。
![アセットセレクターのコレクション](/help/assets/assets/collections-rail-modal-view.png)

### コンテンツハブの新機能 {#content-hub-new-features}

管理者は、有効期限切れのアセットをコンテンツハブに表示する必要があるかどうかを制御できるようになりました。有効期限切れのアセットを表示する場合は、ユーザーがこれらをダウンロードできるかどうかも定義できます。

![コンテンツハブの有効期限切れのアセット](/help/assets/assets/view-download-expired-assets.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースアダプティブフォームのドラフトの自動保存

一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。 この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

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

* Commerce のフィールドが、Assets メタデータスキーマエディターと適切に統合されていない。
* カルーセル製品のマルチフィールドでのドラッグ＆ドロップの問題。
* カルーセルカテゴリのマルチフィールドでのドラッグ＆ドロップの問題。
* カテゴリおよび製品エディターページのページ情報のメニューで、クリックは機能しません。
* 注文番号が注文確認ページに表示されません。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 動的コンテンツ読み込み用のエッジサイドインクルード（ESI） {#esi}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含めることで、より高い TTL で HTML ページ全体を CDN でキャッシュしながら、より頻繁なアップデート（低い TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。この機能は段階的にロールアウトされます。

### CDN での基本認証 {#basicauth-cdn}

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する包括的なソリューションとして機能するのではなく、主にビジネス関係者によるコンテンツのレビューなど、簡易な認証ユースケースを対象としています。ユーザー名とパスワードのリストは、設定パイプラインを介してデプロイされた Git の設定ファイルを通じて、秘密鍵タイプのCloud Manager環境変数への参照を使用して管理されます。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

### サーバーサイドのリダイレクト {#server-side-redirects}

CDN にデプロイされ CDN で評価される設定ファイル Git で [&#x200B; ブラウザーリダイレクト &#x200B;](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) を宣言する。 これは、ページの削除、変更されたサイト構造、SEO の最適化などのシナリオで役立ちます。

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。アドビでは、フィードバックを大切にしています。**<aemcs-new-devconsole-ui-beta@adobe.com>** までメールで送信してください。

![AEM Developer Console の OSGi バンドル画面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### ビジネスユーザーが Git 外部でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。このアプローチにより、ビジネスユーザーは、スプレッドシートや、ACS Commons リダイレクトマップマネージャーやカスタムアプリケーションなどの UI を使用してリダイレクトを宣言できます。早期導入プログラムに参加するには、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信します。

### RDE 用の設定パイプライン（早期導入プログラム） {#config-pipeline-rdes-early-adopter}

[&#x200B; 設定パイプライン &#x200B;](/help/operations/config-pipeline.md) は、CDN オプション（トラフィックフィルタールール、リクエスト/応答の変換など）を含む yaml ファイル設定をデプロイするために使用します。 早期導入プログラムに参加するには、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信し、CLI を使用する RDE（迅速な開発環境）にこれらの同じ設定をデプロイします。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

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
