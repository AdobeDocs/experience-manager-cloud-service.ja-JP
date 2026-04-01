---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e035c1c27f652af231034588eb1359354182dcb0
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 62%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 25194 {#25194}

2026年4月1日（PT）に公開された、メンテナンスリリース 25194 の継続的な改善点を以下にまとめます。前回のメンテナンスリリースは、リリース 24678 でした。

2026.4.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

>[!NOTE]
>
>リリース 24893は非公開になっています。

### 機能強化 {#enhancements-25194}

* ASSETS-65127：イベントカスタムメタデータ：メタデータ名の処理が改善されました。
* ASSETS-63313：書き出されたアセットと親に関する関連リンクを、C2PA マニフェストに基づいて自動作成します。
* ASSETS-10995：ダウンロード zip内のアセットの数を制限します。

### 修正された問題 {#fixed-issues-25194}

* ASSETS-62882：管理者ビュー：複数の無効なファイル名がアップロードされると、情報ツールチップが壊れる。
* ASSETS-63642：一部の開発環境（SLA3）でShare Linkがアセットをレンダリングできない。
* ASSETS-59267：配信ペイロードのアプリケーションメタデータを読み込む際にNPEが発生する。
* ASSETS-59227：メタデータの書き出し：正規表現の一致により、選択されていないプロパティが含まれなくなりました。
* ASSETS-65187：列データにエスケープコンマが含まれている場合、クラウドのCSV プレビュー。
* ASSETS-63441：すべてのユーザーにAssets オムニサーチ設定を読み取る権限があることを確認します。
* SITES-40095: メタデータエディター：ローカルコンテンツフラグメントが10個を超えるエントリを参照します。

### 既知の問題 {#known-issues-25194}

なし。

### 廃止された機能と API {#deprecated-25194}

AEM as a Cloud Service で廃止および削除された機能と API について詳しくは、[廃止および削除された機能と API](/help/release-notes/deprecated-removed-features.md) ドキュメントを参照してください。

### セキュリティ修正 {#security-25194}

AEM as a Cloud Service では、プラットフォームのセキュリティとパフォーマンスの最適化に取り組んでいます。 このメンテナンスリリースでは、特定された 9 つの脆弱性に対処し、堅牢なシステム保護に対する取り組みを強化しています。

### 組み込みテクノロジー {#embedded-tech-25194}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| Apache HTTP サーバー | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM コアコンポーネント | 2.30.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（デフォルト） | [サポートされている Node.js バージョン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
