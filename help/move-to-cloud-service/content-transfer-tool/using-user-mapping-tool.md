---
title: ユーザーマッピングツールの使用
description: ユーザーマッピングツールの使用
translation-type: tm+mt
source-git-commit: d1a944606a88a0afded94592676f14c0ba84e954
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 8%

---


# ユーザーマッピングツールの使用{#user-mapping-tool}

## 概要 {#overview}

トランジションジャーニーの一環として、Cloud ServiceとしてAdobe Experience Manager(AEM)にユーザーとグループを移動するには、既存のAEMシステムからAEMにCloud Serviceとしてユーザーとグループを移動する必要があります。 これは、コンテンツ転送ツールで行います。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。これには、ユーザーとユーザーグループの管理に[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html)を使用する必要があります。 ユーザープロファイル情報は、AdobeIdentity Managementシステム(IMS)に一元化され、すべてのAdobeクラウドアプリケーションにシングルサインオンを提供します。 詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)を参照してください。 この変更により、Cloud Service作成者インスタンス上の重複ユーザーとグループを回避するために、既存のユーザーとグループをIMS IDにマッピングする必要があります。

## 重要な検討事項 {#important-considerations}

考慮すべき例はいくつかある。 次の特定のケースがログに記録され、該当するユーザーまたはグループはマッピングされません。

1. ユーザーの&#x200B;*jcr*&#x200B;ノードの`profile/email`フィールドに電子メールアドレスがない場合。

1. 使用している組織IDのAdobeIdentity Managementシステム(IMS)システムで特定の電子メールが見つからない場合（または、別の理由でIMS IDを取得できない場合）。

1. ユーザーが現在無効になっている場合は、無効になっていない場合と同じように扱われます。 通常どおりマップおよび移行され、クラウドインスタンスでは無効のままになります。

## ユーザーマッピングツールの使用{#using-user-mapping-tool}

ユーザーマッピングツールはAPIを使用します。このAPIを使用すると、AdobeIdentity Managementシステム(IMS)ユーザーを電子メールで検索し、IMS IDを返すことができます。 このAPIでは、ユーザーは組織のクライアントID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

この設定を行うには、次の手順に従います。

1. Adobe IDを使用して[Adobeデベロッパーコンソール](https://console.adobe.io)に移動します。
1. 新しいプロジェクトを作成するか、既存のプロジェクトを開きます。
1. API追加。
1. 「ユーザー管理API」を選択します。
1. JWT秘密鍵証明書を作成します。
1. キーペアを生成するか、公開鍵をアップロードします（rsaは良くありません）。
1. アクセストークン（またはJWTトークンまたはベアラトークン）を生成します。
1. **クライアントID**、**クライアントシークレット**、**テクニカルアカウントID**、**テクニカルアカウント電子メール**、**組織ID**、**アクセストークンなど、すべて保存します**&#x200B;安全。

## ユーザーインターフェイス {#user-interface}

ユーザマッピングツールは、コンテンツ転送ツールに統合されています。 [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html)からContent Transfer Toolをダウンロードできます。 最新バージョンの詳細については、[現在のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ転送**&#x200B;に移動します。
1. 「**ユーザーマッピング設定を作成**」をクリックします。

   >[!NOTE]
   >この手順をスキップすると、ユーザーとグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   以下の説明に従って、User Management API設定のフィールドに値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **組織ID**:移行する組織のAdobeIdentity Managementシステム(IMS)組織IDを入力します。

      >[!NOTE]
      >組織IDを取得するには、[Admin Console](https://adminconsole.adobe.com/)にログインし、（右上の領域で）組織を選択します（複数の組織に属している場合）。 組織IDは、`xx@AdobeOrg`のような形式で、そのページのURLに含まれます。xxはIMS組織IDです。  組織IDは、アクセストークンを生成した[Adobe開発者コンソール](https://console.adobe.io)ページにあります。

   * **クライアントID**:設定手順で保存したクライアントIDを入力します。

   * **アクセストークン**:設定手順で保存したアクセストークンを入力します。

      >[!NOTE]
      >アクセストークンの有効期限は24時間ごとに切れ、新しいアイテムを作成する必要があります。 新しいトークンを作成するには、[Adobe開発者コンソール](https://console.adobe.io)に戻って、プロジェクトを選択し、**User Management API**&#x200B;をクリックして、ボックスに同じ秘密鍵を貼り付けます。

1. 上記の情報を入力したら、「**保存**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. **[移行セットの作成]**&#x200B;をクリックしてフィールドに値を入力し、**[保存]**&#x200B;をクリックして、移行セットを作成します。 詳しくは、[コンテンツ転送ツールの実行](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)を参照してください。

   >[!NOTE]
   >切り替えスイッチで、「Mapping Users from IMS Users and Groups」がデフォルトでオンになっています。 この設定を使用すると、この移行セットで抽出が実行されると、ユーザーマッピングツールは抽出段階の一部として実行されます。 これは、コンテンツ転送ツールの抽出段階を実行する場合に推奨される方法です。 この切り替えをオフにした場合、またはユーザマッピング設定が作成されない場合、ユーザとグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 抽出フェーズを実行するには、「[コンテンツ転送ツールの実行](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)」を参照してください。



