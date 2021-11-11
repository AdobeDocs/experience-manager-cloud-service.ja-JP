---
title: New Relic へのユーザーアクセス
description: New Relic へのユーザーアクセス
index: false
hide: true
source-git-commit: 22dc38ac4aa736ae5c676cfba16e16b0b3e44936
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# AEM as a Cloud Serviceの New Relic Application Performance Monitoring {#new-relic}

## はじめに {#introduction}

Adobeは、アプリケーションの監視、可用性、パフォーマンスを大きく重視します。 この目標を達成するために、AEMas a Cloud Serviceは、標準製品の一部としてカスタム New Relic 監視スイートにアクセスし、Adobe Experience ManagerのCloud Serviceシステムと環境のパフォーマンス指標を最大限に可視化できるようにします。 この節では、AEMas a Cloud Service環境で有効になる New Relic の監視機能を説明します。これにより、パフォーマンスを向上させ、AEM as a Cloud Serviceを最大限に活用できるようになります。

## AEM New Relic を介したas a Cloud Serviceトランザクション監視 {#transaction-monitoring}

AEM as a Cloud Serviceの New Relic Application Performance Monitoring の主な機能を次に示します。

* 専用の New Relic One アカウントへの直接アクセス (Adobe・サポートが管理 )

* 外部の依存関係やデータベースを含む、行番号を持つ正確なメソッド呼び出しを表示する New Relic APM エージェントが実装されました。

* インフラストラクチャレベルの監視とアプリケーション (Adobe Experience Manager) の監視の主要指標を組み合わせることで、全体的なパフォーマンス最適化を実現。

* AEMas a Cloud Serviceの JMX Mbeans とヘルスチェックを New Relic Insights 指標に直接公開し、アプリケーションスタックのパフォーマンスとヘルス指標を詳細に調べることができます。

## AEMas a Cloud Serviceの New Relic アカウントへのアクセス {#accessing-new-relic}

専用の New Relic アカウントは、カスタマーケアエンゲージメントを通じてAdobeによってプロビジョニングおよび管理されます。 Adobeは、所有者および管理者のままとなり、お客様に代わってアカウントをプロビジョニングし、専用のサブアカウントへのアクセスを提供します。

AEMas a Cloud Serviceプログラムに関連付けられた New Relic サブアカウントにアクセスするには、次の手順を実行します。

* リクエストを開くには、Admin Consoleの「サポート」タブにアクセスしてください。
* チケットに、プログラム ID の詳細と、New Relic へのアクセスを開くようAdobeチームにリクエストするユーザーのリストが含まれていることを確認します。
* すべてのユーザーに、フルネームと有効な E メールアドレスが提供される必要があります。

   >[!NOTE]
   >AEMサポートポータルの詳細については、Experience Cloudのサポートを参照してください。

アクセス権が与えられると、New Relic は各ユーザーに確認メールを送信し、設定プロセスを完了してログインできます。 元のアカウント確認 E メールが見つからない場合は、次の手順に従います。

1. New Relic のログインページ (login.newrelic.com/login) に移動します。

1. 「パスワードを忘れた場合」を選択します。

1. アカウントの電子メールアドレスを入力し、「パスワードを送信」を選択します。

1. New Relic のシステムが電子メールメッセージを返したら、その中のリンクを選択して、アカウントを再度確認します。

   >[!NOTE]
   >New Relic からメールが届かない場合は、次の手順に従います。
   >スパムフィルターを確認します。 該当する場合は、New Relic をメール許可リストに追加します。
   >サポートチケットに関するフィードバックをお送りください。アドビのチームがお手伝いします。

1. 登録プロセスが完了し、電子メールまたはパスワードのエラーメッセージが原因でアカウントにログインできない場合は、Admin Consoleからサポートチケットをお送りください。

ログイン中に電子メールを確認するように求められる場合は、電子メールが複数のアカウントに関連付けられ、ログイン中に電子メールを確認するオプションが与えられます。 これにより、アクセスするアカウントを選択できます。 電子メールアドレスを確認しない場合、New Relic は、電子メールアドレスに関連付けられた最新のユーザーレコードを使用してログインを試みます。 ログイン時に電子メールが確認されないようにするには、ログイン画面の「このアカウントを記憶する」チェックボックスをクリックします。

詳しくは、AEMサポートポータルからサポートチケットを開いてください。

## Exceptions {#exceptions}

AEM as a Cloud Serviceは、New Relic APM ソリューションのみに焦点を当て、アラート、ログ、API 統合機能はサポートしていません。

AEMas a Cloud Serviceプログラムの New Relic 製品に関するその他のヘルプやガイダンスについては、 AEMサポートポータルでサポートチケットを開いてください。

## New Relic アカウントに関するよくある質問 (FAQ) {#faqs}

### Adobeは New Relic で何を監視しますか？ {#adobe-monitor}

Adobeは、New Relic APM Java プラグインを介してAEMのas a Cloud Serviceのオーサー、パブリッシュ、プレビュー（利用可能な場合）サービスを監視します。 Adobeは、カスタムの New Relic APM テレメトリと、非実稼働および実稼働のAEMas a Cloud Service環境での監視を可能にします。 お使いの New Relic アカウントは、プライマリAdobeが管理するアカウントに添付され、複数のアプリケーションがそのアカウントにレポートされます。

AEMas a Cloud Service環境ごとに 3 つ：

* 環境ごとに 1 つの Author サービス用アプリケーション
* 環境ごとにパブリッシュサービス用の 1 つのアプリケーション（ゴールデンパブリッシュを含む）
* 各環境で Preview サービス用の 1 つのアプリケーション各アプリケーションで 1 つのライセンスキーを使用するAEMas a Cloud Service環境は、1 つの New Relic アカウントに対してのみレポートします。 New Relic APM とインフラストラクチャの両方の完全な監視指標とイベントは、7 日間保持されます。

### New Relic のCloud Service・データにアクセスできるユーザー {#access-new-relic-cloud}

チームの最大 10 名のメンバーに対してフル読み取りアクセス権が付与されます。 読み取りアクセスには、New Relic エージェントによって収集されたすべての APM 指標が含まれます。

### カスタム SSO 設定はサポートされていますか？ {#custom-sso}

カスタム SSO 設定は、現在、Adobeがプロビジョニングした New Relic アカウントではサポートされていません。

### 既にオンプレミスの New Relic サブスクリプションがある場合はどうなりますか？ {#new-relic-subscription}

New Relic One と呼ばれる新しい観測可能なプラットフォームを使用すると、Adobeサポートグループとチームは、指標とイベントを 1 か所で監視、監視、表示できます。 New Relic One を使用すると、すべてのサービスとホストのデータにアクセスできるすべてのアカウントを 1 つのビューで検索し、視覚化できます。 Adobeサポートチームは、New Relic や他の社内ツールをサービスの一部として使用してAEMas a Cloud Serviceアプリケーションを監視しますが、New Relic は引き続きオンプレミスのホストサービスとインフラストラクチャに活用できます。 お客様が管理する New Relic アカウントとAdobeの両方からのデータを視覚化できます。

>[!NOTE]
>ユーザーは、適切な権限を持ち、両方のアカウントに同じログイン手法を使用する必要があります (Adobeとお客様が管理する New Relic アカウント )。


