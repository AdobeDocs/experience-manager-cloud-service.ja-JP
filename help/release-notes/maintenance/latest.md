---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 51%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 21193 {#21193}

2025年6月10日（PT）に公開された、メンテナンスリリース 21193 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 21005 でした。

2025.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-21193}

* ASSETS-51245：タッチ UI の大規模なフォルダーリストのパフォーマンスが向上しました。
* ASSETS-51686：簡単なジョブキャンセル、拡張ログ、大きな結果を得るための監査ダウンロードなど、一括操作ジョブの改善。
* CQ-4360131:OpenAPI エンドポイントのエラー応答が改善され、API クライアントが正しい構造化エラー情報を受信できるようになりました。

### 修正された問題 {#fixed-issues-21193}

* ASSETS-41007：削除されたアセットがContent Hubに表示されたままになる場合があります。
* ASSETS-50994:AemRequestEventFilter が、過剰な Jetty スレッドの競合を引き起こしている。
* ASSETS-50155：重複メタデータの変更イベントがトリガーされる。
* ASSETS-50716:Assets リスト表示でタイトルで並べ替えると、期待どおりに動作しません。
* ASSETS-50820:Asset Relations API への無効なリクエストが 400 エラーで適切に却下されることを確認します。
* ASSETS-50562：名前の競合が発生した場合、Asset Upload API はデフォルトでバージョンを作成する。
* ASSETS-50992:Assets API initiateUpload.json エンドポイントは、「application/json」のコンテンツタイプを返す必要があります。
* ASSETS-51322：非同期バリケードが、ジョブの失敗後も無期限に保持される場合、このバリケードの自動削除と期限切れ。
* ASSETS-51809：ブラウザーのキャッシュが原因で、CSV エディターに最近保存された変更が表示されなかった。
* SITES-31678：コンテキスト対応参照を含むエクスペリエンスフラグメント（XF）が、XF 公開 API で正しい言語ルートを解決しなかった。


### 既知の問題 {#known-issues-21193}

なし。

### 廃止された機能と API {#deprecated-21193}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-21193}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 2 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-21193}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.29.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
