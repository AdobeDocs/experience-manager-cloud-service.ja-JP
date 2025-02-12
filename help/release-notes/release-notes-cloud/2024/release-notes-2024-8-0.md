---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.8.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.8.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: dd1d4b8f-8331-4e97-a754-37e720974db6
source-git-commit: 61b40acf4f51c16a694b7c3b13ee1c480670ee3f
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.8.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.8.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2022年、2023年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.8.0）の公開日は 2024年8月29日（PT）です。次回の機能リリース（2024.9.0）は、2024年9月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.8.0 リリースで追加された機能の概要については、2024年8月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-feature-sites}

**Edge Delivery Services 用の AEM オーサリング**

次のような既存の Sites [継承](/help/sites-cloud/authoring/universal-editor/inheritance.md)機能がサポートされるようになりました。

* [AEM ローンチ](/help/sites-cloud/authoring/launches/overview.md)
* ページレベルでの [MSM](/help/sites-cloud/administering/msm/overview.md)

さらに、次のページ管理機能がサポートされるようになりました。

* [AEM タグ](/help/sites-cloud/authoring/sites-console/tags.md)は、Edge Delivery Services に[分類](/help/edge/wysiwyg-authoring/taxonomy.md)として書き出すことができます。
* Edge Delivery Services 用[テンプレート](/help/sites-cloud/authoring/universal-editor/templates.md)は、近日中に提供されます。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-new-features}

**アップデート後の Adobe Firefly 画像の生成**

Assets as a Cloud Service では、Firefly の最新ウィジェットを使用するようになりました。これにより、Adobe Firefly を使用して様々なスタイルの画像を生成できます。組み込みの Firefly エディターを使用してスタイル、構成、寸法などを定義すれば、必要なアセットを AEM Assets リポジトリ内で直接作成して保存し、すぐに使用できます。

![Adobe Firefly 画像の生成](/help/assets/assets/bugatti-type-57.png)

**PSB ファイルのサポート**

Assets as a Cloud Service では、既存の PSD ファイルのサポートに加えて、Photoshop の大きなドキュメント（PSB ファイル）がサポートすされるようになりました。

### コンテンツハブの新しい機能強化 {#content-hub-new-enhancements}

* 長いファイル名の取り扱いを改善しました。ツールヒントを使用して完全な名前を簡単に展開できます。
* サムネールを改善し、コンテンツの縦横比に合わせて、より広い領域のコンテンツがカバーされるようにしました。
* コンテンツハブでサポートされる、AEM のカスタムサムネールエクスペリエンス。
* カラー検索の改善。
* 設定の改善により、操作性が向上します。
* 作成者の名前が反映されるように、コレクションの情報ページを改善しました。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースアダプティブフォームのドラフトの自動保存

一部が完了したフォームを自動的にドラフトとして保存する、自動保存機能を利用できるようになりました。後で戻って、同じデバイスまたは他のデバイスで入力を完了できます。この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。


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

* **送信アクションの設定**：生成 AI プロンプトを使用して、フォームの送信アクションを簡単に設定します。事前定義済みの送信アクションのライブラリ、または自社開発チームによって作成およびデプロイされたカスタム送信アクションのリストから選択します。

>[!IMPORTANT]
>
> イノベーションの早期アクセスプログラムへの参加に興味がある方は、興味のある機能のリストを添えて、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信してください。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### コンテンツ配信関連の早期導入プログラム {#foundation-early-adopter}

以下の早期導入プログラムのどれに興味があるかを明記して、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信してください。

#### CDN での基本認証（早期導入プログラム） {#basicauth-cdn}

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する包括的なソリューションとして機能するのではなく、主にビジネス関係者によるコンテンツのレビューなど、簡易な認証ユースケースを対象としています。ユーザー名とパスワードのリストは、秘密鍵タイプの Cloud Manager 環境変数を参照して、設定パイプライン経由でデプロイされる Git の設定ファイルを通じて管理されます。[詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### クライアントサイドのリダイレクト（早期導入プログラム） {#client-side-redirects-early-adopter}

ソース管理で 301/302 クライアントサイドのリダイレクトを設定し、CDN にデプロイします。[詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. -->リクエストと応答の変換、AEM 外のサイトへのトラフィックのルーティングなど、[CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)に関連して既に利用可能な他の機能がいくつかあります。

#### ビジネスユーザーが Git 外部でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。このアプローチにより、ビジネスユーザーは、スプレッドシートや、ACS Commons リダイレクトマップマネージャーやカスタムアプリケーションなどの UI を使用してリダイレクトを宣言できます。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含め、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
