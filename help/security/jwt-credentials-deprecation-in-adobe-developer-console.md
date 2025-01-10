---
title: Adobe Developer Console での JWT 資格情報の廃止
description: AEM の Adobe Developer Console での JWT 資格情報の廃止の影響について説明します。
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 957dedd81d14e921aa8a64de80ef21fd11f713ab
workflow-type: ht
source-wordcount: '768'
ht-degree: 100%

---

# Adobe Developer Console での JWT 資格情報の廃止 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM 6.5 のお客様は、[AEM 6.5 の同等のドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console)を参照して、詳細を確認する必要があります。

アドビのお客様は、[Adobe Developer Console](https://developer.adobe.com/console) を使用すると、様々な API へのアクセスを可能にする資格情報を生成できます。お客様は、OAuth サーバー間からシングルページアプリまで、様々な資格情報タイプから選択できます。これらの資格情報タイプの 1 つであるサービスアカウント（JWT）資格情報は、OAuth サーバー間資格情報に代わって非推奨（廃止予定）になりました。新しいサービスアカウント（JWT）資格情報は 2024年6月3日（PT）以降は作成できなくなり、既存の JWT 資格情報は 2025年6月30日（PT）以降は機能しなくなります。非推奨（廃止予定）については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)を参照してください。

この記事では、AEM as a Cloud Service で非推奨（廃止予定）にどのように対処する必要があるかに関する追加のコンテキストを提供します。

主なポイントは、AEM で AEM as a Cloud Service の新しい OAuth サーバー間資格情報をサポートするようになったということです。JWT 資格情報を移行する手順が記載されたメールを受信した場合は、この移行を今すぐ実行できます。

以下の節では、AEM でサポートするようになり、お客様がサービスアカウント（JWT）資格情報を OAuth サーバー間資格情報に置き換える必要がある（場合によっては置き換えてはいけない）シナリオを示します。資格情報を移行する方法については、[こちら](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)を参照してください。

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)（**Adobe** Developer Console と区別するために名前に **AEM** が含まれています）では、サーバー間 API に使用される [JWT トークン](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)を生成するユーティリティを提供します。これらの資格情報は非推奨（廃止予定）ではなく、引き続き使用できます。

## AEM と他のアドビソリューションの統合 {#integrating-aem-with-other-adobe-solutions}

**アクション**：AEM で OAuth 資格情報をサポートするようになったので、設定を移行します。

**関連する AEM バージョン**：AEM as a Cloud Service

AEM のお客様は、AEM を使用して、他の多くの Adobe ソリューションとの統合を設定します。例えば、Adobe Target、Adobe Analytics などです。

次の方法について詳しくは、[AEM as a Cloud Service の IMS 統合の設定](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)を参照してください。

* OAuth 資格情報を使用した設定の作成
* JWT 資格情報を使用して作成された設定を移行した、OAuth 資格情報の使用

## Cloud Manager API {#cloud-manager-apis}

**アクション**：JWT 資格情報を、Cloud Manager がサポートを開始した OAuth 資格情報に移行します。

**関連する AEM バージョン**：AEM as a Cloud Service

お客様は Adobe Developer Console プロジェクトを作成すると、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) を呼び出すことができます。廃止予定の JWT 資格情報の有効期限（2025年6月）が切れる前に、Adobe Developer プロジェクトの資格情報を OAuth サーバー間資格情報タイプに移行する必要があります。

## 自動生成されたプロジェクト {#autogen-projects}

**アクション**：アドビがお客様に代わって移行するので、お客様側では移行しないでください。

**関連する AEM バージョン**：AEM as a Cloud Service。

Cloud Manager で AEM as a Cloud Service 環境をプロビジョニングすると、JWT 資格情報を使用して Adobe Developer Console プロジェクトが自動生成されます。以下のスクリーンショットに示すように、このプロジェクトは読み取り専用としてマークされます。お客様は、これらのプロジェクトを OAuth サーバー間資格情報に移行することはできません。移行しようとしないでください。代わりに、アドビでは、資格情報が使用できなくなる前に、これらのプロジェクトを独自に移行します。

![自動生成されたプロジェクト](/help/security/assets/jwt-deprecation-autogen-projects.png)

## 自動生成されたプロジェクトに関する FAQ {#autogen-projects-faqs}

この節では、AEM as a Cloud Service で自動生成されたプロジェクトに対する JWT 資格情報の廃止に関してよくある質問とその回答を示します。

**自動生成されたプロジェクトを選択するにはどうすればよいですか？**

Adobe Developer Console の「プロジェクト」セクションに移動します。AEM as a Cloud Service の自動生成されたプロジェクトには、「自動生成」識別子の付いたロックアイコンが表示されます。自動生成されたプロジェクトは、AEM-p#####-e###### の形式に従って、テクニカルアカウントユーザーによって作成されます。

![自動生成されたプロジェクト](/help/security/assets/jwt-alert.png)

**自動生成されたプロジェクトで問題が発生した場合はどうなりますか？**

[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。

**自動生成されたプロジェクトを移行する必要はありますか？**

AEM リリース 17258（2024年8月）以降の環境では、アドビがお客様に代わって自動生成して移行するので、アクションは必要ありません。

**自動生成されたプロジェクトの移行タイムラインはどのようになりますか？**

アドビは、開発環境から始めて、2025年第 1 四半期に段階的な移行アプローチを開始する予定です。

**AEM リリース 17258（2024年8月）より古い AEM リリースがある場合、AEM as a Cloud Service インスタンスはどのような影響を受けますか?**

自動生成されたプロジェクト統合は、2025年6月までに OAuth に移行されない場合、機能しなくなります。

スムーズな移行を確実に行うために、お客様は[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)に迅速に連絡し、[最新の AEM リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)への更新処理を開始する必要があります。これにより、回帰テストに十分な時間を確保でき、アドビはプロジェクトの移行を効率的に管理できます。

**AEM as a Cloud Service AEM リリースをアップグレードせずに、サポートされている OAuth バージョンにアップグレードできますか？**

いいえ。スムーズな移行を確実に行うために、お客様は[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)に迅速に連絡し、[最新の AEM リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest)への更新処理を開始する必要があります。これにより、回帰テストに十分な時間を確保でき、アドビはプロジェクトの移行を効率的に管理できます。
