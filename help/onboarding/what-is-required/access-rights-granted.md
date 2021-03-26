---
title: アクセス権が付与された — 必要なもの
description: アクセス権が付与された — 必要なもの
translation-type: tm+mt
source-git-commit: 8259bf4e7f2004d76fd985ec7ad7c416b6f8d491
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 50%

---


# アクセス権の付与 {#access-rights-granted}

Adobeは、AdobeIdentity Managementシステム(IMS)に、会社の&#x200B;**組織** IDを作成します。このIDでは、すべてのユーザーとユーザーの権限を管理できます。 この組織のメンバーである必要があり、[!UICONTROL Experience Cloud]サービスへのアクセスを許可される各ユーザーは、独自の&#x200B;**Adobe ID**&#x200B;を持つ必要があります。

## ユーザーの ID タイプ {#user-identity-types}

Adobe ID の使用を開始するには、[Adobe ID タイプの管理](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照して、使用可能ないずれかの ID タイプを使用して Adobe ID を取得する方法の詳細を確認してください。

## ユーザーとロール {#users-and-roles}

会社の組織 ID が作成されたら、指定した管理者がこの組織の最初のメンバーとして追加されます。管理者には、デフォルトで管理者権限が付与され、[!UICONTROL AEM Managed Services] **Product** および 1 つ以上の [!UICONTROL Cloud Manager] **製品プロパティ**&#x200B;が割り当てられます。

1. システム管理者からCloud Managerへのアクセス権が付与されると、Cloud Managerのログインページが表示されます。このページは[Adobe Experience Cloud](https://my.cloudmanager.adobe.com/)からもアクセスできます。

1. Cloud Managerのランディングページで、「**アクセスを管理**」をクリックします。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. 「**アクセスを管理**」をクリックすると、**Admin Console**&#x200B;に移動します。ここから、Cloud Managerへのユーザーの役割や権限を管理できます。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   Admin Consoleから、次のようなSysAdminタスクを実行できます。
   * [ロールの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [作成者インスタンスへのアクセスの管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

      >[!NOTE]
      >Cloud Managerのユーザーとロールの定義について詳しくは、[ユーザーとロール](#users-roles)の節を参照してください。

これらの権限を付与されると、管理者は、シングルサインオン（Adobe ID を使用）で [!UICONTROL Experience Cloud] サービスへのアクセス、AEM クラウド環境へのログイン、[!UICONTROL Cloud Manager] の使用をおこなえるように設定されます。

[!UICONTROL Cloud Manager] の多くの機能には、使用するための特定の権限が必要です。

[!UICONTROL Cloud Manager] では、現在、特定の機能を使用できるかどうかを制御する次の 4 つのユーザーロールを定義しています。

* ビジネスオーナー
* プログラムマネージャー
* デプロイメントマネージャー
* デベロッパー

>[!CAUTION]
>[!UICONTROL Cloud Manager]を使用するには、Cloud Service製品コンテキストとして、Adobe IDとAdobe Experience Managerが必要です。

### ロールの定義 {#role-definitions}

>[!NOTE]
>
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

