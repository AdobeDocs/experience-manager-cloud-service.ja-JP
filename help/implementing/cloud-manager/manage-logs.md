---
title: ログへのアクセスと管理
description: ログにアクセスして管理し、AEM as a Cloud Serviceでの開発プロセスを支援する方法について説明します。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 26%

---


# ログへのアクセスと管理 {#manage-logs}

ログにアクセスして管理し、AEM as a Cloud Serviceでの開発プロセスを支援する方法について説明します。

選択した環境で使用可能なログファイルのリストにアクセスするには、 **環境** カード **概要** ページまたは環境の詳細ページに表示されます。

## ログのダウンロード {#download-logs}

ログをダウンロードするには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **概要**&#x200B;ページの&#x200B;**環境**&#x200B;カードに移動します。

1. 選択 **ログをダウンロード** を選択します。

   ![ログメニュー項目をダウンロード](assets/download-logs1.png)

1. 内 **ログをダウンロード** ダイアログで、適切な **サービス** ドロップダウンメニューから

   ![ログをダウンロードダイアログ](assets/download-preview.png)

1. サービスを選択したら、取得するログの横にあるダウンロードアイコンをクリックします。

また、 **環境** ページ。

![環境画面からのログ](assets/download-logs.png)

## API を介したログ {#logs-through-api}

UI を使用したログのダウンロードに加えて、API とコマンドラインインターフェイスを通じてログを入手できます。

特定の環境のログファイルをダウンロードする場合のコマンドは次のようになります。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

コマンドラインインターフェイスを使用して、テールログを作成することもできます。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

環境 ID（この例では 1884）と使用可能なサービスまたはログ名のオプションを取得するには、次のコマンドを使用します。

```shell
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

### その他のリソース {#resources}

Cloud Manager API と Adobe I/O CLI について詳しくは、次の追加のリソースを参照してください。

* [Cloud Manager API ドキュメント](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
