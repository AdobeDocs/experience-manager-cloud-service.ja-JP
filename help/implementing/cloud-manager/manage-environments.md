---
title: 環境の管理 - Cloud Service
description: 環境の管理 - Cloud Service
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 529fbdcba9fc4c1432beef1b63ff89079a900224
workflow-type: tm+mt
source-wordcount: '1618'
ht-degree: 78%

---

# 環境の管理 {#manage-environments}

以下では、ユーザーが作成できる環境のタイプと、環境の作成方法について説明します。

## 環境タイプ {#environment-types}

必要な権限を持っているユーザーは、（特定のテナントで使用できる範囲内で）次のタイプの環境を作成できます。

* **実稼動環境とステージ環境**：実稼動環境とステージ環境はペアとして使用でき、テストおよび実稼動のために使用されます。

* **開発環境**：開発環境は、開発およびテストのために構築でき、実稼動以外のパイプラインにのみ関連付けられます。

   >[!NOTE]
   >サンドボックスプログラムで自動的に作成される開発環境は、Sites および Assets ソリューションを組み込むように設定されます。

   環境タイプとその属性を次の表にまとめます。

   | 名前 | オーサー層 | パブリッシュ層 | ユーザーによる作成が可能 | ユーザーによる削除が可能 | 環境への関連付けが可能なパイプライン |
   |--- |--- |--- |--- |---|---|
   | 実稼動 | はい | はい（Sites が組み込まれる場合） | はい | いいえ | 実稼動パイプライン |
   | ステージ | はい | はい（Sites が組み込まれる場合） | はい | いいえ | 実稼動パイプライン |
   | 開発 | はい | はい（Sites が組み込まれる場合） | はい | はい | 実稼動以外のパイプライン |

   >[!NOTE]
   >実稼動環境とステージ環境はペアとして使用でき、テストおよび実稼動のために使用されます。ユーザーは、ステージ環境か実稼動環境のどちらか一方のみを構築することはできません。

## 環境の追加 {#adding-environments}

1. 環境を追加するには、「**環境を追加**」をクリックします。このボタンは、**環境**画面で使用できます。
   ![](assets/environments-tab.png)

   プログラムに環境がない場合は、**環境**&#x200B;カードでも「**環境を追加**」オプションが使用可能です。

   ![](assets/no-environments.png)

   >[!NOTE]
   >権限がない場合や、契約内容によっては、「**環境を追加**」オプションは無効になります。

1. **環境を追加**&#x200B;ダイアログボックスが表示されます。ユーザーは、「**環境タイプ**」、「**環境名**」、「**環境の説明**」などの詳細を指定する必要があります（必要な情報は、特定のテナントで使用できる範囲内で環境を作成する際のユーザーの目的によって異なります）。

   ![](assets/add-environment2.png)

   >[!NOTE]
   >環境を作成すると、Adobe I/O に 1 つ以上の&#x200B;*統合*&#x200B;が作成されます。これらは、Adobe I/O コンソールにアクセスできる顧客ユーザーに表示され、削除することはできません。削除できないことについては、Adobe I/O コンソール内で説明されます。

   ![](assets/add-environment-image1.png)

1. 「**保存**」をクリックして、条件が入力された環境を追加します。*概要*&#x200B;画面に、パイプラインのセットアップに使用できるカードが表示されます。

   >[!NOTE]
   >実稼動以外のパイプラインをまだセットアップしていない場合は、*概要*&#x200B;画面に、実稼動以外のパイプラインの作成に使用できるカードが表示されます。

## 環境の詳細 {#viewing-environment}

概要ページの&#x200B;**環境**&#x200B;カードは、最大 3 環境を一覧表示します。

1. 「**すべてを表示**」ボタンを選択して&#x200B;**環境**&#x200B;の概要ページに移動し、環境の完全なリストをテーブルに表示します。

   ![](/help/implementing/cloud-manager/assets/environment-showall.png)

1. **環境**&#x200B;ページには、既存の環境のリストが表示されます。

   ![](assets/environment-view-2.png)

1. 環境の詳細を表示するリストの環境のいずれかを選択します。

   ![](assets/environ-preview1.png)


### Preview Serviceへのアクセス {#access-preview-service}

プレビューサービス機能は、Cloud Managerを介して各AEM as a Cloud Service環境に追加のプレビュー（公開）サービスを提供します。

Webサイトがパブリッシュ環境に到達して公開される前に、Webサイトの最終的なエクスペリエンスをプレビューします。 Preview Serviceを確認して使用する前に、次のポインターをいくつか示します。

1. **AEMバージョン**:環境がAEM以降のバージョンである `2021.05.5368.20210529T101701Z` 必要があります。これをおこなうには、更新パイプラインが環境で正常に実行されていることを確認します。

1. **デフォルトのIP許可リストロック**:作成時に、プレビューサービスにはデフォルトのIP許可リスト（ラベル付き）が適用されま `Preview Default [Env ID]`す。

   >[!NOTE]
   >最初の作成時に、アクセスを有効にするには、環境内のプレビューサービスからデフォルトのIP許可リストを積極的に適用解除する必要があります。

   必要な権限を持つユーザーは、プレビューサービスに&#x200B;*ロック解除*&#x200B;アクセスして目的のアクセスを提供するために、次のいずれかの操作を行う必要があります。

   * 適切なIP許可リストを作成し、Preview Serviceに適用します。 これに従うには、Preview Serviceから`Preview Default [Env ID] IP Allow List`を解除します。 詳しくは、[IP許可リストの適用解除](/help/implementing/cloud-manager/ip-allow-lists/unapply-ip-allow-list.md)を参照してください。

      *または*,

   * 「 IPの更新」許可リストワークフローを使用して、デフォルトのIPを削除し、必要に応じてIPを追加します。 詳しくは、[IP許可リストの表示と更新](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)を参照してください。

      >[!NOTE]
      >プレビューURLに適切なメンバーがアクセスできるように、プレビューサービスのURLをチームと共有する前に、上記の手順を実行する必要があります。

      プレビューサービスへのアクセスをロック解除すると、ロックアイコン（下図を参照）は表示されなくなります。

      ![](/help/implementing/cloud-manager/assets/preview-service1.png)

1. **プレビュー用にコンテンツを公開**:AEM内の「公開を管理」UIを使用して、コンテンツをプレビューサービスに公開できます。詳しくは、[コンテンツのプレビュー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/fundamentals/previewing-content.html?lang=en)を参照してください。

## 環境の更新 {#updating-dev-environment}

ステージ環境と実稼動環境の更新は、アドビで自動的に管理されます。

開発環境の更新は、プログラムのユーザーが管理します。ある環境で AEM の最新の公開リリースが動作していない場合、ホーム画面の環境カードのステータスには&#x200B;**更新可能**&#x200B;と表示されます。

![](assets/environ-update.png)


「**更新**」オプションは、**環境**カードから利用できます。
このオプションは、**環境**&#x200B;カードで「**詳細**」をクリックした場合にも使用できます。**環境**&#x200B;ページが開き、「開発」環境を選択したら、「**...**」をクリックして「**更新**」を選択します。次の図を参照してください。

![](assets/environ-update2.png)

これを選択すると、この環境に関連付けられているパイプラインをデプロイメントマネージャーで最新のリリースに更新してから実行できます。

パイプラインが既に更新されている場合は、パイプラインの実行を求めるプロンプトが表示されます。

## 環境の削除 {#deleting-environment}

必要な権限を持つユーザーは、開発環境を削除できます。

**環境**&#x200B;カードのドロップダウンメニューから「**削除**」オプションを使用できます。削除する開発環境の「**...**」をクリックします。

![](assets/environ-delete.png)

**環境**&#x200B;カードの「**詳細**」をクリックした場合も、削除オプションを使用できます。**環境**&#x200B;ページが開き、「開発」環境を選択したら、「**...**」をクリックして「**削除**」を選択します。次の図を参照してください。

![](assets/environ-delete2.png)


>[!NOTE]
>この機能は、実稼動用に設定された実稼動プログラムの実稼働／ステージング環境セットには使用できません。ただし、サンドボックスプログラムの実稼働／ステージング環境には使用できます。

## アクセスの管理 {#managing-access}

**環境**&#x200B;カードのドロップダウンメニューから「**アクセスを管理**」を選択します。オーサーインスタンスに直接移動して、環境のアクセスを管理できます。

詳しくは、「[オーサーインスタンスへのアクセスの管理](/help/onboarding/what-is-required/accessing-aem-instance.md)」を参照してください。

![](assets/environ-access.png)


## 開発者コンソールへのアクセス {#accessing-developer-console}

**環境**&#x200B;カードのドロップダウンメニューから「**開発者コンソール**」を選択します。ブラウザーに新しいタブが開き、**開発者コンソール**&#x200B;へのログインページが表示されます。

**開発者コンソール**&#x200B;にアクセスできるのは、開発者ロールのユーザーだけです。サンドボックスプログラムの場合は例外で、Cloud Manager のサンドボックスプログラムにアクセスできるユーザーは誰でも、**開発者コンソール**&#x200B;にアクセスできます。

詳しくは、[サンドボックス環境の休止と休止解除](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction)を参照してください。


![](assets/environ-devconsole.png)

このオプションは、**環境**&#x200B;カードで「**詳細**」をクリックした場合にも使用できます。**環境**&#x200B;ページが開きます。環境を選択したら、「**...**」をクリックし、「**開発者コンソール**」を選択します。

## ローカルにログイン {#login-locally}

**環境**&#x200B;カードのドロップダウンメニューで「**ローカルログイン**」を選択し、Adobe Experience Manager にローカルでログインします。

![](assets/environ-login-locally.png)

さらに、**環境**&#x200B;の概要ページからローカルにログインできます。

![](assets/environ-login-locally-2.png)


## カスタムドメイン名の管理 {#manage-cdn}

環境の概要ページから&#x200B;**環境**&#x200B;の詳細ページに移動します。

>[!NOTE]
>パブリッシュサービスとプレビューサービスの両方で、Cloud Managerのサイトプログラムでカスタムドメイン名がサポートされるようになりました。 各 Cloud Manager 環境は、1 つの環境につき最大 250 個のカスタムドメインをホストできます。

使用している環境のパブリッシュサービスに対して、次のアクションを下記のとおり実行できます。

1. [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [カスタムドメイン名の表示と更新](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [カスタムドメイン名の削除](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [カスタムドメイン名のステータスの確認](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)または [SSL 証明書のステータスの確認](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)

1. [IP 許可リストのステータスの確認](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)


## IP 許可リストの管理 {#manage-ip-allow-lists}

環境の概要ページから環境の詳細ページに移動します。ここで、使用している環境のパブリッシュサービスやオーサーサービスに対して次のアクションを実行できます。

>[!NOTE]
>IP許可リスト機能が、オーサー、パブリッシュ、プレビューサービス用のCloud Managerでサポートされるようになりました（Sitesプログラムで使用できます）。

### IP 許可リストの適用 {#apply-ip-allow-list}

IP 許可リストを適用すると、許可リストの定義に含まれているすべての IP 範囲が環境のオーサーサービスまたはパブリッシュサービスに関連付けられます。IP 許可リストを適用するには、ビジネスオーナーまたはデプロイメントマネージャーのロールを持つユーザーがログインする必要があります。

>[!NOTE]
>IP 許可リストを環境サービスに適用するには、その IP 許可リストが Cloud Manager に存在する必要があります。Cloud Manager での IP 許可リストについて詳しくは、[概要 - Could Manager での IP 許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)を参照してください。

IP 許可リストを適用するには、次の手順に従います。

1. **環境**&#x200B;の詳細ページから特定の環境に移動し、**IP 許可リスト**&#x200B;テーブルに移動します。
1. IP 許可リストテーブルの上部にある入力フィールドを使用して、IP 許可リストと、その適用先となるオーサーサービスまたはパブリッシュサービスを選択します。
1. 「**適用**」をクリックし、送信を確認します。

### IP 許可リストの適用解除 {#unapply-ip-allow-list}

「IP 許可リストの適用解除」は、許可リストの定義に含まれるすべての IP 範囲が、環境のオーサーサービスやパブリッシュサービスとの関連付けを解除されるプロセスです。IP 許可リストの適用を解除するには、ビジネス所有者またはデプロイメントマネージャーのロールを持つユーザーがログインしている必要があります。

IP 許可リストの適用を解除するには、次の手順に従います。

1. 環境画面から特定の&#x200B;**環境**&#x200B;の詳細ページに移動し、**IP 許可リスト**&#x200B;テーブルに移動します。
1. 適用を解除する IP 許可リスト規則が一覧表示されている行を識別します。
1. 行の右端から **...** メニューを選択します。
1. 「**適用解除**」オプションを選択し、送信を確認します。
