---
title: Edge Delivery パイプラインを追加
description: Edge Delivery パイプラインを追加して、コードをビルドし、実稼動環境にデプロイする方法を説明します。
index: true
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期導入者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: cc3023f0451e0b1d852c497714d6b46fdaed5cfe
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 45%

---


# Edge Delivery パイプラインを追加 {#configure-edge-delivery-pipeline}

本番パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。本番パイプラインは、最初にコードをステージング環境にデプロイします。承認時に、同じコードが本番環境にデプロイされます。

Edge Delivery パイプラインを設定するには、ユーザーに **[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** の役割が必要です。

>[!NOTE]
>
>この記事で説明する機能は、早期導入プログラムを通じてのみ利用できます。 詳細と早期導入者としての新規登録について詳しくは、[独自の Git の導入](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)を参照してください。