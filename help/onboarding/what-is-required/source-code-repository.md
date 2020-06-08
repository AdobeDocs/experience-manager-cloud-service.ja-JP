---
title: ソースコードリポジトリ — クラウドサービス
description: ソースコードリポジトリ — クラウドサービス
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 23%

---


# ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムは、独自のgitリポジトリで自動プロビジョニングされます。

ユーザーがCloud Managerのgitリポジトリにアクセスするには、Gitクライアントとコマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントを設定すると、Cloud Manager UIからgitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、Gitへの [アクセスを参照してください](/help/implementing/cloud-manager/accessing-git.md)。

AEM Cloudアプリケーションの開発を開始するには、Cloud Managerリポジトリから、リポジトリを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>
> ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更をおこなうことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリにコミットして戻すことができます。
