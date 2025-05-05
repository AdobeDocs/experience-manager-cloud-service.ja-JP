---
title: Adobe Experience Manager as a Cloud Service に対する IMS のサポート
description: Adobe Experience Manager as a Cloud Service の Image Management System のサポート。
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
feature: Security
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: ht
source-wordcount: '1941'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service に対する IMS のサポート {#ims-support-for-aem-as-a-cloud-service}

## はじめに {#introduction}

* AEM as a Cloud Service の Admin Console では、AEM インスタンスと、Adobe Identity Management System（IMS）ベースの認証をサポートしてます。
* Admin Console を使用すると、管理者がすべての Experience Cloud ユーザーを一元的に管理できます。
* AEM as a Cloud Service インスタンスに関連付けられている製品プロファイルにユーザーとグループを割り当てることができます。その結果、ユーザーとグループはその特定のインスタンスにログオンできるようになります。

>[!TIP]
>
>Adobe IMS を使用した AEM as a Cloud のユーザー認証の概要については、[AEM のアクセスの設定（管理者向け）](https://experienceleague.adobe.com/?lang=ja&recommended=ExperienceManager-A-1-2020.1.aem)を参照してください。また、Adobe IMS ユーザー、ユーザーグループ、製品プロファイルを使用して、AEM とその機能のアクセス権を制御する方法についても説明します。Adobe ID が必要です。

## 主なハイライト {#key-highlights}

AEM as a Cloud Service では、作成者、管理者および開発者ユーザーに対してのみ IMS 認証をサポートしています。サイトの訪問者など、顧客サイトの外部エンドユーザーに対してはサポートしていません。

* Admin Console では、お客様を IMS 組織として表し、環境内のオーサリングインスタンスとパブリッシュインスタンスを製品コンテキストインスタンスとして表します。これにより、システム管理者と製品管理者がインスタンスへのアクセスを管理できるようになります。
* Admin Console の製品プロファイルによって、ユーザーがアクセスできる AEM インスタンスが決まります。
* お客様は、SAML 2 に準拠している独自の ID プロバイダー（IDP）をシングルサインオンに使用できます。
* Enterprise ID または Federated ID（お客様のシングルサインオン用）のみがサポートされています。個人の Adobe ID はサポートされていません。

## アーキテクチャ {#architecture}

IMS 認証は、AEM と Adobe IMS エンドポイントの間で OAuth プロトコルを使用して機能します。ユーザーが IMS に追加され、アドビの ID を持つようになると、IMS 資格情報を使用して AEM オーサーサービスにログインできます。

ユーザーログインフローを以下に示します。ユーザーは IMS、（オプションとして SSO のためにカスタマー IDP）、AEM の順にリダイレクトされます。

![IMS のアーキテクチャ](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### Adobe Admin Console への組織のオンボーディング {#onboarding-orgs-to-adobe-admin-console}

Adobe Admin Console にお客様をオンボーディングすることは、AEM 認証に Adobe IMS を使用するための前提条件です。

最初の手順として、Adobe IMS に組織をプロビジョニングする必要があります。Adobe Enterprise のお客様は、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) に IMS 組織として表されています。この領域は、アドビのお客様が自社製品に対するユーザーおよびグループの使用権限を管理するために使用するポータルです。

AEM のお客様は、既に組織がプロビジョニングされています。また、IMS プロビジョニングの一環として、ユーザーの使用権限とアクセス権を管理するために、Admin Console でカスタマーインスタンスを利用できるようになります。

お客様が IMS 組織として存在するようになれば、お客様のシステムを、次に要約するように設定する必要があります。

![IMS のオンボーディング](/help/security/assets/ims2.png)

1. 指定されたシステム管理者が、Cloud Manager へのログインの招待を受け取ります。Cloud Manager にログインした後、システム管理者は AEM のプログラムと環境のプロビジョニングを選択するか、Admin Console に移動して管理タスクを実行できます。
1. システム管理者がドメインを要求して、それぞれのドメイン（例：acme.com）の所有権を確認します。
1. システム管理者がユーザーディレクトリを設定します。
1. システム管理者は、シングルサインオンを設定するために Admin Console で IDP 設定を行います。
1. AEM 管理者が、通常どおりローカルグループと権限および特権を管理します。

IDP 設定を含め、Adobe Identity Management Basics について詳しくは、[ID とシングルサインオンの設定](https://helpx.adobe.com/jp/enterprise/using/set-up-identity.html)を参照してください。

Enterprise Administration と Admin Console の使用について詳しくは、[エンタープライズ版およびチーム版の管理者ガイドへようこそ](https://helpx.adobe.com/jp/enterprise/admin-guide.html)を参照してください。

### Admin Console でのユーザーのオンボーディング {#onboarding-users-in-admin-console}

ユーザーをオンボーディングする方法は 3 つあります。いずれの方法も、お客様の規模と好みによります。Admin Console でユーザーを手動で作成することも、.csv ファイルをアップロードすることも、お客様の企業の Active Directory からユーザーを同期することもできます。

**Admin Console UI による手動追加**

ユーザーとグループは、Admin Console の UI で手動で作成できます。この方法は、管理するユーザー数が多くない場合に使用できます。例えば、AEM ユーザーが 50 人未満の場合や、Analytics、Target、Creative Cloud アプリケーションなどの他のアドビ製品を管理するために既にこの方法を使用している場合などです。

![ユーザーのオンボーディング](/help/security/assets/ims3.png)

**Admin Console UI でのファイルアップロード**

ユーザー作成を簡単に処理するために、`.csv` ファイルをアップロードしてユーザーを一括で追加できます。

![ファイルのアップロード](/help/security/assets/ims4.png)

**ユーザー同期ツール**

ユーザー同期ツール（UST）を使用すると、アドビの法人のお客様は、Active Directory を利用してアドビユーザーを作成および管理できます。この UST を使用する方法は、検証済みの他の OpenLDAP ディレクトリサービスでも機能します。ターゲットユーザーは、このツールをインストールおよび設定できる IT 部門の ID 管理者（エンタープライズディレクトリとシステムの管理者）です。オープンソースツールはカスタマイズ可能なので、ユーザーは特定の要件に合わせて変更できます。

ユーザー同期が実行されると、組織の Active Directory からユーザーリストを取得し、それを Admin Console 内のユーザーリストと比較します。その後、Admin Console を組織のディレクトリと同期するために、Adobe User Management API を呼び出します。変更フローは完全に一方向です。Admin Console で行った編集は、ディレクトリにはプッシュされません。

このツールを使用すると、システム管理者は、お客様のディレクトリ内のユーザーグループを、Admin Console 内の製品設定とユーザーグループにマッピングできます。

ユーザー同期を設定するには、[User Management API](https://developer.adobe.com/umapi/) を使用する場合と同様に、組織が一連の資格情報を作成する必要があります。

![ユーザー同期ツール](/help/security/assets/ims5.png)

ユーザー同期ツールは、[こちらの場所](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2)にある Adobe GitHub リポジトリを通じて配布されています。

>[!NOTE]
>
>プレリリースバージョンの **2.4RC1** は動的グループ作成サポートで利用でき、[GitHub の ユーザー同期ツール v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1) にあります。

このリリースの主な機能は、Admin Console でユーザーのメンバーシップに合わせて新しい LDAP グループを動的にマッピングする機能と、動的なユーザーグループ作成です。

新しいグループ機能について詳しくは、[Adobe ユーザー同期ツール - その他のグループオプション](https://adobe-apiplatform.github.io/user-sync.py/jp/user-manual/advanced_configuration.html#additional-group-options)を参照してください。

**ユーザー同期に関するドキュメント**

以下を参照してください。

* [UST のドキュメント](https://adobe-apiplatform.github.io/user-sync.py/jp/)

* ユーザー同期ツールは、[API アクセスの認証](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)の手順を使用して Adobe Developer クライアント UMAPI として登録する必要があります。

* [Adobe Developer Console のドキュメント](https://developer.adobe.com/developer-console/)

* [ユーザー同期ツールで使用される User Management API](https://adobe-apiplatform.github.io/user-sync.py/jp/)

## Adobe Experience Manager as a Cloud Service の設定 {#aem-configuration}

>[!NOTE]
>
>必要な AEM IMS 設定は、AEM の環境とインスタンスがプロビジョニングされる際に自動的に行われます。ただし、管理者は、自らの要件に従って設定を変更できます。[AEM as a Cloud Service へのデプロイ](/help/implementing/deploying/overview.md)を参照してください。

必要な AEM IMS 設定は、AEM の環境とインスタンスがプロビジョニングされる際に自動的に行われます。顧客側の管理者は、自らの要件に応じて設定の一部を変更できます。

Adobe IMS を OAuth プロバイダーとして設定することが全体的なアプローチになります。LDAP の同期と同様に、**Apache Jackrabbit Oak Default Sync Handler** を変更できます。

ユーザーの自動メンバーシップやグループマッピングなどのプロパティを変更するために修正する必要がある主要な OSGi 設定を以下に示します。

<!-- Arun to provide list of osgi configs -->

## 使用方法 {#how-to-use}

### Admin Console での製品とユーザーアクセスの管理 {#managing-products-and-user-access-in-admin-console}

製品管理者が Admin Console にログオンすると、以下に示すように、AEM as a Cloud Service 製品コンテキストの複数のインスタンスが表示されます。例えば、**概要**&#x200B;ページからいずれかの製品を選択します。

![インスタンスへのログイン](/help/security/assets/ims6.png)

既存のインスタンスのリストが表示されます。

![インスタンスへのログイン 2](/help/security/assets/ims7.png)

各製品コンテキストインスタンスの下に、実稼動、ステージング、または開発環境全体でオーサリングサービスまたはパブリッシュサービスにまたがるインスタンスがあります。各インスタンスは、製品プロファイルまたは Cloud Manager の役割に関連付けられます。これらの製品プロファイルは、必要な特権を持つユーザーおよびグループにアクセス権を割り当てるために使用されます。

**AEM Administrator_xxx** プロファイルは関連する AEM インスタンスで管理者権限を付与するために使用され、**AEM Users_xxx** プロファイルは通常のユーザーを追加するために使用されます。

この製品プロファイルの下に追加されたすべてのユーザーおよびグループは、以下の例に示すように、そのインスタンスにログオンできます。

![製品プロファイル](/help/security/assets/ims8.png)

>[!WARNING]
>
>**AEM 管理者**&#x200B;の製品プロファイル名を変更しないでください。**AEM 管理者**&#x200B;の製品プロファイル名を変更すると、そのプロファイルに割り当てられているすべてのユーザーから管理者権限が削除されます。

### Adobe Experience Manager as a Cloud Service へのログイン {#logging-in-to-aem}

**ローカル管理者ログイン**

AEM は、引き続き管理者ユーザーのローカルログインをサポートできます。ログオン画面を使用して、ローカルでログオンできます。

![ローカルログイン](/help/security/assets/ims9.png)

<!-- the above image must be updated for skyline -->

**IMS ベースのログイン**

他のユーザーの場合は、IMS がインスタンスに設定された後に、IMS ベースのログオンを使用できます。ユーザーは、下に示すように、「Adobe にログイン」ボタンをクリックします。

![IMS のログイン](/help/security/assets/ims10.png)


>[!NOTE]
>
>IMS で作成された任意のユーザーは、Adobe ID または Federated ID を使用して作成できます。ユーザーが Federated ID を使用して設定されている場合、ログオンには会社の ID プロバイダーを使用して認証されます。

その後、ユーザーは IMS ログオン画面にリダイレクトされ、資格情報を入力します。

![IMS のログイン 2](/help/security/assets/ims11.png)

![IMS のログイン 3](/help/security/assets/ims12.png)

Admin Console の初期設定中にフェデレーテッド IDP が設定される場合、ユーザーは SSO 用のカスタマー IDP にリダイレクトされます。

![IMS のログイン 4](/help/security/assets/ims13.png)

認証が完了すると、ユーザーは AEM にリダイレクトされてログインします。

![IMS のログイン 5](/help/security/assets/ims14.png)

### Adobe Experience Manager as a Cloud Service での権限と ACL の管理 {#managing-permissions-in-aem}

ACL と権限は引き続き AEM で管理されます。IMS から同期されたユーザーグループは、ACL と特権が定義されているローカルグループに割り当てることができます。

以下の例では、同期グループをローカル **Dam_Users** グループに追加しています。

ユーザーは、IMS の以下のグループの一部です。

![ACL1](/help/security/assets/ims15.png)

ユーザーがログインすると、以下に示すように、グループメンバーシップが同期されます。

![ACL2](/help/security/assets/ims16.png)

AEM では、IMS から同期されたユーザーグループを既存のローカルグループ（**DAM ユーザー**&#x200B;など）にメンバーとして追加できます。

![ACL3](/help/security/assets/ims17.png)

以下に示すように、グループ **AEM-GRP_008** は **DAM ユーザー**&#x200B;の権限と特権を継承します。この継承は同期されたグループに対する権限を管理する効果的な方法であり、LDAP ベースの認証方法で一般的に使用されています。

![ACL3](/help/security/assets/ims18.png)


### Cloud Manager へのアクセス {#accessing-cloud-manager}

Cloud Manager または AEM as a Cloud Service の環境にアクセスするには、Cloud Manager 製品のプロファイルに割り当てられている必要があります。

Cloud Manager で特定の機能の可用性を管理するユーザーの役割について詳しくは、役割の定義を参照してください。

>[!NOTE]
>Cloud Manager には、適切な権限を持つ事前設定済みの役割が用意されています。各役割に関連付けられた、特定の権限、事前設定済みのタスク、または権限を持つ各役割について詳しくは、[役割に基づく権限](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)を参照してください。

**ユーザーの追加手順**

1. 既存ユーザー画面または新規ユーザー画面から、ユーザーを特定のプロファイルに追加します。

1. または、次の図に示すように、**概要**&#x200B;画面から、ユーザーを追加することもできます。

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >次の図に示すように、1 人のプロファイルに複数のユーザーを割り当てることができます。

   ![ACL3](/help/security/assets/ims22.png)


1. 適切なプロファイルに追加したら、ユーザーインターフェイスの右上隅を使用して [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) 経由で、Cloud Manager の各テナントにアクセスできるようになります。


### AEM as a Cloud Service のインスタンスへのアクセス {#accessing-instance-cloud-service}

>[!IMPORTANT]
>前の節で説明した手順は、AEM as a Cloud Service のインスタンスにアクセス可能になる前に、既に完了している必要があります。

**Admin Console** 内の AEM インスタンスにアクセスするには、**Admin Console** の製品リストに Cloud Manager プログラムとプログラム内の環境が表示されている必要があります。

例えば、以下のスクリーンショットには、2 つの利用可能な環境、すなわち *dev author* と *publish* が表示されています。

![ACL3](/help/security/assets/ims19.png)

AEM インスタンスにアクセスするには、適切な Cloud Service 製品のグループにユーザーを追加する必要があります。

すべてのオーサリングインスタンスには AEM 管理者と AEM ユーザーのプロファイルが割り当てられ、すべてのパブリッシュインスタンスには AEM ユーザーのプロファイルが割り当てられます。必要に応じて、他のプロファイルを追加できます。

AEM インスタンスへの管理者レベルのアクセス権を取得するには、その製品の AEM 管理者プロファイルにユーザーを追加します。
