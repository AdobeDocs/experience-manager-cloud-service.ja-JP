---
title: Cloud ServiceとしてのAdobe Experience Manager
description: '違いと新機能 —Cloud ServiceとしてのAdobe Experience Manager(AEM)。 '
translation-type: tm+mt
source-git-commit: ca37f00926fc110b865e6db2e61ff1198519010b
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 11%

---


# 新機能と相違点 {#what-is-new-and-what-is-different}

長年の間、AEMは以下の両方を利用できます。

* オンプレミス

* 管理サービスとして

以前のアプローチとAEMのCloud Serviceには、本質的な違いがあります。

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


## アップデート {#upgrades}

>[!NOTE]
>詳しくは、 [AEM Version Updatesを参照してください](/help/implementing/deploying/aem-version-updates.md)。

AEMをCloud Serviceとして使用する場合、連続配信(CI/CD)を使用して、プロジェクトが確実に最新のAEMバージョンになるようになりました。

これは、すべてのアップグレード操作が完全に自動化されているため、ユーザーに対するサービスの中断を必要としないことを意味します。
Adobeは、サービスのすべての運用インスタンスをAEMコードベースの最新バージョンに更新する際に、事前に対処します。AEMバージョンのアップデートには、次の2種類があります。

* **プッシュの更新**

   * 毎日リリースできます。
   * ほとんどのメンテナンス作業で、最新のバグ修正やセキュリティ更新が含まれています。

   定期的に変更が適用されるにつれ、影響は徐々に大きくなり、サービスへの影響が減少します。

>[!NOTE]
>AEMのプッシュアップデートの詳細については、 [Adobe Experience ManagerのCloud Service継続配信モデルとしてのホワイトペーパーを参照してください](https://fieldreadiness-adobe.highspot.com/items/5ea322e1c714336c23b32599#2)

* **新機能の更新**

   * 予測可能な月次スケジュールでリリース。

>[!NOTE]
>詳しくは、 [デプロイメントアーキテクチャを参照してください](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/core-concepts/architecture.html#deployment-architecture) 。

## Cloud Manager {#cloud-manager}

AdobeCloud Managerは、AEMの継続的なアップグレードアプローチにCloud Serviceとして不可欠です。インスタンスに対するすべてのアップデートを制御します。これは必須です。

更新は、クラウドサービスの新しいバージョンが利用可能な場合に、Adobeによってトリガーされる場合があります。 または、Cloud Managerが提供するパイプラインを使用してアプリケーションの更新をトリガーできます。

Cloud Managerの機能は次のとおりです。

* aemプログラムと環境の管理に使用

* cloud serviceとしてのAEMの不可欠な要素；各新しいテナントは、最初にCloud Managerへのアクセス用にプロビジョニングされます。

* オペレーションおよび開発スタッフのための単一のエントリーポイント

特に、Cloud Managerから作成できるAEMプログラムの数と種類は、次のいずれかに基づいて決定されます。

* お客様の使用許諾契約に基づき、

* aemをCloud Serviceとして使用し、実現やトレーニングを行う場合は、内部からの影響を受けます。

* adobe.comから開始した試行など、外部主導のプロセスから取得した場合。

Cloud Managerは、Cloud ServiceとしてのAEMの主要コンポーネントを作成および設定できるセルフサービスポータルとして発展しました。

* 新規プログラムの作成と管理。 詳細は、 [「プログラムとプログラムタイプについて](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) 」を参照してください。

* これらのプログラム内でAEM環境を作成し、管理します。 Refer to [Managing Environments](/help/implementing/cloud-manager/manage-environments.md) for more details.

* カスタマーコードと関連する設定を特定の環境にデプロイするためのパイプラインの作成と管理。 詳細は、『CI-CDパイプラインの [設定](/help/implementing/cloud-manager/configure-pipeline.md) 』を参照してください。

* これらのコンポーネントに関する重要なライフサイクルイベント（製品の更新など）の通知。

現在、Cloud Managerでは、3つの地域に環境を作成できます（以下に示す地域が増えます）。

* 米国（東部）

* EMEA（オランダ）

* APAC（オーストラリア）

>[!NOTE]
>AEMでCloud ManagerをCloud Serviceとして使用するには、「Cloud Serviceとしての [Experience Managerへのアクセス](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md) 」を参照してください。

## 使用開始 {#onboarding}

>[!NOTE]
>
>詳しくは、 [オンボーディングを参照してください](/help/onboarding/home.md)。

AEMプロジェクトの開始と管理は、AEMをクラウドサービスとして使用する場合に、Adobeは次のような多くの側面を担当します。

* ベースラインAEM画像は、特定の用途向けに最適化されています。

* 手動の構成タスクの多くは冗長化されています。

また、現在とは大きく異なります。

* すべての前提条件が満たされていることを確認する評価フェーズ。例えば、次のように指定します。

   * 法的要件

   * 契約

   * お客様がカスタマイズした既存のコンテンツやコードの技術要件

* 導入要件：

   * コードの更新；aemの以前のバージョン用に開発されたお客様向けアプリケーションは、レビューを行い、場合によっては更新する必要があります。

   * コンテンツの移行

## 開発 {#developing}

>[!NOTE]
>
>詳細については、『 [開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md) &amp; [開発 — WKNDチュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)』を参照してください。

AEMをCloud Serviceとしてサポートする新しいアーキテクチャには、開発者の体験全体に対するいくつかの重要な変更が含まれます。 AEMをCloud Serviceとして使用する主な目標の1つは、経験豊富なお客様(AEMをオンプレミスまたはAdobe Managed Servicesのコンテキストで使用)が、カスタマイズしたコードの大部分を書き直さずに、できるだけ早くAEMにCloud Serviceできるようにすることです。 ただし、一部の調整が必要な場合もあります。

### クラウドの開発 {#aem-as-a-cloud-service-developing-cloud-development}

既存のAEMアプリケーションをCloud ServiceとしてAEM上で実行する場合は、次の手順が必要です。

* アプリケーションのコードと設定は、関連付けられたCloud ManagerプログラムのGitコードリポジトリに保存する必要があります。
* アプリケーションのコードと設定は、ベースラインAEMイメージの最新バージョンと互換性がある必要があります（毎日変更される可能性があります）。
   * お客様のアプリケーションは、Cloud Manager環境に関連付けられたCloud Managerパイプラインを使用して構築およびデプロイする必要があります。
* お客様のアプリケーションは、パイプライン内で実施されるすべてのコード品質、セキュリティ、およびパフォーマンスのゲートを渡す必要があります。
* お客様のアプリケーション用に作成した画像は、Cloud Managerパイプラインでデプロイする必要があります。

このプロセスは、一般に、クラウドファースト開発と呼ばれます。 エンドツーエンドの期間は、（アプリケーションの複雑さに応じて20 ～ 50の間で）数分かかると予想されるので、保留中のコードと設定の変更がクラウドで試行される前に、迅速な開発手法を採用する必要があります。

OSGIバンドルとその関連設定が管理されるWebコンソール、およびAEM QuickStartの以前の部分は、Cloud Service環境としてAEMのユーザーが直接アクセスできなくなりました。 新しい開発者コンソールを使用して、このインターフェイスに引き続き読み取り専用モードでアクセスできます。 このコンソールを使用すると、開発者は作成者または発行サービスの特定のノードを直接選択してログインし、デフォルトでブロックされている領域にアクセスできます。

>[!NOTE]
>
>「 [OSGi設定」も参照](/help/implementing/deploying/overview.md#osgi-configuration)

開発者にとって、様々な環境ーのログファイルにすばやくアクセスする必要があるもう1つの一般的な要件です。 AEMをCloud Serviceとして使用する場合、作成者ノードと発行ノードに含まれる異なるノードのログファイルは、ダウンロード可能なファイルの形式、またはAPI経由でCloud Managerで利用できます。

コードとコンテンツが明確に分割されているので、開発者は、展開の一環として、特定のプロセスを使用してコンテンツを更新できます。 可変コンテンツの一般的な使用例は次のとおりです。

* 顧客プロジェクトの一部である標準 *的なデフォルト* ・コンテンツ(フォルダ、テンプレート、ワークフローなど)

* 検索インデックスの定義

* ACLと権限

* サービスユーザーとユーザーグループ

### ローカル開発 {#aem-as-a-cloud-service-developing-local-development}

迅速な反復と開発をサポートするために、Cloud ServiceコンテキストとしてAEM以外でAEMアプリケーションを開発することも可能です。 この目的で、開発者は次のアーティファクトを使用できます。

* Cloud ServiceクイックスタートとしてのAEM:最新のAEMコードベースの `.jar` ベースのスタンドアロンインストーラーで、同じ機能とAPIサーフェスを備えています。

* Cloud ServiceディスパッチャーSDKとしてのAEM:ディスパッチャー設定をローカルでテストおよび検証する、イメージベースのプロセス

>[!NOTE]
>
>Cloud QuickStartでは、AEM SitesおよびAEM Assetsのすべての機能が使用できないことに注意してください。 これは、大部分の拡張機能を開発およびテストできる、単純な作成者環境で構成されています。

## 運用とパフォーマンス {#operations-and-performance}

>[!NOTE]
>
>詳細については、最初に「[バックアップ](/help/operations/backup.md)」、「[インデックス作成](/help/operations/indexing.md)」、「[その他のメンテナンスタスク](/help/operations/maintenance.md)」を参照してください。

AEMをCloud Serviceとして使用すると、サービスの中断が不要になるように、このような操作が自動化されます。

次の領域で、

* 多くのタスクが自動化されています。

* トポロジーは、最大限の回復性と効率性を実現するために最適化されています。たとえば、バイナリレスレプリケーションがデフォルトです。

* キュー、ジョブ、バルク処理タスクなどの負荷の大きいタスクは、共有および専用のマイクロサービスで処理されるコアAEMインスタンスから移動されました。

Cloud ServiceとしてのAEMの運用も、新しい監視、レポート、および警告インフラストラクチャによってサポートされます。 これにより、AdobeSRE（サイト信頼性エンジニア）は、サービスを積極的に健全な状態に維持できます。 この建築の様々な要素には様々なヘルスチェックが備わっています。 何らかの理由で、アーキテクチャの特定のノードが異常と見なされる場合、そのノードはサービスから削除され、静かに新しい正常なノードに置き換えられます。

## ID 管理 {#identity-management}

>[!NOTE]
>
>詳しくは、 [セキュリティ — IMSのサポートを参照してください](/help/security/ims-support.md)。

Cloud ServiceとしてのAEMに大きな変更があったのは、AdobeIDを完全に統合して作成者層にアクセスすることです。

これには、ユーザーとユーザーグループを管理するために [Adobe管理コンソール](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用する必要があります。 ユーザーアカウントを使用すると、Adobeプロファイル情報はAdobeIdentity Managementシステム(IMS)に一元化され、すべてのクラウドサービスで共有されるので、ユーザーはの製品やサービスにアクセスできます。 AEMへのアクセスを割り当てると、ユーザーアカウントはAEMでCloud Serviceとして（以前と同様）参照できます。例えば、AEMセキュリティユーザーインターフェイスからロールと権限を定義する場合などです。

これにより、次の利点が得られます。

* AdobeIdentity Managementシステム(IMS)を使用して、すべてのAdobeクラウドアプリケーションに対してシングルサインオンを提供する。

* ユーザーの環境設定は、AEMの特定の各インスタンスに対してローカルのままCloud Serviceとして使用します。

## オーサリングユーザーインターフェイス {#authoring-user-interface}

>[!NOTE]
>
>詳しくは、 [基本処理](/help/sites-cloud/authoring/getting-started/basic-handling.md) (Basic Handling)を参考にしてください。

オーサリングユーザーインターフェイス(UI)の基本原則は、サイトとアセットの両方に関し、過去にAEMを使用したことのある人には非常になじみ深いものです。

主な違いは、UIが完全にタッチ対応であることです。従来のUIは使用できなくなりました。 そうしないと、基本は変更されず、わずかな変更だけが表示されます。

## AEM Sites {#aem-sites}

Cloud ServiceとしてのAdobe Experience Manager Sitesは、AEMコンテンツ管理システムの機能とAEM Digital Asset Managementを組み合わせることで、コンテンツ主導のパーソナライズされた体験を顧客に提供できます。

詳しくは、「サイトの [変更点の概要](/help/sites-cloud/sites-cloud-changes.md)」を参照してください。

## AEM Assets {#aem-assets}

Cloud ServiceオファーとしてのAdobe Experience Managerアセットは、デジタルアセット管理とダイナミックメディアの処理を高速かつ影響を与えるだけでなく、常に最新で常に利用可能で、常に学習可能なシステム内で次世代のスマート機能（AI/MLなど）を利用できる、クラウドネイティブのSaaSソリューションです。

アセットの提供には、次世代のアセット処理をクラウドで実行し、高パフォーマンスのアセット取り込みと検索を行う機能が含まれます。

詳しくは、「 [概要とCloud Serviceとしてのアセットの概要](/help/assets/overview.md)」を参照してください。

## Adobe Experience Manager as a Cloud Service の理解 {#getting-to-know-aem-as-cloud-service}

詳しくは、次のセクションを参照してください。

* [Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)
* Adobe Experience Manager as a Cloud Service の[アーキテクチャ](/help/core-concepts/architecture.md)
* [AEM as a Cloud Service の主な変更点（リリースノート）](/help/release-notes/aem-cloud-changes.md)
* [ AEM Sites as a Cloud Service の主な変更点](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service の主な変更点](/help/assets/assets-cloud-changes.md)
* [AEM Assets as a Cloud Service の概要](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/overview.html)
