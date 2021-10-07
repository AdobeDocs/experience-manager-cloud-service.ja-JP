---
title: ユーザーマッピングツールの使用
description: ユーザーマッピングツールの使用
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 69%

---

# ユーザーマッピングツールの使用 {#user-mapping-tool}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピングツール"
>abstract="コンテンツ転送ツールは、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移動する際に役に立ちます。Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#important-considerations" text="ユーザーマッピングツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool" text="ユーザーマッピングツールの使用"

Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。これには、コンテンツ転送ツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。

### ユーザーマッピングツール {#mapping-tool}

コンテンツ転送ツール（ユーザーマッピングなし）は、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。 ユーザーマッピングツールはコンテンツ転送ツールの一部で、AEM as a Cloud Serviceで使用されるシングルサインオン機能である IMS で正しく認識されるようにユーザーとグループを変更することだけが目的です。 これらの変更が完了すると、コンテンツ転送ツールは、指定したコンテンツのユーザーとグループを通常どおり移行します。

## 重要な検討事項 {#important-considerations}

### 例外的な状況 {#exceptional-cases}

次のような状況になった場合は、ログに記録されます。

1. ユーザーの *jcr* ノードの `profile/email` フィールドに電子メールアドレスがない場合、該当するユーザーまたはグループは移行されますが、マッピングされません。

1. 使用している組織 ID に対応する Adobe Identity Management System（IMS）システムで特定の電子メールが見つからない場合（または、別の理由で IMS ID を取得できない場合）、該当するユーザーまたはグループは移行されますが、マッピングされません。

1. ユーザーが現在無効になっている場合は、無効になっていない場合と同じように扱われます。通常どおりマッピングおよび移行され、クラウドインスタンス上では無効のままになります。

1. ソース AEM インスタンスのいずれかのユーザーと同じユーザー名（rep:principalName）のユーザーがターゲット AEM Cloud Service インスタンスに存在する場合、該当するユーザーまたはグループは移行されません。

### その他の考慮事項 {#additional-considerations}

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが設定されている場合は、Cloud Service インスタンス上の転送済みユーザーと既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。また、これにより、ターゲット Cloud Service インスタンスに対する権限を含むすべての設定もリセットされます。これは、**administrators** グループに追加された管理者ユーザーに対しても当てはまります。CTT のアクセストークンを取得するには、管理者ユーザーを **administrators** グループに再度追加する必要があります。

* ユーザーマッピングを使用して CTT を実行する前に、ターゲット Cloud Service AEM インスタンスから既存のユーザーを削除することをお勧めします。これは、ソース AEM インスタンスからターゲット AEM インスタンスにユーザーを移行する際に競合が発生するのを防ぐためです。ソース AEM インスタンスとターゲット AEM インスタンスに同じユーザーが存在する場合、取り込み中に競合が発生します。

* コンテンツ追加を行う際に、前回の転送以降変更がないのでコンテンツが転送されない場合は、その間にユーザーやグループが変更されたとしても、そのコンテンツに関連付けられたユーザやグループは転送されません。これは、ユーザーやグループの移行が、ユーザーやグループが関連付けられているコンテンツと共に行われるからです。

* ターゲットのAEM Cloud Serviceインスタンスのユーザー名が異なり、ソースのAEMインスタンスのユーザーの 1 人と同じ E メールアドレスを持つユーザーが存在し、ユーザーマッピングが有効な場合、エラーメッセージがログに書き込まれ、特定の E メールアドレスを持つ 1 人のユーザーのみがターゲットシステムで許可されます。

* ソースAEMインスタンス上の 2 人のユーザーが同じ E メールアドレスを持ち、ユーザーマッピングが有効な場合、エラーメッセージがログに書き込まれ、1 人のソースAEMユーザーは転送されません。特定の E メールアドレスを持つ 1 人のユーザーのみがターゲットシステムで許可されます。


## ユーザーマッピングツールの使用 {#using-user-mapping-tool}

ユーザーマッピングツールで使用される API は、Adobe Identity Management System（IMS）ユーザーを電子メールアドレスで検索して、各ユーザーの IMS ID を返すことができます。この API では、ユーザーが自分の組織のクライアント ID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

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

## ユーザーインターフェイス {#user-interface}

ユーザーマッピングツールは、コンテンツ転送ツールに統合されています。コンテンツ転送ツールは[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からダウンロードできます。最新バージョンについて詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

1. Adobe Experience Managerを選択し、ツール/ **操作** -> **ユーザーマッピング** に移動します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing1.png)

1. 「**ユーザーマッピング設定を作成**」をクリックします。

   >[!NOTE]
   >この手順をスキップすると、ユーザーおよびグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing2.png)

   **User Management API 設定** のフィールドに、以下のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing3.png)

   * **組織 ID**：ユーザーが移行する組織の Adobe Identity Management System（IMS）組織 ID を入力します。

      >[!NOTE]
      >組織 ID を取得するには、[Admin Console](https://adminconsole.adobe.com/) にログインし、（右上の領域で）組織を選択します（複数の組織に属している場合）。組織 IDは、そのページの URL に `xx@AdobeOrg` のような形式で含まれます（xx が IMS 組織 ID です）。または、アクセストークンを生成した [Adobe 開発者コンソール](https://console.adobe.io)ページでも組織 ID が見つかります。

   * **クライアントID**：設定手順で保存したクライアント ID を入力します。

   * **アクセストークン**：設定手順で保存したアクセストークンを入力します。

      >[!NOTE]
      >アクセストークンの有効期限は 24 時間で切れるので、そのたびに新しいアクセストークンを作成する必要があります。新しいトークンを作成するには、[Adobe 開発者コンソール](https://console.adobe.io)に戻り、プロジェクトを選択し、「**User Management API**」をクリックして、同じ秘密鍵をボックスに貼り付けます。

1. フィールドに値を入力したら、「**設定をテスト**」をクリックして、User Management API サービスへの接続をテストします。 接続に成功した場合は、「**保存**」をクリックして設定を保存できます。

1. 設定を保存したら、設定を選択し、「**Start User Mapping**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. ユーザーマッピングが完了したら、「**結果**」をクリックして概要を表示します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >ユーザーマッピングが完了したら、パンくずリストを使用してコンテンツ移行ページに戻ることができます。 「ユーザーマッピング」カードにステータスとタイムスタンプが表示されます。 「**コンテンツ転送**」をクリックして、抽出を実行する移行セットを作成します。 詳しくは、[ コンテンツ転送ツールの実行 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) を参照してください。
