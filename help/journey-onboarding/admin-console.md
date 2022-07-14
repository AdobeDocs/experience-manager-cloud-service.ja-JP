---
title: Admin Consoleへのアクセス
description: AEMaaCS 構造のオンボーディングに必要な準備と基本事項を理解したら、Admin Consoleに初めてログインする準備が整います。
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 9%

---


# Admin Consoleへのアクセス {#accessing-admin-console}

この部分では、 [オンボーディングジャーニー](overview.md) 初めてシステムにログインする前に必要な準備について学習します。

## 目的 {#objective}

これで記事を読んだ [AEMas a Cloud Service用語](terminology.md) AEMaaCS 構造の基本を理解し、初めてAdmin Consoleにログインする準備が整いました。

システム管理者は、組織内のユーザーを管理する必要があります。 これをおこなうには、Admin Consoleを使用します。 この節を読んだ後、以下をおこなう必要があります。

* Adobe IDとは
* Admin Console
* システム管理者としての権限を確認する方法については、Admin Consoleを参照してください。
* ヘルプが必要な場合は、Adobeサポートに問い合わせる方法を理解してください。

## Admin Console {#admin-console}

Adobe Admin Console では、アドビ製品のライセンスとユーザーを一元管理します。Admin Consoleを使用すると、様々なソリューション内ではなく、1 か所でユーザーを作成および管理できます。

## Adobe ID {#adobe-id}

Admin Consoleにサインインするには、Adobe IDが必要です。 また、Adobe IDは、AEM as a Cloud Serviceや任意のAdobeソリューションにログインしてアクセスするために必要な、特定の電子メールアドレスに関連付けられたアカウントです。 Adobe ID を使用すると、すべてのアドビプランと製品を 1 つのアカウントに関連付けることができます。

システム管理者がAdmin Consoleでチームを設定する際に、Adobe IDとして使用する電子メールアドレスを指定します。

次の 3 つのタイプのAdobeID があります。

* **個人 ID**:これはデフォルトのタイプのAdobe IDで、adobe.com で作成されます。 このアカウントはAdobeが管理し、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**:組織は通常、ユーザーアカウントの制御を強化したいと考えています。 Enterprise ID を作成できるのはシステム管理者のみで、Adobeがホストとしてのみ機能するアカウントを組織が所有している場合は、その管理者のみがです。

* **Federated ID**:Federated ID を使用すると、組織はアカウントの完全な所有権と制御を取得します。 これをおこなうには、組織でAdobe Experience Cloudを SAML2 シングルサインオン (SSO) システムと統合する必要があります。 これにより、Adobeがホストするアカウントではなく、組織の SSO システムに対する認証が可能になります。

システム管理者は、Enterprise ID または Federated ID を設定する前に、個人 ID を使用してAEMas a Cloud Serviceの ID にオンボーディングすることにします。 Enterprise ID または Federated ID を設定したら、それらの ID を使用するようメンバーを移行できます。

## Admin Console へのログイン {#steps-admin-console}

Admin Consoleを使用してチーム内のユーザーを管理する前に、自分がチームに正しくアクセスでき、適切な権限を持っていることを確認する必要があります。

1. システム管理者は、オンボーディングプロセスの一環としてAdobeから複数の電子メールを受け取ります。 アクセス権を付与された組織名に関する情報を記載した「ようこそ」の電子メールを探します。

1. をクリックします。 **はじめに** 「Admin Console」に移動するには、「ようこそ」の電子メールにリンクを含めてください。 電子メールが見つからない場合は、ブラウザーを直接開いて、次の場所にAdmin Consoleします。 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![お知らせメール](/help/journey-onboarding/assets/get-started-email.png)

1. Adobe ID でのログイン。ログインに成功すると、 **概要** Adobe Admin Consoleの

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認してください。 組織を変更するには、右上隅の組織名をクリックし、アクセスする必要のある組織を選択します。

   ![組織を変更](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. 選択 **管理者** から **ユーザー** カードを使用して、システム管理者であることを確認します。

   ![管理者の確認](/help/journey-onboarding/assets/get-started2.png)

1. 次をクリックすると、 **管理者** から **ユーザー** カードを使用する場合、Adobe IDの E メール、ユーザー名、名または姓を入力して検索できます。

   ![ユーザーを検索](/help/journey-onboarding/assets/get-started3.png)

1. すべてが正しく動作している場合は、レコードが返されます。 値が **管理者ロール** 列表示 **システム**&#x200B;を使用する場合は、自分（または表示されているユーザー）がシステム管理者であることがわかります。

   ![システムステータス](/help/journey-onboarding/assets/get-started4.png)

おめでとうございます。システム管理者。

## Adobe Identity Management System {#ims}

AEM as a Cloud Serviceには、認証用にAdobeIdentity Management System（IMS とも呼ばれます）が事前に設定されています。 これを有効にするためにシステム管理者が行う必要はありません。

IMS を使用することで、AEM as a Cloud ServiceはAEMと他のAdobe Experience Cloudの間のログイン操作を統合します。 複数のAdobe製品を持つ組織は、特に、Admin Consoleで役割ベースのグループを作成し、IMS を介してAEMを含む複数の製品にアクセス権を割り当てることで、メリットを得られます。

製品プロファイルの詳細とユーザー割り当てについては、このオンボーディングジャーニーの次のパートで説明します。

## アドビサポートのご案内 {#support}

問題がある場合は、Admin ConsoleからAdobeサポートにアクセスできます。 この **サポート** 「 」タブを使用すると、使いやすいシンプルなインターフェイスを通じて、様々なAdobeサポート機能にアクセスできます。

![「サポート」タブ](/help/journey-onboarding/assets/support-menu.png)

「 」タブでは、ケースの作成と管理、Adobeカスタマーサポート担当者との直接のチャット、エキスパートとのセッションのスケジュール設定をおこなうことができます。 システム管理者とサポート管理者は、サポートケースやエキスパートセッションオプションにアクセスするにはサインインする必要があります。

## 次のステップ {#whats-next}

このドキュメントを読んだら、次の操作を行う必要があります。

* とAdobe IDの概要
* Admin Console
* システム管理者としての権限を確認する方法については、Admin Consoleを参照してください。
* ヘルプが必要な場合は、Adobeサポートに問い合わせる方法を理解してください。

次の方法を学習して、オンボーディングジャーニーを続行する準備が整いました： [Cloud Manager 製品プロファイルへのチームメンバーの割り当て](assign-profiles-cloud-manager.md) 同僚が AEMaaCS にもアクセスできるようにするためです。

## その他のリソース {#additional-resources}

* [Admin Consoleの概要](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) ・Admin Consoleの包括的な概要
* [Adobe IDの作成または更新](https://helpx.adobe.com/jp/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Adobe IDを作成、変更、複数のAdobeID を管理する方法を説明します。
* [SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEMには、SAML 認証ハンドラーが付属しています。 このハンドラーによって、HTTP POST バインディングを使用した SAML 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。
* [管理ロール](https://helpx.adobe.com/jp/enterprise/using/admin-roles.ug.html)  — 組織は、Adobe Admin Consoleを使用して、Adobe製品のアクセスと使用を詳細に管理できる柔軟な管理階層を定義できます。
* [サポートおよびエキスパートセッション](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) -Admin Consoleのサポートオプションへのアクセス、サポートケースの管理、エキスパートセッションのスケジュールなどの方法について説明します。
