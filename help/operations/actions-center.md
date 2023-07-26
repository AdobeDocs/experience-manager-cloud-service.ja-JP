---
title: アクションセンター
description: アクションセンターを活用して、インシデントやその他の重要な情報に対する便利な対応を実行
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 083aa4b893b58102b3a0bf68c4dd3b4c003b48f6
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 27%

---

# アクションセンター {#actions-center}

>[!NOTE]
>この機能はリリースされていません。

AEM as aCloud Serviceは、即時の対応が必要な重大なインシデントが発生した場合に、アクションセンターに電子メール通知を送信し、最適化に関する事前の推奨事項を伝えます。 例えば、ブロックされたキューや、期限が切れる資格情報のセットなどです。アクションセンターの通知タイプの完全なセットは、 [下の表](#supported-notification-types)は、時間の経過と共に展開されます。

アクションセンターの電子メール通知を受け取ったら、クリックしてAEMas a Cloud Serviceのアクションセンターを開き、顧客が実行するアクションを説明する追加のコンテキストを表示するポップアップを表示できます。

アクションセンターは、クリックしたばかりの電子メール通知に関する情報を表示するだけでなく、現在の通知と古い通知のセットを表示および管理できるハブとして機能します。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

アクションセンターに表示される通知には、大まかに 2 つのカテゴリがあります。

1. 運用上のインシデント - イベントが発生した場合に表示され、通常、迅速な解決が求められます（ブロックされたキューの解決など）。
1. プロアクティブなレコメンデーション - アドビでは、顧客が近い将来に実行するべきアクションについてレコメンデーションを提供しています。例えば、非推奨の UI の参照を停止する、など

詳しくは、 [下の表](#supported-notification-types) ：アクションセンターで現在サポートされている通知に関する情報です。

アクションセンターから、特定のプログラムと環境を選択し、その範囲に対するフィルタリングの効果を持たせることができます。

## 設定 {#configuration}

受信アクションセンターの電子メール通知を設定するには、製品プロファイルを作成します。説明 [この記事では、](/help/journey-onboarding/notification-profiles.md)( インシデント通知 —Cloud Serviceおよびプロアクティブ通知 —Cloud Service)。 また、組織の適切なAdobeID をこれらのプロファイルに割り当てます。 これにより、管理者は、これらの電子メール通知を受け取る資格を持つユーザーを決定できます。

>[!NOTE]
>アクションセンターの電子メール通知は組織レベルで機能し、購読者は、それらのプログラム内のすべてのプログラムと環境に関する通知を受け取るようになります。

## 詳細なユーザーフロー {#detailed-user-flow}

電子メールをクリックすると、アクションセンターに移動し、クリックした通知のコンテキストを示すポップアップと、修正処理の実行方法を説明する追加情報へのリンクが表示されます。

![インシデントの詳細](/help/operations/assets/incident-details.png)

クリック **詳細情報** link は、この記事にユーザーを移動し、通知タイプを [サポートされている通知タイプの表](#supported-notification-types) 以下に、実行するアクションに関するガイダンスを示します。

アクションセンターには、他の最近の通知の一覧が表示されます。 「処理」リストを使用して、組織がタスクを認識していることをAdobeに伝える通知を確認し、後で修正処理がおこなわれた場合に通知を解決することをお勧めします。

![通知リスト](/help/operations/assets/notification-list.png)

ほとんどの場合、問題を解決するために必要なすべてのコンテキストがポップアップに表示されます。 ただし、Adobeサポートに関する質問がある場合は、 **サポートへの問い合わせ** リンクをクリックします。 これにより、質問を説明し、サポートチケットを作成するためのフォームが表示されます。このチケットには、特定の通知への参照も含まれ、Adobeサポートエンジニアが関連するコンテキストを持つようになります。

![サポートへのお問い合わせ 1](/help/operations/assets/contact-support1.png)

![サポートへのお問い合わせ 2](/help/operations/assets/contact-support2.png)

すべてのサポートチケットと同様に、[Adobe Admin Console の「サポートケース」タブ](https://helpx.adobe.com/jp/enterprise/using/support-for-enterprise.html)に表示されるので、追跡したり、コメントを追加したりできます。

![Admin Console サポート](/help/operations/assets/admin-console-support.png)

## 表示される通知 {#which-notification}

AEM as a Cloud Serviceには複数のタイプの通知がありますが、次の表に示すように、アクションセンターにはサブセットのみが表示されます。

| 通知タイプ | 説明 | 設定方法 | アクションセンターに表示 |
|---|---|---|---|
| 運用上のインシデント | 即時対応を求められる重大なインシデント | 「インシデント通知 —Cloud Service」製品プロファイルに割り当てられたユーザー | X |
| プロアクティブなレコメンデーション | 予定しておくべき最適化 | 「Proactive Notification - Product」製品プロファイルに割り当てられたCloud Service | X |
| Cloud Manager のパイプラインステータス | パイプラインのステータスに関する情報 | ビジネスオーナー、プログラムマネージャーまたはデプロイメントマネージャーの役割を持ち、[Experience Cloud の環境設定](https://experience.adobe.com/preferences)で「その他」チェックボックスが選択されているユーザー、 [ここで説明](/help/implementing/cloud-manager/notifications.md). |   |

## サポートされている通知タイプ {#supported-notification-types}

次の表に、アクションセンターで現在サポートされている通知の種類を示します。 通知は、現在、実稼動環境に限られています。

| 通知タイプ | 関連する製品プロファイル | 是正措置 |
|---|---|---|
| ブロックされたレプリケーションキュー | インシデント | キューのブロックを解除するには、[レプリケーションドキュメント](/help/operations/replication.md#troubleshooting)の手順に従ってください。 |
| S2S 証明書の有効期限が切れます | 事前対応 | [サーバーサイド API のアクセストークンの生成ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)で資格情報を更新する方法を説明します。 |

