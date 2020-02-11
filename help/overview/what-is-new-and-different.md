---
title: 新機能 — クラウドサービスとしてのAdobe Experience Manager
description: '新機能 — クラウドサービスとしてのAdobe Experience Manager(AEM)。 '
translation-type: tm+mt
source-git-commit: 1548efb4c63c3c5dbd47b1b92a9e8bb998c42267

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

<!-- * [Miscellaneous](#miscellaneous) -->

## アーキテクチャ {#architecture}

>[!NOTE]
>
>詳しくは、アーキテクチャを参照し [てください](/help/core-concepts/architecture.md)。

### 以前のバージョン {#previous-versions-architecture}

AEMオンプレミスとマネージドサービスのAEMの両方で、固定数のマシンとインスタンスで構成された静的アーキテクチャが使用されていました。

![静的アーキテクチャ](assets/introduction-01.png "静的アーキテクチャ")

次の情報：

* ピークトラフィ *ック* （インターネット）とピークアクティビティ ** （マーケティング）に合わせてサイズ設定されたため、アイドル状態が長く続いていました。
   ![静的構造は様々な使用パターンに対応する必要があ](assets/introduction-02.png "ります静的構造は様々な使用パターンに対応する必要があります")

* モノリシックなアプリケーション（クイックスタート）。

* 1つの作成者インスタンスがあり、メンテナンス期間中にダウンタイムが発生する可能性がある

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-architecture}

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

<!--
>[!NOTE]
>
>For further details see the [Deploying Introduction](/help/sites/deploying/introduction.md).
-->

### 以前のバージョン {#previous-versions-upgrades}

AEMオンプレミスおよび管理サービスの下のAEMは、サービスパック、機能パック、およびホットフィックスによって拡張された年別メジャーリリースの固定パターンの対象となりました。 多くの場合、インスタンスでは2年以上メジャーバージョンが実行されます。

アップグレードのタイプに応じて、分析、開発、テストから成る重要な準備を行い、実際のアップグレードに伴うダウンタイムを伴うことが必要になる場合があります。

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-upgrades}

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

* お客様のライセンス契約に基づき、クレジットのプールとして

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

<!--
>[!NOTE]
>
>For further details see [Onboarding - An Overview](/help/onboarding/overview.md).
-->

### 以前のバージョン {#previous-versions-onboarding}

AEMプロジェクトの実装は、基本的に従来のプロジェクト管理方法に従って行われます。

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-onboarding}

AEMプロジェクトの開始と管理は、アドビが様々な側面を担当するので、AEMをクラウドサービスとして使用する場合に大幅に簡単になります。

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
>詳しくは、『開発ガイドライン』のドキュメ [ントを参照して](/help/implementing/developing/introduction/development-guidelines.md) ください。

<!--
>[!NOTE]
>
>For further details start with [The Developing Experience](/help/sites/developing/introduction/developer-experience.md, [Developing - The Basics](/help/sites/developing/introduction/the-basics.md) and [Developing Best Practices](/help/sites/best-practices/developing.md).
-->

### 以前のバージョン {#previous-versions-developing}

<!-- needs more detail -->
開発は、ローカルで実行され、その後実稼働インスタンスにデプロイされるという大量のタスクでした。

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-developing}

<!-- Will need information for new customers -->
AEMをクラウドサービスとしてサポートする新しいアーキテクチャには、開発者エクスペリエンス全体に対する重要な変更が含まれます。 クラウドサービスとしてのAEMの主な目標の1つは、経験豊富なお客様（オンプレミスまたはアドビ管理サービスのコンテキストでAEMを使用しているお客様）が、カスタマイズしたコードを大量に書き直すことなく、できるだけ迅速にAEMに移行できるようにすることです。 ただし、一部の調整が必要な場合もあります。

#### クラウド開発 {#aem-as-a-cloud-service-developing-cloud-development}

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

#### 地域開発 {#aem-as-a-cloud-service-developing-local-development}

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

### 以前のバージョン {#previous-versions-operations-and-performance}

以前は、特に著者側では、定期的にインスタンスを停止する必要がありました。定期的なメンテナンス操作、アップグレードや更新に使用します。 この結果、一部のお客様は、週単位で予定されたダウンタイムが数時間に及ぶことがありました。

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-operatioms-and-performance}

AEMをクラウドサービスとして使用すると、サービスの中断が不要になるように、このような操作が自動化されます。

次の領域では、

* 多くのタスクが自動化されました。

* トポロジーは、最大の耐障害性と効率性を実現するために最適化されています。たとえば、バイナリレスレプリケーションがデフォルトです。

* キュー、ジョブ、バルク処理タスクなどの負荷の高いタスクは、共有および専用のマイクロサービスで処理されるコアAEMインスタンスから移動されました。

クラウドサービスとしてのAEMの運用も、新しい監視、レポート、警告インフラストラクチャでサポートされます。 これにより、Adobe SRE(Site Reliability Engineers)は、サービスの健全性を積極的に維持できます。 この建築の様々な要素には様々なヘルスチェックが備わっています。 何らかの理由で、アーキテクチャの特定のノードが異常と見なされる場合、そのノードはサービスから削除され、新しい正常なノードにサイレントに置き換えられます。

## ID 管理 {#identity-management}

<!--
>[!NOTE]
>
>For further details see [Security - Single Sign-On](/help/sites/security/single-sign-on.md).
-->

### 以前のバージョン {#previous-versions-identity-management}

デフォルトでは、ID管理はAEMの内部にありました。

>[!NOTE]
>
>AEM 6.4.3.0で導入された機能：
>
>* AEMインスタンスの管理コンソールのサポート。
>* AEM Managed Servicesのお客様向けのAdobe IMS(Identity Management System)ベースの認証。


### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-identity-management}

クラウドサービスとしてのAEMの大きな変更点は、作成者層へのアクセスにAdobe IDを完全に統合して使用することです。

これには、ユーザーとユーザーグ [ループを管理するため](https://helpx.adobe.com/enterprise/using/admin-console.html) 、Adobe Admin Consoleを使用する必要があります。 ユーザーアカウントを使用すると、ユーザープロファイル情報がAdobe Identity Management System(IMS)に一元化され、すべてのクラウドサービスで共有されるので、ユーザーはアドビの製品やサービスにアクセスできます。 AEMへのアクセスを割り当てると、そのユーザーアカウントをクラウドサービスとしてAEMで（以前と同様に）参照できます。例えば、AEMセキュリティユーザーインターフェイスからロールと権限を定義する場合などです。

これは、次の利点を兼ね備えています。

* Adobe Identity Management System(IMS)を使用して、すべてのAdobeクラウドアプリケーションにシングルサインオンを提供します。

* AEMの各特定のインスタンスに対して、クラウドサービスとしてローカルのままのユーザー環境設定。

## オーサリングユーザーインターフェイス {#authoring-user-interface}

<!--
>[!NOTE]
>
>For further details, the [Basic Handling](/help/sites/authoring/getting-started/basic-handling.md) and [Best Practices](/help/sites/best-practices/authoring.md) are good starting points.
-->

### 以前のバージョン {#previous-versions-authoring}

オーサーインスタンス(UI)のユーザーインターフェイスは、SitesとAssetsの両方に対して、プログレッシブに開発され、タッチ対応UIとクラシックUIの両方を使用して、すべてのユースケースに対応するように最適化されました。

### クラウドサービスとしてのAEM {#aem-as-a-cloud-service-authoring}

オーサリングユーザーインターフェイス(UI)の基本原則は、サイトとアセットの両方に関して、以前にAEMを使用したことのあるユーザーにとって非常になじみ深いものです。

主な違いは、UIが完全にタッチ対応であることです。従来のUIは使用できなくなりました。 そうしないと、基本的な変更は変わらず、わずかな変更だけが見えます。

## AEM Sites {#aem-sites}

クラウドサービスとしてのAdobe Experience Manager Sitesでは、AEM Content Management systemの機能とAEM Digital Asset Managementを組み合わせることで、顧客に対してパーソナライズされたコンテンツ主導のエクスペリエンスを提供できます。

詳しくは、「サイトの変更」の概 [要を参照してください](/help/sites-cloud/sites-cloud-changes.md)。

## AEM Assets {#aem-assets}

クラウドサービスとしてのAdobe Experience Manager Assetsは、デジタルアセット管理とダイナミックメディアの処理を迅速かつ効果的に行うだけでなく、常に最新で常に利用可能で常に学習可能なシステム内でAI/MLなどの次世代のスマート機能を利用できる、クラウドネイティブのSaaSソリューションです。

アセットの提供には、次世代のアセット処理をクラウドで実行し、高パフォーマンスのアセットの取り込みと検索を行う機能が含まれます。

詳しくは、「クラウドサ [ービスとしてのアセットの概要と概要」を参照してください](/help/assets/overview.md)。

<!--

#### Previous Versions {#previous-versions-aem-sites}

tbc

#### AEM as a Cloud Service {#aem-as-a-cloud-service-aem-sites}

tbc

-->

<!--

#### Previous Versions* {#previous-versions-aem-assets}

tbc

#### AEM as a Cloud Service {#aem-as-a-cloud-service-aem-assets}

tbc 

-->

<!--

### Miscellaneous {#miscellaneous}

#### AEM as a Cloud Service {#aem-as-a-cloud-service-miscellaneous}

Additionally???

-->
