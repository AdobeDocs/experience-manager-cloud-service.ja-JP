---
title: Cloud ServiceとしてのAEM版Cloud Managerへのアクセス
description: Cloud ServiceとしてのAEM版Cloud Managerへのアクセス
translation-type: tm+mt
source-git-commit: 4904d7728befd3562940b35c7d44dbf9cae87fee
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Cloud Service{#navigation}としてAEM版Cloud Managerにアクセスする

システム管理者からCloud Managerへのアクセス権が付与されると、Cloud Managerのログインページが表示されます。このページは[Adobe Experience Cloud](https://my.cloudmanager.adobe.com/)からもアクセスできます。

正常にログインすると、以下に示すようにCloud Managerのランディングページに誘導されます。

![](assets/first_timelogin1.png)

## SysAdminタスク{#sysadmin-tasks}

SysAdminロールのユーザーは、**「アクセスを管理**」を選択して、ロールと権限を管理し、AEMインスタンスにアクセスするAdmin Consoleに直接アクセスできます。

### ロールの管理{#manage-roles}

SysAdminロールのユーザーは、**Admin Console**&#x200B;内の、Cloud Managerに対するユーザーの役割または権限が管理される場所への1回のクリックでのアクセス権を持ちます。

プロファイルにユーザーを追加する方法の詳細については、[Accessing Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager)を参照してください。

>[!NOTE]
>2020年1月以前にAEMにCloud Serviceとしてアクセス権を付与された組織では、組織はAdobe Admin Consoleに移動され、製品と環境の製品プロファイルを選択する必要があります。

1. Cloud Managerのランディングページーに移動し、「**アクセスを管理**」をクリックします。

   ![](assets/sys-admin5.png)

1. 「**アクセスを管理**」をクリックすると、**Admin Console**&#x200B;に移動します。ここから、Cloud Managerへのユーザーの役割や権限を管理できます。

   ![](assets/sys-admin1.png)

### 作成者インスタンスへのアクセスの管理{#manage-access-aem}

SysAdminロールのユーザーは、**Admin Console**&#x200B;への1クリックアクセス権を持ち、ここから作成者インスタンスに直接移動してアクセスを管理できます。

>[!NOTE]
>2020年1月以前にAEMにCloud Serviceとしてアクセス権を付与された組織では、組織はAdobe Admin Consoleに移動され、製品と環境の製品プロファイルを選択する必要があります。

詳細は、「AEMでのインスタンスへのCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#accessing-instance-cloud-service)としてのアクセス」を参照してください。[

1. **環境の概要**&#x200B;ページから&#x200B;**プログラム**&#x200B;カードに移動し、**アクセスの管理**&#x200B;をクリックします。

   ![](assets/sys-admin6.png)

   または、

   **「** Manage  **** Access」も、 **** Environmentscardの「Details」をクリックすると、「 **** Manage」ボタンから使用できます。

   ![](assets/sys-admin4.png)

1. 「**アクセスを管理**」をクリックすると、**Admin Console**&#x200B;に移動します。ここから、環境の作成者インスタンスにアクセスできます。

   ![](assets/sys-admin-2.png)

## 既存のAMSのお客様{#existing-aem}

既存のAMS(Adobe Managed Services)のお客様がCloud Serviceにアクセスできる場合は、既存のプログラムと、ランディングページの右上隅に「**追加プログラム**」ボタンが表示されます。

「**プログラム追加**」ボタンが表示されず、Cloud Serviceへのアクセスに関するご質問は、Adobeの担当者にお問い合わせください。

## 新規Cloud Serviceのお客様向け{#new-cloud-services}

Cloud Serviceを初めてお使いの場合は、空のランディングページの右上隅に「**追加プログラム**」ボタンが表示されます。 Cloud Serviceに新しいプログラムを追加する必要があります。

Cloud Managerでプログラムを追加する方法については、次を参照してください。
* [実稼働プログラムの作成](/help/onboarding/getting-access-to-aem-in-cloud/creating-production-program.md)
* [サンドボックスプログラムの作成](/help/onboarding/getting-access-to-aem-in-cloud/creating-sandbox-program.md)
