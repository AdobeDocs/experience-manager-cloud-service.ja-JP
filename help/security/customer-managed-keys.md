---
title: AEM as a Cloud Service の顧客管理キー
description: AEM as a Cloud Service の暗号化キーの管理方法を学ぶ
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: ht
source-wordcount: '1199'
ht-degree: 100%

---

# AEM as a Cloud Service の顧客管理キーの設定 {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service は現在、顧客データを Azure Blob Storage と MongoDB に保存し、デフォルトでプロバイダー管理の暗号化キーを使用してデータを保護します。この設定は多くの組織のセキュリティニーズを満たしますが、規制の厳しい業界の企業や強化されたデータ主権を必要とする企業は、暗号化の実践をより厳密に制御することを求める場合があります。データのセキュリティ、コンプライアンス、暗号化キーの管理機能を優先する組織にとって、顧客管理キー（CMK）ソリューションは重要な機能強化を提供します。

## 解決中の問題 {#the-problem-being-solved}

プロバイダー管理キーは、厳格な規制によりデータセキュリティの包括的な制御が要求される金融、医療、政府機関などの分野の企業に対して懸念材料となる可能性があります。キー管理を制御できない場合、組織はコンプライアンス要件を満たし、カスタムセキュリティポリシーを実装し、完全なデータ主権を確保するという課題に直面します。

顧客管理キー（CMK）の導入により、AEM のお客様は暗号化キーを完全に制御できることで、これらの懸念に対処します。AEM CS では、Microsoft Entra ID（旧称 Azure Active Directory）を通じて認証することで、お客様の Azure Key Vault に安全に接続し、キーの作成、ローテーション、失効を含む暗号化キーのライフサイクルを管理できます。

CMK には、次のようないくつかの利点があります。

* **セキュリティの強化：**&#x200B;お客様は、暗号化の実践が特定のセキュリティ要件を満たしていることを確保できるので、データ保護に対する安心感を得ることができます。
* **コンプライアンスの柔軟性：**&#x200B;キーのライフサイクルを完全に制御することで、企業は GDPR、HIPAA、CCPA などの進化する規制基準に簡単に適応し、コンプライアンス体制を強力に保つことができます。
* **シームレスな統合：** CMK ソリューションは、AEM CS の Azure Blob Storage および MongoDB と直接統合され、ストレージ操作やユーザビリティが中断されることなく、強力な暗号化機能をお客様に提供します。

CMK を採用することで、お客様はデータセキュリティと暗号化の実践に対する制御を強化し、コンプライアンスを強化してリスクを軽減しながら、AEM CS の拡張性と柔軟性を引き続き享受できます。

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

## キーコンテナに対して Adobe アクセス権を付与する {#grant-adone-access-to-the-key-vault}

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
