---
title: Cloud Manager -Cloud ServicesFAQ
seo-title: Cloud Managerに関するFAQ
description: トラブルシューティングのヒントについては、Cloud ServicesのFAQについてCloud Managerを参照してください
seo-description: このページでは、Cloud ManagerのCloud Servicesに関するFAQについて説明します
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 3%

---

# Cloud ManagerのFAQ {#cloud-manager-faqs}

以下の節では、Cloud Services向けCloud Managerに関するよくある質問に対する回答を示します。

## Cloud ManagerビルドでJava 11を使用することは可能ですか？{#java-11-cloud-manager}

Java 8から11にビルドを切り替えようとすると、AEM Cloud Managerのビルドが失敗します。 問題には多くの原因が考えられ、最も一般的な原因は以下のとおりです。

* [ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)に記載されているように、Java 11用の正しい設定でmaven-toolchains-pluginを追加します。  例えば、[wkndサンプルプロジェクトコード](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)を参照してください。

* 以下のエラーが発生した場合は、`maven-scr-plugin`の使用を削除し、すべてのOSGi注釈をOSGi R6注釈に変換する必要があります。 手順については、[ここ](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)を参照してください。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* Cloud Managerビルドの場合、Maven Enforcerプラグインはエラー`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`で失敗します。 これは、Cloud Managerが別のバージョンのJavaを使用してmavenコマンドを実行し、コードをコンパイルするのとは異なるため、既知の問題です。 現時点では、maven-enforcer-plugin設定から`requireJavaVersion`を省略します。

## コード品質の確認に失敗したため、デプロイメントが停止します。 このチェックをバイパスする方法はありますか？{#deployment-stuck}

*セキュリティ評価*&#x200B;を除くすべてのコード品質エラーは重要ではない指標なので、結果UIの項目を展開することで回避できます。

[Deployment Manager、プロジェクトマネージャー、またはビジネスオーナー](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)の役割を持つユーザーは、問題を上書きできます。この場合、パイプラインは進行し、問題を受け入れます。その場合、パイプラインは失敗して停止します。  詳しくは、[パイプライン実行時の3層ゲート](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=ja#how-to-use)を参照してください。


## MavenプロジェクトのバージョンでSNAPSHOTを使用できますか。 パッケージとバンドルのjarファイルのバージョン管理は、ステージング環境と実稼動環境のデプロイメントでどのように機能しますか。{#snapshot-version}

ステージデプロイメントと実稼動デプロイメント用のパッケージおよびバンドルjarファイルのバージョン管理については、次のシナリオを参照してください。

1. デベロッパーデプロイメントの場合、Gitブランチ`pom.xml`ファイルの`<version>`値の末尾に`-SNAPSHOT`を含める必要があります。 これにより、バージョンが変更されない場合でも、以降のデプロイメントをインストールできます。 デベロッパーデプロイメントでは、Mavenビルド用の自動バージョンが追加または生成されることはありません。

1. ステージ環境および実稼動環境のデプロイメントでは、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)に記載されているように、自動バージョンが生成されます。

1. ステージおよび実稼動環境のデプロイメントでカスタムバージョン管理をおこなう場合は、`1.0.0`のように、適切なmavenバージョンを3つのパートで設定します。 別の実稼動環境へのデプロイを実行するたびに、バージョンを増やします。

1. Cloud Managerは、ステージビルドと実稼動ビルドに自動的にバージョンを追加し、さらにGitブランチを作成します。 特別な設定は不要です。 上記の手順3をスキップした場合、デプロイメントは引き続き正常に動作し、バージョンが自動的に設定されます。

1. ステージングビルドおよび実稼動ビルドまたはデプロイメントで`-SNAPSHOT`のままにしておくと、問題は発生しません。 Cloud Managerは適切なバージョン番号を自動的に設定し、Gitでタグを作成します。 このタグは、必要に応じて後で参照できます。

1. 開発環境で実験的なコードを試す場合は、新しいGitブランチを作成し、その別のブランチを使用するようにパイプラインを設定できます。 これは、デプロイメントが失敗し始めた場合に、古いバージョンのコードでテストして、破損したタイミングを確認する場合に役立ちます。

   以下のGitコマンドは、特定の既存のコミット`485548e4fbafbc83b11c3cb12b035c9d26b6532b`に対して、*testbranch1*&#x200B;というリモートブランチを作成します。  この特別なブランチは、他のブランチに影響を与えることなく、Cloud Managerで使用できます。

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   詳しくは、[Gitのドキュメント](https://git-scm.com/book/en/v2/Git-Internals-Git-References)を参照してください。

   後でテストブランチを削除する場合は、次のdeleteコマンドを使用します。

   `git push origin --delete testbranch1`

## Cloud ManagerのデプロイでMavenビルドが失敗し、エラーなくローカルにビルドされます。 デバッグの方法? {#maven-build-fail}

詳しくは、[Gitリソース](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)を参照してください。

## AEM as a Cloud Managerのデプロイメント手順でCloud Managerのデプロイメントが失敗した場合は、どうすればよいですか？Cloud Service環境としてのデプロイ手順{#cloud-manager-deployment-cloud-service}

デプロイが失敗する最も一般的な理由は、*sling-distribution-importer*ユーザーに十分な権限がないためです。
問題、原因、解決策については、以下の例を参照してください。

****
問題AEM as aCloud Service環境でのCloud Managerデプロイメント中に、デプロイ手順が失敗し、以下のようなエラーが観察されます。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importerユーザーは、ui.contentパッケージで定義されたコンテンツパスごとに、追加の権限が必要です。  これは、通常、/confと/varの両方に対する権限を追加する必要があることを意味します。

****
解決策この解決策は、 [RepositoryInitializer OSGi設定スクリプトをアプリデプロイメントパッケージに追加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#deploying) し、sling-distribution-importerユーザーのACLを追加することです。上記の例のエラーでは、パッケージmyapp-base.ui.content-*.zipに`/conf`と`/var/workflow`の下のコンテンツが含まれます。 デプロイメントが失敗しないようにするには、それらのパスにsling-distribution-importerの権限を追加する必要があります。
例えば、sling-distribution-importerユーザーに追加の権限を追加するOSGi設定の[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config)を示します。  この設定は、/varの下に権限を追加します。  [1]の下にあるこのxmlファイルを、`/apps/myapp/config`の下のアプリケーションパッケージに追加する必要があります（myappはアプリケーションコードが保存されているフォルダーです）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. *sling-distribution-importer*&#x200B;が原因でない場合は、初期設定のサービスを中断する不適切なOSGi設定が原因で、デプロイが失敗する可能性があります。 デプロイメント中にログを調べ、明らかなエラーがあるかどうかを確認します。

1. DispatcherまたはApacheの設定が正しくないため、デプロイメントが失敗する可能性があります。 SDKに含まれるDockerイメージを使用して、Apache設定とDispatcher設定をローカルでテストしてください。 ローカルで簡単にテストをおこなうためのDispatcher Dockerコンテナの設定方法については、クラウド内の[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja#content-delivery)を参照してください。

1. オーサーインスタンスからパブリッシュインスタンスへのコンテンツパッケージ（sling配布）のレプリケーション中に、他のエラーが原因でデプロイメントが失敗する場合があります。

   ローカル設定でこれをシミュレートするには、以下の手順を参照してください。

   * (最新のAEM SDK jarを使用して)オーサーインスタンスとパブリッシュインスタンスをインストールする
   * オーサーインスタンスにログインします。
   * **ツール** -> **デプロイメント** -> **配布**&#x200B;に移動します。
   * コードベースの一部であるコンテンツパッケージを配布し、エラーでキューがブロックされるかどうかを確認します。

## aio cloud manager設定パイプライン変数を介して変数を設定できない。 これらの問題のデバッグ方法は？{#set-variable}

以下のようなコマンドを使用してパイプライン変数をリストまたは設定しようとすると`403`エラーが発生する場合は、Admin Consoleに&#x200B;*Deployment Manager* Cloud Manager製品ロールとして追加する必要があります。\
詳しくは、[API権限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)を参照してください。

関連するコマンドとエラー：

`$ aio cloudmanager:list-pipeline-variables 222`

*エラー*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*エラー*: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*エラー*: `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
