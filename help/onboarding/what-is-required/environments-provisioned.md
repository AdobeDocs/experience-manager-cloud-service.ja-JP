---
title: 環境のプロビジョニング — 必要事項
description: 環境のプロビジョニング — 必要事項
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 59%

---


# プロビジョニング済み環境 {#environments-provisioning}

## プロビジョニング {#provisioning}

顧客が購入したすべてのAEMクラウド環境は、Adobe別に自動的にプロビジョニングされ、Cloud Managerのプログラムにリンクされます。 これらの AEM クラウド環境は、すべての Adobe Managed Services サブスクリプションに含まれ、通常は 1 つ以上の実稼動環境、1 つのステージング環境、1 つ以上の開発環境またはテスト環境（オプション）で構成されます。

## お知らせメール {#welcome-email}

環境プロビジョニングプロセスが完了すると、Adobe Experience Cloud へのアクセス権を付与されたことを確認するお知らせメールが顧客側の指定管理者に届きます。この電子メールには、Experience CloudサービスとCloud Managerセルフサービスポータルの使用を開始する方法に関する詳細情報が含まれています。 さらに、この電子メールには、サポートリソース、フォーラム、FAQの入手先など、重要な情報が含まれています。 電子メールに記載されているリソースの一覧で、Cloud Manager またはお使いの AEM クラウド環境にアクセスする方法の詳細もわかります。

## 次の手順 {#next-steps}

お知らせメールが届くと、Adobe IMS 資格情報を使用して管理者として Cloud Manager にログインする準備が整います。ログインすれば、AEM クラウドの実稼動環境および非実稼動環境が使用可能で正常に動作していることを確認できます。

これらのAEMクラウド環境は、 Cloud ManagerのGitリポジトリからステージング環境を通じてAEM実稼動環境にコードをデプロイする際に、Cloud ManagerでCI/CDパイプラインを実行するために使用されます。 また、Web プロパティのデジタルエクスペリエンスの作成を開始する準備ができたら、Cloud Manager から直接 AEM クラウド環境にアクセスできます。