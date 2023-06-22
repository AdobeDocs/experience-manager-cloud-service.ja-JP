---
title: ユーザーマッピングツールの使用（従来）
description: ユーザーマッピングツールの使用（従来）
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 1fc57dacbf811070664d5f5aaa591dd705516fa8
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 49%

---

# ユーザーマッピングツールの使用（レガシー） {#using-user-mapping-tool}

>[!INFO]
>
>このドキュメントでは、ツールの廃止バージョンを参照しています。 最新バージョンについて詳しくは、 [ユーザーマッピングとプリンシパルの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

ユーザーマッピングツールで使用される API は、Adobe Identity Management System（IMS）ユーザーをメールアドレスで検索して、各ユーザーの IMS ID を返すことができます。この API では、ユーザーが自分の組織のクライアント ID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

## ユーザーマッピングツールのセットアップ {#setting-up-user-mapping}

**前提条件：**&#x200B;ユーザーマッピングでは、IMS ID にマッピングされる各ユーザーは、AEM のプロファイルと IMS にメールアドレスを持っている必要があります。ユーザーがログイン時に電子メールアドレスをユーザー ID として使用している場合でも、電子メールアドレスがプロファイルにも IMS にも存在しない限り、そのユーザーに対するマッピングは機能しません。

これを設定するには、次の手順に従います。

1. Adobe ID を使用して [Adobe 開発者コンソール](https://developer.adobe.com/console/)に移動します。
1. プロジェクトを作成するか、既存のプロジェクトを開きます。
1. API を追加します：「**プロジェクトに追加**」をクリックして、「**API**」を選択します。
1. 「User Management API」を選択します。このオプションを使用するには、システム管理者の権限が必要です。
1. JWT 資格情報を作成します。
1. キーペアを生成するか、公開鍵（rsa 以外）をアップロードします。ボタンがある **公開鍵/秘密鍵のペアを生成** これにより、このキーペアが作成されます。 必ず、公開鍵と秘密鍵の両方を保存してください。
1. User Management API に移動します。
1. テキストボックスに秘密鍵のコンテンツを貼り付け、「 」をクリックして、アクセストークン（または bearer トークン）を生成します。 **トークンを生成**.
1. **クライアント ID**、**クライアントシークレット**、**テクニカルアカウント ID**、**テクニカルアカウントメールアドレス**、**組織 ID**、**アクセストークン**&#x200B;などの情報をすべて安全に保存します。

## ユーザーマッピングツールのユーザーインターフェイスへのアクセス {#user-interface}

ユーザーマッピングツールは、コンテンツ転送ツールに統合されています。コンテンツ転送ツールは[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からダウンロードできます。最新バージョンについて詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ移行**&#x200B;に移動します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 次をクリック： **ユーザーマッピング** カード。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. クリック **ユーザーマッピング設定を作成**.

   >[!NOTE]
   >この手順をスキップした場合、抽出段階でユーザーとグループのマッピングはスキップされます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   **User Management API 設定**&#x200B;のフィールドに、下記のように値を入力します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織 ID**:ユーザーを移行する組織のAdobeIdentity Managementシステム (IMS) 組織 ID を入力します。

     >[!NOTE]
     >組織 ID を取得するには、 [Admin Console](https://adminconsole.adobe.com/) 複数のに属している場合は、（右上の領域で）組織を選択します。 組織 ID は、そのページの URL に、のような形式で含まれます。 `xx@AdobeOrg`（ xx は IMS Org ID です）。 または、アクセストークンを生成した [Adobe 開発者コンソール](https://developer.adobe.com/console/)ページでも組織 ID が見つかります。

   * **クライアントID**：設定手順で保存したクライアント ID を入力します。

   * **アクセストークン**：設定手順で保存したアクセストークンを入力します。

     >[!NOTE]
     >アクセストークンの有効期限は 24 時間ごとに切れ、新しく作成する必要があります。 トークンを作成するには、 [Adobe Developer Console](https://developer.adobe.com/console/)、プロジェクトを選択、 **ユーザー管理 API**&#x200B;をクリックし、ボックスに同じ秘密鍵を貼り付けます。

1. フィールドに値を入力した後、 **設定をテスト** をクリックして、User Management API サービスへの接続をテストします。 接続に成功した場合は、 **保存** 設定を保存します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 設定を保存したら、設定を選択し、 **ユーザーマッピングを開始**.

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. クリック **開始** をクリックして、ユーザーマッピングプロセスを開始します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   「**ステータス**」が&#x200B;**実行中**&#x200B;と表示されます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. ユーザーマッピングが完了したら、「 **結果** をクリックして概要を表示します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* ユーザーマッピングが完了したら、パンくずリストを使用してコンテンツ移行ページに戻ることができます。 ユーザーマッピングカードにステータスとタイムスタンプが表示されます。クリック **コンテンツ転送** そのため、抽出を実行する移行セットを作成できます。 詳しくは、 [コンテンツ転送ツールの実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#running-tool) を参照してください。

### ユーザーマッピングプロセスの再開 {#resume-user-mapping-process}

次のいずれかの理由でユーザーマッピングプロセスが停止した場合、

* オプション **ユーザーマッピングの停止** がユーザーによって選択されました。
* プロセス中にアクセストークンの有効期限が切れました。
* 別の理由でも

  >[!NOTE]
  >進行状況がプロセスの停止位置から保存されます。

ユーザーマッピングプロセスを再開するには、次の手順に従います。

1. クリック **ログを表示** をクリックしてユーザーマッピングログを確認し、保存した進行状況を確認できます。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. クリック **ユーザーマッピングを開始** ボタンを再度クリックすると、中断した位置から再開できます。

   >[!NOTE]
   >再起動する前に、アクセストークンが引き続き有効であるか、更新されていることを確認してください。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. クリック **開始** をクリックして、ユーザーマッピングプロセスを再開します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   ユーザーマッピングプロセスが完了したら、 **ステータス** as **完了** を設定します。

   ![画像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
