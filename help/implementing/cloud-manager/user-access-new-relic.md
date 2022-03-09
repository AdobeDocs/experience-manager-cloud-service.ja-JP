---
title: New Relic One
description: AEM as a Cloud Serviceの New Relic One Application performance Monitoring(APM) サービスと、そのアクセス方法について説明します。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 2%

---


# New Relic One {#user-access}

AEM as a Cloud Serviceの New Relic One Application performance Monitoring(APM) サービスと、そのアクセス方法について説明します。

## はじめに {#introduction}

Adobeは、アプリケーションの監視、可用性、パフォーマンスに大きく重点を置いています。 この目標を達成するために、AEMas a Cloud Serviceは標準製品の一部としてカスタム New Relic One 監視スイートにアクセスし、チームがAEMのas a Cloud Serviceシステムと環境のパフォーマンス指標を最大限に可視化できるようにします。

このドキュメントでは、AEMas a Cloud Service環境で有効になる New Relic One Application Performance Monitoring(APM) 機能を説明し、パフォーマンスをサポートし、AEM as a Cloud Serviceを最大限に活用できるようにします。

## 機能 {#transaction-monitoring}

New Relic One APM for AEM as a Cloud Serviceには、多くの機能があります。

* 専用の New Relic One アカウントへの直接アクセス (Adobe・サポートが管理 )

* Instrumented New Relic One APM エージェントは、外部の依存関係やデータベースを含む、行番号を持つ正確なメソッド呼び出しを表示します。

* インフラストラクチャレベルの監視とアプリケーション (Adobe Experience Manager) の監視の主要指標を組み合わせることで、全体的なパフォーマンスを最適化

* AEMas a Cloud Serviceの JMX Mbeans とヘルスチェックを New Relic Insights 指標内に直接公開し、アプリケーションスタックのパフォーマンスとヘルス指標を詳細に調べることができます。

## New Relic One へのアクセス {#accessing-new-relic}

AEM as a Cloud Service Program に関連付けられた New Relic One サブアカウントにアクセスするには、次の手順に従います。

1. リクエストを開くには、Admin Consoleの「サポート」タブにアクセスしてください。
1. リクエストには、プログラム ID の詳細と、New Relic へのアクセスを必要とするユーザーのリストを含めます。
   * すべてのユーザーのフルネームと有効な E メールアドレスを指定する必要があります。

ドキュメントを参照します。 [AEM Support Portal for Service のExperience Cloud](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) チケットを開く方法の詳細は、を参照してください。

アクセス権が与えられると、New Relic は各ユーザーに確認メールを送信します。これにより、ユーザーは設定プロセスを完了し、サインインできます。

元のアカウント確認 E メールが見つからない場合は、次の手順に従います。

1. New Relic のログインページ ( ) に移動します。 [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. 選択 **パスワードを忘れた場合**.

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. アカウントの電子メールアドレスを入力し、 **リセットリンクを送信**.

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic は、アカウントを確認するためのリンクを含む電子メールをユーザーに送信します。

電子メールまたはパスワードのエラーメッセージが原因でサインアッププロセスが完了し、アカウントにログインできない場合は、 [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>New Relic からメールが届かない場合は、次の手順に従います。
>
>* 以下を確認します。 [スパムフィルター](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* 該当する場合、 [メール許可リストに New Relic を追加](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* どちらの提案もお役に立たない場合は、サポートチケットに関するフィードバックをお寄せください。Adobeサポートチームがお手伝いします。


### メールの確認 {#verify-email}

ログイン中に電子メールを確認するように求められる場合は、電子メールが複数のアカウントに関連付けられていることを意味します。 これにより、アクセスするアカウントを選択できます。

電子メールアドレスを確認しない場合、New Relic は、電子メールアドレスに関連付けられた最新のユーザーレコードを使用してログインを試みます。 ログイン時に電子メールが確認されないようにするには、 **自分を記憶する** 」チェックボックスを使用して、ログイン画面に表示されます。

詳しくは、 [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Exceptions {#exceptions}

AEM as a Cloud Serviceは、New Relic One APM ソリューションのみを提供し、アラート、ログ、API 統合のサポートは提供しません。

AEMas a Cloud Serviceプログラムの New Relic One 製品に関するその他のヘルプやガイダンスについては、 [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## New Relic アカウントに関するよくある質問 (FAQ) {#faqs}

### Adobeは New Relic One で何を監視しますか？ {#adobe-monitor}

Adobeは、New Relic One の Java プラグインを介してAEMのas a Cloud Serviceのオーサー、パブリッシュ、プレビュー（利用可能な場合）サービスを監視します。 Adobeは、カスタムの New Relic One APM テレメトリと、非実稼働および実稼働のAEMas a Cloud Service環境での監視を可能にします。

New Relic One アカウントは、プライマリAdobeが管理するアカウントに添付され、複数のアプリケーションがそのアカウントにレポートされます。AEMas a Cloud Service環境ごとに 3 つ

* 環境ごとにオーサーサービス用の 1 つのアプリケーション
* 環境ごとにパブリッシュサービス用の 1 つのアプリケーション（ゴールデンパブリッシュを含む）
* 環境ごとに 1 つのプレビューサービス用アプリケーション

注 :

* 各アプリケーションは、1 つのライセンスキーを使用します。
* AEMas a Cloud Service環境は、1 つの New Relic One アカウントにのみレポートされます。
* New Relic One の両方の完全な監視指標とイベントは、7 日間保持されます。

### New Relic One クラウドサービスデータにアクセスできるのは誰ですか？ {#access-new-relic-cloud}

チームの最大 10 名のメンバーに対してフル読み取りアクセス権が付与されます。 読み取りアクセスには、New Relic One エージェントが収集したすべての APM 指標が含まれます。

### カスタム SSO 設定はサポートされていますか？ {#custom-sso}

カスタム SSO 設定は、Adobeがプロビジョニングした New Relic One アカウントではサポートされていません。

### 既にオンプレミスの New Relic サブスクリプションを持っている場合はどうすればよいですか？ {#new-relic-subscription}

New Relic One は、New Relic の新しい観測可能なプラットフォームで、Adobeサポートとチームが指標とイベントを 1 か所で監視、監視、表示できます。

New Relic One を使用すると、すべてのサービスとホストのデータにアクセスできるすべてのアカウントを 1 つのビューで検索し、視覚化できます。

Adobeサポートは、New Relic One などの社内ツールをサービスの一部として使用してAEMas a Cloud Serviceアプリケーションを監視しますが、New Relic は引き続きオンプレミスのサービスとインフラストラクチャに活用できます。 AdobeNew Relic One アカウントと顧客が管理する New Relic アカウントの両方からデータを視覚化できます。

>[!NOTE]
>
>New Relic One 内で両方のデータセットを表示するには、ユーザーが適切な権限を持ち、両方のアカウントに同じログイン手法を使用する必要があります (AdobeNew Relic One および顧客が管理する New Relic アカウント )。
