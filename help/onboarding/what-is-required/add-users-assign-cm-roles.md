---
title: 'システム管理者のタスク '
description: このページで、ユーザーを追加し、システム管理者としてCloud Managerの役割に割り当てる方法を学習します
translation-type: tm+mt
source-git-commit: f1f5766a41763634e0aaba44e55471ac2ea5dc8f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# システム管理者タスク{#add-users-assign}

システム管理者は、アクセスから権限まで、ユーザーのあらゆる側面を管理します。 このユーザーは、Admin ConsoleおよびCloud Manager内でタスクを行う開始に初めてアクセスできます。
システム管理者は、次の組織タスクを実行します。

* ユーザーの追加
* Cloud Managerのロールと権限へのユーザーの割り当て

## ユーザーの追加{#add-users}

>[!NOTE]
>ユーザーを追加するには、システム管理者である必要があります。

1. システム管理者の場合は、[Admin Console](https://adminconsole.adobe.com)に移動します。 または、Cloud Managerに移動して、次に説明する「**アクセスを管理**」ボタンが表示されるようにすることもできます。

1. Cloud Managerランディングページの右上にある「アクセスを管理」ボタン&#x200B;**をクリックし、新しいタブでAdmin Consoleを開きます。**

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   **Admin Console**&#x200B;から、Cloud Managerにユーザーを追加し、Admin Consoleの製品プロファイルと呼ばれるロールに割り当てることができます。

1. 以下に示すように、**Products and services**&#x200B;カードから&#x200B;**Adobe Experience ManagerをCloud Service**&#x200B;として選択します。

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. アクションバーの「**ユーザー**」タブを選択し、「**追加ユーザー**」を選択します。

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. ユーザーを選択し、次に示すように、適切なCloud Managerロールまたは製品プロファイルをユーザーに割り当てます。

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >前述の[ユーザーの役割と権限](#user-roles)および[役割の定義に関連付けられている権限](#permissions)の節を参照し、適切なAdmin Consoleに&#x200B;****&#x200B;で適切な役割が割り当てられていることを確認してください。

   これで、ユーザーをCloud Service製品コンテキストとしてAdobe Experience Managerに追加し、適切なロールまたは製品プロファイルを使用してセットアップします。

   例えば、次の

   * ***Business Owner***：新しいプログラムに対する権限、またはプログラムの編集、環境の追加または更新、パイプラインの追加/編集/削除、パイプラインの実行、AEM環境またはコード品質へのコードのデプロイを行うことができます。

   * ***Deployment Manager***、環境の追加または更新、パイプラインの実行、AEM環境またはコード品質へのコードのデプロイを行う権限があります。

   * ***開発者***、Gitにアクセスする個人アクセストークンを生成する権限があります。

      >[!NOTE]
      > 1人のユーザーを複数のロールに割り当てることができます。 例えば、ビジネス所有者ロールとDeployment Managerロールの両方をユーザーに割り当てると、これらの権限の組み合わせまたは合計が表示されます。
