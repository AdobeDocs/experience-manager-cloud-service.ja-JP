---
title: Admin Console へのアクセス
description: オンボーディングに必要な準備と AEMaaCS 構造の基本事項を理解したら、Admin Console に初めてログインする準備が整います。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1071'
ht-degree: 100%

---

# Admin Console へのアクセス {#accessing-admin-console}

[オンボーディングジャーニー](overview.md)のこの部分では、システムに初めてログインする前に必要な準備を説明します。

## 目的 {#objective}

[AEM as a Cloud Service の用語](terminology.md)の記事を読み、AEMaaCS 構造の基本事項を理解したら、Admin Console に初めてログインする準備が整います。

システム管理者は、組織内のユーザーを管理する必要があります。これを行うには、Admin Console を使用します。この節を参照した後、次の内容を理解する必要があります。

* Adobe ID とは
* Admin Console へのログイン方法
* Admin Console でのシステム管理者としての権限を確認する方法
* アドビサポートに問い合わせる方法

## Admin Console {#admin-console}

Adobe Admin Console では、アドビ製品のライセンスとユーザーを一元管理します。Admin Console を使用すると、別々なソリューション内ではなく、1 か所でユーザーを作成および管理できます。

## Adobe ID {#adobe-id}

Admin Console にログインするには、Adobe ID が必要です。また、Adobe ID は、AEM as a Cloud Service や任意のアドビソリューションにログインしてアクセスするために必要な、特定のメールアドレスに関連付けられたアカウントです。Adobe ID を使用すると、アドビのすべてのプランと製品を 1 つのアカウントに関連付けることができます。

システム管理者が Admin Console でチームをセットアップする際に、Adobe ID として使用するメールアドレスを指定します。

Adobe ID には次の 3 種類があります。

* **個人 ID**：adobe.com で作成される、デフォルトのタイプの Adobe ID です。このアカウントはアドビが管理するもので、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**：組織は、ユーザーのアカウントに対する管理を強化したいと考えるのが普通です。Enterprise ID を作成できるのはシステム管理者のみであり、これらのアカウントを所有するのはお客様組織です（アドビはホストとしてのみ機能します）。

* **Federated ID**：Federated ID を使用すると、組織はアカウントを完全に所有して管理できます。これを行うには、組織は Adobe Experience Cloud を SAML2 シングルサインオン（SSO）システムと統合する必要があります。これにより、ユーザーはアドビがホストするアカウントではなく、組織の SSO システムに対して認証できます。

システム管理者は、Enterprise ID または Federated ID を設定する前に、個人 ID を使用して自分自身とチームを AEM as a Cloud Service にオンボードすることを決定できます。Enterprise ID または Federated ID を設定したら、それらの ID を使用するようにメンバーを移行できます。

## Admin Console へのログイン {#steps-admin-console}

Admin Console を使用してチーム内のユーザーを管理する前に、自分自身が正常にアクセスでき、適切な権限を持っていることを確認する必要があります。

1. システム管理者は、オンボーディングプロセスの一環としてアドビから複数のメールを受信します。アクセス権が付与された組織名に関する情報を記載したウェルカムメールを探します。

1. ウェルカムメールの&#x200B;**使用開始**&#x200B;リンクをクリックして、Admin Console に移動します。メールが見つからない場合は、ブラウザーを開いて [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) の Admin Console に直接アクセスします。

   ![ウェルカムメール](/help/journey-onboarding/assets/get-started-email.png)

1. Adobe ID でのログインします。ログインに成功すると、Adobe Admin Console の&#x200B;**概要**&#x200B;ページが表示されます。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認してください。組織を変更するには、右上隅にある組織名をクリックし、アクセスが必要な組織を選択します。

   ![組織を変更](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. **ユーザー**&#x200B;カードから「**管理者**」を選択して、自分がシステム管理者であることを確認します。

   ![管理者の確認](/help/journey-onboarding/assets/get-started2.png)

1. **ユーザー**&#x200B;カードで「**管理者**」をクリックすると、Adobe ID のメールアドレス、ユーザー名、名、姓を入力して検索できます。

   ![ユーザーを検索](/help/journey-onboarding/assets/get-started3.png)

1. すべてが正常に機能している場合は、検索により自分のレコードが返されます。**管理者の役割**&#x200B;列の値に&#x200B;**システム**&#x200B;が表示されている場合、自分（または表示されているユーザー）がシステム管理者であることがわかります。

   ![システムステータス](/help/journey-onboarding/assets/get-started4.png)

おめでとうございます。あなたがシステム管理者であることが確認できました。

## Adobe Identity Management System {#ims}

AEM as a Cloud Service には、認証用に Adobe Identity Management System（IMS とも呼ばれます）が事前設定されています。これを有効にするためにシステム管理者が行うべきことはありません。

AEM as a Cloud Service は IMS を使用することで、AEM と Adobe Experience Cloud のその他の部分との間のログインエクスペリエンスを統合することができます。特に複数のアドビ製品を利用している組織では、Admin Console で役割に基づくグループを作成し、IMS で AEM as a Cloud Service を含む複数の製品へのアクセス権を割り当てることでメリットが得られます。

製品プロファイルとユーザーの割り当てについて詳しくは、このオンボーディングジャーニーの次の部分を参照してください。

## アドビサポートへのお問い合わせ {#support}

問題が発生した場合は、Admin Console からアドビサポートにアクセスできます。「**サポート**」タブを使用すると、シンプルで使いやすいインターフェイスから様々なアドビサポート機能にアクセスできます。

![「サポート」タブ](/help/journey-onboarding/assets/support-menu.png)

このタブを使用すると、ケースの作成や管理、アドビカスタマーサポートの担当者との直接のチャット、エキスパートとのセッションの予約などを行うことができます。サポートケースとエキスパートセッションのオプションにアクセスするには、 システム管理者とサポート管理者としてログインする必要があります。

## 次のステップ {#whats-next}

このドキュメントを読み、次を理解できました。

* Adobe ID の概要
* Admin Console へのログイン方法
* Admin Console でのシステム管理者としての権限を確認する方法
* アドビサポートに問い合わせる方法

同僚も AEMaaCS にアクセスできるように、チームメンバーを [Cloud Manager 製品プロファイルに割り当てる](assign-profiles-cloud-manager.md)方法を学習することで、オンボーディングジャーニーを続ける準備が整いました。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えてさらに詳しく知りたい場合に役立つ、追加のオプションリソースを次に示します。

* [Admin Console の概要](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) - Admin Console の包括的な概要
* [Adobe ID の作成または更新](https://helpx.adobe.com/jp/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Adobe ID の作成および変更と、複数の Adobe ID の管理方法を説明します。
* [SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=ja) - AEMには、SAML 認証ハンドラーが付属しています。このハンドラーによって、HTTP POST バインディングを使用した SAML 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。
* [管理者の役割](https://helpx.adobe.com/jp/enterprise/using/admin-roles.ug.html) - Adobe Admin Console を使用すると、組織は柔軟な管理階層を定義して、アドビ製品のアクセスと使用を詳細に管理できます。
* [サポートおよびエキスパートセッション](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Admin Console でサポートオプションにアクセスする方法、サポートケースを管理する方法、エキスパートセッションを予約する方法などを説明します。
