---
title: Adobe ID
description: このページでは、Adobe IDに関する情報を説明します。
source-git-commit: 90ed13a2d86611aeb709f8e8f0d75aeb8dbd97dd
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 3%

---


# Adobe ID {#adobe-id}

Adobe IDは、Cloud Serviceまたは任意のAdobeソリューションとしてログインし、AEMにアクセスするために使用する電子メールです。 これは、チームの設定時にシステム管理者が使用する電子メールIDです。 Adobe IDを使用すると、1つのアカウントに関連付けられたすべてのAdobeプランと製品を保持できます。

>[!IMPORTANT]
>Adobe IDは、Adobeのアプリケーションやサービスを使用して、安全でパーソナライズされたエクスペリエンスを実現するために不可欠で、Adobe製品を購入する場合に必要です。 Adobe IDを使用すると、1つのアカウントに関連付けられたすべてのAdobeプランと製品を保持できます。 詳しくは、[Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)の作成または更新を参照してください。

次の3種類のAdobe IDの使用方法があります。

* **個人ID**:これはデフォルトのアカウントタイプです。基本的に、ユーザーはadobe.comでアカウントを作成する必要があります。 つまり、このアカウントはAdobeが管理し、誰でもこのタイプのアカウントを作成できます。

* **Enterprise ID**:組織は通常、ユーザーのアカウントの制御を強化したいと考えています。Enterprise IDでは、システム管理者のみがこれらのタイプのアカウントを作成でき、組織はこれらのアカウントを所有しています。Adobeは、これらをホストするだけです。

* **Federated ID**:組織がアカウントの完全な所有権と管理権を取得する場所です。この場合、Adobe Experience CloudをSAML2 SSOシステムと統合する必要があります。 最後の結果は、ユーザーが、Adobeでホストされるアカウントに対してではなく、会社のSSOシステムに対して認証をおこなうことです。 詳しくは、[SAML 2.0認証ハンドラー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=ja)を参照してください。

>[!NOTE]
>Enterprise IDまたはFederated IDがまだ設定されていない場合は、システム管理者が個人IDを使用してチームのオンボーディングを行うこともできます。EnterpriseまたはFederated IDの設定が完了したら、このIDを使用するようにメンバーを移行できます。