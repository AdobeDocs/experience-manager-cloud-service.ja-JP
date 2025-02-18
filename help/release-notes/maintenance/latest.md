---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 49%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 19567 {#19567}

2025年2月18日に公開された、メンテナンスリリース 19567 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 19352 でした。

2025.2.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-19567}

* GRANITE-56650：コンテンツ配信は、数回再試行した後にのみ、ブロックされたキューを通知する必要があります
* SKYOPS-89616:Adobe Developer Consoleで最大 40 個のテクニカルアカウントを作成できます

### 修正された問題 {#fixed-issues-19567}

* CNTBF-232：必須の jcr:content 子を含めるディープパッケージ nt:file ノード
* CQ-4358930：多数のマルチフィールドを含むページプロパティの読み込み中のパフォーマンスの問題
* GRANITE-55960:AEM as Cloud Serviceの Coral Select フィールドに関するパフォーマンスの問題
* GRANITE-56197：新しい TreeActivation ワークフローステップで、大きなフラットフォルダー構造のアセットがバッチ化されない

#### AEM ガイド {#guides}

* GUIDES-23526：フォルダープロファイルから条件を更新すると、すべての条件グループが失われ、条件が統合されます。
* GUIDES-22574：外部リンクに UUID が含まれている場合、後処理に進み、外部リンクを UUID リンクに変換すると、エディター上および公開サイト上のリンクが切断されます。
* GUIDES-24983：任意の外部製品（MS PowerPoint など）から画像をコピーして Guides に貼り付けると、その場でアセットをアップロードしてファイルの破損に使用できる機能。
* GUIDES-21772: **chunk 属性** が **to-content** に設定されたコンテンツで、ネイティブのPDFの生成が失敗する。
* GUIDES-23964: **プロパティを編集** を選択すると、ベースラインダイアログに動的ベースラインの以前に保存した条件が表示されません。
* GUIDES-19067：フォルダープロファイルを複製すると、その管理者ユーザーリストも元のフォルダープロファイルからコピーされる

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)をご覧ください。

### 既知の問題 {#known-issues-19567}

なし。

### 廃止された機能と API {#deprecated-19567}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-19567}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 21 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-19567}

| テクノロジー | バージョン | リンク |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.27.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
