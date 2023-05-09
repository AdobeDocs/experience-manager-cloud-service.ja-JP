---
title: ターゲットコンテンツ用マルチサイト管理の構造
description: 図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 45%

---

# ターゲットコンテンツ用マルチサイト管理の構造  {#how-multisite-management-for-targeted-content-is-structured}

以下の図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています。

領域は **/content/campaigns/&lt;brand>** の下に表示され、デフォルトでは、ブランドごとに自動作成されるマスター領域が 1 つあります。各領域には、独自のアクティビティ、エクスペリエンスおよびオファーのセットが含まれます。

![マルチサイト構造](/help/sites-cloud/authoring/assets/multisite-structure.png)

ターゲットコンテンツを検索するために、ページまたはサイトを特定の領域にマッピングできます。 領域が設定されていない場合、AEMはこの特定のブランドのマスター領域にフォールバックします。

以下の図は、site1、site2、site3 という 3 つのサイトに対してロジックがどのように機能するかを示したものです。

![サイトをまたぐマルチサイト構造](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 は領域マッピングに基づいて、brand1 の myarea1 を検索し、brand2 の otherarea2 を検索します。
* site2 は、brand1 の領域マッピングのみが定義されているので、brand1 の myarea1 と brand2 の master 領域を検索します。
* site3 では、このサイトの他の領域マッピングが定義されていないので、brand1 と brand2 のマスター領域を検索します。
