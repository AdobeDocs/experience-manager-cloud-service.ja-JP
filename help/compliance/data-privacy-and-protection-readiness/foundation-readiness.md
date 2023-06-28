---
title: データ保護とデータプライバシーに関する規制 - Adobe Experience Manager as a Data Foundation の対応
description: 様々なデータ保護およびデータプライバシー規制に対するAdobe Experience Manager as a Cloud Service Foundation のサポートについて説明します。 この記事には、EU 一般データ保護規則 (GDPR)、カリフォルニア州消費者プライバシー法、新しいAEMas a Cloud Serviceプロジェクトを実装する際の準拠方法が含まれています。
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# Adobe Experience Manager as a Data Foundation のデータ保護およびデータプライバシーに関する規制に対する対応 {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>このドキュメントの内容は法的な助言にはならず、その代用になるものでもありません。
>
>データ保護およびデータプライバシー規制に関するアドバイスについては、お客様の企業の法務部門にお問い合わせください。

>[!NOTE]
>
>プライバシーに関する問題に対するAdobeの対応と、プライバシーをご利用のお客様にとっての意味について詳しくは、 [Adobeプライバシーセンター](https://www.adobe.com/jp/privacy.html).

## AEM Foundation のデータプライバシーと保護のサポート {#aem-foundation-data-privacy-and-protection-support}

AEM Foundation レベルでは、保存される個人データはユーザープロファイルに保持されます。したがって、この記事の情報は主に、ユーザープロファイルへのアクセスと削除の方法について説明しているので、アクセス要求と削除要求それぞれに対処できます。

## ユーザープロファイルへのアクセス {#accessing-a-user-profile}

### 手動の手順 {#manual-steps}

1. ユーザー管理コンソールを開きます。開くには、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;を参照するか、または `https://<serveraddress>:<serverport>/security/users.html` を直接参照します。

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. 次に、ページの上部にある検索バーに目的のユーザーの名前を入力して検索します。

   ![アカウントの検索](assets/dpp-foundation-01.png)

1. 最後に、ユーザープロファイルをクリックして開き、「**[!UICONTROL 詳細]**」タブの下で情報を確認します。

   ![ユーザープロファイル](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

既に述べたように、Adobeは、自動化を容易にするユーザーデータにアクセスするための API を提供します。 利用可能な API には、以下のようにいくつかのタイプがあります。

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

上記のコマンドで返された JSON ペイロードの home プロパティに含まれているノードパスの使用

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## ユーザーの無効化と関連プロファイルの削除 {#disabling-a-user-and-deleting-the-associated-profiles}

### ユーザーの無効化 {#disable-user}

1. 前述のように、ユーザー管理コンソールを開き、該当するユーザーを検索します。
2. ユーザーの上にマウスポインターを置いて、選択アイコンをクリックします。 プロファイルがグレーに変わり、選択されたことを示します。

3. 上部のメニューで、 **無効にする** ユーザーを無効（オフ）にするには：

   ![アカウントの無効化](assets/dpp-foundation-03.png)

4. 最後に、アクションを確認します。

   ユーザーインターフェイスは、プロファイルカードに対するロックを追加してグレーアウトすることで、ユーザーアカウントが無効になったことを示します。

   ![無効なアカウント](assets/dpp-foundation-04.png)

### ユーザープロファイル情報の削除 {#delete-user-profile-information}

>[!NOTE]
>
>AEMas a Cloud Serviceの場合、CRXDE にアクセスできないので、UI からユーザープロファイルを削除するための手動の手順はありません。

### HTTP API {#http-api-1}

以下の手順では、 `curl` コマンドラインツールを使用して、 **[!UICONTROL cavery]** `userId` デフォルトの場所にあるユーザーのプロファイルを削除します。

**ユーザーホームの検索：**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**ユーザーの無効化:**

上記のコマンドから返された JSON ペイロードの home プロパティに含まれているノードパスを使用：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**ユーザープロファイルの削除**

アカウント検索コマンドから返された JSON ペイロードの home プロパティに含まれているノードパス、および既知のデフォルトのプロファイルノード位置を使用：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
