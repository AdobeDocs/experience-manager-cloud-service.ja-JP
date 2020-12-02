---
title: ソースコードリポジトリ —Cloud Services
description: ソースコードリポジトリ —Cloud Services
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 23%

---


# ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムは、独自のgitリポジトリで自動プロビジョニングされます。

ユーザーがCloud Managerのgitリポジトリにアクセスするには、Gitクライアントとコマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントを設定すると、Cloud Manager UIからgitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセスを参照してください。

AEM Cloudアプリケーションの開発を開始するには、Cloud Managerリポジトリから、リポジトリを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>
>ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更をおこなうことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリにコミットして戻すことができます。
