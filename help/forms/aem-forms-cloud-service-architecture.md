---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service のアーキテクチャ
description: ' [!DNL AEM Forms] a s a Cloud Service のアーキテクチャを理解し、プラットフォームの拡張性、回復性、パフォーマンスの側面について学習します。'
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 100%

---


# [!DNL AEM] as a Cloud Service のアーキテクチャ {#architecture}

[!DNL AEM Forms] as a Cloud Service は、すべてのお客様に対してデプロイメントアーキテクチャを標準化し、アーキテクチャに関する考慮事項からお客様を完全に解放することを目的としています。例えば、新しい AEM as a Cloud Service アーキテクチャは、永続化のためにマイクロカーネルの概念に依存していますが、お客様はどのマイクロカーネルから選択するかについて心配する必要はありません。オーサー側とパブリッシュ側の両方で使用されるマイクロカーネルは、[!DNL AEM Cloud Service] 独自のもので、それ以外の場合、オンプレミスインストールのお客様は利用できません。

AEM as a Cloud Service は、可変数の AEM インスタンスを持つ動的アーキテクチャを備えています。開発、ステージ、実稼動およびデモンストレーション環境を提供します。AEM インスタンスの管理（Cloud Manager）、ユーザーと認証の管理（Admin Console および IMS（Adobe ID 管理）システム）、キャッシュの設定（Fastly CDN）およびクラウドネイティブの開発環境に使用するツールを提供します。アーキテクチャについて詳しくは、「[ [!DNL Adobe Experience Manager as a Cloud Service] のアーキテクチャの概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=ja)」を参照してください。

## Cloud Manager {#cloud-manager}

Cloud Manager は、[AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=ja) にとって不可欠なコンポーネントです。[!DNL AEM Forms] as a Cloud Service の新しい各テナントは、Cloud Manager にアクセスできるように最初にプロビジョニングされます。Cloud Manager は、お客様の運用および開発者のペルソナのための単一のエントリーポイントです。AEM のプログラムと環境を管理できる場所です。Cloud Manager は、AEM as a Cloud Service の主要コンポーネントを作成および設定できるセルフサービスポータルとして進化しました。

* プログラムの作成と管理
* プログラム内での AEM 環境の作成と管理
* 顧客コードと設定を特定の環境にデプロイするためのパイプラインの作成と管理
* これらのコンポーネントに関する重要なライフサイクルイベント（製品の更新など）の通知
Cloud Manager について詳しくは、「[Adobe Cloud Manager について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=ja)」および「[Cloud Manager の概要](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=ja)」を参照してください。

## ユーザーと認証 {#users-and-authentication}

AEM as a Cloud Service の Admin Console では、AEM インスタンスと、Adobe Identity Management System（IMS）ベースの認証をサポートしてます。Admin Console を使用すると、管理者がすべての Experience Cloud ユーザーを一元的に管理できます。AEM as a Cloud Service インスタンスに関連付けられている製品プロファイルにユーザーとグループを割り当てることができます。その結果、ユーザーとグループはその特定のインスタンスにログインできるようになります。ユーザー、認証および AEM as a Cloud Service インスタンスへのアクセスについて詳しくは、[ [!DNL Adobe Experience Manager] as a Cloud Service の IMS サポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja#introduction)を参照してください。

標準的な [!DNL AEM Forms] プロジェクトには、様々なペルソナが関わっています。[!DNL AEM Forms] as a Cloud Service インスタンスにログインしたら、組織やプロジェクトに適用可能なペルソナについて [Admin Console でユーザーを追加し](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=ja)、[ユーザーを組み込みのグループに割り当てて](forms-groups-privileges-tasks.md)、必要な権限を付与できます。

[!DNL AEM Forms] as a Cloud Services インスタンスで使用できる様々な組み込みの [!DNL AEM Forms] 専用ユーザーグループおよび権限について詳しくは、[設定、ユーザー、役割、グループ](forms-groups-privileges-tasks.md)を参照してください。

## 開発者エクスペリエンス {#developer-experience}

AEM as a Cloud Service をサポートする新しいアーキテクチャには、開発者のエクスペリエンス全体に対するいくつかの重要な変更が伴います。開発者エクスペリエンスの変更の主な目標の 1 つは、既存のカスタムコードをほとんど変更せずに、できるだけ早く AEM as a Cloud Service に移行できるようにすることです。

## クラウド開発 {#cloud-development}

AEM as a Cloud Service 環境で既存のコードをスムーズに実行するためのガイドラインを以下に示します。

* コードと設定を、関連する Cloud Manager プログラムの Git リポジトリーに保存します。コードの管理と CI／CD との統合が簡単になります。
* アプリケーションのコードと設定を、ベースライン [!DNL AEM Forms] 画像と互換性のあるものにします。最新の API を使用すると、より高速で安全なアプリケーションを構築できます。
* Cloud Manager 環境に関連付けられた Cloud Manager パイプラインを使用して、アプリケーションを構築およびデプロイします。[!DNL AEM Forms] as a Cloud Service の最新機能とバグ修正を環境に導入するのに役立ちます。
* カスタムアプリケーションが、パイプラインで適用されるすべてのコード品質、セキュリティおよびパフォーマンスゲートを通過するようにしてください。これにより、安全でパフォーマンスの高いアプリケーションを構築し、顧客エクスペリエンスを向上させることができます。一部のチェックをスキップする場合は、常に Cloud Manager UI を使用できます。
このプロセスは、一般にクラウドファースト開発と呼ばれます。また、[!DNL AEM Forms] as a Cloud Service には、保留中のコードおよび設定変更をクラウドで試す前の迅速な開発をサポートする SDK も用意されています。
以前は AEM QuickStart に含まれていたインターフェイスの一部は、AEM as a Cloud Service 環境のユーザーには使用できなくなりました。例えば、OSGI バンドルおよび関連する設定を管理する Web コンソールなどです。CRXDE Lite コンテンツリポジトリーブラウザーは、非実稼動環境タイプでのみアクセス可能になります。開発者が必要とする Web コンソール機能のサブセットは、特に診断とステータスの目的に関して、新しい開発者コンソールを介して利用できるようになります。
また、開発者にとって最も一般的な要件の 1 つは、様々な環境のログファイルにすばやくアクセスすることです。[!DNL AEM Cloud Service] を使用すると、オーサーノードとパブリッシュノードに含まれる様々なノードのログファイルが、Cloud Manager を通じて（ダウンロード可能なファイルの形式または API 経由で）利用できるようになります。コードとコンテンツが明確に分離されているので、開発者は特定のプロセスを活用して、デプロイメントの一環としてコンテンツを更新できます。可変コンテンツの典型的なユースケースは次のとおりです。
* 顧客プロジェクトの一部となる標準の「デフォルト」コンテンツ（フォルダー、テンプレート、ワークフローなど）
* 検索インデックスの定義
* ACL と権限
* サービスのユーザーおよびユーザーグループ
開発環境を設定し、[CI／CD パイプラインを設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=ja)し、環境に[コードをデプロイする](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja)方法を学習します。

## ローカル開発 {#local-development}

[!DNL AEM Forms] as a Cloud Service 環境を設定する場合は、開発環境、ステージング環境および実稼動環境を設定します。さらに、迅速な反復と開発を行うために、ローカル開発環境を設定します。AEM SDK と [!DNL AEM Forms] アドオン機能アーカイブをダウンロードして設定し、ローカルの [!DNL Forms] as a Cloud Service 開発環境を設定できます。手順について詳しくは、[ローカル開発環境の設定](setup-local-development-environment.md)を参照してください。

## デバッグ {#debugging}

AEM as a Cloud Service は、セルフサービスのスケーラブルなクラウドインフラストラクチャ上で実行します。AEM 開発者は、ビルドとデプロイから、実行中の AEM アプリケーションの詳細情報の取得まで、AEM as a Cloud Service の様々な側面を理解し、デバッグする必要があります。詳しくは、[AEM as a Cloud Service のデバッグ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=ja)を参照してください。
