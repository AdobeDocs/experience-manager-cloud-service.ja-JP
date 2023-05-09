---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.4.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.4.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 55%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.4.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.4.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2023.4.0 のリリース日は 2023 年 4 月 13 日です。 次回のリリースは 2023年5月11日（PT）に予定されています。

## 新機能 {#what-is-new}

* [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)は、バージョン 41 に更新されました。

## バグの修正 {#bug-fixes}

* When a [証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 有効期限 [ドメイン名](/help/implementing/cloud-manager/custom-domain-names/introduction.md) および [IP許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) 証明書に関連付けられていたものは、CDN から削除されなくなります。  このような場合、サイトには引き続き到達可能です。
* Cloud Manager UI には、事前に [SSL 証明書](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 期限が切れそうです。
* まれに、お客様が新しい環境を作成または削除できない問題が修正されました。
