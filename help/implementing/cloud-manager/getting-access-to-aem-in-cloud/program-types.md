---
title: プログラムとプログラムタイプについて
description: Cloud Manager の階層、その構造に様々な種類のプログラムが収まる仕組み、それらのプログラムの違いなどについて説明します。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: ht
source-wordcount: '533'
ht-degree: 100%

---


# プログラムとプログラムタイプについて {#understanding-programs}

Cloud Manager は、エンティティ階層を軸に構築されています。その詳細は、Cloud Manager での日常業務にとって重要ではありませんが、概要はプログラムを理解し独自のプログラムをセットアップするうえで役に立ちます。

![Cloud Manager の階層](assets/program-types1.png)

* **テナント** - これは階層の最上位です。すべての顧客にテナントがプロビジョニングされます。
* **プログラム** - 各テナントには 1 つ以上のプログラムがあります。これらは、[多くの場合、顧客がライセンスを取得したソリューションを反映しています](introduction-production-programs.md)。
* **環境** - 各プログラムには複数の環境があります。ライブコンテンツ用の実稼働環境、ステージングの環境、開発目的の環境などです。
   * 各プログラムでは、実稼動環境は 1 つだけですが、実稼働以外の環境は複数存在できます。
* **リポジトリ** - プログラムには Git リポジトリがあり、そこで環境のアプリケーションとフロントエンドコードが維持管理されています。
* **ツールとワークフロー** - パイプラインはリポジトリから環境へのコードのデプロイメントを管理し、他のツールはログへのアクセス、監視および環境管理を可能にします。

多くの場合、この階層を具体的に説明するうえで例が役に立ちます。

* WKND Travel and Adventure Enterprises は、旅行関連のメディアに重点を置いた&#x200B;**テナント**&#x200B;とします。
* WKND Travel and Adventure Enterprises テナントには、2 つの **プログラム**&#x200B;があるとします。WKND Magazine 用の 1 つの Sites プログラムと WKND Media 用の 1 つの Assets プログラムです。
* WKND Magazine プログラムにも WKND Media プログラムにも、開発、ステージング、実稼動の各&#x200B;**環境**&#x200B;があります。

## ソースコードリポジトリ {#source-code-repository}

Cloud Manager プログラムには、独自の Git リポジトリが自動的にプロビジョニングされます。

Cloud Manager の Git リポジトリにアクセスするには、ユーザーは、コマンドラインツールを持つ Git クライアント、スタンドアロンのビジュアル Git クライアントまたはユーザーが選択した IDE（Eclipse、IntelliJ、NetBeans など）を使用する必要があります。

Git クライアントをセットアップすると、Cloud Manager UI から Git リポジトリを管理できます。Cloud Manager UI を使用して Git を管理する方法については、[Git へのアクセス](/help/implementing/cloud-manager/managing-code/accessing-repos.md)のドキュメントを参照してください。

AEM Cloud アプリケーションの開発を開始するには、Cloud Manager リポジトリからローカルコンピューター上の場所にチェックアウトして、アプリケーションコードのローカルコピーを作成する必要があります。

```java
$ git clone {URL}
```

したがって、ワークフローは次のような標準の Git ワークフローになります。

1. ユーザーが Git リポジトリのローカルコピーを複製します。
1. ユーザーがローカルコードリポジトリに変更を加えます。
1. 準備が整ったら、ユーザーが変更内容を元のリモート Git リポジトリにコミットします。

唯一の違いは、リモート Git リポジトリが Cloud Manager の一部になっており、開発者に対して透過的である点です。

## プログラムの種類 {#program-types}

ユーザーは、**実稼動**&#x200B;プログラムまたは&#x200B;**サンドボックス**&#x200B;プログラムを作成できます。

* **実稼動プログラム**&#x200B;は、サイトのライブトラフィックを有効にするために作成されます。
   * 詳しくは、[実稼動プログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)のドキュメントを参照してください。
* **サンドボックスプログラム**&#x200B;は、通常、トレーニング、デモの実行、イネーブルメント、POC またはドキュメントの目的にかなうように作成されます。
   * サンドボックス環境はライブトラフィックを実行するためのものではなく、実稼動プログラムにはない制限事項があります。
   * Sites と Assets が含まれており、サンプルコード、開発環境および実稼動以外のパイプラインを含んだ Git ブランチが自動生成されて提供されます。
   * 詳しくは、[サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)のドキュメントを参照してください。
