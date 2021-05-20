---
title: ソースコードリポジトリ —Cloud Services
description: ソースコードリポジトリ —Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 23%

---


# ソースコードリポジトリ {#source-code-repository}

Cloud Managerプログラムには、独自のGitリポジトリが自動プロビジョニングされます。

ユーザーがCloud ManagerのGitリポジトリにアクセスするには、コマンドラインツール、スタンドアロンのビジュアルGitクライアント、またはEclipse、IntelliJ、NetBeansなどのユーザーのIDEを使用する必要があります。

Gitクライアントを設定したら、Cloud Manager UIからGitリポジトリを管理できます。 Cloud Manager UIを使用してGitを管理する方法については、[Git](/help/implementing/cloud-manager/accessing-git.md)へのアクセスを参照してください。

AEM Cloudアプリケーションの開発を開始するには、 Cloud Managerリポジトリーから、リポジトリを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして、作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>
>ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリで変更をおこなうことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリにコミットして戻すことができます。
