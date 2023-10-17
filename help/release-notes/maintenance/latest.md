---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e771913562b3770e5a504432d40c770804aadc4b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 30%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13804 {#release-13804}

2023 年 10 月 10 日に公開されたメンテナンスリリース13804の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 13665 からのアップデートです。

2023.10.0機能のアクティベーションでは、このメンテナンスリリースの機能が完全に提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13804}

* GRANITE-47238：監査ログのメンテナンス — cronjobs をパージして、お客様の設定を使用します。
* GRANITE-47123：公開 (Sling) — デフォルトでバニティーパスキャッシュを非同期的に初期化することで、起動時間を短縮します。
* GRANITE-46618：公開（レプリケーション） — レプリケーションステータスメッセージのバッチ処理により、公開の起動速度が向上しました。
* GRANITE-47136：インデックス作成（ダウンロード） — 新しい並列インデックスダウンローダのダウンロード速度を向上させます（チェックサム検証を無効にすることで）。
* GRANITE-47211：パブリッシュ（インフラ） — セグメントストアのリビジョン名を保存および取得することで、パブリッシュ層のデプロイメントの分離を改善します。
* GRANITE-47267: Apache Felix Http Jetty 4.2.18 への更新（リクエストパラメーター処理のバグ修正を含む）([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625)) のパフォーマンスが向上しました。
* GRANITE-47247：サーブレットの解決のパフォーマンスが向上し、Sling Servlets Resolver 2.9.14 に更新しました。

### 修正された問題 {#fixed-issues-13804}

* GRANITE-47376：オーサー (Infra) — ローリング再起動後の DiscoveryTopologyUndefined エラーを修正しました。
* CQ-4353436: AEM Web Console(Sling) - ServiceUserMapperImpl の空の設定のバリデーター（プリンシパル/ユーザー）がAEMインスタンスを壊す ([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912)) をクリックします。
* SKYOPS-63925: Transform Job - JDK 11 での TransformJob の失敗の回避 — ZipException：無効な CEN ヘッダーエラー（disableZip64ExtraFieldValidation JVM フラグ付き）。
* SKYOPS-63361：変換ジョブ（ログ）変換ジョブ（CUSTOMER_EXTRACT サブステップ）を使用したログの改善
* SKYOPS-64103: FACT ツール（ログ） - Clientlib のコンパイルエラーと警告メッセージを減らすか、切り捨てます。
* SKYOPS-65109: FACT ツール（エラー処理） — 未解決の依存関係を持つコンテンツパッケージは、正しく報告されたエラーを引き起こします。
* SKYOPS-65368: FACT ツール（エラー処理） — ツールは無限の包含サイクルに陥り、最終的には Clientlibs の循環埋め込みでタイムアウトします。
* SKYOPS-64031: RDE - ComponentCacheImpl は、ResourceResolverFactory 登録 ([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019)) をクリックします。
* ASSETS-29105: RDE - RDE 機能モデルの SecurityProviderRegistration requiredServicePids に制限プロバイダーがありません。
* GRANITE-44674: CoralUI — 日付選択が必要なフィールドの機能が正しくありません。

### 既知の問題 {#known-issues-13804}

* CQ-4354836：プロジェクトコンソールからワークフローを開始またはタスクを作成できません。
* CQ-4354834 ：ユーザーがインボックスタスクにコメントを追加できません。

### 組み込みテクノロジー {#embedded-tech-13804}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
