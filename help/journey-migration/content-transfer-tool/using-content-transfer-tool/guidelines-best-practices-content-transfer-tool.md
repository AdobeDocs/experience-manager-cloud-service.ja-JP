---
title: コンテンツ転送ツール使用のガイドラインとベストプラクティス
description: コンテンツ転送ツール使用のガイドラインとベストプラクティス
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 89%

---

# コンテンツ転送ツール使用のガイドラインとベストプラクティス {#guidelines}

## ガイドラインとベストプラクティス {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.md#important-considerations" text="Important Considerations when Mapping and Migrating Users" 

-->

コンテンツ転送ツールの新しいバージョンが利用可能です。新バージョンでは、コンテンツ転送プロセスと Cloud Acceleration Manager が統合されています。この新しいバージョンに切り替えて、次の利点をすべて活かすことを強くお勧めします。

* セルフサービス方式で、移行セットを 1 回抽出し、同時に複数の環境に取り込めます。
* 読み込み状態、ガードレール、エラー処理が改善され、ユーザーエクスペリエンスが向上しました
* 取り込みログは永続化され、常にトラブルシューティングに使用することができます。

新しいバージョンの使用を開始するには、コンテンツ転送ツールの古いバージョンをアンインストールする必要があります。新しいバージョンはアーキテクチャが大きく変更されているので、古いバージョンをアンインストールが必要になります。バージョン 2.x では、新しい移行セットを作成し、新しい移行セットに対して抽出と取り込みを再実行する必要があります。
2.0.0 より前のバージョンはサポートされなくなり、最新バージョンを使用することをお勧めします。

コンテンツ転送ツールの新しいバージョンには、次のガイドラインとベストプラクティスが適用されます。

* [リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=ja)と[データストアの整合性チェック](https://helpx.adobe.com/jp/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html)を&#x200B;**ソースリポジトリー**&#x200B;で実行して、潜在的な問題を特定し、リポジトリーのサイズを小さくすることをお勧めします。

* インジェスト段階では、*ワイプ*&#x200B;モードを有効にしてインジェストを実行することをお勧めします。このモードでは、ターゲット AEM as a Cloud Service 環境内の既存のリポジトリー（オーサーまたはパブリッシュ）が完全に削除された後、移行セットのデータで更新されます。このモードは、現在のコンテンツの上に移行セットが適用される非ワイプモードより、はるかに高速です。

* コンテンツ転送アクティビティが完了したら、Cloud Service 環境でコンテンツが正常にレンダリングされるように、Cloud Service 環境で正しいプロジェクト構造を使用する必要があります。

* コンテンツ転送ツールを実行する前に、ソース AEM インスタンスの `crx-quickstart` サブディレクトリに十分なディスク領域があることを確認する必要があります。これは、コンテンツ転送ツールによってリポジトリーのローカルコピーが作成され、後で移行セットにアップロードされるためです。必要な空きディスク容量を計算する一般的な式は次のとおりです。
   `data store size + node store size * 1.5`

   * *data store size*：実際のデータストアのサイズが大きい場合でも、コンテンツ転送ツールは 64 GB を使用します。
   * *node store size*：セグメントストアディレクトリのサイズまたは MongoDB データベースのサイズ。
したがって、セグメントストアのサイズが 20 GB の場合、必要な空きディスク容量は 94 GB になります。

* コンテンツ追加をサポートするには、コンテンツ転送アクティビティ全体を通して移行セットを維持管理する必要があります。Cloud Acceleration Manager では、コンテンツ転送アクティビティ中に、プロジェクトあたり一度に最大 5 個の移行セットを作成および維持管理できます。移行セットが 6 個以上必要な場合は、Cloud Acceleration Manager で 2 つ目のプロジェクトを作成する必要があります。ただし、複数のユーザーがターゲット上のコンテンツを上書きしないようにするために、追加のプロジェクト管理と製品外のガバナンスが必要になります。

## コンテンツ転送ツール使用前の重要な考慮事項 {#important-considerations}

コンテンツ転送ツールを実行する際には、次の重要事項を考慮してください。

* コンテンツ転送ツールに必要なシステム構成は、AEM 6.3 以降と Java 8 です。使用している AEM のバージョンがこれより古い場合、コンテンツ転送ツールを使用するには、コンテンツリポジトリーを AEM 6.5 にアップグレードする必要があります。

* AEM を開始するユーザーが `java` コマンドを実行できるように、AEM 環境上で Java を設定する必要があります。

* コンテンツ転送ツールは、ファイルデータストア、S3 データストア、共有 S3 データストア、Azure Blob Store データストアと共に使用できます。

* *サンドボックス環境*&#x200B;を使用している場合は、環境が最新で最新のリリースにアップグレードされていることを確認してください。*実稼動環境*&#x200B;を使用している場合、環境は自動的に更新されます。

* 取り込みを開始するには、コンテンツの転送先の Cloud Service インスタンスのローカル AEM **管理者**&#x200B;グループに属している必要があります。権限のないユーザーは、移行トークンを手動で指定しない限り、取り込みを開始できません。

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**administrators** グループに追加された管理者ユーザーにも当てはまります。コンテンツ転送ツールのアクセストークンを取得するには、ユーザーを&#x200B;**管理者**&#x200B;グループに再追加する必要があります。

* 2 つのソースのコンテンツがターゲット上の同じパスに移動された場合、取り込みでは、複数のソースのコンテンツをターゲット Cloud Service インスタンスに結合することはできません。複数のソースから 1 つのターゲット Cloud Service インスタンスにコンテンツを移動するには、ソースからのコンテンツパスが重複しないようにする必要があります。

* 抽出キーは、作成または更新時点から 14 日間有効です。抽出キーはいつでも更新できます。抽出キーの有効期限が切れている場合は、抽出を実行できません。

* コンテンツ転送ツール（CTT）は、ソースインスタンスからターゲットインスタンスにコンテンツを転送する前に、どのような種類のコンテンツ分析も実行しません。例えば、CTT では、コンテンツをパブリッシュ環境に取り込む際に、公開済みコンテンツと非公開コンテンツを区別しません。移行セットで指定されているコンテンツは何であれ、選択したターゲットインスタンスに取り込まれます。オーサーインスタンスとパブリッシュインスタンスのどちらか一方または両方に移行セットを取り込むことができます。コンテンツを実稼動インスタンスに移動する際は、ソースオーサーインスタンスに CTT をインストールしてコンテンツをターゲットオーサーインスタンスに移動し、同様に、ソースパブリッシュインスタンスに CTT をインストールしてコンテンツをターゲットパブリッシュインスタンスに移動することをお勧めします。詳しくは、 [パブリッシュインスタンスでのコンテンツ転送ツールの実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html#running-tool) を参照してください。

* コンテンツ転送ツールによって転送されるユーザーとグループは、権限を満たすためにコンテンツで必要なものに限られます。この _抽出_ プロセスは、 `/home` を移行セットに追加し、各ユーザーの電子メールアドレスから作成されたフィールドを追加して、ユーザーマッピングを実行します。 詳しくは、 [ユーザーマッピングとプリンシパルの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md). この _取り込み_ プロセスは、移行されたコンテンツ ACL で参照されているすべてのユーザーとグループをコピーします。

* 抽出段階では、コンテンツ転送ツールはアクティブな AEM ソースインスタンスで実行されます。

* コンテンツ転送プロセスの&#x200B;*抽出*&#x200B;段階が完了したら、*取り込み段階*&#x200B;を開始してコンテンツを AEM as a Cloud Service の&#x200B;*ステージング*&#x200B;インスタンスまたは&#x200B;*実稼働*&#x200B;インスタンスに取り込む前に、サポートチケットを申請して、*取り込み*&#x200B;を実行する意図をアドビに知らせる必要があります。それにより、アドビは、*取り込み*&#x200B;プロセス中に中断が発生しないようにすることができます。予定している&#x200B;*取り込み*&#x200B;日の 1 週間前にサポートチケットを申請する必要があります。サポートチケットを申請したら、サポートチームから、次の手順に関するガイダンスが提供されます。サポートチケットを申請する際には、次の詳細を記載します。

   * *取り込み*&#x200B;段階の開始を予定している正確な日付と大体の時刻（およびタイムゾーン）
   * データの取り込み先として予定している環境のタイプ（ステージングまたは実稼働）
   * プログラム ID

* オーサーの&#x200B;*取得段階*&#x200B;では、オーサーのデプロイメント全体がスケールダウンされます。つまり、オーサー AEM インスタンスは、インジェストプロセス全体で使用できなくなります。また、*取り込み*&#x200B;段階の実行中に Cloud Manager パイプラインが実行されないようにしてください。

* ソース AEM システム上のデータストアとして `Amazon S3` または `Azure` を使用する場合は、保存された BLOB を削除（ガベージコレクション）できないように、データストアを設定する必要があります。これにより、インデックスデータの整合性が確保されます。このように設定しないと、このインデックスデータの整合性が欠落しているために抽出が失敗する可能性があります。

* カスタムインデックスを使用する場合は、コンテンツ転送ツールを実行する前に、`tika` ノードでカスタムインデックスを設定する必要があります。詳細は、「[新しいインデックス定義の準備](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=ja#preparing-the-new-index-definition)」を参照してください。

* 追加を行う場合は、最初の抽出を実行した時点から、追加抽出を実行する時点まで、既存コンテンツのコンテンツ構造が変わらないことが不可欠です。最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行プロセス中は、必ずこの制限を実施してください。

* バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツ転送ツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。

* 移行セットは、長時間使用されなかった後に期限が切れ、その後はデータが使用できなくなります。 確認してください [移行セットの有効期限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#migration-set-expiry) を参照してください。

## 次の手順 {#whats-next}

コンテンツ転送ツールの使用に関するガイドライン、ベストプラクティス、重要な考慮事項を理解したら、ツールをインストールして使用する準備が整いました。まず、移行セットの作成から始めます。詳しくは、[コンテンツ転送ツールの基本を学ぶ](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)を参照してください。
