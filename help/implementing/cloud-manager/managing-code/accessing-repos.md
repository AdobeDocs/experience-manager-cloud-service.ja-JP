---
title: リポジトリへのアクセス
description: Cloud Manager でセルフサービスの Git アカウント管理を使用して、Git リポジトリにアクセスして管理する方法について説明します。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 1b24fa084577f2ba0dc718ee35d12e42ac9d609c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 85%

---


# リポジトリへのアクセス {#accessing-repos}

Cloud Manager でセルフサービスの Git アカウント管理を使用して、Git リポジトリにアクセスして管理する方法について説明します。

## セルフサービスのリポジトリアカウント管理の使用 {#self-service-repos}

Cloud Manager では、パイプラインカードの目立つ位置にある「**リポジトリ情報にアクセス**」ボタンを使用して、リポジトリ情報を簡単に取得できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**リポジトリ情報にアクセス**」ボタンを見つけて、Git リポジトリにアクセスして管理します。

   ![環境カードの「リポジトリ情報にアクセス」ボタン](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 「**リポジトリ情報を表示**」ボタンをクリックして、以下を表示するダイアログを開きます。

   * Cloud Manager Git リポジトリへの URL。
   * Git ユーザー名。
   * Git パスワード。この値は、「**パスワードを生成**」ボタンをクリックすると表示されます。

   ![リポジトリ情報を表示](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

これらの資格情報を使用して、リポジトリのローカルコピーを複製し、そのローカルリポジトリで変更を加えることができます。変更できたら、Cloud Manager のリモートコードリポジトリにコードの変更をコミットして戻すことができます。

「**リポジトリ情報にアクセス**」オプションは、**パイプライン**&#x200B;カードの「**非実稼動**」パイプラインタブでも利用できます。

![「非実稼動」タブの「リポジトリ情報にアクセス」ボタン](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>「**リポジトリ情報にアクセス**」オプションは、**開発者**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーに表示されます。

## アクセスパスワードの取り消し {#revoke-password}

アクセスパスワードはいつでも失効させることができます。 それには、 [このリクエストのサポートチケットを作成します。](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

チケットは優先度が高く処理され、1 日以内に取り消される必要があります。
