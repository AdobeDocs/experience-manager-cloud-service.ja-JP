---
title: Repository Modernizer
description: Repository Modenizer
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 100%

---


# Repository Modernizer {#repo-modernizer}

Repository Modernizer は、Adobe Experience Manager as a Cloud Service 用に定義されたプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再作成するために開発されたユーティリティです。

## 概要 {#introduction}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、可変コンテンツと不変コンテンツの分割を考慮して&#x200B;**コンテンツ**&#x200B;と&#x200B;**コード**&#x200B;を個別のサブパッケージに分離する必要があります。Cloud Service 用の新しい AEM プロジェクト構造の詳細については、「[AEM プロジェクトの構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html)」を参照してください。

Repository Modenizer は、次のデプロイメント構造を作成することで、互換性のある AEM Cloud Service プロジェクト構造を作成します。

* `ui.apps` パッケージは `/apps` にデプロイされ、すべてのコードが含まれます。

* `ui.content` パッケージは実行時に書き込み可能な領域（例：`/content`、 `/conf`、`/home`のいずれか、または `/apps` 以外）にデプロイされ、すべてのコンテンツと設定が含まれます。

* `all` パッケージは、`ui.apps` サブパッケージおよび `ui.content` サブパッケージを含むコンテナパッケージです。

>[!NOTE]
>プロジェクト構造は、パッケージおよびその `pom.xml/filter.xml files` に対して、*アーキタイプ 24* に基づいています。詳細は、「[アーキタイプ 24](https://github.com/adobe/aem-project-archetype)」を参照してください。

## Repository Modernizer の使用 {#using-repo-modernizer}

* Adobe I/O CLI 経由：`aio-cli-plugin-aem-cloud-service-migration`（AEM as a Cloud Service の Adobe I/O CLI 用のコードリファクタリングプラグイン）を介して Repository Modenizer を使用することをお勧めします。

   プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：Repository Modernizer は、スタンドアロンユーティリティとして実行することもできます。

   このツールを使用する方法について詳しくは、 **[Git リソース：Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;を参照してください。

   >[!NOTE]
   >
   >Repository Modenizer は、NodeJS を使用して開発されています。NodeJS 10.0 以降をインストールすることをお勧めします。
