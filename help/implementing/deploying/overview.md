---
title: AEM as a Cloud Service へのデプロイ
description: 'AEM as a Cloud Service へのデプロイ '
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '3537'
ht-degree: 99%

---


# AEM as a Cloud Service へのデプロイ {#deploying-to-aem-as-a-cloud-service}

## 概要 {#introduction}

AEM as a Cloud Service でのコード開発の基本は、AEM On Premise や Managed Services ソリューション上の AEM の場合と同様です。開発者はコードを作成しローカルでテストします。コードはその後、リモートの AEM as a Cloud Service 環境にプッシュされます。Cloud Manager（Managed Services のオプションのコンテンツ配信ツール）が必要です。これが、AEM as a Cloud Service 環境にコードをデプロイするための唯一のメカニズムになりました。

AEM バージョンのアップデートは、常に、カスタムコードのプッシュとは別のデプロイメントイベントになります。別の見方をすれば、カスタムコードリリースは実稼動環境にある AEM バージョンに照らしてテストする必要があります。カスタムコードがその AEM 上にデプロイされるからです。その後におこなわれる AEM バージョンアップデートは、現在の Managed Services と比較すると頻繁で、自動的に適用されます。これらは、既に導入されている顧客コードとの後方互換性を保つためのものです。

次のビデオでは、AEM as a Cloud Service にコードをデプロイする方法の概要を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

このドキュメントの残りの部分では、AEM as a Cloud Service のバージョンアップデートと顧客側でのアップデートの両方に対応できるように、開発者が開発のベストプラクティスをどのように適応させるべきかについて説明します。

>[!NOTE]
>コードベースが既にある場合は、[AEM ドキュメント](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)に記載されているリポジトリ再構築の演習を完了することをお勧めします。


## AEM バージョンのアップデート {#version-updates}

AEM は頻繁に（可能性としては 1 日に 1 回）更新され、バグ修正とパフォーマンス強化に重点を置いておこなわれることを理解することが重要です。アップデートは透過的におこなわれ、ダウンタイムは発生しません。アップデートは後方互換性を保つように作成されています。つまり、カスタムコードを変更する必要はありません。実際、AEM のアップデートは、顧客コードのデプロイメントとは無関係のイベントです。AEM アップデートは、前回正常に完了したコードプッシュの上にデプロイされます。つまり、実稼動環境への前回のプッシュ以降にコミットされた変更はデプロイされません。

>[!NOTE]
>
>カスタムコードがステージング環境にプッシュされた後で拒否された場合、次回の AEM アップデートでは、それらの変更は削除され、顧客が前回実稼動環境に正常にリリースしたコードの Git タグを反映するようになります。

機能リリースは、毎日のリリースと比べてユーザーエクスペリエンスへの影響が大きい機能追加および強化に重点を置いて、通常の頻度でおこなわれます。機能リリースは、大規模な変更セットのデプロイメントではなくリリーストグルの切り替えでトリガーされ、毎日のアップデートを通じて何日または何週間にもわたって蓄積されてきたコードをアクティベートします。

ヘルスチェックは、アプリケーションのヘルスを監視するために使用されます。AEM as a Cloud Service のアップデート中にこれらのチェックが失敗した場合、その環境に対するリリースは続行されず、アップデートがこの予期しない動作を引き起こした原因をアドビが調査します。

### 複合ノードストア {#composite-node-store}

ノードのクラスターであるオーサーの場合も含め、前述のように、ほとんどの場合、アップデートでダウンタイムは発生しません。Oak の「複合ノードストア」機能により、ローリングアップデートが可能です。この機能を利用すると、AEM で複数のリポジトリを同時に参照できます。ローリングデプロイメントでは、新しいグリーン AEM バージョンに古いブルー AEM バージョンとは異なる独自の `/libs`（TarMK ベースの不変リポジトリ）が含まれていますが、どちらも、`/content`、`/conf`、`/etc` などの領域を含んだ DocumentMK ベースの共有の可変リポジトリを参照しています。ブルーバージョンにもグリーンバージョンにも独自の `/libs` があるので、ローリングアップデート中はどちらもアクティブになり、ブルーバージョンが完全にグリーンバージョンに置き換わるまでトラフィックを処理することができます。

## お客様向けリリース {#customer-releases}

### 適切な AEM バージョンに照らしたコーディング {#coding-against-the-right-aem-version}

これまでの AEM ソリューションでは、最新の AEM バージョンが頻繁に（およそ年 1 回、四半期ごとにサービスパックをリリース）変更され、顧客側では、API JAR を参照して、都合の良いときに実稼動インスタンスを最新のクイックスタートに更新するという形でした。しかし、AEM as a Cloud Service アプリケーションは、もっと頻繁に最新バージョンの AEM に自動更新されるので、内部リリースのカスタムコードは、より新しい AEM インターフェイスに対応するように作成する必要があります。

既存の非クラウドバージョンの AEM と同様に、特定のクイックスタートに基づくローカルのオフライン開発がサポートされ、ほとんどの場合にデバッグに最適なツールになると予想されます。

>[!NOTE]
>ローカルマシン上と Adobe Cloud 上のアプリケーションの動作には、運用上のわずかな違いがあります。これらのアーキテクチャの違いは、ローカル開発時に考慮される必要があり、結果的に、クラウドインフラストラクチャにデプロイしたときに動作が異なることになる可能性があります。こうした違いがあるので、実稼動環境で新しいカスタムコードをロールアウトする前に、開発環境とステージ環境で徹底的なテストを実行することが重要です。

内部リリースのカスタムコードを開発するには、[AEM as a Cloud Service の SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) の関連バージョンをダウンロードし、インストールする必要があります。AEM as a Cloud Service Dispatcher ツールを使用する方法について詳しくは、[このページ](/help/implementing/dispatcher/overview.md)を参照してください。

## Cloud Manager とパッケージマネージャーを使用したコンテンツパッケージのデプロイ {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Cloud Manager を使用したデプロイメント {#deployments-via-cloud-manager}

お客様は、Cloud Manager を使用してカスタムコードをクラウド環境にデプロイします。Cloud Manager は、ローカルに作成したコンテンツパッケージを Sling Feature Model に準拠したアーティファクトに変換することに注意してください（このモデルは、クラウド環境で動作する際の AEM as a Cloud Service アプリケーションを記述するものです）。その結果、クラウド環境のパッケージマネージャーでパッケージを調べると、名前に「cp2fm」が含まれており、変換後のパッケージはすべてのメタデータが削除されています。これらを操作することはできません。つまり、ダウンロードしたり、複製したり、開いたりすることはできません。コンバーターについて詳しくは、[こちら](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)を参照してください。

AEM as a Cloud Service アプリケーション用に作成されたコンテンツパッケージでは、不変コンテンツと可変コンテンツを明確に分離する必要があります。分離に従わない場合、Cloud Manager がビルドに失敗し、次のようなメッセージを出力します。

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

この節の残りの部分では、不変パッケージと可変パッケージの構成と意味について説明します。

### 不変コンテンツパッケージ {#immutabe-content-packages}

不変リポジトリに保存されるコンテンツとコードはすべて、Git にチェックインし、Cloud Manager を通じてデプロイする必要があります。つまり、現在の AEM ソリューションとは異なり、コードは実行中の AEM インスタンスには直接デプロイされません。これにより、任意のクラウド環境で特定のリリースに対して同一のコードが実行されるようになり、意図しないコード変更が実稼動環境で発生するリスクをなくすことができます。例えば、OSGi 設定は、AEM Web コンソールの Configuration Manager を通じて実行時に管理されるのではなく、ソース管理にコミットする必要があります。

ブルーグリーンデプロイメントパターンによるアプリケーション変更はスイッチで有効になるので、サービスユーザー、ACL、ノードタイプ、インデックス定義の変更を除き、可変リポジトリ内の変更に応じておこなうことはできません。

コードベースが既にある場合は、AEM ドキュメントに記載されているリポジトリ再構築の演習を完了して、以前 /etc の配下にあったコンテンツが適切な場所に確実に移動されるようにすることが重要です。

## OSGi 設定 {#osgi-configuration}

前述のように、OSGi 設定は Web コンソールを通じて管理するのではなく、ソース管理にコミットする必要があります。そのための手法は次のとおりです。

* AEM Web コンソールの Configuration Manager を使用して開発者のローカル AEM 環境に必要な変更を加えた後、その結果をローカルファイルシステム上の AEM プロジェクトに書き出す。
* ローカルファイルシステム上の AEM プロジェクトに OSGi 設定を手動で作成した後、AEM コンソールの Configuration Manager でプロパティ名を参照する。

OSGI の設定について詳しくは、[AEM as a Cloud Service の OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。

## 可変コンテンツ {#mutable-content}

場合によっては、環境が更新されるたびに Cloud Manager でデプロイできるように、ソース管理でコンテンツの変更を準備すると便利なことがあります。例えば、特定のルートフォルダー構造をシードにしたり、編集可能なテンプレートに変更を集約したりして、アプリケーションのデプロイメントで更新されたコンポーネントの変更でポリシーを有効にするのが妥当な場合があります。

Cloud Manager で可変リポジトリにデプロイされるコンテンツ、可変コンテンツパッケージ、repoinit ステートメントを記述する戦略は 2 通りあります。

### 可変コンテンツパッケージ {#mutable-content-packages}

フォルダーパス階層、サービスユーザー、アクセス制御（ACL）などのコンテンツは、通常、Maven アーキタイプベースの AEM プロジェクトにコミットされます。使用される手法には、AEM からの書き出し、または XML 形式での直接書き込みがあります。ビルドおよびデプロイメントプロセス中に、Cloud Manager は、生成された可変コンテンツパッケージをパッケージ化します。可変コンテンツは、パイプラインのデプロイフェーズで次の 3 回の異なるタイミングでインストールされます。

新しいバージョンのアプリケーションの起動前：

* インデックス定義（追加、変更、削除）

新しいバージョンのアプリケーションの起動中（切り替えの前）：

* サービスユーザー（追加）
* サービスユーザー ACL（追加）
* ノードタイプ（追加）

新しいバージョンのアプリケーションへの切り替え後：

* Jackrabbit FileVault で定義可能なその他のすべてのコンテンツ。次に例を示します。
   * フォルダー（追加、変更、削除）
   * 編集可能なテンプレート（追加、変更、削除）
   * コンテキスト対応の設定（`/conf` 配下のあらゆるもの）（追加、変更、削除）
   * スクリプト（パッケージは、パッケージのインストールプロセスの様々な段階でインストールフックをトリガーできます）

`/apps` 配下の install.author フォルダーまたは install.publish フォルダーにパッケージを埋め込むことで、可変コンテンツのインストールをオーサーまたはパブリッシュのみに制限することができます。推奨されるプロジェクト再構築について詳しくは、[AEM ドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/deploying/restructuring/repository-restructuring.html)を参照してください。

>[!NOTE]
> コンテンツパッケージは、すべての環境タイプ（開発、ステージ、実稼動）にデプロイされます。デプロイメントを特定の環境に限定することはできません。この制限があるのは、自動実行のテスト実行オプションが確実に適用されるようにするためです。環境に固有のコンテンツは、パッケージマネージャーを使用して手動でインストールする必要があります。

また、可変コンテンツパッケージの変更を適用後にロールバックする仕組みはありません。問題を検出した場合は、次回のコードリリースで修正するか、最後の手段としてシステム全体をデプロイメント前の時点に復元するかを選択できます。

サードパーティパッケージが含まれている場合は、それらが AEM as a Cloud Service と互換性があるかどうかを検証する必要があります。互換性がない場合は、それらのパッケージを組み込むとデプロイメントエラーが発生します。

前述のように、コードベースが既にある場合は、[AEM ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)に記載されているリポジトリ再構築の演習に準拠する必要があります。

## repoinit {#repoinit}

次の場合は、OSGi ファクトリ設定で明示的なコンテンツ作成用の `repoinit` ステートメントを手動でコーディングするアプローチを取ることをお勧めします。

* サービスユーザーの作成／削除／無効化
* グループの作成／削除
* ユーザーの作成／削除
* ACL の追加

   >[!NOTE]
   >
   > ACL の定義では、ノード構造が既に存在する必要があります。そのため、先行するパス作成ステートメントが必要になる場合があります。

* パスの追加（例えば、ルートフォルダー構造用）
* CND の追加（ノードタイプ定義）

次の利点があるので、サポートされているこれらのコンテンツ変更使用例には、repoinit の使用をお勧めします。

* repoinit では、起動時にリソースを作成して、それらのリソースの存在を前提としたロジックが可能になるようにします。可変コンテンツパッケージのアプローチでは、リソースは起動後に作成されるので、リソースを利用したアプリケーションコードは失敗する可能性があります。
* 実行されるアクションを明示的に制御するので、repoinit は比較的安全な命令セットです。また、ユーザー、サービスユーザー、グループの削除が可能なセキュリティ関連のいくつかの場合を除き、追加的な操作のみサポートされています。これに対して、可変コンテンツパッケージのアプローチでは、何かの削除は明示的な操作になります。つまり、フィルターを定義すると、フィルターの適用対象となるすべてのものが削除されます。しかし、どのようなコンテンツでも、新しいコンテンツの存在でアプリケーションの動作が変わる可能性があるシナリオが考えられるので、やはり注意が必要です。
* repoinit は高速かつアトミックな操作を実行します。これに対して、可変コンテンツパッケージでは、フィルターの適用対象となる構造によってパフォーマンスが大きく左右される場合があります。1 つのノードだけを更新した場合でも、大きなツリーのスナップショットが作成される可能性があります。
* repoinit ステートメントは OSGi 設定が登録されると実行されるので、ローカル開発環境で実行時に repoinit ステートメントを検証できます。
* repoinit ステートメントはアトミックかつ明示的で、状態が既に一致している場合はスキップされます。

Cloud Manager がアプリケーションをデプロイすると、コンテンツパッケージのインストールとは無関係に、これらのステートメントが実行されます。

repoinit ステートメントを作成するには、次の手順に従います。

1. ファクトリ PID の OSGi 設定 `org.apache.sling.jcr.repoinit.RepositoryInitializer` をプロジェクトの設定フォルダーに追加します。設定には、**org.apache.sling.jcr.repoint.RepositoryInitializer～initstructure** など、わかりやすい名前を付けます。
1. 設定のスクリプトプロパティに repoinit ステートメントを追加します。構文とオプションについては、[Sling のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html)を参照してください。なお、子フォルダーの前に親フォルダーを明示的に作成する必要があります。例えば、`/content` を明示的に作成してから `/content/myfolder` を作成し、その後に `/content/myfolder/mysubfolder` を作成します。ACL を下位レベルの構造に設定する場合は、ACL を上位レベルに設定し、`rep:glob` 制限を適用することをお勧めします。例えば、`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))` のように指定します。
1. 実行時にローカル開発環境で検証します。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>ACL が `/apps` または `/libs` の下位ノードに定義された場合、repoinit ステートメントの実行は空のリポジトリで開始されます。repoinit ステートメントの実行後にパッケージがインストールされるので、ステートメントでは、パッケージ内で定義されたものを使用できませんが、親構造などの前提条件を定義する必要があります。

>[!TIP]
>
>ACL の場合、深い構造の作成は面倒な作業になる可能性があるので、上位レベルで ACL を定義し、rep:glob 制限を使用して ACL の適用範囲を制約するほうが合理的です。

repoinit について詳しくは、[Sling のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html)を参照してください。

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可変コンテンツパッケージに対するパッケージマネージャーの「1 回限り」の使用 {#package-manager-oneoffs-for-mutable-content-packages}

コンテンツパッケージを「1 回限りのもの」としてインストールする必要がある場合が考えられます。例えば、実稼動環境での問題をデバッグするために、実稼動環境からステージング環境に特定のコンテンツを読み込む場合などです。これらのシナリオでは、AEM as a Cloud Service 環境でパッケージマネージャーを使用できます。

パッケージマネージャーは実行時の概念なので、不変リポジトリにコンテンツやコードをインストールすることはできません。そのため、これらのコンテンツパッケージは可変コンテンツ（主に `/content` または `/conf`）のみで構成する必要があります。コンテンツパッケージに混在コンテンツ（可変コンテンツと不変コンテンツの両方）が含まれている場合、可変コンテンツのみインストールされます。

Cloud Manager を使用してインストールされたコンテンツパッケージ（可変および不変）は、AEM パッケージマネージャーのユーザーインターフェイスにフリーズ状態で表示されます。これらのパッケージは再インストールや再ビルド、さらにはダウンロードもできません。また、「**cp2fm**」というサフィックス付きで表示され、そのインストールが Cloud Manager で管理されていることを示します。

### サードパーティパッケージの組み込み {#including-third-party}

アドビの翻訳パートナーを始めとするソフトウェアベンダーなどのサードパーティから提供される事前ビルド済みパッケージを組み込むことがよくあります。これらのパッケージをリモートリポジトリでホストし、それらを `pom.xml` で参照することをお勧めします。これは、パブリックリポジトリと、パスワード保護Mavenリポジトリで説明されているパスワード保護を持つプライベートリポジトリに対しても可能で [](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)す。

パッケージをリモートリポジトリに格納できない場合は、ファイルシステムベースのローカルの Maven リポジトリに保存できます。このリポジトリは、プロジェクトの一環として SCM にコミットされ、利用元から参照されます。このリポジトリは、プロジェクトの POM で次の例のように宣言されます。


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

組み込まれるサードパーティパッケージはすべて、ここで説明している AEM as a Cloud Service のコーディングおよびパッケージングガイドラインに従う必要があります。従わない場合は、パッケージを組み込むとデプロイメントに失敗します。

Maven プラグイン設定 **filevault-package-maven-plugin** を使用してサードパーティパッケージをプロジェクトの「コンテナ」パッケージ（通常は、「**all**」）に埋め込む方法を、次の Maven POM XML スニペットで示します。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## ローリングデプロイメントの仕組み {#how-rolling-deployments-work}

AEM のアップデートと同様に、お客様向けリリースも、適切な状況下でのオーサークラスターのダウンタイムをなくすために、ローリングデプロイメント戦略を使用してデプロイされます。イベントの一般的なシーケンスは、以下に示すとおりです。ここで、**ブルー**&#x200B;は顧客コードの古いバージョン、**グリーン**&#x200B;は顧客コードの新しいバージョンです。ブルーとグリーンの両方で同じバージョンの AEM コードが実行されています。

* ブルーバージョンがアクティブで、グリーンのリリース候補がビルドされ使用可能です。
* 新しいまたは更新されたインデックス定義がある場合は、対応するインデックスが処理されます。なお、ブルーデプロイメントでは常に古いインデックスが使用されるのに対して、グリーンデプロイメントでは常に新しいインデックスが使用されます。
* ブルーがまだサービスを提供している間にグリーンが起動します。
* ヘルスチェックを通じてグリーンの対応準備状況を確認している間は、ブルーが実行中でサービスを提供しています。
* 対応準備ができたグリーンノードがトラフィックを引き受け、ブルーノードに取って代わります。ブルーノードは停止します。
* 時間が経つにつれて、ブルーノードがグリーンノードに置き換えられ、グリーンノードだけが残るようになったら、デプロイメントが完了します。
* 新しいまたは変更された可変コンテンツがデプロイされます。

## インデックス {#indexes}

新しいまたは変更されたインデックスがあると、インデックスの追加作成または再作成の手順がおこなわれてから、新しいバージョン（グリーンバージョン）でトラフィックを引き受けることができるようになります。Skyline でのインデックス管理について詳しくは、[こちら](/help/operations/indexing.md)を参照してください。Cloud Manager のビルドページで、インデックス作成ジョブのステータスを確認できます。新しいバージョンでトラフィックを引き受ける準備ができたら、通知を受け取ります。

>[!NOTE]
>
>ローリングデプロイメントに必要な時間は、インデックスのサイズによって異なります。新しいインデックスが生成されるまで、グリーンバージョンではトラフィックを引き受けられないからです。

現時点では、Skyline はインデックス管理ツール（ACS AEM Commons の Ensure Oak Index ツールなど）とは連携して動作しません。

## レプリケーション {#replication}

公開メカニズムは、[AEM レプリケーション Java API](https://helpx.adobe.com/jp/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html) と後方互換性があります。

クラウド対応の AEM クイックスタートでレプリケーションを使用して開発およびテストをおこなうには、従来のレプリケーション機能をオーサー／パブリッシュ設定で使用する必要があります。クラウドで AEM オーサーの UI エントリポイントが削除された場合、ユーザーは `http://localhost:4502/etc/replication` にアクセスして設定をおこないます。

## ローリングデプロイメントに対応する後方互換コード {#backwards-compatible-code-for-rolling-deployments}

前述のように、AEM as a Cloud Service のローリングデプロイメント戦略は、古いバージョンと新しいバージョンの両方が同時に動作する可能性があることを意味しています。したがって、まだ運用中の古い AEM バージョンとの後方互換性がないコード変更には注意が必要です。

また、ロールバック時には、可変コンテンツが削除されないので、新しいリリースで適用された新しい可変コンテンツ構造との互換性が古いリリースにあるかどうかをテストする必要があります。

### サービスユーザーと ACL の変更 {#service-users-and-acl-changes}

コンテンツやコードへのアクセスに必要なサービスユーザーや ACL を変更すると、古い AEM バージョンでエラーが発生し、その結果、古いサービスユーザーでコンテンツやコードにアクセスすることになるおそれがあります。この動作に対処するには、少なくとも 2 つのリリースに分散して変更をおこない、最初のリリースをブリッジとして機能させてから、後続のリリースでクリーンアップをおこなうことをお勧めします。

### インデックスの変更 {#index-changes}

インデックスに変更を加えた場合、ブルーバージョンは終了するまで現在のインデックスを引き続き使用するのに対して、グリーンバージョンは自分自身の変更済みのインデックスセットを使用します。開発者は、[この記事](/help/operations/indexing.md)で説明しているインデックス管理手法に従う必要があります。

### ロールバックに備えた保守的なコーディング {#conservative-coding-for-rollbacks}

デプロイメント後にエラーが報告または検出された場合は、ブルーバージョンへのロールバックが必要になる可能性があります。新しい構造（可変コンテンツ）はロールバックされないので、ブルーコードとグリーンバージョンで作成された新しい構造との互換性を確保することをお勧めします。古いコードに互換性がない場合は、それ以降のお客様向けリリースで修正を適用する必要があります。

## 実行モード {#runmodes}

既存の AEM ソリューションでは、お客様は任意の実行モードでインスタンスを実行することができ、それらの特定のインスタンスに OSGi 設定を適用したり OSGi バンドルをインストールしたりできます。定義されている実行モードには、通常、*サービス*（author および publish）と環境（dev、stage、prod）があります。

一方、AEM as a Cloud Service は、使用可能な実行モードと、それらへの OSGi バンドルおよび OSGi 設定のマッピング方法について、より保守的です。

* OSGi 設定の実行モードでは、環境については dev（開発）、stage（ステージ）、prod（実稼動）のいずれかを、サービスについては author（オーサー）または publish（パブリッシュ）を参照する必要があります。`<service>.<environment_type>` の組み合わせはサポートされていますが、この特定の順序で使用する必要があります（例えば、`author.dev` や `publish.prod` など）。OSGi トークンは、`getRunModes` メソッドを使用するのではなく、コードから直接参照する必要があります。このメソッドは、実行時に `environment_type` を組み込まなくなりました。詳しくは、[AEM as a Cloud Service の OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。
* OSGi バンドルの実行モードは、サービス（author、publish）のみに制限されます。実行モードごとに、OSGi バンドルを `install/author` または `install/publish` の配下のコンテンツパッケージにインストールする必要があります。

既存の AEM ソリューションと同様に、実行モードを使用して特定の環境やサービス用のコンテンツだけをインストールすることはできません。ステージ環境または実稼動環境にないデータや HTML を含んだ開発環境をシードする必要がある場合は、パッケージマネージャーを使用できます。

サポートされている実行モード設定は次のとおりです。

* **config**（*デフォルト。すべての AEM サービスに適用*）
* **config.author**（*すべての AEM オーサーサービスに適用*）
* **config.author.dev**（*開発環境の AEM オーサーサービスに適用*）
* **config.author.stage**（*ステージング環境の AEM オーサーサービスに適用*）
* **config.author.prod**（*実稼動環境の AEM オーサーサービスに適用*）
* **config.publish**（*AEM パブリッシュサービスに適用*）
* **config.publish.dev**（*開発環境の AEM パブリッシュサービスに適用*）
* **config.publish.stage**（*ステージング環境の AEM パブリッシュサービスに適用*）
* **config.publish.prod**（*実稼動環境の AEM パブリッシュサービスに適用*）
* **config.dev**（開発環境の AEM サービスに適用）
* **config.stage**（ステージング環境の AEM サービスに適用）
* **config.prod**（実稼動環境の AEM サービスに適用）

最も一致する実行モードを持つ OSGi 設定が使用されます。

ローカルで開発する場合は、実行モード起動パラメーターを渡して、使用する実行モード OSGi 設定を指定できます。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## ソース管理下のメンテナンスタスク設定 {#maintenance-tasks-configuration-in-source-control}

**ツール／操作**&#x200B;画面はクラウド環境では使用できなくなったので、メンテナンスタスク設定をソース管理下に置く必要があります。これにより、変更が事後対応的に適用される（場合によっては忘れてしまう）のではなく、必ず意図的に保存されるというメリットがあります。詳しくは、[メンテナンスタスク](/help/operations/maintenance.md)の記事を参照してください。
