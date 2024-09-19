---
title: Cloud ManagerでのEdge Delivery サイトの管理
description: Edge Delivery サイトに CDN 設定を追加する方法や、Edge Delivery サイトを削除する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e28e4bf06c28f97d665e5fd86ab87d484116504f
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---

# Cloud ManagerでEdge Delivery サイトを管理する {#manage-edge-delivery-sites}

CDN 設定を既存のサイトに追加して、Cloud ManagerでEdge Delivery サイトを管理する方法を説明します。 または、Edge Delivery サイトを削除します。

## 既存のEdge Delivery サイトへの CDN 設定の追加 {#add-cdn-to-edge-delivery-site}

[CDN 設定の追加 ](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) を参照してください。

## Edge Delivery サイトの名前の変更（#rename-edge-delivery-site）

Cloud ManagerのAdobeでは、次のようないくつかの理由でEdge Delivery サイトの名前を変更する必要があります。

* **明確さと組織**：サイトの目的や関連する環境（実稼働、ステージングなど）をわかりやすく説明します。
* **混乱を避ける**：複数のサイトを使用している場合、名前を変更すると、サイト間の区別が容易になり、設定や更新が間違ったサイトに適用される可能性を減らすことができます。
* **標準化**：組織のガイドラインに従った一貫性のある命名規則に従い、管理と監査を容易にします。

**Edge Delivery サイトの名前を変更するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されているプログラムを選択します。このプログラムに、Edge Delivery サイトを追加します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 Edge Delivery サイトのテーブルで、サイト名を変更する行の最後にある省略記号をクリックします。
**名前変更** をクリックします。
   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。
Edge Delivery サイトのテーブルで、サイト名を変更する行の最後にある省略記号をクリックします。 **名前変更** をクリックします。

1. **Edge Delivery サイトを編集** ダイアログボックスの **サイト名** テキストフィールドに、サイトの新しい名前を入力します。

1. 「**編集**」をクリックします。

## Edge Delivery サイトを削除する {#delete-edge-delivery-site}

Edge Delivery Servicesサイトを削除すると、関連する CDN 設定もすべて削除されます。 このアクションにより、カスタムドメインとサイトの間の接続が切断されます。 詳しくは、CDN 設定を参照してください。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Edge Delivery サイトを削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されているプログラムを選択します。このプログラムに、Edge Delivery サイトを追加します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。 Edge Deliveryのサイトテーブルで、サイトを削除する行の最後にある省略記号をクリックします。
**削除** をクリックし、もう一度 **削除** をクリックしてサイトの削除を確認します。

     ![ 「Edge Delivery」タブからEdge Delivery サイトを追加する ](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * ページの左上隅にあるハンバーガーアイコンをクリックして、左側のナビゲーションメニューを表示します。 **サービス** 見出しの下の **Edge Delivery Sites** をクリックします。
Edge Deliveryのサイトテーブルで、サイトを削除する行の最後にある省略記号をクリックします。 **削除** をクリックし、もう一度 **削除** をクリックしてサイトの削除を確認します。


     ![ 「Edge Delivery サイト」ボタンから「Edge Delivery サイトを追加」 ](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## サポートチケットを記録 {#eds-support-ticket}

{{support-ticket}}


