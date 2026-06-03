---
title: Adobe Admin ConsoleでのAdobeで管理されるAPI統合
description: Adobe Admin Console for AEM as a Cloud ServiceのAdobeで管理されるサービス統合の概要、その機能、および無効または復元する方法について説明します。
feature: Security
role: Admin
source-git-commit: ab959e98fdca60ea936b14cf6941ab531c32c9ac
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Adobe Admin ConsoleでのAdobeで管理されるAPI統合 {#adobe-managed-api-integrations-in-adobe-admin-console}

Adobeは、AEM as a Cloud Serviceおよび関連するAdobe Experience Cloud機能の一部として、IMS組織に少数の&#x200B;**サービス統合**&#x200B;をプロビジョニングします。 これらの統合機能は、[Adobe Admin Console](https://adminconsole.adobe.com/)に表示され、自分で作成した統合機能と一緒に表示されます。 Adobe サービスが所有し、お客様の代わりに操作します。

IMS組織のシステム管理者または製品管理者は、各統合の機能、それに応じたAdobe機能、および有効のままかどうかを確認できます。 Adobeが管理するサービス統合はいつでも無効にし、必要に応じて後で復元できます。

## 概要 {#overview}

この記事の内容：

* AEM環境にアクセスできる、Adobeで管理されている統合を特定します。
* 各統合の目的と、それがサポートするAdobe機能について説明します。
* 組織が必要とする場合に、Admin Consoleから統合機能を無効にするか復元します。

Adobeでは、以下に示すサービス統合ごとに次の原則を適用します。

* **透過的に名前を付ける** – 各統合では、その目的を説明する人間が読み取れる名前が使用されます。
* **Documented** – 各統合について、サポートする機能を使用してここに説明します。
* **最小権限** – 各統合は、広範な管理者権限ではなく、その機能に必要な製品プロファイル、役割、または権限のみを受け取ります。
* **お客様が制御できる** – 各統合はAdmin Consoleに表示され、管理者は無効にしたり復元したりできます。

## 統合機能の場所 {#where-to-find-these-integrations}

1. IMS組織のSystem Administrator アカウントまたはProduct Administrator アカウントを使用して[Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。
1. すべてのAPI資格情報を表示するには、**Users** > **API Credentials**&#x200B;に移動します。 特定の権限を持つ統合機能を調べるには、**製品** > *カタログ内の名前が付けられたAdobe製品* > *関連する製品プロファイル*&#x200B;に移動します。
1. 名前が`Adobe`で始まるか、下のカタログの名前と一致するサービス統合を探します。

>[!NOTE]
>
>各カタログエントリには、Adobe製品と、そのサービス統合の製品プロファイル、役割、または権限が一覧表示されます。 このパスは、統合を検査、無効化、または復元する際に使用します。
>
>Admin Consoleに表示される名前は、認証識別子です。 以下に記載されていないサービス統合が表示された場合は、無効にする前に[Adobe カスタマーサポート &#x200B;](https://helpx.adobe.com/jp/support.html)にお問い合わせください。

## Adobe Managed Integrations カタログ {#catalog-of-adobe-managed-integrations}

次の表に、AEM as a Cloud Serviceのお客様に対してAdobeが提供するサービス統合を示します。

| Admin Consoleに表示される名前 | 動作 | 使用者 | 付与された権限 | デフォルトで有効 |
|---|---|---|---|---|
| **AEM Managed CDN Integration** | LLM Optimizer サービスがAEM as a Cloud Service Managed CDN **エージェント型トラフィックルーティングルール**&#x200B;をユーザーに代わって更新できるようにし、AIおよびエージェントweb クローラー（ChatGPT、Perplexity、Claudeなど）をチームが手動でCDNを変更することなくLLM Optimizerに最適化されたオリジンにルーティングできるようにします。 | **LLM Optimizer** ～ [Edgeでの最適化](https://experienceleague.adobe.com/ja/docs/llm-optimizer/using/resources/optimize-at-edge/overview)機能 | Cloud Manager **デプロイメントマネージャー**&#x200B;の役割 | はい |

次のスクリーンショットは、上記の表に記載されている&#x200B;**AEM Managed CDN Integration**&#x200B;の例です。

![Adobe Admin ConsoleのCloud Manager Deployment Manager製品プロファイルでのAEM Managed CDN統合](assets/aem-managed-cdn-integration-admin-console.png)

>[!NOTE]
>
>Adobeは現在、このモデルで1つのサービス統合をプロビジョニングしています。 他のサービスで同じアプローチを使用する場合、Adobeはこのテーブルを更新します。 Admin Consoleに、ここに記載されていない別のAdobe プロビジョニング済みサービス統合が表示されている場合は、Admin Consoleを信頼できる唯一の情報源として使用し、詳細については[Adobe カスタマーサポート &#x200B;](https://helpx.adobe.com/jp/support.html)にお問い合わせください。

## 統合を無効にすることの影響 {#impact-of-disabling-an-integration}

Adobe マネージドサービス統合はいつでも無効にできます。 その場合、その統合に依存するAdobe機能は、復元するまで機能しなくなります。 統合を無効にする前に、次の表を確認してください。

| 統合 | 無効にすると動作しなくなります | この後も機能すること |
|---|---|---|
| **AEM Managed CDN Integration** | <ul><li><strong>LLM Optimizer ユーザーは、お使いのドメインのAEM as a Cloud Service Managed CDN エージェンティック トラフィック ルーティング ルール </strong>を更新できなくなります。 エージェント型ルーティングを有効、変更、または取り消すためのLLMO管理者によるその後の試みは、CDN レイヤーでの認証に失敗します。</li><li>AI/エージェントweb クローラーのルーティング（ChatGPT、Perplexity、Claudeなど） LLM Optimizerに最適化されたオリジンは、統合が復元されるまで（再）設定できません。</li><li>既に適用されているエージェント型ルーティングルールはエッジで有効なままですが、統合を再度有効にしない限り（またはAdobe カスタマーサポートと手動で調整しない限り）変更または削除できません。</li></ul> | <ul><li>AEM as a Cloud Serviceのオーサー、パブリッシュ、プレビュー環境では、引き続きトラフィックが正常に処理されます。</li><li>既にデプロイされたサイトの標準（エージェント以外） CDN配信は変更されません。</li><li>Cloud Manager パイプラインとデプロイメントは、デプロイメントマネージャーの権限を持つヒューマンオペレーターでも引き続き機能します。</li><li>エッジルーティングに依存しないLLM Optimizerの機能は、引き続き機能します。</li></ul> |

## 統合を無効にする方法 {#how-to-disable-an-integration}

**誰がこのタスクを実行できます：** IMS組織&#x200B;**システム管理者**、またはプロファイル、ロール、または権限がService Integrationへのアクセス権を付与するAdobe製品の&#x200B;**製品管理者** （カタログ行の&#x200B;*権限*&#x200B;を参照）。

手順は、この記事のすべてのサービス統合で同じです。 Admin Consoleのナビゲーションパスのみが、その統合の製品プロファイルに基づいて変化します。

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にログインします。
1. サービス統合の&#x200B;**Adobe製品**&#x200B;と&#x200B;**製品プロファイル、ロール、または権限**&#x200B;を特定します。 両方ともカタログ行にリストされます。
1. **製品** > *Adobe製品* > *製品プロファイル*&#x200B;に移動します。
1. そのプロファイルの「**API資格情報**」または「**ユーザー**」タブを開きます。
1. カタログ行の正確な名前を使用して、サービス統合を探します。
1. 製品プロファイルからサービス統合を削除します。 組織の統合は無効になっています。 次回Adobe サービスが自分に代わって行動する場合、認証は拒否されます。

**例 – AEM Managed CDN Integration:** **Products** > **Adobe Experience Manager as a Cloud Service** > **Cloud Manager** > **Deployment Manager**&#x200B;に移動し、**AEM Managed CDN Integration**&#x200B;を見つけ、製品プロファイルから削除します。

## 統合を復元する方法 {#how-to-restore-an-integration}

以前に統合を無効にし、もう一度有効にする場合：

1. [Adobe Admin Console](https://adminconsole.adobe.com/)にシステム管理者または製品管理者としてログインします。
1. 上のカタログのサービス統合用に特定された&#x200B;**同じ製品および製品プロファイル**&#x200B;に移動します。これは、サービス統合が無効になったときに削除されたプロファイルです。
1. **ユーザーを追加**&#x200B;または&#x200B;**API**&#x200B;を追加を選択し、カタログに記載されている正確な名前でサービス統合を検索します。
1. サービス統合を製品プロファイルに戻します。 統合は、次にスケジュールまたはユーザーが開始した実行時に再開されます。

**例 – AEM Managed CDN Integration:** **Cloud Manager** > **Deployment Manager**&#x200B;に移動し、**Add user**&#x200B;または&#x200B;**Add API**&#x200B;を使用して&#x200B;**AEM Managed CDN Integration**&#x200B;を再度追加します。

>[!NOTE]
>
>アドユーザーダイアログにサービス統合が見つからない場合（例えば、Adobeがプロファイルからではなく組織から削除したためなど）、[Adobe カスタマーサポート &#x200B;](https://helpx.adobe.com/jp/support.html)に連絡してプロビジョニングをリクエストしてください。 Adobeは、管理者が削除したサービス統合を自動的に再追加しません。

