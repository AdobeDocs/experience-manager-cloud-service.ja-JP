---
title: プログラムとプログラムのタイプについて
description: プログラムとプログラムのタイプについて —Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 13%

---


# プログラムとプログラムの種類について {#understanding-programs}

Cloud Managerでは、最上部にテナントエンティティがあり、このエンティティ内に複数のプログラムを含めることができます。 各プログラムには、1つの実稼働環境と複数の非実稼働環境を含めることができます。

次の図に、Cloud Managerのエンティティの階層を示します。

![画像](assets/program-types1.png)

## ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムは、独自のgitリポジトリで自動プロビジョニングされます。

ユーザーがCloud Managerのgitリポジトリにアクセスするには、Gitクライアントとコマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントを設定すると、Cloud Manager UIからgitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセスを参照してください。

AEM Cloudアプリケーションの開発を開始するには、Cloud Managerリポジトリから、リポジトリを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更をおこなうことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリにコミットして戻すことができます。

## プログラムタイプ{#program-types}

ユーザーは、**Sandbox**&#x200B;または&#x200B;**Production**&#x200B;プログラムを作成できます。

* *本番プログラム*が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。
詳しくは、[実稼働プログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。


* *Sandboxプログラム*は、通常、トレーニング、デモ、有効化、POC、ドキュメントの実行の目的で作成されます。 ライブトラフィックを運ぶことを目的としたものではなく、実稼動プログラムが行わないという制限が課されます。 サイトとアセットが含まれ、サンプルコード、開発環境、非実稼働パイプラインを含むGitブランチが自動入力されて配信されます。
詳しくは、[Sandboxプログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。

