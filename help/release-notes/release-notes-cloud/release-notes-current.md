---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: の最新のリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 1566963898fb7f6999e3fad796b938128521bcce
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 45%

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
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2024.6.0）のリリース日は 2024年6月27日です。次回の機能リリース（2024.7.0）は 2024年7月25日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Experience Manager Sitesの新機能 {#new-feature-sites}

**RUM （Real Use Monitoring）データ・サービス** {#real-use-monitoring}

この [RUM （Real Use Monitoring）データ・サービス](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) が一般入手可能になり、AEM as a Cloud Serviceのクライアントサイドのデータ収集が可能になりました。 このサービスは、ユーザーのインタラクションをより正確に反映し、web サイトエンゲージメントの信頼性の高い尺度を確保します。 ページトラフィックとパフォーマンスに関する高度なインサイトを顧客に提供し、ページのパフォーマンスを理解して強化する貴重な機会を提供します。

### 早期導入プログラム {#sites-early-adopter}

**バリエーションを生成**

AEM の新機能を通じて GenAI を活用し、[バリエーションを生成](/help/generative-ai/generate-variations.md)し、クラウドサービスでアクセスできるようになりました。バリエーションを生成は、生成 AI を使用してコンテンツの作成を生成し拡張するのに役立ちます。プログラムでの検討については、アドビのアカウントチームにお問い合わせください。

**コンテンツフラグメントコンソールでのアセットのブラウジング**

コンテンツ作成者は、コンテンツフラグメントコンソールを離れることなく、画像やその他のアセットを参照、表示およびアクションを実行できるようになりました。

![アセットブラウジング](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

この機能を試してフィードバックを共有いただける場合早期導入プログラムの詳細をご案内いたしますので、ご自身の正式なメール ID から aemcs-headless-adopter@adobe.com までご連絡ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Experience Manager Assetsの新機能 {#new-features-assets}



**Content Hub**

Content Hubは、組織やビジネスパートナーがオンブランドのコンテンツにアクセスしやすくするために、Experience Manager Assetsas a Cloud Serviceの一部として利用できます。 Content Hubを使用すると、アセットを簡単に見つけて配布したり、ブランド上の新しいバリエーションを再利用および作成したり、大規模にアクティベーションを高速化したりできます。

![Content Hub ユーザーインターフェイス](/help/release-notes/assets/content-hub-ui.png)

**OpenAPI 機能を備えたDynamic Media**

OpenAPI 機能を備えたDynamic Mediaは、Adobeおよびサードパーティアプリケーション全体で DAM を拡張し、アセットセレクターまたは OpenAPI スタックを使用して、あらゆるチャネルでブランド承認済みデジタルアセットにへのアクセスを可能にします。 主要な概念 – バイナリコピーがなく、アセットは高速パフォーマンスのためにエッジで最適化および変換され、アセットをパブリックまたはセキュアで配信します。

![新しいDynamic Mediaのデータフロー図](/help/assets/assets/dm-openapi-dfd.png)


### アセットビューの新機能 {#assets-view-new-features}

**Assets Insights ダッシュボードでは、その他のオプションを利用できます**

アセットタイプおよびサイズ別のアセット数がAssets Insights ダッシュボードで使用できるようになりました。 これらのオプションにより、Assets ビュー環境でリアルタイムデータが提供されます。 サイズ範囲とアセットタイプによって、アセットの数と割合が詳しく示されます。

**埋め込みAdobe Expressエディターの更新**

* 新しいアセットとして保存する場合と新しいバージョンとして保存する場合のユーザーエクスペリエンスが向上しました。

* 複数ページの Express 文書を複数ページのPDFと画像形式の両方でエクスポートすることができます。 画像形式を選択すると、ダウンストリーム配信用に DAM で各ページが個別のアセットとして保存されます。

* アセットの保存中に保存ダイアログでメタデータを追加する機能がサポートされました。

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms の新機能 {#forms-new-prerelease-features}

#### コアコンポーネントベースのアダプティブフォーム用のビジュアルルールエディターの強化

このリリースでは、コアコンポーネントをベースとするアダプティブフォームのビジュアルルールエディターが大幅にアップグレードされました。 次の操作が可能になっています。

* ビジュアルルールエディターでルールを作成して、 [デフォルトのフォーム送信成功/失敗メッセージの上書き](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* アダプティブフォームのルールエディターに、[WHEN 操作に対して様々なタイプのフィールドを選択](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when)する機能を追加しました。

* フォーム作成者は、[送信前にデータを前処理](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server)するカスタム関数を適用できるようになりました。

* [**ドラフトとして保存**](/help/forms/save-core-component-based-form-as-draft.md)&#x200B;機能を使用すると、部分的に入力したフォームを後で送信するために保存できます。この機能は、ユーザーがフォームの入力を中断して後で戻る必要がある場合に役立ちます。

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms早期アクセスプログラムは、誰よりも先に最先端のイノベーションに排他的にアクセスし、その発展を形作るユニークな機会を提供します。 プログラムを利用すると、複数のイノベーションにアクセスできます。

このリリースノートでは、現在のリリースで提供されているイノベーションの一覧を示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### ボット保護方法の強化

AEM Forms では、Cloudflare Turnstile と hCaptcha という 2 つの一般的な Captcha ソリューションのサポートを追加して、セキュリティ機能を強化しました。この機能は、既存のGoogle reCAPTCHA を補完し、ユーザーに追加のオプションを提供します。 これにより、ボットやスパム送信からフォームを保護する柔軟性が向上します。

* **Cloudflare Turnstile**：この摩擦のない CAPTCHA は、明示的なインタラクションを必要としないシンプルなチャレンジを通じてユーザーを検証します。 フォームにシームレスに統合し、ユーザーエクスペリエンスを向上させます。
* **hCaptcha**：プライバシーに焦点を当てたこの Captcha は、データプライバシーに焦点を当てた、ユーザーフレンドリーな代替手段を提供します。セキュリティとユーザーエクスペリエンスのバランスを取ることを目的としています。
* **Google reCAPTCHA**：AEM Forms では、引き続き reCAPTCHA v2 と reCAPTCHA Enterprise の両方をサポートし、信頼性が高く確立されたソリューションを提供します。

AEM Forms では、複数の CAPTCHA オプションを提供して、特定のニーズに最適なソリューションを選択できるようになりました。

アダプティブFormsにこれらの CAPTCHA ソリューションを統合する準備はできていますか？ Adobeのドキュメントでは、次の各項目について詳しい手順を説明しています。 [Cloudflare Turnstile](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [Captcha](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components)、および [Google reCAPTCHA](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Forms サービス

Forms サービスでは、データキャプチャ用のインタラクティブな PDF フォームを生成します。また、これを使用して、既存のインタラクティブ PDF フォームとの間でデータを読み込みまたは書き出したり、送信済みデータを検証したりすることもできます。機能の分類を以下に示します。

* **Forms のレンダリング**：AEM Forms Designer を使用して作成したテンプレートからと、オプションで XML データから、インタラクティブな PDF フォームを生成します。この機能は、オプションでデータが事前入力された入力可能なPDFフォームを生成します。
* **データの抽出と読み込み**： 既存の PDF フォームにデータを読み込んだり、入力済みの PDF フォームからデータを抽出したりします。XDP と XML の両方のデータ形式がサポートされ、XFA 以外の PDF フォーム（AcroForms とも呼ばれます）への読み込みでは、さらに FDF および XFDF データもサポートされます。
* **データの検証**：XDP または XML 形式で送信されたデータを、AEM Forms Designer を使用して作成されたテンプレートに対して検証します。

>[!IMPORTANT]
>
> Adobeの早期アクセスプログラムに参加して早期アクセスのイノベーションを実現することに関心がある場合は、公式アドレスからにメールを送信するだけです。 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) アクセスをリクエストします。 すべてのイノベーションまたは特定のイノベーションに対して利用申請できます。


## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### コンテンツヘルス関連アクションセンター通知早期導入プログラム {#actions-center-notifications}

[アクション センター](/help/operations/actions-center.md) は、重要なインシデントが発生した場合や、プロアクティブなアクションを実行する必要があるコードや設定に関して何かが検出された場合に、メール通知を送信します。 Adobeでは、コンテンツの正常性に関連するいくつかの新しいタイプの通知が導入されました。 この機能は、早期導入プログラムを通じて利用できます。 Adobeカスタマーケアにお問い合わせください。

#### ページに多数のノードが含まれる {#page-nodes}

ノードの数が多いと、レンダリングのパフォーマンスが低下し、ページの読み込み時間が短縮される可能性があります。 ページで大量のノードが検出されると、アクションセンターを通じて事前通知が届きます。これにより、ページ内のノードの合計数を減らすために必要な手順を実行できます。

#### 実行中のワークフローインスタンスの数が多い {#running-workflows}

オーサー環境で実行中のワークフローが多数ある場合は、ワークフローエンジンのパフォーマンスが影響を受けます。 実行中のワークフローインスタンスが多数検出された場合は、アクションセンターから事前通知が届きます。 このプロセスでは、パージジョブを設定して、不要な実行中のワークフローを終了できます。

#### ユーザーがカスタムグループに直接追加されました {#users-customgroups}

ユーザーがカスタムグループに直接追加されると、アクションセンターを通じて事前通知が届きます。 このプロセスを使用すると、関連する IMS グループにユーザーを追加し、それらの IMS グループをAEM グループのメンバーとして含めることで、IMS のベストプラクティスに従うことができます。

#### JCR コンテンツが欠落しています {#jcr-content}

欠落している JCR コンテンツが検出されると、アクションセンターは事前に通知します。 このアプローチにより、欠落しているコンテンツを追加し、特定のAEM Assets機能のエラーを防ぐことができます。

#### 完了したワークフローがパージされない {#workflows}

完了したワークフローが 90 日以上経過してもパージされていないことが、事前にアクションセンターから通知されます。 このアプローチは、ワークフローインスタンスの数を減らすことで、ワークフローエンジンのパフォーマンスを向上させるのに役立ちます。

#### Sling リソースがありません {#sling-resource}

欠落している Sling リソースが検出されると、アクションセンターは事前に通知します。 このアプローチにより、不足しているリソースを追加し、特定のAEM Assets機能のエラーを防ぐことができます。

### コンテンツ配信関連の早期導入プログラム {#foundation-early-adopter}

以下の早期導入プログラムのどれに興味があるかを明記して、**<aemcs-cdn-config-adopter@adobe.com>** にメールを送信してください。

#### CDN での基本認証（早期導入プログラム） {#basicauth-cdn}

ユーザー名とパスワードの入力を求める基本認証ダイアログを表示して、特定のコンテンツリソースを保護します。この機能は、エンドユーザーのアクセス権に対する包括的なソリューションとしてではなく、主にビジネス関係者がコンテンツをレビューするような、認証の軽いユースケースを対象としています。 秘密鍵タイプのCloud Manager環境変数への参照を使用して、設定パイプラインを介してデプロイされた Git の設定ファイルを通じて管理されるのユーザー名とパスワードのリスト。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth)。

#### セルフサービス API キーを使用して CDN でコンテンツをパージする（早期導入プログラム） {#purge-cdn}

CDN パージ API キーをセルフサービス方式で登録し、これを使用して CDN のコンテンツをグローバルに、または 1 つ以上のリソースに対して無効にします。[詳細情報](/help/implementing/dispatcher/cdn-cache-purge.md)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### 顧客管理 CDN （BYOCDN）用 X-AEM-Edge キーのセルフサービス作成（早期導入プログラム） {#byocdn-keys}

以前は、顧客管理 CDN の設定に必要な X-AEM-Edge-Key を生成するには、サポートチケットが必要でした。この結果は、設定パイプラインを使用してデプロイされた設定ファイルを介してセルフサービス方式で実行できるようになり、新しい環境のオンボーディングの遅延をなくすことができます。 [詳細情報](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value)。

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### クライアントサイドのリダイレクト（早期導入プログラム） {#client-side-redirects-early-adopter}

ソース管理で 301/302 クライアントサイドのリダイレクトを設定し、CDN にデプロイします。[詳細情報](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)。<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. -->リクエストと応答の変換、AEM 外のサイトへのトラフィックのルーティングなど、[CDN 設定](/help/implementing/dispatcher/cdn-configuring-traffic.md)に関連して既に利用可能な他の機能がいくつかあります。

#### トラフィックフィルタールールアラート（早期導入プログラム） {#traffic-filter-rules-alerts-early-adopter}

最近リリースされた[トラフィックフィルタールール](/help/security/traffic-filter-rules-including-waf.md)には、オプションでライセンス可能な web アプリケーションファイアウォール（WAF）ルールが含まれており、許可または拒否するトラフィックを設定できます。

早期導入プログラムに参加すると、トラフィックフィルタールールがトリガーされるたびにアラートを受け取ることができます。アクションセンターメール通知では、特定のトラフィック条件が発生した場合に情報が保持されるので、適切な対策を講じることができます。

#### ビジネスユーザーは Git 外でリダイレクトを宣言できる（早期導入プログラム） {#apache-rewritemaps-early-adopter}

AEM 6.5 と同様に、Apache/Dispatcher は、パブリッシュリポジトリーの特定の場所に配置された書き換えマップを取り込んで読み込みます。web 層パイプラインを実行する必要はありません。 このアプローチを使用すると、ビジネスユーザーはスプレッドシートや UI （ACS Commons リダイレクトマップマネージャーやカスタムアプリケーションなど）を使用してリダイレクトを宣言できます。 <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### 動的コンテンツを読み込むためのエッジサイドインクルード（ESI）（早期導入プログラム） {#esi-early-adopter}

アドビが管理する CDN で、エッジレベルの動的 web コンテンツアセンブリ用のマークアップ言語である[エッジサイドインクルード（ESI）](/help/implementing/dispatcher/edge-side-includes.md)がサポートされるようになりました。ESI スニペットを含め、より大きい TTL で HTML ページ全体を CDN にキャッシュしながら、より頻繁なアップデート（小さい TTL）を必要とする小さなセクションを、接触チャネルから頻繁に取得できます。<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0)を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## 移行ツール {#migration-tools}

移行ツールのリリースの完全なリストは、[こちら](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)で確認できます

## ユニバーサルエディター {#universal-editor}

ユニバーサルエディターのリリースの完全なリストを確認できます [こちら](/help/release-notes/universal-editor/current.md).

## バリエーションの生成 {#generate-variations}

バリエーションを生成リリースの完全なリストを見つけることができます [こちら](/help/generative-ai/release-notes-generate-variations.md).

## Experience Cloud のリリースノート {#experience-cloud}

他の Experience Cloud アプリケーションのリリースについて詳しくは、[こちら](https://experienceleague.adobe.com/ja/docs/release-notes/experience-cloud/current)を参照してください。
Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。