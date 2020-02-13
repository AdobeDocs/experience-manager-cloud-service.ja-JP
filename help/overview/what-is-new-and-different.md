---
title: 新機能 — クラウドサービスとしてのAdobe Experience Manager
description: '新機能 — クラウドサービスとしてのAdobe Experience Manager(AEM)。 '
translation-type: tm+mt
source-git-commit: b8eed5bd68d961a95d0ed15a4e88cee327a82594

---


# 新機能と機能の違い {#what-is-new-and-what-is-different}

AEMは、長い間、次の両方の機能を利用できます。

* オンプレミス

* 管理サービスとして

以前の方法とクラウドサービスとしてのAEMとの間には、本質的に異なる点があります。

* [アーキテクチャ](#architecture)
* [アップグレード](#upgrades)
* [Cloud Manager](#cloud-manager)
* [使用開始](#onboarding)
* [開発](#developing)
* [運用とパフォーマンス](#operations-and-performance)
* [ID 管理](#identity-management)
* [オーサリングユーザーインターフェイス](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>これらの概要は完全なものではありませんが、紹介を目的としています。

<!-- change link when 6.5 hub page migrated -->

>[!NOTE]
>
>オンプレミスバージョンとマネージドサービスバージョンの詳細については、 [AEM 6.5のドキュメントセットを参照してください](https://helpx.adobe.com/support/experience-manager/6-5.html)。

## アーキテクチャ {#architecture}

>[!NOTE]
>
>詳しくは、アーキテクチャを参照し [てください](/help/core-concepts/architecture.md)。

<!--
### Previous Versions {#previous-versions-architecture}

Both AEM on-premise, and AEM under Managed Services used a static architecture comprised of a fixed number of machines and instances. 

![Static architecture](assets/introduction-01.png "Static architecture")

These:

* Were sized for *peak* traffic (internet) and *peak* activity (marketing), which resulted in them being idle for significant periods of time:
![Static structure must cater for varying usage patterns](assets/introduction-02.png "Static structure must cater for varying usage patterns")

* Were monolithic applications (the quickstart).

* Had a single author instance; which was subject to downtime during maintenance windows.

### AEM as a Cloud Service {#aem-as-a-cloud-service-architecture}
-->

クラウドサービスとしてのAEMには、次の機能が追加されました。

* 可変数のAEM画像を持つ動的アーキテクチャ。

![動的アーキテクチャ](assets/introduction-03.png "動的アーキテクチャ")

このアーキテクチャ：

* 実際のトラフィックと実際のアクティビティ *に基づいて* 、スケール *設定されます* 。

* 個々のインスタンスが必要な場合にのみ実行されます。

* モジュール化されたアプリケーションを使用します。

* デフォルトとして作成者クラスターを持つ。これにより、メンテナンスタスクのダウンタイムを回避できます。

これにより、様々な使用パターンに対する自動スケーリングが可能になります。

![様々な使用パターンの自動スケー](assets/introduction-04.png "リング様々な使用パターンの自動スケーリング")


## アップグレード {#upgrades}

>[!NOTE]
>
>詳しくは、「導入のデプロイ」を [参照してください](/help/implementing/deploying/overview.md)。

<!--
### Previous Versions {#previous-versions-upgrades}

Both AEM on-premise, and AEM under Managed Services were subject to a fixed pattern of a yearly major release augmented by service packs, feature packs and hot-fixes. Often instances would run a major version for two or more years. 

Depending on the upgrade type, the process could require significant preparation consisting of analysis, development and testing, followed with a window of downtime for the actual upgrade.

### AEM as a Cloud Service {#aem-as-a-cloud-service-upgrades}
-->

クラウドサービスとしてのAEMで、継続的な統合と継続的な配信(CI/CD)を使用して、プロジェクトが完全に最新の状態に保たれるようになりました。 これは、すべてのアップグレード操作が完全に自動化され、ユーザーに対するサービスの中断を必要としないことを意味します。

アドビは、サービスのすべての運用インスタンスを最新バージョンのAEMコードベースに事前に更新します。

* バグ修正：

   * 毎日リリースできます。

   * インスタンスは、頻繁に最新のバグ修正で更新されます。 定期的に変更が適用されるにつれ、影響は徐々に大きくなり、サービスへの影響が小さくなります。

   * ほとんどのアップデートは、メンテナンスとセキュリティ上の理由により行われます。

* 新機能:

   * 予測可能な月次スケジュールでリリースされます。

>[!NOTE]
>
>詳しくは、「デプロイメントアーキテクチャ [」を参照してくださ](/help/core-concepts/architecture.md#deployment-architecture)い。

## Cloud Manager {#cloud-manager}

Adobe Cloud Managerは、クラウドサービスとしてのAEMの継続的なアップグレードアプローチに不可欠です。インスタンスへのすべてのアップデートを制御します。これは必須です。

アップデートは、新しいバージョンのクラウドサービスが利用可能な場合にアドビがトリガーできます。 または、Cloud Managerが提供するパイプラインを使用して、アプリケーションの更新をトリガーできます。

Cloud Managerの機能：

* aemプログラムと環境の管理に使用します。

* クラウドサービスとしてのAEMの重要なコンポーネント各新しいテナントは、最初にCloud Managerへのアクセス用にプロビジョニングされます。

* お客様のオペレーションおよび開発スタッフのための単一のエントリーポイント

特に、Cloud Managerから作成できるAEMプログラムの数と種類は、次のいずれかに基づいて決定されます。

* お客様の使用許諾契約に基づき、

* クラウドサービスとしてのAEMを使用して有効化やトレーニングを行う場合は、内部主導型アクターから

* をAdobe.comから開始した試用などの外部駆動型プロセスから呼び出します。

Cloud Managerは、クラウドサービスとしてのAEMの主要コンポーネントを作成し設定できるセルフサービスポータルとして発展しました。

* 新しいプログラムの作成と管理。

* これらのプログラム内でAEM環境を作成し、管理します。

* 顧客コードと関連する設定を特定の環境にデプロイするためのパイプラインを作成し、管理します。

* これらのコンポーネントに関する重要なライフサイクルイベント（製品の更新など）の通知。

現在、Cloud Managerは3つの地域に環境を作成できます（その他の地域は以下のとおりです）。

* 米国（東部）

* EMEA（オランダ）

* APAC（オーストラリア）

## 使用開始 {#onboarding}

>[!NOTE]
>
>詳しくは、オンボーディングを参 [照してくださ](/help/onboarding/home.md)い。

<!--
### Previous Versions {#previous-versions-onboarding}

Implementing an AEM project basically followed traditional project management methods.  

### AEM as a Cloud Service {#aem-as-a-cloud-service-onboarding}

Starting and managing an AEM project is significantly easier when using AEM as a Cloud service as Adobe is responsible for many aspects:
-->

AEMプロジェクトの開始と管理は、AEMをクラウドサービスとして使用する場合に簡単です。アドビは次のような様々な側面を担当しています。

* ベースラインAEM画像は、特定の用途向けに最適化されています。

* 手動で行う設定作業の多くは冗長化されています。

また、現在とは大きく異なります。

* すべての前提条件が満たされていることを確認する評価段階例えば、次のように指定します。

   * 法的要件

   * 契約

   * お客様がカスタマイズした既存のコンテンツやコードに関する技術的要件

* 導入要件：

   * コードの更新；以前のバージョンのAEM用に開発されたお客様向けアプリケーションは、確認して更新する必要があります。

   * コンテンツの移行

## 開発 {#developing}

>[!NOTE]
>
>詳細については、『開発ガイドライン [&amp;開発 — WKNDチュ](/help/implementing/developing/introduction/development-guidelines.md) ートリアル』から始めます [](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

<!--
### Previous Versions {#previous-versions-developing}
-->

<!-- needs more detail -->

<!-- 
Development was an intensive task performed locally, followed by deployment to the production instance. 

### AEM as a Cloud Service {#aem-as-a-cloud-service-developing}
-->

<!-- Will need information for new customers -->
AEMをクラウドサービスとしてサポートする新しいアーキテクチャには、開発者エクスペリエンス全体に対する重要な変更が含まれます。 クラウドサービスとしてのAEMの主な目標の1つは、経験豊富なお客様（オンプレミスまたはアドビ管理サービスのコンテキストでAEMを使用しているお客様）が、カスタマイズしたコードを大量に書き直すことなく、できるだけ迅速にAEMに移行できるようにすることです。 ただし、一部の調整が必要な場合もあります。

<!-- adjusting title level -->

### クラウド開発 {#aem-as-a-cloud-service-developing-cloud-development}

既存のAEMアプリケーションをクラウドサービスとしてAEM上で実行するには、次の手順が必要です。

* アプリケーションのコードと設定は、関連付けられたCloud ManagerプログラムのGitコードリポジトリに保存する必要があります。
* アプリケーションのコードと設定は、ベースラインAEMイメージの最新バージョン（毎日変更される可能性がある）と互換性がある必要があります。
   * お客様のアプリケーションは、Cloud Manager環境に関連付けられたCloud Managerパイプラインを使用して構築およびデプロイする必要があります。
* お客様のアプリケーションは、パイプライン内で実施されるすべてのコード品質、セキュリティ、パフォーマンスのゲートを渡す必要があります。
* お客様のアプリケーション用に作成した画像は、Cloud Managerパイプラインでデプロイする必要があります。

<!-- duration of what? -->
このプロセスは、一般にクラウドファースト開発と呼ばれます。 エンドツーエンドの期間は数分かかると予想されるので（アプリケーションの複雑さに応じて20 ～ 50）、保留中のコードと設定の変更がクラウドで試行される前に、迅速な開発手法を採用する必要があります。

<!-- is this really relevant at this point? -->
OSGIバンドルとその関連設定が管理されるWebコンソール、およびAEM quickStartの以前の部分は、クラウドサービス環境としてAEMのユーザーが直接アクセスできなくなりました。 このインターフェイスは、新しい開発者コンソールを使用して読み取り専用モードで引き続きアクセスできます。 このコンソールを使用すると、開発者は作成者または発行サービスの特定のノードを直接選択してログインし、デフォルトでブロックされている領域にアクセスできます。

開発者にとっては、様々な環境のログファイルにすばやくアクセスする必要があるもう1つの一般的な要件です。 AEMをクラウドサービスとして使用すると、作成者ノードと発行ノードに含まれる各ノードのログファイルが、ダウンロード可能なファイルの形式またはAPI経由でCloud Managerから利用できるようになります。

コードとコンテンツが明確に分離されているので、開発者は、デプロイメントの一部として、特定のプロセスを使用してコンテンツを更新できます。 可変コンテンツの一般的な使用例を次に示します。

* 顧客 *プロジェクト* （フォルダー、テンプレート、ワークフローなど）に含まれる標準のデフォルトコンテンツ

* 検索インデックスの定義

* ACLと権限

* サービスユーザーとユーザーグループ

<!-- adjusting title level -->

### 地域開発 {#aem-as-a-cloud-service-developing-local-development}

迅速な繰り返しと開発をサポートするために、AEMの外部でAEMアプリケーションをクラウドサービスのコンテキストとして開発することもできます。 この目的で、開発者は次のアーティファクトを使用できるようになります。

* AEM as a Cloud Service quickStart:最新のAEM `.jar` コードベースのベースで、同じ機能とAPIサーフェスを備えた、ベースのスタンドアロンインストーラー。

* AEM as a Cloud Service Dispatcher SDK:ディスパッチャー設定をローカルでテストし、検証するためのイメージベースのプロセス

>[!NOTE]
>
>Cloud quickStartでは、AEMサイトとAEM Assetsの機能の一部が許可されていないことに注意してください。 これは、ほとんどの拡張機能を開発およびテストできるシンプルな作成者環境で構成されています。

## 運用とパフォーマンス {#operations-and-performance}

>[!NOTE]
>
>詳細は、「バックアップ」、「インデック [ス作成](/help/operations/backup.md)」、「その他のメンテナ [ンスタスク」から始めます](/help/operations/indexing.md)[](/help/operations/maintenance.md)。

<!--
### Previous Versions {#previous-versions-operations-and-performance}

In the past, especially on the author side, there was a need to periodically stop an instance; for routine maintenance operations, as well as upgrades and updates. For some customers, this resulted in hours of scheduled downtime on a weekly basis. 

### AEM as a Cloud Service {#aem-as-a-cloud-service-operatioms-and-performance}
-->

AEMをクラウドサービスとして使用すると、サービスの中断が不要になるように、このような操作が自動化されます。

次の領域では、

* 多くのタスクが自動化されました。

* トポロジーは、最大の耐障害性と効率性を実現するために最適化されています。たとえば、バイナリレスレプリケーションがデフォルトです。

* キュー、ジョブ、バルク処理タスクなどの負荷の高いタスクは、共有および専用のマイクロサービスで処理されるコアAEMインスタンスから移動されました。

クラウドサービスとしてのAEMの運用も、新しい監視、レポート、警告インフラストラクチャでサポートされます。 これにより、Adobe SRE(Site Reliability Engineers)は、サービスの健全性を積極的に維持できます。 この建築の様々な要素には様々なヘルスチェックが備わっています。 何らかの理由で、アーキテクチャの特定のノードが異常と見なされる場合、そのノードはサービスから削除され、新しい正常なノードにサイレントに置き換えられます。

## ID 管理 {#identity-management}

>[!NOTE]
>
>詳しくは、セキュリティ — IMS [のサポートを参照してください](/help/security/ims-support.md)。

<!--
### Previous Versions {#previous-versions-identity-management}

By default, identity management was internal to AEM.

>[!NOTE]
>
>AEM 6.4.3.0 introduced:
>
>* Admin Console support for AEM instances. 
>* Adobe IMS (Identity Management System) based authentication for AEM Managed Services customers.

### AEM as a Cloud Service {#aem-as-a-cloud-service-identity-management}
-->

クラウドサービスとしてのAEMの大きな変更点は、作成者層へのアクセスにAdobe IDを完全に統合して使用することです。

これには、ユーザーとユーザーグ [ループを管理するため](https://helpx.adobe.com/enterprise/using/admin-console.html) 、Adobe Admin Consoleを使用する必要があります。 ユーザーアカウントを使用すると、ユーザープロファイル情報がAdobe Identity Management System(IMS)に一元化され、すべてのクラウドサービスで共有されるので、ユーザーはアドビの製品やサービスにアクセスできます。 AEMへのアクセスを割り当てると、そのユーザーアカウントをクラウドサービスとしてAEMで（以前と同様に）参照できます。例えば、AEMセキュリティユーザーインターフェイスからロールと権限を定義する場合などです。

これは、次の利点を兼ね備えています。

* Adobe Identity Management System(IMS)を使用して、すべてのAdobeクラウドアプリケーションにシングルサインオンを提供します。

* AEMの各特定のインスタンスに対して、クラウドサービスとしてローカルのままのユーザー環境設定。

## オーサリングユーザーインターフェイス {#authoring-user-interface}

>[!NOTE]
>
>詳しくは、基本処理 [を参照](/help/sites-cloud/authoring/getting-started/basic-handling.md) 。

<!--
### Previous Versions {#previous-versions-authoring}

The user interface of the author instance (UI), for both Sites and Assets, was progressively developed and optimized to cater for all use-cases, using both the touch-enabled and classic UIs.

### AEM as a Cloud Service {#aem-as-a-cloud-service-authoring}
-->

オーサリングユーザーインターフェイス(UI)の基本原則は、サイトとアセットの両方に関して、以前にAEMを使用したことのあるユーザーにとって非常になじみ深いものです。

主な違いは、UIが完全にタッチ対応であることです。従来のUIは使用できなくなりました。 そうしないと、基本的な変更は変わらず、わずかな変更だけが見えます。

## AEM Sites {#aem-sites}

クラウドサービスとしてのAdobe Experience Manager Sitesでは、AEM Content Management systemの機能とAEM Digital Asset Managementを組み合わせることで、顧客に対してパーソナライズされたコンテンツ主導のエクスペリエンスを提供できます。

詳しくは、「サイトの変更」の概 [要を参照してください](/help/sites-cloud/sites-cloud-changes.md)。

## AEM Assets {#aem-assets}

クラウドサービスとしてのAdobe Experience Manager Assetsは、デジタルアセット管理とダイナミックメディアの処理を迅速かつ効果的に行うだけでなく、常に最新で常に利用可能で常に学習可能なシステム内でAI/MLなどの次世代のスマート機能を利用できる、クラウドネイティブのSaaSソリューションです。

アセットの提供には、次世代のアセット処理をクラウドで実行し、高パフォーマンスのアセットの取り込みと検索を行う機能が含まれます。

詳しくは、「クラウドサ [ービスとしてのアセットの概要と概要」を参照してください](/help/assets/overview.md)。
