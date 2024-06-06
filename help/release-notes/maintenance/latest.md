---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f52b5f763277c9288d5dd30b01cfb7a4afeddda7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 43%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16544 {#release-16544}

2024年6月4日（PT）に公開された、メンテナンスリリース 16544 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 16461 でした。

2024.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16544}

* GRANITE-41133:Jakarta Servlet API 5 および OSGi Servlet Whiteboard API をサポートします。
* GRANITE-51355:org.slf4j.event を非推奨（廃止予定）にします。
* GRANITE-51565：ローカルグループがAEMから公開されると、AEMは外部グループとのローカルグループ関係を失います。
* GRANITE-51707：認証のために http リダイレクト中に cookie saml_request_path を設定する。
* GRANITE-52010:Jackrabbit バージョンを 2.20.16 に更新します。
* GRANITE-52057:JCRVLT-745 を修正して Filevault を 3.7.3-T20240514105118-694f6aea に更新。
* SKYOPS-35998:「Sling RepoInit」依存関係を更新する：Repoinit パーサー 1.9.0、Repoinit JCR 1.1.46。

### 修正された問題 {#fixed-issues-16544}

* GRANITE-51375：中間パスが指定されていない場合、idp-sync は NPE をスローします。
* GUIDES-17171:15 KB を超えるトピックのコピーと貼り付け操作が、予期しないエラーで失敗します。
* ガイド–17088：からドキュメントの状態を変更する機能 **ファイルのプロパティ** パネルが正しく動作しておらず、 *ドラフト* 都道府県。
* GUIDES-16931：トピックのリンク画像が、バージョンの作成後にベースラインに表示されない。
* ガイド–16896：再利用可能なコンテンツパネルで、 **ユーザー環境設定** は、次の方法でファイルを表示するように設定されています **ファイル名**.

Experience Managerガイドで修正された新機能や機能強化および問題について詳しくは、を参照してください [Experience Managerガイドのリリースロードマップ](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### 既知の問題 {#known-issues-16544}

なし。

### 変更通知 {#change-notice-16544}

2024 年 9 月以降、AEM as a Cloud Serviceは Sling Model エクスポーターフレームワークを介してリソースリゾルバーのシリアル化を無効にします。 参照： [ドキュメント](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter) を参照してください。

### 非推奨（廃止予定）機能と API {#deprecated-16544}

AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16544}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
