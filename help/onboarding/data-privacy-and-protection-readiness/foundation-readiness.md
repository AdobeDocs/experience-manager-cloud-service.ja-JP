---
title: データ保護とデータプライバシーに関する規制 — Adobe Experience Manager as a Data Foundation Readiness
description: 様々なデータ保護およびCloud Serviceプライバシー規制に対するAdobe Experience Manager as a Data Foundationのサポートについて説明します。EU一般データ保護規則(GDPR)、カリフォルニア州消費者プライバシー法、新しいAEM as a Cloud Serviceプロジェクトを実装する際の準拠方法を含みます。
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 32%

---

# Adobe Experience Manager as a Data Foundationデータ保護およびデータプライバシーに関する規制に対する対応{#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、貴社の法務部門にお問い合わせください。

>[!NOTE]
>
>Adobeのプライバシーに関する問題への対応と、Adobeのお客様への影響について詳しくは、[Adobeのプライバシーセンター](https://www.adobe.com/privacy.html)を参照してください。

## AEM Foundationのデータプライバシーと保護のサポート{#aem-foundation-data-privacy-and-protection-support}

AEM Foundationレベルでは、保存される個人データはユーザープロファイルに保持されます。 したがって、この記事の情報は主に、アクセス要求と削除要求にそれぞれ対処するための、ユーザープロファイルへのアクセス方法と削除方法に関するものです。

## ユーザープロファイルへのアクセス {#accessing-a-user-profile}

### 手動の手順 {#manual-steps}

1. **[!UICONTROL ツール/セキュリティ/ユーザー]**&#x200B;を参照するか、`https://<serveraddress>:<serverport>/security/users.html`を直接参照して、ユーザー管理コンソールを開きます。

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. 次に、ページの上部にある検索バーに目的のユーザーの名前を入力して検索します。

   ![アカウントの検索](assets/dpp-foundation-01.png)

1. 最後に、ユーザープロファイルをクリックして開き、「**[!UICONTROL 詳細]**」タブの下で情報を確認します。

   ![ユーザープロファイル](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

前述したように、自動化を促進するために、ユーザーデータにアクセスするための API が用意されています。利用可能な API には、以下のようにいくつかのタイプがあります。

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**ユーザーホームの検索：**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**ユーザーデータを取得する:**

上記のコマンドから返されたJSONペイロードのhomeプロパティからのノードパスを使用する。

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## ユーザーの無効化と関連プロファイルの削除 {#disabling-a-user-and-deleting-the-associated-profiles}

### ユーザーの無効化 {#disable-user}

1. 前述のように、ユーザー管理コンソールを開き、目的のユーザーを検索します。
2. ユーザーの上にマウスポインターを置き、選択アイコンをクリックします。プロファイルがグレーに変わり、選択されたことが示されます。

3. 上部のメニューの「**無効**」ボタンを押して、ユーザーを無効にします。

   ![アカウントの無効化](assets/dpp-foundation-03.png)

4. 最後に、アクションを確認します。

   次に、ユーザーインターフェイスは、ユーザーアカウントが無効になったことを示し、次のようにグレーアウトし、プロファイルカードにロックを追加します。

   ![無効なアカウント](assets/dpp-foundation-04.png)

### ユーザープロファイル情報の削除 {#delete-user-profile-information}

>[!NOTE]
>
>AEM as aCloud Serviceの場合、CRXDEにアクセスできないので、UIからユーザープロファイルを削除するための手動の手順はありません。

### HTTP API {#http-api-1}

以下の手順では `curl`コマンドラインツールを使用して、**[!UICONTROL cavery]** `userId` を持つユーザーを無効化し、デフォルト位置にあるそのユーザーのプロファイルを削除する方法を示しています。

**ユーザーホームの検索：**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**ユーザーの無効化:**

上記のコマンドから返されたJSONペイロードのhomeプロパティからのノードパスを使用する。

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**ユーザープロファイルの削除**

アカウント検出コマンドから返されるJSONペイロードのhomeプロパティからのノードパスと、既知の標準プロファイルノードの場所を使用します。

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
