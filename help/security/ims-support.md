---
title: クラウドサービスとしてのAdobe Experience ManagerのIMSサポート
description: 'クラウドサービスとしてのAdobe Experience ManagerのIMSサポート '
translation-type: tm+mt
source-git-commit: 7ece752a5f59966e0c6be638c37bcaaf238b629a

---


# クラウドサービスとしてのAdobe Experience ManagerのIMSサポート {#ims-support-for-aem-as-a-cloud-service}

## 概要 {#introduction}

* クラウドサービスとしてのAEMには、AEMインスタンスとAdobe ID管理システム（短縮版の場合はIMS）ベースの認証に対する管理コンソールのサポートが含まれています。
* 管理コンソールを使用すると、管理者はすべてのExperience cloudユーザーを一元的に管理できます。
* ユーザーとグループは、AEMに関連付けられた製品プロファイルにクラウドサービスインスタンスとして割り当て、そのインスタンスにログインできます。

## 主なハイライト {#key-highlights}

クラウドサービスとしてのAEMは、作成者、管理者および開発者ユーザーに対してのみIMS認証をサポートします。 サイトの訪問者など、顧客サイトの外部エンドユーザーに対するサポートは提供されません。

* 管理コンソールは、お客様を製品コンテキストインスタンスとして、環境内のIMS組織、作成者および発行インスタンスとして表します。 これにより、システム管理者と製品管理者はインスタンスへのアクセスを管理できます。
* 管理コンソールの製品プロファイルは、ユーザーがアクセスできるインスタンスを決定します。
* お客様は、独自のSAML 2準拠IDプロバイダー（短くはIDP）をシングルサインオンに使用できます。
* お客様のシングルサインオン用のEnterprise IDまたはFederated IDのみがサポートされ、個人のAdobe IDはサポートされません。

## アーキテクチャ {#architecture}

IMS認証は、AEMとAdobe IMSエンドポイント間でOAuthプロトコルを使用して機能します。 ユーザーが IMS に追加され、Adobe Identity を持つようになると、IMS 資格情報を使用して AEM Managed Services インスタンスにログインできます。

ユーザーログインフローを以下に示します。ユーザーはIMSにリダイレクトされ、オプションでSSO用の顧客IDPにリダイレクトされ、AEMにリダイレクトされます。

![IMSアーキテクチャ](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### Onboarding Organizations to Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

Adobe IMSをAEM認証に使用する前提条件は、Adobe Admin Consoleへのオンボーディングです。

最初の手順として、お客様はAdobe IMSで組織をプロビジョニングする必要があります。 Adobe Enterpriseのお客様は、 [Adobe Admin ConsoleでIMS組織として表されます](https://helpx.adobe.com/enterprise/using/admin-console.html) 。これは、アドビのお客様がユーザーおよびグループに対する製品の権利付与を管理するために使用するポータルです。

AEMのお客様は、既に組織をプロビジョニングしておく必要があります。また、IMSプロビジョニングの一環として、顧客インスタンスを管理コンソールで使用して、ユーザーの権利付与とアクセスを管理できます。

顧客がIMS組織として存在したら、次に要約するようにシステムを設定する必要があります。

![IMSオンボーディング](/help/security/assets/ims2.png)

1. 指定されたシステム管理者が、Cloud Managerへのログインの招待を受け取ります。 Cloud Managerにログインした後、システム管理者はAEMプログラムと環境のプロビジョニングを選択したり、管理タスクの管理コンソールに移動したりできます。
1. システム管理者は、それぞれのドメイン（acme.comなど）の所有権を確認するドメインを要求します。
1. システム管理者がユーザーディレクトリを設定します
1. システム管理者は、シングルサインオンを設定するために管理コンソールでIDP設定を行います。
1. AEM管理者は、ローカルグループと権限および権限を通常どおり管理します。

IDP設定を含むAdobe ID管理の基本については、ここで説明 [します](https://helpx.adobe.com/enterprise/using/set-up-identity.html)。

Enterprise AdministrationとAdmin Consoleの使用方法については、こちらを参照し [てくださ](https://helpx.adobe.com/enterprise/managing/user-guide.html)い。

### Onboarding Users in Admin Console {#onboarding-users-in-admin-console}

ユーザーをオンボードする方法は、お客様の規模と好みに応じて3つあります。管理コンソールでユーザーを手動で作成し、.csvファイルをアップロードするか、お客様のエンタープライズActive Directoryからユーザーを同期します。

**アドミンコンソール UI による手動追加**

ユーザーとグループは、アドミンコンソールの UI で手動で作成できます。この方法は、管理するユーザーの数が多くない場合に使用できます。 例えば、50人未満のAEMユーザーや、Analytics、Target、Creative cloudなどの他のアドビ製品の管理にこの方法を既に使用している場合などです。

![ユーザーのオンボーディング](/help/security/assets/ims3.png)

**管理コンソールUIでのファイルのアップロード**

For easy handling of user creation, a `.csv` file can be uploaded for adding users in bulk.

![ファイルのアップロード](/help/security/assets/ims4.png)

**ユーザー同期ツール**

ユーザー同期ツール（略してUST）を使用すると、エンタープライズのお客様は、Active Directoryを使用してアドビのユーザーを作成および管理できます。 これは、他のテスト済みOpenLDAPディレクトリサービスでも機能します。 対象ユーザーは、ツールのインストールと設定が可能なIT ID管理者（Enterprise DirectoryまたはSystem Admin）です。 オープンソースツールはカスタマイズ可能で、顧客は独自の要件に合わせて変更できます。

ユーザー同期を実行すると、組織のActive Directoryからユーザーのリストを取得し、管理コンソール内のユーザーのリストと比較します。  その後、アドミンコンソールを組織のディレクトリと同期するために、Adobe User Management API を呼び出します。変更フローは完全に一つの方法です。 管理コンソールで行った編集は、ディレクトリにプッシュされません。

このツールを使用すると、システム管理者は、顧客のディレクトリ内のユーザーグループを、管理コンソール内の製品設定とユーザーグループにマッピングできます。

To set up User Sync, the organization needs to create a set of credentials in the same way they would use the [User Management API](https://www.adobe.io/apis/experienceplatform/umapi-new.html).

![ユーザー同期ツール](/help/security/assets/ims5.png)

User Sync Tool is distributed through the Adobe Github repository [at this location](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> プレリリース版 **2.4RC1は** 、動的グループ作成のサポートで入手でき、こちらを参照してく [ださい](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)。

このリリースの主な機能は、アドミンコンソールでユーザーのメンバーシップに合わせて新しい LDAP グループを動的にマッピングする機能と、動的なユーザーグループ作成です。

新しいグループ機能の詳細については、ここを参 [照してください](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)。

**ユーザー同期ドキュメント**

詳細は、 [USTのマニュアルを参照](https://adobe-apiplatform.github.io/user-sync.py/en/) 。

The User Sync Tool needs to register as an Adobe I/O client UMAPI using the procedure [here](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Adobe I/O Console Documentation can be found [here](https://www.adobe.io/apis/cloudplatform/console.html).

The User Management API that is used by the User Sync Tool is covered [here](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## クラウドサービス設定としてのAdobe Experience {#aem-configuration}

> [!NOTE]
>
>必要なAEM IMS設定は、AEM環境とインスタンスがプロビジョニングされる際に自動的に設定されます。 ただし、管理者は、ここで説明する方法を使用して、要件に従って変更で [きます](/help/implementing/deploying/overview.md)。

必要なAEM IMS設定は、AEM環境とインスタンスがプロビジョニングされる際に自動設定されます。  お客様の管理者は、要件に応じて設定の一部を変更できます

全体的なアプローチは、Adobe IMSをOAuthプロバイダーとして設定することです。 LDAP同期 **と同様に、Apache Jackrabbit Oak Default Sync Handler** （Apache Jackrabbit Oakデフォルト同期ハンドラ）を変更できます。

ユーザーの自動メンバーシップやグループのマッピングなどのプロパティを変更するために変更する必要がある主要なOSGI設定を以下に示します。

<!-- Arun to provide list of osgi configs -->

## 使用方法 {#how-to-use}

### アドミンコンソールでの製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

製品管理者が管理コンソールにログインすると、次に示すように、AEM Managed Services製品コンテキストの複数のインスタンスが表示されます。

![インスタンスログイン](/help/security/assets/ims6.png)

In this example, the org **AEM-MS-Onboard** has 32 instances spanning different topologies and environments like Stage or Prod.

![インスタンスlogin2](/help/security/assets/ims7.png)

各製品コンテキストインスタンスの下に、製品プロファイルが関連付けられます。 これらの製品プロファイルは、必要な権限を持つユーザーおよびグループへのアクセス権を割り当てるために使用されます。

Administrator_xxx **プロファイルは** 、関連するAEMインスタンスで管理者権限を付与するために使用されます。 **User_xxx** プロファイルは、通常のユーザーを追加するために使用されます。

この製品プロファイルに基づいて追加されたユーザーおよびグループは、次の例のように、その特定のインスタンスにログインできます。

![製品プロファイル](/help/security/assets/ims8.png)

### クラウドサービスとしてのAdobe Experience Managerへのログイン(#logging-in-to-aem)

**ローカル管理者ログイン**

AEMは、管理者ユーザーのローカルログインを引き続きサポートできます。ログイン画面には、ローカルでログインするオプションがあります。

![ローカルログイン](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS ベースのログイン**

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログインを使用できます。ユーザーはまず、下に示すように、「Sign in with Adobe」ボタンをクリックします。

![IMSログイン](/help/security/assets/ims10.png)

その後、IMSログイン画面にリダイレクトされ、資格情報を入力する必要があります。

![IMSログイン2](/help/security/assets/ims11.png)

![IMSログイン3](/help/security/assets/ims12.png)

Federated IDPが最初の管理コンソールのセットアップ中に設定された場合、SSO用の顧客IDPにリダイレクトされます。

![IMSログイン4](/help/security/assets/ims13.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![IMSログイン5](/help/security/assets/ims14.png)

### クラウドサービスとしてのAdobe Experience Managerでの権限とACLの管理 {#managing-permissions-in-aem}

ACLと権限は引き続きAEMで管理されます。 IMSから同期されるユーザーグループは、ACLと権限が定義されているローカルグループに割り当てることができます。

In the example below, we are adding synced groups to the local **Dam_Users** group as an example.

ユーザーは、IMS の以下のグループの一部です。

![ACL1](/help/security/assets/ims15.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![ACL2](/help/security/assets/ims16.png)

In AEM, the User Groups synced from IMS can be added as members to existing local groups, like **DAM Users**.

![ACL3](/help/security/assets/ims17.png)

次に示すように、グループ **AEM-GRP_008は** DAM Users ****（DAMユーザー）の権限と権限を継承します。これは、同期グループの権限を効果的に管理する方法で、LDAPベースの認証方法でも一般的に使用されます。

![ACL3](/help/security/assets/ims18.png)