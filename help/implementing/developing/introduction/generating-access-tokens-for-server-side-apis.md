---
title: サーバー側 API のアクセストークンの生成
description: セキュアな JWT トークンを生成してサードパーティサーバーと AEM as a Cloud Service の間の通信を容易にする方法について説明します。
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 41458eb1fba12e8ef45a32d3bb6fc5dd732f78ec
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 36%

---

# サーバー側 API のアクセストークンの生成 {#generating-access-tokens-for-server-side-apis}

>[!AVAILABILITY]
>
>Adobeは、この記事で説明する新しい多資格情報および資格情報の失効機能を徐々に展開する過程です。 組織のAEM開発者コンソールの「統合」タブを確認すると、画面が以下のスクリーンショットとは異なる場合、新しい変更はまだ組織にロールアウトされていないことを意味します。 この場合、 [レガシードキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis-legacy.md).

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持ち、AEM オーサーのAEM Users またはAEM Administrators 製品プロファイルのメンバーでもあるユーザーは、AEMのas a Cloud Serviceの資格情報のセットを生成できます。各資格情報は、証明書（公開鍵）、秘密鍵、次にから成る技術アカウントを含む JSON ペイロードです `clientId` および `clientSecret`. その後、これらの資格情報は、AEMas a Cloud Serviceの環境管理者の役割を持つユーザーが取得でき、AEM以外のサーバーにインストールして、秘密鍵として慎重に扱う必要があります。 この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータは、署名済みの JWT トークンの作成に使用され、AdobeのIdentity Management Services(IMS) と IMS アクセストークンと交換されます。 その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報に含まれる証明書は、デフォルトで 1 年後に期限切れになりますが、説明に従って、必要に応じて更新できます [ここ](#refresh-credentials).

サーバー間フローは次のステップで構成されます。

* 開発者コンソールから AEM as a Cloud Service 資格情報を取得する
* AEM に対して呼び出しを行う AEM 以外のサーバーに AEM as a Cloud Service 資格情報をインストールする
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service開発者コンソールへのアクセス権を持つユーザーには、特定の環境の開発者コンソールに「統合」タブが表示されます。 AEMas a Cloud Service環境管理者の役割を持つユーザーは、資格情報の作成、表示、管理をおこなうことができます。

クリック **新しいテクニカルアカウントを作成** ボタンをクリックすると、ポッドの選択に関係なく、環境のオーサー層とパブリッシュ層用のクライアント id、クライアントの秘密鍵、秘密鍵、証明書、設定を含む新しい資格情報のセットが作成されます。

![新しいテクニカルアカウントの作成](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

新しいブラウザータブが開き、資格情報が表示されます。 この表示を使用して、ステータスのタイトルの横にあるダウンロードアイコンをクリックすると、資格情報をダウンロードできます。

![認証情報のダウンロード](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

資格情報が作成されると、その資格情報が「 **テクニカルアカウント** 」タブをクリックします。 **統合** セクション：

![認証情報の表示](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

ユーザーは、後で表示アクションを使用して資格情報を表示できます。 また、証明書を更新または取り消す必要がある場合に備えて、後述のように、ユーザーは新しい秘密鍵または証明書を作成することで、同じテクニカルアカウントの資格情報を変更できます。

AEMas a Cloud Serviceの環境管理者の役割を持つユーザーは、後で追加のテクニカルアカウントの新しい資格情報を作成できます。 これは、API が異なればアクセス要件が異なる場合に役立ちます。 例えば、読み取りと読み取り/書き込みが可能です。

>[!NOTE]
>
>お客様は、既に削除されているテクニカルアカウントを含め、最大 10 個のテクニカルアカウントを作成できます。

>[!IMPORTANT]
>
>AEM オーサーインスタンスのAEMユーザーまたはAEM管理者製品プロファイルのメンバーでもある IMS 組織管理者（通常は Cloud Manager を使用して環境をプロビジョニングした同じユーザー）は、最初に開発者コンソールにアクセスし、 **新しいテクニカルアカウントを作成** ボタンを使用して、資格情報を生成し、AEMas a Cloud Service環境に対する管理者権限を持つユーザーが後で取得することができます。 IMS 組織管理者がこの操作をまだ行っていない場合は、IMS 組織管理者の役割が必要であることを通知するメッセージが表示されます。

### AEM 以外のサーバーへの AEM サービス資格情報のインストール {#install-the-aem-service-credentials-on-a-non-aem-server}

AEMを呼び出すアプリケーションは、AEMのas a Cloud Serviceの資格情報にアクセスし、秘密鍵として扱うことができます。

### JWT トークンの生成とアクセストークンとの交換  {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

アクセストークンを取得するには、アドビの IMS サービスへの呼び出しで資格情報を使用して JWT トークンを作成します。このトークンは 24 時間有効です。

AEM CS サービス資格情報は、専用のクライアントライブラリを使用して、アクセストークンと交換できます。このクライアントライブラリは、[アドビが公開している GitHub リポジトリー](https://github.com/adobe/aemcs-api-client-lib)から入手可能です。このリポジトリーには、より詳細なガイダンスと最新の情報が含まれています。

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

同じ交換は、正しい形式の署名済み JWT トークンの生成と IMS トークン交換 API の呼び出しが可能な任意の言語で実行できます。

アクセストークンには有効期限が定義されます（通常は 24 時間です）。Git リポジトリーには、アクセストークンを管理して期限切れの前に更新するサンプルコードが含まれています。

>[!NOTE]
>複数の資格情報がある場合は、後で呼び出されるAEMへの API 呼び出しに適した JSON ファイルを必ず参照してください。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

まず、新しい製品プロファイルをAdobe Admin Consoleで作成する必要があります。 これは、次の手順に従って実行できます。

1. Adobe Admin Console( ) に移動します。 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. を押します。 **管理** 下のリンク **製品とサービス** 列を左側に配置します。
1. 選択 **AEMas a Cloud Service**
1. を押します。 **新しいプロファイル** ボタン

   ![新しいプロファイル](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. プロファイルに名前を付け、 **保存**

   ![プロファイルを保存](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 作成したプロファイルをプロファイルリストから選択します
1. を押します。 **ユーザーを追加** ボタン

   ![ユーザーを追加](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 作成したテクニカルアカウントを追加します ( この場合は `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) をクリックし、 **保存**

   ![テクニカルアカウントを追加](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 変更が有効になるまで 10 分待ち、新しい資格情報から生成されたアクセストークンでAEMに対する API 呼び出しをおこないます。 cURL コマンドの場合、次の例のようになります。

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


API 呼び出しをおこなうと、製品プロファイルがAEMas a Cloud Serviceのオーサーインスタンスにユーザーグループとして表示され、適切なテクニカルアカウントがそのグループのメンバーとして表示されます。

これを確認するには、次の手順を実行する必要があります。

1. オーサーインスタンスにログインします。
1. に移動します。 **ツール** - **セキュリティ** をクリックし、 **グループ** カード
1. グループのリストで作成したプロファイルの名前を探し、それをクリックします。

   ![グループプロファイル](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 次のウィンドウで、 **メンバー** 」タブに移動し、テクニカルアカウントが正しく一覧表示されているかどうかを確認します。

   ![「メンバー」タブ](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


または、オーサーインスタンスで次の手順を実行して、テクニカルアカウントがユーザーリストに表示されることを確認することもできます。

1. に移動します。 **ツール** - **セキュリティ** - **ユーザー**
1. お使いのテクニカルアカウントがユーザーリストであることを確認し、それをクリックします
1. をクリックします。 **グループ** 」タブを使用して、ユーザーが製品プロファイルに対応するグループに属していることを確認します。 また、このユーザーは、寄稿者を含む一部の他のグループのメンバーでもあります。

   ![グループのメンバーシップ](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>2023 年半ば以前は、複数の資格情報を作成できる前は、Adobeの Admin Console で製品プロファイルを作成するガイドがおこなわれていなかったので、技術アカウントはAEMas a Cloud Serviceインスタンスの「寄稿者」以外のグループに関連付けられていませんでした。 一貫性を保つため、このテクニカルアカウントの場合は、前述のようにAdobe Admin Consoleで新しい製品プロファイルを作成し、既存のテクニカルアカウントをそのグループに追加することをお勧めします。

<u>**適切なグループ権限の設定**</u>

最後に、API を適切に呼び出すかロックダウンするために必要な適切な権限でグループを設定します。 次の方法で実行できます。

1. 適切なオーサーインスタンスにログインし、に移動します。 **設定** - **セキュリティ** - **権限**
1. 左側のパネルで製品プロファイルに対応するグループの名前（この場合は読み取り専用 API）を検索し、クリックします。

   ![グループを検索](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 次のウィンドウで「編集」ボタンをクリックします。

   ![権限を編集](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 権限を適切に変更し、「 **保存**

   ![権限の編集の確認](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Identity Management System(IMS)AdobeとAEMユーザーおよびグループについて詳しくは、 [ドキュメント](/help/security/ims-support.md).

## 開発者フロー {#developer-flow}

開発者は、AEM as a Cloud Service 開発環境に対してリクエストを行う AEM 以外のアプリケーションの開発インスタンス（ラップトップ上で動作するか他でホストされている）を使用してテストを行うことになります。ただし、開発者は必ずしも IMS 管理者の役割の権限を持ってはいないので、通常のサーバー間フローで説明されている JWT ベアラーを開発者が生成できるとは想定できません。したがって、アクセスできる AEM as a Cloud Service 環境へのリクエストで使用できるアクセストークンを開発者が直接生成するメカニズムが用意されています。

AEM as a Cloud Service 開発者コンソールの使用に必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
>
>ローカル開発アクセストークンは最大 24 時間有効で、その後は同じ方法で再生成する必要があります。

開発者は、このトークンを使用して AEM 以外のテストアプリケーションから AEM as a Cloud Service 環境に呼び出しを行うことができます。通常、開発者は自分のノート PC で動作する AEM 以外のアプリケーションでこのトークンを使用します。また、AEM as a Cloud Service は通常、非実稼働環境です。

開発者フローは次のステップで構成されます。

* 開発者コンソールからアクセストークンを生成する
* そのアクセストークンを指定して AEM アプリケーションを呼び出す

また、開発者は、ローカルマシン上で動作している AEM プロジェクトに対して API 呼び出しを行うこともできます。この場合、アクセストークンは不要です。

### アクセストークンの生成 {#generating-the-access-token}

1. 次に移動： **ローカルトークン** under **統合**
1. アクセストークンを生成するには、開発者コンソールで「**ローカル開発トークンを取得**」ボタンをクリックします。

### アクセストークンでのAEMアプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報の更新 {#refresh-credentials}

デフォルトでは、AEM as a Cloud Service 資格情報は 1 年後に期限切れになります。サービスの継続性を確保するために、開発者は資格情報を更新して、利用期間をさらに 1 年間延長することができます。

これを実現するには、次の操作を実行します。

* 以下を使用： **証明書を追加** 下のボタン **統合** - **テクニカルアカウント** 開発者コンソールで、次に示すように

   ![資格情報の更新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* ボタンを押すと、新しい証明書を含む一連の資格情報が生成されます。 古い資格情報を削除せずに、オフAEMサーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。 
* アクセストークンを生成する際に、古い資格情報ではなく新しい資格情報が使用されていることを確認します
* 必要に応じて、以前の証明書を失効（および削除）して、AEM as a Cloud Serviceでの認証に使用できなくします。

## 資格情報失効 {#credentials-revocation}

秘密鍵が侵害された場合は、新しい証明書と新しい秘密鍵で資格情報を作成する必要があります。 アプリケーションが新しい資格情報を使用してアクセストークンを生成した後、古い証明書を失効および削除できます。

これは、次の手順で行います。

1. まず、新しいキーを追加します。 これにより、新しい秘密鍵と新しい証明書を持つ資格情報が生成されます。 新しい秘密鍵は、UI で **現在** 今後、このテクニカルアカウントのすべての新しい資格情報に使用されます。 古い秘密鍵に関連付けられている資格情報は、取り消されるまで有効です。 これを行うには、**...**) をクリックし、を押します。 **新しい秘密鍵を追加**:

   ![新しい秘密鍵を追加](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 押す **追加** 次のプロンプトに対して実行します。

   ![新しい秘密鍵の追加を確認](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   新しいレンダリアルを含む新しい参照タブが開き、UI が更新されて秘密鍵が両方とも表示されます。新しい参照タブは **現在**:

   ![UI の秘密鍵](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. AEM以外のサーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。 詳しくは、 [サーバー間フローセクション](#the-server-to-server-flow) この方法の詳細については、を参照してください。
1. 古い証明書を失効します。 これを行うには、3 つのドット (**...**) をクリックし、 **失効**:

   ![証明書を失効](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   次に、次のプロンプトで「 **失効** ボタン：

   ![証明書の確認を取り消す](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後に、問題が発生した証明書を削除します。
