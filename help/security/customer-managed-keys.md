---
title: AEM as a Cloud Serviceの顧客管理キー
description: AEM as a Cloud Serviceの暗号化キーを管理する方法を学ぶ
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# AEM as a Cloud Serviceの顧客管理キーの設定 {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Serviceは現在、顧客データを Azure Blob Storage と MongoDB に保存し、デフォルトでは、プロバイダーが管理する暗号化キーを使用してデータを保護します。 この設定は多くの組織のセキュリティ要件を満たしていますが、規制対象の業界や強化されたデータ主権を必要とする企業は、暗号化方法をより詳細に制御したいと考えるかもしれません。 データのセキュリティ、コンプライアンス、および暗号化キーの管理機能に優先順位を付ける組織にとって、顧客管理キー（CMK）ソリューションは重要な機能強化です。

## 解決される問題 {#the-problem-being-solved}

プロバイダ管理キーは、厳格な規制によりデータ・セキュリティの包括的な制御が要求される金融、医療、政府機関などの分野の企業に対して懸念を生じさせます。 主要な管理を管理できない組織は、コンプライアンス要件への対応、カスタム・セキュリティ・ポリシーの導入、完全なデータ主権の確保という課題に直面しています。

顧客管理キー（CMK）の導入は、AEMのお客様が暗号化キーを完全に制御できるようにすることで、これらの懸念に対処します。 AEM CS では、Microsoft Entra ID （旧称 Azure Active Directory）を介して認証を行うことで、お客様の Azure Key Vault に安全に接続し、キーの作成、ローテーション、失効など、暗号化キーのライフサイクルを管理できます。

CMK には次のようないくつかの利点があります。

* **セキュリティの強化：** お客様は、特定のセキュリティ要件を満たす暗号化プラクティスを確保できるので、データ保護に対する安心感を得ることができます。
* **コンプライアンスの柔軟性：** 主要なライフサイクルを完全に制御することで、企業は GDPR、HIPAA、CCPA などの進化する規制基準に容易に適応でき、コンプライアンス体制を強力に保つことができます。
* **シームレスな統合：** CMK ソリューションは、AEM CS で Azure Blob Storage および MongoDB と直接統合され、ストレージ操作やユーザビリティに影響を与えることなく、強力な暗号化機能をお客様に提供します。

CMK を採用すると、お客様は、AEM CS の拡張性と柔軟性を引き続き享受しながら、データセキュリティと暗号化プラクティスに対する制御を強化し、コンプライアンスを強化し、リスクを軽減できます。

AEM as a Cloud Serviceでは、保存中のデータを暗号化するために独自の暗号化キーを持ち込むことができます。 このガイドでは、AEM as a Cloud Service用の Azure Key Vault で顧客管理キー（CMK）を設定する手順について説明します。

>[!WARNING]
>
>CMK を設定した後は、システム管理キーに戻すことはできません。 キーを安全に管理し、Azure 内で Key Vault、キー、CMK アプリへのアクセスを提供して、データへのアクセスが失われないようにする責任があります。

また、必要なインフラストラクチャを作成して設定するための次の手順も説明します。

1. 環境の設定
1. Adobeからのアプリケーション ID の取得
1. 新しいリソースグループの作成
1. キーカルトの作成
1. キーカルトへのAdobeアクセス権の付与
1. 暗号化キーの作成

Key Vault の URL、暗号化キーの名前および Key Vault に関する情報をAdobeと共有する必要があります。

## 環境のセットアップ {#setup-your-environment}

Azure コマンドラインインターフェイス（CLI）は、このガイドの唯一の要件です。 Azure CLI をまだインストールしていない場合は、公式のインストール手順 [ こちら ](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) に従ってください。

このガイドの残りの部分に進む前に、`az login` を使用して CLI にログインしてください。

>[!NOTE]
>
>このガイドでは Azure CLI を使用しますが、Azure コンソールを使用しても同じ操作を実行できます。 Azure コンソールを使用する場合は、次のコマンドを参考にしてください。

## Adobeからのアプリケーション ID の取得 {#obtain-an-application-id-from-adobe}

Adobeでは、このガイドの残りの部分で必要になる Entra アプリケーション ID を提供します。 アプリケーション ID がまだない場合は、Adobeにお問い合わせいただき、ID を取得してください。

## 新しいリソースグループの作成 {#create-a-new-resource-group}

選択した場所に新しいリソースグループを作成します。

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

既にリソースグループがある場合は、代わりにそのリソースグループを自由に使用してください。 このガイドの残りの部分では、リソースグループの場所とその名前は、それぞれ `$location` と `$resourceGroup` で識別されています。

## Key Vault の作成 {#create-a-key-vault}

暗号化キーを格納する Key Vault を作成する必要があります。 Key Vault では、消去保護が有効になっている必要があります。 他の Azure サービスから保存中のデータを暗号化するには、パージ保護が必要です。 Adobeテナントが Key Vault にアクセスできることを確認するには、公開ネットワークアクセスも有効にする必要があります。

>[!IMPORTANT]
>公開ネットワークアクセスが無効な Key Vault を作成すると、KeyVault にネットワークアクセスできる環境（KeyVault にアクセスできる VM など）から、キーの作成やローテーションなどのすべての Key Vault 関連の操作を実行する必要があります。

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## Key Vault へのAdobeアクセスの許可 {#grant-adone-access-to-the-key-vault}

この手順では、Adobeが Entra アプリケーションを使用して Key Vault にアクセスできるようにします。 Entra アプリケーションの ID は、Adobeによって既に提供されている必要があります。

まず、Entra アプリケーションに接続されたサービスプリンシパルを作成し、それに **Key Vault ユーザー** と **Key Vault Crypto Reader** のロールを割り当てる必要があります。 役割は、このガイドで作成した Key Vault に制限されます。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## 暗号化キーの作成 {#create-an-ecryption-key}

最後に、Key Vault に暗号化キーを作成できます。 この手順を完了するには、**Key Vault Crypto Officer** の役割が必要となることに注意してください。 ログインユーザーにこの役割がない場合は、システム管理者に問い合わせてこの役割を付与してもらうか、その役割を既に持っているユーザーにこの手順を完了するように依頼してください。

暗号化キーを作成するには、Key Vault へのネットワークアクセスが必要です。 まず、Key Vault にアクセスできることを確認し、キーの作成に進みます。

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Key Vault 情報の共有 {#share-the-key-vault-information}

この時点で、すべての設定が完了しています。 必要な情報をAdobeに伝えるだけで、環境の設定を担当します。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## キーアクセスの取り消しの影響 {#implications-of-revoking-key-access}

Key Vault、キー、CMK アプリへのアクセスの取り消しまたは無効にすると、プラットフォームの操作の重大な変更など、重大な中断が生じる可能性があります。 これらのキーを無効にすると、Platform のデータにアクセスできなくなる可能性があり、このデータに依存するダウンストリーム操作は機能しなくなります。 主要な設定を変更する前に、ダウンストリームの影響を十分に理解することが重要です。

データへの Platform アクセスを取り消す場合は、アプリケーションに関連付けられているユーザーの役割を Azure 内の Key Vault から削除します。

## 次の手順 {#next-steps}

Adobeに連絡して共有：

* Key Vault の URL。 この手順で取得し、`$keyVaultUri` 変数に保存しました。
* 暗号化キーの名前。 前の手順でキーを作成し、`$keyName` 変数に保存しました。
* Key Vault への接続をセットアップするために必要な `$resourceGroup`、`$subscriptionId` および `$tenantId`。

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Private Betaの顧客管理キー {#customer-managed-keys-in-private-beta}

Adobeのエンジニアリングチームは現在、Azure のプライベートリンクを活用した CMK の拡張実装に取り組んでいます。 新しい実装では、Adobeのテナントと Key Vault の間に直接プライベートリンクが接続されているので、Azure バックボーンを介してキーを共有できます。

現在、この強化された実装はPrivate Betaで行われており、Private Beta プログラムに登録してAdobeエンジニアリングと緊密に連携することに同意している、一部のお客様に対して有効にすることができます。 プライベートリンクを使用した CMK のPrivate Betaに興味がある場合は、Adobeにお問い合わせください。
