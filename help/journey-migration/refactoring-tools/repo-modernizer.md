---
title: Repository Modernizer
description: Repository Modernizer
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 64%

---

# Repository Modernizer {#repo-modernizer}

Repository Modernizer は、Adobe Experience Manager as a Cloud Service 用に定義されたプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再作成するために開発されたユーティリティです。

## はじめに {#introduction}

Adobe Experience Manager a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、AEMでは **コンテンツ** および **コード** 可変コンテンツと不変コンテンツの分割を考慮して、個別のサブパッケージに分割します。 詳しくは、 [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=ja) を参照してください。

Repository Modenizer は、次のデプロイメント構造を作成することで、互換性のある AEM Cloud Service プロジェクト構造を作成します。

* `ui.apps` パッケージは `/apps` にデプロイされ、すべてのコードが含まれます。

* `ui.content` パッケージは、実行時に書き込み可能な領域（例：`/content`、 `/conf`、`/home` または `/apps` 以外）にデプロイされ、すべてのコンテンツと設定を含んでいます。

* `all` パッケージは、サブパッケージを含むコンテナパッケージです `ui.apps` および `ui.content`.

>[!NOTE]
>プロジェクト構造は、パッケージおよびその `pom.xml/filter.xml files` に対して、*アーキタイプ 24* に基づいています。詳細は、「[アーキタイプ 24](https://github.com/adobe/aem-project-archetype)」を参照してください。

## Repository Modernizer の使用 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Adobe I/OCLI:を介して Repository Modernizer を使用することをお勧めします。 `aio-cli-plugin-aem-cloud-service-migration` (Adobe I/OCLI 用のAEMas a Cloud Serviceコードリファクタリングプラグイン )。

  詳しくは、 **[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** そのため、プラグインをインストールして使用する方法を学ぶことができます。

* スタンドアロンユーティリティとして：Repository Modernizer は、スタンドアロンユーティリティとして実行することもできます。

  詳しくは、 **[Git リソース：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** このツールの使い方を学ぶことができます。

  >[!NOTE]
  >
  >Repository Modenizer は、NodeJS を使用して開発されています。NodeJS 10.0 以降をインストールすることをお勧めします。
