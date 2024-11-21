---
title: Cloud Manager UI の操作
description: Cloud Manager UI の整理方法と、プログラムと環境を管理する操作方法について説明します。
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 40%

---


# Cloud Manager UI の操作 {#navigation}

Cloud Manager UI の整理方法と、プログラムと環境を管理する操作方法について説明します。

Cloud Manager UI は、主に次の 2 つのグラフィカルインターフェイスで構成されます。

* [マイプログラムコンソール](#my-programs-console)：すべてのプログラムを表示および管理できます。
* [プログラムの概要ウィンドウ](#program-overview)：個々のプログラムの詳細を確認して管理できます。

>[!TIP]
>
>また、Cloud Managerを使用してAEM as a Cloud Serviceを導入する方法の概要については、[ オンボーディングドキュメントジャーニー ](/help/journey-onboarding/overview.md) も参照してください。

## マイプログラムコンソール {#my-programs-console}

[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択すると、**マイプログラム**&#x200B;コンソールが表示されます。

![マイプログラムコンソール](assets/my-programs-console.png)

マイプログラムコンソールには、選択した組織でアクセス権を持つすべてのプログラムの概要が表示されます。複数のパーツで構成されます。

1. [ツールバー](#toolbars-my-programs-toolbars)：組織の選択、アラート、アカウント設定を行います。
1. プログラムの現在のビューを切り替えることができるタブ。
   * **ホーム**&#x200B;ビュー（デフォルト）：すべてのプログラムの概要を表示する&#x200B;**マイプログラム**&#x200B;ビューを選択します
   * **ライセンス** [ ライセンスダッシュボード ](/help/implementing/cloud-manager/license-dashboard.md) にアクセスする。
   * タブはデフォルトで閉じられ、[Cloud Managerヘッダーの ![ メニューアイコンを表示 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) を使用して表示され ](#cloud-manager-header) す。
1. [統計とコールトゥアクション](#statistics)：最近のアクティビティの概要を確認します。
1. [**「マイプログラム」**&#x200B;セクション](#my-programs-section)：すべてのプログラムの概要を表示します
1. 関連リソースに簡単にアクセスするための [ クイックリンク ](#quick-links-section)。

>[!TIP]
>
>プログラムについて詳しくは、[プログラムとプログラムタイプ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)を参照してください。

### ツールバー {#my-programs-toolbars}

2 つのツールバーが重なり合っています。

#### Cloud Manager ヘッダー {#cloud-manager-header}

1 つ目は Cloud Manager ヘッダーで、Cloud Manager を操作する際に保持されます。Cloud Manager プログラム全体に適用される設定と情報にアクセスできるアンカーです。

![Experience Cloud ヘッダー](assets/experience-cloud-header.png)

1. ![ メニューアイコンを表示 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) （サイドメニューを表示または非表示）をクリックすると、個々のプログラムの特定の部分に移動できる様々なタブにアクセスできます。 または、コンテキストに応じて [ ライセンスダッシュボード ](/help/implementing/cloud-manager/license-dashboard.md) と **[マイプログラム](#my-programs-console)** コンソールを切り替えることができます。
1. 「Cloud ManagerをAdobe」ボタンをクリックすると、Cloud Managerのどこにいても、Cloud Managerのマイプログラム コンソールに戻ります。
1. **フィードバック** をクリックして、Cloud Managerに関するAdobeにフィードバックを提供します。
1. 組織セレクターをクリックすると、現在ログインしている組織（この例では、Foundation Internal）が表示されます。 Adobe ID が複数の組織に関連付けられている場合、別の組織に切り替えるには、クリックします。
1. ![ アプリアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) （ソリューション切り替えボタン）をクリックすると、他のExperience Cloudソリューションにすばやくジャンプできます。
1. ![ ヘルプアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Help_18_N.svg) をクリックすると、学習リソースやサポートリソースにすばやくアクセスできます。
1. ![ ベルアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) （[ 通知 ](/help/implementing/cloud-manager/notifications.md)）をクリックすると、通知やお知らせを表示できます。
1. ユーザー設定へのユーザーアクセスを表すアイコンをクリックします。 ユーザー画像が設定されていない場合、アイコンがランダムに割り当てられます。

#### プログラムツールバー {#program-toolbar}

プログラムツールバーには、Cloud Manager プログラムとコンテキストに適したアクションを切り替えるリンクが表示されます。

![プログラムツールバー](assets/program-toolbar.png)

1. **マイプログラム** セレクターによってドロップダウンが開き、他のプログラムをすばやく選択したり、新しいプログラムの作成など、コンテキストに適したアクションを実行したりできます
1. **はじめに** リンクをクリックすると、Cloud Managerを使い始めるための [ オンボーディングドキュメントジャーニー ](/help/journey-onboarding/overview.md) にアクセスできます。
1. アクションボタンは、プログラムの追加など、コンテキストに適したアクションを提供します。

### 統計とコールトゥアクション {#statistics}

「統計とコールトゥアクション」セクションには、組織の集計データが表示されます。例えば、プログラムを正常に設定した場合、過去 90 日間のアクティビティの統計に次のような情報が表示されます。

* [デプロイ](/help/implementing/cloud-manager/deploy-code.md)数
* 特定された[コード品質の問題](/help/implementing/cloud-manager/code-quality-testing.md)の数
* ビルド数

組織の設定を開始したばかりの場合は、次の手順やドキュメントのリソースに関するヒントが表示される場合があります。

### マイ プログラム セクション {#my-programs-section}

**マイプログラム** コンソールのメインコンテンツは、「マイプログラム **セクション内のプログラムのリスト** す。

**マイプログラム** セクションには、各プログラムを表すカードが一覧表示されます。 カードをクリックすると、**プログラムの概要**&#x200B;ページにアクセスしてプログラムの詳細を確認できます。

>[!NOTE]
>
>権限によっては、特定のプログラムを選択できない場合があります。


必要なプログラムをより簡単に見つけるには、並べ替えオプションを使用します。

![並べ替えオプション](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* 並べ替え :
   * **作成日** （デフォルト）
   * **プログラム名**
   * **ステータス**
* ![ 並べ替え順の下のアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg) 昇順（デフォルト）/![ 並べ替え順の上のアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg) 降順
* ![ クラシックグリッド表示アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg) グリッド表示（デフォルト）
* ![ リスト表示アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) リスト表示

#### プログラムカード {#program-cards}

カード（またはテーブルの行）はすべてのプログラムを表し、プログラムの概要と、アクションを実行するためのクイックリンクを提供します。

![プログラムカード](assets/program-card.png)

* プログラムに関連付けられた画像（設定されている場合）。 上の画像は「WKND」です。
* プログラムに割り当てられた名前。 上の画像は、プログラム名として「SecurBank Sample」を示しています。
* サービスタイプ：
   * **Experience Managerクラウド** — AEM as a Cloud Service プログラム用
   * **Experience Manager** — [AMS （AdobeManaged Services）プログラム用 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/introduction)
* [ プログラムの種類 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md):
   * サンドボックス
   * 実稼動
* ステータス。 上の画像で、ステータスはチェックマークが付いた準備完了です。
* 設定済みのソリューション。 上の画像では、Sites とAssetsが設定済みのソリューションです。
* 作成日。

実稼動プログラムには、追加時に選択した追加の機能を示す次のようなバッジが付いている場合があります。

* ![HIPAA バッジ ](assets/hipaa.png) [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* ![WAF-DDOS バッジ ](assets/waf-ddos-protection.png) [WAF-DDOS 対策 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* [99.99% SLA（Service Level Agreement）](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

また、情報アイコンを使用すると、プログラムに関する追加情報にすばやくアクセスできます（リスト表示で役立ちます）。

![情報](assets/information-list-view.png)

![ その他 ](https://spectrum.adobe.com/static/icons/workflow_22/Smock_More_22_N.svg) アイコンを使用すると、プログラムに対して実行できる追加のアクションにアクセスできます。

![プログラムの省略記号ボタン](assets/program-ellipsis.png)

* プログラムの特定の ![ データアイコン ](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Data_22_N.svg)[ 環境 ](/help/implementing/cloud-manager/manage-environments.md) に移動します
* ![ プログラムの概要アイコン ](/help/implementing/cloud-manager/assets/program-overview.svg)[ プログラムの概要 ](#program-overview) を開きます。
* ![ 編集アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)[ プログラムを編集 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* ![ 削除アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)[ サンドボックスプログラムを削除する ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>プログラムおよびプログラムの追加と管理の詳細については、次を参照してください。
>
>* [ プログラムとプログラムの種類 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [ 実稼動プログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [ サンドボックスプログラムの作成 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### クイック リンク セクション {#quick-links-section}

「クイックリンク」セクションでは、関連する一般的に使用されるリソースにアクセスできます。

## プログラムの概要ページ {#program-overview}

**[マイプログラム](#my-programs-console)** コンソールでプログラムを選択すると、**プログラムの概要** ページが表示されます。

![プログラムの概要](assets/program-overview.png)

プログラムの概要では、Cloud Manager プログラムのすべての詳細にアクセスできます。**マイプログラム** コンソールと同様に、いくつかの部分で構成されています。

1. [ ツールバー ](#program-overview-toolbar) をクリックすると、[ マイ プログラム ] コンソールにすばやく戻り、プログラム内を移動できます
1. [タブ](#program-tabs)：プログラムの様々な側面を切り替えることができます。
1. [コールトゥアクション](#cta)：プログラムの最後のアクションに基づきます。
1. [環境の概要](#environments)：プログラムの環境について。
1. [パイプラインの概要](#pipelines)：プログラムのパイプラインについて。
1. プログラムの [ パフォーマンスの概要 ](#performance)
1. [役立つリソース](#useful-resources)：リンク先が含まれます。

### ツールバー {#program-overview-toolbar}

プログラムの概要のツールバーは、[ マイプログラムコンソール ](#my-programs-toolbars) のツールバーと似ています。 ここでは違いのみを説明します。

#### Cloud Manager ヘッダー {#cloud-manager-header-2}

ページの左上隅にはAdobeCloud Managerが表示されます。 ![ サイドメニューアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、タブのサイドメニューをソフトウェアの他の領域に表示したり非表示にしたりできます。

![Cloud Managerのサイドメニュー ](assets/cloud-manager-hamburger.png)

「AdobeCloud Manager」をクリックしてホームに戻ります。

#### プログラムツールバー {#program-toolbar-2}

プログラムツールバーを使用すると、他のプログラムにすばやく切り替えることができますが、プログラムの追加や編集など、コンテキストに適したアクションにもアクセスできます。

![プログラムツールバー](assets/cloud-manager-program-toolbar.png)

![ メニューアイコンを表示 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) を使用してタブを非表示にしている場合でも、ツールバーには常に現在表示しているタブが表示されます。

### プログラムタブ {#program-tabs}

各プログラムには、多数のオプションとデータが関連付けられています。これらのオプションとデータはタブにまとめられるので、プログラムのナビゲーションが簡単になります。 タブを使用すると、次のパーツにアクセスできます。

**プログラム**

* ![ 最新のグリッド表示アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg) 概要 – 現在のドキュメントで説明されているプログラムの概要
* ![ ベルアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg)[ アクティビティ ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - プログラムのパイプライン実行履歴
* ![ ワークフローアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)[ パイプライン ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - プログラム用に設定されているすべてのパイプライン
* ![ フォルダーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)[ リポジトリ ](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - プログラム用に設定されているすべてのリポジトリ
* ![ グラフ円アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg)[ レポート ](/help/implementing/cloud-manager/sla-reporting.md) - SLA データなどの指標

**サービス**

* ![ データアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)[ 環境 ](/help/implementing/cloud-manager/manage-environments.md) - プログラム用に設定されたすべての環境
* ![Web ページアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Edge Delivery Sites](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) - Edge Delivery Sites の管理
* ![ 設定アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg)[ ドメイン設定 ](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - プログラムのカスタムドメイン名を管理します
* ![ 鍵がかかったアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg)[SSL 証明書 ](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) - プログラムの SSL 証明書を管理します
* ![ ソーシャルネットワークアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg)[CDN 設定 ](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - CDN 設定の管理
* ![ タスクリストアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg)[IP 許可リスト](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) – 特定の IP アドレスの許可リストを定義します
* ![ ボックスアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg)[ コンテンツセット ](/help/implementing/developing/tools/content-copy.md) - コピー用に作成されたコンテンツのセット
* ![ 履歴アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg)[ コンテンツをコピーアクティビティ ](/help/implementing/developing/tools/content-copy.md) - コンテンツのコピーアクティビティ
* ![ チャネルアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg)[ ネットワークインフラストラクチャ ](/help/security/configuring-advanced-networking.md) - プログラムの高度なネットワークオプションを管理します

**リソース**

* ![ 本のアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Book_18_N.svg) ラーニングパス - Cloud Managerに関するその他のラーニングリソース

デフォルトでは、プログラムを開くと、「**概要**」タブが表示されます。現在のタブがハイライト表示されます。別のタブを選択すると、その詳細が表示されます。

[Cloud Managerヘッダーの左上隅にある ![ メニューアイコンを表示 ](#cloud-manager-header-2) をクリックして、タブのサイドメニューの表示と非表示を切り替えます。](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)

### コールトゥアクション {#cta}

「コールトゥアクション」セクションでは、プログラムのステータスに応じて役立つ情報を提供します。新しいプログラムの場合は、次の手順が示され、開始日 [ プログラムの作成時に設定 ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) が示されます。

![新規プログラムのアクションの呼び出し](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

ライブプログラムの場合、最後のデプロイメントのステータスと、詳細および新しいデプロイメントを開始するためのリンクが表示されます。

![コールトゥアクション](/help/implementing/cloud-manager/assets/info-banner.png)

### 環境カード {#environments}

**環境**&#x200B;カードには、環境の概要とクイックアクションへのリンクが表示されます。

**環境**&#x200B;カードには 3 つの環境のみ表示されます。「**すべて表示**」ボタンをクリックすると、プログラムのすべての環境が表示されます。

[ 環境の管理 ](/help/implementing/cloud-manager/manage-environments.md) も参照してください。

### パイプラインカード {#pipelines}

**パイプライン**&#x200B;カードには、パイプラインの概要とクイックアクションへのリンクが表示されます。

**パイプライン**&#x200B;カードには 3 つのパイプラインのみ表示されます。「**すべて表示**」をクリックすると、プログラムのすべてのパイプラインが表示されます。

パイプラインの管理方法について詳しくは、[ パイプラインの管理 ](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) も参照してください。

### パフォーマンスカード {#performance}

**パフォーマンス** カードには、**[CDN ダッシュボード](/help/implementing/cloud-manager/cdn-performance.md)** の概要が表示されます。

![パフォーマンスカード](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### 役立つリソース {#useful-resources}

「**役立つリソース**」セクションには、Cloud Manager のその他の学習リソースへのリンクが含まれます。
