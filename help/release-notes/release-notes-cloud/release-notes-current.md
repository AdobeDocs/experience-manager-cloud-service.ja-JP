---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 9cc49bf83d278d4064faa1d0157201226a067cb1
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 53%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.8.0）の公開日は 2024年8月29日（PT）です。次回の機能リリース（2024.9.0）は、2024年9月26日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- ## Release Video {#release-video}

Have a look at the August 2024 Release Overview video for a summary of the features added in the 2024.8.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sites の新機能 {#new-feature-sites}

**Edge Delivery Services 用の AEM オーサリング**

次のような既存の Sites [ 継承 ](/help/sites-cloud/authoring/universal-editor/inheritance.md) 機能がサポートされるようになりました。

* [AEM ローンチ](/help/sites-cloud/authoring/launches/overview.md)
* ページレベルでの [MSM](/help/sites-cloud/administering/msm/overview.md)

さらに、次のページ管理機能がサポートされるようになりました。

* [AEM タグ ](/help/sites-cloud/authoring/sites-console/tags.md) は、Edge Delivery Servicesに [ 分類 ](/help/edge/wysiwyg-authoring/taxonomy.md) として書き出すことができます。
* Edge Delivery Services用 [ テンプレート ](/help/edge/wysiwyg-authoring/templates.md) は、近日中に提供されます。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### アセットビューの新機能 {#assets-view-new-features}

**更新されたAdobe Firefly画像の生成**

Assetsのas a Cloud Serviceでは、Fireflyの最新ウィジェットを使用するようになりました。このウィジェットを使用すると、Adobe Fireflyを使用して様々なスタイルの画像を生成できます。 組み込みのアセットエディターを使用してスタイル、構成、寸法などを定義することで、必要なFireflyをすばやく作成してAEM Assets リポジトリー内に直接保存し、すぐに使用できます。

![Adobe Firefly画像の生成 ](/help/assets/assets/bugatti-type-57.png)

**PSB ファイルのサポート**

Assetsのas a Cloud Serviceでは、既存のPSDファイルのサポートに加えて、Photoshopの大きなドキュメント（PSB ファイル）をサポートするようになりました。

### Content Hubの新しい機能強化 {#content-hub-new-enhancements}

* 長いファイル名の処理が改善され、ツールヒントを使用して完全な名前を簡単に拡張できます。
* コンテンツの縦横比に合わせて、より広い領域のコンテンツをカバーするようにサムネールを改善しました。
* コンテンツハブでサポートされる、AEMのカスタムサムネールエクスペリエンス。
* カラー検索の改善。
* 設定の改善により、操作性が向上します。
* コレクションの情報ページが改善され、作成者の名前が反映されるようになりました。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Formsの新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースのアダプティブFormsのドラフトを自動保存

部分的に完了したフォームを自動的にドラフトとして保存する自動保存機能を利用できるようになりました。 後で戻って、同じデバイスまたは他のデバイスで充填を完了することができます。 この機能により、ユーザーはフォームへの入力を最初からやり直す必要がなくなるので、フォームの放棄が減り、組織のコンバージョン率が向上します。


### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms早期アクセスプログラム プログラムは、最先端のイノベーションに独占的にアクセスし、その発展を形作るユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### AEM Forms AI アシスタント

アダプティブForms用のジェネレーティブ AI は、まったく新しいレベルの機能を提供し、フォーム開発プロセスを簡単にします。 これにより、以前よりも迅速に、より優れたフォームを作成できます。

![ ジェネレーティブ AI アシスタント、アダプティブForms](/help/forms/assets/generative-ai-assistant.png)

提供されるジェネレーティブ AI 機能は次のとおりです。

* **製品クエリ用 AI アシスタント**:AEM フォームに関する質問にすぐに回答できます。 AI アシスタントは、独自の個人のナレッジベースとして機能し、プラットフォーム内で直接洞察に満ちたガイダンスと推奨事項を提供します。

* **アダプティブフォームの生成**：生成 AI プロンプトを使用して、本格的なフォームを簡単に作成します。 ジェネレーティブ AI は、ドロップオフを減らし、エクスペリエンスをパーソナライズする、使いやすいフォームを自動的に生成します。

* **Formsのパネル生成**：特定のデータ収集ニーズに合わせてカスタマイズされたフォームセクションを生成します。 例えば、支払い情報、顧客の環境設定、旅行の詳細を収集するためのセクションを生成します。

* **フォームレイアウトの変更**：生成 AI プロンプトを使用して、様々なレイアウトやデザインを試します。 フォームに最適なレイアウトをウィザードやタブ付きビューで試すことができます。 ジェネレーティブ AI プロンプトを使用すると、モバイルの応答性に合わせてフォームを最適化し、ユーザーの好みに合わせて視覚的に魅力的なフォームを作成できます。

* **送信アクションの設定**：生成 AI プロンプトを使用すると、フォームの送信アクションを簡単に設定できます。 事前定義済みの送信アクションのライブラリから、または独自の開発チームが作成およびデプロイしたカスタム送信アクションのリストから選択します。

>[!IMPORTANT]
>
> 任意のイノベーションのために早期アクセスプログラムへの参加に興味がある場合は、興味のある機能のリストを記載したメールを公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) に送信するだけです。


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
