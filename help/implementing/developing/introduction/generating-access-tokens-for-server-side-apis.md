---
title: サーバー側 API のアクセストークンの生成
description: セキュアな JWT トークンを生成してサードパーティサーバーと AEM as a Cloud Service の間の通信を容易にする方法について説明します。
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: dd869397feca593f93ee8ed5030828e01cc45c4d
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 100%

---

# サーバーサイド API のアクセストークンの生成 {#generating-access-tokens-for-server-side-apis}

一部のアーキテクチャでは、AEM インフラストラクチャの外部にあるサーバーにホストされているアプリケーションから AEM as a Cloud Service への呼び出しの実行がベースになっています。例えば、モバイルアプリケーションがサーバーを呼び出し、その後、サーバーが AEM as a Cloud Service に対して API リクエストを行います。

サーバー間フローと簡略化した開発フローを以下に示します。認証プロセスに必要なトークンの生成には、AEM as a Cloud Service [開発者コンソール](development-guidelines.md#crxde-lite-and-developer-console)を使用します。

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## サーバー間フロー {#the-server-to-server-flow}

IMS 組織管理者の役割を持ち、AEM オーサー上の「AEM ユーザー」または「AEM 管理者」製品プロファイルのメンバーでもあるユーザーは、AEM as a Cloud Service の資格情報のセットを生成できます。各資格情報は、証明書 (公開鍵)、秘密鍵、および `clientId` と `clientSecret` から成るテクニカルアカウントを含む JSON ペイロードです。その資格情報は後で、AEM as a Cloud Service 環境管理者の役割を持つユーザーによって取得され、AEM 以外のサーバーにインストールされることになるので、秘密鍵として慎重に取り扱う必要があります。この JSON 形式のファイルには、AEM as a Cloud Service API との統合に必要なすべてのデータが含まれています。このデータを使用して、署名済み JWT トークンを作成します。このトークンは、Adobe IMS（Identity Management Services）との間で IMS アクセストークンと交換されます。その後、このアクセストークンをベアラー認証トークンとして使用して、AEM as a Cloud Service にリクエストを行うことができます。資格情報はデフォルトで 1 年後に期限切れになりますが、必要に応じて更新できます。詳しくは、[こちら](#refresh-credentials)を参照してください。

サーバー間フローは次のステップで構成されます。

* 開発者コンソールから AEM as a Cloud Service 資格情報を取得する
* AEM に対して呼び出しを行う AEM 以外のサーバーに AEM as a Cloud Service 資格情報をインストールする
* JWT トークンを生成し、そのトークンをアドビの IMS API を使用してアクセストークンと交換する
* アクセストークンをベアラー認証トークンに使用して AEM API を呼び出す
* AEM 環境のテクニカルアカウントユーザーに適切な権限を設定する

### AEM as a Cloud Service 資格情報の取得 {#fetch-the-aem-as-a-cloud-service-credentials}

AEM as a Cloud Service の Developer Console にアクセスすると、特定の環境向けの「統合」タブが表示されます。AEM as a Cloud Service 環境管理者の役割を持つユーザーは、資格情報を作成、表示、管理できます。

「**新しいテクニカルアカウントを作成**」ボタンをクリックすると、選択したポッドにかかわらず、環境のオーサー層とパブリッシュ層用のクライアント ID、クライアントシークレット、秘密鍵、証明書、設定を含む、新しい資格情報のセットが作成されます。

![新しいテクニカルアカウントの作成](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

新しいブラウザータブが開き、資格情報が表示されます。このビューで、ステータスタイトルの横にあるダウンロードアイコンをクリックすると、資格情報をダウンロードできます。

![資格情報のダウンロード](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

資格情報が作成されると、その資格情報が「**統合**」セクションの「**テクニカルアカウント**」タブに表示されます。

![資格情報の表示](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

ユーザーは、後で表示アクションを使用して資格情報を表示できます。また、証明書を更新または取り消す必要がある場合に備えて、後述のように、ユーザーは新しい秘密鍵または証明書を作成することで、同じテクニカルアカウントの資格情報を変更できます。

AEM as a Cloud Service の環境管理者の役割を持つユーザーは、後で追加のテクニカルアカウントの新しい資格情報を作成できます。これは、複数の API を使用しており、それらのアクセス要件が異なる場合に役立ちます（例：読み取り専用 API と読み取り／書き込み可能な API）。

>[!NOTE]
>
>テクニカルアカウントは、最大 10 個まで作成できます（既に削除されているテクニカルアカウントを含む）。

>[!IMPORTANT]
>
>資格情報を生成して、AEM as a Cloud Service 環境への管理者権限を持つユーザーが後で取得できるようにするには、AEM オーサー上の「AEM ユーザー」または「AEM 管理者」製品プロファイルのメンバーでもある IMS 組織管理者（通常は、Cloud Manager を介して環境をプロビジョニングしたユーザーと同じ）が、まず Developer Console にアクセスして「**新しいテクニカルアカウントを作成**」ボタンをクリックする必要があります。IMS 組織管理者がこの操作をまだ行っていない場合は、IMS 組織管理者の役割が必要であることを通知するメッセージが表示されます。

### AEM 以外のサーバーへの AEM サービス資格情報のインストール {#install-the-aem-service-credentials-on-a-non-aem-server}

AEM に対して呼び出しをおこなうアプリケーションは、AEM as a Cloud Service 資格情報にアクセスしてそれをシークレットとして扱える必要があります。

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
>複数の資格情報がある場合は、後で呼び出される AEM への API 呼び出しに適した JSON ファイルを必ず参照してください。

### AEM API の呼び出し {#calling-the-aem-api}

ヘッダーにアクセストークンを含めて、AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。例えば、`curl` を使用して次のように呼び出します。

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### AEM のテクニカルアカウントユーザーに対する適切な権限の設定 {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

まず、新しい製品プロファイルを Adobe Admin Console で作成する必要があります。 これは、次の手順に従って実行できます。

1. Adobe Admin Console（[https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)）に移動します
1. 左側の&#x200B;**製品とサービス**&#x200B;列の下にある&#x200B;**管理**&#x200B;リンクをクリックします。
1. **AEM as a Cloud Service** を選択します
1. 「**新しいプロファイル**」ボタンを押します

   ![新しいプロファイル](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. プロファイルに名前を付け、「**保存**」を押します

   ![プロファイルの保存](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. 作成したばかりのプロファイルをプロファイルリストから選択します
1. 「**ユーザーを追加**」ボタンを押します

   ![ユーザーを追加](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. 作成したばかりのテクニカルアカウント（この場合は `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`）を追加し、「**保存**」を押します

   ![テクニカルアカウントの追加](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. 変更が反映されるまで 10 分間待ち、新しい資格情報から生成されたアクセストークンを使用して AEM への API 呼び出しを行います。cURL コマンドの場合、次の例のようになります。

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


API 呼び出しを行うと、製品プロファイルが AEM as a Cloud Service のオーサーインスタンスにユーザーグループとして表示され、適切なテクニカルアカウントがそのグループのメンバーとして表示されます。

これを確認するには、以下の手順を実行します。

1. オーサーインスタンスにログインします
1. **ツール**／**セキュリティ**&#x200B;に移動し、**グループ**&#x200B;カードをクリックします
1. グループのリストで作成したプロファイルの名前を見つけて、クリックします。

   ![グループプロファイル](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. 次のウィンドウで、「**メンバー**」タブに切り替えて、テクニカルアカウントが正しく一覧表示されているかどうかを確認します。

   ![「メンバー」タブ](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


または、オーサーインスタンスで次の手順を実行して、テクニカルアカウントがユーザーリストに表示されることを確認することもできます。

1. **ツール**／**セキュリティ**／**ユーザー**&#x200B;に移動します
1. お使いのテクニカルアカウントがユーザーリストにあることを確認し、クリックします
1. 「**グループ**」タブをクリックして、ユーザーが製品プロファイルに対応するグループに属していることを確認します。 また、このユーザーは、投稿者を含む一部の他のグループのメンバーでもあります。

   ![グループのメンバーシップ](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>2023 年半ば以前の、複数の資格情報を作成できる前は、顧客は Adobe Admin console で製品プロファイルを作成するように指示されなかったので、テクニカルアカウントは AEM as a Cloud Service インスタンスの「投稿者」以外のグループに関連付けられていませんでした。 一貫性を保つため、このテクニカルアカウントの場合は、前述のように Adobe Admin Console で新しい製品プロファイルを作成し、既存のテクニカルアカウントをそのグループに追加することをお勧めします。

<u>**適切なグループ権限の設定**</u>

最後に、必要な適切な権限でグループを設定して、API を適切に呼び出したり、ロックダウンを行ったりします。これを設定するには、次の操作を行います。

1. 適切なオーサーインスタンスにログインし、**設定**／**セキュリティ**／**権限**&#x200B;に移動します
1. 左側のパネルで製品プロファイルに対応するグループの名前（この場合は読み取り専用 API）を検索し、クリックします。

   ![グループの検索](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. 次のウィンドウで「編集」ボタンをクリックします。

   ![権限を編集](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. 権限を適切に変更し、「**保存**」をクリックします

   ![権限の編集の確認](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Adobe Identity Management System（IMS）と AEM ユーザーおよびグループについて詳しくは、[ドキュメント](/help/security/ims-support.md)を参照してください。

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

1. **統合**&#x200B;の下の&#x200B;**ローカルトークン**&#x200B;に移動します
1. アクセストークンを生成するには、開発者コンソールで「**ローカル開発トークンを取得**」ボタンをクリックします。

### アクセストークンを使用した AEM アプリケーションの呼び出し {#call-the-aem-application-with-an-access-token}

ヘッダーにアクセストークンを含めて、AEM 以外のアプリケーションから AEM as a Cloud Service 環境に対して適切なサーバー間 API 呼び出しを行います。そのため、「Authorization」ヘッダーには `"Bearer <access_token>"` の値を使用します。

## 資格情報の更新 {#refresh-credentials}

デフォルトでは、AEM as a Cloud Service 資格情報は 1 年後に期限切れになります。サービスの継続性を確保するために、開発者は資格情報を更新して、利用期間をさらに 1 年間延長することができます。

これを実現するには、次の操作を実行します。

* 以下に示すように、開発者コンソールの&#x200B;**統合**／**テクニカルアカウント**&#x200B;の下の「**証明書を追加**」ボタンを使用します

   ![資格情報の更新](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* ボタンを押すと、新しい証明書を含む一連の資格情報が生成されます。 古い資格情報を削除せずに、AEM 以外のサーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。 
* アクセストークンを生成する際に、古い資格情報ではなく新しい資格情報が使用されていることを確認します
* 必要に応じて、以前の証明書を失効（および削除）させて、AEM as a Cloud Service での認証に使用できないようにします。

## 資格情報の失効 {#credentials-revocation}

秘密鍵が侵害された場合は、新しい証明書と新しい秘密鍵を使用して、資格情報を作成する必要があります。 アプリケーションが新しい資格情報を使用してアクセストークンを生成した後、古い証明書を失効させて削除できます。

これは、次の手順で行います。

1. まず、新しいキーを追加します。 これにより、新しい秘密鍵と新しい証明書を使用して、資格情報が生成されます。 新しい秘密鍵は、UI で&#x200B;**現在**&#x200B;とマークされ、今後このテクニカルアカウントでのすべての新しい資格情報に使用されます。 古い秘密鍵に関連付けられている資格情報は、取り消されるまで有効です。これを行うには、現在のテクニカル アカウントの下にある 3 つのドット（**...**）を押して、「**新しい秘密鍵を追加**」を押します。

   ![新しい秘密鍵の追加](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. 次のプロンプトで「**追加**」を押します。

   ![新しい秘密鍵の追加の確認](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   新しい資格情報を含む新しい参照タブが開き、UI が更新されて秘密鍵が両方とも表示されます。新しい秘密鍵は&#x200B;**現在**&#x200B;としてマークされます。

   ![UI の秘密鍵](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. 非 AEM サーバーに新しい資格情報をインストールし、接続が期待どおりに動作することを確認します。これを行う方法について詳しくは、[サーバーからサーバーへの流れの節](#the-server-to-server-flow)を参照してください。
1. 古い証明書を失効させます。 これを行うには、証明書の右側にある 3 つのドット（**...**）を選択し、**失効**&#x200B;を押します。

   ![証明書の失効](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   次に、**失効**&#x200B;ボタンを押して、次のプロンプトで失効を確認します。

   ![証明書の確認の失効](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. 最後に、問題が発生した証明書を削除します。
