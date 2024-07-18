---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: ht
source-wordcount: '332'
ht-degree: 100%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 17098 {#release-17098}

2024年7月16日（PT）に公開された、メンテナンスリリース 17098 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 16971 でした。

2024.7.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-17098}

- SKYOPS-79817：サービスユーザーマッピング用の Sling 機能アナライザータスクを有効にする

### 修正された問題 {#fixed-issues-17098}

- ASSETS-39665：6.5 から AEMCS への移行後、スマート切り抜き同期が機能しない
- FORMS-14993：以前機能していた販促物に対して、Forms API が 500 を返す
- GRANITE-52120：アクセス制御データを表示する際に、CRXDE が 500 を返す
- GRANITE-52573：書き換えられた URL で // を使用する際に、リクエストが 400 を返す
- GRANITE-52746：ノードを作成ダイアログに、すべてのノードタイプが読み込まれない
- GRANITE-52777：リクエストをラップする際に、404 の処理が破損する
- GRANITE-52871：publish-worker が golden-publish と同期され、コンパクション前に完了する
- SKYOPS-79173：レプリケーターが、特定の AgentIdFilter に一致する複数のエージェントにレプリケートしない
- SKYOPS-80075：アセット名のウムラウトの問題により、公開キューがブロックされる（Mac）
- SKYOPS-81032：拡張ロギングを使用する際に、ログを取得するリクエストで生成したログが除外される

### 既知の問題 {#known-issues-17098}

なし

### 変更通知 {#change-notice-17098}

- 2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。 詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 廃止された機能と API {#deprecated-17098}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### 組み込みテクノロジー {#embedded-tech-17098}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
