---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 92%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 15575 {#release-15575}

2024年3月19日（PT）に公開された、メンテナンスリリース 15575 の継続的な改善点を以下にまとめます。以前のメンテナンスリリースは、リリース 15262 でした。

2024.3.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。詳しくは、[Experience Manager リリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja)を参照してください。

### 機能強化 {#enhancements-15575}

なし。

### 修正された問題 {#fixed-issues-15575}

* ASSETS-36358：アップロードレポートをレンダリングできない。
* GRANITE-50774：GraniteContent には、初期化時にプロパティ値の決定的な順序を使用する必要がある。

### 既知の問題 {#known-issues-15575}

なし。

### 変更通知 {#change-notice-15575}

**必須アクション**

#### CM Java バージョンを 11 に設定 {#set-java-version-11}

新しいバージョンの aem-sdk-api には、Java 11 ターゲットでコンパイルされたクラスが含まれていますが、Cloud Manager ビルド環境のデフォルトの JDK バージョン 1.8 と互換性がありません。この更新では、JDK 11 を使用して Maven を実行する必要があります。

お客様には、`11` の内容を含む `.cloudmanager/java-version` ファイルを Git リポジトリのルートに追加することをお勧めします。詳しくは、 [ビルド環境/ Maven JDK バージョンの設定](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### aem-cloud-testing-clients を 1.2.1 に更新 {#update-aem-cloud-testing-clients}

今後の変更では、カスタム機能テストで使用されるライブラリ [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) を少なくともバージョン **1.2.1** に更新する必要があります

`it.tests/pom.xml` の依存関係が更新されていることを確認してください。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

この変更は、2024 年 4 月 7 日より前に実行する必要があります。

依存関係ライブラリの更新に失敗すると、「カスタム機能テスト」手順でパイプラインにエラーが発生します。

### 組み込みテクノロジー {#embedded-tech-15575}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.4 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
