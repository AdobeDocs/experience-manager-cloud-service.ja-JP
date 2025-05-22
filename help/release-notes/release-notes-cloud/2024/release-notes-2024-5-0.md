---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2024.5.0 リリースのリリースノート。'
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: 8be0a9894bb5b3a138c0ec40a437d6c8e4bc7e25
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2024.5.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager] as a Cloud Service の 2024.5.0 バージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2022年、2023年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)をご覧ください。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.5.0）のリリース日は、2024年5月30日（PT）です。次回の機能リリース（2024.6.0）は 2024年6月27日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

## リリースビデオ {#release-video}

2024.5.0 リリースで追加された機能の概要については、2024年5月リリースの概要ビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Sites の新機能 {#sites-new-features}

#### AEM 翻訳統合 {#translation-integration}

コンテンツ翻訳アクションとワークフローはイベントをトリガーし、外部アプリケーションから関連するプロセスステップと状態を追跡できるようになりました。次のイベントが生成されています。ユーザーは、Adobe Developer Console を使用してイベントを購読できます。

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### 運用上のテレメトリサービス {#real-use-monitoring}

* **[運用上のテレメトリサービスが GA になり](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**AEM as a Cloud Serviceのクライアントサイドのデータ収集が可能になりました。
クライアントサイドのコレクションである実際の使用のモニタリングサービスは、ユーザーインタラクションをより正確に反映し、web サイトのエンゲージメントを信頼性の高い方法で測定できるようにします。これにより、お客様はページのトラフィックとパフォーマンスに関する高度なインサイトを取得できます。ページのパフォーマンスについて詳しく知り、改善するためのインサイトを得る絶好の機会です。

#### Edge Delivery Services 用の AEM オーサリング {#edge-enhancements}

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
* MP4 は、Express の AEM のネイティブ統合（読み込みと書き出し）でサポートされるようになりました。

### アセットビューの新機能 {#assets-view-new-features}

**AEM および Dynamic Media へのアセットの公開**

Experience Manager Assets では、管理ビューに切り替えなくても、アセットビューを使用して [Experience Manager および Dynamic Media にアセットをすばやく公開](/help/assets/publish-assets-to-aem-and-dm.md)できるようになりました。アセットのアップロード、参照および検索時に、アセットを公開できます。

![公開ステータス 1 の確認](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms の新しいプレリリース機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースのアダプティブフォーム用のビジュアルルールエディターの強化

このリリースでは、コアコンポーネントに基づいたアダプティブフォームのビジュアルルールエディターが、大幅にアップグレードされました。次の操作が可能になっています。

* ビジュアルルールエディターでルールを作成して、[デフォルトのフォーム送信の成功／失敗メッセージを上書き](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers)します。

* アダプティブフォームのルールエディターに、[WHEN 操作に対して様々なタイプのフィールドを選択](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)する機能を追加しました。

* フォーム作成者は、[送信前にデータを前処理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)するカスタム関数を適用できるようになりました。

* [**ドラフトとして保存**](/help/forms/save-core-component-based-form-as-draft.md)&#x200B;機能を使用すると、部分的に入力したフォームを後で送信するために保存できます。これは、ユーザーがフォームへの入力を中断し、後で戻る必要があるシナリオで役立ちます。



### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、他のユーザーよりも先に最先端のイノベーションに独占的にアクセスし、その開発に貢献できるユニークな機会を提供します。プログラムを利用すると、複数のイノベーションにアクセスできます。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### ボット保護方法の強化

AEM Forms では、Cloudflare Turnstile と hCaptcha という 2 つの一般的な Captcha ソリューションのサポートを追加して、セキュリティ機能を強化しました。これにより、既に利用可能な Google reCAPTCHA が追加され、ボットやスパムの送信からフォームを保護するためのより多くの選択肢と柔軟性がユーザーに提供されます。

* **Cloudflare Turnstile**：このスムーズな Captcha は、明示的なインタラクションを必要としないシンプルなテストを通じてユーザーを検証します。フォームにシームレスに統合し、ユーザーエクスペリエンスを向上させます。
* **hCaptcha**：プライバシーに焦点を当てたこの Captcha は、データプライバシーに焦点を当てた、ユーザーフレンドリーな代替手段を提供します。セキュリティとユーザーエクスペリエンスのバランスを取ることを目的としています。
* **Google reCAPTCHA**：AEM Forms では、引き続き reCAPTCHA v2 と reCAPTCHA Enterprise の両方をサポートし、信頼性が高く確立されたソリューションを提供します。

AEM Forms では、複数の CAPTCHA オプションを提供して、特定のニーズに最適なソリューションを選択できるようになりました。

これらの Captcha ソリューションをアダプティブフォームに統合する準備はできていますか？アドビのドキュメントでは、[Cloudflare Turnstile](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components)、[hCaptcha](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、[Google reCAPTCHA](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components) の各項目について詳しい手順を示しています。


### Forms サービス

Forms サービスでは、データキャプチャ用のインタラクティブな PDF フォームを生成します。また、これを使用して、既存のインタラクティブ PDF フォームとの間でデータを読み込みまたは書き出したり、送信済みデータを検証したりすることもできます。機能の分類を以下に示します。

* **Forms のレンダリング**：AEM Forms Designer を使用して作成したテンプレートからと、オプションで XML データから、インタラクティブな PDF フォームを生成します。これにより、基本的に、入力可能な PDF フォーム（オプションでデータを事前入力することもできます）が生成されます。
* **データの抽出と読み込み**： 既存の PDF フォームにデータを読み込んだり、入力済みの PDF フォームからデータを抽出したりします。XDP と XML の両方のデータ形式がサポートされ、XFA 以外の PDF フォーム（AcroForms とも呼ばれます）への読み込みでは、さらに FDF および XFDF データもサポートされます。
* **データの検証**：XDP または XML 形式で送信されたデータを、AEM Forms Designer を使用して作成されたテンプレートに対して検証します。

>[!IMPORTANT]
>
> 早期アクセスイノベーションの早期アクセスプログラムへの参加に興味がある方は、公式アドレスから [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) にメールを送信して利用申請してください。すべてのイノベーションまたは特定のイノベーションに対して利用申請できます。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### AEM と他のアドビソリューションとの統合のための OAuth サーバー間資格情報のサポート {#S2S-OAuth-credentials}

Adobe Developer Console は、様々な API にアクセスするための資格情報を生成するために使用されます。これらの資格情報のタイプの 1 つであるサービスアカウント（JWT）資格情報は非推奨（廃止予定）となり、代わりに OAuth サーバー間資格情報が採用されました。AEM Cloud Service では、Adobe Analytics や Adobe Target などの他のアドビソリューションとの統合で OAuth サーバー間資格情報がサポートされるようになりました。

[非推奨（廃止予定）については、こちら](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)を参照し、[AEM オーサー UI の使用方法については、こちら](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)を参照してから、他のアドビソリューションとの統合を設定してください。

### 接触チャネルアラートでのトラフィックスパイク {#traffic-spike-origin}

接触チャネルのトラフィックパターンが DDoS 攻撃を示している場合は、アクションセンターを通じて[プロアクティブな通知を受信](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert)し、トラフィックフィルタールールを調査して設定できます。

### RDE の新機能 {#RDE-new-features}

[迅速な開発環境（RDE）](/help/implementing/developing/introduction/rapid-development-environments.md)を使用すると、開発者はクラウドで変更を迅速にデプロイ、レビュー、テストできます。6 月中にいくつかの新機能がロールアウトされる予定です。また、[RDE ディスコードチャネル](https://discord.com/channels/1131492224371277874/1245304281184079872)では、アドビのエンジニアリングと直接やり取りすることもできます。


#### サイトテーマとサイトテンプレートを使用したフロントエンドコードの RDE サポート {#rde-frontend}

[RDE](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) は、早期導入者向けに、[サイトテーマ](/help/sites-cloud/administering/site-creation/site-themes.md)と[サイトテンプレート](/help/sites-cloud/administering/site-creation/site-templates.md)に基づいたフロントエンドコードをサポートするようになりました。RDE では、[フロントエンドパイプライン](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)ではなくコマンドラインディレクティブを使用して行われます。

#### RDE ロギングの強化 {#rde-logging}

RDE でコードをデバッグする際、バージョン管理で OSGI プロパティを変更することなく、コマンドラインを使用して、開発者が[より生産的にログを設定し、ストリーミング](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging)できるようになりました。次のような機能があります。

* パッケージまたはクラスレベルごとのログレベルの宣言
* ログ出力形式のカスタマイズ
* 複数のログを並行してストリーミング

#### RDE CLI の機能強化 {#rde-cli-enhancements}

RDE コマンドラインインターフェイスには、開発者エクスペリエンスを向上させる新機能がいくつか備わっています。

* [setup コマンドはインタラクティブ](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive)なので、組織、プログラム、環境を簡単に選択できます。また、コマンドラインでこれらの値を上書きできるようになりました。
* [静止モード](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)では、冗長性の低い出力を実現します。
* [jJSON モード](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags)では、プログラムで呼び出すと有用な出力が得られます。

### 新しいアクションセンターの通知 {#actions-center-notifications}

[アクションセンター](/help/operations/actions-center.md)は、重要なインシデントが発生した場合や、コードや設定に関してプロアクティブなアクションを実行する必要がある場合にメール通知を送信します。通知には、次の 3 つの新しいタイプがあります。

* 高度なネットワークインフラストラクチャを介した送信接続が多すぎる
* 非推奨のサービスユーザーマッピング形式の使用
* 潜在的な DDoS 攻撃が進行中

### 早期導入プログラム {#foundation-early-adopter}

以下の早期導入プログラムのどれに興味があるかを明記して、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信してください。

#### セルフサービス API キーを使用して CDN のコンテンツをパージ（早期導入プログラム） {#purge-cdn}

CDN パージ API キーをセルフサービス方式で登録し、これを使用して CDN のコンテンツをグローバルに、または 1 つ以上のリソースに対して無効にします。[詳細情報](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 顧客管理 CDN（BYOCDN）用の X-AEM-Edge-Key のセルフサービス作成（早期導入プログラム） {#byocdn-keys}

以前は、顧客管理 CDN の設定に必要な X-AEM-Edge-Key を生成するには、サポートチケットが必要でした。これにより、設定パイプラインを使用してデプロイされる設定ファイルを通じてセルフサービス方式で実行できるようになり、新しい環境のオンボーディングの遅延がなくなりました。[詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### サーバーサイドのリダイレクト（早期導入プログラム） {#server-side-redirects-early-adopter}

ソース管理で 301/302 サーバーサイドのリダイレクトを設定し、CDN にデプロイします。 [詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. -->リクエストと応答の変換、AEM 外のサイトへのトラフィックのルーティングなど、[CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)に関連して既に利用可能な他の機能がいくつかあります。

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

早期導入プログラムに参加すると、トラフィックフィルタールールがトリガーされるたびにアラートを受け取ることができます。特定のトラフィック状況が発生するとアクションセンターのメール通知が送信されるので、適切な対策を講じることができます。

#### ビジネスユーザーが Git 外部でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache／Dispatcher は、web 階層パイプラインの実行を必要とせずに、公開リポジトリ内の特定の場所に配置された書き換えマップを取り込んで読み込みます。これにより、ビジネスユーザーが、ACS Commons リダイレクトマップマネージャーが提供するようなスプレッドシートまたは UI や顧客アプリケーションの一部として作成するようなスプレッドシートまたは UI を使用して、リダイレクトを宣言できるようになります。<!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含め、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] ガイド {#guides}

* **エクスペリエンスフラグメントへのトピックまたはその要素の公開**
Experience Manager Guiedes を使用すると、トピックまたはその要素をエクスペリエンスフラグメントに公開できるようになりました。エクスペリエンスフラグメントは、コンテンツとレイアウトの両方を統合するモジュール型コンテンツユニットです。エクスペリエンスフラグメントは便利で、一貫性のある魅力的なエクスペリエンスを作成するのに役立ちます。
* **トピックのアセットメタデータをネイティブ PDF 出力に渡す機能**
ネイティブ PDF 出力の生成時に、トピックのアセットメタデータを追加できます。この機能を使用すると、トピックのタイトルや作成者など、様々なトピックの特定のメタデータを、トピックページのヘッダーとフッターに追加できます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)をご覧ください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。
