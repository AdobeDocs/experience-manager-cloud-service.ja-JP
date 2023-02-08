---
title: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
description: の最新のメンテナンスリリースノート [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、as a Cloud ServiceExperience Managerの最新メンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 10912 {#release-10912}

2023 年 2 月 3 日に公開されたメンテナンスリリース10912の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、以前のメンテナンスリリース 9850 からの更新です。

このメンテナンスリリースで機能を有効にすると、すべての機能セットが提供されます。 詳しくは、 [最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md) 詳細はこちら。

### 既知の問題 {#known-issues}

CORS を使用している場合はアップグレードしないでください。 このリリースのGraphQLコンテンツ配信部分に影響を与える問題を特定しました。 GraphQLでの永続化されたクエリのキャッシュ方法に関するデフォルトのAEM Dispatcher 設定の変更により、CORS 設定を使用しているお客様に対して、永続化されたクエリのGraphQLコンテンツ配信が機能しなくなる場合があります。

### 組み込みテクノロジ {#embedded-tech}

| 科学技術 | バージョン | リンク |
|---|---|---|
| AEM WCM コアコンポーネント | バージョン2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
