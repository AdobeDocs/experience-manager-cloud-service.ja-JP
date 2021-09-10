---
title: リポジトリーへのアクセス
seo-title: Accessing Repositories
description: このページでは、Git リポジトリーにアクセスして管理する方法について説明します。
seo-description: Follow this page to learn how to access and manage your Git repository.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 97%

---

# リポジトリーへのアクセス {#accessing-repos}

Cloud Manager UI のセルフサービス Git アカウント管理を使用して、Git リポジトリーにアクセスし、管理できます。

## セルフサービスリポジトリーのアカウント管理の使用 {#self-service-repos}

Cloud Manager UI から利用できる「**リポジトリー情報にアクセス**」ボタンを使用します。このボタンはパイプラインカードで最も目立つ場所にあります。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動します。

1. Git リポジトリーにアクセスして管理するための「**リポジトリー情報にアクセス**」オプションが表示されます。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

   さらに、「**実稼動以外**」パイプラインタブを選択すると、そこにも「**リポジトリー情報にアクセス**」オプションが表示されます。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >「**リポジトリー情報にアクセス**」オプションは、デベロッパーまたはデプロイメントマネージャーの役割を持つユーザーに表示されます。このボタンをクリックすると、Cloud Manager Git リポジトリーへの URL およびユーザー名とパスワードを確認できるダイアログが開きます。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

   Cloud Manager で Git を管理するうえで重要な考慮事項は次のとおりです。

   * **URL**：リポジトリーの URL
   * **ユーザー名**：ユーザー名
   * **パスワード**：「**パスワードを生成**」ボタンをクリックしたときに表示される値。


      >[!NOTE]
      >ユーザーは、自分のコードのコピーをチェックアウトし、ローカルコードリポジトリーで変更を行うことができます。準備ができたら、ユーザーはコードの変更内容を Cloud Manager のリモートコードリポジトリーにコミットして戻すことができます。
