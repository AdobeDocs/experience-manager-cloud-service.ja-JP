---
title: Cloud Manager とクイックサイト作成ワークフローについて
description: Cloud Manager と、新しいクイックサイト作成プロセスとの結び付けについて説明します。
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---


# Cloud Manager とクイックサイト作成ワークフローについて {#understand-cloud-manager}

Cloud Manager と、新しいクイックサイト作成プロセスとの結び付けについて説明します。

>[!TIP]
>
>自分の役割がフロントエンド開発のみである場合は、この記事にスキップできます。 [Git リポジトリのアクセス情報の取得](retrieve-access.md) このジャーニー内。
>
>AEM管理者（Cloud Manager 管理者）が、フロントエンド開発と管理者の両方のタスクを担当している場合、またはAEMのフロントエンド開発のエンドツーエンドプロセスを理解したい場合は、現在のドキュメントを引き続き読み、このジャーニーを続行します。

## 目的 {#objective}

このドキュメントでは、AEMクイックサイト作成ツールの仕組みとエンドツーエンドのフローの概要を説明します。 ドキュメントを読めば、以下が可能です。

* AEM Sitesと Cloud Manager が連携してフロントエンド開発を容易にする仕組みを理解する
* フロントエンドのカスタマイズの手順がAEMと完全に切り離され、AEMに関する知識が不要なことを確認します。

このドキュメントでは、設定を開始するジャーニーの次のステップに進む前に、クイックサイト作成ソリューションのこれらの基本的な要素を理解することに焦点を当てています。

このジャーニーを順を追って進めることをお勧めしますが、既にAEM Sitesと Cloud Manager が連携し、設定を直接開始することを理解している場合は、次の操作を実行できます。 [ジャーニーの次のステップにスキップします。](create-site.md)

## 担当ロール {#responsible-role}

このジャーニーの部分は、AEM管理者と Cloud Manager 管理者の両方に適用されます。

## 要件と前提条件 {#requirements-prerequisites}

クイックサイト作成ツールを使用してサイトの作成とカスタマイズを開始する前に、いくつかの要件があります。

このジャーニーは、フロントエンド開発者、管理者、およびすべての役割の組み合わせを対象としているので、すべての役割の要件を以下に示します。

フロントエンド開発者は、AEMへのアクセスや知識が必要ないことを理解することが重要です。

### 知識 {#knowledge}

| 知識 | 役割 |
|---|---|
| フロントエンド開発の標準ツールとプロセスに関する理解 | フロントエンド開発者 |
| AEMでサイトを作成および管理する方法に関する基本的な知識 | AEM 管理者 |
| Cloud Manager の基本知識 | Cloud Manager 管理者 |

フロントエンド開発者にとって、AEMに関する知識は必要ありません。

### ツール {#tools}

| ツール | 役割 |
|---|---|
| 優先フロントエンド開発環境 | フロントエンド開発者 |
| npm モジュール。 | フロントエンド開発者 |
| webpack | フロントエンド開発者 |
| Cloud Manager へのアクセス | Cloud Manager 管理者 |
| メンバーになる **ビジネスオーナー** Cloud Manager での役割 | Cloud Manager 管理者 |
| Cloud Manager のシステム管理者になる | Cloud Manager 管理者 |
| Admin Consoleへのアクセス | Cloud Manager 管理者 |
| のメンバーである **デプロイメントマネージャー** Cloud Manager での役割 | Cloud Manager 管理者 |
| のメンバーである **デプロイメントマネージャー** Cloud Manager での役割 | フロントエンド開発者 |

フロントエンド開発者は、AEMを使用する必要はありません。

>[!TIP]
>
>Cloud Manager の役割と役割の管理に詳しくない場合は、 [その他のリソース](#additional-resources) 」セクションに入力します。

## Cloud Manager {#cloud-manager}

Cloud Manager は、AEM as a Cloud Serviceの必須コンポーネントで、プラットフォームの単一のエントリポイントとして機能します。

エンタープライズ開発の設定をおこなうお客様をサポートするために、AEM as a Cloud Serviceは Cloud Manager とその専用の CI/CD パイプラインと完全に統合されています。 クイックサイト作成ツールは、専用のフロントエンド開発パイプラインをサポートするために、これらの機能を拡張します。

このジャーニーの目的上、Cloud Manager に関する完全な理解は必要ありません。 Cloud Manager の概要は、複数のレベルの構造で構成されます。

![Cloud Manager の構造](assets/cloud-manager-structure.png)

* **テナント**  — すべての顧客にテナントがプロビジョニングされます。 **WKND Travel and Adventure Enterprises** テナントの可能性があります。
* **プログラム**  — 各テナントには 1 つ以上のプログラムがあります。 この **WKND Travel and Adventure Enterprises** テナントは **WKND Nightlife** および **WKND Afton Projects** プログラム。
* **環境**  — 各プログラムには、実稼動コンテンツ用の実稼動環境や、開発目的のステージング環境および開発環境など、複数の環境があります。 **WKND Nightlife** および **WKND Afton Projects** プログラムには、開発環境、ステージ環境、実稼動環境の両方があります。
* **リポジトリ**  — 環境には git リポジトリがあり、アプリケーションとフロントエンドコードが維持されています。
* **ツールとワークフロー**  — パイプラインは、リポジトリから環境へのコードのデプロイメントを管理します。

## クイックサイト作成フロントエンド開発フロー {#flow}

全体的なフローは、Cloud Manager に関する豊富な経験をまだ持っていなくても、シンプルで直感的です。

1. AEM管理者はAEM環境にサインインし、サイトテンプレートを使用して新しいサイトを作成します。
1. Cloud Manager 管理者が、Cloud Manager でフロントエンドパイプラインを作成します。 パイプラインは、Git リポジトリからAEM環境へのコードのデプロイメントを調整します。
1. AEM管理者が、プログラムのAEMインスタンスからサイトテーマを書き出し、フロントエンド開発者に提供します。
1. Cloud Manager 管理者は、カスタマイズをコミットできるAEM Git リポジトリーに対するフロントエンド開発者アクセスを許可します。
1. フロントエンド開発者は、Git およびパイプラインにアクセスするためのアクセス資格情報を取得します。
1. フロントエンド開発者はテーマをカスタマイズし、プロキシを使用してサイトの実際のコンテンツを使用してテストし、その変更を Git リポジトリにコミットします。
1. フロントエンド開発者は、パイプラインを実行して、テーマのカスタマイズをプログラムの実稼動環境にデプロイします。

![クイックサイト作成フロー](assets/qsc-flow.png)

クイックサイト作成ツールを使用する主な利点は、純粋なフロントエンド開発者が実際のカスタマイズのみを担当することです。 フロントエンド開発者は、AEMとのやり取りがなく、AEMに関する知識が必要です。

## 次の手順 {#what-is-next}

これで、AEM Quick Site Creation ジャーニーのこの部分が完了し、次の作業をおこなう必要があります。

* AEM Sitesと Cloud Manager が連携してフロントエンド開発を容易にする仕組みを理解する
* フロントエンドのカスタマイズの手順がAEMと完全に切り離され、AEMに関する知識が不要なことを確認します。

この知識に基づいてドキュメントを次に確認し、AEMクイックサイト作成のジャーニーを続行します [テンプレートからサイトを作成し、](create-site.md) ここでは、テンプレートを使用して新しいAEMサイトをすばやく作成する方法について説明します。

## その他のリソース {#additional-resources}

クイックサイト作成ジャーニーの次の部分に進むことをお勧めしますが、ドキュメントを確認してください [テンプレートからサイトを作成し、](create-site.md) 以下に、このドキュメントで取り上げたいくつかの概念について詳しく説明する、その他のオプションのリソースを示します。ただし、このジャーニーを続行する必要はありません。

* [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Cloud Manager の機能の詳細については、詳細な技術ドキュメントを直接お問い合わせください。
* [ロールに基づく権限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager には、適切な権限を持つ事前設定済みのロールが用意されています。 これらの役割の詳細と管理方法については、このドキュメントを参照してください。
* [npm](https://www.npmjs.com) - AEMテーマを使用してサイトをすばやく作成する場合は、npm に基づきます。
* [webpack](https://webpack.js.org) - AEMテーマは、webpack に依存するサイトをすばやく構築するために使用します。
