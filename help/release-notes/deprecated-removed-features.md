---
title: 非推奨（廃止予定）の機能と削除された機能
description: ' [!DNL Adobe Experience Manager] 内の非推奨機能および削除された機能に固有のリリースノート（a1/>として）です。 [!DNL Cloud Service]'
translation-type: tm+mt
source-git-commit: e6ad571b7428f6fb7a11907e752ba670a722057c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 49%

---


# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。また、[!DNL Adobe Experience Manager]は[!DNL Cloud Service]と同様に、クラウドとネイティブの展開モデルを提供するので、一部の機能と機能は、対応するクラウドネイティブの機能に置き換えられました。

[!DNL Experience Manager]機能の差し迫った削除/交換を伝えるには、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨の機能は引き続き利用できますが、それ以上強化されません。
1. 廃止予定と発表された機能は、早ければ後続のメジャーリリースで削除されます。削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

このセクションのリストは、[!DNL Experience Manager]で[!DNL Cloud Service]として非推奨とマークされた機能と特徴を示しています。 通常、将来のリリースで削除される機能は、非推奨となるように最初に設定されますが、代わりの機能も提供されます。

お客様は、現在の導入で機能や機能を使用しているかどうかを確認し、提供される代替機能を使用するように導入を変更する計画を立てることをお勧めします。

| 機能 | 非推奨（廃止予定）の機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | 取り込んだ画像を処理する `DAM Asset Update` ワークフロー | 現在は、アセットの取り込みで[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が使用されています。 |
| [!DNL Assets] | アセットを[!DNL Experience Manager]に直接アップロードします。[非推奨のアセットアップロードAPI](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)を参照してください。 | [直接バイナリアップロード](/help/assets/add-assets.md)を使用。技術的な詳細については、[直接アップロード API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください。 |
| [!DNL Assets] | ImageMagick などのコマンドラインツールの呼び出しを含め、[ ワークフローの](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)特定のワークフローステップ`DAM Asset Update`はサポートされていません. | [アセットマイクロサービス](/help/assets/asset-microservices-overview.md)が多くのワークフローの代替機能となります。カスタム処理の場合は、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用します。 |
| [!DNL Assets] | ビデオの FFmpeg トランスコード。 | FFmpeg サムネールの生成には、[アセットマイクロサービス](/help/assets/asset-microservices-overview.md)を使用。FFmpeg トランスコードの場合は、[Dynamic Media](/help/assets/manage-video-assets.md) を使用。 |

## 削除された機能 {#removed-features}

このセクションのリストは、[!DNL Experience Manager]から[!DNL Experience Manager]を[!DNL Cloud Service]として削除された機能と特徴を示しています。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| ユーザーインターフェイス | クラシックUIが製品のユーザーインターフェイスから削除されました。 いくつかの選択機能(リンクチェッカー、Cloud Serviceの削除、一部のバージョン設定など)で使用できるクラシックUIダイアログがいくつかあります。 今後の[製品のアップデート](/help/release-notes/home.md)により、従来のUIがさらに削除される可能性があります。 | 標準 UI |
| [!DNL Dynamic Media] | [Dynamic Mediaクラシック](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=ja#integration)および[Dynamic Mediaハイブリッドモード](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=ja#dynamic)との以前の統合は、[!DNL Experience Manager]では[!DNL Cloud Service]として使用できません。 | [!DNL Experience Manager]に付属の[Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)を[!DNL Cloud Service]として使用します。 |
| [!DNL Sites] | Portal Director とポートレットコンポーネント | これらの機能は[!DNL Experience Manager] 6.4で廃止され、[!DNL Experience Manager]から削除されました。 |
| [!DNL Sites] | デザインインポーター | この機能は、[!DNL Experience Manager]リポジトリの不変セクションが実行時にアクセスできないため、削除されました。 |
| [!DNL Assets] | [[!DNL Assets] Experience Cloud Assets コアサービスおよび Creative Cloud サービスとの の共有](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/integration/configure-assets-cc-integration.html)は使用できません。 | [!DNL Adobe Creative Cloud]との統合には、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)を使用します。 |
