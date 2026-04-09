---
title: New Relic One
description: AEM as a Cloud Service の New Relic One アプリケーションパフォーマンスモニタリング（APM）サービスと、そのサービスへのアクセス方法について説明します。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 090a890e25ee45fb8a46255c097f243a24b00756
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 55%

---


# New Relic One {#user-access}

AEM as a Cloud Service の New Relic One アプリケーションパフォーマンスモニタリング（APM）サービスと、そのサービスへのアクセス方法について説明します。

## New Relic One について {#introduction}

アドビは、アプリケーションのモニタリング、可用性、パフォーマンスを重視しています。AEM as a Cloud Service には、New Relic One モニタリングへのアクセスが含まれており、チームは標準製品の一部としてシステムと環境のパフォーマンス指標を包括的に可視化できます。

この記事では、AEM as a Cloud Service環境でNew Relic One Application Performance Monitoring （APM）機能へのアクセスを管理する方法の概要を説明します。 これらの機能を効果的に管理することで、最適なパフォーマンスをサポートし、AEM as a Cloud Service のメリットを最大限に活用できます。

新しい実稼動プログラムが作成されると、AEM as a Cloud Service プログラムに関連付けられた New Relic One サブアカウントが自動的に作成されます。データの取り込みを開始するには、[このサブアカウントをアクティベートする必要があります](#activate-sub-account)。

## 機能 {#transaction-monitoring}

AEM as a Cloud Service 用の New Relic One APM には、多くの機能があります。

* 専用のNew Relic Oneアカウントに直接アクセスできます。

* 外部の依存関係やデータベースを含む、行番号を持つ正確なメソッド呼び出しを表示するNew Relic One APM エージェントを実装しました。

* インフラレベルのモニタリングとAdobe Experience Manager（アプリケーション）モニタリングの主要指標を組み合わせることで、包括的なパフォーマンス最適化を実現します。

* Cloud Manager パイプライン実行、AEMのアップグレード、およびコード復元操作の自動変更トラッカー。 これらのトラッカーを利用することで、New Relic Oneで直接デプロイメントとアプリケーションパフォーマンスの変更を関連付けることができます。

## New Relic One サブアカウントをアクティベート {#activate-sub-account}

新しく作成したプログラムの場合は、New Relic One サブアカウントが作成されます。ただし、データを取り込むには、アクティベートする必要があります。このアクティベーションは自動ではありません。サブアカウントをアクティベートするには、次の手順に従います。

>[!NOTE]
>
>New Relic One サブアカウントを管理するには、**ビジネスオーナー**&#x200B;の役割を持つユーザーがログインする必要があります。

**New Relic One サブアカウントをアクティブ化するには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
   1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
   1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、New Relic One ユーザーを管理するプログラムをクリックします。
1. 左側のメニューの&#x200B;**サービス**&#x200B;で、![&#x200B; データアイコンまたは環境アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**&#x200B;をクリックします。
1. 環境ページの右上隅付近で、![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**New Relicをアクティブ化**&#x200B;をクリックします。

   ![New Relicのライセンス認証](/help/implementing/cloud-manager/assets/new-relic/new-relic-activate.png)

1. [同じ環境でパイプライン &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)を実行して正常に完了し、サブアカウントのアクティベーションを完了します。

サブアカウントをアクティベート解除すると、データの取り込みは行われません。

## New Relic One ユーザーを管理 {#manage-users}

AEM as a Cloud Service プログラムに関連付けられているNew Relic One サブアカウントのユーザーを定義できます。

>[!NOTE]
>
>New Relic One ユーザーを管理するには、**ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;の役割を持つユーザーがログインしている必要があります。

**New Relic One ユーザーを管理するには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
   1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
   1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、New Relic One ユーザーを管理するプログラムをクリックします。
1. 左側のメニューの&#x200B;**サービス**&#x200B;で、![&#x200B; データアイコンまたは環境アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**&#x200B;をクリックします。
1. 環境ページの右上隅付近で、![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**ユーザーの管理**&#x200B;をクリックします。

   ![New Relic ユーザーの管理](/help/implementing/cloud-manager/assets/new-relic/new-relic-manage-users.png)

1. **New Relic ユーザーの管理** ダイアログボックスで、次の操作を行います。

   * 追加するユーザーの姓と名を入力します
   * 関連する電子メールアドレスを入力
   * ![&#x200B; アイコンを追加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **追加**&#x200B;をクリックします。 追加するユーザーごとに、この手順を繰り返します。
   * ![削除アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)をクリックして、ユーザーを削除します。

   ![ユーザーを追加](assets/newrelic-add-users.png)

1. 「**保存**」をクリックします。

ユーザーが定義されると、New Relicは各ユーザーに確認メールを送信します。 そこから、アクティベーションプロセスを完了してログインします。

>[!NOTE]
>
>New Relic One ユーザーを管理している場合は、自分自身もユーザーとして追加する必要があります。 **ビジネスオーナー**&#x200B;または&#x200B;**デプロイメントマネージャー**&#x200B;であるだけでは、New Relic Oneへのアクセス権を持つことはできません。

## New Relic One ユーザーアカウントをアクティベート {#activate-user-account}

New Relic One ユーザーアカウントが作成されると、[New Relic One ユーザーの管理](#manage-users)の説明に従って、New Relicは指定されたアドレスに確認メールを送信します。 これらのアカウントを使用するには、ユーザーはまずパスワードをリセットして New Relic のアカウントを有効にする必要があります

**New Relic One ユーザーアカウントをアクティベートするには：**

1. New Relic からのメールに記載されているリンクをクリックします。

1. New Relic ログインページで、「**パスワードを忘れた場合**」をクリックします。

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 確認メールを受信したメールアドレスを入力し、「**リセットリンクを送信**」を選択します。

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載されたメールが送信されます。

New Relic から確認メールが届かない場合は、[トラブルシューティングの節](#troubshooting)を参照してください。

## New Relic Oneを開く {#accessing-new-relic}

[New Relic アカウントをアクティベートしたら](#activate-account)、Cloud Manager経由または直接New Relic Oneを開くことができます。

**Cloud Manager経由でNew Relic Oneを開くには：**

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
   1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
   1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、New Relic Oneを開くプログラムをクリックします。
1. 左側のメニューの&#x200B;**サービス**&#x200B;で、![&#x200B; データアイコンまたは環境アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **環境**&#x200B;をクリックします。
1. 環境ページの右上隅付近で、![詳細アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)をクリックし、**New Relicを開く**&#x200B;をクリックします。

   ![New Relicを開く](/help/implementing/cloud-manager/assets/new-relic/new-relic-open-new-relic.png)

1. 開いた新しいブラウザータブで、New Relic One にログインします。

**New Relic Oneを直接開くには：**

1. [New Relicのログインページ &#x200B;](https://login.newrelic.com/login)に移動します。

1. New Relic One にログインします。

### メールの検証 {#verify-email}

New Relic One へのログイン中に使用するメールを確認するように求められた場合は、メールが複数のアカウントに関連付けられていることを意味します。アクセスするアカウントを選択できます。

メールアドレスを確認しない場合、New Relic は、メールアドレスに関連付けられた最新のユーザーレコードを使用してログインを試みます。ログインする度にメールが確認されないようにするには、ログイン画面の「**このアカウントを記憶する**」チェックボックスをクリックします。

詳細なヘルプについては、[AEM サポートポータル](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)を介してサポートチケットを開いてください。

## 変更トラッカーの使用 {#change-tracker}

サポートされているパイプラインの実行、Cloud Managerのアップグレード、コードの復元が完了すると、New Relic Oneに変更トラッカーが自動的に送信されます。 これらのトラッカーは、New Relicの&#x200B;**Change Tracking** ビューで変更イベントとして表示され、デプロイメントをアプリケーションパフォーマンス、エラー率、スループットの変化と関連付けることができます。

<!-- See also [Introduction to change tracking](https://docs.newrelic.com/docs/change-tracking/overview/) and [Record and view deployments](https://docs.newrelic.com/docs/apm/apm-ui-pages/events/record-deployments/). -->

### サポートされているパイプラインとワークフロー {#supported-pipelines}

次のCloud Manager パイプラインと最後の2つのワークフロータイプは、New Relic Oneで変更履歴を生成します。

| パイプライン/ワークフロータイプ | 説明 |
|---|---|
| **フルスタック （CI_CD デプロイ）** | フルスタックパイプライン実行： トレースには、パイプライン名と実行IDが含まれます。 |
| **Web階層設定** | Web階層設定パイプライン実行。 トレースには、パイプライン名と実行IDが含まれます。 |
| **フロントエンド** | フロントエンドパイプライン実行： トレースには、パイプライン名と実行IDが含まれます。 |
| **構成** | 設定パイプライン実行。 トレースには、パイプライン名と実行IDが含まれます。 |
| **AEMの更新** | AEMのバージョンのアップグレード： 例えば、バージョン {}からバージョン {}までです。 環境変更イベントが完了すると、トラッカーが作成されます。 |
| **コードの復元** | コードは、特定のリポジトリとブランチから操作を復元します。 |

>[!NOTE]
>
>変更トラッカーは現在、スカイライン環境でのみサポートされています。 スケールアップパイプラインやサービスパックパイプラインなど、スコープ外のパイプラインはトラッカーを生成しません。

### New Relic Oneの変更履歴を見る {#view-change-trackers}

サポートされているパイプラインの実行が完了したら、New Relic Oneで対応する変更トラッカーを表示できます。

**New Relic Oneで変更履歴を表示するには：**

1. [Cloud Manager経由または直接New Relic One](#accessing-new-relic)にアクセスします。
1. **APM &amp; Services**&#x200B;に移動し、関連する環境のアプリケーションを選択します。
1. アプリケーションの概要ページで、チャート上の変更トラッカー指標を探します。 トラッカーにカーソルを合わせると、デプロイメントの詳細が表示されます。

   ![Web トランザクション時間チャートのトラッカー指標の変更](/help/implementing/cloud-manager/assets/new-relic/new-relic-web-transactions-time.png)

1. グラフ内の任意の変更イベントをクリックして、詳細ビューを開きます。

   ![DeepLink URLが強調表示されたデプロイメント属性パネル &#x200B;](/help/implementing/cloud-manager/assets/new-relic/new-relic-deeplink.png) <i>変更イベントの詳細ビュー</i>

   右側の&#x200B;**詳細を変更** パネルには、特に、エンティティ、タイムスタンプ、エポック、カテゴリ、デプロイメント ID、API タイプが表示されます。

   Cloud ManagerがNew Relic Oneに送信する変更トラッカーごとに、右下の&#x200B;**デプロイメント属性** パネルに次の属性が表示されます。

   | 属性 | 説明 |
   |---|---|
   | **バージョン** | パイプライン名と実行IDを含む説明文字列。 |
   | **changelog** | 将来の使用のために予約されています。 |
   | **コミット** | 将来の使用のために予約されています。 |
   | **deepLink** | URLをクリックして、Cloud Managerのパイプライン実行ページにリンクし直します。 |

1. 変更トラッカーの完全なリストを表示するには、左側のサイドバーの&#x200B;**イベント**&#x200B;で、**変更トラッキング**&#x200B;をクリックします。

   **変更イベント** テーブルには、タイムスタンプとバージョンの説明が記載された各デプロイメントが表示されます。

   ![変更イベント テーブルに](/help/implementing/cloud-manager/assets/new-relic/new-relic-change-tracking.png)が表示されたトラッキング オプションの変更

>[!TIP]
>
>**応答時間**&#x200B;や&#x200B;**スループット**&#x200B;など、New Relic Oneのパフォーマンス指標と共に変更履歴を使用します。 これらの指標は、特定のデプロイメントがパフォーマンスのリグレッションや改善を導入したかどうかを特定するのに役立ちます。 デプロイメントの前後の指標を、イベントの変更の詳細ページで直接比較できます。

## New Relic One ユーザーアクセスのトラブルシューティング {#troubleshooting}

[New Relic One ユーザーの管理](#manage-users)で説明しているように New Relic One ユーザーとして追加され、元のアカウント確認メールが見つからない場合は、次のトラブルシューティング手順に従ってください。

**New Relic One ユーザーアクセスのトラブルシューティングを行うには：**

1. [`login.newrelic.com/login`](https://login.newrelic.com/login) にある New Relic のログインページに移動します。

1. 「**[!UICONTROL パスワードを忘れた場合]**」をクリックします。

   ![New Relic ログイン](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. アカウントの作成に使用したメールアドレスを入力し、「**リセットリンクを送信**」を選択します。

   ![メールアドレスを入力](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic から、アカウントを確認するためのリンクが記載されたメールが送信されます。

新規登録プロセスを完了し、メールまたはパスワードのエラーメッセージが原因でアカウントにログインできない場合は、[Admin Console](https://adminconsole.adobe.com/) からサポートチケットをログに記録します。

New Relic からメールが届かない場合は、次の操作を実行します。

* [スパムフィルター](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/)を確認します。
* 該当する場合、[メール許可リストに New Relic を追加](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist)します。
* いずれの提案も役に立たない場合は、サポートチケットに関するフィードバックを提供してください。

## 使用上のメモ {#usage-notes}

* 最大 30 人のユーザーを追加できます。ユーザーの最大数に達した場合は、新しいユーザーを追加できるように、ユーザーを削除します。
* New Relic に追加されたユーザーは、**基本**&#x200B;のタイプになります。詳しくは、[New Relic のドキュメント](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-type/)を参照してください。
* AEM as a Cloud Service は New Relic One APM ソリューションのみを提供し、アラート、ログ、API 統合のサポートは提供していません。

>[!NOTE]
>
>New Relic One サブアカウントで 30 日以上&#x200B;**ユーザーログイン**&#x200B;アクティビティが検出されなかった場合、APM エージェントは停止します。AEM Cloud Service から New Relic にデータは送信されません。*サブアカウントを再アクティブ化するまで、データは再送信されません。*
>
>このドキュメントの [New Relic One サブアカウントのアクティベート](#activate-sub-account)の節と同じ手順に従って、New Relic One サブアカウントを再アクティベートします。

AEM as a Cloud Service プログラムの New Relic One 製品に関する詳細なヘルプまたは追加のガイダンスについては、[AEM サポートポータル](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)からサポートチケットを開いてください。

## よくある質問 {#faqs}

+++**アドビが New Relic One でモニタリングするものは何ですか？**

アドビは、New Relic One の Java プラグインを介して AEM as a Cloud Service のオーサー、パブリッシュ、プレビュー（利用可能な場合）サービスをモニタリングします。アドビは、カスタムの New Relic One APM テレメトリと、実稼動および実稼動以外の AEM as a Cloud Service 環境でのモニタリングを有効にします。

New Relic One アカウントは、アドビが管理するプライマリアカウントに接続されており、複数のアプリケーションがレポートを作成します。AEM as a Cloud Service 環境ごとに 3 つあります。

* 環境ごとにオーサーサービス用の 1 つのアプリケーション
* 環境ごとに `Publish` サービス用の 1 つのアプリケーション（ゴールデンパブリッシュを含む）
* 環境ごとにプレビューサービス用の 1 つのアプリケーション

メモ：

* 各アプリケーションは、1 つのライセンスキーを使用します。
* AEM as a Cloud Service 環境は、1 つの New Relic One アカウントにのみレポートします。
* 両方の New Relic One の完全なモニタリング指標およびイベントは、3 か月間保持されます。

+++

+++**アドビは New Relic Oneからのアラート通知を送信しますか？**

アドビは、監視の目的でのみ New Relic One へのアクセスを提供します。お客様への警告や内部の運用アラートには使用しません。インシデントに関する通知は、[ユーザー通知プロファイル](/help/journey-onboarding/notification-profiles.md)を使用して送信されます。
+++

+++**New Relic One Cloud Service のデータへは、誰がアクセスできますか？**

最大 30 人のチームメンバーに完全な読み取りアクセスが許可されます。読み取りアクセスには、New Relic One エージェントによって収集されたすべての APM 指標が含まれます。
+++

+++**カスタム SSO 設定はサポートされていますか？**

カスタム SSO 設定は、アドビがプロビジョニングした New Relic One アカウントではサポートされていません。
+++

+++**既にオンプレミスの New Relic サブスクリプションがある場合はどうなりますか？**

New Relic One は、New Relic の新しい観測可能なプラットフォームであり、アドビサポートとお客様のチームが指標とイベントをすべて 1 か所で観測、監視、表示できます。

New Relic One を使用すると、ユーザーがアクセスできるすべてのアカウントを検索し、すべてのサービスとホストからのデータを 1 つのビューで視覚化できます。

アドビサポートは、New Relic One やその他のツールを使用して AEM as a Cloud Service を監視しますが、お客様のチームは引き続き New Relic をオンプレミスのサービスとインフラストラクチャに活用できます。Adobe New Relic One アカウントと顧客管理の New Relic アカウントの両方からのデータを視覚化できるようになります。

>[!NOTE]
>
>New Relic One 内で両方のデータセットを表示するには、ユーザーが適切な権限を持ち、両方のアカウント（Adobe New Relic One と顧客管理の New Relic アカウント）に同じログイン方法を使用する必要があります。

+++

+++**New Relic One アカウントの APM エージェントが停止しました。何が起きたのでしょうか？**

30 日以上アクティビティが検出されなかった場合、[APM エージェントは停止します](#limitations)。このドキュメントの [New Relic One サブアカウントのアクティベート](#activate-sub-account)の節と同じ手順に従って、New Relic One サブアカウントを再アクティベートします。
+++
