---
title: DNS レコードのステータスの確認
description: Cloud Manager を使用して、DNS 設定が正しく解決されているかどうかを判断する方法について説明します。
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 17%

---

# DNS レコードのステータスの確認 {#check-dns-record-status}

Cloud Manager 内では、ドメイン名がAEMas a Cloud Serviceの Web サイトに正しく解決されているかどうかを判断できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 次に移動： **環境** 画面から **概要** ページ。

1. クリック **ドメイン設定** をクリックします。

1. 次をクリック： **ステータス** ドメイン名のアイコン。

Cloud Manager は、ドメイン名の DNS ルックアップを実行し、次のいずれかのステータスメッセージを表示します。

* **DNS ステータスが検出されませんでした**  — カスタムドメイン名が正常に検証およびデプロイされるまで、DNS ステータスは検出されません。

   * このステータスは、カスタムドメイン名が削除中の場合にも表示されます。

* **DNS が正しく解決されません**  — これは、DNS レコードの設定が解決されていないか、エラーが発生していることを示します。

   * ドキュメントを参照します。 [DNS 設定の構成](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) を参照してください。
   * 準備が整ったら、 **再解決** ステータスの横のアイコン

* **DNS 解決が進行中です**  — 解決が進行中です。

   * このステータスは、通常、 **再解決** ステータスの横のアイコン

* **DNS が正しく解決されました** - DNS 設定が正しく構成されています。

   * サイトは訪問者にサービスを提供しています。

カスタムドメイン名が最初に正常に検証およびデプロイされると、Cloud Manager は DNS 参照を自動的にトリガーします。 その後の試行では、 **再解決** ステータスの横のアイコン
