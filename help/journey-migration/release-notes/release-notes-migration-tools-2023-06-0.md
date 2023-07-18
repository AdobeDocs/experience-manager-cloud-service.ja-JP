---
title: AEM as a Cloud Service リリース 2023.06.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.06.0 の移行ツールのリリースノート
feature: Release Information
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 33%

---

# AEM as a Cloud Service リリース 2023.06.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.06.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v2.0.20 のリリース日は 2023 年 6 月 08 日です。

### 新機能 {#what-is-new-ctt}

* 新しい移行ツールである Content Transformer(CT) が、このリリースのコンテンツ転送ツール (CTT) と統合されました。 Content Transformer は、 [ベストプラクティスアナライザー (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=ja) 現在のAEM実装 ( オンプレミスまたはManaged Services) からAEM as a Cloud Serviceにコンテンツを移行する前に。
Content Transformer が提供するメリットは次のとおりです。
   * フェイルセーフ：パッケージは、問題を修正するためにリポジトリを変更するたびに、Content Transformer によって作成されます。 必要に応じて、パッケージをインストールして前の状態に戻すことができます。
   * 使いやすさ：Content Transformer は、コンテンツ転送ツールに統合され、直感的なシンプルなユーザーインターフェイスを備えています。
   * 時間を節約：1 つのパターンに該当するコンテンツの問題が多数ある場合、Content Transformer を使用して、数回のクリックですべての問題を解決でき、時間と移行の複雑さを大幅に削減できます。
