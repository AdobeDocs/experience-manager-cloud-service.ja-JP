---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 17%

---


# メンテナンスリリースノート {#maintenance-release-notes}

以下の節では、as a Cloud ServiceExperience Managerの現在のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 11835 {#release-11835}

2023 年 4 月 19 日に公開されたメンテナンスリリース11835の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース11382のアップデートです。

このメンテナンスリリースにおける機能イネーブルメントでは、包括的な機能セットを提供します。詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

### 修正された問題 {#fixed-issues-11835}

- SITES-12573 - 1 つの変数が指定されていない場合、フィルター内の変数を使用するGraphQLクエリは失敗します。 このリリースにはアップデートしないでください。AEM as a Cloud Serviceと共にGraphQLを使用する必要があります。
- SKYOPS-51970 - buildImage ステップで使用される FACT バージョンの回帰を識別し、一致しないユーザーマッピングを引き起こしました。
- GRANITE-44542 — パッケージフィルターに含まれるフォルダーに対して（jcr:primaryType を含む.content.xml を提供することで）パッケージノードタイプを指定しなかったお客様に対して、問題が報告されています。 その結果、これらのフォルダーが nt:folder として扱われ、様々な状況で問題が発生していました。
- SKYOPS-56928 - Apache HTTPD 回帰は、404 エラーを引き起こす可能性があります。 これらの問題が発生した場合は、安全上の理由から、以前のバージョンにロールバックし、その期間中にパイプラインが実行されるのを防ぐことをお勧めします。

### 組み込みテクノロジー {#embedded-tech-11835}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | バージョン 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | バージョン 1.4.20 ～ 1.4.0 | [HTMLテンプレート言語の仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.21.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
