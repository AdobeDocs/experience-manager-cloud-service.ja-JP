---
title: AEM AssetsをCreative Cloudに接続
description: AEM Assetsを設定し、Creative Cloudに接続する方法を説明します。 AEM Assetsでの最新のCreative Cloud統合 (Express やCreative Cloudライブラリなど ) を簡単に使用できるように、別の IMS 組織にプロビジョニングされたCreative Cloud権限に接続します。
source-git-commit: 8c0c01be301ccaeac4e658c16d63227e55b67fcf
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# AEM AssetsをCreative Cloudに接続  {#cross-org-entitlements}

Experience Manager Assetsは、異なる IMS 組織にプロビジョニングされたCreative Cloud権限に接続して、AEM Assetsでの最新のCreative Cloud統合 (Express ライブラリやCreative Cloudライブラリなど ) を簡単に使用できます。

Creative Cloud製品とAEM Assetsが別々の IMSCreative Cloudにプロビジョニングされている場合、別の組織に接続して、2 つのソリューション間で統合ワークフローを実行できます。

## 前提条件 {#prerequisites}

* Experience Manager Assetsに対する管理者権限

* Creative CloudとExperience Managerの間で使用されるのと同じユーザー ID のCreative Cloudに対するアクティブな権限。 同じ E メールアドレスを持つ個人 ID と Federated ID に対する使用権限は、異なるユーザー ID として扱われます。

## 新しいCreative Cloud組織に接続 {#connect-to-creative-cloud-org}

新しいCreative Cloud組織に接続するには、次の手順を実行します。

1. に移動します。 **[!UICONTROL 設定]** > **[!UICONTROL Creative Cloud]**.

1. 次を使用して新しいCreative Cloud組織を選択します： **[!UICONTROL 新しいCreative Cloud組織 ID を選択]** 」ドロップダウンリストから選択できます。 リストには、アクセス権を持つすべての組織が表示されます。 アクティブなCreative Cloud権限を持つ組織を選択します。

1. クリック **[!UICONTROL 組織を切り替え]** をクリックして、新しい組織に切り替えます。

   ![組織をまたぐ権利](assets/cross-org-entitlements.png)

## 制限事項 {#limitations}

* 一度にAEM Assetsを 1 つのCreative Cloud組織に接続できます。 一度に複数のCreative Cloud組織に接続することはできません。

* AEM Assets内で接続するCreative Cloud組織は、組織内のすべてのユーザーに適用できます。

