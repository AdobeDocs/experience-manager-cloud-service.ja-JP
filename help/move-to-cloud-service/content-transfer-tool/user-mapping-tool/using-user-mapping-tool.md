---
title: ユーザーマッピングツールの使用
description: ユーザーマッピングツールの使用
source-git-commit: 2f763f774b21b0c3b43d61964dda2d2ae596161a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 62%

---


# ユーザーマッピングツールの使用 {#using-user-mapping-tool}

ユーザーマッピングツールで使用される API は、Adobe Identity Management System（IMS）ユーザーを電子メールアドレスで検索して、各ユーザーの IMS ID を返すことができます。この API では、ユーザーが自分の組織のクライアント ID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

## ユーザーマッピングツールの設定 {#setting-up-user-mapping}

これを設定するには、次の手順に従います。

1. Adobe ID を使用して [Adobe 開発者コンソール](https://console.adobe.io)に移動します。
1. 新しいプロジェクトを作成するか、既存のプロジェクトを開きます。
1. API を追加 — **プロジェクトに追加** をクリックし、**API** を選択します
1. 「User Management API」を選択します。このオプションを使用するには、権限の取得が必要になる場合があります。
1. JWT 資格情報を作成します。
1. キーペアを生成するか、公開鍵（rsa 以外）をアップロードします。**公開鍵と秘密鍵のペアを生成** するボタンがあります。  公開鍵と秘密鍵の両方を保存してください。
1. ユーザー管理 API に移動します。
1. 秘密鍵の内容をテキストボックスに貼り付けて「**トークンを生成**」をクリックし、アクセストークン（または bearer トークン）を生成します。
1. **クライアント ID**、**クライアントシークレット**、**テクニカルアカウント ID**、**テクニカルアカウント電子メールアドレス**、**組織 ID**、**アクセストークン**&#x200B;などの情報をすべて安全に保存します。

## ユーザー・マッピング・ツールのユーザー・インタフェースへのアクセス {#user-interface}

ユーザーマッピングツールは、コンテンツ転送ツールに統合されています。コンテンツ転送ツールは[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からダウンロードできます。最新バージョンについて詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ移行**&#x200B;に移動します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. **User Mapping** カードをクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 「**ユーザーマッピング設定を作成**」をクリックします。

   >[!NOTE]
   >この手順をスキップすると、ユーザーおよびグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   **User Management API 設定** のフィールドに、以下のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織 ID**：ユーザーが移行する組織の Adobe Identity Management System（IMS）組織 ID を入力します。

      >[!NOTE]
      >組織 ID を取得するには、[Admin Console](https://adminconsole.adobe.com/) にログインし、（右上の領域で）組織を選択します（複数の組織に属している場合）。組織 IDは、そのページの URL に `xx@AdobeOrg` のような形式で含まれます（xx が IMS 組織 ID です）。または、アクセストークンを生成した [Adobe 開発者コンソール](https://console.adobe.io)ページでも組織 ID が見つかります。

   * **クライアントID**：設定手順で保存したクライアント ID を入力します。

   * **アクセストークン**：設定手順で保存したアクセストークンを入力します。

      >[!NOTE]
      >アクセストークンの有効期限は 24 時間で切れるので、そのたびに新しいアクセストークンを作成する必要があります。新しいトークンを作成するには、[Adobe 開発者コンソール](https://console.adobe.io)に戻り、プロジェクトを選択し、「**User Management API**」をクリックして、同じ秘密鍵をボックスに貼り付けます。

1. フィールドに値を入力したら、「**設定をテスト**」をクリックして、User Management API サービスへの接続をテストします。 接続に成功した場合は、「**保存**」をクリックして設定を保存できます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 設定を保存したら、設定を選択し、「**Start User Mapping**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. ユーザーマッピングが完了したら、「**結果**」をクリックして概要を表示します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >ユーザーマッピングが完了したら、パンくずリストを使用してコンテンツ移行ページに戻ることができます。 「ユーザーマッピング」カードにステータスとタイムスタンプが表示されます。 「**コンテンツ転送**」をクリックして、抽出を実行する移行セットを作成します。 詳しくは、[ コンテンツ転送ツールの実行 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) を参照してください。
