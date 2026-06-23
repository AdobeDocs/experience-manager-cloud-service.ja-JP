---
title: Cloud Manager での Edge Delivery サイトの管理
description: Edge Delivery サイトに CDN 設定を追加する方法や、Edge Delivery サイトを削除する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: 069e94e230b856fba15c3f465c966a5bf6b0ac46
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 43%

---

# Cloud Manager での Edge Delivery サイトの管理 {#manage-edge-delivery-sites}

Cloud Manager で Edge Delivery サイトを管理するために、既存のサイトに CDN 設定を追加する方法や、 Edge Delivery サイトを削除する方法について説明します。

## 既存の Edge Delivery サイトへのドメインマッピングの追加 {#add-cdn-to-edge-delivery-site}

[ドメインマッピングの追加](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)を参照してください。

## Edge Delivery サイト（#rename-edge-delivery-site）の名前の変更

Adobe Cloud Managerでは、いくつかの理由でEdge Delivery サイトの名前を変更します。

* **明確さと組織**：サイトの目的や関連する環境（実稼動、ステージングなど）をより適切に説明します。
* **混乱の回避**：複数のサイトを使用している場合、名前を変更すると、それらのサイトを区別しやすくなり、構成や更新を誤ったサイトに適用するリスクが軽減されます。
* **標準化**：管理と監査を簡単にするために、組織のガイドラインに沿った一貫した命名規則に従います。

**Edge Delivery サイトの名前を変更するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、Edge Delivery サイトを追加するプログラム（Edge Delivery Services が設定されているもの）を選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。Edge Delivery サイト テーブルで、名前を変更するサイトの行の末尾にある省略記号をクリックします。
「**名前を変更**」をクリックします。
   * ページの左上隅にある「![&#x200B; メニューアイコンを表示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)」をクリックして、左側のメニューを表示します。「**サービス**」の見出しの下で、![Web ページアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**&#x200B;をクリックします。
Edge Delivery サイト テーブルで、名前を変更するサイトの行の末尾にある![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。「**名前を変更**」をクリックします。

1. **Edge Delivery サイトを編集**&#x200B;ダイアログボックスの「**サイト名**」テキストフィールドに、サイトの新しい名前を入力します。
1. 「**編集**」をクリックします。


## Edge Delivery サイトのパブリッシュ層をアクティブ化する（Beta） {#activate-publish-tier-for-eds}

>[!NOTE]
>
>ここで説明する公開機能はBetaにあります。 Betaに参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

この機能は、柔軟なパブリッシュ階層機能が有効になっているプログラムの&#x200B;**AEM オーサリング** オプションで作成されたEdge Delivery サイトにのみ適用されます。

Edge Delivery サイトでAEM オーサリングを使用している場合、Edge Deliveryはコンテンツ配信を処理するため、Adobeはデフォルトでパブリッシュ層をプロビジョニングしません。 ただし、サイトで必要な場合は、いつでもパブリッシュ層をアクティブ化できます。 たとえば、Edge Deliveryと並行して従来のAEM公開をサポートする必要がある場合。

Edge Delivery サイトを作成し、そのステータスがCloud Managerで&#x200B;**検証済み**&#x200B;と表示されたら、AEM ユニバーサルエディターを使用してコンテンツをオーサリングおよび公開できます。

**Cloud Managerからユニバーサルエディターにアクセスするには：**

1. 「Edge Delivery」タブの「Edge Delivery サイト」リストで、サイトを見つけます。

   ![AEM オーサーからEdge Deliveryへのコンテンツの公開。](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. サイトの行にある&#x200B;**コンテンツSource** リンクをクリックします。 このリンクをクリックすると、AEM ユニバーサルエディターページが開き、サイトのコンテンツを作成および編集できます。—>

**Edge Delivery サイトのパブリッシュ層をアクティブ化するには：**

1. **プログラムの概要** ページの&#x200B;**配信を公開** タブの&#x200B;**環境** カードで、情報アイコンをクリックします。

1. 情報ポップアップの「**公開URL**」で「**クリックしてアクティブ化**」を選択し、Cloud Manager ユーザーインターフェイスでパブリッシュ層のプロビジョニングを有効にします。

   ![&#x200B; クリックしてパブリッシュ層プロビジョニングをアクティブ化](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

1. パブリッシュ層をアクティブ化ダイアログボックスで、**アクティブ化**&#x200B;をクリックします。

   ![&#x200B; パブリッシュ層をアクティブ化ダイアログボックス &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

   アクティブ化すると、パブリッシュ層が自動的にプロビジョニングされます。 または、作成者がAEM ユーザーインターフェイスからコンテンツを直接公開しようとすると、パブリッシュ層を自動的にプロビジョニングできます。

   パブリッシュ層がアクティブ化され、正常にプロビジョニングされると、**クリックしてアクティブ化** リンクが無効/使用できなくなります。

* **AEM オーサー**&#x200B;から – AEM オーサリングインターフェイスで、**クイック公開**&#x200B;をクリックして、コンテンツをEdge Delivery サイトに直接公開します。 Edge Deliveryで配信を処理する場合、この操作に公開層は必要ありません。

公開後、サイトの`.page` URLでコンテンツをプレビューするか、`.live` URLでライブ表示します。—>

>[!NOTE]
>
>パブリッシュ層をアクティブ化すると、パブリッシュインフラストラクチャが環境に追加されます。 この機能は、プログラムのリソース消費に影響します。 パブリッシュ層がプログラムレベルで必要かどうかを設定するには、[柔軟なパブリッシュ層（Beta） &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。


## Edge Delivery サイトの削除 {#delete-edge-delivery-site}

Edge Delivery Services サイトを削除すると、関連付けられている CDN 設定もすべて削除されます。 このアクションにより、カスタムドメインとサイト間の接続が切断されます。 詳しくは、CDN 設定を参照してください。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Edge Delivery サイトを削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、Edge Delivery サイトを追加するプログラム（Edge Delivery Services が設定されているもの）を選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。Edge Delivery サイト テーブルで、削除するサイトの行の末尾にある![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。
![Edge Delivery サイトの削除アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **削除**&#x200B;をクリックしてから、もう一度&#x200B;**削除**&#x200B;をクリックして、サイトの削除を確定します。

     ![「Edge Delivery」タブから Edge Delivery サイトを追加](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * ページの左上隅にある「![&#x200B; メニューアイコンを表示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)」をクリックして、左側のメニューを表示します。「**サービス**」の見出しの下で、![Edge Delivery サイトのWeb ページ アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery サイト**&#x200B;をクリックします。
Edge Delivery サイト テーブルで、削除するサイトの行の末尾にある![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックします。![Edge Delivery サイトの削除アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **削除**&#x200B;をクリックし、次に&#x200B;**削除**&#x200B;をもう一度クリックして、サイトの削除を確定します。

     ![「Edge Delivery サイト」ボタンからの Edge Delivery サイトの追加](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Helix 4 と Helix 5 間の Edge Delivery サイトの管理

`/program/{programId}/site/{siteId}` API エンドポイントを使用して、Edge Delivery サイトを Helix 4 と Helix 5 間で移行します。

>[!IMPORTANT]
>
>Helix 4 web サイトの CDN 設定は、Helix 5 に自動的に移行できません。 この制限は、お客様の本番サイトがHelix 4で稼働し、Helix 5のバージョンがまだ開発中であるため存在します。

**前提条件**

* `sitename` が既に存在している必要があります。
* 適切な `branchName`、Helix `version` および `repo` の値を把握します。
* 移行では、`branchName`、Helix `version` および `repo` のみが変更されます。 所有者フィールドは変更できません。

**API 形式**

```http
PUT /api/program/{programId}/site/{siteId}
```

**リクエスト本文パラメーター**
リクエスト本文で指定されたオリジンを適用するためのEdge Delivery サイトのオーバーライドを作成します。

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### 例 1：Helix 5 への移行

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**オリジン URL結果**
次のオリジン URLを持つEdge Delivery サイトを返します。

`"origin": "branch--my-website–Teo48.aem.live"`


### 例 2：Helix 4 への移行

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**オリジン URL結果**
次のオリジン URLを持つEdge Delivery サイトを返します。

`"origin": "branch--my-website--Teo48.hlx.live"`

### 例 3：Helix 5 への repoless サイトの移行

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**オリジン URL結果**
次のオリジン URLを持つEdge Delivery サイトを返します。

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## サポートチケットのログ {#eds-support-ticket}

{{support-ticket}}
