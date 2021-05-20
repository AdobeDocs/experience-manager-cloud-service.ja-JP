---
title: ユーザーマッピングツールの使用
description: ユーザーマッピングツールの使用
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: 7bdf8f1e6d8ef1f37663434e7b14798aeb8883f4
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 58%

---

# ユーザーマッピングツールの使用 {#user-mapping-tool}

## 概要 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="ユーザーマッピングツール"
>abstract="コンテンツ転送ツールを使用すると、ユーザーとグループを既存のAEMシステムからAEMにCloud Serviceとして移動できます。 Cloud Serviceオーサーインスタンス上でユーザーとグループが重複しないように、既存のユーザーとグループをIMS IDにマッピングする必要があります。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="ユーザーマッピングツール使用時の重要な考慮事項"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="ユーザーマッピングツールの使用"


Adobe Experience Manager（AEM）as a Cloud Service への移行の一環として、ユーザーとグループを既存の AEM システムから AEM as a Cloud Service に移行する必要があります。これには、コンテンツ転送ツールを使用します。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化され、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能です。詳しくは、[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=ja#identity-management) を参照してください。この変更により、Cloud Service オーサーインスタンスでのユーザーおよびグループの重複を避けるために、既存のユーザーおよびグループをそれぞれの IMS ID にマッピングする必要があります。

## 重要な検討事項 {#important-considerations}

### 例外的なケース{#exceptional-cases}

次の特定のケースがログに記録されます。

1. ユーザーの&#x200B;*jcr*&#x200B;ノードの`profile/email`フィールドに電子メールアドレスがない場合、該当するユーザーまたはグループは移行されますが、マッピングされません。

1. 使用する組織IDのIdentity Managementシステム(IMS)Adobeで特定の電子メールが見つからない場合（または別の理由でIMS IDを取得できない場合）、該当するユーザーまたはグループは移行されますが、マッピングされません。

1. ユーザーが現在無効になっている場合は、無効になっていない場合と同じように扱われます。通常どおりマッピングおよび移行され、クラウドインスタンス上では無効のままになります。

1. ターゲットAEMCloud Serviceインスタンス上に、ソースAEMインスタンス上のユーザーと同じユーザー名(rep:principalName)を持つユーザーが存在する場合、該当するユーザーまたはグループは移行されません。

### その他の考慮事項{#additional-considerations}

* 「**取得前にCloudインスタンス上の既存のCloud Serviceを消去**」設定が指定されている場合、既に転送されたユーザーは既存のリポジトリ全体と共に削除され、コンテンツを取り込むための新しいリポジトリが作成されます。 また、ターゲットCloud Serviceインスタンスに対する権限を含むすべての設定もリセットされ、管理者ユーザーが&#x200B;**administrators**&#x200B;グループに追加された場合はtrueになります。 CTTのアクセストークンを取得するには、管理者ユーザーを&#x200B;**administrators**&#x200B;グループに再追加する必要があります。

* ユーザーマッピングを使用してCTTを実行する前に、ターゲットCloud ServiceのAEMインスタンスから既存のユーザーを削除することをお勧めします。 これは、ユーザーをソースのAEMインスタンスからターゲットのAEMインスタンスに移行する際の競合を防ぐためです。 ソースAEMインスタンスとターゲットAEMインスタンスに同じユーザーが存在する場合、取り込み中に競合が発生します。

* コンテンツ追加を行う際、前回の転送以降に変更がなかったのでコンテンツが転送されない場合、その間にユーザやグループが変更されても、そのコンテンツに関連付けられたユーザやグループも転送されない。 これは、ユーザーとグループが、関連付けられているコンテンツと共に移行されるためです。

* 取り込みは次のシナリオで失敗します。

1. ターゲットのAEMCloud Serviceインスタンスに、別のユーザー名を持つが、ソースのAEMインスタンスのユーザーの1人と同じEメールアドレスを持つユーザーがいる場合。

1. ソースAEMインスタンス上に、ユーザー名は異なり、Eメールアドレスが同じ2人のユーザーがいる場合。 AEM as aCloud Serviceでは、2人のユーザーに同じ電子メールアドレスを割り当てることはできません。

## ユーザーマッピングツールの使用 {#using-user-mapping-tool}

Adobeマッピングツールは、Identity Management System(IMS)ユーザーを電子メールで検索し、そのIMS IDを返すAPIを使用します。 この API では、ユーザーが自分の組織のクライアント ID、クライアントシークレット、アクセスまたはベアラートークンを作成する必要があります。

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
