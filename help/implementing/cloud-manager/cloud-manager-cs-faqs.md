---
title: Cloud Manager - Cloud Services FAQ
seo-title: Cloud Manager FAQ
description: トラブルシューティングのヒントについては、Cloud Manager for Cloud Servicesの FAQ を参照してください。
seo-description: Cloud Manager - Cloud Services の FAQ に関する回答を得るには、このページを参照してください。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '1152'
ht-degree: 100%

---

# Cloud Manager FAQ {#cloud-manager-faqs}

次の節では、Cloud Manager for Cloud Services に関するよくある質問に対する回答を示します。

## Cloud Manager ビルドで Java 11 を使用できますか？ {#java-11-cloud-manager}

Java 8 から Java 11 に切り替えようとすると、AEM Cloud Manager ビルドは機能しなくなります。この問題の原因は様々で、最も一般的なものは次のとおりです。

* [こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=ja#getting-started)の記載どおりに、Java 11 を正しく設定して maven-toolchains-plugin を追加します。例えば、[WKND サンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)を参照してください。

* 以下のエラーが発生した場合は、`maven-scr-plugin` の使用箇所を削除し、すべての OSGi 注釈を OSGi R6 注釈に変換する必要があります。手順については、[こちら](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)を参照してください。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Cloud Manager ビルドについては、maven-enforcer-plugin が失敗して `"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"` というエラーが表示されます。これは既知の問題です。Cloud Manager で別のバージョンの Java を使用してコードのコンパイル用の maven コマンドを実行していることが原因です。ひとまず、maven-enforcer-plugin の設定から `requireJavaVersion` を省略します。

## デプロイメントが停止したのは、コード品質チェックに失敗したからですか？このチェックを回避する方法はありますか？ {#deployment-stuck}

*セキュリティ評価*&#x200B;を除くすべてのコード品質チェックエラーは重大な指標ではないので、結果の UI で項目を展開してこれらのエラーを回避できます。

[デプロイメントマネージャー、プロジェクトマネージャー、ビジネスオーナー](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja#requirements)のいずれかの役割を持つユーザーは、問題をオーバーライドできます。その場合、パイプラインは続行されます。または、問題を承認できます。その場合、パイプラインはエラーで停止します。詳しくは、[パイプライン実行中の 3 層ゲート](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=ja#how-to-use)を参照してください。


## Maven プロジェクトのバージョンでスナップショットを使用できますか？ステージングデプロイメントと実稼動デプロイメントの場合、パッケージとバンドル jar ファイルのバージョン管理はどのように機能しますか？ {#snapshot-version}

ステージングデプロイメントと実稼動デプロイメントのパッケージおよびバンドル jar ファイルのバージョン管理については、次のシナリオを参照してください。

1. 開発者デプロイメントの場合は、Git ブランチ `pom.xml` ファイルの `<version>` 値の末尾に `-SNAPSHOT` が含まれている必要があります。これにより、以降のデプロイメントはバージョンが変わらない場合でも、インストールされます。開発者デプロイメントでは、Maven ビルドの自動バージョンは追加または生成されません。

1. ステージングデプロイメントおよび実稼働デプロイメントでは、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=ja#managing-code)の記載どおり、自動バージョンが生成されます。

1. ステージングデプロイメントおよび実稼働デプロイメントでのカスタムバージョン管理の場合は、3 つパートからなる適切な Maven バージョン（例：`1.0.0`）を設定します。実稼働環境に別のデプロイを行う必要があるたびに、バージョンを増やします。

1. Cloud Manager がそれ自身のバージョンをステージングビルドと実稼働ビルドに自動的に追加するほか、Git ブランチも作成します。特別な設定は必要ありません。上記の手順 3 を省略した場合でも、デプロイメントは問題なく機能し、バージョンが自動的に設定されます。

1. ステージングおよび実稼働ビルドまたはデプロイメントの場合に `-SNAPSHOT` の付いたバージョンをそのままにしておいても問題はありません。Cloud Manager が適切なバージョン番号を自動的に設定し、Git にタグを自動的に作成します。このタグは、必要に応じて後で参照できます。

1. 開発環境で試験的なコードを試す場合は、新しい Git ブランチを作成し、その異なるブランチを使用するようにパイプラインを設定します。これは、デプロイメントの開始に失敗したとき、古いバージョンのコードでテストして、デプロイメントがいつ機能しなくなったかを確認する場合に便利です。

   以下の Git コマンドでは、既存の特定のコミット `485548e4fbafbc83b11c3cb12b035c9d26b6532b` に対して、*testbranch1* というリモートブランチを作成します。この特別なブランチは、他のブランチに影響を与えずに Cloud Manager で使用できます。

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   詳しくは、[Git のドキュメント](https://git-scm.com/book/en/v2/Git-Internals-Git-References)を参照してください。

   テストブランチを後で削除する場合は、次の delete コマンドを使用します。

   `git push origin --delete testbranch1`

## Maven ビルドが Cloud Manager によるデプロイでは失敗しますが、ローカルではエラーなしでビルドされます。デバッグするには、どうすればよいですか？ {#maven-build-fail}

詳しくは、[Git リソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEM as a Cloud Service 環境のデプロイステップで Cloud Manager によるデプロイが失敗した場合は、どうすればよいですか？ {#cloud-manager-deployment-cloud-service}

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

## aio cloudmanager:set-pipeline-variables を使用して変数を設定できません。この問題をデバッグするには、どうすればよいですか？ {#set-variable}

以下に示すようなコマンドでパイプライン変数をリストまたは設定しようとして `403` エラーが発生した場合は、Admin Console で、Cloud Manager 製品の役割の 1 つである&#x200B;*デプロイメントマネージャー*&#x200B;として自分自身を追加する必要があります。\
詳しくは、[API 権限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)を参照してください。

関連するコマンドとエラー：

`$ aio cloudmanager:list-pipeline-variables 222`

*エラー* : `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*エラー* : `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*エラー* : `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
