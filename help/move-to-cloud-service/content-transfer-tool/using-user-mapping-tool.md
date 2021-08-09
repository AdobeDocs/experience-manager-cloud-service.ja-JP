---
title: ユーザーマッピングツールの使用
description: ユーザーマッピングツールの使用
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: a9119ac04762c91230d52d6418b7808bca7e9f9f
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 93%

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

コンテンツ転送ツール（ユーザーマッピングなし）は、移行されるコンテンツに関連付けられているすべてのユーザーとグループを移行します。 Cloud Serviceマッピングツールはコンテンツ転送ツールの一部で、AEM as a  as a User. これらの変更が完了すると、コンテンツ転送ツールは、指定されたコンテンツのユーザーとグループを通常どおり移行します。

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

* 取り込みが失敗するのは、次のシナリオの場合です。

1. ユーザー名は異なるものの、ソース AEM インスタンスのいずれかのユーザーと同じ電子メールアドレスを持つユーザーが、ターゲット AEM Cloud Service インスタンスに存在する場合。

1. ユーザー名が異なり電子メールアドレスが同じ 2 人のユーザーがソース AEM インスタンスに存在する場合。AEM as a Cloud Service では、2 人のユーザーが同じ電子メールアドレスを持つことはできません。

## ユーザーマッピングツールの使用 {#using-user-mapping-tool}

ユーザーマッピングツールで使用される API は、Adobe Identity Management System（IMS）ユーザーを電子メールアドレスで検索して、各ユーザーの IMS ID を返すことができます。この API では、ユーザーが自分の組織のクライアント ID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

これを設定するには、次の手順に従います。

1. Adobe ID を使用して [Adobe 開発者コンソール](https://console.adobe.io)に移動します。
1. 新しいプロジェクトを作成するか、既存のプロジェクトを開きます。
1. API を追加します。
1. 「User Management API」を選択します。
1. JWT 資格情報を作成します。
1. キーペアを生成するか、公開鍵（rsa 以外）をアップロードします。
1. アクセストークン（または JWT トークンかベアラートークン）を生成します。
1. **クライアント ID**、**クライアントシークレット**、**テクニカルアカウント ID**、**テクニカルアカウント電子メールアドレス**、**組織 ID**、**アクセストークン**&#x200B;などの情報をすべて安全に保存します。

## ユーザーインターフェイス {#user-interface}

ユーザーマッピングツールは、コンテンツ転送ツールに統合されています。コンテンツ転送ツールは[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)からダウンロードできます。最新バージョンについて詳しくは、[最新のリリースノート](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

1. Adobe Experience Manager を選択し、ツール／**運営**／**コンテンツ転送**&#x200B;に移動します。
1. 「**ユーザーマッピング設定を作成**」をクリックします。

   >[!NOTE]
   >この手順をスキップすると、ユーザーおよびグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   User Management API 設定のフィールドに、下記のように値を入力します。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **組織 ID**：ユーザーが移行する組織の Adobe Identity Management System（IMS）組織 ID を入力します。

      >[!NOTE]
      >組織 ID を取得するには、[Admin Console](https://adminconsole.adobe.com/) にログインし、（右上の領域で）組織を選択します（複数の組織に属している場合）。組織 IDは、そのページの URL に `xx@AdobeOrg` のような形式で含まれます（xx が IMS 組織 ID です）。または、アクセストークンを生成した [Adobe 開発者コンソール](https://console.adobe.io)ページでも組織 ID が見つかります。

   * **クライアントID**：設定手順で保存したクライアント ID を入力します。

   * **アクセストークン**：設定手順で保存したアクセストークンを入力します。

      >[!NOTE]
      >アクセストークンの有効期限は 24 時間で切れるので、そのたびに新しいアクセストークンを作成する必要があります。新しいトークンを作成するには、[Adobe 開発者コンソール](https://console.adobe.io)に戻り、プロジェクトを選択し、「**User Management API**」をクリックして、同じ秘密鍵をボックスに貼り付けます。

1. 上記の情報を入力したら、「**保存**」をクリックします。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. 移行セットを作成するには、「**移行セットを作成**」をクリックし、各フィールドに値を入力して、「**保存**」をクリックします。詳しくは、[コンテンツ転送ツールの実行](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)を参照してください。

   >[!NOTE]
   >「IMS ユーザーおよびグループからのマッピングを含める」の切り替えスイッチがデフォルトでオンになっています。この設定の場合は、この移行セットに対して抽出を実行すると、ユーザーマッピングツールが抽出段階の一環として実行されます。コンテンツ転送ツールの抽出段階を実行するには、この方法をお勧めします。この切り替えをオフにした場合やユーザーマッピング設定を作成しない場合、ユーザーおよびグループのマッピングは抽出段階でスキップされます。

   ![画像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 抽出段階を実行するには、[コンテンツ転送ツールの実行](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)を参照してください。
