---
title: 'チーム・メンバーのAEM as a Cloud Service製品プロファイルへの割り当て '
description: このページでは、チームメンバーをAEM as a Cloud Service製品プロファイルに割り当てる方法について説明します
hide: true
hidefromtoc: true
index: false
source-git-commit: fa61dc122cec5466827d06ffb2eca1c1c5f8bae6
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---


# チーム・メンバーのAEM as a Cloud Service製品プロファイルへの割り当て {#assign-team-members-cloud-service}

## 目的 {#objective}

このドキュメントでは、チームメンバーをCloud Service製品プロファイルとしてAEMに割り当てるためにシステム管理者が実行する必要がある手順と、AEM作成者がAEMを使用してジャーニーを開始できるようにすることが重要な理由を説明します。

この節を読むと、次の内容を理解できます。

* チームメンバーが製品プロファイルとしてAEMに割り当てられる理由と方法。
* チームメンバーをAEM User製品プロファイルに追加する方法。
* チームメンバーをAEM Administrators製品プロファイルに追加する方法。


## はじめに {#introduction}

AEM as aCloud Serviceユーザーに対するアクセス権を付与するには、*AEM Users*&#x200B;または&#x200B;*AEM Administrators*&#x200B;など、2つの製品プロファイルのいずれかに属している必要があります。 Cloud Managerを管理する権限では不十分なので、チームメンバーにAEMインスタンスに対する権限を付与する必要があります。 詳細情報を参照してください。

>[!NOTE]
>システム管理者がAEMユーザー製品プロファイルに割り当てたすべてのユーザーは、Cloud Managerに（読み取り専用）アクセスできます。

## 前提条件 {#prerequisites}

この節を読む前に、次の前提条件を検討する必要があります。

* [AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)について
* [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)について
* Cloud Managerの製品プロファイルが必要に応じてチームメンバーに割り当てられ、クラウドリソースが設定されている
* チームメンバーの詳細：システム管理者は、AEM as aCloud Serviceへのアクセスが必要なチームメンバーの名前と電子メールアドレス、役割と責任を持っている必要があります。

   >[!NOTE]
   >オンボーディングを目的として、最初に管理者、開発者、コンテンツ作成者など、即時タスクに参加するユーザーを追加することをお勧めします。 すべてのユーザーを追加することなく、残りのオンボーディングを続行できます。 オンボーディングが完了したら、後でより多くのユーザーに拡大できます。


1. Admin Consoleへのログイン
（以前と同じ）

1. AEM as aCloud Service製品プロファイルの確認
Admin Consoleから、Cloud Managerのプロファイルのリストを確認できます。 次の手順を実行します。

1. Adobe Admin Consoleにログインしたら、製品とサービスカードでAdobe Experience Manager as a Cloud Serviceを選択します。

1. 次の図に示すように、インスタンス（開発環境のオーサーインスタンス）に移動して選択します。



   これで、AEMの役割に基づいてCloud Serviceに割り当てる必要がある製品プロファイルとしてのリストを確認できます。 これらの詳細については、 AEM as a Cloud Service製品プロファイルを参照してください。


## AEMユーザーまたはAEM管理者製品プロファイルへのチームメンバーの追加 {#add-team-members}

AEM as aCloud Serviceインスタンスへのアクセス権を付与するには、ユーザーが「AEM Users」または「AEM Administrators」の2つの製品プロファイルのいずれかに属している必要があります。

>[!NOTE]
>インスタンスに対する権限を付与されている必要があります。Cloud Managerを管理する権限では不十分です。 詳細情報を参照してください。

以下の手順に従う必要があるのは、ビジネスオーナーの役割も持つシステム管理者です。

1. Cloud ManagerからCloud Managerに移動し、次に示すように、目的の環境のコンテキストで「アクセスを管理」ボタンを選択します。

1. 「アクセスを管理」をクリックすると、新しいタブが表示され、環境のオーサーインスタンスにアクセスできるAdmin Consoleに移動します。 *AEM Administrators*&#x200B;または&#x200B;*AEM Users*&#x200B;を、この個人が付与する必要がある権限に基づいて選択します。 [AEM as aCloud Service製品プロファイル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)の詳細をご覧ください。

1. 以下に示すように「ユーザーを追加」を選択し、必要な詳細を送信してチームメンバーの追加を完了します。


1. アクセス権を必要とするチームメンバーの情報を持っている場合は、開発、ステージング、実稼動を含むすべての環境に対して、これらの手順を繰り返します。

   追加したユーザーは、AEM as a User Authorサービスにアクセスできます。


## 次の作業 {#whats-next}

これで、AEMにCloud Service製品プロファイルとして割り当てたCloud Serviceは、作成者にアクセスする方法と、AEM as a Usitorのページのオーサリングについて理解する方法を学ぶ準備が整いました。 パスに従う必要があります。次に、「 AEM Usersの学習パス」ドキュメントを確認します。

## その他のリソース {#additional-resources}

AEMへのアクセスの設定（ビデオウォークスルー）
ページのオーサリングのクイックスタートガイド
