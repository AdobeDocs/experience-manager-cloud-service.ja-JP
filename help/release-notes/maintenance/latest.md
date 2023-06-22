---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 39696141a50bf8204d37341a85a4f4a8acae69db
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 31%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 12255 {#release-12255}

2023 年 6 月 13 日に公開されたメンテナンスリリース12255の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 12142 からのアップデートです。

2023.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-12255}

なし。

### 修正された問題 {#fixed-issues-12255}

- 各種アクセシビリティ関連の更新
- ASSETS-15116 - Assets の検索ビューの「Go to location」オプション
- ASSETS-17453 - (Dynamic Media) ビデオのカスタムサムネールを選択できません
- ASSETS-19279 — 大きなファイルのアセットダウンロードアーカイブ
- ASSETS-19544 — アセットの更新のためにユーザーが最終変更したもの
- ASSETS-20146 - （タッチ UI）検証エラーによるアセットダウンロードレポート失敗レポートは、レポートのリストページの常に上部に表示されます
- ASSETS-21056：書き込みを最小限に抑えるためのアセット参照パフォーマンスの最適化
- ASSETS-21909 - vtt のダウンロードに失敗した場合、スマート切り抜きビデオを表示できません
- ASSETS-22261 - Linkshare がダウンロードするフォルダー構造が Assets UI ダウンロードと一致しない
- ASSETS-22550 — 検索フィルターパネルがデフォルトで開くようになりました。
- ASSETS-22920 - Brand Portalからフォルダーを非公開にしても、内のアセットが非公開としてマークされない
- ASSETS-22922 — 無効になっているビューアプリセットがDynamic Mediaコンポーネントに表示される
- ASSETS-23461 - Brand Portal Assets 検索ビューからのクイック公開
- ASSETS-23466 -InDesign Serverアクセスできないリンク処理で、スペースを含む AAL リンクを解決できない
- ASSETS-23469 — デフォルトのアセットフィルターは、カスタムフィルターと競合します
- ASSETS-23981 — コレクションリンクでタイトルが機能しない並べ替え機能
- ASSETS-24723 — 公開済みアセットが再処理され、ユーザーの操作が不要になった問題を修正しました。
- GRANITE-45385 — ツリーのアクティベーションを移行して、ワークフローの代わりに sling ジョブを使用する

### 既知の問題 {#known-issues-12255}

- ASSETS-25729 — ビュースイッチャーメニューが切れている
- ASSETS-25728 - 「アセットを再処理」オプションは検索表示で使用できません
- ASSETS-22603 — 一部のダウンロードタイプのアセットレポート列には、UI に「null」値が表示されます。 ダウンロード可能な CSV は影響を受けません。

### 組み込みテクノロジー {#embedded-tech-12255}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | バージョン 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.0 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
