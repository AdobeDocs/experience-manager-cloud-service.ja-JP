---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 20476 {#20476}

2025年4月15日（PT）に公開された、メンテナンスリリース 20476 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 20133 でした。

2025.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20476}

* CNTBF-411：JCR でドロップした場合に Sling ジョブを削除する可能性を追加。
* CQ-4359813：AEM 翻訳キット：3月20日（PT）。
* CQ-4359811：Granite 翻訳キット：3月20日（PT）。
* GRANITE-57863：FileVault をバージョン 3.8.4 にアップデート。
* GRANITE-56154：oak-segment-azure で指数関数的再試行を設定。
* GRANITE-55999：UserPropertiesService のパフォーマンスを向上。
* GRANITE-55781：ユーザーメンバーシップの冗長な再設定を回避。
* GRANITE-53956：oak-segment-azure の Azure SDK V8 を V12 にアップグレード。
* GRANITE-50654：「プリンシパル権限」タブで、フロントエンドの「すべてのユーザー」の読み込みをデフォルトで削除。
* SKYOPS-103444：Sling ResourceResolver 1.12.6 にアップデート。
* SKYOPS-101147：caconfig 実装をアップデート。
* SKYOPS-97124：SPIFly バンドルの古いバージョンに対するアナライザー警告を追加。
* SKYOPS-95826：ランタイム Java バージョンを 11.0.26 および 21.0.6 にアップデート。
* SKYOPS-53671：（RDE）AEM の再起動時に機能モデルから顧客がインストールしたアーティファクトを使用。

### 修正された問題 {#fixed-issues-20476}

* ASSETS-49027：[回帰] AemRequestEventFilter により、OSGI web コンソールへの POST リクエストが中断される。
* ASSETS-44956：Dynamic Media レンディションを選択できない - スクリプトタグは上位レベルのコンポーネントに読み込む必要がある。
* CNTBF-410：ContentCopy バンドルの CheckJob getId が null ポインタである。
* CNTBF-341：ContentCopy 書き出しのインデックスが範囲外である。
* CQ-4355411：ツールチップが「ユーザーの環境設定」ダイアログに表示されたままになる。
* GRANITE-57265：ドロップダウン選択値が選択されない。
* GRANITE-57067 - UI に効果的なポリシーが欠落している。
* SITES-30727：AEM エディター内のサブコンポーネントのドラッグ＆ドロップが失敗する場合がある。
* SKYOPS-90607：Sling ジョブが非アクティブなデプロイメント／可変コンテンツで実行される。
* SKYOPS-95722：AEM-SDK のクイックスタートフラグから `MaxPermSize` サイズが削除される。
* SKYOPS-103569：特定の画像が Java 21 で読み込めない：`javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`。

### 既知の問題 {#known-issues-20476}

なし。

### 廃止された機能と API {#deprecated-20476}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-20476}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 5 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-20476}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.28.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
