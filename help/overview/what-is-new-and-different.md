---
title: 相違点と新機能 - Adobe Experience Manager as a Cloud Service
description: '相違点と新機能 - Adobe Experience Manager（AEM） as a Cloud Service。 '
translation-type: tm+mt
source-git-commit: 52e8cf1e3fb503c1d222a9543cfc1ddfe87132b6
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 100%

---


# 新機能と相違点 {#what-is-new-and-what-is-different}

長年にわたって、AEM の利用形態は次の 2 とおりでした。

* オンプレミス

* as a Managed Services

これら以前のアプローチと AEM as a Cloud Service には、次の点で本質的な違いがあります。

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
>以下の概要は網羅的なものではなく、基本事項の紹介を目的としています。

>[!NOTE]
>
>オンプレミス版および Managed Services 版について詳しくは、[AEM 6.5](https://helpx.adobe.com/jp/support/experience-manager/6-5.html) のドキュメントセットを参照してください。

## アーキテクチャ {#architecture}

>[!NOTE]
>
>詳しくは、[アーキテクチャ](/help/core-concepts/architecture.md)を参照してください。

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


## AEM のアップデート {#aem-updates}

>[!NOTE]
>詳しくは、[AEM バージョンのアップデート](/help/implementing/deploying/aem-version-updates.md)を参照してください。

AEM as a Cloud Service では、継続的統合および継続的配信（CI／CD）を使用して、プロジェクトが確実に最新の AEM バージョンで稼働できるようになっています。つまり、ユーザーに対するサービスが中断することなく、実稼働インスタンスとステージングインスタンスが AEM の最新バージョンに更新されます。

>[!NOTE]
> 実稼働環境へのアップデートに失敗した場合、Cloud Manager はステージング環境を自動的にロールバックします。これは、アップデート完了後も、ステージング環境と実稼働環境の両方が確実に同じ AEM バージョンに基づくようにするために、自動的におこなわれます。

AEM バージョンのアップデートには、次の 2 種類があります。

* **AEM プッシュアップデート**

   * 毎日リリース可能です。
   * 主に、最新のバグ修正やセキュリティの更新などのメンテナンス作業です。

      変更が定期的に適用されるので影響は増分的で、サービスへの影響が少なくなります。

* **新機能アップデート**

   * 予測可能な月次スケジュールでリリースされます。

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager は、インスタンスに対するすべてのアップデートを制御するので（必須）、AEM as a Cloud Service の継続的アップグレードアプローチに欠かせません。

Cloud Service の新しいバージョンが使用可能になったら、アドビがアップデートをトリガーできます。または、Cloud Manager から提供されるパイプラインを使用して、ユーザーがアプリケーションのアップデートをトリガーすることもできます。

Cloud Manager の役割は次のとおりです。

* AEM プログラムおよび環境の管理に使用されます。

* AEM as a Cloud Service の必須コンポーネントです。Cloud Manager へのアクセス用に最初に新しいテナントがそれぞれプロビジョニングされます。

* 運用および開発スタッフのための単一のエントリポイントになります。

特に、Cloud Manager から作成できる AEM プログラムの数と種類は、次のいずれかに基づいて決定されます。

* 顧客の使用許諾契約

* 内的要因（AEM as a Cloud Service をイネーブルメントやトレーニングに使用する場合）

* 外部主導のプロセス（Adobe.com から開始された体験版利用など）

Cloud Manager は、AEM as a Cloud Service の主要コンポーネントを作成および設定できるセルフサービスポータルとして進化しました。

* 新規プログラムの作成と管理。詳しくは、[プログラムとプログラムの種類について](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)を参照してください。

* これらのプログラム内での AEM 環境の作成と管理。詳しくは、[環境の管理](/help/implementing/cloud-manager/manage-environments.md)を参照してください。

* 顧客コードと関連設定を特定の環境にデプロイするためのパイプラインの作成と管理。詳しくは、[CI／CD パイプラインの設定](/help/implementing/cloud-manager/configure-pipeline.md)を参照してください。

* これらのコンポーネントの重要なライフサイクルイベント（製品アップデートなど）の通知の受信。

現在、Cloud Manager では、次の 3 つの地域で環境を作成できます（その他の地域も今後追加される予定です）。

* 米国（東部）

* EMEA（オランダ）

* APAC（オーストラリア）

>[!NOTE]
>AEM as a Cloud Service で Cloud Manager の使用を開始するには、[Adobe Experience Manager as a Cloud Service へのアクセス](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md)を参照してください。

## オンボーディング {#onboarding}

>[!NOTE]
>
>詳しくは、[オンボーディング](/help/onboarding/home.md)を参照してください。

AEM as a Cloud Service を使用すると、次のように作業の多くの側面がアドビの担当になるので、AEM プロジェクトの開始と管理は簡単になります。

* ベースライン AEM イメージが特定のユースケース向けに最適化されている。

* 手動設定タスクの多くが既に冗長化されている。

また、現在は次の要素もあるので、作業自体が大幅に異なります。

* すべての前提条件（例えば下記のもの）が満たされていることを確認する評価フェーズ：

   * 法的要件

   * 契約

   * 顧客がカスタマイズした既存のコンテンツやコードの技術的要件

* デプロイメント要件：

   * コードのアップデート。旧バージョンの AEM 用に開発された顧客アプリケーションをレビューし、場合によっては更新する必要があります。

   * コンテンツの移行

## 開発 {#developing}

>[!NOTE]
>
>詳しくは、まず[AEM as a Cloud Service の開発ガイドライン](/help/implementing/developing/introduction/development-guidelines.md)と [AEM Sites の開発の手引き - WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)を参照してください。

AEM as a Cloud Service をサポートする新しいアーキテクチャには、開発者のエクスペリエンス全体に対するいくつかの重要な変更が含まれています。AEM as a Cloud Service の主要な目標の 1 つは、（AEM をオンプレミスまたは Adobe Managed Services のコンテキストで使用したことがある）経験豊富な顧客が、カスタマイズしたコードの大部分を書き直さずに、できるだけ迅速に AEM as a Cloud Service に移行できるようにすることです。ただし、若干の調整が必要になる可能性はあります。

### クラウド開発 {#aem-as-a-cloud-service-developing-cloud-development}

既存の AEM アプリケーションを AEM as a Cloud Service 上で動作させるには、次の手順が必要です：

* アプリケーションのコードと設定を、関連する Cloud Manager プログラムの Git コードリポジトリに保存する必要があります。
* アプリケーションのコードと設定は、ベースライン AEM イメージの最新バージョン（日々変更される可能性があります）と互換性がある必要があります。
   * 顧客アプリケーションは、Cloud Manager 環境に関連付けられた Cloud Manager パイプラインを使用して作成およびデプロイする必要があります。
* 顧客アプリケーションは、パイプライン内で実施されるすべてのコード品質ゲート、セキュリティゲート、パフォーマンスゲートに合格する必要があります。
* 顧客アプリケーション用に作成したイメージは、Cloud Manager パイプラインでデプロイする必要があります。

このプロセスは一般にクラウドファースト開発と呼ばれます。所要時間は全体で数 10 分（アプリケーションの複雑さに応じて 20～50 分）と見込まれるので、保留中のコードや設定変更がクラウドで試行される前に、迅速な開発手法を採用する必要があります。

OSGi バンドルとその関連設定を管理する Web コンソール（以前は AEM QuickStart の一部）は、AEM as a Cloud Service 環境のユーザーからは直接アクセスできなくなりました。新しい開発者コンソールを使用すれば、このインターフェイスに読み取り専用モードで引き続きアクセスできます。このコンソールを使用すると、開発者はオーサーサービスまたはパブリッシュサービスの特定のノードを直接選択してログインし、デフォルトでブロックされている領域にアクセスできます。

>[!NOTE]
>
>[OSGi 設定](/help/implementing/deploying/overview.md#osgi-configuration)も参照してください。

開発者にとって、もう 1 つの共通の要件は、様々な環境のログファイルにすばやくアクセスできることです。AEM as a Cloud Service では、オーサーノードとパブリッシュノードに含まれる様々なノードのログファイルが、ダウンロード可能なファイルの形式または API 経由で Cloud Manager を通じて利用できるようになっています。

コードとコンテンツが明確に分離されているので、開発者は、特定のプロセスを使用して、デプロイメントの一環としてコンテンツを更新できます。可変コンテンツの典型的なユースケースは次のとおりです。

* 顧客プロジェクトの一部となる標準的な&#x200B;*デフォルト*&#x200B;コンテンツ（フォルダー、テンプレート、ワークフローなど）

* 検索インデックスの定義

* ACL と権限

* サービスのユーザーおよびユーザーグループ

### ローカル開発 {#aem-as-a-cloud-service-developing-local-development}

迅速な反復と開発をサポートするために、AEM as a Cloud Service のコンテキスト以外で AEM アプリケーションを開発することもできます。このために、次のアーティファクトが開発者に公開されています。

* AEM as a Cloud Service QuickStart：最新 AEM コードベースの `.jar` ベーススタンドアロンインストーラーで、同じ機能と API サーフェスを備えています。

* AEM as a Cloud Service Dispatcher SDK：Dispatcher 設定をローカルにテストおよび検証するためのイメージベースのプロセス

>[!NOTE]
>
>Cloud QuickStar では、AEM Sites および AEM Assets の機能をすべて使用できるわけではありません。この QuickStar は、拡張機能の大部分を開発およびテストできるシンプルなオーサー環境で構成されています。

## 運用とパフォーマンス {#operations-and-performance}

>[!NOTE]
>
>詳しくは、まず[AEM as a Cloud Service でのバックアップと復元](/help/operations/backup.md)、[コンテンツの検索とインデックス作成](/help/operations/indexing.md)、[AEM as a Cloud Service でのメンテナンスタスク](/help/operations/maintenance.md)を参照してください。

AEM as a Cloud Service では、サービスの中断が不要になるように、このような操作は自動化されています。

これらの操作では、

* 多くのタスクが自動化されています。

* 耐障害性と効率性を最大限に高めるために、トポロジーが最適化されています。例えば、バイナリレスレプリケーションがデフォルトになっています。

* キュー、ジョブ、一括処理タスクなどの負荷の高いタスクは、コア AEM インスタンスから移動され、共有および専用のマイクロサービスで処理されるようになりました。

AEM as a Cloud Service の運用も、監視、レポート、警告用の新しいインフラストラクチャでサポートされています。これにより、Adobe SRE（サイトリライアビリティエンジニア）はサービスの健全性をプロアクティブ（予見的）に維持できます。アーキテクチャの様々な要素に様々なヘルスチェックが備わっています。何らかの理由で、アーキテクチャの特定のノードが異常と見なされた場合、そのノードはサービスから削除され、ユーザーへの通知なしで新しい正常なノードに置き換えられます。

## ID 管理 {#identity-management}

>[!NOTE]
>
>詳しくは、[Adobe Experience Manager as a Cloud Service に対する IMS のサポート](/help/security/ims-support.md)を参照してください。

AEM as a Cloud Service の重要な変更の 1 つは、Adobe ID を使用したオーサー層へのアクセスが完全に統合されていることです。

それには、[Adobe Admin Console](https://helpx.adobe.com/jp/enterprise/using/admin-console.html) を使用してユーザーとユーザーグループを管理する必要があります。ユーザープロファイル情報が Adobe Identity Management System（IMS）に一元化されてすべてのクラウドサービスで共有されるので、ユーザーはユーザーアカウントを使用してアドビ製品およびサービスにアクセスできます。AEM へのアクセスを割り当てられると、ユーザーアカウントを（以前と同様）AEM as a Cloud Service で参照して、例えば、AEM セキュリティユーザーインターフェイスから役割と権限を定義できます。

これは次の利点を兼ね備えています。

* Adobe Identity Management System（IMS）の使用で、すべての Adobe クラウドアプリケーションでシングルサインオンが利用可能になる

* ユーザーの環境設定は、AEM as a Cloud Service の個々のインスタンスで引き続きローカルに管理できる

## オーサリングユーザーインターフェイス {#authoring-user-interface}

>[!NOTE]
>
>詳しくは、まず[基本操作](/help/sites-cloud/authoring/getting-started/basic-handling.md)を参照してください。

AEM Sites についても AEM Assets についても、オーサリングユーザーインターフェイス（UI）の基本原則は、これまでに AEM を使用したことがある人にとってはなじみ深いものです。

主な違いは、UI が完全にタッチ対応であることです。クラシック UIは使用できなくなりました。それ以外の点では、基本はそのまま変わらず、見た目のわずかな変更があるだけです。

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service は、AEM コンテンツ管理システムの機能と AEM デジタルアセット管理を組み合わせて、コンテンツ主導のパーソナライズされたエクスペリエンスをユーザーに提供できます。

詳しくは、[AEM Sites as a Cloud Service の主要な変更点](/help/sites-cloud/sites-cloud-changes.md)を参照してください。

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service は、クラウドネイティブな SaaS ソリューションです。企業がデジタルアセット管理と Dynamic Media 操作を迅速かつ効果的におこなうだけでなく、常に最新で常に可用性が高く常に学習可能なシステム内から AI や機械学習などの次世代スマート機能を使用するうえでも役に立ちます。

Assets が提供する機能には、クラウドでの次世代アセット処理やパフォーマンスの高いアセット取り込みおよび検索などがあります。

詳しくは、[AEM Assets as a Cloud Service の概要](/help/assets/overview.md)を参照してください。

## Adobe Experience Manager as a Cloud Service の理解 {#getting-to-know-aem-as-cloud-service}

詳しくは、次のセクションを参照してください。

* [Adobe Experience Manager as a Cloud Service の概要](/help/overview/introduction.md)
* [Adobe Experience Manager as a Cloud Service のアーキテクチャ](/help/core-concepts/architecture.md)
* [AEM as a Cloud Service の主な変更点（リリースノート）](/help/release-notes/aem-cloud-changes.md)
* [ AEM Sites as a Cloud Service の主な変更点](/help/sites-cloud/sites-cloud-changes.md)
* [AEM Assets as a Cloud Service の主な変更点](/help/assets/assets-cloud-changes.md)
* [AEM Assets as a Cloud Service の概要](/help/assets/overview.md)
* [Adobe Experience Manager as a Cloud Service のチュートリアル](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/cloud-service/overview.html)
