---
title: プログラムとプログラムの種類について
description: プログラムとプログラムの種類について - Cloud Services
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 63%

---

# プログラムとプログラムの種類について {#understanding-programs}

Cloud Manager では、最上位にテナントエンティティがあり、このエンティティ内に複数のプログラムを含めることができます。各プログラムには、1 つの実稼動環境と複数の非実稼動環境を含めることができます。

次の図に、Cloud Manager のエンティティの階層を示します。

![画像](assets/program-types1.png)

## ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムには、独自のGitリポジトリが自動プロビジョニングされます。

ユーザーがCloud ManagerのGitリポジトリにアクセスするには、コマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントを設定したら、Cloud Manager UIからGitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセスを参照してください。

AEM Cloudアプリケーションの開発を開始するには、 Cloud Managerリポジトリーから、リポジトリを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして、作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更をおこなうことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリにコミットして戻すことができます。

## プログラムの種類 {#program-types}

ユーザーは、**ｻサンドボックス**&#x200B;または&#x200B;**実稼動**&#x200B;プログラムを作成できます。

* *実稼動プログラム*&#x200B;が作成され、将来の適切なタイミングでライブトラフィックを利用できるようになります。詳しくは、[実稼動プログラムの概要](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)を参照してください。


* *サンドボックスプログラム*は、通常、トレーニング、デモの実行、イネーブルメント、POC、ドキュメントの実行の目的で作成されます。ライブトラフィックを運ぶことを目的としたものではなく、実稼動プログラムにはない制限が課されます。Sites と Assets が含まれ、サンプルコード、開発環境、非実稼動パイプラインを含む Git ブランチが自動生成されて配信されます。
詳しくは、[サンドボックスプログラムの紹介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)を参照してください。
