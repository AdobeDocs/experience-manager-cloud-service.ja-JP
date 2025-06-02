---
title: ドメイン名ステータスの確認
description: Cloud Manager がカスタムドメイン名を正常に確認したことを確かめる方法について説明します。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68da11037cb3572a6f869fe8bd6a898e0aad87ec
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 88%

---


# ドメイン名ステータスの確認 {#check-status}

Cloud Manager がカスタムドメイン名を正常に確認したことを確かめる方法について説明します。

## カスタムドメイン名のステータスの確認 {#how-to}

Cloud Manager でドメイン名のステータスを確認する前に、[顧客が管理する SSL 証明書の追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert)の説明に従って、カスタムドメイン用の顧客が管理する（OV/EV）SSL 証明書が既に追加されていることを確認してください。

**カスタムドメイン名のステータスを確認するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のサイドメニューで「**ドメイン設定**」をクリックします。

1. そのドメイン名の&#x200B;**ステータス**&#x200B;アイコンをクリックします。

ステータスの詳細が表示されます。ステータスが&#x200B;**ドメインが検証済みでデプロイ済み**&#x200B;と表示されたら、カスタムドメインを使用する準備が整います。様々なステータスとその意味について詳しくは、[次の節](#statuses)を参照してください。

>[!NOTE]
>
>ドメインで&#x200B;*アドビが管理する（DV）SSL 証明書*&#x200B;を使用している場合、[カスタムドメイン名を追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)する際にドメインを検証ダイアログボックスの「**検証**」をクリックすると、Cloud Manager は自動的に検証をトリガーします。
>
>**顧客が管理する（OV/EV）SSL 証明書**&#x200B;を使用する予定がある場合、[OV/EV SSL 証明書を追加](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)した&#x200B;*後*&#x200B;にドメインが検証されます。


## 検証ステータス {#statuses}

Cloud Manager は、顧客が管理する（OV/EV）SSL 証明書を使用してドメインの所有権を検証します。完了すると、次のいずれかのステータスメッセージが表示されます。

| ステータス | 説明 |
| --- | --- |
| ドメイン検証失敗 | 顧客が管理する EV／OV 証明書が見つからないか、エラーが検出されました。<br>ステータスメッセージに表示される指示に従って、問題を解決します。準備が整ったら、ステータスの横にある「**再検証**」アイコンを選択する必要があります。 |
| ドメイン検証中 | 検証が進行中です。<br>このステータスは、通常、ステータスの横にある&#x200B;**再検証**&#x200B;アイコンを選択した後に表示されます。DNS の生成遅延が原因で、DNS 検証の処理に数時間かかる場合があります。 |
| 検証済み - デプロイメント失敗 | EV／OV 証明書検証は成功しましたが、CDN のデプロイメントに失敗しました。<br>この場合は、アドビ担当者にお問い合わせください。 |
| ドメイン検証済みおよびデプロイ済み | このステータスは、カスタムドメイン名が使用できる状態であることを示します。<br>この時点で、カスタムドメイン名はテストの準備ができており、Cloud Manager のドメイン名を指すようになっています。詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。 |
| 削除中 | カスタムドメイン名を削除中です。 |
| 削除に失敗しました | カスタムドメイン名の削除に失敗しました。再試行する必要があります。<br>詳しくは、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)を参照してください。 |


## ドメイン名エラー {#domain-error}

次に、一般的なドメイン名の検証エラーとその一般的な解決策を示します。

### エラー : ドメインがインストールされていません {#domain-not-installed}

<!-- This error may occur during domain validation of the EV/OV certificate even after you have checked that the certificate has been updated appropriately. -->

Cloud Managerでドメインマッピングを追加しようとすると、次のエラーメッセージが表示される場合があります。

*ドメインは既に Fastly アカウントにインストールされています。 Cloud Serviceに追加する前に、まずここから削除してください。*

<!-- This message indicates that the domain is currently associated with a different Fastly account—typically outside of Adobe's control. To proceed, the domain must be disassociated from the other account before it can be added to the Adobe-managed Cloud Service. This issue usually occurs when the same domain is already mapped to a different origin in a non-Adobe Fastly configuration. -->

**エラーの原因**
Fastly は、ドメインをまず登録したアカウントにロックします。他のアカウントは、サブドメインを登録する権限をリクエストする必要があります。 さらに、Fastly では、apex ドメインと関連するサブドメインを 1 つの Fastly サービスおよびアカウントに割り当てることができます。AEM Cloud Service ドメインで使用されるのと同じ apex およびサブドメインをリンクする既存の Fastly アカウントがある場合、このエラーが表示されます。

**エラーの解決**
エラーは次のように修正されます。

* Cloud Manager にドメインをインストールする前に、既存のアカウントから apex とサブドメインを削除します。

* apex ドメインとすべてのサブドメインを AEM as a Cloud Service Fastly アカウントにリンクするには、このオプションを使用します。詳しくは、Fastly のドキュメントの [ ドメインの使用 ](https://www.fastly.com/documentation/guides/getting-started/domains/working-with-domains/working-with-domains/) を参照してください。

* 異なる Fastly アカウントにリンクする必要がある AEM as a Cloud Service および非 AEM サイト用の複数のサブドメインが apex ドメインにある場合は、Cloud Manager でドメインをインストールしてみてください。このプロセスは、異なる Fastly アカウントにまたがるサブドメイン接続の管理に役立ちます。ドメインのインストールに失敗した場合は、Fastly でカスタマーサポートチケットを作成し、お客様に代わってアドビが Fastly でフォローアップを行えるようにします。

>[!TIP]
>
>Fastly でのドメインの委任に関する問題を解決するには、通常 1～2 営業日かかります。そのため、運用開始日の前にドメインを適切にインストールしておくことをお勧めします。

>[!NOTE]
>
>ドメインが正常にインストールされなかった場合は、サイトの DNS を AEM as a Cloud Service の IP にルーティングしないでください。

## カスタムドメイン名の既存の CDN 設定 {#pre-existing-cdn}

カスタムドメイン名の CDN（コンテンツ配信ネットワーク）設定が既にある場合は、**カスタムドメイン名**&#x200B;ページと&#x200B;**環境**&#x200B;ページに情報メッセージが表示されます。これらの設定を UI を通じて追加し、Cloud Manager で表示および管理できるようにすることをお勧めします。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。

## 次の手順 {#next-steps}

Cloud Manager でドメインのステータスを確認したら、AEM as a Cloud Service を指す DNS レコード、CNAME レコードまたは APEX レコードを追加して、DNS 設定を指定します。カスタムドメイン名の設定を続行するには、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)ドキュメントに進んでください。
