---
title: プロビジョニングプロセス - 概要
description: プロビジョニングプロセス - 概要
source-git-commit: ffeda76f9c661117ddba50588ebea01d151ee8c3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 100%

---


# AEM as a Cloud Service：オンボーディングとアクセス

ここでは、Adobe Experience Manager as a Cloud Service のプロビジョニングプロセスに関するセルフヘルプリソースの一覧を示します。

## AEM as a Cloud Service プロビジョニングプロセスの概要

ここでは、以下を重点的に扱った主要な記事を紹介します。

* AEM as a Cloud Service へのアクセス
* Adobe Experience Manager as a Cloud Service のオンボーディングとプロビジョニングプロセス
* ヘルプとリソース


### AEM as a Cloud Service へのアクセス

自動プロビジョニングが完了すると、次のようになります。

* アクセス権が付与され、アドビは、Adobe Identity Management System（IMS）内に組織を作成する
* 指定された管理者は、デフォルトで管理者権限を持つ
* 管理者は、Admin Console を使用して、追加のチームメンバーにユーザーと役割を追加できる
* 役割に基づいたユーザーの権限を確認し、Cloud Manager で権限の割り当てを決定する

![processoverview.jpg](assets/processOverview.jpg)


詳しくは、Experience Leagueue の [Experience Manager as a Cloud Service へのオンボーディング](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=ja)を参照してください。

### リソースとリンク

* [AEM as a Cloud Service の IMS サポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja)
* [Cloud Manager での役割ベースの権限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=ja#what-is-required)
* [Adobe Experience Manager as a Cloud Service へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=ja#getting-access)


## Adobe Experience Manager as a Cloud Service のオンボーディングプロセス

### 1. 購入注文によって自動プロビジョニングがトリガーされます。

### 2. Adobe Admin Console への組織がオンボーディングされます。

![processoverview2.jpg](assets/processOverview2.jpg)

* システム管理者：
   * AEM プログラムと環境をプロビジョニングします。
   * Admin Console に移動して管理タスクを実行します。
   * 各ドメインの所有権を確認するドメインをリクエストします。
   * ユーザーディレクトリを設定します。
   * IDP を設定します。
* AEM 管理者：
   * ローカルグループ、許可および権限を管理します。

### 3. Admin Console でユーザーをオンボーディングし、アクセスを管理します。

![processoverview3.jpg](assets/processOverview3.jpg)

サイズと環境に応じて、3 つの方法でユーザーをオンボードします。
* Admin Console から手動でユーザーを作成する
* .csv ファイルをアップロードする
* エンタープライズ Active Directory からユーザーを同期する

### 4. 管理者が組織を設定し、ユーザーとグループに環境へのアクセスを許可します。

## ヘルプとリソース

* [初回ログイン - Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [AEM as a Cloud Service へのアクセスの設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=ja#accessing)
