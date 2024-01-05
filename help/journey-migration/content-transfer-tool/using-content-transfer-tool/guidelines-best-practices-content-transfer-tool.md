---
title: コンテンツ転送ツール使用のガイドラインとベストプラクティス
description: コンテンツ転送ツールを使用する際のガイドラインとベストプラクティスについて説明します。
exl-id: d1975c34-85d4-42e0-bb1a-968bdb3bf85d
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 62%

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

コンテンツ転送ツールの新しいバージョンが利用可能です。新バージョンでは、コンテンツ転送プロセスと Cloud Acceleration Manager が統合されています。次の利点をすべて活用するには、この新しいバージョンに切り替えることを強くお勧めします。

* セルフサービス方式で、移行セットを 1 回抽出し、同時に複数の環境に取り込めます。
* 読み込み状態、ガードレール、エラー処理が改善され、ユーザーエクスペリエンスが向上しました。
* 取り込みログは永続化され、常にトラブルシューティングに使用することができます。

新しいバージョンの使用を開始するには、コンテンツ転送ツールの古いバージョンをアンインストールします。 新しいバージョンはアーキテクチャが大きく変更されているので、古いバージョンをアンインストールする必要があります。バージョン 2.x では、移行セットを作成し、セットに対して抽出と取り込みを再実行します。
2.0.0 より前のバージョンはサポートされていません。最新バージョンを使用することをお勧めします。

コンテンツ転送ツールの新しいバージョンには、次のガイドラインとベストプラクティスが適用されます。

* 実行 [リビジョンのクリーンアップ](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=ja) および [データストアの整合性チェック](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16550.html) の **ソース** リポジトリを使用して、潜在的な問題を特定し、リポジトリのサイズを小さくすることができます。

* インジェスト段階では、Adobeは、 *ワイプ* モードは有効です。target Adobe Experience Manager(AEM) リポジトリ環境の既存のリポジトリ（オーサーまたはパブリッシュ）が削除される場合に有効になります。 次に、移行セットのデータでを更新します。 このモードは、現在のコンテンツの上に移行セットが適用される非ワイプモードよりも高速です。

* コンテンツ転送アクティビティが完了したら、Cloud Service 環境でコンテンツが正常にレンダリングされるように、Cloud Service 環境で正しいプロジェクト構造を使用する必要があります。

* コンテンツ転送ツールを実行する前に、ソース AEM インスタンスの `crx-quickstart` サブディレクトリに十分なディスク領域があることを確認する必要があります。これは、コンテンツ転送ツールによってリポジトリーのローカルコピーが作成され、後で移行セットにアップロードされるためです。必要な空きディスク容量を計算する一般的な式は次のとおりです。
  `data store size + node store size * 1.5`

   * *data store size*：実際のデータストアのサイズが大きい場合でも、コンテンツ転送ツールは 64 GB を使用します。
   * *node store size*：セグメントストアディレクトリのサイズまたは MongoDB データベースのサイズ。
したがって、セグメントストアのサイズが 20 GB の場合、必要な空きディスク容量は 94 GB になります。

* コンテンツの追加をサポートするには、コンテンツ転送アクティビティ全体を通して移行セットを維持管理する必要があります。Cloud Acceleration Manager では、コンテンツ転送中に一度に 1 つのプロジェクトにつき最大 20 個の移行セットを作成および管理できます。 20 を超える移行セットが必要な場合は、Cloud Acceleration Manager で 2 つ目のプロジェクトを作成します。 ただし、複数のユーザーがターゲット上のコンテンツを上書きしないように、追加のプロジェクト管理と製品外ガバナンスが必要です。

* CTT ツールのインストールディレクトリを変更しないでください。 デフォルトでは、インストールは crx-quickstart/cloud-migration パスで実行されます。 この特定の場所は、他のライブラリによって内部的に使用されます。 このパスを変更すると、抽出の問題が発生する可能性があります。

## コンテンツ転送ツール使用前の重要な考慮事項 {#important-considerations}

コンテンツ転送ツールを実行する際には、次の重要事項を考慮してください。

* コンテンツ転送ツールに必要なシステム構成は、AEM 6.3 以降と Java™ 8 です。それ以前のAEMバージョンの場合、コンテンツ転送ツールを使用するには、コンテンツリポジトリをAEM 6.5 にアップグレードします。

* AEM を開始するユーザーが `java` コマンドを実行できるように、AEM 環境上で Java™ を設定する必要があります。

* コンテンツ転送ツールは、ファイルデータストア、S3 データストア、共有 S3 データストア、Azure Blob Store データストアと共に使用できます。

* *サンドボックス環境*&#x200B;を使用している場合は、環境が最新で最新のリリースにアップグレードされていることを確認してください。*実稼動環境*&#x200B;を使用している場合、環境は自動的に更新されます。

* 取り込みを開始するには、ローカルのAEMに属している必要があります **管理者** グループを作成し、Cloud Serviceの転送先となるコンテンツインスタンスに含めます。 権限のないユーザーは、移行トークンを手動で指定しない限り、取り込みを開始できません。

* 「**取得前にクラウドインスタンス上の既存のコンテンツを消去**」オプションが有効な場合は、既存のリポジトリー全体が削除され、コンテンツの取り込み先となる新しいリポジトリーが作成されます。つまり、ターゲットの Cloud Service インスタンスに対する権限を含むすべての設定がリセットされます。また、管理者ユーザーが **管理者** グループ化します。 ユーザーは、 **管理者** グループを使用して、コンテンツ転送ツールのアクセストークンを取得します。

* 2 つのソースのコンテンツがターゲット上の同じパスに移動された場合、取り込みでは、複数のソースのコンテンツをターゲット Cloud Service インスタンスに結合することはできません。複数のソースから 1 つのターゲットCloud Serviceインスタンスにコンテンツを移動するには、ソースからのコンテンツパスが重複しないようにします。

* 抽出キーは、作成または更新された日時から 14 日間有効です。 抽出キーはいつでも更新できます。抽出キーの有効期限が切れている場合は、抽出を実行できません。

* コンテンツ転送ツール（CTT）は、ソースインスタンスからターゲットインスタンスにコンテンツを転送する前に、どのような種類のコンテンツ分析も実行しません。例えば、CTT では、コンテンツをパブリッシュ環境に取り込む際に、公開済みコンテンツと非公開コンテンツを区別しません。移行セットで指定されているコンテンツはすべて、選択したターゲットインスタンスに取り込まれます。ユーザーは、オーサーインスタンスとパブリッシュインスタンスのどちらか一方または両方に移行セットを取り込むことができます。Adobeでは、コンテンツを実稼動インスタンスに移動する際に、コンテンツをターゲットのオーサーインスタンスに移動するために、CTT をソースオーサーインスタンスにインストールすることをお勧めします。 同様に、ソースパブリッシュインスタンスに CTT をインストールして、コンテンツをターゲットパブリッシュインスタンスに移動します。詳しくは、[パブリッシュインスタンスでのコンテンツ転送ツールの実行](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#running-tool)を参照してください。

* コンテンツ転送ツールによって転送されるユーザーとグループは、権限を満たすためにコンテンツで必要なものに限られます。_抽出_&#x200B;プロセスは、`/home` 全体を移行セットにコピーし、各ユーザーのメールアドレスから作成されたフィールドを追加して、ユーザーマッピングを実行します。詳しくは、[ユーザーマッピングとプリンシパルの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md)を参照してください。The _取得_ プロセスは、移行されたコンテンツ ACL で参照されているすべてのユーザーとグループをコピーします。 詳しくは、 [閉じられたユーザーグループの移行](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) 閉じられたユーザーグループ (CUG) ポリシーで使用されるグループに関するその他の考慮事項については、を参照してください。

* 抽出段階では、コンテンツ転送ツールはアクティブな AEM ソースインスタンスで実行されます。

* オーサーの&#x200B;*取得段階*&#x200B;では、オーサーのデプロイメント全体がスケールダウンされます。つまり、オーサー AEM インスタンスが取り込みプロセス全体で使用できなくなります。また、*取り込み*&#x200B;段階の実行中に Cloud Manager パイプラインが実行されないようにする必要があります。

* ソース AEM システム上のデータストアとして `Amazon S3` または `Azure` を使用する場合は、保存された BLOB を削除（ガベージコレクション）できないように、データストアを設定する必要があります。これにより、インデックスデータの整合性が確保されます。このように設定しないと、このインデックスデータの整合性が欠落しているために抽出が失敗する可能性があります。

* カスタムインデックスを使用する場合は、コンテンツ転送ツールを実行する前に、`tika` ノードでカスタムインデックスを設定する必要があります。詳しくは、[新しいインデックス定義の準備](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#preparing-the-new-index-definition)を参照してください。

* 追加を行う場合は、最初の抽出を実行した時点からに既存のコンテンツのコンテンツ構造を変更しないでください。 最初の抽出以降に構造が変更されたコンテンツに対しては、追加を実行できません。移行作業中には必ず制限するようにしてください。

* バージョンを移行セットの一部に含める予定で、`wipe=false` を指定して追加を行う場合、コンテンツ転送ツールの現在の制限事項により、バージョンのパージを無効にする必要があります。バージョンのパージを有効にしたまま、移行セットへの追加を行う場合は、`wipe=true` を指定して取り込みを実行する必要があります。

* 移行セットは、無操作状態が長時間続くと有効期限が切れ、その後はデータが使用できなくなります。 詳しくは、[移行セットの有効期限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja#migration-set-expiry)を参照してください。

## 次の手順 {#whats-next}

コンテンツ転送ツールの使用に関するガイドライン、ベストプラクティス、重要な考慮事項を理解したら、ツールをインストールして使用する準備が整いました。まず、移行セットの作成から始めます。詳しくは、 [コンテンツ転送ツールの概要](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).
