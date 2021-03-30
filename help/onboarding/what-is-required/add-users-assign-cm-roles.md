---
title: 'ユーザーの追加とCloud Managerロールの割り当て '
description: ユーザーを追加し、Cloud Managerのロールに割り当てる方法を学ぶには、このページに従います
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 33%

---


# ユーザーの追加とCloud Managerの役割の割り当て{#add-users-assign}

Adobeは、AdobeIdentity Managementシステム(IMS)に、会社の&#x200B;**組織** IDを作成します。このIDでは、すべてのユーザーとユーザーの権限を管理できます。 この組織のメンバーである必要があり、[!UICONTROL Experience Cloud]サービスへのアクセスを許可される各ユーザーは、独自の&#x200B;**Adobe ID**&#x200B;を持つ必要があります。

## ユーザーの役割について{#user-roles}

Cloud Manager の多くの機能には、使用するための特定の権限が必要です。

Cloud Manager では、現在、特定の機能を使用できるかどうかを制御する次の 4 つのユーザーロールを定義しています。

* ビジネスオーナー
* デプロイメントマネージャー
* プログラムマネージャー
* デベロッパー

>[!NOTE]
>Admin Console の「開発者」ペルソナは、[!UICONTROL Cloud Manager] の「デベロッパー」ロールとは無関係です。

ロールの概要を次の表に示します。

| [!UICONTROL Cloud Manager] のロール | 説明 |
|--- |--- |
| ビジネスオーナー | KPI の定義、実稼動デプロイメントの承認、重大な 3 層エラーのオーバーライドを担当します。 |
| プログラムマネージャー | [!UICONTROL Cloud Manager] を使用して、チームの設定、ステータスのレビュー、KPI の確認をおこないます。重大な 3 層エラーを承認することができます。 |
| デプロイメントマネージャー | デプロイメント作業を管理します。[!UICONTROL Cloud Manager] を使用して、ステージング環境または実稼動環境へのデプロイメントを実行します。CI/CD パイプラインを編集できます。重大な 3 層エラーを承認することができます。Git リポジトリにアクセスできます。 |
| デベロッパー | カスタムアプリケーションコードを開発およびテストします。主に [!UICONTROL Cloud Manager] を使用してステータスを確認します。Git リポジトリにアクセスして、コードをコミットできます。 |
| コンテンツ作成者 | 通常は、[!UICONTROL Cloud Manager] を操作しません。（[!UICONTROL Experience Cloud] からナビゲートした）[!UICONTROL Cloud Manager] プログラムスイッチャーを使用して、AEM にアクセスできます。 |

### 統合製品プロファイル{#integration-product-profile}

上記に加えて、Cloud Managerでは「Integrations -Cloud Service」という製品プロファイルが自動的に作成されます。 この製品プロファイルは、Adobe Experience Manager製品と他のAdobe製品との統合に使用されます。 この製品プロファイル&#x200B;**は削除できません。** 誤ってこのプロファイルを削除した場合は、手動で再作成する必要があります。 このプロファイルの表示名&#x200B;**は**`CM_CS_DEFAULT`でなければなりません。


## ロール定義に関連付けられている権限{#permissions}

[!UICONTROL Cloud Manager] には、適切な権限を持つ事前設定済みのロールが用意されています。例えば、デベロッパーには、開発したコードを **Git リポジトリ**&#x200B;にプッシュする権限があります。また、ビジネスオーナーには、主要業績評価指標（KPI）を定義しデプロイメントを承認できる様々な権限があります。

各ロールには、それぞれのロールに関連付けられた特定の権限があります。 次の表に、ロール、使用可能な関数のリスト、および関数を実行できるロールの概要を示します。

| 権限 | 説明 | ビジネスオーナー | デプロイメントマネージャー | プログラムマネージャー | デベロッパー |
|--- |--- |--- |--- |--- |--- |
| プログラムの追加 | 追加新しいプログラム。 | x |  |  |  |
| 環境の作成 | Prod+Stage、Dev、環境を作成します。 | x | x |  |  |
| 環境の更新 | Prod+Stage、Dev、環境を更新します。 | x | x |  |  |
| 環境を削除 | 非prod、開発、環境を削除します。 | x | x |  |  |
| パイプライン設定 | パイプラインの設定または編集を参照してください。 |  | x |  |  |
| パイプラインの実行 | パイプラインの開始。 | x | x |  |  |
| パイプラインの実行 | 重要な3層のエラーを拒否/承認します。 | x | x | x |  |
| パイプラインの実行 | GoLive 承認を提供します。 | x | x | x |  |
| パイプラインの実行 | 実稼動環境へのデプロイメントのスケジュールを設定します。 | x | x | x |  |
| パイプラインの削除 | パイプラインの削除を許可します。 |  | x |  |  |
| 実行のキャンセル | 現在の実行をキャンセル |  | x |  |  |
| 個人用アクセストークンの生成 | Git にアクセスします。 |  | x |  | x |

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
