---
title: 新機能と新機能 —Cloud ServiceとしてのAdobe Experience Manager
description: 'Cloud Serviceとしての違いおよび新機能 —Adobe Experience Manager(AEM) '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 10%

---


# 新機能と相違点 {#what-is-new-and-what-is-different}

AEMは、長年にわたって、次の両方を利用できます。

* オンプレミス

* 管理サービスとして

以前のアプローチとCloud ServiceとしてのAEMには、本質的に異なる点があります。

* [アーキテクチャ](#architecture)
* [アップグレード](#upgrades)
* [Cloud Manager](#cloud-manager)
* [オンボーディング](#onboarding)
* [開発](#developing)
* [運用とパフォーマンス](#operations-and-performance)
* [ID 管理](#identity-management)
* [オーサリングユーザーインターフェイス](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>これらの概要は完全なものではありませんが、紹介を目的としています。

>[!NOTE]
>
>オンプレミスおよびマネージドサービスのバージョンについて詳しくは、 [AEM 6.5のドキュメントセットを参照してください](https://helpx.adobe.com/jp/support/experience-manager/6-5.html)。

## アーキテクチャ {#architecture}

>[!NOTE]
>
>詳しくは、 [アーキテクチャを参照してください](/help/core-concepts/architecture.md)。

AEM as a Cloud Service には次の機能が追加されました。

* AEM イメージの数が可変の動的なアーキテクチャ。

![動的なアーキテクチャ](assets/introduction-03.png "動的なアーキテクチャ")

このアーキテクチャには次の特長があります。

* *実際の*&#x200B;トラフィックと&#x200B;*実際の*&#x200B;アクティビティに基づいて、規模が拡大／縮小されます。

* 必要な場合にのみ個々のインスタンスが実行されます。

* モジュール型アプリケーションを使用します。

* デフォルトでオーサークラスターがあるので、メンテナンスタスクのダウンタイムを避けることができます。

これにより、様々な使用パターンに応じた自動スケーリングが可能になります。

![様々な使用パターンに応じた自動スケーリング](assets/introduction-04.png "様々な使用パターンに応じた自動スケーリング")


## アップグレード {#upgrades}

>[!NOTE]
>
>詳しくは、「 [導入のデプロイ」を参照してください](/help/implementing/deploying/overview.md)。

Cloud ServiceとしてのAEMで、連続統合と連続配信(CI/CD)を使用して、プロジェクトが完全に最新の状態に保たれるようになりました。 これは、すべてのアップグレード操作が完全に自動化されているため、ユーザーに対するサービスの中断を必要としないことを意味します。

アドビは、サービスのすべての操作インスタンスを最新バージョンのAEMコードベースに更新する際に、事前に対処します。

* バグ修正：

   * 毎日リリースできます。

   * インスタンスは、頻繁に最新のバグ修正で更新されます。 定期的に変更が適用されるにつれ、影響は徐々に大きくなり、サービスへの影響が減少します。

   * ほとんどのアップデートは、メンテナンスおよびセキュリティ上の理由により行われます。

* 新機能:

   * 予測可能な月次スケジュールでリリースされます。

>[!NOTE]
>
>詳しくは、 [デプロイメントアーキテクチャ](/help/core-concepts/architecture.md#deployment-architecture)を参照してください。

## Cloud Manager {#cloud-manager}

Adobe Cloud Managerは、AEMの継続的なアップグレードアプローチにCloud Serviceとして不可欠です。インスタンスに対するすべてのアップデートを制御します。これは必須です。

アップデートは、クラウドサービスの新しいバージョンが利用可能な場合にアドビがトリガーできます。 または、Cloud Managerが提供するパイプラインを使用してアプリケーションの更新をトリガーできます。

Cloud Managerの機能は次のとおりです。

* AEMのプログラムと環境の管理に使用、

* Cloud ServiceとしてのAEMの不可欠な要素； 各新しいテナントは、最初にCloud Managerへのアクセス用にプロビジョニングされます。

* オペレーションおよび開発スタッフのための単一のエントリーポイント

特に、Cloud Managerから作成できるAEMプログラムの数と種類は、次のいずれかに基づいて決定されます。

* お客様の使用許諾契約に基づき、

* Cloud ServiceとしてのAEMが有効化やトレーニングに使用されている場合、内部主導のアクターから

* を呼び出す必要があります。

Cloud Managerは、Cloud ServiceとしてのAEMの主要コンポーネントを作成および設定できるセルフサービスポータルとして発展しました。

* 新規プログラムの作成と管理。

* これらのプログラム内でAEM環境を作成し、管理します。

* カスタマーコードと関連する設定を特定の環境にデプロイするためのパイプラインの作成と管理。

* これらのコンポーネントに関する重要なライフサイクルイベント（製品の更新など）の通知。

現在、Cloud Managerでは、3つの地域に環境を作成できます（以下に示す地域が増えます）。

* 米国（東部）

* EMEA（オランダ）

* APAC（オーストラリア）

## 使用開始 {#onboarding}

>[!NOTE]
>
>詳しくは、 [オンボーディングを参照してください](/help/onboarding/home.md)。

AEMプロジェクトの開始と管理は、AEMをクラウドサービスとして使用する場合に簡単です。アドビは次のような様々な側面を担当しています。

* ベースラインAEM画像は、特定の用途向けに最適化されています。

* 手動の構成タスクの多くは冗長化されています。

また、現在とは大きく異なります。

* すべての前提条件が満たされていることを確認する評価フェーズ。 例えば、次のように指定します。

   * 法的要件

   * 契約

   * お客様がカスタマイズした既存のコンテンツやコードの技術要件

* 導入要件：

   * コードの更新； 以前のバージョンのAEM用に開発されたお客様向けアプリケーションは、確認して更新する必要があります。

   * コンテンツの移行

## 開発 {#developing}

>[!NOTE]
>
>詳細については、『 [開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md) &amp; [開発 — WKNDチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)』を参照してください。

AEMをCloud Serviceとしてサポートする新しいアーキテクチャには、開発者の体験全体に対していくつかの重要な変更が含まれます。 Cloud ServiceとしてのAEMの主な目標の1つは、経験豊富なお客様(AEMをオンプレミスまたはAdobe Managed Servicesのコンテキストで使用した場合)が、カスタマイズしたコードの大部分を書き直さずに、できるだけ早くAEMに移行できるようにすることです。 ただし、一部の調整が必要な場合もあります。

### クラウドの開発 {#aem-as-a-cloud-service-developing-cloud-development}

既存のAEMアプリケーションをCloud ServiceとしてAEM上で実行する場合は、次の手順が必要です。

* アプリケーションのコードと設定は、関連付けられたCloud ManagerプログラムのGitコードリポジトリに保存する必要があります。
* アプリケーションのコードと設定は、ベースラインAEMイメージの最新バージョンと互換性がある必要があります（毎日変更される可能性があります）。
   * お客様のアプリケーションは、Cloud Manager環境に関連付けられたCloud Managerパイプラインを使用して構築およびデプロイする必要があります。
* お客様のアプリケーションは、パイプライン内で実施されるすべてのコード品質、セキュリティ、およびパフォーマンスのゲートを渡す必要があります。
* お客様のアプリケーション用に作成した画像は、Cloud Managerパイプラインでデプロイする必要があります。

このプロセスは、一般に、クラウドファースト開発と呼ばれます。 エンドツーエンドの期間は、（アプリケーションの複雑さに応じて20 ～ 50の間で）数分かかると予想されるので、保留中のコードと設定の変更がクラウドで試行される前に、迅速な開発手法を採用する必要があります。

OSGIバンドルとその関連設定が管理されるWebコンソール、およびAEM QuickStartの以前の一部であるWebコンソールは、Cloud Service環境としてAEMのユーザーが直接アクセスできなくなりました。 新しい開発者コンソールを使用して、このインターフェイスに引き続き読み取り専用モードでアクセスできます。 このコンソールを使用すると、開発者は作成者または発行サービスの特定のノードを直接選択してログインし、デフォルトでブロックされている領域にアクセスできます。

>[!NOTE]
>
>「 [OSGi設定」も参照](/help/implementing/deploying/overview.md#osgi-configuration)

開発者にとって、様々な環境ーのログファイルにすばやくアクセスする必要があるもう1つの一般的な要件です。 AEMをCloud Serviceとして使用する場合、作成者ノードと発行ノードに含まれる異なるノードのログファイルは、ダウンロード可能なファイルの形式、またはAPIを介してCloud Managerで利用できます。

コードとコンテンツが明確に分割されているので、開発者は、展開の一環として、特定のプロセスを使用してコンテンツを更新できます。 可変コンテンツの一般的な使用例は次のとおりです。

* 顧客プロジェクトの一部である標準 *的なデフォルト* ・コンテンツ(フォルダ、テンプレート、ワークフローなど)

* 検索インデックスの定義

* ACLと権限

* サービスユーザーとユーザーグループ

### ローカル開発 {#aem-as-a-cloud-service-developing-local-development}

迅速な反復と開発をサポートするために、AEMの外部でAEMCloud Serviceを開発コンテキストとして開発することもできます。 この目的で、開発者は次のアーティファクトを使用できます。

* Cloud ServiceクイックスタートとしてのAEM: 最新のAEMコードベースの `.jar` ベースで、同じ機能とAPIサーフェスを持つスタンドアロンのインストーラー。

* Cloud ServiceDispatcherSDKとしてのAEM: Dispatcher設定をローカルでテストおよび検証する画像ベースのプロセス

>[!NOTE]
>
>Cloud QuickStartでは、すべてのAEM SitesおよびAEM Assets機能が使用できるわけではありません。 これは、大部分の拡張機能を開発およびテストできる、単純な作成者環境で構成されています。

## 運用とパフォーマンス {#operations-and-performance}

>[!NOTE]
>
>詳細については、最初に「[バックアップ](/help/operations/backup.md)」、「[インデックス作成](/help/operations/indexing.md)」、「[その他のメンテナンスタスク](/help/operations/maintenance.md)」を参照してください。

AEMをCloud Serviceとして使用する場合、このような操作は自動化され、サービスの中断が不要になります。

次の領域で、

* 多くのタスクが自動化されています。

* トポロジーは、最大限の回復性と効率性を実現するために最適化されています。 たとえば、バイナリレスレプリケーションがデフォルトです。

* キュー、ジョブ、バルク処理タスクなどの負荷の大きいタスクは、共有および専用のマイクロサービスで処理されるコアAEMインスタンスから移動されました。

Cloud ServiceとしてのAEMの運用も、新しい監視、レポート、および警告インフラストラクチャでサポートされます。 これにより、Adobe SRE（サイト信頼性エンジニア）は、サービスの健全性をプロアクティブに維持できます。 この建築の様々な要素には様々なヘルスチェックが備わっています。 何らかの理由で、アーキテクチャの特定のノードが異常と見なされる場合、そのノードはサービスから削除され、静かに新しい正常なノードに置き換えられます。

## ID 管理 {#identity-management}

>[!NOTE]
>
>詳しくは、 [セキュリティ — IMSのサポートを参照してください](/help/security/ims-support.md)。

Cloud ServiceとしてのAEMの大きな変更点は、Adobe IDを統合して作成者層にアクセスすることです。

これには、ユーザーとユーザーグループを管理するために [Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用する必要があります。 ユーザーアカウントを使用すると、ユーザープロファイル情報がAdobeIdentity Managementシステム(IMS)に一元化され、すべてのクラウドサービスで共有されるので、ユーザーはアドビの製品やサービスにアクセスできます。 AEMへのアクセスを割り当てると、ユーザーアカウントはAEM内でCloud Serviceとして（以前と同様）参照できます。 例えば、AEMセキュリティユーザーインターフェイスからロールと権限を定義する場合などです。

これにより、次の利点が得られます。

* AdobeIdentity Managementシステム(IMS)を使用して、すべてのAdobeクラウドアプリケーションでシングルサインオンを提供する。

* AEMの各特定のインスタンスに対してCloud Serviceとしてローカルのままのユーザー環境設定。

## オーサリングユーザーインターフェイス {#authoring-user-interface}

>[!NOTE]
>
>詳しくは、 [基本処理](/help/sites-cloud/authoring/getting-started/basic-handling.md) (Basic Handling)を参考にしてください。

オーサリングユーザーインターフェイス(UI)の基本原則は、サイトとアセットの両方にとって、これまでAEMを使用したことのある人には非常になじみ深いものです。

主な違いは、UIが完全にタッチ対応であることです。 従来のUIは使用できなくなりました。 そうしないと、基本は変更されず、わずかな変更だけが表示されます。

## AEM Sites {#aem-sites}

Adobe Experience ManagerサイトをCloud Serviceとして使用すると、AEMコンテンツ管理システムの機能とAEM Digital Asset Managementを組み合わせて、コンテンツ主導のパーソナライズされた体験を顧客に提供できます。

詳しくは、「サイトの [変更点の概要](/help/sites-cloud/sites-cloud-changes.md)」を参照してください。

## AEM Assets {#aem-assets}

Adobe Experience Manager資産をCloud ServiceオファーとしてクラウドネイティブのSaaSソリューションとしてDynamic Mediaし、高速でインパクトを与えるだけでなく、常に最新で常に利用可能で常に学習可能なシステム内で、AI/MLなどの次世代のスマート機能を利用できます。

アセットの提供には、次世代のアセット処理をクラウドで実行し、高パフォーマンスのアセット取り込みと検索を行う機能が含まれます。

詳しくは、「 [概要とCloud Serviceとしてのアセットの概要](/help/assets/overview.md)」を参照してください。

## Adobe Experience Manager as a Cloud Service の理解 {#getting-to-know-aem-as-cloud-service}

詳しくは、次のセクションを参照してください。

* [Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service の[アーキテクチャ](/help/core-concepts/architecture.md)
* [Cloud ServiceとしてのAEMに対する注目すべき変更点（リリースノート）](/help/release-notes/aem-cloud-changes.md)
* [ Sites as a Cloud Service の主な変更点](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service の主な変更点](/help/assets/assets-cloud-changes.md)
* [Cloud ServiceとしてのAEM Assetsの導入](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)
