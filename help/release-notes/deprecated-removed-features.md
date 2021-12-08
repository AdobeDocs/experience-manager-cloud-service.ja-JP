---
title: 廃止される機能および削除された機能
description: リリースノート（ [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の非推奨（廃止予定）の機能と削除された機能）。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 9410b061278d916c95233ecba7f7f946fccc51ed
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 96%

---

# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service の非推奨（廃止予定）の機能と削除された機能"
>abstract="AEM as a Cloud Service には、クラウドネイティブなデプロイメントモデルがあります。一部の機能や特徴は、クラウドネイティブな同等機能に置き換えられました。ここでは、それらの機能を示します。"


アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。また、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] はクラウドネイティブなデプロイメントモデルを提供するので、一部の機能はクラウドネイティブな同等機能に置き換わりました。

近い将来行われる [!DNL Experience Manager] 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表が行われます。廃止される機能は引き続き使用できますが、それ以上改善されません。
1. 廃止予定と発表された機能は、早ければ後続のメジャーリリースで削除されます。削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

ここでは、[!DNL Experience Manager] as a [!DNL Cloud Service] で廃止予定の機能について説明します。通常、将来のリリースで削除が予定される機能はまず廃止対象として代替手段が提示されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | のエクスペリエンスフラグメントプロパティ **ソーシャルメディアのステータス**. | 機能は間もなく削除されます。 |
| [!DNL Sites] | テンプレートベースのシンプルなコンテンツフラグメント。 | [モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md) 今すぐ。 |
| [!DNL Assets] | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| [!DNL Assets] | [!DNL Experience Manager] へのアセットの直接アップロード。[非推奨（廃止予定）のアセットアップロード API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| [!DNL Assets] | [!DNL ImageMagick] などのコマンドラインツールの呼び出しを含め、`DAM Asset Update` ワークフローの[特定のワークフローステップ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)はサポートされていません。 | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| [!DNL Assets] | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |
| [!DNL Foundation] | レプリケーションエージェントの「配布」タブのツリーレプリケーション UI（2021 年 9 月 30 日以降に削除） | [公開を管理](/help/operations/replication.md#manage-publication)または[コンテンツツリーの公開ワークフロー](/help/operations/replication.md#publish-content-tree-workflow)アプローチ |

## 削除された機能 {#removed-features}

ここでは、[!DNL Experience Manager] as a [!DNL Cloud Service] の導入で [!DNL Experience Manager] から削除された機能の一覧を示します。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| ユーザーインターフェイス | クラシック UI が製品ユーザーインターフェイスから削除されました。いくつかのクラシック UI ダイアログは、リンクチェッカー、バージョンパージ、一部の Cloud Service 設定など、いくつかの機能で使用できます。今後の[製品アップデート](/help/release-notes/home.md)により、クラシック UI の利用範囲がさらに狭まる可能性があります。 | 標準 UI |
| [!DNL Dynamic Media] | [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=ja#integration) および [Dynamic Media Hybrid モード](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=ja#dynamic)との従来の統合は、[!DNL Experience Manager] as a [!DNL Cloud Service] では使用できません。 | [!DNL Experience Manager] as a [!DNL Cloud Service] に用意されている [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) を使用します。 |
| [!DNL Sites] | Portal Director とポートレットコンポーネント | これらの機能は [!DNL Experience Manager] 6.4 で非推奨（廃止予定）となり、現在は [!DNL Experience Manager] から削除されています。 |
| [!DNL Sites] | デザインインポーター | 実行時に [!DNL Experience Manager] リポジトリーの不変セクションにアクセスできないので、この機能は削除されました。 |
| [!DNL Assets] | [!DNL Assets]Experience Cloud Assets コアサービスおよび Creative Cloud サービスとの の共有は使用できません。 | [!DNL Adobe Creative Cloud] との統合には、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) を使用します。 |
| [!DNL Foundation] | Apache Sling データソース（OSGi バンドル org.apache.sling.datasource）のサポート。 | 該当なし |

## Java API {#java-api}

非推奨（廃止予定）の Java API や削除された Java API については、[このページ](/help/release-notes/deprecated-apis.md)を参照してください。

## OSGi 設定 {#osgi-configuration}

OSGi プロパティの設定に関する制限事項（一部は将来的に導入される可能性もあります）については、[この記事](/help/implementing/deploying/osgi-configuration-api.md)を参照してください。
