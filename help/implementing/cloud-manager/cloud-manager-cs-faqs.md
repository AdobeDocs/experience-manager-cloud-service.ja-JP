---
title: Cloud Manager - Cloud Services FAQ
seo-title: Cloud Manager FAQs
description: トラブルシューティングのヒントについては、Cloud Manager for Cloud Servicesの FAQ を参照してください。
seo-description: Follow this page to get answers on Cloud Manager - Cloud Services FAQs
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 100%

---

# Cloud Manager FAQ {#cloud-manager-faqs}

次の節では、Cloud Manager for Cloud Services に関するよくある質問に対する回答を示します。

## Cloud Manager ビルドで Java 11 を使用することは可能ですか？ {#java-11-cloud-manager}

ビルドを Java 8 から 11 に切り替えようとすると、AEM Cloud Manager のビルドに失敗します。この問題には多くの原因があり、ほとんどの一般的な原因は以下のとおりです。

* [ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=ja#getting-started)に記載されているように、maven-toolchains-plugin を Java 11 用の正しい設定で追加します。例えば、[wknd サンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)を参照してください。

* 以下のエラーが発生した場合は、`maven-scr-plugin` の使用を削除し、すべての OSGi 注釈を OSGi R6 注釈に変換する必要があります。手順については、[ここ](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)を参照してください。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Cloud Manager ビルドの場合、Maven Enforcer プラグインはエラー `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"` で失敗します。これは既知の問題です。Cloud Manager では、maven コマンドの実行に、コードをコンパイルした際と異なるバージョンの Java を使用しているためです。ひとまず、maven-enforcer-plugin 設定から `requireJavaVersion` を省略します。

## コード品質のチェックの失敗が原因で、デプロイメントが停止します。このチェックを回避する方法はありますか？ {#deployment-stuck}

*セキュリティ評価*&#x200B;以外のコード品質エラー指標は重要ではありません。結果として生成される UI の項目を展開すると、これらのエラーを回避できます。

[デプロイメントマネージャー、プロジェクトマネージャーまたはビジネスオーナー](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja#requirements)は、問題をオーバーライドできます。この場合、パイプラインは続行されます。または、問題を承認できます。この場合、パイプラインはエラーで停止します。詳しくは、[パイプライン実行中の 3 層ゲート](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=ja#how-to-use)を参照してください。


## Maven プロジェクトのバージョンでは SNAPSHOT を使用できますか？パッケージとバンドル jar ファイルのバージョン管理は、ステージング環境および実稼動環境でのデプロイメントでどのように機能しますか？ {#snapshot-version}

ステージング環境および実稼動環境でのデプロイメント向けパッケージおよびバンドル jar ファイルのバージョン管理については、次のシナリオを参照してください。

1. デベロッパーデプロイメントでは、Git ブランチの `pom.xml` ファイルで、`<version>` 値の末尾に `-SNAPSHOT` を含める必要があります。これにより、バージョンが変更されない場合でも、以降のデプロイメントは引き続きインストールされます。デベロッパーデプロイメントでは、maven ビルドの自動バージョンは追加または生成されません。

1. ステージング環境および実稼動環境でのデプロイメントでは、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=ja#managing-code)に記載されているように、自動バージョンが生成されます。

1. ステージング環境および実稼動環境でカスタムバージョンを設定する場合は、`1.0.0` のように、maven のバージョンを 3 つのパーツに設定します。実稼動環境に別のデプロイを実行するたびに、バージョンを増やします。

1. Cloud Manager は、ステージング環境および実稼動環境のビルドへ自動的にバージョンを追加し、Git ブランチを作成します。特別な設定は必要ありません。上記の手順 3 をスキップした場合でも、デプロイメントは引き続き問題なく動作し、バージョンが自動的に設定されます。

1. ステージングおよび実稼動ビルドまたはデプロイメントの場合は、バージョンに `-SNAPSHOT` が付いたままにしておいても問題はありません。Cloud Manager は、適切なバージョン番号を自動的に設定し、Git でタグを作成します。このタグは、必要に応じて後で参照できます。

1. 開発環境で試験的なコードを試す場合は、新しい Git ブランチを作成し、そのブランチを使用するようにパイプラインを設定します。これは、デプロイメントの開始に失敗したときに、コードがどこで壊れているか確認するために、古いバージョンのコードを使用してテストする場合に便利です。

   以下の Git コマンドは、特定の既存のコミット `485548e4fbafbc83b11c3cb12b035c9d26b6532b` に対して、*testbranch1* という名前のリモートブランチを作成します。この特別なブランチは、Cloud Manager で使用でき、他のブランチには影響を与えません。

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   詳しくは、[Git ドキュメント](https://git-scm.com/book/en/v2/Git-Internals-Git-References)を参照してください。

   後でテストブランチを削除する場合は、次の delete コマンドを使用します。

   `git push origin --delete testbranch1`

## Cloud Manager での maven のビルド失敗はデプロイされますが、ローカルではビルドされ、エラーは発生しません。デバッグの方法？ {#maven-build-fail}

詳しくは、[Git リソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEM as a Cloud Service 環境のデプロイステップで Cloud Manager によるデプロイが失敗した場合は、どうすればよいですか？  {#cloud-manager-deployment-cloud-service}

デプロイが失敗する最も一般的な理由は、*sling-distribution-importer* ユーザーの権限が不十分なことです。問題、原因、解決策については、次の例を参照してください。

**問題**：
AEM as a Cloud Service 環境で、Cloud Manager によるデプロイ中にデプロイステップが失敗し、例えば次のようなエラーが発生します。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**：

sling-distribution-importer ユーザーには、ui.content パッケージに定義されているコンテンツパスごとに、追加の権限が必要です。これは、通常、/conf と /var の両方に対する権限を追加する必要があるということです。

**解決策**：
この問題の解決策は、[RepositoryInitializer OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#deploying)スクリプトをアプリケーションデプロイメントパッケージに追加して sling-distribution-importer ユーザーの ACL を追加することです。上記のエラー例では、パッケージ myapp-base.ui.content-*.zip の `/conf` と `/var/workflow` の下にコンテンツが含まれています。デプロイメントが失敗しないようにするには、これらのパス下への sling-distribution-importer の権限を追加する必要があります。sling-distribution-importer ユーザーの権限を追加するこのような OSGi 設定の例として、[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) を紹介します。この設定では /var 下への権限を追加します。[1] の下にあるこの xml ファイルを `/apps/myapp/config` の下のアプリケーションパッケージに追加する必要があります（myapp はアプリケーションコードが格納されているフォルダー）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. *sling-distribution-importer* が原因でない場合は、標準提供サービスの動作を妨げる不正な OSGi 設定が原因で、デプロイが失敗している可能性があります。デプロイ時のログを調べて、明らかなエラーがないかどうかを確認します。

1. Dispatcher や Apache の不正な設定が原因でデプロイに失敗する場合があります。SDK に含まれている Docker イメージを使用して、Apache 設定と Dispatcher 設定をローカルでテストしてください。ローカルテストを簡単に行うための Dispatcher Docker コンテナの設定方法については、[クラウド内の Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#content-delivery) を参照してください。

1. オーサーインスタンスからパブリッシュインスタンスへのコンテンツパッケージのレプリケーション（Sling 配布）時に他の何らかのエラーが発生したために、デプロイが失敗する場合があります。

   次の手順を参照して、ローカル設定でこれをシミュレートしてください。

   * （最新の AEM SDK JAR を使用して）オーサーインスタンスとパブリッシュインスタンスをインストールします。
   * オーサーインスタンスにログインします。
   * **ツール**／**デプロイメント**／**配布**&#x200B;に移動します。
   * コードベースの一部となるコンテンツパッケージを配布し、キューがブロックされてエラーが発生するかどうかを確認します。

## aio cloudmanager:set-pipeline-variables を使用して変数を設定できません。これらの問題をデバッグするにはどうすればよいですか？ {#set-variable}

以下に示すようなコマンドでパイプライン変数をリストまたは設定しようとして `403` エラーが発生した場合は、Admin Console で、Cloud Manager 製品の役割の 1 つである&#x200B;*デプロイメントマネージャー*&#x200B;として自分自身を追加する必要があります。\
詳しくは、[API の権限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)を参照してください。

関連するコマンドとエラー：

`$ aio cloudmanager:list-pipeline-variables 222`

*エラー*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*エラー* : `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*エラー*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
