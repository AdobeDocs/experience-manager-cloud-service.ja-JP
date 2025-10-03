---
title: コンテンツトランスファーツール使用のガイドラインとベストプラクティス
description: コンテンツトランスファーツール使用のガイドラインとベストプラクティスについて説明します。
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
feature: Migration
role: Admin
source-git-commit: 943685ed9c33ba42c4dd1cb941b2eca1cce8bfe8
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 100%

---


# コンテンツトランスファーツール使用のガイドラインとベストプラクティス {#guidelines}

## ガイドラインとベストプラクティス {#best-practices}

<!-- Alexandru: hiding for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_guidelines"
>title="Guidelines and Best Practices"
>abstract="Review guidelines and best practices to use the Content Transfer tool including revision cleanup tasks, Disk space considerations and more."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Important Considerations for using Content Transfer Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/group-migration.md#important-considerations" text="Important Considerations when Migrating Groups" 

-->

コンテンツトランスファーツールは、コンテンツ転送プロセスを Cloud Acceleration Manager と統合します。次のすべての利点を得るには、このバージョン（2.0 以降ですが、現在はバージョン 3.0 が推奨）を使用することが必須です。

* セルフサービス方式で、移行セットを 1 回抽出し、同時に複数の環境に取り込めます。
* 読み込み状態、ガードレール、エラー処理の改善により、ユーザーエクスペリエンスが向上しました。
* 取り込みログは永続化され、常にトラブルシューティングに使用することができます。

最新バージョンの使用を開始するには、コンテンツトランスファーツールの古いバージョンをアンインストールします。バージョン 2.0 では、移行セットを作成し、そのセットで抽出と取り込みを再実行します。
2.0.0 より前のバージョンはサポートされていません。最新バージョンを使用することをお勧めします。

コンテンツトランスファーツールの新しいバージョンには、次のガイドラインとベストプラクティスが適用されます。

* **ソース**&#x200B;リポジトリに対して[リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=ja)と[データストア整合性チェック](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html?lang=ja)を実行し、潜在的な問題を特定してリポジトリのサイズを小さくします。

* 取り込み段階では、*ワイプ*&#x200B;モードを有効にして取り込みを実行することをお勧めします。このモードでは、ターゲットとなる Adobe Experience Manager（AEM）Cloud Service 環境内の既存のリポジトリ（オーサーまたはパブリッシュ）を削除します。次に、移行セットデータで更新します。このモードは、現在のコンテンツの上に移行セットが適用される非ワイプモードより高速です。

* コンテンツ転送アクティビティが完了したら、Cloud Service 環境でコンテンツが正常にレンダリングされるように、Cloud Service 環境で正しいプロジェクト構造を使用する必要があります。

* コンテンツトランスファーツールを実行する前に、ソース AEM インスタンスの `crx-quickstart` サブディレクトリに十分なディスク領域があることを確認する必要があります。これは、コンテンツトランスファーツールによってリポジトリーのローカルコピーが作成され、後で移行セットにアップロードされるためです。必要な空きディスク容量を計算する一般的な式は次のとおりです。
  `data store size + node store size * 1.5`

* *data store size*：実際のデータストアのサイズが大きい場合でも、コンテンツトランスファーツールは 64 GB を使用します。
* *node store size*：セグメントストアディレクトリのサイズまたは MongoDB データベースのサイズ。
したがって、セグメントストアのサイズが 20 GB の場合、必要な空きディスク容量は 94 GB になります。

* コンテンツの追加をサポートするには、コンテンツ転送アクティビティ全体を通して移行セットを維持管理する必要があります。Cloud Acceleration Manager では、コンテンツ転送アクティビティ中に、プロジェクトあたり一度に最大 10 個の移行セットを作成および維持管理できます。移行セットが 10 個以上必要な場合は、Cloud Acceleration Manager で 2 つ目のプロジェクトを作成します。ただし、複数のユーザーがターゲット上のコンテンツを上書きしないようにするために、追加のプロジェクト管理と製品外のガバナンスが必要になります。

* CTT ツールのインストールディレクトリを変更しないようにします。デフォルトでは、インストールは crx-quickstart/cloud-migration パスで実行されます。この特定の場所は、他のライブラリによって内部的に使用されます。このパスを変更すると、抽出の問題が発生する可能性があります。

## コンテンツトランスファーツール使用前の重要な考慮事項 {#important-considerations}

コンテンツトランスファーツールを実行する際には、次の重要事項を考慮してください。

* コンテンツトランスファーツールに必要なシステム構成は、AEM 6.3 以降と Java™ 8 です。使用している AEM のバージョンがこれより古い場合、コンテンツトランスファーツールを使用するには、コンテンツリポジトリーを AEM 6.5 にアップグレードします。

* AEM を開始するユーザーが `java` コマンドを実行できるように、AEM 環境上で Java™ を設定する必要があります。

* コンテンツトランスファーツールは、ファイルデータストア、S3 データストア、共有 S3 データストア、Azure Blob Store データストアと共に使用できます。

* *サンドボックス環境*&#x200B;を使用している場合は、環境が最新で最新のリリースにアップグレードされていることを確認してください。*実稼動環境*&#x200B;を使用している場合、環境は自動的に更新されます。

* 取り込みを開始するには、コンテンツの転送先の Cloud Service インスタンスのローカル AEM **管理者**&#x200B;グループに属している必要があります。権限のないユーザーは、移行トークンを手動で指定しない限り、取り込みを開始できません。

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。これは、**管理者**&#x200B;グループに追加された管理者ユーザーにも当てはまります。コンテンツトランスファーツールのアクセストークンを取得するには、ユーザーを&#x200B;**管理者**&#x200B;グループに再び追加する必要があります。

* 抽出キーは、作成または更新時点から 14 日間有効です。抽出キーはいつでも更新できます。抽出キーの有効期限が切れている場合は、抽出を実行できません。

* コンテンツトランスファーツール（CTT）は、ソースインスタンスからターゲットインスタンスにコンテンツを転送する前に、どのような種類のコンテンツ分析も実行しません。例えば、CTT では、コンテンツをパブリッシュ環境に取り込む際に、公開済みコンテンツと非公開コンテンツを区別しません。移行セットで指定されているコンテンツはすべて、選択したターゲットインスタンスに取り込まれます。ユーザーは、オーサーインスタンスとパブリッシュインスタンスのどちらか一方または両方に、移行セットを取り込むことができます。コンテンツを実稼動インスタンスに移動する際に、ソースオーサーインスタンスに CTT をインストールして、コンテンツをターゲットオーサーインスタンスに移動することをお勧めします。同様に、ソースパブリッシュインスタンスに CTT をインストールして、コンテンツをターゲットパブリッシュインスタンスに移動します。詳しくは、[パブリッシュインスタンスでのコンテンツトランスファーツールの実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#running-tool)を参照してください。

* コンテンツトランスファーツールによって転送されるグループは、権限を満たすためにコンテンツで必要なものに限られます。_抽出_&#x200B;プロセスは、`/home/groups` 全体を移行セットにコピーします。詳しくは、[グループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)を参照してください。_取り込み_&#x200B;プロセスは、移行されたコンテンツ ACL で参照されているすべてのグループをコピーします。クローズドユーザーグループ（CUG）ポリシーで使用されるグループに関するその他の考慮事項について詳しくは、[クローズドユーザーグループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)を参照してください。

* 抽出段階では、コンテンツトランスファーツールはアクティブな AEM ソースインスタンスで実行されます。

* オーサーの&#x200B;*取り込み段階*&#x200B;では、オーサーのデプロイメント全体がスケールダウンされます。つまり、オーサー AEM インスタンスが取り込みプロセス全体で使用できなくなります。また、*取り込み*&#x200B;段階の実行中に Cloud Manager パイプラインが実行されないようにする必要があります。

* ソース AEM システム上のデータストアとして `Amazon S3` または `Azure` を使用する場合は、保存された BLOB を削除（ガベージコレクション）できないように、データストアを設定する必要があります。これにより、インデックスデータの整合性が確保されます。このように設定しないと、このインデックスデータの整合性が欠落しているために抽出が失敗する可能性があります。

* カスタムインデックスを使用する場合は、コンテンツトランスファーツールを実行する前に、`tika` ノードでカスタムインデックスを設定する必要があります。詳しくは、[新しいインデックス定義の準備](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=ja#preparing-the-new-index-definition)を参照してください。

* 追加を行う場合は、最初の抽出を実行した時点から、追加抽出を実行する時点まで、既存コンテンツのコンテンツ構造が変わらないようにします。最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行作業中には必ず制限するようにしてください。

* バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツトランスファーツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。

* コンテンツトランスファーツール（CTT）は、結合の取り込みをサポートしていません。複数システムのコンテンツを 1 つの Cloud Service インスタンスに統合するには、1 つのソースシステムのバージョンのみを移行します。このプロセスでは、wipe=false パラメーターを持つ移行を使用する必要がありますが、操作の増分的な性質により、取り込み時間が長くなる可能性があります。可能であれば、移行を開始する前にコンテンツを単一のソースシステムに統合して、コンテンツを結合する必要をなくします。

* 移行セットは、無操作状態が長時間続くと有効期限が切れ、その後はデータが使用できなくなります。詳しくは、[移行セットの有効期限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#migration-set-expiry)を参照してください。

## 次の手順 {#whats-next}

コンテンツトランスファーツールの使用に関するガイドライン、ベストプラクティス、重要な考慮事項を理解したら、ツールをインストールして使用する準備が整いました。まず、移行セットの作成から始めます。[コンテンツトランスファーツールの](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)を参照してください。
