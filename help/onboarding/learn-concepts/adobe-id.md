---
title: Adobe ID について
description: ここでは、Adobe ID について説明します。
exl-id: 55f66f24-d523-4f8f-9cb6-337bd31fc315
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%

---

# Adobe ID {#adobe-id}

Adobe ID は、AEM as a Cloud Service または任意のアドビソリューションへのログインとアクセスに使用する電子メールアドレスです。これは、チームのセットアップ時にシステム管理者が使用する電子メール ID です。Adobe ID を使用すると、すべてのアドビプランと製品を 1 つのアカウントに関連付けることができます。

>[!IMPORTANT]
>Adobe ID は、アドビのアプリケーションとサービスを、安全に、かつパーソナライズして利用するうえで不可欠であり、アドビ製品を購入する際にも必要になります。Adobe ID を使用すると、すべてのアドビプランと製品を 1 つのアカウントに関連付けることができます。詳しくは、[Adobe ID の作成または更新](https://helpx.adobe.com/jp/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)を参照してください。

Adobe ID には次の 3 種類があります。

* **個人 ID**：これはデフォルトのアカウントタイプです。基本的に、ユーザーは adobe.com でアカウントを作成する必要があります。つまり、このアカウントはアドビが管理するもので、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**：組織は、ユーザーのアカウントに対する管理を強化したいと考えるのが普通です。システム管理者のみが Enterprise ID タイプのアカウントを作成でき、組織がアカウントを所有します。アドビは、これらをホストするだけです。

* **Federated ID**：この ID では、組織がアカウントを完全に所有して管理できます。この場合、Adobe Experience Cloud を SAML2 SSO システムと統合する必要があります。最終的には、ユーザーは、アドビでホストされるアカウントに対してではなく、会社の SSO システムに対して認証を行うことになります。詳しくは、[SAML 2.0 認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=ja)を参照してください。

>[!NOTE]
>Enterprise ID または Federated ID がまだセットアップされていない場合、システム管理者は個人 ID を使用してチームのオンボーディングを行うこともできます。Enterprise ID または Federated ID がセットアップされたら、その ID を使用するようにメンバーを移行できます。
