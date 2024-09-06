---
title: DNS レコードのステータスの確認
description: Cloud Manager を使用して、DNS 設定が正しく解決されているかどうかを判断する方法について説明します。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 90%

---


# DNS レコードのステータスの確認 {#check-dns-record-status}

Cloud Manager を使用して、DNS 設定が正しく解決されているかどうかを判断する方法について説明します。

## DNS レコードのステータス {#status}

カスタムドメイン名は、DNS が正しく解決されるまで、ライブトラフィックを提供できません。Cloud Manager 内では、お使いのドメイン名が AEM as a Cloud Service の web サイトに正しく解決されているかどうかを判断できます。

## 要件 {#requirements}

Cloud Manager を使用して DNS レコードのステータスを確認する前に、次の要件を満たす必要があります。

* [DNS 設定の指定 ](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) のドキュメントに従って、カスタムドメイン名の DNS 設定を既に設定している必要があります。

## DNS レコードのステータスの確認方法 {#how-to}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」をクリックします。

1. そのドメイン名の&#x200B;**ステータス**&#x200B;アイコンをクリックします。

Cloud Managerはドメイン名に対して DNS 検索を実行し、それを表示します [ 現在のステータス ](#statuses)。

カスタムドメイン名の初期の検証と展開が正常に完了すると、Cloud Manager は自動的に DNS 検索をトリガーします。それ以降の試行では、ステータスの横にある「**もう一度解決する**」アイコンをアクティブに選択する必要があります。

## Cloud Manager の DNS ステータス {#statuses}

Cloud Manager では、カスタムドメインのステータスは次のいずれかになります。

* **DNS ステータスが検出されませんでした** - カスタムドメイン名が正常に検証およびデプロイされるまで、DNS ステータスは検出されません。

   * このステータスは、カスタムドメイン名が削除中の場合にも表示されます。

* **DNS が正しく解決されません** - これは、DNS レコードの設定が解決されていないか、間違っていることを示します。

   * 詳細については、「[DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)」を参照してください。
   * 準備が整ったら、ステータスの横にある「**もう一度解決する**」アイコンを選択する必要があります。

* **DNS 解決が進行中です** - 解決が進行中です。

   * このステータスは、通常、ステータスの横にある「**もう一度解決する**」アイコンを選択した後に表示されます。

* **DNS が正しく解決されます** - DNS 設定が正しく構成されています。

   * サイトは訪問者にサービスを提供しています。

## 次の手順 {#next-steps}

これで完了です。Cloud Manager で使用するカスタムドメインが正常に設定されました。Cloud Manager を使用してカスタムドメイン名を管理する方法について詳しくは、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)ドキュメントを参照してください。
