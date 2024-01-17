---
title: New Relic One
description: AEM as a Cloud Service の New Relic One アプリケーションパフォーマンスモニタリング（APM）サービスと、そのサービスへのアクセス方法について説明します。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 85%

---


# New Relic One {#user-access}

AEM as a Cloud Service の New Relic One アプリケーションパフォーマンスモニタリング（APM）サービスと、そのサービスへのアクセス方法について説明します。

## はじめに {#introduction}

アドビは、アプリケーションのモニタリング、可用性、パフォーマンスを重視しています。AEM as a Cloud Service では、標準製品の一部としてカスタム New Relic One モニタリングスイートにアクセスできるため、お客さまのチームが AEM as a Cloud Service システムと環境のパフォーマンス指標を最大限に可視化できるようになります。

このドキュメントでは、AEM as a Cloud Service 環境で有効になっている New Relic One Application Performance Monitoring（APM）機能へのアクセスを管理し、パフォーマンスをサポートし、AEM as a Cloud Service を最大限に活用する方法について説明します。

新しい実稼動プログラムを作成すると、AEM as a Cloud Serviceプログラムに関連付けられたNew Relic Oneサブアカウントが自動的に作成されます。 [このサブアカウントを有効化する必要があります](#activate-sub-account) データの取り込みを開始するために。

## 機能 {#transaction-monitoring}

AEM as a Cloud Service 用の New Relic One APM には、多くの機能があります。

* 専用の New Relic One アカウントへの直接アクセス

* 外部の依存関係やデータベースを含む、行番号のある正確なメソッド呼び出しを表示する New Relic One APM エージェントを実装。

* インフラストラクチャレベルのモニタリングおよびアプリケーション（Adobe Experience Manager）のモニタリングからの主要指標を組み合わせることで、全体的なパフォーマンス最適化を実現

* AEM as a Cloud Service の JMX Mbeans とヘルスチェックを New Relic Insights 指標内に直接公開し、アプリケーションスタックのパフォーマンスとヘルス指標を詳細に調査。

## New Relic Oneサブアカウントをアクティブ化 {#activate-sub-account}

新しく作成したプログラムの場合は、New Relic Oneサブアカウントが作成されます。 ただし、データを取り込むには、アクティブ化する必要があります。 これは、自動的にはおこなわれません。 サブアカウントをアクティブ化するには、次の手順に従います。

>[!NOTE]
>
>のユーザー **ビジネスオーナー** または **デプロイメントマネージャー** New Relic Oneサブアカウントを管理するには、の役割をログインする必要があります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. 次の日： **[マイプログラム](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 画面で、New Relic Oneユーザーを管理するプログラムをタップまたはクリックします。

1. の下部に **環境** 「プログラムの概要」ページのカードで、省略記号ボタンをクリックし、「 **New Relicをアクティベート**.

   ![ユーザーを管理](assets/newrelic-activate-sub-account.png)

   * プログラムの&#x200B;**環境**&#x200B;画面の上部にある省略記号ボタンから「**ユーザーを管理**」オプションにアクセスすることもできます。

1. [パイプラインの実行](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) を有効にします。

サブアカウントが無効化されると、データの取り込みはおこなわれません。

## New Relic One ユーザーの管理 {#manage-users}

次の手順に従って、AEM as a Cloud Service プログラムに関連付けられた New Relic One サブアカウントのユーザーを定義します。

>[!NOTE]
>
>New Relic One ユーザーを管理するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーがログインしている必要があります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. New Relic One ユーザーを管理するプログラムをクリックします。

1. プログラムの概要ページの&#x200B;**環境**&#x200B;カードの下部にある省略記号ボタンをクリックし、「**ユーザーを管理**」を選択します。

   ![ユーザーを管理](assets/newrelic-manage-users.png)

   * プログラムの&#x200B;**環境**&#x200B;画面の上部にある省略記号ボタンから「**ユーザーを管理**」オプションにアクセスすることもできます。

1. 「**New Relic ユーザーを管理**」ダイアログで、追加するユーザーの氏名を入力し、「**追加**」ボタンをクリックします。追加するすべてのユーザーについて、この手順を繰り返します。

   ![ユーザーを追加](assets/newrelic-add-users.png)

1. New Relic One ユーザーを削除するには、ユーザーを表す行の右端にある削除ボタンをクリックします。

1. 「**保存**」をクリックして、ユーザーを作成します。

ユーザーが定義されると、New Relic は、アクセス権を付与した各ユーザーに確認メールを送信します。これにより、ユーザーは設定プロセスを完了し、サインインできるようになります。

>[!NOTE]
>
>New Relic One ユーザーを管理している場合は、アクセスできるように自分自身もユーザーとして追加する必要があります。New Relic One にアクセスするには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;であるだけでは十分ではありません。自分自身もユーザーとして作成する必要があります。

## New Relic One ユーザーアカウントの有効化 {#activate-user-account}

[New Relic One ユーザーの管理](#manage-users)のプレビューセクションで説明しているように、New Relic One ユーザーアカウントが作成されると、New Relic はそれらのユーザーに指定されたアドレスに確認メールを送信します。これらのアカウントを使用するには、ユーザーはまずパスワードをリセットして New Relic のアカウントを有効にする必要があります

次の手順に従って、New Relic ユーザーとしてアカウントを有効にします。

1. New Relic からのメールに記載されているリンクをクリックします。これにより、ブラウザーが開き、New Relic ログインページが表示されます。

1. New Relic ログインページで、「**パスワードを忘れた場合**」を選択します。

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 確認メールを受信したメールアドレスを入力し、「**リセットリンクを送信**」を選択します。

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載されたメールが送信されます。

New Relic から確認メールが届かない場合は、[トラブルシューティングの節](#troubshooting)を参照してください。

## New Relic One へのアクセス {#accessing-new-relic}

[New Relic アカウントを有効](#activate-account)にすると、Cloud Manager を介して、または直接、New Relic One にアクセスできます。

Cloud Manager を介して New Relic One にアクセスするには：

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. New Relic One にアクセスするプログラムをクリックします。

1. プログラムの概要ページの&#x200B;**環境**&#x200B;カードの下部にある省略記号ボタンをクリックし、「**New Relic を開く**」を選択します。

   ![ユーザーの管理](assets/newrelic-access.png)

   * プログラムの&#x200B;**環境**&#x200B;画面の上部にある省略記号ボタンから New Relic にアクセスすることもできます。

1. 開いた新しいブラウザータブで、New Relic One にログインします。

New Relic One に直接アクセスするには：

1. [`https://login.newrelic.com/login`](https://login.newrelic.com/login) にある New Relic のログインページに移動します。

1. New Relic One にログインします。

### メールの確認 {#verify-email}

New Relic One へのログイン中にご利用のメールを確認するように求められた場合は、メールが複数のアカウントに関連付けられていることを意味します。これにより、アクセスするアカウントを選択できます。

メールアドレスを確認しない場合、New Relic は、メールアドレスに関連付けられた最新のユーザーレコードを使用してログインを試みます。ログインする度にメールが確認されないようにするには、ログイン画面の「**このアカウントを記憶する**」チェックボックスをクリックします。

詳細なヘルプについては、[AEM サポートポータル](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)を介してサポートチケットを開いてください。

## New Relic One User Access のトラブルシューティング {#troubleshooting}

[New Relic One ユーザーの管理](#manage-users)の節で説明しているように New Relic One ユーザーとして追加され、元のアカウント確認メールが見つからない場合は、次の手順に従ってください。

1. [`login.newrelic.com/login`](https://login.newrelic.com/login) にある New Relic のログインページに移動します。

1. 「**パスワードを忘れた場合**」を選択します。

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. アカウントの作成に使用したメールアドレスを入力し、「**リセットリンクを送信**」を選択します。

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載されたメールが送信されます。

新規登録プロセスを完了し、メールまたはパスワードのエラーメッセージが原因でアカウントにログインできない場合は、[Admin Console](https://adminconsole.adobe.com/) からサポートチケットをログに記録します。

New Relic からメールが届かない場合は、次の操作を実行します。

* [スパムフィルター](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/)を確認します。
* 該当する場合、[メール許可リストに New Relic を追加](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist)してください。
* どちらの提案も効果がない場合は、サポートチケットに関するフィードバックを提供してください。アドビサポートチームがお手伝いします。

## 制限事項 {#limitations}

New Relic One にユーザーを追加する場合は、次の制限が適用されます。

* 最大 30 人のユーザーを追加できます。ユーザーの最大数に達した場合は、新しいユーザーを追加できるように、ユーザーを削除します。
* New Relic に追加されたユーザーは、**制限付き**&#x200B;のタイプになります。詳しくは、[New Relic のドキュメントを参照してください。](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)
* AEM as a Cloud Service は New Relic One APM ソリューションのみを提供し、アラート、ログ、API 統合のサポートは提供していません。

>[!NOTE]
>
>New Relic Oneサブアカウントで 90 日以上アクティビティが検出されなかった場合、APM エージェントは停止します。
>
>同じ手順 ( [New Relic Oneサブアカウントをアクティブ化](#activate-sub-account) の節を参照して、New Relic Oneサブアカウントを再アクティブ化してください。

AEM as a Cloud Serviceプログラム向けのNew Relic One製品に関するその他のヘルプまたはガイダンスについては、 [AEMサポートポータル。](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)

## New Relic One に関するよくある質問（FAQ） {#faqs}

### アドビは New Relic One で何をモニタリングしますか？ {#adobe-monitor}

アドビは、New Relic One の Java プラグインを介して AEM as a Cloud Service のオーサー、パブリッシュ、プレビュー（利用可能な場合）サービスをモニタリングします。アドビは、カスタムの New Relic One APM テレメトリと、実稼動および実稼動以外の AEM as a Cloud Service 環境でのモニタリングを有効にします。

New Relic One アカウントは、アドビが管理するプライマリアカウントに接続されており、複数のアプリケーションがレポートを作成します。AEM as a Cloud Service 環境ごとに 3 つあります。

* 環境ごとにオーサーサービス用の 1 つのアプリケーション
* 環境ごとにパブリッシュサービス用の 1 つのアプリケーション（ゴールデンパブリッシュを含む）
* 環境ごとにプレビューサービス用の 1 つのアプリケーション

メモ：

* 各アプリケーションは、1 つのライセンスキーを使用します。
* AEM as a Cloud Service 環境は、1 つの New Relic One アカウントにのみレポートします。
* 両方の New Relic One の完全なモニタリング指標およびイベントは、7 日間保持されます。

### アドビは New Relic Oneからのアラート通知を送信しますか？ {#alerting-new-relic}

アドビは、監視の目的でのみ New Relic One へのアクセスを提供します。お客様への警告や内部の運用アラートには使用しません。インシデントに関する通知は、[ユーザー通知プロファイル](/help/journey-onboarding/notification-profiles.md)を使用して送信されます。

### New Relic One Cloud Service のデータへは、誰がアクセスできますか？ {#access-new-relic-cloud}

最大 30 人のチームメンバーに完全な読み取りアクセスが許可されます。読み取りアクセスには、New Relic One エージェントによって収集されたすべての APM 指標が含まれます。

### カスタム SSO 設定はサポートされていますか？ {#custom-sso}

カスタム SSO 設定は、アドビがプロビジョニングした New Relic One アカウントではサポートされていません。

### 既にオンプレミスの New Relic サブスクリプションがある場合はどうなりますか？ {#new-relic-subscription}

New Relic One は、New Relic の新しい観測可能なプラットフォームであり、アドビサポートとお客様のチームが指標とイベントをすべて 1 か所で観測、監視、表示できます。

New Relic One を使用すると、ユーザーがアクセスできるすべてのアカウントを検索し、すべてのサービスとホストからのデータを 1 つのビューで視覚化できます。

アドビサポートは、サービスの一部として New Relic One やその他の社内ツールを使用して AEM as a Cloud Service アプリケーションを監視しますが、お客様のチームは引き続き New Relic をオンプレミスのホストサービスとインフラストラクチャに活用できます。Adobe New Relic One アカウントと顧客管理の New Relic アカウントの両方からのデータを視覚化できるようになります。

>[!NOTE]
>
>New Relic One 内で両方のデータセットを表示するには、ユーザーが適切な権限を持ち、両方のアカウント（Adobe New Relic One と顧客管理の New Relic アカウント）に同じログイン方法を使用する必要があります。

### New Relic One アカウントの APM エージェントが停止しました。なぜですか？ {#deactivated}

90 日以上アクティビティが検出されなかった場合、[APM エージェントは停止します](#limitations)。同じ手順 ( [New Relic Oneサブアカウントをアクティブ化](#activate-sub-account) の節を参照して、New Relic Oneサブアカウントを再アクティブ化してください。
