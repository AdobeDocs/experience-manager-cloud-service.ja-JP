---
title: Cloud Manager に関する FAQ
description: AEM as a Cloud Serviceの Cloud Manager に関するよくある質問への回答を見つけます。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 5f4bbedaa5c4630d6f955bb0986e8b32444d6aa3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 21%

---


# Cloud Manager FAQ {#cloud-manager-faqs}

このドキュメントでは、AEM as a Cloud Serviceの Cloud Manager に関するよくある質問に対する回答を示します。

## Cloud Manager ビルドで Java 11 を使用することは可能ですか？ {#java-11-cloud-manager}

はい。次の項目を追加する必要があります： `maven-toolchains-plugin` Java 11 用の適切な設定を使用して、

* これについては、 [ここ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).
* 例えば、 [wknd プロジェクトのサンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## Java 8 から Java 11 に切り替えた後、maven-scr-plugin に関するエラーでビルドが失敗します。 何ができる？ {#build-fails-maven-scr-plugin}

ビルドを Java 8 から 11 に切り替えようとすると、AEM Cloud Manager のビルドが失敗する場合があります。 次のエラーが発生した場合は、 `maven-scr-plugin` すべての OSGi 注釈を OSGi R6 注釈に変換します。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

このプラグインの削除方法については、 [こちら。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## Java 8 から Java 11 に切り替えた後、RequireJavaVersion に関するエラーでビルドが失敗しました。 何ができる？ {#build-fails-requirejavaversion}

Cloud Manager ビルドの場合、 `maven-enforcer-plugin` は失敗し、このエラーが表示されます。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

これは既知の問題です。Cloud Manager では、maven コマンドの実行に、コードをコンパイルした際と異なるバージョンの Java を使用しているためです。単に省略する `requireJavaVersion` から `maven-enforcer-plugin` 設定。

## コード品質チェックに失敗し、デプロイメントが停止しています。 このチェックを回避する方法はありますか？ {#deployment-stuck}

はい。セキュリティ評価を除くすべてのコード品質チェックの失敗は、重要でない指標なので、結果 UI の項目を展開することで回避できます。

ドキュメントを参照 [コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md) を参照してください。

## Maven プロジェクトのバージョンに SNAPSHOT を使用できますか？ {#use-snapshot}

はい。デベロッパーデプロイメントの場合、Git ブランチ `pom.xml` ファイルに含める必要がある `-SNAPSHOT` ～の終わりに `<version>` の値です。

これにより、バージョンが変更されなかった場合でも、以降のデプロイメントを引き続きインストールできます。 デベロッパーデプロイメントでは、maven ビルドの自動バージョンは追加または生成されません。

また、バージョンを `-SNAPSHOT` ステージング環境および実稼動環境のビルドまたはデプロイメントの場合。 Cloud Manager は適切なバージョン番号を自動的に設定し、Git でタグを作成します。 このタグは、必要に応じて後で参照できます。

## パッケージとバンドルのバージョン管理は、ステージング環境および実稼動環境でのデプロイメントでどのように機能しますか？ {#snapshot-version}

ステージおよび実稼動環境でのデプロイメントでは、自動バージョンは [ここで説明します。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

ステージおよび実稼動環境でのデプロイメントのカスタムバージョン管理の場合は、次のような適切な 3 部構成の Maven バージョンを設定します。 `1.0.0`. 実稼動環境にデプロイするたびに、バージョンを増やします。

Cloud Manager は、ステージビルドと実稼動ビルドにバージョンを自動的に追加し、Git ブランチを作成します。 特別な設定は必要ありません。前述のように Maven バージョンを設定しない場合、デプロイメントは成功し、バージョンが自動的に設定されます。

## Cloud Manager デプロイメントで Maven ビルドが失敗しましたが、エラーなくローカルにビルドされます。 どうしたの？ {#maven-build-fail}

詳しくは、 [この git リソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) を参照してください。

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

この `sling-distribution-importer` ユーザーには、 `ui.content package`.  これは通常、 `/conf` および `/var`.

解決策は、 [RepositoryInitializer OSGi 設定](/help/implementing/deploying/overview.md#repoint) スクリプトをアプリデプロイメントパッケージに追加して、 `sling-distribution-importer` ユーザー。

前の例のエラーでは、パッケージ `myapp-base.ui.content-*.zip` 次のコンテンツを含む `/conf` および `/var/workflow`. デプロイメントを成功させるには、 `sling-distribution-importer` その下に必要なパスがあります。

 ユーザーの権限を追加するこのような OSGi 設定の例として、[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) を紹介します。`sling-distribution-importer`この設定により、 `/var`.  [1] の下にあるこの xml ファイルを `/apps/myapp/config` の下のアプリケーションパッケージに追加する必要があります（myapp はアプリケーションコードが格納されているフォルダー）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

## AEM as a Cloud Serviceのデプロイ手順で Cloud Manager のデプロイメントが失敗し、既に RepositoryInitializer OSGi 設定になっています。 他に何ができる？ {#build-failures}

If [RepositoryInitializer OSGi 設定の追加](##cloud-manager-deployment-cloud-service) がエラーを解決しなかった場合は、これらの追加の問題の 1 つが原因である可能性があります。

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
