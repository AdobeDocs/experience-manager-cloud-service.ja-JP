---
title: Adobe Experience Manager as a Cloud Service に対する IMS のサポート
description: Adobe Experience Manager as a Cloud Serviceの画像管理システムのサポート
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 40%

---

# Adobe Experience Manager as a Cloud Service に対する IMS のサポート {#ims-support-for-aem-as-a-cloud-service}

## はじめに {#introduction}

* AEM as a Cloud Service の Admin Console では、AEM インスタンスと、Adobe Identity Management System（IMS）ベースの認証をサポートしてます。
* Admin Console を使用すると、管理者がすべての Experience Cloud ユーザーを一元的に管理できます。
* ユーザーとグループは、AEMas a Cloud Serviceのインスタンスに関連付けられた製品プロファイルに割り当てることができ、そのインスタンスにログオンできます。

>[!TIP]
>
>詳しくは、 [管理者向けAEMへのアクセスの設定](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem) を参照してください。 また、Adobe IMSユーザー、ユーザーグループ、製品プロファイルを使用して、AEMとその機能へのアクセスを制御する方法についても説明します。 Adobe ID が必要です。

>[!NOTE]
>
>AEM では、現在、プロファイルへのグループの割り当てをサポートしていません。代わりに、ユーザーを個別に追加する必要があります。

## 主なハイライト {#key-highlights}

AEM as a Cloud Serviceでは、オーサー、管理者、開発者ユーザーに対してのみ IMS 認証をサポートしています。 サイトの訪問者など、顧客サイトの外部エンドユーザーに対してはサポートしていません。

* Admin Consoleは、お客様を IMS 組織、オーサーおよびパブリッシュインスタンスとして、環境内の製品コンテキストインスタンスとして表します。 この表示では、システム管理者と製品管理者がインスタンスへのアクセスを管理できます。
* ユーザーがアクセスできるAdmin Consoleの製品プロファイルは、ユーザーがアクセスできるインスタンスを決定します。
* お客様は、SAML 2 に準拠した独自の ID プロバイダー (IDP) をシングルサインオンに使用できます。
* お客様のシングルサインオン用の Enterprise ID または Federated ID のみがサポートされ、個人のAdobeID はサポートされません。

## アーキテクチャ {#architecture}

IMS 認証は、AEM と Adobe IMS エンドポイントの間で OAuth プロトコルを使用して機能します。ユーザーが IMS に追加され、アドビの ID を持つようになると、IMS 資格情報を使用して AEM オーサーサービスにログインできます。

ユーザーのログオンフローを以下に示します。ユーザーは IMS にリダイレクトされ、必要に応じて SSO 用に顧客 IDP にリダイレクトされてから、AEMにリダイレクトされます。

![IMS のアーキテクチャ](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### Adobe Admin Console への組織のオンボーディング {#onboarding-orgs-to-adobe-admin-console}

Adobe Admin Console にお客様をオンボーディングすることは、AEM 認証に Adobe IMS を使用するための前提条件です。

最初の手順として、組織がAdobe IMSでプロビジョニングされている必要があります。 Adobeの企業のお客様は、 [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html). この領域は、Adobeのお客様が自社製品に対するユーザーおよびグループの使用権限を管理するために使用するポータルです。

AEMのお客様は、既に組織をプロビジョニングしておく必要があります。また、IMS プロビジョニングの一環として、ユーザーの使用権限とアクセスを管理するために、Admin Console内で顧客インスタンスを使用できるようになります。

お客様が IMS 組織として存在する場合は、次に示すようにシステムを設定する必要があります。

![IMS のオンボーディング](/help/security/assets/ims2.png)

1. 指定されたシステム管理者が、Cloud Manager へのログインの招待を受け取ります。Cloud Manager にログインした後、システム管理者は AEM のプログラムと環境のプロビジョニングを選択するか、Admin Console に移動して管理タスクを実行することができます。
1. システム管理者がドメインを要求して、それぞれのドメイン（この例では acme.com）の所有権を確認します。
1. システム管理者がユーザーディレクトリを設定します。
1. システム管理者は、シングルサインオンを設定するAdmin Consoleで IDP 設定を行います。
1. AEM 管理者が、通常どおりローカルグループと権限および特権を管理します。

IDP 設定など、アドビの ID 管理の基本については、[こちら](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)を参照してください。

Enterprise Administration と Admin Console の使用方法については、[こちら](https://helpx.adobe.com/jp/enterprise/admin-guide.html)を参照してください。

### Admin Console でのユーザーのオンボーディング {#onboarding-users-in-admin-console}

ユーザーをオンボーディングする方法は 3 つあります。 各方法は、お客様の規模と好みに応じて異なります。 ユーザーは、Admin Console内で手動で作成したり、.csv ファイルをアップロードしたり、お客様の企業の Active Directory からユーザーを同期したりできます。

**Admin Console UI による手動追加**

ユーザーとグループは、Admin Console の UI で手動で作成できます。この方法は、管理するユーザーが多くない場合に使用できます。 例えば、AEMユーザーが 50 人未満の場合や、Analytics、Target、Creative Cloudアプリケーションなどの他のAdobe製品を管理するために既にこの方法を使用している場合などです。

![ユーザーのオンボーディング](/help/security/assets/ims3.png)

**Admin Console UI でのファイルアップロード**

ユーザー作成を簡単に処理するために、`.csv` ファイルをアップロードしてユーザーを一括で追加できます。

![ファイルのアップロード](/help/security/assets/ims4.png)

**ユーザー同期ツール**

ユーザー同期ツール (UST) を使用すると、Adobeの企業のお客様は、Active Directory を使用してAdobeユーザーを作成および管理できます。 この UST は、テスト済みの他の OpenLDAP ディレクトリサービスでも機能します。 対象ユーザーは、ツールをインストールおよび設定できる IT ID 管理者（Enterprise Directory または System Admin）です。 オープンソースツールはカスタマイズ可能なので、顧客が特定の要件に合わせて変更できます。

ユーザー同期が実行されると、組織の Active Directory からユーザーのリストを取得し、Admin Console内のユーザーのリストと比較します。 その後、Adobeが組織のディレクトリと同期されるように、Admin ConsoleUser Management API を呼び出します。 変更フローは完全に一方向です。Admin Console で行った編集は、ディレクトリにはプッシュされません。

このツールを使用すると、システム管理者は、お客様のディレクトリ内のユーザーグループを、製品設定およびユーザー内のユーザーグループにマッピングできます。

ユーザー同期を設定するには、組織は、 [ユーザー管理 API](https://developer.adobe.com/umapi/).

![ユーザー同期ツール](/help/security/assets/ims5.png)

ユーザー同期ツールは、AdobeGitHub リポジトリを通じて配布されます [この場所で](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2).

>[!NOTE]
>
>プレリリースバージョンの **2.4RC1** は動的グループ作成サポートで利用でき、[この場所](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)にあります。

このリリースの主な機能は、Admin Console内のユーザーメンバーシップに対して新しい LDAP グループを動的にマッピングする機能と、動的なユーザーグループの作成です。

新しいグループ機能の詳細については、[こちら](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)を参照してください。

**ユーザー同期に関するドキュメント**

詳しくは、[UST のドキュメント](https://adobe-apiplatform.github.io/user-sync.py/en/)を参照してください。

ユーザー同期ツールは、手順を使用して、Adobe Developerクライアント UMAPI として登録する必要があります [ここ](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

Adobe Developer Console のドキュメントは、 [ここ](https://developer.adobe.com/developer-console/).

ユーザー同期ツールで使用される User Management API については、[こちら](https://adobe-apiplatform.github.io/user-sync.py/en/)を参照してください。

## Adobe Experience Manager as a Cloud Service の設定 {#aem-configuration}

>[!NOTE]
>
>必要なAEM IMS 設定は、AEM環境とインスタンスがプロビジョニングされる際に自動的に設定されます。 ただし、管理者は、[こちら](/help/implementing/deploying/overview.md)で説明している方法を使用して、自らの要件に従って設定を変更できます。

必要なAEM IMS 設定は、AEMの環境とインスタンスがプロビジョニングされる際に自動的におこなわれます。 顧客側の管理者は、自らの要件に応じて設定の一部を変更できます。

Adobe IMS を OAuth プロバイダーとして設定することが全体的なアプローチになります。LDAP の同期と同様に、**Apache Jackrabbit Oak Default Sync Handler** を変更できます。

ユーザーの自動メンバーシップやグループマッピングなどのプロパティを変更するために変更が必要な主要な OSGi 設定を以下に示します。

<!-- Arun to provide list of osgi configs -->

## 使用方法 {#how-to-use}

### Admin Console での製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

製品管理者がAdmin Consoleにログオンすると、次に示すように、AEMas a Cloud Serviceの製品コンテキストの複数のインスタンスが表示されます。 例えば、 **概要** ページ：

![インスタンスへのログイン](/help/security/assets/ims6.png)

既存のインスタンスのリストが表示されます。

![インスタンスへのログイン 2](/help/security/assets/ims7.png)

各製品コンテキストインスタンスの下に、実稼動、ステージ、または開発環境全体でオーサーサービスまたはパブリッシュサービスにまたがるインスタンスがあります。 各インスタンスは、製品プロファイルまたは Cloud Manager の役割に関連付けられています。 これらの製品プロファイルは、必要な特権を持つユーザーおよびグループにアクセス権を割り当てるために使用されます。

この **AEM Administrators_xxx** プロファイルは、関連するAEMインスタンスで管理者権限を付与するために使用されます。 **AEM Users_xxx** プロファイルは、通常のユーザーを追加するために使用されます。

この製品プロファイルの下に追加されたユーザーとグループは、次の例に示すように、そのインスタンスにログオンできます。

![製品プロファイル](/help/security/assets/ims8.png)

>[!WARNING]
>
>次を変更しない： **AEM Administrators** 製品プロファイル名。 名前の変更 **AEM Administrators** 製品プロファイルは、そのプロファイルに割り当てられているすべてのユーザーから管理者権限を削除します。

### Adobe Experience Manager as a Cloud Service へのログイン {#logging-in-to-aem}

**ローカル管理者ログイン**

AEMは、引き続き管理者ユーザーのローカルログインをサポートできます。 ログオン画面を使用して、ローカルでログオンできます。

![ローカルログイン](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS ベースのログイン**

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログオンが使用されます。 次に示すように、ユーザーは「Adobeを使用してログイン」ボタンをクリックします。

![IMS のログイン](/help/security/assets/ims10.png)


>[!NOTE]
>
>IMS で作成された任意のユーザーは、Adobe ID または Federated ID を使用して作成できます。ユーザーがFederated IDを使用して設定されている場合、ユーザーは会社の ID プロバイダーを使用して認証され、ログオンします。

ユーザーは IMS ログオン画面にリダイレクトされ、資格情報を入力する必要があります。

![IMS のログイン 2](/help/security/assets/ims11.png)

![IMS のログイン 3](/help/security/assets/ims12.png)

初期Admin Console設定中にフェデレーテッド IDP が設定されると、ユーザーは SSO 用にカスタマー IDP にリダイレクトされます。

![IMS のログイン 4](/help/security/assets/ims13.png)

認証が完了すると、ユーザーはAEMにリダイレクトされ、ログインします。

![IMS のログイン 5](/help/security/assets/ims14.png)

### Adobe Experience Manager as a Cloud Service での権限と ACL の管理 {#managing-permissions-in-aem}

ACL と権限は、引き続きAEMで管理されます。 IMS から同期されたユーザーグループは、ACL と特権が定義されているローカルグループに割り当てることができます。

以下の例では、同期されたグループがローカルに追加されています **Dam_Users** グループを作成します。

ユーザーは、IMS の以下のグループの一部です。

![ACL1](/help/security/assets/ims15.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![ACL2](/help/security/assets/ims16.png)

AEM では、IMS から同期されたユーザーグループを既存のローカルグループ（**DAM ユーザー**&#x200B;など）にメンバーとして追加できます。

![ACL3](/help/security/assets/ims17.png)

以下に示すように、グループは **AEM-GRP_008** はの権限と権限を継承します。 **DAM ユーザー**. この継承は、同期されたグループの権限を効果的に管理する方法であり、LDAP ベースの認証方法で一般的に使用されます。

![ACL3](/help/security/assets/ims18.png)


### Cloud Manager へのアクセス {#accessing-cloud-manager}

AEM as a Cloud Service上の環境や Cloud Manager にアクセスするには、Cloud Manager 製品のプロファイルに割り当てられている必要があります。

Cloud Manager の特定の機能の可用性を管理するユーザーの役割について詳しくは、役割の定義を参照してください。

>[!NOTE]
>Cloud Manager には、適切な権限を持つ事前設定済みの役割が用意されています。特定の権限、事前設定済みのタスク、または各役割に関連付けられた権限を持つ各役割について詳しくは、 [ロールベースの権限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions.html?lang=en).

**ユーザーの追加手順**

1. 既存ユーザー画面または新規ユーザー画面から、ユーザーを特定のプロファイルに追加します。

1. または、次の図に示すように、**概要**&#x200B;画面から、ユーザーを追加することもできます。

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >次の図に示すように、1 人のプロファイルに複数のユーザーを割り当てることができます。

   ![ACL3](/help/security/assets/ims22.png)


1. 適切なプロファイルに追加したら、次の手順で Cloud Manager の各テナントにアクセスできるようになります。 [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) ユーザーインターフェイスの右上隅を使用する。


### AEM as a Cloud Service のインスタンスへのアクセス {#accessing-instance-cloud-service}

>[!IMPORTANT]
>前の節で説明した手順は、AEM as a Cloud Service のインスタンスにアクセス可能になる前に、既に完了している必要があります。

内のAEMインスタンスにアクセスするには **Admin Console**&#x200B;の製品リストに、 Cloud Manager プログラムとプログラム内の環境が表示されます。 **Admin Console**.

例えば、以下のスクリーンショットには、次の 2 つの使用可能な環境が表示されます。 *開発者* および *公開*.

![ACL3](/help/security/assets/ims19.png)

AEMインスタンスにアクセスするには、ユーザーが適切な製品のグループに追加されている必要があります。Cloud Service

すべてのオーサーインスタンスにはAEM管理者とAEMユーザープロファイルが割り当てられ、すべてのパブリッシュインスタンスにはAEMユーザープロファイルが割り当てられます。 必要に応じて、他のプロファイルを追加できます。

AEM インスタンスへの管理者レベルのアクセス権を取得するには、その製品の AEM 管理者プロファイルにユーザーを追加します。
