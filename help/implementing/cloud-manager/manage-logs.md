---
title: ログの管理 — クラウドサービス
description: ログの管理 — クラウドサービス
translation-type: tm+mt
source-git-commit: 5913151c4e2bebb84bd68377d64f43e07caaf2dd

---


# ログへのアクセスと管理 {#manage-logs}

ユーザーは、環境カードを使用して、選択した環境で使用可能なログファイルのリストにアクセスできます。  ユーザーは、選択した環境で使用可能なログファイルのリストにアクセスできます。

これらのファイルは、概要ページからUIからダウンロードで **きます** 。

![](assets/manage-logs1.png)

または、環境ペ **ージ** :

![](assets/manage-logs2.png)

>[!N注]
>開いた場所に関係なく、同じダイアログが表示され、個々のログファイルをダウンロードできます。

![](assets/manage-logs3.png)


## APIを使用したログ {#logs-thorugh-api}

UIからログをダウンロードする以外に、APIとコマンドラインインターフェイスからログを使用できます。

例えば、特定の環境用のログファイルをダウンロードする場合、このコマンドは

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

次のコマンドを使用すると、ログのテーリングが可能です。

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

環境ID（この場合1884）と、使用可能なサービスまたはログ名のオプションを取得するには、次の手順を実行します。

```java
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

>[!N注]
>**ログダウンロード**&#x200B;は、UI と API の両方から利用できますが、**ログテーリング**&#x200B;は API/CLI のみです。

### その他のリソース {#resources}

Cloud Manager APIとAdobe I/O CLIについて詳しくは、次の追加のリソースを参照してください。

* [Cloud Manager APIドキュメント](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)