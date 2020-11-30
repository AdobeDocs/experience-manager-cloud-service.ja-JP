---
title: 非推奨（廃止予定）の機能と削除された機能
description: リリースノート（Adobe Experience Manager as a Cloud Service の非推奨（廃止予定）の機能と削除された機能）
translation-type: tm+mt
source-git-commit: 0a9a462f1b92a0dcb712163574bbf57582f8145c
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 100%

---


# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。また、Adobe Experience Manager as a Cloud Service はクラウドネイティブなデプロイメントモデルを提供するので、一部の機能はクラウドネイティブな同等機能に置き換わりました。

近い将来おこなわれる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上改善されません。
1. 廃止予定と発表された機能は、早ければ後続のメジャーリリースで削除されます。削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

ここでは、Adobe Experience Manager as a Cloud Service で廃止予定の機能について説明します。通常、将来のリリースで削除が予定される機能は、まず非推奨（廃止予定）とされ、代替手段が提示されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| Assets | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| Assets | AEM へのアセットの直接アップロード。[非推奨（廃止予定）のアセットアップロード API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| Assets | ImageMagick などのコマンドラインツールの呼び出しを含め、[ ワークフローの](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)特定のワークフローステップ`DAM Asset Update`はサポートされていません。 | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| Assets | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |

## 削除された機能 {#removed-features}

ここでは、Adobe Experience Manager as a Cloud Service から削除された機能について説明します。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| UI | （リンクチェッカー、バージョンパージ、一部の Cloud Services 設定など）いくつかの選択機能については、一部のクラシック UI ダイアログが当面そのまま残りますが、一般的なクラシック UI へのアクセスは AEM 製品 UI から削除されました。 | 標準 UI |
| Dynamic Media | [Dynamic Media Classic（Scene7）](https://helpx.adobe.com/jp/experience-manager/6-5/sites/administering/using/scene7.html)および [Dynamic Media Hybrid モード](https://helpx.adobe.com/jp/experience-manager/6-5/assets/using/config-dynamic.html)とのこれまでの統合は、AEM as a Cloud Service では使用できません。 | Adobe Experience Manager as a Cloud Service で提供される [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) を使用します。 |
| Sites | Portal Director とポートレットコンポーネント | これらの機能は AEM 6.4 で非推奨（廃止予定）となり、現在は AEM から削除されています。 |
| Sites | デザインインポーター | 実行時に AEM リポジトリの不変セクションにアクセスできないので、この機能は削除されました。 |
| Assets | [Experience Cloud Assets コアサービスおよび Creative Cloud サービスとの AEM Assets の共有](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/configure-assets-cc-integration.html)は使用できません。 | Creative Cloud との統合には、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) を使用します。 |
