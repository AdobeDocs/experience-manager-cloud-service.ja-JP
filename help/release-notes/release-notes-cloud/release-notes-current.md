---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 5247a06f15a3edd34a419f9d64aa0590b43c1612
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 25%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2021年、2022年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.5.0）のリリース日は、2024年5月30日（PT）です。次回の機能リリース（2024.6.0）は 2024年6月27日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.5.0 リリースで追加された機能の概要については、2024年5月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Sites の新機能 {#sites-new-features}

**Edge Delivery Services 用の AEM オーサリング**

安定性の向上と様々な機能強化により、オーサリングエクスペリエンスが向上しました。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットのブラウジング**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像やその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットブラウジング](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合早期導入プログラムの詳細をご案内いたしますので、ご自身の正式なメール ID から aemcs-headless-adopter@adobe.com までご連絡ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理ビューの新機能 {#admin-view-new-features}

* WebM は、ビデオの処理プロファイルでサポートされる出力ファイルになりました。
* MP4 は、Express のAEMのネイティブ統合（インポートおよびエクスポート）でサポートされるようになりました。

### アセットビューの新機能 {#assets-view-new-features}

**AEMとDynamic Mediaへのアセットの公開**

Experience Manager Assetsでは、次のことがすぐに可能になりました [Experience ManagerとDynamic Mediaへのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md) 管理者ビューに切り替えずに、アセット ビューを使用します。 アセットのアップロード、参照および検索時に、アセットを公開できます。

![公開ステータス 1 を確認](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Formsの新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースのアダプティブFormsの強化されたビジュアルルールエディター

このリリースでは、コアコンポーネントベースのアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。次の操作が可能になっています。

* ビジュアルルールエディターでルールを作成して [デフォルトのフォーム送信成功/失敗メッセージを上書き](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* アダプティブFormsのルールエディターで、次の機能が追加されました。 [「WHEN」操作に対して様々なタイプのフィールドを選択します](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* フォーム作成者は、カスタム関数をに適用できるようになりました [送信前にデータを前処理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* の使用 [**ドラフトとして保存**](/help/forms/save-core-component-based-form-as-draft.md) 後で送信するために、部分的に完了したフォームを保存する機能。 これは、ユーザーがフォームの入力を中断して後で戻る必要がある場合に便利です。



### AEM Formsの早期導入者機能 {#forms-new-early-adopter-features}

AEM Forms早期導入プログラムは、誰よりも先に最先端のイノベーションに排他的にアクセスし、開発を形作るユニークな機会を提供します。
プログラムでは、複数のイノベーションにアクセスできます。

このリリースノートでは、現在のリリースで提供されているイノベーションの一覧を示します。 早期導入プログラムで利用可能なイノベーションの完全なリストについては、次を参照してください。 [AEM Forms早期導入プログラムドキュメント](/help/forms/early-adopter-ea-features.md).

#### ボット保護方法の強化

AEM Formsは、2 つの一般的な CAPTCHA ソリューション（Cloudflare Turnstile および hCaptcha）のサポートを追加することにより、セキュリティ機能を強化しました。 これにより、既に利用可能なGoogle reCAPTCHA が追加され、ボットやスパムの送信からフォームを保護するためのより多くの選択肢と柔軟性が提供されます。

* **Cloudflare Turnstile**：この摩擦のない CAPTCHA は、明示的なインタラクションを必要としないシンプルなチャレンジを通じてユーザーを検証します。 フォームにシームレスに統合し、ユーザーエクスペリエンスを向上させます。
* **Captcha**：プライバシーに焦点を当てたこの CAPTCHA は、データプライバシーに焦点を当てた、ユーザーフレンドリーな代替手段を提供します。 セキュリティとユーザーエクスペリエンスのバランスを取ることを目的としています。
* **Google reCAPTCHA**: AEM Formsは、信頼性が高く確立されたソリューションを提供することで、reCAPTCHA v2 と reCAPTCHA Enterprise の両方を引き続きサポートします。

AEM Formsでは、複数の CAPTCHA オプションを提供することで、特定のニーズに最適なソリューションを選択できるようになりました。

これらの CAPTCHA ソリューションをアダプティブFormsに統合する準備はできていますか？ アドビのドキュメントでは、次の各項目に関する詳細な手順を提供します。 [Cloudflare Turnstile](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [Captcha](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、および [Google reCAPTCHA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms サービス

Forms サービスは、データキャプチャ用のインタラクティブPDF formsを生成します。 また、既存のインタラクティブPDFフォームとの間でデータの書き出しをインポートし、送信されたデータを検証する場合にも使用できます。 機能の分類を次に示します。

* **Formsのレンダリング**:AEM Forms Designer とオプションで XML データを使用して作成されたテンプレートからインタラクティブPDFフォームを生成します。 これは基本的に、オプションでデータが事前入力された入力可能なPDFフォームを生成します。
* **データの抽出と読み込み**：既存のPDFフォームにデータを読み込むだけでなく、入力済みのPDFフォームからデータを抽出します。 XDP と XML データ形式の両方がサポートされており、非 XFAPDF forms（AcroForms とも呼ばれます）への読み込みには、FDF および XFDF データもサポートされています。
* **データの検証**: AEM Forms Designer を使用して作成されたテンプレートに対して、送信されたデータを XDP 形式または XML 形式で検証します。

>[!IMPORTANT]
>
> 早期導入プログラムに参加して早期導入イノベーションを得たい場合は、公式アドレスからにメールを送信するだけです。 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) アクセスをリクエストします。 すべてまたは特定のイノベーションへのアクセスをリクエストできます。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 他のAdobeソリューションとのAEM統合に対する OAuth サーバー間資格情報のサポート {#S2S-OAuth-credentials}

Adobe Developer コンソールは、様々な API にアクセスするための資格情報を生成するために使用されます。 これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に置き換えて非推奨になりました。AEM Cloud Serviceでは、Adobe AnalyticsやAdobe Targetなど、他のAdobeソリューションとの統合をサポートするようになりました。

[廃止について読む](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) および [AEM オーサー UI の使用方法を学ぶ](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) 他のAdobeソリューションとの統合を設定する場合

### オリジンアラートでのトラフィックスパイク {#traffic-spike-origin}

[事前通知の受信](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) オリジンのトラフィックパターンが DDoS 攻撃を示している場合は、アクションセンターを通じてトラフィックフィルタールールを調査および設定できます。

### RDE の新機能 {#RDE-new-features}

[迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md) 開発者がクラウド内の変更を迅速にデプロイ、レビュー、テストできるようにします。 いくつかの新機能が 6 月の間にロールアウトされます。 また、でAdobeエンジニアリングに直接関与することをお勧めします。 [RDE 不一致チャネル](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート {#rde-frontend}

[RDE でフロントエンドコードがサポートされるようになりました](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) 基準： [サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md) および [サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)早期導入者向け。 RDE の場合、これは [フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

#### RDE のロギングの強化 {#rde-logging}

RDE でコードをデバッグする際に、開発者は次の操作を実行できるようになりました [ログの設定とストリーミングをより生産的に](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)、コマンドラインを使用し、バージョン管理で OSGi プロパティを変更しない。 次のような機能があります。

* パッケージまたはクラスレベルごとのログレベルの宣言
* ログ出力形式のカスタマイズ
* 複数のログの並行ストリーミング

#### RDE CLI の機能強化 {#rde-cli-enhancements}

RDE コマンドラインインターフェイスには、開発者エクスペリエンスを向上させる新機能がいくつか備わっています。

* [setup コマンドはインタラクティブです](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)を使用すると、組織、プログラム、環境を簡単に選択できます。 また、コマンドラインでこれらの値を上書きできるようになりました。
* [クワイエットモード](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) より冗長でない出力の場合。
* [json モード](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) プログラム的に呼び出された際に有用な出力として。

### 新しいアクション センターの通知 {#actions-center-notifications}

[アクション センター](/help/operations/actions-center.md) は、重要なインシデントが発生した場合、またはコードや設定に関してプロアクティブなアクションを実行する必要があるものが検出された場合に、メール通知を送信します。 通知には、次の 3 つの新しいタイプがあります。

* 高度なネットワーク インフラストラクチャを介した発信接続が多すぎます
* 非推奨（廃止予定）のサービスユーザーマッピング形式の使用
* ddos 攻撃の可能性がある

### 早期導入プログラム {#foundation-early-adopter}

電子メール **<aemcs-cdn-config-adopter@adobe.com>**」を選択し、関心のある以下の早期導入プログラムを示します。

#### セルフサービス API キーを使用して CDN でコンテンツをパージする（早期導入プログラム） {#purge-cdn}

CDN パージ API キーをセルフサービス方式で登録し、それを使用して、グローバルまたは 1 つ以上のリソースについて CDN のコンテンツを無効にします。 [詳細情報](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 顧客管理 CDN （BYOCDN）用 X-AEM-Edge-Key のセルフサービス作成（早期導入プログラム） {#byocdn-keys}

以前は、顧客が管理する CDN の設定に必要な X-AEM-Edge-Key を生成するために、サポートチケットが必要でした。 これは、設定パイプラインを使用してデプロイされた設定ファイルを介してセルフサービス方式で実行できるようになり、新しい環境のオンボーディングの遅延をなくすことができます。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### クライアントサイドのリダイレクト（早期導入プログラム） {#client-side-redirects-early-adopter}

ソース管理で 301/302 クライアントサイドのリダイレクトを設定し、CDN にデプロイします。[詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> に関連して既に使用できる機能は他にもいくつかあります [CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)（リクエストと応答の変換、AEM外のサイトへのトラフィックのルーティングを含む）。

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

早期導入プログラムに参加すると、トラフィックフィルタールールがトリガーされるたびにアラートを受け取ることができます。 特定のトラフィック状況が発生するとアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

#### ビジネスユーザーは Git 外でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。これにより、ビジネスユーザーがスプレッドシートまたは UI （ACS Commons リダイレクトマップマネージャーで提供されるものや、顧客アプリケーションの一部として作成されたものなど）を使用してリダイレクトを宣言する機会が開きます。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

Adobeが管理する CDN が、をサポートするようになりました [エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)：エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語です。 ESI スニペットを含めることで、より高い TTL で CDN のHTMLページ全体をキャッシュしながら、より高いケイデンスの更新（低い TTL）を必要とする小さなセクションをオリジンから頻繁に取得できます。 <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

#### Real User Monitoring （RUM）データ・サービス（早期導入プログラム）

* **[RUM （Real Use Monitoring）データ・サービスが GA になりました](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** AEMas a Cloud Service用のクライアントサイドのデータ収集を有効にする。
クライアントサイドコレクションである Real Use Monitoring サービスは、インタラクションをより正確に反映し、web サイトのエンゲージメントを信頼性の高い方法で測定できるようにします。 これにより、ページトラフィックとパフォーマンスに関する高度なインサイトを持つ顧客が可能になります。 ページのパフォーマンスについて詳しく知り、改善するためのインサイトを得る絶好の機会です。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と機能強化の完全なリストを確認できます [こちら](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2404-release/whats-new-2024-04-0).

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます
