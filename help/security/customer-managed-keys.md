---
title: AEM as a Cloud Service の顧客管理キー
description: AEM as a Cloud Service の暗号化キーの管理方法を学ぶ
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: eb38369ee918851a9f792af811bafff9b2e49a53
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 86%

---

# AEM as a Cloud Service の顧客管理キーの設定 {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service は現在、顧客データを Azure Blob Storage と MongoDB に保存し、デフォルトでプロバイダー管理の暗号化キーを使用してデータを保護します。この設定は多くの組織のセキュリティ要件を満たしていますが、規制対象の業界や、強化されたデータセキュリティを必要とする企業は、暗号化方法をより詳細に制御したいと考えるかもしれません。 データのセキュリティ、コンプライアンス、暗号化キーの管理機能を優先する組織にとって、顧客管理キー（CMK）ソリューションは重要な機能強化を提供します。

## 解決中の問題 {#the-problem-being-solved}

プロバイダー管理キーは、追加のプライバシーと整合性を必要とする企業に対して懸念を生じさせる可能性があります。 鍵の管理を管理できない組織は、コンプライアンス要件への対応、カスタム・セキュリティ・ポリシーの導入、完全なデータ・セキュリティの確保という課題に直面しています。

顧客管理キー（CMK）の導入により、AEM のお客様は暗号化キーを完全に制御できることで、これらの懸念に対処します。AEM CS では、Microsoft Entra ID（旧称 Azure Active Directory）を通じて認証することで、お客様の Azure Key Vault に安全に接続し、キーの作成、ローテーション、失効を含む暗号化キーのライフサイクルを管理できます。

CMK には、次のようないくつかの利点があります。

* **データとアプリケーションの暗号化を制御：** AEM アプリケーションとデータ暗号化キーを直接管理することで、セキュリティを強化します。
* **機密性と整合性の向上：** 完全な暗号化管理により、機密性の高いデータや専有データへの不用意なアクセスや開示の可能性を軽減します。
* **Azure Key Vault のサポート：** Azure Key Vault を使用すると、キーストレージ、シークレットの操作の処理、キーの回転の実行が可能になります。

CMK を採用すると、お客様は、AEM CS の拡張性と柔軟性を引き続き享受しながら、データセキュリティと暗号化プラクティスに対する制御を強化し、セキュリティを強化し、リスクを軽減できます。

AEM as a Cloud Service を使用すると、保存データを暗号化するための独自の暗号化キーを使用できます。このガイドでは、AEM as a Cloud Service の Azure Key Vault で顧客管理キー（CMK）を設定する手順について説明します。

>[!WARNING]
>
>CMK を設定した後は、システム管理キーに戻すことはできません。データへのアクセスが失われないように、キーを安全に管理し、Azure 内でキーコンテナ、キー、CMK アプリへのアクセスを提供するのはお客様の責任です。

また、必要なインフラストラクチャを作成および設定するための次の手順についても説明します。

1. 環境の設定
1. アドビからのアプリケーション ID の取得
1. 新しいリソースグループの作成
1. キーコンテナの作成
1. キーコンテナに対して Adobe アクセス権を付与する
1. 暗号化キーの作成

キーコンテナの URL、暗号化キー名、およびキーコンテナに関する情報をアドビと共有する必要があります。

## 環境の設定 {#setup-your-environment}

Azure コマンドラインインターフェイス（CLI）は、このガイドの唯一の要件です。Azure CLI をまだインストールしていない場合は、[こちら](https://learn.microsoft.com/ja-jp/cli/azure/install-azure-cli)にある公式のインストール手順に従ってください。

このガイドの残りの部分に進む前に、`az login` を使用して CLI にログインしてください。

>[!NOTE]
>
>このガイドでは Azure CLI を使用しますが、Azure コンソール経由で同じ操作を実行することもできます。Azure コンソールを使用する場合は、以下のコマンドを参考にしてください。

## アドビからのアプリケーション ID の取得 {#obtain-an-application-id-from-adobe}

アドビでは、このガイドの残りの部分で必要になる Entra アプリケーション ID を提供します。アプリケーション ID をまだお持ちでない場合は、アドビに問い合わせて取得してください。

## 新しいリソースグループの作成 {#create-a-new-resource-group}

選択した場所に新しいリソースグループを作成します。

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

既にリソースグループがある場合は、代わりにそのリソースグループを使用できます。このガイドの残りの部分では、リソースグループの場所とその名前は、それぞれ `$location` と `$resourceGroup` で識別されます。

## キーコンテナの作成 {#create-a-key-vault}

暗号化キーを格納するには、キーコンテナを作成する必要があります。キーコンテナでは、パージ保護が有効になっている必要があります。他の Azure サービスからの保存データを暗号化するには、パージ保護が必要です。アドビのテナントがキーコンテナにアクセスできることを確認するには、パブリックネットワークアクセスも有効にする必要があります。

>[!IMPORTANT]
>パブリックネットワークアクセスを無効にしてキーコンテナを作成すると、キーの作成やローテーションなどのすべてのキーコンテナ関連の操作は、キーコンテナへのネットワークアクセス権を持つ環境（キーコンテナにアクセスできる VM など）から実行する必要があります。

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

## キーコンテナに対して Adobe アクセス権を付与する {#grant-adobe-access-to-the-key-vault}

この手順では、アドビが Entra アプリケーションを通じてキーコンテナにアクセスできるようにします。Entra アプリケーションの ID は、アドビから既に提供されている必要があります。

まず、Entra アプリケーションにアタッチされたサービスプリンシパルを作成し、それに **Key Vault Reader** の役割と **Key Vault Crypto User** の役割を割り当てる必要があります。役割は、このガイドで作成したキーコンテナに限定されます。

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

最後に、キーコンテナで暗号化キーを作成できます。この手順を完了するには、**Key Vault Crypto Officer** の役割が必要です。ログインしたユーザーにこの役割がない場合は、システム管理者に問い合わせて、この役割を付与してもらうか、既にその役割を持っているユーザーにこの手順を完了するよう依頼してください。

暗号化キーを作成するには、キーコンテナへのネットワークアクセスが必要です。まず、キーコンテナにアクセスできることを確認してから、キーを作成します。

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## キーコンテナ情報の共有 {#share-the-key-vault-information}

この時点で、すべての準備が整いました。必要な情報をアドビにお伝えいただければ、アドビがお使いの環境の設定を行います。

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

キーコンテナ、キー、または CMK アプリへのアクセスを取り消したり無効にしたりすると、プラットフォームの操作に重大な変更が行われるなど、重大な中断が生じる可能性があります。これらのキーが無効になると、プラットフォーム内のデータにアクセスできなくなる場合があり、このデータに依存するダウンストリーム操作は機能しなくなります。主要な設定に変更を行う前に、ダウンストリームの影響を完全に理解することが重要です。

データへのプラットフォームアクセスを取り消す場合は、Azure 内のキーコンテナからアプリケーションに関連付けられているユーザーの役割を削除します。

## 次の手順 {#next-steps}

アドビに連絡して以下を共有します。

* キーコンテナの URL。この手順で取得し、`$keyVaultUri` 変数に保存しました。
* 暗号化キーの名前。前の手順でキーを作成し、`$keyName` 変数に保存しました。
* キーコンテナへの接続を設定するために必要な `$resourceGroup`、`$subscriptionId`、`$tenantId`。

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Private Beta の顧客管理キー {#customer-managed-keys-in-private-beta}

アドビのエンジニアリングチームは現在、Azure のプライベートリンクを活用した CMK の拡張実装に取り組んでいます。新しい実装では、アドビのテナントとお使いのキーコンテナ間を直接プライベートリンクで接続し、Azure バックボーンを通じてキーを共有できます。

この強化された実装は、現在 Private Beta であり、Private Beta プログラムに登録し、アドビのエンジニアリングチームと緊密に連携することに同意した一部のお客様にご利用いただけます。プライベートリンクを使用した CMK の Private Beta に興味がある場合、詳しくは、アドビにお問い合わせください。
