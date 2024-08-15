---
title: AEM as a Cloud Service へのデプロイ
description: AEM as a Cloud Service へのデプロイの基本とベストプラクティスについて説明します。
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '3441'
ht-degree: 97%

---

# AEM as a Cloud Service へのデプロイ {#deploying-to-aem-as-a-cloud-service}

## はじめに {#introduction}

AEM as a Cloud Service でのコード開発の基本は、AEM On Premise や Managed Services ソリューション上の AEM の場合と同様です。開発者はコードを作成しローカルでテストします。コードはその後、AEM as a Cloud Service のリモート環境にプッシュされます。Cloud Manager（Managed Services のオプションのコンテンツ配信ツール）が必要です。この配信ツールは、AEM as a Cloud Service 開発、ステージ、および実稼動環境にコードをデプロイするための唯一のメカニズムになりました。前述の環境をデプロイする前に、機能の検証とデバッグを迅速に行うために、コードをローカル環境から[迅速な開発環境](/help/implementing/developing/introduction/rapid-development-environments.md)に同期できます。

[AEM バージョン](/help/implementing/deploying/aem-version-updates.md)のアップデートは、常に、[カスタムコード](#customer-releases)のプッシュとは別のデプロイメントイベントになります。別の見方をすれば、カスタムコードリリースは実稼動環境にある AEM バージョンに照らしてテストする必要があります。カスタムコードがその AEM 上にデプロイされるからです。その後に発生する AEM バージョンの更新で、頻繁に自動的に適用されます。これらは、既に導入されている顧客コードとの後方互換性を保つためのものです。

このドキュメントの残りの部分では、AEM as a Cloud Service のバージョンアップデートと顧客側でのアップデートの両方に対応できるように、開発者が開発のベストプラクティスをどのように適応させるべきかについて説明します。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## お客様向けリリース {#customer-releases}

### 適切な AEM バージョンに照らしたコーディング {#coding-against-the-right-aem-version}

これまでの AEM ソリューションでは、最新の AEM バージョンが頻繁に（およそ年 1 回、四半期ごとにサービスパックをリリース）変更され、顧客側では、API JAR を参照して、都合の良いときに実稼動インスタンスを最新のクイックスタートに更新するという形でした。しかし、AEM as a Cloud Service 上のアプリケーションは、より頻繁に最新バージョンの AEM に自動更新されるので、内部リリースのカスタムコードは、最新の AEM バージョンに対応するように作成する必要があります。

既存の非クラウド AEM バージョンと同様に、特定のクイックスタートに基づくローカルのオフライン開発がサポートされ、通常はデバッグに最適なツールとなることが期待されています。

>[!NOTE]
>ローカルマシン上と Adobe Cloud 上のアプリケーションの動作には、運用上のわずかな違いがあります。これらのアーキテクチャの違いは、ローカル開発時に考慮される必要があり、結果的に、クラウドインフラストラクチャにデプロイしたときに動作が異なることになる可能性があります。こうした違いがあるので、実稼動環境で新しいカスタムコードをロールアウトする前に、開発環境とステージ環境で徹底的なテストを実行することが重要です。

内部リリースのカスタムコードを開発するには、[AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) の関連バージョンをダウンロードし、インストールする必要があります。AEM as a Cloud Service Dispatcher Tools の使用について詳しくは、[Cloud のDispatcher](/help/implementing/dispatcher/disp-overview.md) を参照してください。

次のビデオでは、AEM as a Cloud Service にコードをデプロイする方法の概要を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## Cloud Manager およびパッケージマネージャーを使用したコンテンツパッケージのデプロイ {#deploying-content-packages-via-cloud-manager-and-package-manager}

### Cloud Manager を使用したデプロイメント {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

お客様は、Cloud Manager を使用してカスタムコードをクラウド環境にデプロイします。Cloud Manager は、ローカルでアセンブルされたコンテンツパッケージを Sling Feature Model に準拠したアーティファクトに変換します（このモデルは、クラウド環境で動作する際の AEM as a Cloud Service 上のアプリケーションを記述するものです）。その結果、クラウド環境の[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)でパッケージを調べると、名前に「cp2fm」が含まれており、変換後のパッケージではすべてのメタデータが削除されています。これらを操作することはできません。つまり、ダウンロードしたり、複製したり、開いたりすることはできません。コンバーターに関する詳細なドキュメントについては、[ を参照してください
github](https://github.com/apache/sling-org-apache-sling-feature-cpconverter) の sling-org-apache-sling-feature-cpconverter。

AEM as a Cloud Service 上のアプリケーション用に作成されたコンテンツパッケージでは、不変コンテンツと可変コンテンツを明確に分離する必要があります。Cloud Manager は可変コンテンツのみインストールし、次のようなメッセージも出力します。

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

この節の残りの部分では、不変パッケージと可変パッケージの構成と関係について説明します。

### 不変コンテンツパッケージ {#immutabe-content-packages}

不変リポジトリーに保存されるコンテンツとコードはすべて、Git にチェックインし、Cloud Manager を通じてデプロイする必要があります。つまり、現在の AEM ソリューションとは異なり、コードは実行中の AEM インスタンスには直接デプロイされません。このワークフローにより、任意のクラウド環境で特定のリリースに対して同一のコードが実行されるようになり、意図しないコード変更が実稼動環境で発生するリスクをなくすことができます。例えば、OSGi 設定は、AEM Web コンソールの設定マネージャーを使用して実行時に管理されるのではなく、ソース管理にコミットする必要があります。

デプロイメントパターンによるアプリケーション変更はスイッチで有効になるので、サービスユーザー、ACL、ノードタイプ、インデックス定義の変更を除き、可変リポジトリ内の変更に依存することはできません。

既存のコードベースをお持ちのお客様は、AEM ドキュメントに記載されているリポジトリー再構築の演習を完了して、以前 /etc の配下にあったコンテンツが適切な場所に確実に移動されるようにすることが重要です。

これらのコードパッケージには、いくつかの追加の制限が適用されます。例えば、[インストールフック](https://jackrabbit.apache.org/filevault/installhooks.html)はサポートされません。

## OSGi 設定 {#osgi-configuration}

前述のように、OSGi 設定は Web コンソールを通じて管理するのではなく、ソース管理にコミットする必要があります。そのための手法は次のとおりです。

* AEM Web コンソールの Configuration Manager を使用して開発者のローカル AEM 環境に必要な変更を加えた後、その結果をローカルファイルシステム上の AEM プロジェクトに書き出す。
* ローカルファイルシステム上の AEM プロジェクトに OSGi 設定を手動で作成した後、AEM コンソールの Configuration Manager でプロパティ名を参照する。

OSGI の設定について詳しくは、[AEM as a Cloud Service の OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。

## 可変コンテンツ {#mutable-content}

場合によっては、環境が更新されるたびに Cloud Manager でデプロイできるように、ソース管理でコンテンツの変更を準備すると便利なことがあります。例えば、特定のルートフォルダー構造をシードするのが妥当な場合があります。または、変更を編集可能なテンプレートに並べて、アプリケーションのデプロイメントによって更新されたポリシーコンポーネントを有効にします。

Cloud Manager で可変リポジトリにデプロイされるコンテンツ、可変コンテンツパッケージ、 `repoinit` ステートメントを記述する戦略は 2 通りあります。

### 可変コンテンツパッケージ {#mutable-content-packages}

フォルダーパス階層、サービスユーザー、アクセス制御（ACL）などのコンテンツは、通常、Maven アーキタイプベースの AEM プロジェクトにコミットされます。使用される手法には、AEM からの書き出し、または XML 形式での直接書き込みがあります。ビルドおよびデプロイメントプロセス中に、Cloud Manager は、生成された可変コンテンツパッケージをパッケージ化します。可変コンテンツは、パイプラインのデプロイフェーズで次の 3 回の異なるタイミングでインストールされます。

新しいバージョンのアプリケーションの起動前：

* インデックス定義（追加、変更、削除）

新しいバージョンのアプリケーションの起動中（切り替えの前）：

* サービスユーザー（追加）
* サービスユーザー ACL（追加）
* ノードタイプ（追加）

新しいバージョンのアプリケーションへの切り替え後：

* Jackrabbit Vault を使用して定義可能なその他のすべてのコンテンツ。次に例を示します。
   * フォルダー（追加、変更、削除）
   * 編集可能なテンプレート（追加、変更、削除）
   * コンテキスト対応の設定（`/conf` 配下のあらゆるもの）（追加、変更、削除）
   * スクリプト（パッケージは、パッケージのインストールプロセスの様々な段階でインストールフックをトリガーできます）インストールフックについては、[Jackrabbit FileVault のドキュメント](https://jackrabbit.apache.org/filevault/installhooks.html)を参照してください。AEM as a Cloud Service では現在、FileVault バージョン 3.4.0 を使用しています（インストールフックの使用は管理者ユーザー、システムユーザー、管理者グループのメンバーに限定されています）。

`/apps` 配下の install.author フォルダーまたは install.publish フォルダーにパッケージを埋め込むことで、可変コンテンツのインストールをオーサーまたはパブリッシュのみに制限することができます。この分離を反映した再構築は AEM 6.5 で行われました。推奨されるプロジェクト再構築の詳細については、 [AEM 6.5 のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=ja) を参照してください。

>[!NOTE]
>コンテンツパッケージは、すべての環境タイプ（開発、ステージ、実稼動）にデプロイされます。デプロイメントを特定の環境に限定することはできません。この制限があるのは、自動実行のテスト実行オプションが確実に適用されるようにするためです。環境に固有のコンテンツは、[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)を使用して手動でインストールする必要があります。

また、可変コンテンツパッケージの変更を適用後にロールバックする仕組みはありません。問題を検出した場合は、次回のコードリリースで修正するか、最後の手段としてシステム全体をデプロイメント前の時点に復元するかを選択できます。

サードパーティパッケージが含まれている場合は、それらが AEM as a Cloud と互換性があるかどうかを検証する必要があります。互換性がない場合は、それらのパッケージを組み込むとデプロイメントに失敗します。

前述のように、コードベースが既にある場合は、[AEM 6.5 のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html?lang=ja)に記載されている 6.5 リポジトリの変更に伴うリポジトリ再構築演習に準拠する必要があります。

## repoinit {#repoinit}

次の場合は、OSGi ファクトリ設定で明示的なコンテンツ作成用の `repoinit` ステートメントを手動でコーディングするアプローチを取ることをお勧めします。

* サービスユーザーの作成／削除／無効化
* グループの作成／削除
* ユーザーの作成／削除
* ACL の追加

  >[!NOTE]
  >
  >ACL の定義では、ノード構造が既に存在する必要があります。そのため、先行するパス作成ステートメントが必要になる場合があります。

* パスの追加（例えば、ルートフォルダー構造用）
* CND の追加（ノードタイプ定義）

次の利点があるので、サポートされているこれらのコンテンツ変更使用例には、repoinit の使用をお勧めします。

* `Repoinit` では、起動時にリソースを作成して、それらのリソースの存在を前提としたロジックが可能になるようにします。可変コンテンツパッケージのアプローチでは、リソースは起動後に作成されるので、リソースを利用したアプリケーションコードは失敗する可能性があります。
* 実行されるアクションを明示的に制御するので、`Repoinit` は比較的安全な命令セットです。また、ユーザー、サービスユーザー、グループの削除が可能なセキュリティ関連のいくつかの場合を除き、追加的な操作のみサポートされています。これに対して、可変コンテンツパッケージのアプローチでは、何かの削除は明示的な操作になります。つまり、フィルターを定義すると、フィルターの適用対象となるすべてのものが削除されます。しかし、どのようなコンテンツでも、新しいコンテンツの存在でアプリケーションの動作が変わる可能性があるシナリオが考えられるので、やはり注意が必要です。
* `Repoinit` は高速かつアトミックな操作を実行します。これに対して、可変コンテンツパッケージでは、フィルターの適用対象となる構造によってパフォーマンスが大きく左右される場合があります。1 つのノードだけを更新した場合でも、大きなツリーのスナップショットが作成される可能性があります。
* `repoinit` ステートメントは OSGi 設定が登録されると実行されるので、ローカル開発環境で実行時に repoinit ステートメントを検証できます。
* `Repoinit` ステートメントはアトミックかつ明示的で、状態が既に一致している場合はスキップされます。

Cloud Manager がアプリケーションをデプロイすると、コンテンツパッケージのインストールとは無関係に、これらのステートメントが実行されます。

`repoinit` ステートメントを作成するには、次の手順に従います。

1. ファクトリ PID の OSGi 設定 `org.apache.sling.jcr.repoinit.RepositoryInitializer` をプロジェクトの設定フォルダーに追加します。設定には、**org.apache.sling.jcr.repoint.RepositoryInitializer～initstructure** など、わかりやすい名前を付けます。
1. 設定のスクリプトプロパティに `repoinit` ステートメントを追加します。構文とオプションについては、 [Sling のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html) を参照してください。子フォルダーの前に親フォルダーを明示的に作成する必要があります。例えば、`/content` を明示的に作成してから `/content/myfolder` を作成し、その後に `/content/myfolder/mysubfolder` を作成します。ACL を下位レベルの構造に設定する場合は、ACL を上位レベルに設定し、`rep:glob` 制限を適用することをお勧めします。例：`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`
1. 実行時にローカル開発環境で検証します。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>ACL が `/apps` または `/libs` の下位ノードに定義された場合、`repoinit` の実行は空のリポジトリで開始されます。`repoinit` の実行後にパッケージがインストールされるので、ステートメントでは、パッケージ内で定義されたものを使用できませんが、親構造などの前提条件を定義する必要があります。

>[!TIP]
>
>ACL の場合、深い構造の作成が面倒な場合があります。したがって、ACL をより高いレベルで定義し、`rep:glob` 制限によって動作する場所を制限する方が合理的です。

`repoinit` について詳しくは、[Sling のドキュメントを参照してください](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可変コンテンツパッケージに対するパッケージマネージャーの「1 回限り」の使用 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="パッケージマネージャー - 可変コンテンツパッケージの移行"
>abstract="コンテンツパッケージを「1 回限り」としてインストールするユースケースへのパッケージマネージャーの使用方法を説明します。インストールには、実稼動環境での問題をデバッグするために実稼動環境からステージング環境に特定のコンテンツを読み込む場合や、オンプレミス環境から AEM Cloud 環境に小規模なコンテンツパッケージを転送する場合などが含まれます。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=ja" text="コンテンツ転送ツール"

コンテンツパッケージを「1 回限りのもの」としてインストールする必要がある場合が考えられます。例えば、実稼動環境での問題をデバッグするために、実稼動環境からステージング環境に特定のコンテンツを読み込む場合などです。これらのシナリオでは、AEM as a Cloud Service 環境で[パッケージマネージャー](/help/implementing/developing/tools/package-manager.md)を使用できます。

パッケージマネージャーは実行時の概念なので、不変リポジトリにコンテンツやコードをインストールすることはできません。そのため、これらのコンテンツパッケージは可変コンテンツ（主に `/content` または `/conf`）のみで構成する必要があります。コンテンツパッケージに混在コンテンツ（可変コンテンツと不変コンテンツの両方）が含まれている場合、可変コンテンツのみインストールされます。

>[!IMPORTANT]
>
>パッケージのインストールに 10 分以上かかる場合は、パッケージマネージャーのユーザーインターフェイスで **未定義** のエラーメッセージが返される場合があります。
>
>この時間は、インストールのエラーではなく、すべての要求に対して Cloud Service が持つタイムアウトによるものです。
>
>このようなエラーが表示された場合は、インストールを再試行しないでください。インストールはバックグラウンドで正しく進行しています。インストールを再開すると、複数の同時読み込みプロセスによって競合が発生する可能性があります。

Cloud Manager を使用してインストールされたコンテンツパッケージ（可変および不変）は、AEM パッケージマネージャーのユーザーインターフェイスにフリーズ状態で表示されます。これらのパッケージは再インストールや再ビルド、さらにはダウンロードもできません。また、「**cp2fm**」というサフィックス付きで表示され、そのインストールが Cloud Manager で管理されていることを示します。

### サードパーティ製パッケージを含める {#including-third-party}

アドビの翻訳パートナーを始めとするソフトウェアベンダーなどのサードパーティから提供される事前ビルド済みパッケージを組み込むことがよくあります。これらのパッケージをリモートリポジトリでホストし、それらを `pom.xml` で参照することをお勧めします。このメソッドは、パブリックリポジトリと、[パスワード保護 Maven リポジトリ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)で説明されているパスワード保護を持つプライベートリポジトリに対しても可能です。

パッケージをリモートリポジトリに格納できない場合は、ファイルシステムベースのローカルの Maven リポジトリに保存できます。このリポジトリは、プロジェクトの一環として SCM にコミットされ、利用元から参照されます。このリポジトリは、プロジェクトの POM で次の例のように宣言されます。


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

組み込まれるサードパーティパッケージは、この記事で説明している AEM as a Cloud Service のコーディングとパッケージングのガイドラインに従う必要があります。従わない場合は、パッケージを組み込むとデプロイメントに失敗します。

Maven プラグイン設定 **filevault-package-maven-plugin** を使用してサードパーティパッケージをプロジェクトの「コンテナ」パッケージ（通常は、「**all**」）に埋め込む方法を、次の Maven `POM.xml` スニペットで示します。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## ローリングデプロイメントの仕組み {#how-rolling-deployments-work}

AEM のアップデートと同様に、お客様向けリリースも、適切な状況下でのオーサークラスターのダウンタイムをなくすために、ローリングデプロイメント戦略を使用してデプロイされます。イベントの一般的なシーケンスを以下で説明します。ここでは、顧客コードの古いバージョンと新しいバージョンの両方を持つノードで同じバージョンの AEM コードが実行されます。

* 古いバージョンを持つノードがアクティブになり、新しいバージョンのリリース候補が構築されて使用可能になります。
* 新しいまたは更新されたインデックス定義がある場合は、対応するインデックスが処理されます。古いバージョンのノードでは常に古いインデックスを使用し、新しいバージョンのノードでは常に新しいインデックスを使用します。
* 新しいバージョンが起動するノードで、古いバージョンでは引き続きトラフィックを提供します。
* 古いバージョンのノードは実行中であり、処理を続行します。一方、新しいバージョンのノードは、ヘルスチェックを通じて準備状況を確認します。
* 準備が整った新しいバージョンのノードでトラフィックを受け入れ、ノードを古いバージョンに置き換えます。ノードは停止します。
* 時間が経つと、古いバージョンのノードは、新しいバージョンのノードのみが残るまで、新しいバージョンのノードに置き換えられ、デプロイメントが完了します。
* 新しいまたは変更された可変コンテンツがデプロイされます。

## インデックス {#indexes}

新しいまたは変更されたインデックスがあると、インデックスの追加作成または再作成の手順が行われてから、新しいバージョンでトラフィックを引き受けることができるようになります。AEM as a Cloud Serviceのインデックス管理について詳しくは、[ コンテンツの検索とインデックス作成 ](/help/operations/indexing.md) を参照してください。 Cloud Manager でビルドページのインデックス作成ステータスを確認し、新しいバージョンでトラフィックを引き受ける準備ができたら通知を受け取ることができます。

>[!NOTE]
>
>ローリングデプロイメントに必要な時間は、インデックスのサイズによって異なります。これは、新しいインデックスが生成されるまで、新しいバージョンではトラフィックを受け入れられないためです。

現時点では、AEM as a Cloud Service はインデックス管理ツール（ACS AEM Commons の Ensure Oak Index ツールなど）とは連携して動作しません。

## レプリケーション {#replication}

公開メカニズムは、[AEM レプリケーション Java API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) と後方互換性があります。

クラウド対応の AEM クイックスタートでレプリケーションを使用して開発およびテストを行うには、従来のレプリケーション機能をオーサー／パブリッシュ設定で使用する必要があります。クラウドで AEM オーサーのユーザーインターフェイスエントリポイントが削除された場合、ユーザーは設定のために `http://localhost:4502/etc/replication` に移動します。

## ローリングデプロイメントに対応する後方互換コード {#backwards-compatible-code-for-rolling-deployments}

前述のように、AEM as a Cloud Service のローリングデプロイメント戦略は、古いバージョンと新しいバージョンの両方が同時に動作する可能性があることを意味しています。したがって、まだ運用中の古い AEM バージョンとの後方互換性がないコード変更には注意が必要です。

また、ロールバック時には、可変コンテンツが削除されないので、新しいリリースで適用された新しい可変コンテンツ構造との互換性が古いリリースにあるかどうかをテストする必要があります。

### サービスユーザーと ACL の変更 {#service-users-and-acl-changes}

コンテンツやコードにアクセスするサービスユーザーや ACL を変更すると、古い AEM バージョンでエラーが発生し、その結果、古いサービスユーザーでコンテンツやコードにアクセスするエラーが発生するおそれがあります。この動作に対処するには、少なくとも 2 つのリリースに分散して変更を行い、最初のリリースをリンクとして機能させてから、後続のリリースでクリーンアップを行うことをお勧めします。

### インデックスの変更 {#index-changes}

インデックスに変更を加えた場合、新しいバージョンは終了するまで現在のインデックスを引き続き使用するのに対して、古いバージョンは自分自身の変更済みのインデックスセットを使用します。開発者は、「コンテンツの検索とインデックス作成 [ で説明しているインデックス管理手法に従う必要があ ](/help/operations/indexing.md) ます。

### ロールバックに備えた保守的なコーディング {#conservative-coding-for-rollbacks}

デプロイメント後に失敗が報告または検出された場合は、古いバージョンへのロールバックが必要になる可能性があります。新しい構造（可変コンテンツ）はロールバックされないので、新しいコードが、その新しいバージョンで作成された新しい構造と互換性があることを確認します。古いコードに互換性がない場合は、それ以降のお客様向けリリースで修正を適用する必要があります。

## 迅速な開発環境（RDE） {#rde}

[迅速な開発環境](/help/implementing/developing/introduction/rapid-development-environments.md)（略して RDE）を使用すると、デベロッパーは、ローカル開発環境での動作が既に証明済みの機能に要するテスト時間を最小限に抑え、変更を迅速にデプロイおよびレビューできます。

Cloud Manager パイプラインを使用してコードをデプロイする通常の開発環境とは異なり、デベロッパーはコマンドラインツールを使用してローカル開発環境から RDE にコードを同期できます。変更が RDE で正常にテストされたら、Cloud Manager パイプラインを通じて通常のクラウド開発環境にデプロイします。これにより、コードが適切な品質ゲートを経由します。

## 実行モード {#runmodes}

既存の AEM ソリューションでは、お客様は任意の実行モードでインスタンスを実行することができ、それらの特定のインスタンスに OSGi 設定を適用したり OSGi バンドルをインストールしたりできます。定義されている実行モードには、通常、*サービス*（author および publish）と環境（rde、dev、stage、prod）があります。

一方、AEM as a Cloud Service は、使用可能な実行モードと、それらへの OSGi バンドルおよび OSGi 設定のマッピング方法について、より保守的です。

* OSGi 設定の実行モードでは、環境については RDE（迅速な開発環境）、開発、ステージ、実稼動のいずれかを、サービスについてはオーサーまたはパブリッシュを参照する必要があります。`<service>.<environment_type>` の組み合わせはサポートされていますが、これらの環境は、この特定の順序で使用する必要があります（例えば、`author.dev` や `publish.prod` など）。OSGi トークンは、`getRunModes` メソッドを使用するのではなく、コードから直接参照する必要があります。このメソッドは、実行時に `environment_type` を組み込まなくなりました。詳しくは、[AEM as a Cloud Service の OSGi の設定](/help/implementing/deploying/configuring-osgi.md)を参照してください。
* OSGi バンドルの実行モードは、サービス（author、publish）のみに制限されます。実行モードごとに、OSGi バンドルを `install.author` または `install.publish` の配下のコンテンツパッケージにインストールする必要があります。

AEM as a Cloud Service では、実行モードを使用して特定の環境やサービスのコンテンツをインストールすることはできません。開発環境で、ステージング環境または実稼動環境にないデータや HTML を使用して開発環境をシードする必要がある場合は、パッケージマネージャーを使用できます。

サポートされている実行モード設定は次のとおりです。

* **config**（*デフォルト。すべての AEM サービスに適用*）
* **config.author**（*すべての AEM オーサーサービスに適用*）
* **config.author.dev**（*開発環境の AEM オーサーサービスに適用*）
* **config.author.rde**（*AEM RDE オーサーサービスに適用*）
* **config.author.stage**（*ステージング環境の AEM オーサーサービスに適用*）
* **config.author.prod**（*実稼動環境の AEM オーサーサービスに適用*）
* **config.publish**（*AEM パブリッシュサービスに適用*）
* **config.publish.dev**（*開発環境の AEM パブリッシュサービスに適用*）
* **config.publish.rde**（*AEM RDE パブリッシュサービスに適用*）
* **config.publish.stage**（*ステージング環境の AEM パブリッシュサービスに適用*）
* **config.publish.prod**（*実稼動環境の AEM パブリッシュサービスに適用*）
* **config.dev**（*開発環境の AEM サービスに適用*）
* **config.rde**（*RDE サービスに適用*）
* **config.stage**（*ステージング環境の AEM サービスに適用*）
* **config.prod**（*実稼動環境の AEM サービスに適用*）

最も一致する実行モードを持つ OSGi 設定が使用されます。

ローカルで開発する場合、実行モードの起動パラメーター `-r` を使用して、実行モードの OSGI 設定を指定します。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## ソース管理下のメンテナンスタスク設定 {#maintenance-tasks-configuration-in-source-control}

**ツール／操作**&#x200B;画面はクラウド環境では使用できないので、メンテナンスタスク設定をソース管理下に置く必要があります。このメリットにより、変更が事後対応的に適用され忘れられるのではなく、意図的に保存されるようになります。詳しくは、[AEM as a Cloud Serviceのメンテナンスタスク ](/help/operations/maintenance.md) を参照してください。
