---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service の最新のリリースノート。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: bbf66195593032eb2ccf073ec78685c9d9726235
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 84%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下のセクションでは、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンの機能リリースノートの概要について説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2023年、2024年）のリリースノートに移動できます。
>
>[!DNL Experience Manager] as a Cloud Service の今後の機能のアクティベーションについての詳細は、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)をご覧ください。

>[!NOTE]
>
>Experience Cloud リリースノートの更新に関するメール通知を毎月受信するには、[アドビ製品アップデートの優先通知](https://www.adobe.com/subscription/priority-product-update.html)を購読してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新の機能リリース（2025.3.0）のリリース日は、2025年3月27日（PT）です。次回の機能リリース（2025.4.0）は 2025年4月24日（PT）に予定されています。

## メンテナンスリリースノート {#maintenance}

最新のメンテナンスリリースノートについては、[こちら](/help/release-notes/maintenance/latest.md)をご覧ください。

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media の新機能 {#new-features-dynamic-media}

**Open API を備えた Dynamic Media で配信されるビデオのロングフォームのサポート**

OpenAPI を備えた Dynamic Media で、ロングフォームのビデオがサポートされるようになりました。長形式のビデオは、最大 50 GB と 2 時間をサポートできます。

### Dynamic Media Classic {#dmc}

<!-- CARRY OVER TO APRIL 2025 RELEASE NOTES -->

2025 年 4 月リリースより、Dynamic Media Classic レポートダッシュボードの「帯域幅」タブはサポートされなくなりました。

[ 帯域幅とストレージ、レポートのタイプ ](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports) を参照してください。


## アセットビューの新機能 {#new-features-assets-view}


**ルートタグのサポート**

AEM Assets では、カスタムメタデータへのメタデータフォームのタグプロパティのマッピングがサポートされるようになりました。さらに、管理者は、特定のルートタグと、このルートタグの下に存在するタグへのアクセスを制限して、ユーザーに対するタグの可用性を制限できます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### AEM Forms の早期アクセス機能 {#forms-new-early-access-features}

AEM Forms 早期アクセスプログラムでは、最先端のイノベーションに排他的にアクセスし、その開発に貢献できるユニークな機会を提供します。

このリリースノートでは、現在のリリースで提供されるイノベーションのリストを示します。 早期アクセスプログラムで利用可能なイノベーションの完全なリストについては、[AEM Forms 早期アクセスプログラムのドキュメント](/help/forms/early-access-ea-features.md)を参照してください。

#### アダプティブフォームの HTML メールテンプレート

アダプティブフォームでは、[HTML メールテンプレート](/help/forms/html-email-templates-in-adaptive-forms.md)を使用できます。HTML メールテンプレートを使用すると、フォームの送信時に、リッチでパーソナライズされた、魅力的な外観のメールを送信できます。これらのメールは、フォームデータでカスタマイズしたり、画像やリンクなどの様々なメールタグを使用して強化したりできます。アダプティブフォームでは、HTML テンプレートを含むファイルをアップロードするか、プレーンテキストエディターを使用してこれらのテンプレートを作成できます。

![HTML メールテンプレート](/help/forms/assets/html-email.png)

#### クラウドストレージのサポートの強化：Azure Blob Storage への直接 PDF アップロード

AEM Forms Document Generation API を使用すると、Azure Blob ストレージに [ 生成されたPDF ドキュメントを直接アップロード ](/help/forms/early-access-ea-features.md#doc-generation-api) できるようになりました。 この機能強化により、ストレージと取得が合理化され、効率の向上やクラウドワークフローとの統合が促進されます。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### Java 21 サポート {#java21}

1 月リリースの時点で、Java 21 および Java 17 を使用してコードをビルドできます。 パターンマッチング、密封クラス、様々なパフォーマンス向上などの新機能にアクセスできます。 Maven プロジェクトとライブラリのバージョンの更新など、設定手順については、[ ビルド環境 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) の記事を参照してください。

Java 17 または 21 ビルドが検出されると、よりパフォーマンスの高い Java 21 **runtime** が自動的にデプロイされます。 ただし、Adobeでは、Java 11 でビルドされた環境の場合は、[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) に電子メールで Java 21 ランタイムをオプトインすることをお勧めします。 [Java 21 ランタイム要件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)について説明します。

>[!IMPORTANT]
>
> Java 21 **ランタイム** は、2 月に開発環境/RDE 環境にデプロイされました。これは、**4 月 28 日と 29 日** にステージ環境/実稼動環境に適用されます。 Java 21（または Java 17）を使用した&#x200B;**コードのビルド**&#x200B;は、Java 21 ランタイムとは独立しています。Java 21（または Java 17）でコードをビルドする手順を明示的に実行する必要があります。

### その他の宛先へのAEM ログ転送 - ベータ版プログラム {#log-forwarding-earlyadopter}

現在のベータ版では、AEM ログを New Relic（HTTPS を使用）、Amazon S3、Sumo Logic に転送できます。AEM ログ（Apache／Dispatcher を含む）はサポートされていますが、CDN ログはサポートされていません。アクセスについて詳しくは、[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) までメールで送信してください。

ログは Cloud Manager からダウンロードできますが、多くの組織では、これらのログを優先されるログの宛先にストリームすると役立ちます。AEM では既に、Azure Blob Storage、Datadog、HTTPS、Elasticsearch（および OpenSearch）、Splunk への AEM および CDN ログ転送（GA）をサポートしています。この機能は、セルフサービス方式で設定し、設定パイプラインを使用してデプロイします。

詳しくは、[ログ転送ドキュメント](/help/implementing/developing/introduction/log-forwarding.md)を参照してください。

### Edge コンピューティング - フィードバックのリクエスト {#edge-computing-feedback}

Edge コンピューティングには、データ処理がブラウザーに近づくので、待ち時間が短縮されるなどのメリットがあります。 このテクノロジーが AEM の配信を公開および Edge Delivery Services プロジェクトに役立つかどうかについて、ぜひお聞かせください。さらに、製品ロードマップへのインプットとして、お客様が何を想定されるかをお教えください。

いくつかの考えられるユースケース：

* コンテンツへのアクセスをゲートする IdP を使用した認証
* 位置情報、デバイスタイプ、ユーザー属性などに基づく動的（パーソナライズされ、ローカライズされた）コンテンツのレンダリング。
* 高度な画像操作
* CDN とオリジンの間のミドルウェア
* ブラウザーとサードパーティ API の間のレイヤー（API 応答の再フォーマット用など）
* クライアントブラウザーでレンダリングしやすくする、複数のオリジンからのデータの集計

ご質問やご意見がある場合は、[aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) までメールで送信してください。

### OpenAPI ベースの API - 早期導入プログラム {#open-apis-earlyadopter}

開発者は、AEM as Cloud Service の機能を独自のアプリケーションやツールに深く統合できます。 新しい AEM as a Cloud Service API は、OpenAPI 仕様に従い、一貫性の確保、明確な文書化、使いやすさを目標とします。認証を必要とするエンドポイントの資格情報は、Adobe Developer Console プロジェクトを作成することによって生成されます。

詳しくは、[OpenAPI ベースの AEM API](/help/implementing/developing/open-api-based-apis.md) を参照し、設定と使用方法を説明した[エンドツーエンドチュートリアル](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s)を試してください。

具体的には、以下に示す API エンドポイントが早期導入プログラムの一部として使用可能です。 興味がある場合は、どのように活用する予定かを記載したメールを [aem-apis@adobe.com](mailto:aem-apis@adobe.com) まで送信してください。

* [Sites Content Fragments API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [Assets API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [Sites and Assets Folders API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [Forms Communications API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### 新しい AEM Developer Console（パブリックベータ版） {#aem-developer-console-beta}

クラウド環境でのコードのデバッグに対して、よりインタラクティブなエクスペリエンスを提供する、刷新された [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) を試してください。

現在の AEM Developer Console の「*新しいコンソールが使用可能*」ボタンをクリックすると、誰でもパブリックベータ版にアクセスできます。 アドビでは、フィードバックを大切にしています。[aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com) までメールで送信してください。

## [!DNL Experience Manager] ガイド {#guides}

Adobe Experience Manager Guides の最新リリースの新機能と強化機能の完全なリストについては、[こちら](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2025-releases/2502-release/whats-new-2025-02-0)を参照してください。

<!-- THE FOLLOWING URL WAS USED ABOVE BUT IT WAS 404. IT WAS REPLACED WITH THE URL ABOVE 
(https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0). -->

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
