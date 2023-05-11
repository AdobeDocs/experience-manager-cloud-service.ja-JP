---
title: 通知センター
description: 通知センターを活用して、インシデントやその他の重要な情報に関する便利な対応を取る
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 3aa753fb5cc5130ced7e9baafde63e8825394dce
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# 通知センター {#notification-center}

>[!NOTE]
>この機能はリリースされていません。

AEM as aCloud Serviceは、即時の対応が必要な重大なインシデントが発生した場合に通知を送信し、最適化に関する事前の推奨事項を提示します。 例えば、ブロックされたキューや、期限が切れる一連の資格情報などです。すべての通知タイプは、 [下の表](#supported-notification-types)：時間の経過と共に展開されます。

これらの通知は、電子メールと通知ウィジェットの両方で受け取るように設定できます。通知ウィジェットにアクセスするには、Adobe Experience Cloud全体の右上隅にあるベルのアイコンをクリックします。

通知を受け取ったら、クリックしてAEMas a Cloud Serviceの通知センターを開き、顧客が実行するアクションを説明する追加のコンテキストを表示するポップアップを表示できます。

クリックした通知に関する情報が表示されるほか、通知センターは現在の通知と過去の通知のセットを表示および管理できるハブとして機能します。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知センターには、通知の大まかなカテゴリが 2 つあります。

1. オペレーショナルインシデント — イベントが発生しました。通常、迅速な解決が必要です。 例えば、ブロックされたキューの解決などです。
1. 事前の推奨事項 —Adobeは、近い将来に顧客がおこなう必要のあるアクションに対する推奨事項を持っています。 例えば、非推奨の UI の参照を停止する場合は、を指定します。

詳しくは、 [下の表](#supported-notification-types) ：現在サポートされている通知用。

通知センターから、特定のプログラムと環境を選択できます。このプログラムと環境は、その範囲に対するフィルタリングの効果を持ちます。

## 設定 {#configuration}

次の手順に従って、受信通知を設定します。

1. 説明に従って、次の製品プロファイルを作成します。 [この記事では、](/help/journey-onboarding/notification-profiles.md)」で、組織の適切なAdobeID をこれらのプロファイルに割り当てます。 これにより、管理者は、これらの通知を受け取る資格を持つユーザーを決定できます。
1. 前の手順で割り当てられた各ユーザーは、通知の受信方法を設定できます。 の [Experience Cloud設定ページ](https://experience.adobe.com/preferences/notification-section)、Experience Manager購読が有効になっていること、および **運用インシデント** および **事前の推奨事項** アプリ内列と E メール列の両方にチェックボックスがオンになっている（下図を参照）。 また、E メールセクションを **インスタント通知** したがって、インシデントが発生するとすぐに通知が受信されます。

![購読を設定](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>通知は組織レベルで機能するので、購読者は、プログラム内のすべてのプログラムと環境に関する通知を受け取ります。

## 詳細なユーザーフロー {#detailed-user-flow}

E メールをクリックすると、通知センターに移動し、クリックした通知のコンテキストを示すポップアップと、修正処理の実行方法を説明する追加情報へのリンクが表示されます。

![インシデントの詳細](/help/operations/assets/incident-details.png)

クリック **詳細情報** link は、この記事にユーザーを移動します。この記事では、以下の表で通知を参照できます。この記事では、実行するアクションに関するガイダンスを提供しています。

通知センターには、他の最近の通知のリストが表示されます。 「処理」リストを使用して、組織がタスクを認識していることをAdobeに伝え、後で修正処理が行われた場合に通知を解決するために、通知を確認することをお勧めします。

![通知リスト](/help/operations/assets/notification-list.png)

ほとんどの場合、問題を解決するために必要なすべてのコンテキストが通知に表示されます。 ただし、Adobeサポートに関する質問がある場合は、 **サポートに連絡** リンクをクリックします。 これにより、質問を説明し、サポートチケットを作成するためのフォームが表示されます。このフォームには、特定の通知への参照も含まれ、Adobeサポートエンジニアが関連するコンテキストを持つようになります。

![サポート 1 に連絡してください](/help/operations/assets/contact-support1.png)

![サポート 2 に連絡してください](/help/operations/assets/contact-support2.png)

すべてのサポートチケットと同様、 [Adobe Admin Consoleの「サポートケース」タブ](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)を開き、追跡したり、コメントを追加したりできます。

![Admin Consoleサポート](/help/operations/assets/admin-console-support.png)

## どの通知が表示されますか？ {#which-notification}

AEM as a Cloud Serviceには複数のタイプの通知がありますが、次の表に示すように、通知センターにはサブセットのみが表示されます。

| 通知タイプ | 説明 | 設定方法 | 通知センターに表示 |
|---|---|---|---|
| 運用インシデント | 迅速な対応が必要な重大なインシデント | 「インシデント通知 —Cloud Service」製品プロファイルに割り当てられたユーザー。「オペレーショナルインシデント」チェックボックス ( [Experience Cloud設定](https://experience.adobe.com/preferences) | X |
| 事前の推奨事項 | 計画する必要がある最適化 | 製品プロファイル「Proactive Notification - Production」に割り当てられたユーザー。「Proactive recommendations」チェックボックス ( [Experience Cloud設定](https://experience.adobe.com/preferences) | X |
| Cloud Manager のパイプラインステータス | パイプラインの状態に関する情報 | ビジネスオーナー、プログラムマネージャーまたはデプロイメントマネージャーの役割を持つユーザー（で「その他」チェックボックスを選択） [Experience Cloud設定](https://experience.adobe.com/preferences) |  |

## サポートされる通知タイプ {#supported-notification-types}

次の表に、現在サポートされている通知タイプを示します。

| 通知タイプ | 関連する製品プロファイル | 是正措置 |
|---|---|---|
| ブロックされたレプリケーションキュー | インシデント | キューのブロックを解除するには、 [レプリケーションドキュメント](/help/operations/replication.md#troubleshooting) |
| S2S 証明書の期限が切れています | 事前対応 | で資格情報を更新する方法を説明します。 [サーバー側 API ドキュメントのアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

