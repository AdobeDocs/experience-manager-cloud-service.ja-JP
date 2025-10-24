---
title: Admin Console へのアクセス
description: オンボーディングに必要な準備とAEM as a Cloud Service構造の基本を理解したら、Admin Consoleに初めてログインする準備が整います。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 55%

---

# Admin Console へのアクセス {#accessing-admin-console}

[オンボーディングジャーニー](overview.md)のこの部分では、システムに初めてログインする前に必要な準備を説明します。

## 目的 {#objective}

[AEM as a Cloud Service の用語](terminology.md)の記事を読み、AEMaaCS 構造の基本事項を理解したら、Admin Console に初めてログインする準備が整います。

システム管理者は、Admin Consoleを使用して組織内のユーザーを管理する必要があります。 この節を読むと、次のことができるようになります。

* Adobe ID とは
* Admin Consoleにログインできること。
* Admin Consoleを介してシステム管理者としての権限を確認する方法を理解します。
* アドビサポートに問い合わせる方法

## Admin Consoleについて {#admin-console}

Adobe Admin Console では、アドビ製品のライセンスとユーザーを一元管理します。Admin Console を使用すると、別々なソリューション内ではなく、1 か所でユーザーを作成および管理できます。

### Adobe ID {#adobe-id}

Admin Console にログインするには、Adobe ID が必要です。Adobe IDは、AEM as a Cloud Serviceまたは任意のAdobe ソリューションにログインしてアクセスするために必要な、特定のメールアドレスに関連付けられたアカウントです。 Adobe IDを使用すると、すべてのAdobe プランと製品を 1 つのアカウントに関連付けることができます。

システム管理者が Admin Console でチームをセットアップする際に、Adobe ID として使用するメールアドレスを指定します。

Adobe ID には次の 3 種類があります。

* **個人 ID**:adobe.comで作成される、デフォルトのタイプのAdobe IDです。 Adobeによって管理され、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**：組織は、ユーザーのアカウントに対する管理を強化したいと考えるのが普通です。 Enterprise ID を作成できるのはシステム管理者のみであり、これらのアカウントを所有するのはお客様組織です（アドビはホストとしてのみ機能します）。

* **Federated ID**: Federated ID を使用すると、組織はアカウントを完全に所有して管理できます。 Adobe Experience Cloudを SAML2 シングルサインオン（SSO）システムと統合する必要があります。 これにより、ユーザーは、Adobeがホストするアカウントではなく、組織の SSO システムに対して認証することができます。

システム管理者は、自分自身とチームを、個人 ID を使用してAEM as a Cloud Serviceにオンボーディングできます。 Enterprise ID または Federated ID を設定する前に、このタスクを実行します。 Enterprise ID または Federated ID を設定したら、それらの ID を使用するようにメンバーを移行できます。

### Admin Consoleに直接ログインします {#steps-admin-console}

Admin Console を使用してチーム内のユーザーを管理する前に、自分自身が正常にアクセスでき、適切な権限を持っていることを確認する必要があります。

1. システム管理者は、オンボーディングプロセスの一環としてAdobeから複数のメールを受け取ります。 アクセス権が付与された組織名に関する情報を記載したウェルカムメールを探します。

1. お知らせメールの **使用を開始** リンクをクリックして、Admin Consoleに移動します。 メールが見つからない場合は、ブラウザーを開いて [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) の Admin Console に直接アクセスします。

   ![ウェルカムメール](/help/journey-onboarding/assets/get-started-email.png)

1. Adobe ID でのログインします。ログインに成功すると、Adobe Admin Console の&#x200B;**概要**&#x200B;ページが表示されます。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認します。 組織を変更するには、右上隅にある組織名をクリックし、アクセスが必要な組織を選択します。

   ![組織を変更](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. **ユーザー**&#x200B;カードから「**管理者**」を選択して、自分がシステム管理者であることを確認します。

   ![管理者の確認](/help/journey-onboarding/assets/get-started2.png)

1. **ユーザー**&#x200B;カードで「**管理者**」をクリックすると、Adobe ID のメールアドレス、ユーザー名、名、姓を入力して検索できます。

   ![ユーザーを検索](/help/journey-onboarding/assets/get-started3.png)

1. すべてが正常に動作する場合は、検索によってレコードが返されます。 **管理者の役割**&#x200B;列の値に&#x200B;**システム**&#x200B;が表示されている場合、自分（または表示されているユーザー）がシステム管理者であることがわかります。

   ![システムステータス](/help/journey-onboarding/assets/get-started4.png)

おめでとうございます。あなたがシステム管理者であることが確認できました。

## Experience HubからAdmin Consoleへのアクセス  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md) は、AEM用に統合され、パーソナライズされたホームです。 AEM Tools とAdmin Consoleが一元化されます。

![Experience Hub ホームページに表示される「Admin Console」オプション &#x200B;](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**Experience HubからAdmin Consoleにアクセスする**

1. [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) をクリックして、Experience Hubのホームページを開きます。

1. **クイックアクセス** グループ化で、[**Admin Console**](https://experience.adobe.com) をクリックします。

## Adobe Identity Management System {#ims}

AEM as a Cloud Service には、認証用に Adobe Identity Management System（IMS とも呼ばれます）が事前設定されています。この機能を有効にするためにシステム管理者が行うべきことはありません。

AEM as a Cloud Service は IMS を使用することで、AEM と Adobe Experience Cloud のその他の部分との間のログインエクスペリエンスを統合することができます。多くのAdobe製品を持つ組織が最も多くの利益を得ることができます。 Admin Consoleで役割に基づくグループを作成し、IMS （AEM as a Cloud Serviceなど）を通じて製品アクセスを付与します。

製品プロファイルとユーザーの割り当てについて詳しくは、このオンボーディングジャーニーの次の部分を参照してください。

## Adobe サポートに連絡 {#support}

問題が発生した場合は、Admin Console からアドビサポートにアクセスできます。「**サポート**」タブを使用すると、シンプルで使いやすいインターフェイスから様々なアドビサポート機能にアクセスできます。

![「サポート」タブ](/help/journey-onboarding/assets/support-menu.png)

このタブを使用すると、ケースの作成や管理、アドビカスタマーサポートの担当者との直接のチャット、エキスパートとのセッションの予約などを行うことができます。サポートケースとエキスパートセッションのオプションにアクセスするには、 システム管理者とサポート管理者としてログインする必要があります。

## 次の手順 {#whats-next}

このドキュメントを読み、次を理解できました。

* Adobe ID の概要
* Admin Consoleにログインできること。
* Admin Consoleを使用して、システム管理者としての権限を確認する方法を理解します。
* アドビサポートに問い合わせる方法

同僚も AEMaaCS にアクセスできるように、チームメンバーをCloud Manager製品プロファイルに割り当てる [&#x200B; 方法を学習して &#x200B;](assign-profiles-cloud-manager.md) オンボーディングジャーニーを続ける準備が整いました。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えた情報について詳しくは、次の追加のオプションリソースを参照してください。

* [Admin Console の概要](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) - Admin Console の包括的な概要
* [Adobe ID の作成または更新](https://helpx.adobe.com/jp/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Adobe ID の作成および変更と、複数の Adobe ID の管理方法を説明します。
* [SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#) - AEMには、SAML 認証ハンドラーが付属しています。このハンドラーによって、HTTP POST バインディングを使用した SAML 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。
* [管理者の役割](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html) - Adobe Admin Console を使用すると、組織は柔軟な管理階層を定義して、アドビ製品のアクセスと使用を詳細に管理できます。
* [&#x200B; サポートおよびエキスパートセッション &#x200B;](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) - Admin Consoleでサポートオプションにアクセスする方法、サポートケースを管理する方法、エキスパートセッションを予約する方法などを説明します。
