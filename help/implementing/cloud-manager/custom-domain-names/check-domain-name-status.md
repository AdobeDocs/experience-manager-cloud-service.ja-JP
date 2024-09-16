---
title: ドメイン名ステータスの確認
description: Cloud Managerがカスタムドメイン名を正常に確認したことを確認する方法について説明します。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3ff7b76f7892269f6ca001ff2c079bc693c06d93
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 41%

---


# ドメイン名のステータスの確認 {#check-status}

Cloud Managerがカスタムドメイン名を正常に確認したことを確認する方法について説明します。

## 要件 {#requirements}

Cloud Managerでドメイン名のステータスを確認する前に、次の要件を満たします。

* まず、「カスタムドメイン名の追加 [ ドキュメントの説明に従って、カスタムドメインの TXT レコードを追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) します。

## カスタムドメイン名のステータスの確認 {#how-to}

Cloud Manager内でカスタムドメイン名のステータスを判断できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」をクリックします。

1. そのドメイン名の&#x200B;**ステータス**&#x200B;アイコンをクリックします。

ステータスの詳細が表示されます。ステータスが&#x200B;**ドメインが検証済みでデプロイ済み**&#x200B;と表示されたら、カスタムドメインを使用する準備が整います。様々なステータスとその意味について詳しくは、[次の節](#statuses)を参照してください。

>[!NOTE]
>
>[Cloud Managerへの新しいカスタムドメイン名の追加 **時に、** カスタムドメインの追加 **ウィザードのトリガー手順で「** 作成を選択すると、Cloud Managerが自動的に検証を追加します ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 それ以降の検証では、ステータスの横にある再検証アイコンをアクティブに選択する必要があります。

## 検証ステータス {#statuses}

Cloud Managerは、[TXT 値 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を使用してドメインの所有権を確認し、次のいずれかのステータスメッセージを表示します。

| ステータス | 説明 |
| --- | --- |
| ドメイン検証に失敗しました | TXT 値が見つからないか、エラーが検出されました。<br> ステータスメッセージに表示される手順に従って、問題を解決します。 準備が整ったら、ステータスの横にある「**再検証**」アイコンを選択する必要があります。 |
| ドメイン検証中 | 検証中です。<br> このステータスは、通常、ステータスの横にある **再検証** アイコンを選択した後に表示されます。 DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。 |
| 検証済み – デプロイメントに失敗しました | TXT 検証は成功しましたが、CDN のデプロイメントに失敗しました。<br> この場合は、Adobe担当者にお問い合わせください。 |
| ドメインの検証とデプロイ | このステータスは、カスタムドメイン名が使用できる状態であることを示します。<br> この時点で、カスタムドメイン名はテストの準備ができており、Cloud Manager ドメイン名を指すようになっています。 詳しくは、[ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。 |
| 削除中 | カスタムドメイン名を削除中です。 |
| 削除に失敗しました | カスタムドメイン名の削除に失敗しました。再試行する必要があります。<br> 詳しくは、[ カスタムドメイン名の管理 ](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) を参照してください。 |


## ドメイン名エラー {#domain-error}

次に、一般的なドメイン名の検証エラーとその一般的な解決方法を示します。

### ドメインがインストールされていないエラー {#domain-not-installed}

このエラーは、レコードが適切にアップデートされたことを確認した後でも、TXT レコードのドメイン検証中に発生する可能性があります。

#### エラー原因 {#cause}

Fastly は、ドメインをまず登録したアカウントにロックします。他のアカウントは、サブドメインを登録する権限をリクエストする必要があります。 さらに、Fastly では、apex ドメインと関連するサブドメインを 1 つの Fastly サービスおよびアカウントに割り当てることができます。AEM Cloud Service ドメインで使用されるのと同じ apex およびサブドメインをリンクする既存の Fastly アカウントがある場合、このエラーが表示されます。

#### エラーの解決 {#resolution}

エラーは次のように修正されます。

* Cloud Manager にドメインをインストールする前に、既存のアカウントから apex とサブドメインを削除します。

* apex ドメインとすべてのサブドメインを AEM as a Cloud Service Fastly アカウントにリンクするには、このオプションを使用します。詳しくは、[Fastly でのドメインの使用ドキュメント](https://docs.fastly.com/en/guides/working-with-domains)を参照してください。

* apex ドメインにAEM as a Cloud Service用の複数のサブドメインがあり、異なる Fastly アカウントにリンクする必要があるAEM以外のサイトがある場合は、Cloud Managerにドメインをインストールします。 このプロセスは、様々な Fastly アカウントをまたいだサブドメイン接続の管理に役立ちます。 ドメインのインストールに失敗した場合は、Fastly でカスタマーサポートチケットを作成し、Adobeがお客様に代わって Fastly でフォローアップを行えるようにします。

>[!TIP]
>
>Fastly でのドメインの委任に関する問題を解決するには、通常 1～2 営業日かかります。このため、運用開始日より早い時期にドメインをインストールすることを強くお勧めします。

>[!NOTE]
>
>ドメインが正常にインストールされなかった場合は、サイトの DNS を AEM as a Cloud Service の IP にルーティングしないでください。

## カスタムドメイン名の既存の CDN 設定 {#pre-existing-cdn}

カスタムドメイン名の CDN 設定が既にある場合は、「**カスタムドメイン名**」ページと「**環境**」ページに情報メッセージが表示されます。 Cloud Manager内で管理および表示できるように、UI を通じてこれらの設定を追加することをお勧めします。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは [ カスタムドメイン名の追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) を参照してください。

## 次の手順 {#next-steps}

Cloud Managerでドメインのステータスを確認したら、AEM as a Cloud Serviceを指す DNS、CNAME または APEX レコードを追加して、DNS 設定を指定します。 [ カスタムドメイン名を追加 ](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) のドキュメントに進んで、カスタムドメイン名の設定を続行します。
