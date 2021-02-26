---
title: Cloud Manager -Cloud ServicesFAQ
seo-title: Cloud Manager FAQ
description: Cloud Servicesに関するFAQについては、Cloud Managerを参照して、トラブルシューティングのヒントを確認してください
seo-description: Cloud Managerに関する回答を得るには、このページに従ってください —Cloud Servicesに関するFAQ
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 3%

---


# Cloud Manager FAQ {#cloud-manager-faqs}

次の節では、Cloud Services向けCloud Managerに関するよくある質問と、その回答を示します。

## Java 11をCloud Managerビルドと共に使用することは可能ですか？{#java-11-cloud-manager}

ビルドをJava 8から11に切り替えようとすると、AEM Cloud Managerのビルドに失敗する。 この問題には多くの原因があり、ほとんどの一般的な原因は以下に記載されています。

* [追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)に記載されているように、maven-toolchains-pluginをJava 11用に正しい設定にして記述します。  例えば、[wkndサンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)を参照してください。

* 以下のエラーが発生した場合は、`maven-scr-plugin`の使用を削除し、すべてのOSGi注釈をOSGi R6注釈に変換する必要があります。 手順については、[ここ](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)を参照してください。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Cloud Managerビルドの場合、Maven Enforcerプラグインはエラー`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`で失敗します。 これは既知の問題です。Cloud Managerで、mavenコマンドを実行するのに別のバージョンのJavaを使用し、コードをコンパイルするのに対して、既知の問題です。 ここでは、maven-enforcer-plugin設定から`requireJavaVersion`を省略します。

## コードの質のチェックに失敗したため、展開が停止します。 このチェックを回避する方法はありますか。{#deployment-stuck}

*セキュリティレーティング*&#x200B;を除くすべてのコード品質のエラーは重要ではない指標なので、結果UIの項目を展開すると、これらのエラーを回避できます。

[Deployment Manager、Project Manager、またはBusiness Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)の役割を持つユーザーは、問題を上書きできます。この場合、パイプラインは続行するか、問題を受け入れることができます。この場合、パイプラインは失敗して停止します。  詳細は、[パイプラインの実行中の3層ゲート](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=ja#how-to-use)を参照してください。


## MavenプロジェクトのバージョンでSNAPSHOTを使用できますか。 パッケージとバンドルjarファイルのバージョン付けは、ステージおよび実稼働環境ではどのように機能しますか。{#snapshot-version}

ステージおよび実稼働環境での展開用のパッケージおよびバンドルjarファイルのバージョンの設定については、次のシナリオを参照してください。

1. 開発者のデプロイメントでは、Gitブランチ`pom.xml`ファイルの`<version>`値の末尾に`-SNAPSHOT`を含める必要があります。 これにより、バージョンが変更されない場合でも、以降のデプロイメントは引き続きインストールされます。 開発者デプロイメントでは、Mavenビルドの自動バージョンは追加または生成されません。

1. ステージおよび実稼働環境でのデプロイメントでは、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)に記載されているように、自動バージョンが生成されます。

1. ステージおよび実稼働環境でのカスタムバージョン設定の場合は、`1.0.0`のように、適切なmavenバージョンを3つのパーツに設定します。 実稼働環境に別のデプロイを実行するたびに、バージョンを増やします。

1. Cloud Managerは、自動的にStageビルドとProductionビルドにバージョンを追加し、Gitブランチを作成します。 特別な設定は必要ありません。 上記の手順3をスキップした場合、デプロイメントは引き続き問題なく動作し、バージョンが自動的に設定されます。

1. ステージ版と実稼働版のビルドまたはデプロイメント用に`-SNAPSHOT`を残しておくと問題はありません。 Cloud Managerは、適切なバージョン番号を自動的に設定し、Gitにタグを作成します。 このタグは、必要に応じて後で参照できます。

1. 開発環境で試験的なコードを試す場合は、新しいGitブランチを作成し、その異なるブランチを使用するようにパイプラインを設定します。 これは、デプロイメントの開始に失敗し、古いバージョンのコードを使用してテストし、コードが壊れたかどうかを確認する場合に便利です。

   以下のGitコマンドは、特定の既存のコミット`485548e4fbafbc83b11c3cb12b035c9d26b6532b`に対して、*testbranch1*&#x200B;という名前のリモートブランチを作成します。  この特別なブランチは、Cloud Managerで使用でき、他のブランチに影響を与えません。

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   詳しくは、[Gitドキュメント](https://git-scm.com/book/en/v2/Git-Internals-Git-References)を参照してください。

   後でテストブランチを削除する場合は、次のdeleteコマンドを使用します。

   `git push origin --delete testbranch1`

## MavenのビルドはCloud Managerでは失敗しますが、ローカルにビルドされ、エラーは発生しません。 デバッグの方法? {#maven-build-fail}

詳しくは、[Git Resource](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEMでの展開手順でCloud Managerの展開が失敗し、Cloud Service環境としてのでの展開に失敗した場合、どうすればよいですか？{#cloud-manager-deployment-cloud-service}

展開が失敗する最も一般的な理由は、*sling-distribution-importer*ユーザーに対する権限が不十分であるためです。
問題、原因、解決方法については、次の例を参照してください。

****
問題AEMでのCloud Managerのデプロイメント中に、Cloud Service環境としてデプロイすると、デプロイ手順が失敗し、次のようなエラーが発生します。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importerユーザーは、ui.contentパッケージで定義されているコンテンツパスごとに、追加の権限が必要です。  これは、通常、/confと/varの両方に対する権限を追加する必要があることを意味します。

**解決**
策：sling-distribution-importerユーザーのACLを追加するには、 [RepositoryInitializer OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#deploying) 設定スクリプトをアプリケーション展開パッケージに追加します。上の例のエラーでは、パッケージmyapp-base.ui.content-*.zipには`/conf`と`/var/workflow`の下のコンテンツが含まれています。 デプロイメントが失敗しないようにするには、それらのパスの下にSling-Distribution-importerの権限を追加する必要があります。
以下は、sling-distribution-importerユーザーに追加の権限を追加するOSGi設定の例です。[org.apache.sling.jcr.repoint.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config)  この設定は、/varの下に権限を追加します。  [1]の下のこのxmlファイルは、`/apps/myapp/config`の下のアプリケーションパッケージに追加する必要があります（myappはアプリケーションコードが保存されているフォルダー）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. *sling-distribution-importer*&#x200B;が原因でない場合は、初期設定のサービスを中断する不正なOSGi設定が原因で、デプロイが失敗する可能性があります。 展開中にログを確認し、明らかなエラーがないかどうかを確認します。

1. ディスパッチャーまたはApacheの設定が正しくないため、デプロイメントに失敗する場合があります。 SDKに含まれるDockerイメージを使用して、Apacheの設定とディスパッチャーの設定をローカルでテストしてください。 ローカルテストを簡単に行うためのディスパッチャーDockerコンテナの設定方法については、Cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#content-delivery)の[ディスパッチャーを参照してください。

1. コンテンツパッケージの作成者から発行インスタンスへのレプリケーション（Sling配布）中に、他のエラーが発生したため、展開が失敗する場合があります。

   ローカル設定でこの動作をシミュレートするには、次の手順を参照してください。

   * 作成者インスタンスと発行インスタンスのインストール(最新のAEM SDK JARを使用)
   * 作成者インスタンスにログインします
   * **ツール** -> **導入** -> **配布**&#x200B;に移動します
   * コードベースの一部であるコンテンツパッケージを配布し、キューがエラーでブロックされるかどうかを確認します。

## Aio Cloud Managerが設定したパイプライン変数を介して変数を設定できません。 これらの問題のデバッグ方法{#set-variable}

以下に示すようなコマンドを使用してパイプライン変数をリストまたは設定しようとすると`403`エラーが発生する場合は、Admin Consoleに&#x200B;*Deployment Manager* Cloud Manager製品ロールとして追加する必要があります。\
詳しくは、[API権限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)を参照してください。

関連するコマンドとエラー：

`$ aio cloudmanager:list-pipeline-variables 222`

*エラー*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*エラー*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*エラー*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
