---
title: Assets パフォーマンスチューニングガイド
description: AEM Assets のボトルネックを解消し、パフォーマンスを最適化するための、AEM の設定、ハードウェア、ソフトウェアおよびネットワークコンポーネントの変更に関する留意点。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Assets パフォーマンスチューニングガイド{#assets-performance-tuning-guide}

Adobe Experience Manager(AEM)Assetsのセットアップには、多数のハードウェア、ソフトウェアおよびネットワークコンポーネントが含まれています。 導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

また、特定のハードウェアおよびソフトウェアを最適化するガイドラインを識別してそれに従うことで優良な基盤を構築し、AEM Assets の導入によりパフォーマンス、スケーラビリティおよび信頼性の面で期待どおりの結果を得られます。

AEM Assets のパフォーマンスが低下すると、インタラクティブパフォーマンス、アセット処理、ダウンロード速度などの領域におけるユーザーエクスペリエンスに影響します。

実際、パフォーマンスの最適化は、プロジェクトのターゲット指標を設定する前に実行する基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## プラットフォーム {#platform}

AEMは多くのプラットフォームでサポートされていますが、LinuxおよびWindows上でネイティブツールのサポートが最も多くなり、最適なパフォーマンスと実装のしやすさに貢献しています。 AEM Assets のデプロイメントでは、高いメモリ要件を満たすために 64 ビットのオペレーティングシステムを採用するのが理想です。あらゆる AEM のデプロイメントにおいて、可能である場合は TarMK を実装してください。TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMK オフロードインスタンスを追加すると、AEM Assets のデプロイメントのワークフローの処理能力を高めることができます。

### 一時フォルダー {#temp-folder}

アセットのアップロード時間を短縮するには、Java 一時ディレクトリに高性能ストレージを使用します。LinuxおよびWindowsでは、RAMドライブまたはSSDを使用できます。 クラウドベースの環境では、同等の高速ストレージタイプを使用できます。 For example in Amazon EC2, an [&quot;ephemeral drive&quot;](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) drive can be used for the temp folder.

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linuxでは、次のコマンドを実行して8 GBのRAMドライブを作成します。

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS の場合、サードパーティ製ドライバーを使用して RAM ドライブを作成するか、SSD などの高性能ストレージを使用する必要があります。

高性能一時ボリュームの準備ができたら、JVM パラメーター -Djava.io.tmpdir を設定します。例えば、AEMのbin/startスクリプトのCQ_JVM_OPTS変数に以下のJVMパラメーターを追加できます。

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

Oracleは2015年4月にJava 7のアップデートのリリースを停止したので、Java 8にAEM Assetsをデプロイすることをお勧めします。 場合によってはパフォーマンスの改善が見られます。

### JVM パラメーター {#jvm-parameters}

次の JVM パラメーターを設定してください。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

すべての AEM Assets のユーザーに、データストアをセグメントストアから分離することをお勧めします。また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。Set `maxCachedBinarySize` to the smallest file size that can be held in the cache. Specify the size of the in-memory cache to use for the datastore within `cacheSizeInMB`. この値は合計ヒープサイズの 2～10 ％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

大量のアセットをAdobe Experience Managerにアップロードする場合、メモリ消費量が予期せず急増し、OutOfMemoryErrorsでJVMが失敗するのを防ぐために、バッファーされた画像キャッシュの設定済みの最大サイズを小さくします。 Consider an example that you have a system with a maximum heap (- `Xmx`param) of 5 GB, an Oak BlobCache set at 1 GB, and document cache set at 2 GB. このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。で、プ `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`ロパティをバイト単位 `cq.dam.image.cache.max.memory` で設定します。 例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

AEM 6.1 SP1 以降で `sling:osgiConfig` ノードを使用してこのプロパティを設定する場合は、データタイプを必ず Long にします。詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。

### S3 データストア {#s-data-store}

次の S データストアの設定（`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`3）は、アドビが 12.8 TB のバイナリラージオブジェクト（BLOB）を既存のファイルデータストアから顧客サイトの S3 データストアに抽出するのに役立ちました。

```
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## ネットワークの最適化 {#network-optimization}

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。大きなファイルをアップロードする場合は、WiFiネットワークが急速に飽和状態になるので、ユーザーがネットワークに有線接続していることを確認します。 To assess network performance by analyzing network topology, see [Assets Network Considerations](/help/assets/assets-network-considerations.md).

第一に、ネットワークの最適化戦略は使用できる帯域幅や、AEM インスタンスに対する負荷によって変わります。ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスタイプ（小、中、大）によって、AEM インスタンスに十分なネットワーク帯域幅があることを確認します。AEM が AWS にホストされている場合、帯域幅が適切に分散されていることが特に重要です。
* AEM インスタンスが AWS にホストされている場合、広い用途に対応するスケールポリシーがあると便利です。ユーザーが高い負荷を予想する場合は、インスタンスをアップサイズします。 負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

可能な限り、「DAM アセットの更新」ワークフローを「一時的」に設定します。この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

>[!NOTE]
>
>「DAM アセットの更新」ワークフローは、AEM 6.3 ではデフォルトで「一時的」に設定されます。この場合、以下の手順をスキップできます。

1. Navigate to */miscadmin* in the AEM instance to be configured (i.e. [https://localhost:4502/miscadmin)](https://localhost:4502/miscadmin)).
1. ナビゲーションツリーで、**ツール**／**ワークフロー**／**モデル**／**dam** と展開します。
1. 「**DAM アセットの更新**」をダブルクリックします。
1. フローティングツールパネルで、「**ページ**」タブに切り替えて「**ページプロパティ...**」をクリックします。
1. 「**一時的なワークフロー**」を選択し、「**OK**」をクリックします。

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。AEM Assets のデプロイメントにこれらの機能が必要な場合は、一時的なワークフローを設定しないでください。

   一時的なワークフローを使用できない場合は、定期的にパージされるワークフローを実行してアーカイブされた「DAM アセットの更新」ワークフローを削除し、システムのパフォーマンスが低下しないようにします。

   通常、パージワークフローは毎週実行する必要があります。ただし、大規模なアセットの取り込みがおこなわれている間など、リソースが限られているシナリオではより頻繁に実行できます。

   ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

   パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

   For example, after running numerous non-transient workflows (that creates workflow instance nodes), you can run [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) on an ad-hoc basis. これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

デフォルトでは、AEM は最大でサーバー上のプロセッサーと同じ数の並列ジョブを実行できます。この設定の問題点は、負荷が高い期間ではすべてのプロセッサーが「DAM アセットの更新」ワークフローに占有されるので、UI の応答が遅くなり、AEM がサーバーのパフォーマンスや安定性を保護するその他の処理を実行できなくなる点です。次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. On AEM Author, go to [https://localhost:4502/system/console/slingevent](https://localhost:4702/system/console/slingevent).
1. 実装に関連する各ワークフローキュー（Granite の一時的なワークフローキューなど）で「編集」をクリックします。
1. 並列ジョブの最大数の値を変更し、「保存」をクリックします。

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50 ％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要がある場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

「DAM アセットの更新」ワークフローには、Scene7 PTIFF の生成や InDesign サーバーの統合など、タスク向けに設定された一連の手順がすべて含まれています。ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。アドビでは「DAM アセットの更新」ワークフローモデルのカスタムコピーを作成し、不要な手順はすべて削除することをお勧めします。この場合、DAM アセットの更新のランチャーを更新して新しいモデルを参照するようにします。

>[!NOTE]
>
>DAM アセットの更新ワークフローを集中的に実行すると、ファイルデータストアのサイズが急激に増加する可能性があります。アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。
>
>これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。
>
>通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。
>
>ディスク領域が限られている場合に、DAM アセットの更新ワークフローを集中的に実行する際は、ガベージコレクションタスクの実行頻度を増やすことを検討してください。

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

もう 1 つの方法では、Scene7 テクノロジーを使用して画像の操作をすべて引き渡します。さらに、Brand Portal もデプロイできます。Brand Portal は、AEM インフラストラクチャからレンディションを生成する責務だけでなく、パブリッシュ層全体も受け継ぎます。

### XMP の書き戻し {#xmp-writeback}

XMP の書き戻しにより、AEM でメタデータが変更されたときは常に元のアセットが更新されます。これにより、次のような結果になります。

* アセット自体が変更されます
* アセットのバージョンが作成されます
* 「DAM アセットの更新」がアセットに対して実行されます

上記の結果により、大量のリソースが消費されます。このため、この機能が必要でない場合は、[XMP の書き戻しを無効化する](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)ことをお勧めします。

ワークフロー実行フラグがチェックされている場合、大量のメタデータをインポートすると、リソースを集中的に使用する XMP 書き戻しアクティビティが発生するおそれがあります。このようなインポートは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

## レプリケーション {#replication}

Sites の実装などで、アセットを多数のパブリッシュインスタンスにレプリケートするときは、チェーンレプリケーションを使用することをお勧めします。この場合、オーサーインスタンスが単一のパブリッシュインスタンスにレプリケートし、そのパブリッシュインスタンスが代わりに他のパブリッシュインスタンスにレプリケートすることで、オーサーインスタンスを解放します。

### チェーンレプリケーションの設定 {#configure-chain-replication}

1. レプリケーションのチェーンに使用する発行インスタンスを選択します
1. そのパブリッシュインスタンスで、他のパブリッシュインスタンスを指すレプリケーションエージェントを追加します。
1. 追加した各レプリケーションエージェントで、「トリガー」タブの「受信時」を有効にします。

>[!NOTE]
>
>アセットの自動アクティベートはお勧めしません。ただし、必要な場合は、ワークフローの最後の手順（通常は「DAM アセットの更新」）で実行することをお勧めします。

## 検索インデックス {#search-indexes}

システムインデックスの更新が含まれている場合が多いので、最新のサービスパックやパフォーマンス関連のホットフィックスを実装してください。See [Performance tuning tips | 6.x](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) for some index optimizations that can be applied, depending on your version of AEM.

<!--
Create custom indexes for queries that you run often. For details, see [methodology for analyzing slow queries](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) and [crafting custom indexes](/help/sites-deploying/queries-and-indexing.md). For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
-->

### Lucene Index の設定 {#lucene-index-configurations}

Oak インデックス設定を最適化して、AEM Assets のパフォーマンスを向上させることができる場合があります。

インデックス設定を更新してインデックス再構築時間を短縮します。

1. CRXDe /crx/de/index.jsp を開き、管理者ユーザーとしてログインします。
1. /oak:index/lucene を探します。
1. Add a String[] property named &quot;excludedPaths&quot; with values &quot;/var&quot;, &quot;/etc/workflow/instances&quot;, and &quot;/etc/replication&quot;
1. /oak:index/damAssetLucene を探します。
1. Add a String[] property named &quot;includedPaths&quot; with one value &quot;/content/dam&quot;
1. 保存

（AEM 6.1 および 6.2 のみ）ntBaseLucene インデックスを更新して、アセットの削除および移動のパフォーマンスを向上させます。

1. Browse to */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Add two nt:unstructured nodes &quot;slingResource&quot; and &quot;damResolvedPath&quot; under */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Set the properties below on the nodes (where ordered and propertyIndex properties are of type *Boolean*:
slingResource
name=&quot;sling:resource&quot;
ordered=false
propertyIndex= true
type=&quot;String&quot;
damResolvedPath
name=&quot;dam:resolvedPath&quot;
ordered=false
propertyIndex=true
type=&quot;String&quot;

1. On the /oak:index/ntBaseLucene node, set the property *reindex=true*
1. 「すべて保存」をクリックします。
1. Monitor the error.log to see when indexing is completed:
Reindexing completed for indexes: [/oak:index/ntBaseLucene]
1. CRXDe で /oak:index/ntBaseLucene ノードを更新すると reindex プロパティが false に戻るので、インデックス構築が完了したかどうかを確認することもできます。
1. インデックスの構築が完了したら、CRXDe に戻り、次の 2 つのインデックスに対して &quot;type&quot; プロパティを disabled に設定します。

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. 「すべて保存」をクリックします。

<!--
Disable Lucene Text Extraction:

If your users don't need to be able to search the contents of assets, for example, searching the text contained in PDF documents, then you can improve index performance by disabling this feature.

1. Go to the AEM package manager /crx/packmgr/index.jsp
1. Upload and install the package below

[Get File](assets/disable_indexingbinarytextextraction-10.zip)
-->

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

AEMの大きなファイルに関連する2つの主な既知の問題があります。 ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。このシナリオは、コンテンツパッケージを含む、AEM 内の 2 GB を超えるすべてのファイルが該当します。

同様に、S3 共有データストアを使用している間にファイルのサイズが 2 GB に到達すると、キャッシュからファイルシステムにファイルが完全に保持されるまで、少し時間がかかることがあります。結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

すべての AEM のデプロイメントでボトルネックをすばやく特定し解決できるように、パフォーマンステストの体制を確立してください。留意点は次のとおりです。

### ネットワークのテスト {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストするにあることで画像コンポーネントに問題が生じる。AMSのお客様は、アドビのネットワーク内でCSEを使用してテストを行います。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### AEM インスタンスのテスト {#aem-instance-testing}

CPU を効率的に使用し、負荷を分割することで遅延を最小限に抑え、高いスループットを実現するには、AEM インスタンスのパフォーマンスを定期的に監視してください。具体的には、次のことを実行します。

* AEM インスタンスに対して負荷テストを実行する
* アップロードのパフォーマンスと UI の応答性を監視する

## AEM Assets のパフォーマンスチェックリストおよびアセット管理タスクの影響 {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する
* サイズの大きなアセットのアップロードには有線接続を使用する
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する
* ファイルシステムデータストアまたは S3 データストアを設定する
* 一時的なワークフローを有効化する
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する
* ImageMagick を設定してリソースの消費を制限する
* 「DAM アセットの更新」ワークフローから不要な手順を削除する
* ワークフローとバージョンのパージを設定する
* 最新のサービスパックとホットフィックスでインデックスを最適化する。利用可能な追加のインデックスの最適化については、アドビのサポートにお問い合わせください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* （**[!UICONTROL AEM Webコンソール]**&#x200B;の&#x200B;**[!UICONTROL Day CQ DAM Mime Typeサービス]**&#x200B;を有効にすることで）ファイルのコンテンツからファイルタイプを検出するように AEM を構成している場合、大量のファイルを一括アップロードする際はリソースを大量に消費するので、ピーク時以外の時間におこないます。

