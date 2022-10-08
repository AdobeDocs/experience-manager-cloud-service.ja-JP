---
title: Repository Modernizer
description: Repository Modernizer
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 94%

---

# Repository Modernizer {#repo-modernizer}

Repository Modernizer は、Adobe Experience Manager as a Cloud Service 用に定義されたプロジェクト構造と互換性を持たせるために、コンテンツとコードを個別のパッケージに分離して、既存のプロジェクトパッケージを再作成するために開発されたユーティリティです。

## はじめに {#introduction}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトに様々な新機能と可能性を提供します。ただし、AEM Cloud Service との互換性を保つためには、Adobe Experience Manager Maven プロジェクトにいくつかの変更が必要です。上位レベルでは、可変コンテンツと不変コンテンツの分割を考慮して&#x200B;**コンテンツ**&#x200B;と&#x200B;**コード**&#x200B;を個別のサブパッケージに分離する必要があります。Cloud Service 用の新しい AEM プロジェクト構造の詳細については、「[AEM プロジェクトの構造](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=ja)」を参照してください。

Repository Modenizer は、次のデプロイメント構造を作成することで、互換性のある AEM Cloud Service プロジェクト構造を作成します。

* `ui.apps` パッケージは `/apps` にデプロイされ、すべてのコードが含まれます。

* `ui.content` パッケージは、実行時に書き込み可能な領域にデプロイされます ( 例： `/content`, `/conf`, `/home`または何も `/apps`) およびには、すべてのコンテンツと設定が含まれます。

* `all` パッケージは、`ui.apps` サブパッケージおよび `ui.content` サブパッケージを含むコンテナパッケージです。

>[!NOTE]
>プロジェクト構造は、パッケージおよびその `pom.xml/filter.xml files` に対して、*アーキタイプ 24* に基づいています。詳細は、「[アーキタイプ 24](https://github.com/adobe/aem-project-archetype)」を参照してください。

## Repository Modernizer の使用 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Adobe I/O CLI 経由：`aio-cli-plugin-aem-cloud-service-migration`（AEM as a Cloud Service の Adobe I/O CLI 用のコードリファクタリングプラグイン）を介して Repository Modenizer を使用することをお勧めします。

   このプラグインをインストールして使用する方法については、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：Repository Modernizer は、スタンドアロンユーティリティとして実行することもできます。

   このツールを使用する方法について詳しくは、 **[Git リソース：Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;を参照してください。

   >[!NOTE]
   >
   >Repository Modenizer は、NodeJS を使用して開発されています。NodeJS 10.0 以降をインストールすることをお勧めします。
