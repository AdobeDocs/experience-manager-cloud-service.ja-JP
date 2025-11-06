---
title: Cloud Manager に関する FAQ
description: AEM as a Cloud Service の Cloud Manager に関するよくある質問への回答を確認できます。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 81%

---


# Cloud Manager に関する FAQ {#cloud-manager-faqs}

このドキュメントでは、AEM as a Cloud Service の Cloud Manager に関するよくある質問とその回答を示します。

## Cloud Manager ビルドで Java™ 11 を使用できますか？ {#java-11-cloud-manager}

はい。Java™ 11 向けに適切に設定された `maven-toolchains-plugin` を追加します。

プロセスはドキュメント化されています。[プロジェクト作成ウィザード](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started)を参照してください。

例えば、[lWKND プロジェクトサンプルプロジェクトコード &#x200B;](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75) を参照してください。

## Java™ 8 から Java™ 11 に切り替えた後、maven-scr-plugin に関するエラーでビルドが失敗します。どうすればいいですか？ {#build-fails-maven-scr-plugin}

ビルドを Java™ 8 から 11 に切り替えようとすると、AEM Cloud Manager のビルドに失敗する場合があります。次のエラーが発生した場合は、`maven-scr-plugin` を削除し、すべての OSGi 注釈を OSGi R6 注釈に変換する必要があります。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 > [Help 1]
```

このプラグインを削除する手順については、[SCR 注釈から OSGi 注釈へ](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/)を参照してください。

## Java™ 8 から Java™ 11 に切り替えた後、RequireJavaVersion に関するエラーでビルドが失敗します。どうしたらいいでしょうか。 {#build-fails-requirejavaversion}

Cloud Manager ビルドの場合、`maven-enforcer-plugin` がこのエラーで失敗する場合があります。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

このエラーは既知の問題です。Cloud Managerで別のバージョンの Java™ を使用してコードのコンパイル用の Maven コマンドを実行していることが原因です。 この問題を解決するには、`maven-enforcer-plugin` の設定から `requireJavaVersion` を省略するだけです。

## コード品質チェックに失敗し、デプロイメントが停止しています。このチェックを回避する方法はありますか？ {#deployment-stuck}

はい。セキュリティ評価以外のコード品質チェックの失敗は、重要な指標ではありません。 その結果、結果の UI で項目を展開することで、デプロイメントパイプラインの一部としてバイパスできます。

[&#x200B; デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナー &#x200B;](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles) の役割を持つユーザーは、問題を上書きできます。 その場合、パイプラインは続行されます。または、問題を受け入れることもでき、その場合、パイプラインはエラーで停止します。

[コード品質テスト](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate)および[実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines)について詳しくは、ドキュメントを参照してください。

## Maven プロジェクトのバージョンに SNAPSHOT を使用できますか？ {#use-snapshot}

はい。開発者向けデプロイメントの場合、Git ブランチの `pom.xml` ファイルには、`<version>` 値の最後に `-SNAPSHOT` が含まれている必要があります。

この値を使用すると、バージョンが変更されなかった場合でも、以降のデプロイメントを引き続きインストールできます。 デベロッパーデプロイメントでは、maven ビルドの自動バージョンは追加または生成されません。

また、ステージおよび実稼働ビルドまたはデプロイメントのバージョンを `-SNAPSHOT` に設定することもできます。Cloud Manager では、適切なバージョン番号を自動的に設定し、Git にタグを作成します。このタグは、必要に応じて後で参照できます。

バージョン処理について詳しくは、[Maven プロジェクトのバージョン処理 &#x200B;](/help/implementing/cloud-manager/managing-code/project-version-handling.md) を参照してください。

## パッケージとバンドルのバージョン管理は、ステージングと実稼動のデプロイメントでどのように機能しますか？ {#snapshot-version}

ステージングと実稼動のデプロイメントでは、自動バージョンが生成されます。[Maven プロジェクトのバージョン処理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)を参照してください。

ステージングと実稼働のデプロイメントでカスタムバージョン管理を行うには、`1.0.0` のように、3 つの部分から成る適切な Maven バージョンを設定します。実稼動にデプロイするたびに、バージョンを増やします。

Cloud Manager では、自らのバージョンをステージビルドと実稼動ビルドに自動的に追加し、Git ブランチを作成します。特別な設定は必要ありません。前述のように Maven バージョンを設定しない場合でも、デプロイメントは成功し、バージョンが自動的に設定されます。

## Maven ビルドが Cloud Manager デプロイメントでは失敗しますが、ローカルではエラーなしでビルドされます。何が問題なのでしょうか。 {#maven-build-fail}

詳しくは、[こちらの Git リソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEM as a Cloud Service のデプロイステップで Cloud Manager のデプロイメントが失敗した場合は、どうすればよいですか？ {#cloud-manager-deployment-cloud-service}

デプロイメントが失敗する最も一般的な理由は、`sling-distribution-importer` ユーザーの権限が不十分なことです。その場合、Cloud Manager のデプロイメント中にデプロイステップが失敗し、次のようなエラーが生成されます。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

`sling-distribution-importer` ユーザーは、`ui.content package` で定義されたコンテンツパスに対して追加の権限が必要です。このルールは、通常、`/conf` と `/var` の両方に対する権限を追加する必要があるということです。

解決策は、[RepositoryInitializer OSGi 設定](/help/implementing/deploying/overview.md#repoint)スクリプトをアプリケーションデプロイメントパッケージに追加して、`sling-distribution-importer` ユーザーの ACL を追加することです。

上記のエラー例では、パッケージ `myapp-base.ui.content-*.zip` の `/conf` と `/var/workflow` の下にコンテンツが含まれています。デプロイメントを成功させるには、これらのパスの下に `sling-distribution-importer` の権限が必要です。

`sling-distribution-importer` ユーザーの権限を追加する OSGi 設定の例として、[`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) を紹介します。この設定により、`/var` 下に権限が追加されます。このような設定は、`/apps/myapp/config` （`myapp` はアプリケーションコードが保存されるフォルダー）下のアプリケーションパッケージに追加する必要があります。

## AEM as a Cloud Service のデプロイステップで Cloud Manager のデプロイメントが失敗します。RepositoryInitializer OSGi 設定は追加済みです。他に何ができますか？ {#build-failures}

[RepositoryInitializer OSGi 設定の追加](#cloud-manager-deployment-cloud-service)でエラーが解決しない場合は、次のような問題の 1 つが原因である可能性があります。

* 標準のサービスを中断する無効な OSGi 設定が原因で、デプロイメントが失敗する可能性があります。
   * デプロイ時のログを調べて、明らかなエラーがないかどうかを確認します。

* Dispatcher や Apache の不正な設定が原因でデプロイに失敗する場合があります。
   * SDK に含まれている Docker イメージを使用して、Apache 設定と Dispatcher 設定をローカルでテストしてください。
   * ローカルテストを簡単に行うための Dispatcher Docker コンテナの設定方法については、[クラウド内の Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery) を参照してください。

* オーサーインスタンスからパブリッシュインスタンスへのコンテンツパッケージのレプリケーション（Sling 配布）時に他の何らかのエラーが発生したために、デプロイが失敗する場合があります。
   * ローカル設定で問題をシミュレートするには、次の手順に従います。
      1. 最新のAEM SDK jar を使用して、オーサーインスタンスとパブリッシュインスタンスをローカルにインストールします。
      1. オーサーインスタンスにログオンします。
      1. **ツール**／**デプロイメント**／**配布**&#x200B;に移動します。
      1. コードベースの一部となるコンテンツパッケージを配布し、キューがブロックされてエラーが発生するかどうかを確認します。。

## aio コマンドを使用して変数を設定できません。どうすればいいですか？ {#set-variable}

`aio` コマンドでパイプライン変数をリストアップまたは設定しようとすると、次のような `403` エラーが発生する場合があります。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

この場合、これらのコマンドを実行するユーザーに、Admin Console で&#x200B;**デプロイメントマネージャー**&#x200B;の役割を追加する必要があります。

詳しくは、[API の権限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)を参照してください。
