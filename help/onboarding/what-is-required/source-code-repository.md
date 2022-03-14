---
title: ソースコードリポジトリ —Cloud Services
description: ソースコードリポジトリ —Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 94%

---


# ソースコードリポジトリー {#source-code-repository}

Cloud Manager プログラムには、独自の Git リポジトリーが自動プロビジョニングされます。

ユーザーが Cloud Manager の Git リポジトリーにアクセスするには、コマンドラインツール、スタンドアロンのビジュアル Git クライアント、または Eclipse、IntelliJ、NetBeans などの IDE を使用する必要があります。

Git クライアントを設定すると、Cloud Manager UI から Git リポジトリーを管理できます。Cloud Manager UI を使用して Git を管理する方法については、「[Git へのアクセス](/help/implementing/cloud-manager/accessing-git.md)」を参照してください。

AEM Cloud アプリケーションの開発を開始するには、 Cloud Manager リポジトリーから、リポジトリーを作成するローカルコンピューター上の場所にアプリケーションコードのローカルコピーをチェックアウトして、作成する必要があります。

```java
$ git clone {URL}
```

>[!NOTE]
>
>ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリーで変更を行うことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリーにコミットして戻すことができます。
