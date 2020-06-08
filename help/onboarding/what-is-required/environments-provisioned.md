---
title: 環境のプロビジョニング — 必要なもの
description: 環境のプロビジョニング — 必要なもの
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 51%

---


# プロビジョニング済み環境 {#environments-provisioning}

## プロビジョニング {#provisioning}

お客様が購入したすべてのAEMクラウド環境は、自動的にアドビにプロビジョニングされ、Cloud Managerのプログラムにリンクされます。 これらの AEM クラウド環境は、すべての Adobe Managed Services サブスクリプションに含まれ、通常は 1 つ以上の実稼動環境、1 つのステージング環境、1 つ以上の開発環境またはテスト環境（オプション）で構成されます。

## お知らせメール {#welcome-email}

環境プロビジョニングプロセスが完了すると、Adobe Experience Cloud へのアクセス権を付与されたことを確認するお知らせメールが顧客側の指定管理者に届きます。この電子メールには、Experience Cloudサービスの使い始め方とCloud Managerセルフサービスポータルに関する詳細情報が記載されています。 また、この電子メールには、サポートリソース、フォーラム、FAQなど、重要な情報が記載されています。 電子メールに記載されているリソースの一覧で、Cloud Manager またはお使いの AEM クラウド環境にアクセスする方法の詳細もわかります。

## 次の手順 {#next-steps}

お知らせメールが届くと、Adobe IMS 資格情報を使用して管理者として Cloud Manager にログインする準備が整います。ログインすると、AEMクラウドの実稼働環境と実稼働以外の環境が使用可能で、正常に実行されていることを確認できます。

これらのAEMクラウド環境は、Cloud ManagerのGitリポジトリからステージング環境を経由し、AEM実稼働環境まで、コードをデプロイする際に、CI/CDパイプラインの実行にCloud Managerで使用されます。 また、Web プロパティのデジタルエクスペリエンスの作成を開始する準備ができたら、Cloud Manager から直接 AEM クラウド環境にアクセスできます。