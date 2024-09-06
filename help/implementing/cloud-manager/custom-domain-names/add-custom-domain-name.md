---
title: カスタムドメイン名を追加
description: Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 48%

---


# カスタムドメイン名を追加 {#adding-cdn}

Cloud Manager を使用してカスタムドメイン名を追加する方法を説明します。

## 要件 {#requirements}

Cloud Managerでカスタムドメイン名を追加する前に、次の要件を満たします。

* [SSL 証明書の追加 ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) ドキュメントで説明されているように、カスタムドメイン名を追加する前に、追加するドメインのドメイン SSL 証明書を追加する必要があります。
* Cloud Manager でカスタムドメイン名を追加するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割が必要です。
* Fastly CDN を使用している。

## カスタムドメイン名の追加場所 {#where}

Cloud Manager では、次の 2 つの場所からカスタムドメイン名を追加できます。

* [ドメイン設定ページから](#adding-cdn-settings)
* [環境ページから](#adding-cdn-environments)

カスタムドメイン名を追加する場合、ドメインは最も具体的で有効な証明書を使用して提供されます。 複数の証明書が同じドメインを持つ場合は、直近に更新されたものが選択されます。重複するドメインがないように証明書を管理することをお勧めします。

このドキュメントで説明する手順は、Fastly に基づいています。別の CDN を使用していた場合は、使用するように選択した CDN でドメインを設定します。

## ドメイン設定ページからカスタムドメイン名を追加します {#adding-cdn-settings}

**ドメイン設定**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」タブに移動し、選択します。

   ![ドメイン設定ウィンドウ](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 右上の「**ドメインを追加**」ボタンをクリックして「**ドメイン名を追加**」ダイアログを開きます。

   ![ ドメインを追加ダイアログボックス ](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 「**ドメイン名**」タブで、「**ドメイン名**」フィールドにカスタムドメイン名を入力します。

   >[!NOTE]
   >
   >ドメイン名を入力する際は、`http://`、`https://`、スペースを含めないでください。

1. そのドメイン名と関連付けられるサービスを持つ&#x200B;**環境**&#x200B;を選択します。

1. **公開**&#x200B;サービスまたは&#x200B;**プレビュー**&#x200B;サービスのいずれかを選択します。

1. ドロップダウンから、ドメイン名と関連付けられている「**ドメイン SSL 証明書**」を選択し、「**続行**」を選択します。

1. 「**検証**」タブが表示されます。

   ![ドメイン名の検証](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * 「**検証**」タブには、カスタムドメイン名を設定するための次の手順が記載されています。この手順では、必要な TXT レコードを作成します。
   * この操作は、ダイアログボックスで「**作成**」をクリックする前に行うことも、ダイアログボックスで「**作成**」をクリックした後に行うこともできます。
   * オプションと次の手順については、以下で説明します。

1. **作成** をクリックして、カスタムドメイン名をCloud Managerに保存します。

**カスタムドメインを追加** ウィザードで「**作成**」を選択すると、Cloud Managerによって TXT 検証がトリガーされます。 Cloud Managerでカスタムドメイン名を設定した場合は、TXT レコードを作成します。 ただし、この手順は必須ではありません。 以降の検証では、ステータスの横にある **再検証** アイコンをアクティブに選択する必要があります。

この名前は、Cloud Managerが TXT エントリの追加と検証を検証するまでアクティブになりません。 **検証済みおよびデプロイ済み** ステータスは、TXT 検証が成功したことを示します。

* TXT レコードについて詳しくは、[TXT レコードの追加 ](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) を参照してください。
* Cloud Managerによるカスタムドメイン名とその TXT エントリの検証方法について詳しくは、[ ドメイン名のステータスの確認 ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) を参照してください。

## 次の手順 {#next-steps}

Cloud Managerでカスタムドメイン名を作成したら、TXT エントリを追加して、ドメインの所有権を確認します。 カスタムドメイン名の設定を続行するには、[TXT レコードの追加](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)ドキュメントに進んでください。

## 環境ページからのカスタムドメイン名の追加 {#adding-cdn-environments}

**環境** ページからカスタムドメイン名を追加する手順は、[ ドメイン設定ページからカスタムドメイン名を追加する ](#adding-cdn-settings) 場合と同じですが、エントリポイントが異なります。 **環境**&#x200B;ページからカスタムドメイン名を追加するには、次の手順に従います。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. 対象となる環境の **環境の詳細** ページに移動します。

   ![環境の詳細ページでのドメイン名の入力](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. **ドメイン名**&#x200B;テーブルを使用してカスタムドメイン名を送信します。

   1. カスタムドメイン名を入力します。
   1. この名前に関連付けられている SSL 証明書をドロップダウンリストから選択します。
   1. 「**+追加**」をクリックします。

   ![ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **ドメイン名を追加** ダイアログボックスが開き、「**ドメイン名**」タブが表示されます。 [ ドメイン設定ページからのカスタムドメイン名の追加 ](#adding-cdn-settings) の場合と同様に続行します。
