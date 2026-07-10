---
title: 外部 Git リポジトリを使用するために Edge Delivery サイトを設定
description: Edge Delivery サイトをプライベートまたはエンタープライズ Git リポジトリにリンクする方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: dea8a3df29876df1c97454a97602045eb50121ad
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 35%

---

# 外部 Git リポジトリを使用するために Edge Delivery サイトを設定

Cloud Managerに既にオンボーディングされているプライベート Git リポジトリからコードを取得するには、Edge Delivery サイトを設定します。

<!--
**Supported Git Vendors**

| Support level | Vendors | Notes |
| --- | --- | --- |
| General availability | &bull; GitHub Enterprise (self-hosted version)<br>&bull; Bitbucket (Cloud version)<br>&bull; GitLab (Cloud and self-hosted version) | Connect without enablement requests |
| Alpha program | Azure DevOps (Cloud version) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta program | Adobe-hosted repository (created in Cloud Manager) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
-->

**外部Git リポジトリを使用するには、Edge Delivery サイトを設定します：**

{{sign-in-to-cloud-manager}}

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)** コンソールで、Edge Delivery Servicesが設定されたプログラムを選択します。 外部Git リポジトリを使用するようにEdge Delivery サイトを設定するプログラムを選択します。
1. 左側のパネルの&#x200B;**プログラム**&#x200B;見出しの下にある「**![概要アイコン](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) 概要**」をクリックします。
1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。
1. **Edge Delivery サイト**&#x200B;のテーブルで、外部リポジトリを使用するように設定するサイトの行の末尾にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックし、「**Bring your own Git**」をクリックします。
1. **独自のGit** ダイアログボックスで、**リポジトリ名** ドロップダウンリストで、`READY` ステータスのGit リポジトリを選択し、**確認**&#x200B;をクリックします。

   Cloud Manager は、1 回限りの秘密鍵トークンを返します。 サイトを再設定すると、Cloud Manager により新しい秘密鍵トークンが生成されます。

1. トークンをコピーし、[BYO Git ガイド &#x200B;](https://www.aem.live/developer/byo-git)の説明に従って、**helix-admin**&#x200B;でサイト設定に追加します。
1. Cloud Managerで、外部リポジトリを使用するようにサイトが設定されている行の末尾にある![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**Sync code**&#x200B;をクリックします。
1. 同期する分岐を選択し、「**同期**」をクリックします。

任意の分岐の各コミットで、自動同期がトリガーされるようになりました。 完全な手動同期が必要な場合は、**コードを同期**&#x200B;を再度使用します。

## Git クローン要求の認証 {#authenticate-git-clone-requests}

IMS トークンまたはサイトの設定時にCloud Managerが生成するbyogit シークレットを使用して、Cloud Managerから[!DNL Bring Your Own Git] リポジトリを複製できます。 両方の資格情報がコピーエンドポイントに対して認証されるので、helix-adminが既に保存しているシークレットを[!DNL Edge Delivery Services] コード同期に使用できます。

コピーエンドポイントは、`Authorization` ヘッダーの資格情報を受け入れます。 Cloud Managerは、そのリポジトリに保存された値に対してbyogit シークレットを検証します。 有効なIMS トークンも有効なbyogit シークレットも含まないリクエストは、`401`応答を返します。

>[!NOTE]
>
>既存のIMS認証コピーワークフローは影響を受けません。 byogit秘密鍵は追加のオプションであり、置き換えではありません。

**リポジトリをbyogit秘密鍵で複製するには：**

1. サイトの設定時にCloud Managerが返すシークレットをコピーします。
1. コピーコマンドを実行し、`Authorization` ヘッダーにシークレットを渡します。

   `git -c http.extraHeader="Authorization: <byogit-secret>"` クローン `https://cm-repo.adobe.io/api/program/<program-id>/repository/<repository-id>.git`

   `<byogit-secret>`をCloud Managerのシークレットに置き換え、`<program-id>`と`<repository-id>`をプログラムの値に置き換えます。
