---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 50%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 20476 {#20476}

2025年4月15日（PT）に公開された、メンテナンスリリース 20476 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 20133 でした。

2025.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-20476}

* CNTBF-411:JCR によって削除された場合に、Sling ジョブを削除できる機能を追加しました。
* CQ-4359813:AEM翻訳キット：3 月 20 日（PT）。
* CQ-4359811:Granite 翻訳キット：3 月 20 日（PT）。
* GRANITE-57863：FileVault をバージョン 3.8.4 にアップデート。
* GRANITE-56154:oak-segment-azure での指数関数的再試行を設定します。
* GRANITE-55999:UserPropertiesService のパフォーマンスを向上させます。
* GRANITE-55781：ユーザーメンバーシップの冗長な再設定を避けます。
* GRANITE-53956:oak-segment-azure の Azure SDK V8 を V12 にアップグレードします。
* GRANITE-50654:「プリンシパル権限」タブで、フロントエンドの「everyone」の読み込みをデフォルトで削除します。
* SKYOPS-103444：Sling ResourceResolver 1.12.6 にアップデート。
* SKYOPS-101147:caconfig impl を更新します。
* SKYOPS-97124:SPIFly バンドルの古いバージョンに対するアナライザーの警告を追加しました。
* SKYOPS-95826：ランタイム Java バージョンを 11.0.26 および 21.0.6 に更新します。
* SKYOPS-53671: （RDE）AEMの再起動時に、機能モデルからカスタムでインストールしたアーティファクトを使用します。

### 修正された問題 {#fixed-issues-20476}

* ASSETS-49027:[ リグレッション ]AemRequestEventFilter が、OSGI web コンソールへの POST リクエストを中断します。
* ASSETS-44956:Dynamic Media レンディションを選択できません – スクリプトタグは、トップレベルコンポーネントに読み込む必要があります。
* CNTBF-410: ContentCopy バンドル内の CheckJob getId null ポインター。
* CNTBF-341: ContentCopy エクスポート インデックスが範囲外です。
* CQ-4355411：ツールチップが「ユーザーの環境設定」ダイアログに表示されたままになる。
* GRANITE-57265：ドロップダウン選択値が選択されない。
* GRANITE-57067 - UI に有効なポリシーがありません。
* SITES-30727：AEM エディター内のサブコンポーネントのドラッグ＆ドロップが失敗する場合がある。
* SKYOPS-90607:Sling ジョブが、非アクティブなデプロイメント/可変コンテンツで実行される。
* SKYOPS-95722:AEM-SDK`MaxPermSize` クイックスタートフラグからサイズを削除します。
* SKYOPS-103569:Java 21 で読み込めない画像があります：`javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`。

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
