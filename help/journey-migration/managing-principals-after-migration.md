---
title: 移行後のプリンシパルの管理
description: IMS と AEM でユーザーとグループを設定する方法について説明します
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: 1c638f3d1cca4f97eb1f760054febd405b5714f5
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 79%

---

# 移行後のプリンシパルの管理 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="移行後のプリンシパルの管理"
>abstract="IMS と AEM でユーザーとグループを設定する方法について説明します"

このドキュメントでは、AEM as a Cloud Service 環境を操作する IMS および AEM のユーザーとグループを設定するのにお客様が実行する必要がある高レベルの手順について説明します。

グループの移行と、各取り込みで使用できるプリンシパル移行レポートについて詳しくは、[ グループの移行 ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) を参照してください。

Admin Consoleでのグループファイルとユーザーファイルの一括使用に関するガイドについては、[CTT を使用した後の IMS へのプリンシパルの一括アップロード ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md) を参照してください。

## プリンシパルの管理 {#managing-principals}

AEM as a Cloud Service の場合、ユーザーとグループは主に Admin Console を使用して管理する必要があります。移行を考慮する際、これらのタスクの一部は、コンテンツの移行が行われる前に実行できます。基本的に、次の主要なタスクグループのうち

* IMS でのユーザーとグループの作成
* IMS でのグループへのユーザーの割り当て
* AEM グループへの IMS グループの割り当て（必要に応じて）

最初の 2 つは、コンテンツの移行の前または後に実行できます。  これらは、IMS 内のユーザーとグループにのみ影響する手順で、Active Directory や LDAP などの外部 IDP との統合が含まれる可能性があります。これらの手順について詳しくは、[Admin Console を使用した IMS でのプリンシパルの管理](/help/journey-migration/managing-principals.md)を参照してください。

コンテンツを AEM as a Cloud Service 環境に移行すると、3 番目の手順を実行できます。

### グループの移行

移行の取り込みフェーズ中に、移行したコンテンツの ACL または CUG ポリシーを満たす必要がある場合は、グループを移行します。詳しくは、[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照してください。

移行したグループ（アセットコレクションの作成によって作成されていないグループ - 以下のコレクションを参照）は、IMS グループとして設定されます。つまり、（例えば、Admin Console コンソールを通じて）IMS で作成した同じ名前のグループはすべて AEM のグループにリンクされ、IMS グループのメンバーであるユーザーは AEM のグループのメンバーにもなります。このリンクを実行するには、まず IMS でグループも作成する必要があります。[Admin Console を使用した IMS でのプリンシパルの管理](/help/journey-migration/managing-principals.md)の説明に従って、Admin Console を使用して AEM インスタンスにグループを個別または一括で作成します。

AEM セキュリティ UI を使用して、IMS グループをローカルのAEM グループに割り当てます。 これをおこなうには、AEMのツールページに移動して、「セキュリティ」をクリックし、「グループ」を選択します。

### IMS ユーザー

ユーザーは移行されないので、AEM で使用できるように IMS で作成する必要があります。これを行う方法はいくつかありますが、以前の AEM システムで持っていたのと同じコンテンツへのアクセス権をユーザーに持たせるには、作成したユーザーを正しい IMS グループに割り当てることが重要です。これに使用できるツールの 1 つは、Admin Console の一括アップロード機能です。一括アップローダーを使用して、ユーザーと、そのユーザーがメンバーである必要があるグループをアップロードします。これを行う前に、上記のように、まず IMS でグループを作成する必要があります。

各ユーザーが属する必要があるグループを把握するには、ユーザーレポートを利用できます（[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照）。このレポートは、各ユーザーが属する必要があるグループをリストします。このリストは、Admin Consoleの一括アップロード機能で使用するために、通常はユーザーの一括入力ファイルに含まれます。

### コレクション

アセットコレクションを作成すると、そのコレクションへのアクセスを管理するグループも自動的に作成されます。これらのグループは、移行対象のコレクションに記載されている場合は移行されますが、IMS グループに直接リンクするように設定されていません。AEM では、これらのグループは「ローカルグループ」のままで、IMS 経由で管理できません。

これらのグループは IMS 内にないので、一括アップロードツールを使用してユーザーを直接のメンバーとして作成できません。AEM にも存在する IMS ユーザーをこれらのグループに個別に追加することはできますが、これを一括で行うには追加の手順が必要です。これを実行する方法の 1 つを次に示します。
* コレクションにアクセスする新しいグループを Admin Console／IMS に作成し、AEM 用に設定します。
* グループのメンバーとしてログインすると、AEM にグループが作成されます。
* 移行対象のコレクションの場合は、アセットコレクション UI を使用して、新しいグループを編集者／所有者／閲覧者として追加します。
* Admin Console で、新しいグループにユーザーを追加（または一括アップロード）します。
* ユーザーが初めてログインすると、AEM に IMS ユーザーが作成され、新しいグループと元のコレクショングループにアクセスできます。

注意：ユーザーの一括割り当ての場合、上記の手順を使用して IMS でユーザーを作成する必要があります。IMS に既に存在するユーザーはバルクアップロードで再度作成できませんが、バルクエディターを使用してこれらの種類の変更を行うことができます（**ユーザーの詳細を編集** の [Admin Consoleのバルクユーザーアップロード ](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html) を参照）。
