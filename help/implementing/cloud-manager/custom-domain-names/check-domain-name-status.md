---
title: ドメイン名ステータスの確認
description: Cloud Manager でカスタムドメイン名が正常に検証されたかどうかを判断する方法について説明します。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0c9328dc5be8f0a5e0924d0fc2ec59c9fce4141b
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 73%

---


# ドメイン名ステータスの確認 {#check-status}

Cloud Manager でカスタムドメイン名が正常に検証されたかどうかを判断する方法について説明します。

## 要件 {#requirements}

Cloud Managerでドメイン名のステータスを確認する前に、これらの要件を満たす必要があります。

* [TXT レコードの追加 ](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) のドキュメントで説明されているように、最初にカスタムドメインの TXT レコードを追加する必要があります。

## カスタムドメイン名のステータスの確認方法 {#how-to}

Cloud Manager 内でカスタムドメイン名のステータスを決定できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **概要**&#x200B;ページから&#x200B;**環境**&#x200B;画面に移動します。

1. 左側のナビゲーションパネルで「**ドメイン設定**」をクリックします。

1. ドメイン名の「**ステータス**」アイコンをクリックします。

ステータスの詳細が表示されます。 ステータス **ドメインが検証済みでデプロイ済み** が表示されると、カスタムドメインを使用する準備が整います。 様々なステータスとその意味について詳しくは、[ 次の節 ](#statuses) を参照してください。

>[!NOTE]
>
>Cloud Managerに新しいカスタムドメイン名を追加する **場合** カスタムドメインを追加 **ウィザードのトリガー手順で「** 作成 [」を選択すると、Cloud Managerによって検証が自動的に追加されます。](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 以降の検証では、ステータスの横にある再検証アイコンをアクティブに選択する必要があります。

## 検証ステータスについて {#statuses}

Cloud Managerは、[TXT 値 ](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) を介してドメインの所有権を検証し、次のいずれかのステータスメッセージを表示します。

* **ドメイン検証失敗** - TXT 値が見つからないか、エラーが検出されました。

   * ステータスメッセージに表示される指示に従って、問題を解決します。
   * 準備が整ったら、ステータスの横にある「**再検証**」アイコンを選択する必要があります。

* **ドメイン検証中** - 検証が進行中です。

   * このステータスは、通常、ステータスの横にある「**再検証**」アイコンを選択した後に表示されます。
   * DNS の伝播遅延が原因で、DNS 検証の処理に数時間かかる場合があります。

* **検証済み、デプロイメントに失敗しました** - TXT 検証は成功しましたが、CDN のデプロイメントに失敗しました。

   * この場合は、アドビ担当者にお問い合わせください。

* **ドメインが検証済みでデプロイ済み** - このステータスは、カスタムドメイン名が使用できる状態であることを示します。

   * この時点で、カスタムドメイン名はテストの準備ができており、Cloud Manager のドメイン名を指すようになっています。
   * 詳細については、[DNS 設定の指定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)を参照してください。

* **削除中** - カスタムドメイン名を削除中です。

* **削除に失敗しました** - カスタムドメイン名の削除に失敗しました。再試行する必要があります。

   * 詳しくは、[カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)を参照してください。

## ドメイン名エラー {#domain-error}

次に、一般的なドメイン名の検証エラーとその一般的な解決策を示します。

### エラー：ドメインがインストールされていません {#domain-not-installed}

このエラーは、レコードが適切にアップデートされたことを確認した後でも、TXT レコードのドメイン検証中に発生する可能性があります。

#### エラーの原因 {#cause}

Fastly は、ドメインを最初に登録したアカウントにロックし、他のアカウントは権限を要求することなくサブドメインを登録することができません。さらに、Fastly では、apex ドメインと関連するサブドメインを 1 つの Fastly サービスおよびアカウントに割り当てることができます。AEM Cloud Service ドメインで使用されるのと同じ apex およびサブドメインをリンクする既存の Fastly アカウントがある場合、このエラーが表示されます。

#### エラーの解決 {#resolution}

エラーは次のように修正されます。

* Cloud Manager にドメインをインストールする前に、既存のアカウントから apex とサブドメインを削除します。

* apex ドメインとすべてのサブドメインを AEM as a Cloud Service Fastly アカウントにリンクするには、このオプションを使用します。詳しくは、[Fastly でのドメインの使用ドキュメント](https://docs.fastly.com/en/guides/working-with-domains)を参照してください。

* apex ドメインに、異なる Fastly アカウントにリンクさせる AEM as a Cloud Service および非 AEM as a Cloud Service サイト用の複数のサブドメインがある場合は、Cloud Manager にドメインをインストールしてみてください。 ドメインのインストールに失敗した場合は、Fastly でカスタマーサポートチケットを作成し、Adobe がお客様に代わって Fastly でフォローアップを行えるようにします。

>[!TIP]
>
>Fastly でのドメインの委任に関する問題を解決するには、通常 1～2 営業日かかります。このため、運用開始日より早い時期にドメインをインストールすることを強くお勧めします。

>[!NOTE]
>
>ドメインが正常にインストールされなかった場合は、サイトの DNS を AEM as a Cloud Service の IP にルーティングしないでください。

## カスタムドメイン名の既存の CDN 設定 {#pre-existing-cdn}

カスタムドメイン名の既存の CDN 設定がある場合は、UI を通じてこれらの設定を追加して Cloud Manager で表示および設定できるようにすることを促す情報メッセージが&#x200B;**カスタムドメイン名**&#x200B;ページと&#x200B;**環境**&#x200B;ページに表示されます。

UI を使用して既存の環境設定をすべて移行すると、このメッセージは表示されなくなります。メッセージが表示されなくなるまでに 1～2 営業日かかる場合があります。

詳しくは、[カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)を参照してください。

## 次の手順 {#next-steps}

Cloud Managerでドメインステータスを確認したら、AEM as a Cloud Serviceを指す DNS CNAME または APEX レコードを追加して、DNS 設定を指定する必要があります。 ドキュメント [DNS 設定の指定 ](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) に進んで、カスタムドメイン名の設定を続行します。
