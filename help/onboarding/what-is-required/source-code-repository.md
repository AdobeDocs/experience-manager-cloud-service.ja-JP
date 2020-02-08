---
title: ソースコードリポジトリ — クラウドサービス
description: ソースコードリポジトリ — クラウドサービス
translation-type: tm+mt
source-git-commit: 6f323f33663f83043eb8a15fe00e6ed872c3cac1

---


# ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムは、独自のgitリポジトリで自動プロビジョニングされます。

ユーザーがCloud Managerのgitリポジトリにアクセスするには、Gitクライアントとコマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントが設定されると、Cloud Manager UIからgitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、Gitへのアクセスを参照し [てください](/help/implementing/cloud-manager/accessing-git.md)。

AEM cloudアプリケーションの開発を開始するには、アプリケーションコードのローカルコピーをCloud Managerリポジトリから、リポジトリを作成するローカルコンピューター上の場所にチェックアウトして作成する必要があります。

```java
$ git clone {URL}
```

> [!NOTE]
> ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更を行うことができます。 準備が整ったら、ユーザーはコードの変更をCloud Managerのリモートコードリポジトリにコミットして戻すことができます。
