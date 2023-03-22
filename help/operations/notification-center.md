---
title: 通知センター
description: 通知センターを活用して、インシデントやその他の重要な情報に関する便利な対応を取る
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 通知センター {#notification-center}

>[!NOTE]
>この機能はリリースされていません。

設定が完了すると、AEM as aCloud Serviceは、顧客が行動を起こす必要のある重要な情報に関する通知を送信します。 通知の例としては、ブロックされたキューや、期限が切れる一連の資格情報などがあります。 すべての通知タイプは、 [下の表](#current-notification-types)、は時間の経過と共に展開されます。 通知は、電子メールと通知ウィジェットの下の新しいエントリの両方を通じて受信されます。通知ウィジェットには、Adobe Experience Cloud全体の右上隅にあるベルのアイコンをクリックするとアクセスできます。 通知設定を構成できます。

通知を受け取ったら、クリックしてAEMas a Cloud Serviceの通知センターを開き、顧客が実行すべき推奨アクションを説明する追加のコンテキストを表示するポップアップを表示できます。

クリックした通知に関する情報が表示されるほか、通知センターは現在および古い通知のセットを表示および管理できるハブとして機能します。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

通知には、大まかに次の 2 つのカテゴリがあります。

1. インシデント — イベントが発生しました。通常、迅速な解決が必要です。 例えば、ブロックされたキューの解決
1. 事前対応 —Adobeは、近い将来にお客様が取るべきアクションに対する推奨を持っています。 例えば、非推奨の UI の参照を停止する場合は、を指定します。

詳しくは、 [下の表](#current-notification-types) ：現在サポートされている通知用。

通知センター画面から、特定のプログラムと環境を選択できます。このプログラムと環境は、その範囲に対するフィルタリングの効果を持ちます。

## 設定 {#configuration}

次の手順に従って、受信通知を設定できます。

1. 説明に従って、次の製品プロファイルを作成します。 [この記事では、](/help/journey-onboarding/notification-profiles.md)で、組織の適切なAdobeID をこれらのプロファイルに割り当てます。
1. 通知設定を決定します。 [このページ](https://experience.adobe.com/preferences/notification-section)を設定する場合は、Experience Manager配信登録が有効になっていて、 **その他** チェックボックスがオンになっている。 また、E メールセクションを **インスタント通知** したがって、インシデントが発生した直後に通知を受け取ります。

>[!NOTE]
>購読は組織レベルで機能するので、購読者は、プログラム内のすべてのプログラムと環境に関する通知を受け取ります。

## 詳細なユーザーフロー {#detailed-user-flow}

E メールをクリックすると、通知センターに移動し、クリックした通知のコンテキストを示すポップアップと、修正処理の実行方法を説明する追加情報へのリンクが表示されます。

![インシデントの詳細](/help/operations/assets/incident-details.png)

クリック **詳細情報** link は、この記事にユーザーを移動します。この記事では、以下の表で通知を参照できます。この記事では、実行するアクションに関するガイダンスを提供しています。

通知センターには、他の最近の通知のリストが表示されます。 「処理」リストを使用して、組織がタスクを認識していることをAdobeに伝え、後で修正処理が行われた場合に通知を解決するために、通知を確認することをお勧めします。

![通知リスト](/help/operations/assets/notification-list.png)

ほとんどの場合、問題を解決するために必要なすべてのコンテキストが通知に表示されます。 ただし、Adobeサポートに関する質問がある場合は、 **サポートに連絡** リンクをクリックします。 これにより、質問を説明し、サポートチケットを作成するためのフォームが表示されます。このフォームには、Adobeサポートエンジニアが関連するコンテキストを持つように、特定の通知への参照も含まれます。

![サポート 1 に連絡してください](/help/operations/assets/contact-support1.png)

![サポート 2 に連絡してください](/help/operations/assets/contact-support2.png)

すべてのサポートチケットと同様、 [Adobe Admin Consoleの「サポートケース」タブ](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html)を開き、追跡したり、コメントを追加したりできます。

![Admin Consoleサポート](/help/operations/assets/admin-console-support.png)

## 現在の通知タイプ {#current-notification-types}

現在サポートされている通知タイプを次の表に示します

| 通知タイプ | 関連する製品プロファイル | 是正措置 |
|---|---|---|
| ブロックされたレプリケーションキュー | インシデント | キューのブロックを解除するには、 [レプリケーションドキュメント](/help/operations/replication.md#troubleshooting) |
| S2S 証明書の期限が切れています | 事前対応 | で資格情報を更新する方法を説明します。 [サーバー側 API ドキュメントのアクセストークンの生成](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
