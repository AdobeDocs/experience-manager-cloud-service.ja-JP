---
title: Repository Modernizer
description: 既存のプロジェクトパッケージを再構築し、Adobe Experience Manager as a Cloud Service 用に定義されたプロジェクト構造と互換性を持たせる方法を説明します。
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 6920651420da9b427510518b7add0637479adef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%

---

# リポジトリモダナイザー {#repo-modernizer}

Repository Modernizer は、Adobe Experience Manager as a Cloud Service 用に定義されたプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再作成するために開発されたユーティリティです。

## はじめに {#introduction}

Adobe Experience Manager a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEM は可変コンテンツと不変コンテンツの分割を考慮して&#x200B;**コンテンツ**&#x200B;と&#x200B;**コード**&#x200B;を個別のサブパッケージに分離する必要があります。Cloud Service の新しい AEM プロジェクト構造について詳しくは、[AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=ja)を参照してください。

Repository Modenizer は、次のデプロイメント構造を作成することで、互換性のある AEM Cloud Service プロジェクト構造を作成します。

* `ui.apps` パッケージは `/apps` にデプロイされ、すべてのコードが含まれます。

* `ui.content` パッケージは、実行時に書き込み可能な領域（例：`/content`、 `/conf`、`/home` または `/apps` 以外）にデプロイされ、すべてのコンテンツと設定を含んでいます。

* `all` パッケージは、`ui.apps` サブパッケージおよび `ui.content` サブパッケージを含むコンテナパッケージです。

>[!NOTE]
>
>プロジェクト構造は、パッケージおよびその `pom.xml/filter.xml files` に対して、*アーキタイプ 24* に基づいています。詳しくは、[アーキタイプ 24](https://github.com/adobe/aem-project-archetype) を参照してください。

## Repository Modernizer の使用 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/3412961/?quality=12&learn=on&captions=jpn)

* Adobe I/O CLI 経由：`aio-cli-plugin-aem-cloud-service-migration`（AEM as a Cloud Service の Adobe I/O CLI 用のコードリファクタリングプラグイン）を介して Repository Modenizer を使用することをお勧めします。

  プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：Repository Modernizer は、スタンドアロンユーティリティとして実行することもできます。

  このツールの使用方法について詳しくは、**[Git リソース：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** を参照してください。

  >[!NOTE]
  >
  >Repository Modenizer は、NodeJS を使用して開発されています。NodeJS 10.0 以降をインストールすることをお勧めします。
