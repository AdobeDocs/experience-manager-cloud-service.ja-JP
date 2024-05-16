---
title: 公開チェックリスト
description: AEM as a Cloud Service の運用開始を成功させるために必要なすべての要素について説明します。
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
source-git-commit: 581f075483280e4b33574bfd4cc1cb01b5601440
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

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
* Dispatcher 設定を検証します。
   * Dispatcher のローカルでの設定、検証およびシミュレーションを容易に行えるようにするローカルの Dispatcher バリデーターを使用します。
      * [ローカルの Dispatcher ツールを設定します。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=ja#prerequisites)
   * 仮想ホストの設定を慎重に確認します。
      * 最も簡単な（デフォルトの）解決策は、`/dispatcher/src/conf.d/available_vhostsfolder` 内の仮想ホストファイルに `ServerAlias *` を含めることです。
         * これにより、製品機能テスト、Dispatcher キャッシュの無効化、およびクローンで使用されるホストエイリアスが機能するようになります。
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
         * [SSL 証明書の管理の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * カスタムドメイン名（DNS）の管理
         * DNS カットオーバーによって予期しない問題が発生しないことを確認するには、実稼動インスタンスを接続するテスト用サブドメインを作成してから、運用を開始して一連の UAT テストを行うことをお勧めします。したがって、ドメインが example.com の場合は、サブドメイン test.example.com を作成して、実稼動環境に適用することができます。 ドメインの UAT テスト中に、適切なリンクリダイレクト、キャッシュ、Dispatcher 設定などを探す必要があります。
         * [カスタムドメイン名の概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * DNS レコードに設定されている TTL を必ず検証してください。
      * TTL は、DNS レコードがキャッシュに残ってから、サーバーに更新を要求するまでの時間です。
      * TTL が非常に大きい場合、DNS レコードの更新が反映されるまでに時間がかかります。
* ビジネス要件とビジネス目標を満たすパフォーマンステストとセキュリティテストを実行します。
   * ステージング環境でテストを実行します。規模は実稼動と同じです。
   * 開発環境は、ステージング環境や実稼動環境とは異なるサイズに設定されます。
* カットオーバーし、新しいデプロイメントやコンテンツの更新を行わずに実際の運用開始が確実に実行されるようにします。
* Admin Console ユーザー通知グループを作成します。詳しくは、[通知プロファイル](/help/journey-onboarding/notification-profiles.md)を参照してください
* トラフィックフィルタールールを設定して、web サイト上で許可されないトラフィックを制御することを検討します。
   * レート制限トラフィックフィルタールールは、DDoS 攻撃に対する効果的なツールになる場合があります。WAF ルールと呼ばれる特別なカテゴリのトラフィックフィルタールールには、別のライセンスが必要です。
   * いくつかの[推奨スタータールール](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules)については、ドキュメントを参照してください。

運用開始中にタスクを再調整する必要がある場合は、いつでもリストを参照できます。
