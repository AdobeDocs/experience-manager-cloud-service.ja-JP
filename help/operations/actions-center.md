---
title: アクションセンター
description: アクションセンターを活用して、インシデントやその他の重要な情報への処理を効果的に行います。
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 7a05b5f19d9d59ad438c18ce510e0c54acd49a93
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 95%

---

# アクションセンター {#actions-center}

AEM as Cloud Service では、即時対応を求められる重大なインシデントが発生した場合のアクションセンターのメール通知や、最適化のための事前対応の推奨事項が送信されます。 例えば、ブロックされたキューや、期限が切れる一連の資格情報などです。すべてのアクションセンター通知タイプは[下の表](#supported-notification-types)で確認でき、この表には時間の経過と共に項目が追加されます。

アクションセンターのメール通知を受信したら、クリックすると AEM as a Cloud Service のアクションセンターとポップアップが開き、顧客が実行すべきアクションを説明する追加のコンテキストが表示されます。

アクションセンターは、クリックした通知に関する情報を表示するだけでなく、現在および過去に受信した一連の通知を表示して管理するための拠点としても機能します。 <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

アクションセンターに表示される通知には、大きく分けて 2 つのカテゴリがあります。

1. 運用上のインシデント - イベントが発生した場合に表示され、通常、迅速な解決が求められます （ブロックされたキューの解決など）。
1. プロアクティブなレコメンデーション - アドビでは、顧客が近い将来に実行するべきアクションについてレコメンデーションを提供しています。 例えば、非推奨の UI の参照を停止する、など

アクションセンターで現在サポートされている通知について詳しくは、[以下の表](#supported-notification-types)を参照してください。

アクションセンターから特定のプログラムと環境を選択することができ、これにより選択した範囲のフィルタリングが行われます。

## 設定 {#configuration}

受信するアクションセンターのメール通知を設定するには、[通知プロファイル](/help/journey-onboarding/notification-profiles.md)の説明に従って、「インシデント通知 - Cloud Service」製品プロファイルおよび「事前通知 - Cloud Service」製品プロファイルを作成します。また、組織の適切な Adobe ID をこれらのプロファイルに割り当てます。 これにより、管理者は、これらの電子メール通知を受信する対象ユーザーを決定できます。

>[!NOTE]
>アクションセンターの電子メール通知は組織レベルで機能するので、サブスクライバーは、すべてのプログラムとプログラム内の環境に関する通知を受信します。

## 詳細なユーザーフロー {#detailed-user-flow}

メールをクリックすると、アクションセンターに移動し、クリックした通知のコンテキストを示すポップアップと、是正措置の実行方法を説明する追加情報へのリンクが表示されます。 また、次の場所からアクションセンターに直接アクセスすることもできます：[https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/)。アクションセンターでは、関連するプログラムおよび環境を選択できます。

![インシデントの詳細](/help/operations/assets/incident-details.png)

**詳細情報**&#x200B;リンクをクリックすると、ユーザーはこの記事に移動し、以下の[サポートされている通知タイプの表](#supported-notification-types)で通知タイプを参照して、実行するアクションに関するガイダンスを確認できます。

アクションセンターには、その他の最近の通知がリスト表示されます。 通知を確認することで組織がタスクを認識していることをアドビに伝えるために、または後で是正措置が実行されたときに通知を解決するために、アクションリストの使用をお勧めします。

![通知リスト](/help/operations/assets/notification-list.png)

ほとんどの場合、問題を解決するために必要なすべてのコンテキストがポップアップに表示されます。 ただし、アドビサポートに質問がある場合は、ポップアップの&#x200B;**サポートへのお問い合わせ**&#x200B;リンクをクリックします。 表示されたフォームで質問を説明して送信し、サポートチケットを作成することができます。このフォームには、アドビサポートエンジニアが関連コンテキストを把握できるように、特定の通知への参照も含まれます。

![サポートへのお問い合わせ 1](/help/operations/assets/contact-support1.png)

![サポートへのお問い合わせ 2](/help/operations/assets/contact-support2.png)

すべてのサポートチケットと同様に、[Adobe Admin Console の「サポートケース」タブ](https://helpx.adobe.com/jp/enterprise/using/support-for-enterprise.html)に表示されるので、追跡したり、コメントを追加したりできます。

![Admin Console サポート](/help/operations/assets/admin-console-support.png)

## 表示される通知 {#which-notification}

AEM as a Cloud Service の通知には複数のタイプがありますが、次の表に示すように、アクションセンターにはサブセットのみが表示されます。

| 通知タイプ | 説明 | 設定方法 | センターに表示されるかどうか |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| 運用上のインシデント | 即時対応を求められる重大なインシデント | 「インシデント通知 - Cloud Service」製品プロファイルに割り当てられたユーザー | X |
| プロアクティブなレコメンデーション | 予定しておくべき最適化 | 「事前通知 - Cloud Service」製品プロファイルに割り当てられたユーザー | X |
| Cloud Manager のパイプラインステータス | パイプラインのステータスに関する情報 | ビジネスオーナー、プログラムマネージャーまたはデプロイメントマネージャーの役割を持ち、[Experience Cloud の環境設定](https://experience.adobe.com/preferences)で「その他」チェックボックスがオンになっているユーザー。[通知](/help/implementing/cloud-manager/notifications.md)を参照してください。 |                           |

## サポートされている通知タイプ {#supported-notification-types}

アクションセンターで現在サポートされている通知タイプを次の表に示します。 現在、通知を使用できるのは実稼動環境に限定されています。

| 通知タイプ | 関連する製品プロファイル | 是正措置 |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ブロックされたレプリケーションキュー | インシデント | キューのブロックを解除するには、[レプリケーションドキュメント](/help/operations/replication.md#troubleshooting)の手順に従ってください。 |
| 無効な永続 GraphQL クエリ | インシデント | [永続 GraphQL クエリのトラブルシューティングドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html?lang=ja)を参照して、無効な GraphQL クエリを修正する |
| オリジンでのトラフィックスパイク | インシデント | オリジンアラートでのデフォルトのトラフィックスパイクよりも低いしきい値でトリガーされるレート制限トラフィックフィルタールールを設定して、オリジンを保護します。  チュートリアルを参照しているトラフィックフィルタールールのドキュメントの[トラフィックルールを使用した DoS および DDoS 攻撃のブロック](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules)の節を参照してください。 |
| トリガーされた CDN トラフィックフィルタールール | インシデント | 一致するトラフィックフィルタールールが攻撃を反映し、サイトがそのトラフィックをブロックしていない場合は、トラフィックフィルタールールをブロックモードで設定してサイトを保護します。チュートリアルを参照しているトラフィックフィルタールールのドキュメントの[トラフィックフィルタールール（WAF ルールを含む）による web サイトの保護](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites)の節を参照してください。 |
| Splunk ログ転送エラー | インシデント | Splunk エンドポイントが機能し、AEM Cloud Service 環境からアクセスできることを確認します。ログ転送について詳しくは、[Splunk ログ転送ドキュメント](/help/implementing/developing/introduction/logging.md#splunk-logs)を参照してください。トラブルシューティングに関するサポートが必要な場合や、ログ設定を変更する必要がある場合は、アドビにサポートチケットを発行してください。 |
| ページに多数のノードが含まれる | 事前対応 | ページ内のノードの合計数を減らします。 [ページの複雑さのドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/pcx)を参照してください | |
| 実行中のワークフローインスタンスの数が多い | 事前対応 | 不要になった実行中のワークフローを終了します。 詳しくは、[パージジョブの設定](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance)方法を参照してください |               |
| S2S 証明書の有効期限が切れます | 事前対応 | [サーバーサイド API のアクセストークンの生成ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)で資格情報を更新する方法を説明します。 | 高い接続数 | 事前対応 | 接続プーリングについて詳しくは、[高度なネットワークとの接続プーリングに関するドキュメント](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)を参照してください |
| 非推奨（廃止予定）のサービスユーザーマッピング | 事前対応 | 新しい Sling サービスユーザーマッピング形式の使用方法について詳しくは、[Sling サービスユーザーマッピングとサービスユーザー定義のベストプラクティス](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition)を参照してください |
| 高い接続数 | 事前対応 | 接続プーリングについて詳しくは、[高度なネットワークに関するドキュメント](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)を参照してください |  |
| ユーザーがカスタムグループに直接追加される | 事前対応 | ユーザーを関連する IMS グループに追加し、これらの IMS グループを AEM グループのメンバーとして追加する必要があります。 [IMS のベストプラクティス](/help/security/ims-support.md)に合わせて調整します | |
| JCR コンテンツが欠落しています | 事前対応 | 欠落している JCR コンテンツノードを追加します。 [Assets のコンテンツバリデーターのドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv)を参照してください | |
| 完了したワークフローがパージされない | 事前対応 | 90 日以上経過したワークフローインスタンスをパージして、ワークフローインスタンスの数を最小限に抑え、パフォーマンスを向上させます。 詳しくは、[メンテナンスタスクの設定](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance)方法を参照してください | |
| ページに Sling リソースが欠落している | 事前対応 | 欠落している Sling リソースタイプノードを追加します。 [Assets のコンテンツバリデーターのドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-pattern-detection/table-of-contents/acv)を参照してください | |
| 処理に時間のかかるクエリ | 事前対応 | [JCQ クエリチートシート](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf?lang=ja)で推奨されているように、正しいインデックス定義を定義して、処理に時間のかかるクエリを修正します | |
| インデックスのないクエリ | 事前対応 | インデックスを使用しないクエリの実行を回避します -[インデックス作成に関するドキュメントへのリンク](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/indexing) | |
| 非推奨ライブラリのアラート | 事前対応 | [ 非推奨の記事 ](/help/release-notes/deprecated-removed-features.md) で説明しているように、アプリケーションのセキュリティとパフォーマンスを維持するために、非推奨パッケージを推奨される新しいバージョンに置き換えます | |
| 非推奨の設定アラート | 事前対応 | [ 廃止の記事 ](/help/release-notes/deprecated-removed-features.md) で説明しているように、アプリケーションのセキュリティとパフォーマンスを維持するために、非推奨（廃止予定）の設定を、推奨される新しいバージョンに置き換えます |
