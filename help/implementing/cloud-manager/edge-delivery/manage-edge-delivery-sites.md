---
title: Cloud Manager での Edge Delivery サイトの管理
description: Edge Delivery サイトに CDN 設定を追加する方法や、Edge Delivery サイトを削除する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: 603602dc70f9d7cdf78b91b39e3b7ff5090a6bc0
workflow-type: ht
source-wordcount: '712'
ht-degree: 100%

---

# Cloud Manager での Edge Delivery サイトの管理 {#manage-edge-delivery-sites}

Cloud Manager で Edge Delivery サイトを管理するために、既存のサイトに CDN 設定を追加する方法や、Edge Delivery サイトを削除する方法について説明します。

## 既存の Edge Delivery サイトへのドメインマッピングの追加 {#add-cdn-to-edge-delivery-site}

[ドメインマッピングの追加](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)を参照してください。

## Edge Delivery サイト（#rename-edge-delivery-site）の名前の変更

Adobe Cloud Manager では、次のようないくつかの理由で Edge Delivery サイトの名前を変更する必要がある場合があります。

* **明確さと組織**：サイトの目的や関連する環境（実稼動、ステージングなど）をより適切に説明します。
* **混乱の回避**：複数のサイトを使用している場合は、名前を変更すると、サイトを簡単に区別できるようになり、間違ったサイトに設定や更新を適用する可能性が減ります。
* **標準化**：管理と監査を簡単にするために、組織のガイドラインに沿った一貫した命名規則に従います。

**Edge Delivery サイトの名前を変更するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、Edge Delivery サイトを追加するプログラム（Edge Delivery Services が設定されているもの）を選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要ページ**&#x200B;で、「**Edge Delivery**」タブをクリックします。Edge Delivery サイトテーブルで、名前を変更するサイトの行の末尾にある省略記号をクリックします。
「**名前を変更**」をクリックします。
   * ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左側のサイドメニューを表示します。**サービス**&#x200B;見出しの下にある ![Web ページアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery サイト**」をクリックします。
Edge Delivery サイトテーブルで、名前を変更するサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。「**名前を変更**」をクリックします。

1. **Edge Delivery サイトを編集**&#x200B;ダイアログボックスの「**サイト名**」テキストフィールドに、サイトの新しい名前を入力します。

1. 「**編集**」をクリックします。

## Edge Delivery サイトの削除 {#delete-edge-delivery-site}

Edge Delivery Services サイトを削除すると、関連付けられている CDN 設定もすべて削除されます。このアクションにより、カスタムドメインとサイト間の接続が切断されます。詳しくは、CDN 設定を参照してください。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Edge Delivery サイトを削除するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、Edge Delivery サイトを追加するプログラム（Edge Delivery Services が設定されているもの）を選択します。
1. 次のいずれかの操作を行います。

   * **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。Edge Delivery サイトテーブルで、削除するサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。
![Edge Delivery サイトを削除アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)「**削除**」をクリックし、もう一度「**削除**」をクリックして、サイトの削除を確認します。

     ![「Edge Delivery」タブから Edge Delivery サイトを追加](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左側のサイドメニューを表示します。**サービス**&#x200B;見出しの下にある ![Edge Delivery サイトの web ページアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery サイト**」をクリックします。
Edge Delivery サイトテーブルで、削除するサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックします。![Edge Delivery サイトを削除アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)「**削除**」をクリックし、もう一度「**削除**」をクリックして、サイトの削除を確認します。

     ![「Edge Delivery サイト」ボタンからの Edge Delivery サイトの追加](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Helix 4 と Helix 5 間の Edge Delivery サイトの管理

`/program/{programId}/site/{siteId}` API エンドポイントを使用して、Edge Delivery サイトを Helix 4 と Helix 5 間で移行します。

>[!IMPORTANT]
>
>Helix 4 web サイトの CDN 設定は、Helix 5 に自動的に移行できません。この制限が存在するのは、お客様の実稼動サイトが Helix 5 バージョンの開発中であっても、引き続き Helix 4 で稼動している場合があるからです。

**前提条件**

* `sitename` が既に存在している必要があります。
* 適切な `branchName`、Helix `version` および `repo` の値を把握します。
* 移行では、`branchName`、Helix `version` および `repo` のみが変更されます。所有者フィールドは変更できません。

**API 形式**

```http
PUT /api/program/{programId}/site/{siteId}
```

**リクエスト本文パラメーター**
リクエスト本文で指定された接触チャネルを適用するために、Edge Delivery サイトの上書きを作成します。

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

**接触チャネル URL の結果**
次の接触チャネル URL を持つ Edge Delivery サイトを返します。

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

**接触チャネル URL の結果**
次の接触チャネル URL を持つ Edge Delivery サイトを返します。

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

**接触チャネル URL の結果**
次の接触チャネル URL を持つ Edge Delivery サイトを返します。

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## サポートチケットのログ {#eds-support-ticket}

{{support-ticket}}
