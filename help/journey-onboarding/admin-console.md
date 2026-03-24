---
title: Admin Console へのアクセス
description: オンボーディングに必要な準備とAEM as a Cloud Service構造の基本を理解したら、初めてAdmin Consoleにログインする準備が整います。
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 9f237747f19ee537fbc51f39e935472c6a023328
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 55%

---

# Admin Console へのアクセス {#accessing-admin-console}

[オンボーディングジャーニー](overview.md)のこの部分では、システムに初めてログインする前に必要な準備を説明します。

## 目的 {#objective}

[AEM as a Cloud Service の用語](terminology.md)の記事を読み、AEMaaCS 構造の基本事項を理解したら、Admin Console に初めてログインする準備が整います。

Admin Consoleを使用して、組織内のユーザーを管理する責任があります。 このセクションを読めば、次のことが可能になるはずです，

* Adobe ID とは
* Adobe Admin Consoleにログインします。
* Admin Consoleを使用して、システム管理者としての権限を確認する方法について説明します。
* アドビサポートに問い合わせる方法

## Admin Consoleについて {#admin-console}

Adobe Admin Console では、アドビ製品のライセンスとユーザーを一元管理します。Admin Console を使用すると、別々なソリューション内ではなく、1 か所でユーザーを作成および管理できます。

### Adobe ID {#adobe-id}

Admin Console にログインするには、Adobe ID が必要です。Adobe IDは、AEM as a Cloud ServiceまたはAdobe ソリューションにログインしてアクセスするために必要な特定のメールアドレスに関連付けられたアカウントです。 Adobe IDを使用すると、1つのアカウントに関連付けられたすべてのAdobe プランと製品を保持できます。

システム管理者が Admin Console でチームをセットアップする際に、Adobe ID として使用するメールアドレスを指定します。

Adobe ID には次の 3 種類があります。

* **個人ID**: Adobe IDのデフォルトタイプで、adobe.comで作成されます。 Adobeによって管理され、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**：通常、組織はユーザーのアカウントの管理を強化したいと考えています。 Enterprise ID を作成できるのはシステム管理者のみであり、これらのアカウントを所有するのはお客様組織です（アドビはホストとしてのみ機能します）。

* **Federated ID**：連合IDを使用すると、組織はアカウントの完全な所有権と制御を取得します。 Adobe Experience CloudとSAML2 シングルサインオン （SSO） システムを統合する必要があります。 これにより、Adobeがホストするアカウントではなく、組織のSSO システムに対して認証を行うことができます。

システム管理者は、個人IDを使用して、自分自身とチームをAEM as a Cloud Serviceにオンボーディングできます。 エンタープライズ IDまたはフェデレーション IDが配置される前に、このタスクを実行します。 Enterprise ID または Federated ID を設定したら、それらの ID を使用するようにメンバーを移行できます。

### Admin Consoleに直接ログイン {#steps-admin-console}

Admin Console を使用してチーム内のユーザーを管理する前に、自分自身が正常にアクセスでき、適切な権限を持っていることを確認する必要があります。

1. システム管理者は、オンボーディングプロセスの一環として、Adobeから複数のメールを受け取ります。 アクセス権が付与された組織名に関する情報を記載したウェルカムメールを探します。

1. ウェルカムメールの「**はじめに**」リンクをクリックして、Admin Consoleに移動します。 メールが見つからない場合は、ブラウザーを開いて [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) の Admin Console に直接アクセスします。

   ![ウェルカムメール](/help/journey-onboarding/assets/get-started-email.png)

1. Adobe ID でのログインします。ログインに成功すると、Adobe Admin Console の&#x200B;**概要**&#x200B;ページが表示されます。

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. 複数の組織にアクセスできる場合は、正しい組織にログインしていることを確認してください。 組織を変更するには、右上隅にある組織名をクリックし、アクセスが必要な組織を選択します。

   ![組織を変更](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. **ユーザー**&#x200B;カードから「**管理者**」を選択して、自分がシステム管理者であることを確認します。

   ![管理者の確認](/help/journey-onboarding/assets/get-started2.png)

1. **ユーザー**&#x200B;カードで「**管理者**」をクリックすると、Adobe ID のメールアドレス、ユーザー名、名、姓を入力して検索できます。

   ![ユーザーを検索](/help/journey-onboarding/assets/get-started3.png)

1. すべてが正しく機能すれば、検索でレコードが返されます。 **管理者の役割**&#x200B;列の値に&#x200B;**システム**&#x200B;が表示されている場合、自分（または表示されているユーザー）がシステム管理者であることがわかります。

   ![システムステータス](/help/journey-onboarding/assets/get-started4.png)

おめでとうございます。あなたがシステム管理者であることが確認できました。

## Experience HubからAdmin Consoleにアクセスする  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md)は、AEMの統合されたパーソナライズされたホームです。 AEM ToolsとAdmin Consoleを1か所に統合しています。

![Experience Hub ホームページに表示されるAdmin Console オプション &#x200B;](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**Experience HubからAdmin Consoleにアクセスするには：**

1. [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)をクリックして、Experience Hubのホームページを開きます。

1. **クイックアクセス**&#x200B;のグループ化で、[**Admin Console**](https://experience.adobe.com)をクリックします。

## Adobe Identity Management System {#ims}

AEM as a Cloud Service には、認証用に Adobe Identity Management System（IMS とも呼ばれます）が事前設定されています。この機能を有効にするために、システム管理者として実行する必要はありません。

AEM as a Cloud Service は IMS を使用することで、AEM と Adobe Experience Cloud のその他の部分との間のログインエクスペリエンスを統合することができます。Adobe製品を数多く導入している企業は、スコアを最大化できます。 Admin Consoleでロールベースのグループを作成し、AEM as a Cloud ServiceなどのIMSを通じて製品アクセスを許可します。

製品プロファイルとユーザーの割り当てについて詳しくは、このオンボーディングジャーニーの次の部分を参照してください。

## Adobe サポートへのお問い合わせ {#support}

問題が発生した場合は、Admin Console からアドビサポートにアクセスできます。「**サポート**」タブを使用すると、シンプルで使いやすいインターフェイスから様々なアドビサポート機能にアクセスできます。

![「サポート」タブ](/help/journey-onboarding/assets/support-menu.png)

このタブを使用すると、ケースの作成や管理、アドビカスタマーサポートの担当者との直接のチャット、エキスパートとのセッションの予約などを行うことができます。サポートケースとエキスパートセッションのオプションにアクセスするには、 システム管理者とサポート管理者としてログインする必要があります。

## 次の手順 {#whats-next}

このドキュメントを読み、次を理解できました。

* Adobe ID とは
* Adobe Admin Consoleにログインします。
* Admin Consoleを使用して、システム管理者としての権限を確認する方法について説明します。
* アドビサポートに問い合わせる方法

Cloud Manager製品プロファイルにチームメンバーを[割り当てる](assign-profiles-cloud-manager.md)方法を学ぶことで、オンボーディングジャーニーを続ける準備が整い、同僚もAEMaaCSにアクセスできるようになります。

## その他のリソース {#additional-resources}

オンボーディングジャーニーのコンテンツの範囲を超えた情報について詳しくは、次の追加のオプションリソースを参照してください。

* [Admin Console の概要](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) - Admin Console の包括的な概要
* [Adobe ID の作成または更新](https://helpx.adobe.com/jp/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Adobe ID の作成および変更と、複数の Adobe ID の管理方法を説明します。
* [SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#) - AEMには、SAML 認証ハンドラーが付属しています。このハンドラーによって、HTTP POST バインディングを使用した SAML 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。
* [管理者の役割](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html) - Adobe Admin Console を使用すると、組織は柔軟な管理階層を定義して、アドビ製品のアクセスと使用を詳細に管理できます。
* [&#x200B; サポートとエキスパートセッション &#x200B;](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) - Admin Consoleのサポートオプションにアクセスする方法、サポートケースを管理する方法、エキスパートセッションをスケジュールする方法などを説明します。
