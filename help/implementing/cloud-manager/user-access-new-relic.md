---
title: New Relic One
description: AEM as a Cloud Serviceの New Relic One Application performance Monitoring(APM) サービスと、そのアクセス方法について説明します。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 8ae52afc366c6607cfc806f68bec2069a2e93f94
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 10%

---


# New Relic One {#user-access}

AEM as a Cloud Serviceの New Relic One Application performance Monitoring(APM) サービスと、そのアクセス方法について説明します。

## はじめに {#introduction}

Adobeは、アプリケーションの監視、可用性、パフォーマンスに大きく重点を置いています。 AEM as a Cloud Serviceは、標準製品の一部としてカスタム New Relic One 監視スイートにアクセスし、チームがAEMのas a Cloud Serviceシステムと環境のパフォーマンス指標を最大限に可視化できるようにします。

このドキュメントでは、AEMas a Cloud Service環境で有効になっている New Relic One Application Performance Monitoring(APM) 機能へのアクセスを管理し、パフォーマンスをサポートし、AEM as a Cloud Serviceを最大限に活用する方法について説明します。

新しい実稼働プログラムが作成されると、AEMas a Cloud Serviceプログラムに関連付けられた New Relic One サブアカウントが自動的に作成されます。

## 機能 {#transaction-monitoring}

New Relic One APM for AEM as a Cloud Serviceには、多くの機能があります。

* 専用の New Relic One アカウントへの直接アクセス (Adobe・サポートが管理 )

* Instrumented New Relic One APM エージェントは、外部の依存関係やデータベースを含む、行番号を持つ正確なメソッド呼び出しを表示します。

* インフラストラクチャレベルの監視とアプリケーション (Adobe Experience Manager) の監視の主要指標を組み合わせることで、全体的なパフォーマンスを最適化

* AEMas a Cloud Serviceの JMX Mbeans とヘルスチェックを New Relic Insights 指標内に直接公開し、アプリケーションスタックのパフォーマンスとヘルス指標を詳細に調べることができます。

## New Relic One ユーザーの管理 {#manage-users}

次の手順に従って、AEM as a Cloud Service Program に関連付けられた New Relic One サブアカウントのユーザーを定義します。

>[!NOTE]
>
>のユーザー **ビジネスオーナー** または **デプロイメントマネージャー** の役割は、New Relic One ユーザーを管理するためにログインする必要があります。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. New Relic One ユーザーを管理するプログラムをクリックします。

1. の下部に **環境** 「プログラムの概要」ページで、省略記号ボタンをクリックし、「 **ユーザーを管理**.

   ![ユーザーを管理](assets/newrelic-manage-users.png)

   * また、 **ユーザーを管理** オプション ( **環境** 画面に表示されます。

1. 内 **New Relic ユーザーの管理** ダイアログで、追加するユーザーの姓名を入力し、 **追加** 」ボタンをクリックします。 追加するすべてのユーザに対して、この手順を繰り返します。

   ![ユーザーを追加](assets/newrelic-add-users.png)

1. New Relic One ユーザーを削除するには、ユーザーを表す行の右端にある削除ボタンをクリックします。

1. クリック **保存** をクリックして、ユーザーを作成します。

ユーザーが定義されると、New Relic は、アクセス権を付与された各ユーザーに確認メールを送信し、ユーザーは設定プロセスを完了してログインできます。

>[!NOTE]
>
>New Relic One ユーザーを管理している場合は、アクセス権も持つために、自分自身もユーザーとして追加する必要があります。 は **ビジネスオーナー** または **デプロイメントマネージャー** は New Relic One にアクセスするのに十分ではありません。 ユーザーとしても自分を作成する必要があります。

## New Relic One ユーザーアカウントを有効化 {#activate-account}

プレビューの節で説明されているように、New Relic One ユーザーアカウントが作成されます [New Relic One ユーザーの管理](#manage-users)「 」と入力すると、New Relic は指定したアドレスに確認 E メールを送信します。 これらのアカウントを使用するには、ユーザーはまずパスワードをリセットして New Relic でアカウントをアクティブ化する必要があります。

New Relic ユーザーとしてアカウントをアクティブ化するには、次の手順に従います。

1. New Relic からのメールに記載されているリンクをクリックします。 ブラウザーが開き、New Relic のログインページが表示されます。

1. New Relic ログインページで、「 」を選択します。 **パスワードを忘れた場合**.

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 確認 E メールを受け取った E メールアドレスを入力し、「 」を選択します。 **リセットリンクを送信**.

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載された電子メールが送信されます。

New Relic から確認メールが届かない場合は、 [トラブルシューティングの節を参照してください。](#troubshooting)

## New Relic One へのアクセス {#accessing-new-relic}

一度 [New Relic アカウントを有効化しました。](#activate-account) New Relic One には、Cloud Manager からアクセスすることも、直接アクセスすることもできます。

Cloud Manager を使用して New Relic One にアクセスするには：

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. New Relic One にアクセスするプログラムをクリックします。

1. の下部に **環境** 「プログラムの概要」ページで、省略記号ボタンをクリックし、「 **New Relic を開く**.

   ![ユーザーを管理](assets/newrelic-access.png)

   * また、 **環境** 画面に表示されます。

1. 開いた新しいブラウザータブで、New Relic One にログインします。

New Relic One に直接アクセスするには：

1. New Relic のログインページ ( ) に移動します。 [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. New Relic One にログインします。

### メールの確認 {#verify-email}

New Relic One へのログイン中にメールを確認するように求められた場合は、メールが複数のアカウントに関連付けられていることを意味します。 これにより、アクセスするアカウントを選択できます。

電子メールアドレスを確認しない場合、New Relic は、電子メールアドレスに関連付けられた最新のユーザーレコードを使用してログインを試みます。ログイン時に電子メールが確認されないようにするには、 **自分を記憶する** 」チェックボックスを使用して、ログイン画面に表示されます。

詳しくは、 [AEM Support Portal](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html).

## New Relic One アクセスのトラブルシューティング {#troubleshooting}

New Relic One ユーザーとして追加された場合は、「 」の節で説明されています。 [New Relic One ユーザーの管理](#manage-users) 元のアカウント確認メールが見つからない場合は、次の手順に従います。

1. New Relic のログインページ ( ) に移動します。 [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. 選択 **パスワードを忘れた場合**.

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. アカウントの作成に使用した電子メールアドレスを入力し、「 」を選択します。 **リセットリンクを送信**.

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載された電子メールが送信されます。

電子メールまたはパスワードのエラーメッセージが原因でサインアッププロセスが完了し、アカウントにログインできない場合は、 [Admin Console。](https://adminconsole.adobe.com/)

New Relic からメールが届かない場合：

* [スパムフィルター](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/) を確認します。
* 該当する場合、 [メール許可リストに New Relic を追加](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist) してください。
* どちらの提案もお役に立たない場合は、サポートチケットに関するフィードバックをお寄せください。Adobeサポートチームがお手伝いします。

## 制限事項 {#limitations}

New Relic One にユーザーを追加する場合は、次の制限が適用されます。

* 最大 25 人のユーザーを追加できます。 ユーザーの最大数に達した場合は、新しいユーザーを追加できるように、ユーザーを削除します。
* New Relic に追加されたユーザーは、 **制限** 参照する [詳しくは、 New Relic のドキュメントを参照してください。](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20personals%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Serviceは、New Relic One APM ソリューションのみを提供し、アラート、ログ、API 統合のサポートは提供しません。

AEMas a Cloud Serviceプログラムの New Relic One 製品に関するその他のヘルプやガイダンスについては、 [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## New Relic One に関するよくある質問 (FAQ) {#faqs}

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

最大 10 人のチームメンバーに完全な読み取りアクセスが許可されます。読み取りアクセスには、New Relic One エージェントが収集したすべての APM 指標が含まれます。

### カスタム SSO 設定はサポートされていますか？ {#custom-sso}

カスタム SSO 設定は、Adobeがプロビジョニングした New Relic One アカウントではサポートされていません。

### 既にオンプレミスの New Relic サブスクリプションを持っている場合はどうすればよいですか？ {#new-relic-subscription}

New Relic One は、New Relic の新しい観測可能なプラットフォームで、Adobeサポートとチームが指標とイベントを 1 か所で監視、監視、表示できます。

New Relic One を使用すると、ユーザーがアクセスできるすべてのアカウントを検索し、すべてのサービスとホストからのデータを 1 つのビューで視覚化できます。

Adobeサポートは、New Relic One などの社内ツールをサービスの一部として使用してAEMas a Cloud Serviceアプリケーションを監視しますが、New Relic は引き続きオンプレミスのサービスとインフラストラクチャに活用できます。 AdobeNew Relic One アカウントと顧客が管理する New Relic アカウントの両方からデータを視覚化できます。

>[!NOTE]
>
>New Relic One 内で両方のデータセットを表示するには、ユーザーが適切な権限を持ち、両方のアカウントに同じログイン手法を使用する必要があります (AdobeNew Relic One および顧客が管理する New Relic アカウント )。
