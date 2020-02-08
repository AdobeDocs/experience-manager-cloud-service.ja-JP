---
title: 廃止および削除された機能
description: クラウドサービスとしてのAdobe Experience Managerの廃止および削除された機能に固有のリリースノートです。
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Deprecated and removed features {#deprecated-and-removed-features}

アドビは、製品の機能を常に評価し、長期的には古い機能をより最新の代替手段に置き換えて、全体的な顧客価値を向上させ、常に下位互換性を慎重に検討します。 また、クラウドサービスとしてのAdobe Experience Managerは、クラウドネイティブの展開モデルを提供するので、一部の機能と機能はクラウドネイティブの機能に置き換えられました。

近い将来おこなわれる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. 廃止の発表がまずおこなわれます。非推奨の機能は引き続き使用できますが、それ以上拡張されません。
1. 非推奨と発表された機能は、後続のメジャーリリースでは早くとも削除されます。 削除の実際の目標日が通知されます。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## Deprecated features {#deprecated-features}

ここでは、Experience Managerでクラウドサービスとして非推奨としてマークされた機能について説明します。 通常、将来のリリースで削除される予定の機能は、代替手段として提供され、非推奨に設定されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| Assets | アセットの取り込みと処理でワークフローが使用されなくな `DAM Asset Update` った | アセットの取り込みで、現在はア [セットマイクロサービス](/help/assets/asset-microservices-overview.md) を使用します。 |
| Assets | アセットをAEMに直接アップロード — 非推奨のアセットア [ップロードAPIを参照](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [直接バイナリアップロードは](/help/assets/add-assets.md) 、Experience Managerでクラウドサービスとして使用されます。 技術的な詳細については、直接アップロ [ードAPIを参照してください](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。 |
| Assets | [ImageMagickなどのコマンドラインツ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)`DAM Asset Update` ールの呼び出しなど、ワークフローの特定のワークフロー手順はサポートされていません | [Asset Microservicesは](/help/assets/asset-microservices-overview.md) 、多くのワークフローの代替機能です。 カスタム処理の場合は、後処理 [ワークフローを使用します](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |

## Removed features {#removed-features}

ここでは、Experience Managerをクラウドサービスとして使用するAEMから削除された機能について説明します。

| 領域 | 機能 | 代替手段 |
| ------------ | ------------------ | ----------- |
| UI | 一部のクラシックUIダイアログは、リンクチェッカー、バージョンの削除、一部のクラウドサービス設定など、いくつかの選択機能に対して当面の間残りますが、一般的なクラシックUIへのアクセスはAEM製品UIで削除されました。 | 標準 UI |
| Dynamic Media | AEMでは、 [Dynamic Media Classic(Scene7)および](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) Dynamic Media Hybridモードとの以前の統合は [](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) 、クラウドサービスとして使用できません。 | Experience Managerで提供さ [れる](/help/assets/dynamic-media/dynamic-media.md) Dynamic Mediaをクラウドサービスとして使用します。 |
| Sites | ポータル・ダイレクタおよびポートレット・コンポーネント | これらの機能はAEM 6.4で廃止され、AEMから削除されました。 |
| Sites | デザインインポーター | この機能は、AEMリポジトリの不変セクションが実行時にアクセスできないので削除されました。 |
| Assets | [Marketing Cloud AssetsコアサービスおよびCreative cloudサービスとのAEM Assets共有は](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) 、使用できません。 | Creative cloudとの統合には、 [Adobe Asset Linkを使用します](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)。 |
