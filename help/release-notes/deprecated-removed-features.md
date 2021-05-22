---
title: 非推奨（廃止予定）の機能と削除された機能
description: リリースノート( [!DNL Adobe Experience Manager] の非推奨（廃止予定）の機能と削除された機能) a [!DNL Cloud Service]
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 8c26dbcc77113b86ab28ab52e0b6564fa5ed538a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 48%

---

# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。また、[!DNL Adobe Experience Manager]は[!DNL Cloud Service]としてクラウドネイティブなデプロイメントモデルを提供するので、一部の機能はクラウドネイティブな対応する機能に置き換えられました。

[!DNL Experience Manager]機能の差し迫った削除/置き換えを伝えるために、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上強化されません。
1. 廃止予定と発表された機能は、早ければ後続のメジャーリリースで削除されます。削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、[!DNL Experience Manager]で[!DNL Cloud Service]として非推奨とマークされた機能について説明します。 通常、将来のリリースで削除される機能は、まず非推奨（廃止予定）に設定され、代わりの機能が提供されます。

現在のデプロイメントで機能を使用しているかどうかを確認し、提供される代替機能を使用するように実装を変更する計画を立てることをお勧めします。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| [!DNL Assets] | [!DNL Experience Manager]にアセットを直接アップロードします。[非推奨（廃止予定）のアセットアップロードAPI](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| [!DNL Assets] | ImageMagick などのコマンドラインツールの呼び出しを含め、[ ワークフローの](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)特定のワークフローステップ`DAM Asset Update`はサポートされていません. | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| [!DNL Assets] | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |

## 削除された機能 {#removed-features}

この節では、[!DNL Experience Manager]を[!DNL Cloud Service]として[!DNL Experience Manager]から削除された機能について説明します。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| ユーザーインターフェイス | クラシックUIが製品ユーザーインターフェイスから削除されました。 いくつかのクラシックUIダイアログは、リンクチェッカー、バージョンのパージ、一部のCloud Service設定など、いくつかの選択機能で使用できます。 今後の[製品アップデート](/help/release-notes/home.md)により、クラシックUIの可用性がさらに低下する可能性があります。 | 標準 UI |
| [!DNL Dynamic Media] | [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=ja#integration)と[Dynamic Mediaハイブリッドモード](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=ja#dynamic)との以前の統合は、[!DNL Experience Manager]では[!DNL Cloud Service]として使用できません。 | [!DNL Experience Manager]に付属する[Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)を[!DNL Cloud Service]として使用します。 |
| [!DNL Sites] | Portal Director とポートレットコンポーネント | これらの機能は[!DNL Experience Manager] 6.4で廃止され、[!DNL Experience Manager]から削除されました。 |
| [!DNL Sites] | デザインインポーター | [!DNL Experience Manager]リポジトリの不変セクションは実行時にアクセスできないので、この機能は削除されました。 |
| [!DNL Assets] | [!DNL Assets]Experience Cloud Assets コアサービスおよび Creative Cloud サービスとの の共有は使用できません。 | [!DNL Adobe Creative Cloud]との統合には、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)を使用します。 |
