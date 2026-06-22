---
title: プログラムとプログラムタイプ
description: Cloud Manager の階層、その構造に様々な種類のプログラムが収まる仕組み、それらのプログラムの違いなどについて説明します。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 01db3bdabcbdcc8256b80841cf6fa84e4726c0a2
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 75%

---


# プログラムとプログラムタイプ {#understanding-programs}

Cloud Managerは、エンティティの階層として構成されます。 詳細は、Cloud Managerの日常業務に欠かせないものです。プログラムの概要を理解し、独自のテンプレートを設定するのに役立ちます。

![Cloud Manager の階層](assets/program-types1.png)

* **テナント** - これは階層の最上位です。 すべての顧客にテナントがプロビジョニングされます。
* **プログラム** - 各テナントには 1 つ以上のプログラムがあります。[これらは、多くの場合、顧客がライセンスを取得したソリューションを反映しています](introduction-production-programs.md)。
* **環境** - 各プログラムには複数の環境があります。ライブコンテンツ用の実稼働環境、ステージングの環境、開発目的の環境などです。
   * 各プログラムでは、本番環境は 1 つだけですが、実稼働以外の環境は複数存在できます。
* **リポジトリ** - プログラムには Git リポジトリがあり、そこで環境のアプリケーションとフロントエンドコードが維持管理されています。
* **ツールとワークフロー** - パイプラインはリポジトリから環境へのコードのデプロイメントを管理し、他のツールはログへのアクセス、監視および環境管理を可能にします。

多くの場合、この階層を具体的に説明するうえで例が役に立ちます。

* WKND Travel and Adventure Enterprisesは、旅行関連のメディアに重点を置いた&#x200B;**テナント**&#x200B;です。
* WKND Travel and Adventure Enterprises テナントには、WKND Magazine用の1つのSites プログラムとWKND Media用の1つのAssets プログラムの2つの&#x200B;**プログラム**&#x200B;があります。
* WKND MagazineおよびWKND Media プログラムには、開発、ステージ、および実稼動&#x200B;**環境**&#x200B;があります。

## ソースコードリポジトリ {#source-code-repository}

Cloud Manager プログラムには、独自の Git リポジトリが自動的にプロビジョニングされます。

ユーザーは、コマンドラインツールを備えた Git クライアントまたはスタンドアロンのビジュアル Git クライアントを使用して、Cloud Manager Git リポジトリにアクセスできます。 また、Eclipse、IntelliJ、NetBeans など、好みの統合開発環境（IDE）を使用することもできます。

Git クライアントをセットアップすると、Cloud Manager ユーザーインターフェイスから Git リポジトリを管理できます。 Cloud Manager ユーザーインターフェイスを使用してGitを管理する方法については、[Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)へのアクセスを参照してください。

AEM Cloud アプリケーションの開発を開始するには、Cloud Manager リポジトリからローカルコンピューターにアプリケーションコードをチェックアウトします。

```java
$ git clone {URL}
```

標準的な Git プロセスに従ったワークフローを以下に示します。

1. ユーザーがリモート Git リポジトリをローカルにクローンします。
1. ユーザーがローカルリポジトリに変更を加えます。
1. 準備が整ったら、ユーザーは変更内容をリモート Git リポジトリにコミットします。

唯一の違いは、リモート Git リポジトリがCloud Managerの一部であり、開発者には表示されないことです。

## プログラムタイプ {#program-types}

ユーザーは、**実稼動**&#x200B;プログラムまたは&#x200B;**サンドボックス**&#x200B;プログラムを作成できます。

* **実稼動プログラム**&#x200B;は、サイトのライブトラフィックを有効にするために作成されます。
   * 詳しくは、[実稼動プログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。
* **サンドボックスプログラム**&#x200B;は、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されます。
   * サンドボックス環境はライブトラフィックを実行するためのものではなく、実稼動プログラムにはない制限事項があります。
   * Sites、Assets、Edge Delivery Services が含まれており、サンプルコード、開発環境および実稼動以外のパイプラインを含む Git 分岐が事前設定されています。
   * 詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。
