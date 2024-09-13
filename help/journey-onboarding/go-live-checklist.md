---
title: 公開チェックリスト
description: AEM as a Cloud Serviceとの運用開始を成功させるために必要な、すべての要素について説明します。
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 56%

---

# 公開チェックリスト {#Go-Live-Checklist}

このアクティビティのリストを確認して、運用開始をスムーズかつ正常に実行できるようにします。

* 機能テストと UI テストを含んだエンドツーエンドの実稼動パイプラインを実行して、AEM 製品エクスペリエンスを&#x200B;**常に最新**&#x200B;に保ちます。詳しくは、次のリソースを参照してください。
   * [AEM バージョンのアップデート](/help/implementing/deploying/aem-version-updates.md)
   * [カスタム機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI テスト](/help/implementing/cloud-manager/ui-testing.md)
* AEM 6.5 から移行する場合は、コンテンツを本番環境に移行し、テスト用のステージングで関連するサブセットが使用可能であることを確認する必要があります。
   * AEM の DevOps ベストプラクティスでは、コードは開発環境から実稼動環境に移行しますが、コンテンツは実稼動環境から下方に移行します。
* コードとコンテンツの凍結期間のスケジュールを設定します。
   * [移行に必要なコードおよびコンテンツの凍結タイムライン](#code-content-freeze)の節も参照してください。
* 最終コンテンツ追加を実行します。
* Dispatcher設定を検証します。
   * Dispatcherのローカルでの設定、検証、シミュレーションを容易にするローカルのDispatcher バリデーターを使用します。
      * [ ローカルのDispatcher ツールを設定します ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites)。
   * 仮想ホストの設定を慎重に確認します。
      * 最も簡単な（デフォルトの）解決策は、`/dispatcher/src/conf.d/available_vhostsfolder` の仮想ホストファイルに `ServerAlias *` を含めることです。 これにより、製品機能テスト、Dispatcher キャッシュの無効化、クローンで使用されるホストエイリアスが機能するようになります。
      * ただし、`ServerAlias *` を指定できない場合は、カスタムドメインに加えて、少なくとも次の `ServerAlias` エントリが許可される必要があります。
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* CDN、SSL および DNS を設定します。
   * 独自の CDN を使用している場合は、適切なルーティングを設定するためのサポートチケットを入力します。
      * 詳しくは、CDN ドキュメントの[顧客 CDN で AEM 管理 CDN を参照する](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)の節を参照してください。
      * CDN ベンダーのドキュメントに従って、SSL および DNS を設定します。
   * 追加の CDN を使用しない場合は、次のドキュメントに従って、SSL と DNS を管理します。
      * SSL 証明書の管理
         * [SSL 証明書の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
         * [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * カスタムドメイン名（DNS）の管理
         * DNS カットオーバーによって予期しない問題が発生しないようにしてください。 実稼動インスタンスを接続するテストサブドメインを作成してから、運用を開始し、一連の UAT テストを行います。 そのため、ドメインがexample.comの場合は、サブドメイン test.example.comを作成して、実稼動環境に適用することができます。 ドメインの UAT テスト中に、適切なリンクリダイレクト、キャッシュ、Dispatcher設定などを探します。
         * [カスタムドメイン名の概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [カスタムドメイン名を追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * DNS レコードに設定されている TTL を必ず検証してください。
      * TTL は、DNS レコードがキャッシュに残ってから、サーバーに更新を要求するまでの時間です。
      * TTL が非常に大きい場合、DNS レコードの更新が反映されるまでに時間がかかります。
* ビジネス要件とビジネス目標を満たすパフォーマンステストとセキュリティテストを実行します。
   * ステージング環境でテストを実行します。  規模は実稼動と同じです。
   * 開発環境は、ステージング環境や実稼動環境とは異なるサイズに設定されます。
* カットオーバーし、新しいデプロイメントやコンテンツの更新を行わずに実際の運用開始が確実に実行されるようにします。
* Admin Consoleユーザー通知プロファイルを作成します。 詳しくは、[通知プロファイル](/help/journey-onboarding/notification-profiles.md)を参照してください
* トラフィックフィルタールールを設定して、web サイト上で許可されないトラフィックを制御することを検討します。
   * レート制限トラフィックフィルタールールは、DDoS 攻撃に対する効果的なツールになる可能性があります。 WAF（Web Application Firewall）ルールと呼ばれる特別なカテゴリのトラフィックフィルタールールには、別のライセンスが必要です。
   * いくつかの[推奨スタータールール](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules)については、ドキュメントを参照してください。

運用開始中にタスクを再調整する必要がある場合は、いつでもリストを参照できます。
