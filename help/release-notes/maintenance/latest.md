---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e1fa4b3bcb04ab3e834b34f507f1350fb536b513
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 52%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21005 {#21005}

2025年5月27日（PT）に公開された、メンテナンスリリース 21005 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 20626 でした。

2025.5.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21005}

* GRANITE-58927：セマンティック検索の切り替えの改善。
* GRANITE-58800:Apache Commons コレクションをバージョン 4.5.0 に更新。
* GRANITE-58866:Oakを 1.80.0 にアップデート。
* SKYOPS-106509:Java 21 での反射アクセスにより、GSON 互換性が強化されました。
* SKYOPS-107761:Sling Models Jackson エクスポーターを 1.1.6 に更新しました。
* SKYOPS-107813：Sling ResourceResolver 1.12.8 にアップデート。

### 修正された問題 {#fixed-issues-21005}

* CNTBF-443: SearchSlingJob `EVENT_JOB_TOPIC` プロパティを修正しました。
* GRANITE-57853:UI でのドロップダウン位置の問題を修正しました。
* GRANITE-58107:OAuth ハンドラーでユーザーベースのポッドアフィニティを無効にすることで、パブリッシュで 404 エラーが発生する問題を修正しました。
* GRANITE-58276、SLING-12755:HTL スクリプトエンジンファクトリが正しく開始されず、サーバーサイドのレンダリングエラーが断続的に発生する可能性がある OSGi 依存関係サイクルを修正しました。
* SKYOPS-105151：バンドルリストにアクセスする際の NPE を修正しました。
* SKYOPS-83910、SKYOPS-82371 - JSP コンパイルの同時実行の問題を修正しました。

#### AEM ガイド {#guides}

* GUIDES-26919：統合シェルを有効にして DITA マップを開くと、エディターが断続的に更新される。
* GUIDES-26282：トピックの更新または作成中に JCR セッション接続を閉じないと、メモリリークやサービスのダウンタイムが発生します。
* GUIDES-26434:DITA コンテンツに Web リンクがあり、範囲がが `external` でない場合、PDFのネイティブパブリッシングが無期限に続きます。
* GUIDES-26516：コンテンツにエラーがある場合、ネイティブ PDF およびAEM サイトの公開が停止し、キューに入れられます。

このリリースの新機能および機能強化と修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-21005}

なし。

### 非推奨（廃止予定）機能と API {#deprecated-21005}

* GRANITE-54164：パブリック API から `org.apache.jackrabbit.oak.plugins.blob` を削除しました。
* GRANITE-54280：パブリック API から `org.apache.jackrabbit.oak.cache` を削除しました。
* GRANITE-58332：パブリック API の非推奨（廃止予定）の `org.apache.jackrabbit.oak.plugins.memory` です。
* [Experience Cloud設定の自動化 ](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) 機能は廃止されました。

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21005}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 5 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 変更通知 {#change-notice-21005}

* このリリースには、次の新しい製品インデックスバージョンが含まれています。
   * **damAssetLucene-12**

以前のインデックスバージョンのカスタムバージョンは、新しい製品インデックスバージョンと自動的に結合されます。結合バージョンに対して、さらにカスタムアップデートを適用してください。

#### aem-cloud-testing-clients を更新する {#update-aem-cloud-testing-clients-21005}

今後の変更では、カスタム機能テストで使用するライブラリ [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) を、少なくともバージョン **1.2.1** に更新する必要があります（推奨：最新バージョン 1.2.9）

`it.tests/pom.xml` の依存関係が更新されていることを確認してください。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

この変更は、2025 年 6 月 15 日（PT）までに実行する必要があります。
依存関係ライブラリの更新に失敗すると、「カスタム機能テスト」手順でパイプラインにエラーが発生します。

### 組み込みテクノロジー {#embedded-tech-21005}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
