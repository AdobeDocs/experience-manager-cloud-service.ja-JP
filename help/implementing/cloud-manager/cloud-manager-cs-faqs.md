---
title: Cloud Manager に関する FAQ
description: AEM as a Cloud Serviceの Cloud Manager に関するよくある質問への回答を見つけます。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 11ac22974524293ce3e4ceaa26e59fe75ea387e6
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 21%

---


# Cloud Manager FAQ {#cloud-manager-faqs}

このドキュメントでは、AEM as a Cloud Serviceの Cloud Manager に関するよくある質問に対する回答を示します。

## Cloud Manager ビルドで Java 11 を使用することは可能ですか？ {#java-11-cloud-manager}

ビルドを Java 8 から 11 に切り替えようとすると、AEM Cloud Manager のビルドが失敗する場合があります。 この問題には多くの原因があり、最も一般的な原因はこの節に記載されています。

* を `maven-toolchains-plugin` Java 11 用の適切な設定を使用して、
   * これについては、 [ここ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).
   * 例えば、 [wknd プロジェクトのサンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

* 次のエラーが発生した場合は、 `maven-scr-plugin` すべての OSGi 注釈を OSGi R6 注釈に変換します。
   * 手順については、 [こちら。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/).

   ```text
   [main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
   ```

* Cloud Manager ビルドの場合、 `maven-enforcer-plugin` エラーで失敗 `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`. これは既知の問題です。Cloud Manager では、maven コマンドの実行に、コードをコンパイルした際と異なるバージョンの Java を使用しているためです。ひとまず、 設定から `requireJavaVersion` を省略します。`maven-enforcer-plugin`

## コード品質チェックに失敗し、デプロイメントが停止しています。 このチェックを回避する方法はありますか？ {#deployment-stuck}

セキュリティ評価を除くすべてのコード品質チェックの失敗は、重要でない指標なので、結果 UI の項目を展開することで回避できます。

ユーザーの [デプロイメントマネージャー、プログラムマネージャー、またはビジネスオーナー](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md) の役割は、問題を上書きできます。この場合、パイプラインは続行します。 また、これらのの使用では問題を受け入れることができます。問題が発生した場合、パイプラインは停止します。

ドキュメントを参照 [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md) を参照してください。

## Maven プロジェクトのバージョンに SNAPSHOT を使用できますか？ ステージング環境および実稼動環境でのデプロイメントで、パッケージとバンドル jar ファイルのバージョン管理はどのように機能しますか？ {#snapshot-version}

次のシナリオでは、ステージング環境および実稼動環境へのデプロイメント用に、パッケージとバンドルの jar ファイルのバージョン管理を扱います。

* デベロッパーデプロイメントの場合、Git ブランチ `pom.xml` ファイルに含める必要がある `-SNAPSHOT` ～の終わりに `<version>` の値です。
   * これにより、バージョンが変更されなかった場合でも、以降のデプロイメントを引き続きインストールできます。 デベロッパーデプロイメントでは、maven ビルドの自動バージョンは追加または生成されません。

* ステージおよび実稼動環境でのデプロイメントでは、自動バージョンは [ここで説明します。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

* ステージおよび実稼動環境でのデプロイメントのカスタムバージョン管理の場合は、次のような適切な 3 部構成の Maven バージョンを設定します。 `1.0.0`. 実稼動環境にデプロイするたびに、バージョンを増やします。

* Cloud Manager は、ステージビルドと実稼動ビルドにバージョンを自動的に追加し、Git ブランチを作成します。 特別な設定は必要ありません。前述のように Maven バージョンを設定しない場合、デプロイメントは成功し、バージョンが自動的に設定されます。

* バージョンを `-SNAPSHOT` ステージ版および実稼動版のビルドまたはデプロイメントで問題なく実行できる場合。 Cloud Manager は適切なバージョン番号を自動的に設定し、Git でタグを作成します。 このタグは、必要に応じて後で参照できます。

* 開発環境で実験的なコードを試す場合は、新しい Git ブランチを作成し、そのブランチを使用するようにパイプラインを設定できます。
   * これは、デプロイメントが失敗し、古いバージョンのコードでテストして、どの変更が失敗を引き起こしたのかを判断する場合に役立ちます。

   * 以下の git コマンドは、という名前のリモートブランチを作成します。 `testbranch1` 既存のコミットに基づく `485548e4fbafbc83b11c3cb12b035c9d26b6532b`.  このブランチは、他のブランチに影響を与えることなく、Cloud Manager で使用できます。

   ```shell
   git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1
   ```

   * 詳しくは、 [git ドキュメント](https://git-scm.com/book/en/v2/Git-Internals-Git-References) を参照してください。

   * 後でテストブランチを削除する場合は、次の delete コマンドを使用します。

   ```shell
   git push origin --delete testbranch1
   ```

## Cloud Manager デプロイメントで Maven ビルドが失敗しましたが、エラーなくローカルにビルドされます。 どうしたの？ {#maven-build-fail}

詳しくは、[Git リソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEM as a Cloud Serviceのデプロイ手順で Cloud Manager のデプロイメントが失敗した場合は、どうすればよいですか？ {#cloud-manager-deployment-cloud-service}

デプロイメントが失敗する最も一般的な理由は、 `sling-distribution-importer` ユーザー。 この場合、Cloud Manager のデプロイメント中にデプロイ手順が失敗し、次のようなエラーが生成されます。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

この場合、 `sling-distribution-importer` ユーザーには、 `ui.content package`.  これは通常、 `/conf` および `/var`.

解決策は、 [RepositoryInitializer OSGi 設定](/help/implementing/deploying/overview.md#repoint) スクリプトをアプリデプロイメントパッケージに追加して、 `sling-distribution-importer` ユーザー。

前の例のエラーでは、パッケージ `myapp-base.ui.content-*.zip` 次のコンテンツを含む `/conf` および `/var/workflow`. デプロイメントを成功させるには、 `sling-distribution-importer` その下に必要なパスがあります。

 ユーザーの権限を追加するこのような OSGi 設定の例として、[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) を紹介します。`sling-distribution-importer`この設定により、 `/var`.  [1] の下にあるこの xml ファイルを `/apps/myapp/config` の下のアプリケーションパッケージに追加する必要があります（myapp はアプリケーションコードが格納されているフォルダー）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

RepositoryInitializer OSGi 設定を追加してもエラーが解決しなかった場合は、次の追加の問題の 1 つが原因である可能性があります。

* 標準のサービスを中断する無効な OSGi 設定が原因で、デプロイメントが失敗する可能性があります。
   * デプロイ時のログを調べて、明らかなエラーがないかどうかを確認します。

* Dispatcher または Apache の設定が正しくないため、デプロイメントが失敗する可能性があります。
   * SDK に含まれる Docker イメージを使用して、Apache および Dispatcher の設定をローカルでテストしてください。
   * ローカルテストを簡単に行うための Dispatcher Docker コンテナの設定方法については、[クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery) を参照してください。

* オーサーインスタンスからパブリッシュインスタンスへのコンテンツパッケージ（Sling 配布）のレプリケーション中に、他のエラーが発生したため、デプロイメントが失敗する場合があります。
   * ローカル設定での問題をシミュレートするには、次の手順に従います。
      1. 最新のAEM SDK JAR を使用して、オーサーインスタンスとパブリッシュインスタンスをローカルにインストールします。
      1. オーサーインスタンスにログインします。
      1. に移動します。 **ツール** -> **導入** -> **配布**.
      1. コードベースの一部であるコンテンツパッケージを配布し、キューがエラーでブロックされたかどうかを確認します。

## aio コマンドを使用して変数を設定できません。 何ができる？ {#set-variable}

以下を受け取ることができます： `403` 経由でパイプライン変数をリストまたは設定しようとした場合に次のようなエラーが発生しました `aio` コマンド

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

この場合、これらのコマンドを実行するユーザーを **デプロイメント管理** Admin Consoleの

詳しくは、[API の権限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)を参照してください。
