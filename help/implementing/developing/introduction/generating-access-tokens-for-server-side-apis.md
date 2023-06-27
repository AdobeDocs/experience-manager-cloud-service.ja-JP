---
title: サーバー側 API 用のアクセストークンの生成
description: セキュアな JWT トークンを生成することで、サードパーティサーバーとAEMas a Cloud Serviceの間の通信を容易にする方法を説明します
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 39%

---

# サーバー側 API 用のアクセストークンの生成 {#generating-access-tokens-for-server-side-apis}

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持つユーザー、および AEM オーサー上のAEMユーザーまたはAEM管理者製品プロファイルのメンバーであるユーザーは、AEM as a Cloud Serviceから一連の資格情報を生成できます。 各秘密鍵証明書は、証明書（公開鍵）、秘密鍵、および `clientId` および `clientSecret`. これらの資格情報は、後でAEMas a Cloud Serviceの環境管理者の役割を持つユーザーが取得できます。AEM以外のサーバーにインストールし、秘密鍵として慎重に扱う必要があります。 この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータを使用して、署名済み JWT トークンを作成します。このトークンは、Adobe IMS（Identity Management Services）との間で IMS アクセストークンと交換されます。その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報に含まれる証明書は、デフォルトで 1 年後に期限切れになりますが、説明に従って、必要に応じて更新できます [ここ](#refresh-credentials).

サーバー間フローは次のステップで構成されます。

* 開発者コンソールからAEM as a Cloud Serviceの資格情報を取得します
* AEMを呼び出すAEM以外のサーバーに、AEMas a Cloud Serviceの資格情報をインストールします
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service開発者コンソールへのアクセス権を持つユーザーは、特定の環境の開発者コンソールに「統合」タブが表示されます。 AEMas a Cloud Service環境管理者の役割を持つユーザーは、資格情報を作成、表示、管理できます。

クリック **新しいテクニカルアカウントを作成**&#x200B;には、ポッドの選択に関係なく、環境のオーサー層とパブリッシュ層用のクライアント id、クライアントの秘密鍵、秘密鍵、証明書、設定を含む一連の資格情報が作成されます。

![新しいテクニカルアカウントの作成](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

新しいブラウザータブが開き、資格情報が表示されます。 このビューで、ステータスタイトルの横にあるダウンロードアイコンをクリックすると、資格情報をダウンロードできます。

![資格情報のダウンロード](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

資格情報が作成されると、その資格情報が「**統合**」セクションの「**テクニカルアカウント**」タブに表示されます。

![資格情報の表示](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

ユーザーは、後で表示アクションを使用して資格情報を表示できます。さらに、この記事で後述するように、ユーザーは同じテクニカルアカウントの資格情報を編集できます。 証明書を更新または失効させる必要がある場合に備えて、新しい秘密鍵または証明書を作成することで、この編集を実行します。

AEMas a Cloud Serviceの環境管理者の役割を持つユーザーは、後で追加のテクニカルアカウントの資格情報を作成できます。 この機能は、API が異なるとアクセス要件が異なる場合に役立ちます。 例えば、読み取りと読み取り/書き込みが対象です。

>[!NOTE]
>
>お客様は、既に削除されているアカウントを含め、最大 10 個のテクニカルアカウントを作成できます。

>[!IMPORTANT]
>
>AEM オーサーインスタンスのAEMユーザーまたはAEM管理者製品プロファイルのメンバーでもある IMS 組織管理者（通常は Cloud Manager を通じて環境をプロビジョニングした同じユーザー）は、まず開発者コンソールにアクセスする必要があります。 次に、「 **新しいテクニカルアカウントを作成** 認証情報を生成し、AEMas a Cloud Service環境に対する管理者権限を持つユーザーが取得するためのもの。 IMS 組織管理者がテクニカルアカウントをまだ作成していない場合は、IMS 組織管理者の役割が必要であることを示すメッセージが表示されます。

### AEMサービス資格情報をAEM以外のサーバーにインストールする {#install-the-aem-service-credentials-on-a-non-aem-server}

AEMを呼び出すアプリケーションは、AEM as a Cloud Serviceの資格情報にアクセスし、秘密として扱うことができます。

### JWT トークンの生成とアクセストークンとの交換  {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

資格情報を使用して、Adobeの IMS サービスへの呼び出しで JWT トークンを作成し、24 時間有効なアクセストークンを取得します。

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

アクセストークンは、有効期限を定義します（通常は 24 時間）。 Git リポジトリーには、アクセストークンを管理して期限切れの前に更新するサンプルコードが含まれています。

>[!NOTE]
>複数の資格情報がある場合は、後で呼び出されるAEMへの API 呼び出しに適した JSON ファイルを必ず参照してください。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

まず、新しい製品プロファイルをAdobe Admin Consoleで作成する必要があります。

1. Adobe Admin Console( ) に移動します。 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. 左側の&#x200B;**製品とサービス**&#x200B;列の下にある&#x200B;**管理**&#x200B;リンクをクリックします。
1. **AEM as a Cloud Service** を選択します。
1. を押します。 **新しいプロファイル** 」ボタンをクリックします。

   ![新しいプロファイル](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. プロファイルに名前を付け、「**保存**」を押します。

   ![プロファイルの保存](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 作成したプロファイルを「プロファイル」リストから選択します。
1. 選択 **ユーザーを追加**.

   ![ユーザーを追加](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 作成したテクニカルアカウントを追加します ( この場合は `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) をクリックし、 **保存**.

   ![テクニカルアカウントの追加](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 変更が反映されるまで 10 分間待ち、新しい資格情報から生成されたアクセストークンを使用して AEM への API 呼び出しを行います。cURL コマンドの場合、次の例のようになります。

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


API 呼び出しをおこなうと、製品プロファイルがAEMas a Cloud Serviceのオーサーインスタンスのユーザーグループとして表示され、適切なテクニカルアカウントがそのグループのメンバーとして表示されます。

この情報を確認するには、次の手順を実行します。

1. オーサーインスタンスにログオンします。
1. に移動します。 **ツール** > **セキュリティ**」、「 **グループ** カード。
1. グループのリストで作成したプロファイルの名前を探し、クリックします。

   ![グループプロファイル](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 次のウィンドウで、「**メンバー**」タブに切り替えて、テクニカルアカウントが正しく一覧表示されているかどうかを確認します。

   ![「メンバー」タブ](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


または、オーサーインスタンスで次の手順を実行して、ユーザーのリストにテクニカルアカウントが表示されることを確認することもできます。

1. 「**ツール**」／「**セキュリティ**」／「**ユーザー**」に移動します。
1. お使いのテクニカルアカウントがユーザーリストであることを確認し、選択します。
1. 次をクリック： **グループ** 」タブを使用して、ユーザーが製品プロファイルに対応するグループに属していることを確認できます。 また、このユーザーは、寄稿者を含む一部の他のグループのメンバーでもあります。

   ![グループのメンバーシップ](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>2023 年半ば以前は、複数の資格情報を作成できるようになる前は、Adobe Admin Consoleでの製品プロファイルの作成に関するガイドはありませんでした。 したがって、テクニカルアカウントはAEM as a Cloud Serviceインスタンスの「寄稿者」以外のグループに関連付けられていませんでした。 一貫性を保つため、このテクニカルアカウントの場合は、前述のようにAdobe Admin Consoleで製品プロファイルを作成し、既存のテクニカルアカウントをそのグループに追加することをお勧めします。

<u>**適切なグループ権限の設定**</u>

最後に、API を適切に呼び出すか、またはロックダウンできるように、必要な適切な権限でグループを設定します。

1. 適切なオーサーインスタンスにログオンし、に移動します。 **設定** > **セキュリティ** > **権限**
1. 左側のパネル（この場合は読み取り専用 API）で製品プロファイルに対応するグループ名を検索して選択します。

   ![グループの検索](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 次のウィンドウで「編集」ボタンをクリックします。

   ![権限を編集](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 権限を適切に変更し、「**保存**」をクリックします

   ![権限の編集の確認](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Identity Management System(IMS)AdobeとAEMのユーザーおよびグループについて詳しく説明します。 詳しくは、 [ドキュメント](/help/security/ims-support.md).

## 開発者フロー {#developer-flow}

開発者は、開発AEM as a Cloud Service開発環境にリクエストを送信するAEM以外のアプリケーション（ノート PC で実行するか、ホストしている）の開発インスタンスを使用してテストを行いたいと考える場合があります。 ただし、開発者には必ずしも IMS 管理者ロールの権限がないので、Adobeは、通常のサーバー間フローで説明される JWT ベアラーを生成できるとは想定できません。 したがって、Adobeは、開発者がアクセス権を持つAEM上の環境へのリクエストで使用できるアクセストークンを直接生成するメカニズムを提供します。

AEM as a Cloud Service 開発者コンソールの使用に必要な権限については、[開発者ガイドラインドキュメント](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

>[!NOTE]
>
>ローカル開発アクセストークンは最大 24 時間有効で、その後は同じ方法で再生成する必要があります。

開発者は、このトークンを使用して AEM 以外のテストアプリケーションから AEM as a Cloud Service 環境に呼び出しを行うことができます。通常、開発者は、このトークンを、自分のノート PC 上の非AEMアプリケーションで使用します。 また、AEM as a Cloud Service は通常、非実稼働環境です。

開発者フローは次のステップで構成されます。

* 開発者コンソールからアクセストークンを生成する
* そのアクセストークンを指定して AEM アプリケーションを呼び出す

また、開発者は、ローカルマシン上で動作している AEM プロジェクトに対して API 呼び出しを行うこともできます。この場合、アクセストークンは不要です。

### アクセストークンの生成 {#generating-the-access-token}

1. **統合**&#x200B;の下の&#x200B;**ローカルトークン**&#x200B;に移動します
1. クリック **ローカル開発トークンを取得** を開発者コンソールに追加して、アクセストークンを生成できます。

### アクセストークンを使用した AEM アプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報の更新 {#refresh-credentials}

デフォルトでは、AEM as a Cloud Serviceの資格情報は 1 年後に期限切れになります。 サービスの継続性を確保するために、開発者は資格情報を更新して、利用期間をさらに 1 年間延長することができます。

この更新拡張機能を実行するには、以下の手順を実行します。

* 以下に示すように、開発者コンソールの&#x200B;**統合**／**テクニカルアカウント**&#x200B;の下の「**証明書を追加**」ボタンを使用します

  ![資格情報の更新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* ボタンを押すと、新しい証明書を含む一連の資格情報が生成されます。 古い資格情報を削除せずに、オフAEMサーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。
* アクセストークンを生成する際には、古い資格情報の代わりに新しい資格情報が使用されていることを確認してください。
* 必要に応じて、以前の証明書を失効（および削除）させて、AEM as a Cloud Service での認証に使用できないようにします。

## 資格情報の失効 {#credentials-revocation}

秘密鍵が侵害された場合は、新しい証明書と新しい秘密鍵で資格情報を作成する必要があります。 アプリケーションが新しい資格情報を使用してアクセストークンを生成した後、次の手順を実行して、古い証明書を失効および削除できます。

1. まず、新しいキーを追加します。 このキーは、新しい秘密鍵と新しい証明書を持つ資格情報を生成します。 新しい秘密鍵は、ユーザーインターフェイスで **現在** したがって、今後このテクニカルアカウントのすべての新しい資格情報に使用されます。 古い秘密鍵に関連付けられている資格情報は、取り消されるまで有効です。 この失効を実現するには、3 つのドット (**...**) を選択し、「 」を選択します。 **新しい秘密鍵を追加**:

   ![新しい秘密鍵の追加](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 選択 **追加** 次のプロンプトに対して実行します。

   ![新しい秘密鍵の追加の確認](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   新しい資格情報が設定された新しい「参照」タブが開き、ユーザーインターフェイスが更新されて、新しい秘密鍵が「 」とマークされた秘密鍵が両方とも表示されます **現在**:

   ![UI の秘密鍵](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 非 AEM サーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。詳しくは、 [サーバー間フローセクション](#the-server-to-server-flow) 」を参照してください。
1. 3 つのドット (**...**) を証明書の右側に追加し、「 」を選択します。 **失効**:

   ![証明書の失効](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   次に、**失効**&#x200B;ボタンを押して、次のプロンプトで失効を確認します。

   ![証明書の確認の失効](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後に、問題が発生した証明書を削除します。
