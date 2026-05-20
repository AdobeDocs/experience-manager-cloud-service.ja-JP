---
title: ログへのアクセスと管理
description: AEM as a Cloud Service での開発プロセスを支援するために、ログにアクセスして管理する方法について説明します。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: b8faae6a4237bf7d564bf989b4e728342c7bd5fc
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 55%

---


# ログへのアクセスと管理 {#manage-logs}

AEM as a Cloud Service での開発プロセスを支援するために、ログにアクセスして管理する方法について説明します。

選択した環境で使用可能なログファイルのリストにアクセスするには、**概要** ページまたは&#x200B;**環境の詳細** ページの&#x200B;**環境** カードを使用します。

ログは 7 日間保持されます。

## ログのダウンロード {#download-logs}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;カードに移動します。

1. 省略記号メニューから「**ログをダウンロード**」を選択します。

   ![ログをダウンロードメニュー項目](assets/download-logs1.png)

1. **ログをダウンロード** ダイアログボックスで、ドロップダウンメニューから適切な&#x200B;**サービス**&#x200B;を選択します。

   ![ログをダウンロードダイアログ](assets/download-preview.png)

   環境で[追加の公開領域](/help/operations/additional-publish-regions.md)が有効になっている場合は、以下に示すように、各領域を選択し、そのログを個別にダウンロードできます。

   ![その他の公開地域についてはログをダウンロード](assets/download-publish-region-logs.png)

1. サービスを選択したら、取得するログの隣にあるダウンロードアイコンをクリックします。

**環境**&#x200B;ページからもログにアクセスできます。

![環境画面からのログ](assets/download-logs.png)

## API経由のログ {#logs-through-api}

UI でログをダウンロードする以外に、API やコマンドラインインターフェイスを介してログを入手することもできます。

特定の環境のログファイルをダウンロードするには、次のようなコマンドを使用します。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

また、コマンドラインインターフェイスを使用してログをテールアップすることもできます。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

環境ID （この例では1884）と使用可能なサービスまたはログ名オプションを取得するには、次のコマンドを使用します。

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

>[!TIP]
>
>AEM as a Cloud Serviceのデバッグについて詳しくは、[このビデオリソース &#x200B;](https://app.frame.io/reviews/28cdf463-b7fc-443b-a54a-93cb7da6567e/dbf158f1-568b-4efc-8fbc-3b241561cbab)をご覧ください。

Cloud Manager API と Adobe I/O CLI について詳しくは、次の追加のリソースを参照してください。

* [Cloud Manager API ドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [ADOBE I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)

AEM as a Cloud Service のログファイルについて詳しくは、次のその他のリソースを参照してください。

* [Cloud 5 AEM ログファイル](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/expert-resources/cloud-5/cloud5-aem-log-files#)
* [ログを使用した AEM as a Cloud Service のデバッグ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs#)
