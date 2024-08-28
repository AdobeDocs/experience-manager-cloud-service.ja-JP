---
title: 移行後のプリンシパルの管理
description: IMS とAEMでユーザーとグループを設定する方法について説明します
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# 移行後のプリンシパルの管理 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="移行後のプリンシパルの管理"
>abstract="IMS とAEMでユーザーとグループを設定する方法について説明します"

このドキュメントでは、AEM as a Cloud Service環境と連携するために IMS およびAEMでユーザーとグループを設定する際に必要な大まかな手順について説明します。

## プリンシパルの管理 {#managing-principals}

AEM as a Cloud Serviceの場合、ユーザーとグループの管理には、主にAdmin Consoleを使用する必要があります。  移行を検討する場合、これらのタスクの一部は、コンテンツの移行が行われる前に実行できます。  基本的に、次の主要なタスクグループのうち

* IMS でのユーザーとグループの作成
* IMS でのグループへのユーザーの割り当て
* IMS グループをAEM グループに割り当てる（必要な場合）

最初の 2 つは、コンテンツの移行の前または後に実行できます。  これらは、IMS 内のユーザーとグループにのみ影響するステップで、Active Directory や LDAP などの外部 IDP との統合が含まれる場合があります。  これらの手順については、[Admin Consoleを使用した IMS でのプリンシパルの管理 ](/help/journey-migration/managing-principals.md) を参照してください。

コンテンツをAEM as a Cloud Service環境に移行したら、3 番目の手順を実行できます。

### グループの移行

移行の取り込みフェーズでは、移行されたコンテンツに対する ACL または CUG ポリシーを満たすためにグループが必要な場合、グループが移行されます。  詳しくは、[ グループの移行 ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) を参照してください。

移行されたグループ（Assets コレクションの作成で作成されたものではない。以下のコレクションを参照）は、IMS グループとして設定されます。  つまり、（例えば、Admin Consoleを介して） IMS で作成された同じ名前のグループはすべてAEMのグループにリンクされ、IMS グループのメンバーであるユーザーはAEMのグループのメンバーにもなります。  このリンクを実行するには、まず IMS でもグループを作成する必要があります。  [Admin Consoleを使用した IMS でのプリンシパルの管理 ](/help/journey-migration/managing-principals.md) の説明に従って、Admin Consoleを使用して、AEM インスタンスにグループを個別にまたは一括で作成します。

AEM セキュリティ UI を使用して、IMS グループをローカルのAEM グループに割り当てます。  [ グループの作成および設定 ](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group) を参照してください。  このドキュメントはAEM 6.5 を対象としていますが、AEM as a Cloud Serviceで他のグループにグループを追加する場合にも当てはまります。

### IMS ユーザー

ユーザーは移行されないので、AEMで使用できるように、IMS で作成する必要があります。  これを行うには複数の方法がありますが、以前のAEM システムのコンテンツに同じアクセス権を持たせるには、作成したユーザーを正しい IMS グループに割り当てることが重要です。  これに使用できるツールの 1 つは、Admin Consoleのバルクアップロード機能です。バルクアップローダを使用して、メンバーである必要のあるグループと共にユーザーをアップロードします。  これを行う前に、前述のように、まず IMS でグループを作成する必要があります。

各ユーザーが属するグループを把握するには、ユーザーレポートを利用できます（[ グループの移行 ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) を参照）。  このレポートには、各ユーザーが属する必要があるグループが一覧表示され、このリストはAdmin Console一括アップロード機能の入力ファイルに含めることができます。

### コレクション

Assets コレクションを作成すると、そのコレクションへのアクセスを管理するためのグループも自動的に作成されます。  これらのグループは、移行済みコレクションでメンションされている場合は移行されますが、IMS グループに直接リンクするように設定されていません。AEMでは「ローカルグループ」のままであり、IMS を使用して管理することはできません。

これらのグループは IMS 内にないので、バルクアップロードツールを使用してユーザーを直接メンバーとして作成することはできません。  同じくAEM内にある IMS ユーザーはこれらのグループに個別に追加できますが、一括で追加するには追加の手順が必要です。  これを行う方法の 1 つを次に示します。
* コレクションにアクセスするための新しいグループをAdmin Consoleまたは IMS に作成し、AEM用に設定します。
* グループのメンバーとしてログインし、AEMでグループが作成されるようにします。
* 移行されたコレクションの場合は、Assets コレクション UI を使用して、新しいグループをエディター/オーナー/ビューアとして追加します。
* Admin Consoleの新しいグループにユーザーを追加（またはバルクアップロード）します。
* ユーザーが初めてログインすると、AEMに IMS ユーザーが作成され、新しいグループと元のコレクショングループにアクセスできるようになります。

注意：ユーザーを一括割り当てする場合、上記の手順を使用して IMS でユーザーを作成する必要があります。既に IMS に存在するユーザーは、一括アップロードでは再作成できません。


