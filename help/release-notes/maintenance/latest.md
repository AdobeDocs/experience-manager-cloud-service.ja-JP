---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: de06178f66c95baef15de19296a654f1ed4a0387
workflow-type: ht
source-wordcount: '383'
ht-degree: 100%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 16544 {#release-16544}

2024年6月4日（PT）に公開された、メンテナンスリリース 16544 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 16461 でした。

2024.6.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)を参照してください。

### 機能強化 {#enhancements-16544}

* GRANITE-41133：Jakarta Servlet API 5 と OSGi Servlet Whiteboard API をサポートします。
* GRANITE-51355：org.slf4j.event を非推奨にします。
* GRANITE-51565：ローカルグループが AEM から公開されると、AEM は外部グループとのローカルグループ関係を失います。
* GRANITE-51707：認証のための http リダイレクト中に cookie saml_request_path を設定します。
* GRANITE-50957：Jackrabbit バージョンを 2.20.16 に更新します。
* GRANITE-52057：Filevault を 3.7.3-T20240514105118-694f6aea に更新して、JCRVLT-745 を修正します。
* SKYOPS-35998：「Sling RepoInit」の依存関係（Repoinit パーサー 1.9.0、Repoinit JCR 1.1.46）を更新します。

### 修正された問題 {#fixed-issues-16544}

* GRANITE-51375：中間パスを指定しない場合、idp-sync が NPE をスローする。
* GUIDES-17171：15 KB を超えるトピックのコピー＆ペースト操作が、予期しないエラーで失敗する。
* GUIDES-17088：**ファイルプロパティ**&#x200B;パネルからドキュメントの状態を変更する機能が正しく動作せず、*下書き*&#x200B;状態に変わります。
* GUIDES-16931：バージョン作成後、トピックからリンクされた画像がベースラインに表示されない。
* GUIDES-16896：**ファイル名**&#x200B;でファイルを表示するように&#x200B;**ユーザーの環境設定**&#x200B;を設定する際、再利用可能なコンテンツパネルに要素がリストされない。

Experience Manager Guides の新機能や機能強化および修正された問題について詳しくは、[Experience Manager Guides リリースロードマップ](https://experienceleague.adobe.com/ja/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)を参照してください。

### 既知の問題 {#known-issues-16544}

なし。

### 変更通知 {#change-notice-16544}

2024年9月以降、AEM as a Cloud Service では、Sling Model Exporter フレームワークを介したリソースリゾルバーのシリアル化が無効になります。詳しくは、[ドキュメント](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)を参照してください。

### 非推奨（廃止予定）機能と API {#deprecated-16544}

AEM as a Cloud Service で非推奨（廃止予定）または削除された機能については、[非推奨（廃止予定）および削除された機能と API](/help/release-notes/deprecated-removed-features.md)を参照してください。

### 組み込みテクノロジー {#embedded-tech-16544}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | 2.25.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
