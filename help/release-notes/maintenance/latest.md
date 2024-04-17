---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: ht
source-wordcount: '272'
ht-degree: 100%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15860 {#release-15860}

2024年4月10日（PT）に公開された、メンテナンスリリース 15860 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15787 でした。

2024.3.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-15860}

なし。

### 修正された問題 {#fixed-issues-15860}

* ローンチが削除または移動されたページを参照する場合の、ローンチコンソールを表示する際のリグレッションを修正しました。

### 既知の問題 {#known-issues-15860}

なし。

### 廃止された機能と API {#deprecated-15860}

* [Adobe Developer Console での JWT 資格情報の廃止](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

AEM as a Cloud Serviceで廃止または削除された機能については、[廃止または削除された機能と API](/help/release-notes/deprecated-removed-features.md) を参照してください。

### 変更通知 {#change-notice-15860}

**必須アクション**

#### CM Java バージョンを 11 に設定 {#set-java-version-11}

新しいバージョンの aem-sdk-api には、Java 11 ターゲットでコンパイルされたクラスが含まれていますが、Cloud Manager ビルド環境のデフォルトの JDK バージョン 1.8 と互換性がありません。この更新では、JDK 11 を使用して Maven を実行する必要があります。

お客様には、`11` の内容を含む `.cloudmanager/java-version` ファイルを Git リポジトリのルートに追加することをお勧めします。[ビルド環境／Maven JDK バージョンの設定](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version)を参照してください。


### 組み込みテクノロジー {#embedded-tech-15860}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.24.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
