---
title: プログラムとプログラムの種類
description: Cloud Manager の階層と、様々な種類のプログラムが構造に適合する方法、およびプログラムの違いについて説明します。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# プログラムとプログラムの種類 {#understanding-programs}

Cloud Manager は、エンティティの階層を中心に構築されています。 この詳細は、Cloud Manager の毎日の作業にとって重要ではありませんが、概要は、プログラムを理解し、独自の設定に役立ちます。

![Cloud Manager の階層](assets/program-types1.png)

* **テナント**  — これは階層の最上位です。 すべての顧客にテナントがプロビジョニングされます。
* **プログラム**  — 各テナントには 1 つ以上のプログラムがあります。 [多くの場合、お客様がライセンスを取得したソリューションを反映したものです。](introduction-production-programs.md)
* **環境**  — 各プログラムには、実稼動コンテンツ用、ステージング用、開発用など、複数の環境があります。
   * 各プログラムには、1 つの実稼動環境のみを設定できますが、複数の非実稼動環境を設定できます。
* **リポジトリ** ：プログラムには git リポジトリがあり、環境用にアプリケーションとフロントエンドコードが管理されています。
* **ツールとワークフロー**  — パイプラインはリポジトリから環境へのコードのデプロイメントを管理し、他のツールはログ、監視、環境管理へのアクセスを許可します。

例は、多くの場合、この階層を文脈化する際に役立ちます。

* WKND Travel and Adventure Enterprises は、 **テナント** 旅行関連のメディアに焦点を当てています。
* WKND Travel and Adventure Enterprises テナントは、2 つの **プログラム**:WKND Magazine 向けの 1 つの Sites プログラムと WKND Media 向けの 1 つの Assets プログラムです。
* WKND Magazine と WKND Media の両方のプログラムには、開発、ステージ、実稼動が含まれます **環境**.

## ソースコードリポジトリー {#source-code-repository}

Cloud Manager プログラムには、独自の Git リポジトリが自動プロビジョニングされます。

Cloud Manager の Git リポジトリにアクセスするには、コマンドラインツール、スタンドアロンの Visual Git クライアント、または Eclipse、IntelliJ、NetBeans などのユーザーの IDE を使用して Git クライアントを使用する必要があります。

Git クライアントを設定したら、Cloud Manager UI から Git リポジトリを管理できます。 Cloud Manager UI を使用して Git を管理する方法については、このドキュメントを参照してください [Git にアクセスします。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

AEM Cloud アプリケーションの開発を開始するには、Cloud Manager リポジトリーからローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして、作成する必要があります。

```java
$ git clone {URL}
```

したがって、ワークフローは標準の Git ワークフローになります。

1. ユーザーは、Git リポジトリのローカルコピーを複製します。
1. ユーザーがローカルコードリポジトリで変更をおこないます。
1. 準備が整うと、ユーザーは変更をリモート Git リポジトリにコミットし直します。

唯一の違いは、リモート Git リポジトリが Cloud Manager に含まれていることです。Cloud Manager は開発者に対して透過的です。

## プログラムの種類 {#program-types}

ユーザーは、 **実稼動** プログラムまたは **サンドボックス** プログラム。

* A **生産計画** は、サイトのライブトラフィックを有効にするために作成されます。
   * ドキュメントを参照してください [実稼働プログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) を参照してください。
* A **サンドボックスプログラム** は、通常、トレーニング、デモの実行、イネーブルメント、POC、ドキュメントの実行の目的で作成されます。
   * サンドボックス環境は、ライブトラフィックを運ぶためのものではなく、実稼動プログラムが運用しないという制限を持ちます。
   * これには Sites と Assets が含まれ、サンプルコード、開発環境、実稼動以外のパイプラインを含む Git ブランチが自動入力されて配信されます。
   * ドキュメントを参照してください [サンドボックスプログラムの概要](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) を参照してください。
