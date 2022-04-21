---
title: 運用開始
description: コードとコンテンツがクラウドに対応した後に移行を実行する方法について
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 9a10348251fe7559ae5d3c4a203109f1f6623bce
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 76%

---

# 運用開始 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="運用開始準備"
>abstract="AEM as a Cloud Service 上でうまくスムーズに運用を開始できるようにするには、コードおよびコンテンツ凍結期間、反復テスト、コンテンツ追加、パフォーマンステスト、セキュリティテストなどの計画を立案してください。"

ジャーニーのこのステップでは、コードとコンテンツの両方を AEM as a Cloud Service に移行する準備ができた後で移行を計画して実行する方法を説明します。さらに、移行を実行する際のベストプラクティスと既知の制限事項についても説明します。

## これまでの説明内容 {#story-so-far}

ジャーニーのこれまでのフェーズでは、

* AEM as a Cloud Service への移行に着手する方法を [はじめに](/help/journey-migration/getting-started.md) ページで学びました。
* [準備フェーズ](/help/journey-migration/readiness.md) を読んで、デプロイメントをクラウドに移動する準備ができているかどうかを判断しました。
* [実装フェーズ](/help/journey-migration/implementation.md) でコードとコンテンツをクラウド対応にするためのツールとプロセスをよく理解しました。

## 目的 {#objective}

このドキュメントでは、ジャーニーのこれまでのステップをよく理解した後で AEM as a Cloud Service への移行を実行する方法を説明します。実稼働環境の初期移行を実行する方法と、AEM as a Cloud Service への移行時に従うべきベストプラクティスについて説明します。

## 初期の実稼動環境移行 {#initial-migration}

実稼働環境の移行を実行する前に、 [実装フェーズ](/help/journey-migration/implementation.md) の [コンテンツ移行の戦略とタイムライン](/help/journey-migration/implementation.md##strategy-timeline) の節に従って移行手順の準備と検証を行ってください。

* クローンで実行された AEM as a Cloud Service ステージ移行時に得た経験に基づいて、実稼働環境からの移行を開始します。
   * オーサー - オーサー
   * パブリッシュ - パブリッシュ

* AEM as a Cloud Service のオーサー層とパブリッシュ層の両方に取り込まれたコンテンツを検証します。
* 取り込みが完了するまでソースと移行先の両方のコンテンツが移動しないようにコンテンツオーサリングチームに指示します。
* 新しいコンテンツの追加、編集または削除はできますが、移動は避けてください。 これは、ソースと移行先の両方に適用されます。
* 完全な抽出と取り込みに [要した時間](/help/journey-migration/implementation.md#gathering-data) を記録して、将来の追加移行のタイムラインを見積もります。
* オーサーとパブリッシュの両方に対して [移行プランナー](/help/journey-migration/implementation.md#migration-plan) を作成します。

## 増分追加 {#top-up}

実稼働環境からの最初の移行を行ったら、クラウドインスタンス上でコンテンツを最新の状態にするために、増分追加を実行する必要があります。このため、次のベストプラクティスに従うことをお勧めします。

* コンテンツの量に関するデータを収集します。例：1 週間ごと、2 週間ごと、1 か月ごと。
* 48 時間を超えるコンテンツ抽出および取り込みを避けるように、追加を計画します。この方法は、コンテンツの追加が週末の時間枠に収まるようにすることをお勧めします。
* 必要な追加数を計画し、それらの見積もりを使用して開始日を計画します。

## 移行にともなうコードおよびコンテンツの凍結タイムラインの特定 {#code-content-freeze}

前述のように、コードとコンテンツの凍結期間をスケジュールする必要があります。凍結期間の計画に役立てるため、次の質問を使用します。

* コンテンツのオーサリングアクティビティを凍結する必要がある期間はどのくらいですか？
* 配信チームに新機能の追加を停止するように依頼する必要がある期間はどのくらいですか？

最初の質問に答えるには、実稼動環境以外での試験的実行に要した時間を考慮してください。2 つ目の質問に答えるには、新しい機能を追加するチームと、コードをリファクタリングするチームとの緊密なコラボレーションが必要です。目標は、既存のデプロイメントに追加されているすべてのコードが、クラウドサービスブランチにも追加、テスト、デプロイされるようにすることです。一般的には、コードの凍結量が少なくなることを意味します。

さらに、最終的なコンテンツ追加がスケジュールされたときに、コンテンツの凍結を計画する必要があります。

## ベストプラクティス {#best-practices}

移行を計画または実行する際は、次のガイドラインを考慮してください。

* オーサーからオーサーへの移行とパブリッシュからパブリッシュへの移行
* 次の用途に使用できる実稼働クローンをリクエストします。
   * リポジトリ統計のキャプチャ
   * 移行アクティビティの検証
   * 移行計画の準備
   * コンテンツ凍結要件の特定
   * 実稼動環境から移行する際に、実稼動環境でのアップサイズのニーズを特定する

**コンテンツ転送ツールのベストプラクティス**

運用を開始する際は、クローンではなく実稼動環境でコンテンツ移行を実行するようにしてください。最初の移行に [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) を使用してから、追加抽出を頻繁に（毎日でも）実行して、より小さなチャンクを抽出し、ソース AEM への長期的な負荷を避けるのが良いアプローチです。

実稼動環境の移行を実行する場合は、次の理由により、コンテンツ転送ツールをクローンから実行しないでください。

* 顧客が追加移行時にコンテンツバージョンを移行する必要がある場合、クローンからコンテンツ転送ツールを実行しても、バージョンは移行されません。クローンがライブ作成者から頻繁に再作成された場合でも、クローンが作成されるたびに、差分の計算にコンテンツ転送ツールで使用されるチェックポイントがリセットされます。
* クローン全体を更新することはできないので、ACL クエリパッケージを使用して、追加または編集するコンテンツをパッケージ化して実稼動環境からクローンにインストールする必要があります。このアプローチの問題は、ソースインスタンス上の削除されたコンテンツは、ソースとクローンの両方から手動で削除しない限り、クローンに到達しないことです。これにより、実稼動環境で削除されたコンテンツがクローンやAEM as a Cloud Service上で削除されない可能性が生じます。

**コンテンツ移行中の AEM ソースの負荷の最適化**

抽出段階では、AEM ソースの負荷が大きくなることに注意してください。次の点に注意してください。

* コンテンツ転送ツールは、4 GB の JVM ヒープを使用する外部 Java プロセスです
* 非 AzCopy バージョンのバイナリはダウンロードされ、ソース AEM 作成者上の一時的な領域に保存され、ディスク I/O を消費した後、ネットワーク帯域幅を消費する Azure コンテナーにアップロードされます
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) は、BLOB を BLOB ストアから Azure コンテナーに直接転送します。このコンテナーは、ディスク I/O とネットワーク帯域幅を節約します。AzCopy バージョンでは、引き続きディスクとネットワーク帯域幅を使用して、セグメントストアから Azure コンテナーにデータを抽出してアップロードします
* コンテンツ転送ツールプロセスは、取り込みログをストリーミングするだけで、ディスク I/O やネットワーク帯域幅に関してはソースインスタンスに大きな負荷がかからないので、取り込み段階ではシステムリソースの方が軽くなります

## 既知の制限事項 {#known-limitations}

抽出された移行セットの一部として以下の制限が見つかった場合、取り込み全体が失敗することを考慮してください。

* 名前が 150 文字を超える JCR ノード
* 16 MB を超える JCR ノード
* AEM as a Cloud Service に既に存在する、取り込み中の `rep:AuthorizableID` を持つすべてのユーザー／グループ
* 抽出されて取り込まれたアセットが、次の移行処理の前に、ソースまたは宛先で別のパスに移動する場合

## アセットの正常性 {#asset-health}

上記の節と比較すると、以下のアセットの問題が原因で取り込みが失敗することは **ありません**。ただし、次のシナリオでは、適切な手順を実行することを強くお勧めします。

* 元のレンディションがないアセット
* `jcr:content` ノードが見つからないフォルダー

上記の両方の項目が識別され、 [ベストプラクティスアナライザー](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) レポートで報告されます。

## 運用開始チェックリスト {#Go-Live-Checklist}

このアクティビティリストを確認し、スムーズで正常な移行を実行できるようにしてください。

* 機能と UI テストを使用してエンドツーエンドの実稼動パイプラインを実行し、 **常に最新** AEM製品エクスペリエンス。 次のリソースを参照してください。
   * [AEM バージョンのアップデート](/help/implementing/deploying/aem-version-updates.md)
   * [カスタム機能テスト](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI テスト](/help/implementing/cloud-manager/ui-testing.md)
* コンテンツを実稼動環境に移行し、関連するサブセットがステージング環境でテストに使用できることを確認します。
   * AEMの DevOps ベストプラクティスは、コードが開発環境から実稼動環境に移行したことを意味していますが、 [コンテンツを実稼動環境から下に移動します。](/help/overview/enterprise-devops.md#code-movement)
* コードとコンテンツの凍結期間のスケジュール設定。
   * 関連トピック [移行のためのコードとコンテンツのフリーズタイムライン](#code-content-freeze)
* 最終コンテンツの追加.
* Dispatcher 設定を検証します。
   * Dispatcher をローカルで設定、検証、シミュレーションする、ローカルの Dispatcher バリデーターを使用します
      * [ローカルの Dispatcher ツールを設定します。](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=ja#prerequisites)
   * 仮想ホストの構成を慎重に確認します。
      * 最も簡単な（デフォルトの）解決策は、次のものです。 `ServerAlias *` 仮想ホストファイルの `/dispatcher/src/conf.d/available_vhostsfolder`.
         * これにより、製品機能テスト、Dispatcher キャッシュの無効化、クローンで使用されるホストエイリアスが機能するようになります。
      * ただし、 `ServerAlias *` は、少なくとも次の条件を満たすことはできません `ServerAlias` カスタムドメインに加えて、エントリも許可する必要があります。
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* CDN、SSL および DNS を設定します。
   * 独自の CDN を使用している場合は、適切なルーティングを設定するためのサポートチケットを入力します。
      * の節を参照してください。 [顧客 CDN がAEM管理 CDN を指す](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) （ CDN ドキュメント）を参照してください。
      * CDN ベンダーのドキュメントに従って、SSL および DNS を設定する必要があります。
   * 追加の CDN を使用しない場合は、次のドキュメントに従って、SSL と DNS を管理します。
      * SSL 証明書の管理
         * [SSL 証明書管理の概要](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [SSL 証明書の管理](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * カスタムドメイン名 (DNS) の管理
         * [カスタムドメイン名の概要](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [カスタムドメイン名の追加](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [カスタムドメイン名の管理](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * DNS レコードの TTL 設定を必ず検証してください。
      * TTL は、DNS レコードがキャッシュに残ってから、サーバーに更新を要求するまでの時間です。
      * TTL が非常に高い場合、DNS レコードの更新が反映されるまでに時間がかかります。
* ビジネス要件と目標を満たすパフォーマンスとセキュリティのテストを実行します。
* 切り替えて、新しいデプロイメントやコンテンツの更新を行わずに、実際の運用開始が実行されるようにします。

移行の実行中にタスクを再調整する必要がある場合は、いつでもリストを参照できます。

## 次の手順 {#what-is-next}

AEM as a Cloud Service への移行の実行方法を理解したら、[運用開始後](/help/journey-migration/post-go-live.md)ページを開いて、インスタンスのスムーズな実行を維持できます。
