---
title: リポジトリのアクセス情報
description: Cloud Manager でセルフサービスの Git アカウント管理を使用して、Adobeが管理する Git リポジトリにアクセスして管理する方法について説明します。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0b39fc4dcaf86d436547d3941b1f12bca8c5bc9b
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 24%

---


# リポジトリのアクセス情報 {#accessing-repos}

Cloud Manager でセルフサービスの Git アカウント管理を使用して、Adobeが管理する Git リポジトリにアクセスして管理する方法について説明します。

## 概要ページからのリポジトリ情報へのアクセス {#overview-page}

Cloud Manager では、を使用することで、Adobeが管理するリポジトリのリポジトリアクセス情報を簡単に取得できます **リポジトリ情報にアクセス** ボタンは、パイプラインカードで目立って使用できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

   ![環境カードの「リポジトリ情報にアクセス」ボタン](assets/pipelines-card.png)

1. 「」をタップまたはクリックします **リポジトリ情報にアクセス** を開くためのボタン **リポジトリ情報** ダイアログとビュー：

   * Git ユーザー名。
   * Git のパスワード。
   * Cloud Manager Git リポジトリへの URL。
   * リモートを Git リポジトリーおよびプッシュコードにすばやく追加するための、事前定義済み Git コマンド。

   ![リポジトリ情報ウィンドウ](assets/repository-info.png)

1. パスワードにアクセスするには、新しいパスワードを生成する必要があります。 それには、「」をタップまたはクリックします **パスワードを生成** ボタン。

1. でのパスワード生成の確認 **本当に…** タップまたはクリックによるダイアログ **パスワードを生成**.

   ![パスワード生成の確認](assets/confirm-password-generation.png)

1. パスワードが生成され、にコピーするために表示されます。 **パスワード** フィールド。

   * パスワードを生成すると、以前のパスワードが無効になります。
   * Cloud Manager はパスワードを保存しません。 このパスワードを安全に保存するのはユーザーの責任です。
   * Cloud Manager はパスワードを保存しないので、パスワードが失われた場合は、新しく再生成する必要があります。

   ![生成されたパスワードの例](assets/generated-password.png)

これらの資格情報を使用して、リポジトリのローカルコピーを複製し、そのローカルリポジトリで変更を加え、準備ができたら、Cloud Manager のリモートコードリポジトリにコードの変更をコミットして戻すことができます。

>[!NOTE]
>
>* 「**リポジトリ情報にアクセス**」オプションは、**開発者**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーに表示されます。
>* この **リポジトリ情報にアクセス** ボタンは、Adobeが管理するリポジトリのリポジトリ・アクセス情報のみを表示します。 に関する情報へのアクセス [プライベートリポジトリー](private-repositories.md) は、Cloud Manager では使用できません。

## 「リポジトリ」ウィンドウからのリポジトリ情報へのアクセス {#repositories-window}

An **リポジトリ情報にアクセス** ボタンはツールバーでも使用できます [**リポジトリ** ウィンドウ。](managing-repositories.md) Adobeが管理するリポジトリへのアクセスに関する同じ情報が表示されます。

## アクセスパスワードの失効 {#revoke-password}

アクセスパスワードはいつでも失効できます。これを行うには、[このリクエストに対するサポートチケットを作成](https://experienceleague.adobe.com/ja?support-solution=Experience+Manager&amp;support-tab=home#support)してください。

チケットは高い優先度で処理され、1 日以内に失効されます。
