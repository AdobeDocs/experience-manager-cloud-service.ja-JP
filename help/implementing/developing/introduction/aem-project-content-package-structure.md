---
title: AEM プロジェクトの構造
description: Adobe Experience Manager as a Cloud Service へのデプロイメント用にパッケージ構造を定義する方法について説明します。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 56%

---

# AEM プロジェクトの構造

>[!TIP]
>
>[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)の基本的な使用法と、[FileVault コンテンツパッケージ Maven プラグイン](/help/implementing/developing/tools/maven-plugin.md)について説明します。この記事では、これらの概念の理解を前提としています。

この記事では、可変コンテンツと不変コンテンツの分割に従ってAEMとas a Cloud Service互換性を保つためにAdobe Experience Manager Maven プロジェクトに必要な変更点について説明します。 また、依存関係は、競合しない決定論的デプロイメントを作成するために確立され、デプロイ可能な構造でパッケージ化されます。

AEMアプリケーションのデプロイメントは、単一のAEMパッケージで構成する必要があります。 次に、このパッケージには、コード、設定、サポートするベースラインコンテンツなど、アプリケーションが機能するのに必要なすべてのサブパッケージを含める必要があります。

AEM では、**コンテンツ**&#x200B;と&#x200B;**コード**&#x200B;を分離する必要があります。つまり、単一のコンテンツパッケージを&#x200B;**両方**`/apps`およびランタイム書き込み可能な領域（たとえば、`/content`、`/conf`、`/home`、または `/apps` 以外の任意のもの）にデプロイすることは&#x200B;**できません**。代わりに、アプリケーションを AEM にデプロイするには、コードとコンテンツを別々のパッケージに分離する必要があります。

このドキュメントで概要を説明しているパッケージ構造は、ローカル開発デプロイメントと AEM as a Cloud Service デプロイメントの&#x200B;**両方**&#x200B;に対応しています。

>[!TIP]
>
>このドキュメントで概要を説明している設定は、[AEM プロジェクト Maven アーキタイプ 24 以降](https://github.com/adobe/aem-project-archetype/releases)で提供されます。

## リポジトリの可変領域と不変領域 {#mutable-vs-immutable}

この `/apps` および `/libs` AEMの領域は **不変の** AEMの起動後（つまり実行時）に変更（作成、更新、削除）できないので、変更できません。 実行時に不変領域を変更しようとすると失敗します。

リポジトリ内のその他すべて `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`などを行うと、 **可変** 領域とは、実行時に変更できる領域のことです。

>[!WARNING]
>
>以前のバージョンの AEM と同様に、`/libs` は変更しないでください。`/libs` にデプロイできるのは、AEM 製品コードだけです。

### Oak インデックス {#oak-indexes}

Oak インデックス (`/oak:index`) は、AEMas a Cloud Serviceデプロイメントプロセスで管理されます。 これは、新しいインデックスがデプロイされて完全に再インデックスされるまで、Cloud Manager は新しいコードイメージに切り替わる前に待機する必要があるからです。

このため、Oak インデックスは実行時に可変ですが、可変パッケージがインストールされる前にインストールできるように、コードとしてデプロイする必要があります。したがって、`/oak:index` 設定はコードパッケージの一部であり、[以下に説明する](#recommended-package-structure)コンテンツパッケージの一部ではありません。

>[!TIP]
>
>AEM as a Cloud Serviceでのインデックス作成について詳しくは、 [コンテンツの検索とインデックス作成](/help/operations/indexing.md).

## 推奨されるパッケージ構造 {#recommended-package-structure}

![Adobe Experience Manager プロジェクトのパッケージ構造](assets/content-package-organization.png)

この図は、推奨されるプロジェクト構造とパッケージデプロイメントアーティファクトの概要を示しています。

推奨されるアプリケーションデプロイメント構造は次のとおりです。

### コードパッケージ／OSGi バンドル

+ OSGi バンドルの Jar ファイルが生成され、すべてのプロジェクトに直接埋め込まれます。

+ `ui.apps` パッケージは、デプロイされるすべてのコードを含んでおり、`/apps` にのみデプロイされます。`ui.apps` パッケージの共通要素には次のものがありますが、これらに限定されるわけではありません。
   + [コンポーネントの定義と HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) スクリプト
      + `/apps/my-app/components`
   + JavaScript と CSS（[クライアントライブラリ](/help/implementing/developing/introduction/clientlibs.md)経由）
      + `/apps/my-app/clientlibs`
   + `/libs` の[オーバーレイ](/help/implementing/developing/introduction/overlays.md)
      + `/apps/cq`, `/apps/dam/`, などなど.
   + コンテキスト対応のフォールバック設定
      + `/apps/settings`
   + ACL（権限）
      + `/apps` の配下にある任意のパスの任意の `rep:policy`
   + [事前コンパイル済みバンドルスクリプト](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html?lang=ja)

>[!NOTE]
>
>同じコードをすべての環境にデプロイする必要があります。このコードは、ステージ環境での検証も実稼動環境で行われるという信頼水準を保証します。 詳しくは、「[実行モード](/help/implementing/deploying/overview.md#runmodes)」の節を参照してください。


### コンテンツパッケージ

+ `ui.content` パッケージには、すべてのコンテンツと設定が含まれています。コンテンツパッケージには、`ui.apps` パッケージまたは `ui.config` パッケージに含まれないすべてのノード定義が含まれます。言い換えれば、`/apps` または `/oak:index` に含まれないすべてが含まれます。`ui.content` パッケージの共通要素には次のものがありますが、これらに限定されるわけではありません。
   + コンテキスト対応の設定
      + `/conf`
   + 必須の複雑なコンテンツ構造（つまり、Repo Init で定義された過去のベースラインコンテンツ構造に基づいて構築され、拡張されるコンテンツ構築）。
      + `/content`, `/content/dam`, などなど.
   + 管理されるタグ付け分類
      + `/content/cq:tags`
   + レガシー etc ノード（理想的には、これらのノードを非 etc 場所に移行）
      + `/etc`

### コンテナパッケージ

+ この `all` パッケージは、デプロイ可能なアーティファクト（OSGI バンドル JAR ファイル）を含むコンテナパッケージです。 `ui.apps`, `ui.config`、および `ui.content` 埋め込み用パッケージ。 この `all` パッケージは次の条件を満たしてはいけません **コンテンツまたはコード** リポジトリへのすべてのデプロイメントをサブパッケージまたは OSGi バンドル JAR ファイルに委任します。

  Maven を使用してパッケージが組み込まれるようになりました。 [FileVault パッケージ Maven プラグインの埋め込み設定](#embeddeds)ではなく `<subPackages>` 設定。

  複雑なExperience Managerデプロイメントの場合は、複数の `ui.apps`, `ui.config`、および `ui.content` AEMの特定のサイトまたはテナントを表すプロジェクト/パッケージです。 この方法がおこなわれる場合は、必ず、可変コンテンツと不変コンテンツの分割に従い、必要なコンテンツパッケージと OSGi バンドル JAR ファイルをサブパッケージとして `all` コンテナコンテンツパッケージ。

  複雑なデプロイメントコンテンツパッケージ構造は、例えば、次のようになります。

   + `all` コンテンツパッケージに次のパッケージが埋め込まれて、単一のデプロイメントアーティファクトが作成されます。
      + `common.ui.apps`：サイト A とサイト B の&#x200B;**両方**&#x200B;に必要なコードをデプロイします
      + `site-a.core` サイト A に必要な OSGi バンドル JAR
      + `site-a.ui.apps`：サイト A に必要なコードをデプロイします
      + `site-a.ui.config`：サイト A に必要な OSGi 設定をデプロイします
      + `site-a.ui.content`：サイト A に必要なコンテンツと設定をデプロイします
      + `site-b.core` サイト B に必要な OSGi バンドル JAR
      + `site-b.ui.apps`：サイト B に必要なコードをデプロイします
      + `site-b.ui.config`：サイト B に必要な OSGi 設定をデプロイします
      + `site-b.ui.content`：サイト B に必要なコンテンツと設定をデプロイします

+ `ui.config` パッケージには、すべての [OSGi 設定](/help/implementing/deploying/configuring-osgi.md) が含まれています。
   + コードと見なされ、OSGi バンドルに属していますが、通常のコンテンツノードは含まれていません。したがって、コンテナパッケージとしてマークされます
   + 実行モード固有の OSGi 設定定義を含む組織フォルダー
      + `/apps/my-app/osgiconfig`
   + すべてのターゲット AEM as a Cloud Service デプロイメントターゲットに適用されるデフォルトの OSGi 設定を含む、共通の OSGi 設定フォルダー
      + `/apps/my-app/osgiconfig/config`
   + すべてのターゲットAEMas a Cloud Serviceデプロイメントターゲットに適用されるデフォルトの OSGi 設定を含む、実行モード固有の OSGi 設定フォルダー
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi 設定スクリプト
      + AEM アプリケーションの論理的な一部である（可変）コンテンツをデプロイする方法として、[Repo Init](#repo-init) を使用することをお勧めします。Repo Init OSGi 設定は、上述のように適切な `config.<runmode>` フォルダーに配置し、次の定義に使用します。
         + ベースラインコンテンツの構造
         + ユーザー
         + サービスユーザー
         + グループ
         + ACL（権限）

### 追加のアプリケーションパッケージ {#extra-application-packages}

独自のコードとコンテンツパッケージで構成される他のAEMプロジェクトをAEMのデプロイメントで使用する場合は、そのコンテナパッケージをプロジェクトの `all` パッケージ。

例えば、2 つのベンダーのAEMアプリケーションを含むAEMプロジェクトは、次のようになります。

+ `all` コンテンツパッケージに次のパッケージが埋め込まれて、単一のデプロイメントアーティファクトが作成されます。
   + `core` AEM アプリケーションで必要な OSGi バンドル JAR
   + `ui.apps`：AEM アプリケーションで必要なコードをデプロイします
   + `ui.config`：AEM アプリケーションで必要な OSGi 設定をデプロイします
   + `ui.content`：AEM アプリケーションで必要なコンテンツと設定をデプロイします
   + `vendor-x.all`：ベンダー X アプリケーションで必要なすべて（コードとコンテンツ）をデプロイします
   + `vendor-y.all`：ベンダー Y アプリケーションで必要なすべて（コードとコンテンツ）をデプロイします

## パッケージタイプ {#package-types}

パッケージは、宣言済みのパッケージタイプでマークされる必要があります。パッケージタイプは、パッケージの目的とデプロイメントを明確にするのに役立ちます。

+ コンテナパッケージでは、`packageType` を `container` に設定する必要があります。コンテナパッケージには通常のノードを含めることはできません。OSGi バンドル、設定、サブパッケージのみを使用できます。 AEM as a Cloud Service のコンテナは、 [インストールフック](https://jackrabbit.apache.org/filevault/installhooks.html) を使用できません。
+ コード（不変）パッケージは、`packageType` を `application` に設定する必要があります。
+ コンテンツ（可変）パッケージは、`packageType` を `content` に設定する必要があります。


詳しくは、[Apache Jackrabbit FileVault - Package Maven プラグインのドキュメント](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)、[Apache Jackrabbit パッケージタイプ](https://jackrabbit.apache.org/filevault/packagetypes.html)、以下の [FileVault Maven 設定スニペット](#marking-packages-for-deployment-by-adoube-cloud-manager) を参照してください。

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-package-types) の節を参照してください。

## Adobe Cloud Manager によるデプロイメント用のパッケージのマーク {#marking-packages-for-deployment-by-adoube-cloud-manager}

デフォルトでは、AdobeCloud Manager は、Maven ビルドで作成されたすべてのパッケージをハーベストします。 ただし、コンテナ (`all`) パッケージは、すべてのコードパッケージとコンテンツパッケージを含む単一のデプロイメントアーティファクトです。 **のみ** コンテナ (`all`) パッケージがデプロイされます。 これを確実に行うには、Maven ビルドで生成される他のパッケージを、`<properties><cloudManagerTarget>none</cloudManageTarget></properties>` という FileVault コンテンツパッケージ Maven プラグイン設定でマークする必要があります。

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#pom-xml-snippets) の節を参照してください。

## Repo Init {#repo-init}

Repo Init は、フォルダーツリーなどの一般的なノード構造から、ユーザー、サービスユーザー、グループ、ACL 定義まで、JCR 構造を定義する手順（スクリプト）を提供します。

Repo Init の主なメリットは、スクリプトで定義されたすべてのアクションを実行する暗黙の権限を持っていることです。 また、このようなスクリプトは、デプロイメントライフサイクルの初期段階で呼び出され、必要な JCR 構造がすべてタイムコードの実行時に確実に存在します。

Repo Init スクリプト自体はスクリプトとして `ui.config` プロジェクト内に存在しますが、スクリプトは次の可変構造を定義するために使用でき、また使用する必要があります。

+ ベースラインコンテンツの構造
+ サービスユーザー
+ ユーザー
+ グループ
+ ACL

Repo Init スクリプトは、 `scripts` エントリ `RepositoryInitializer` OSGi ファクトリ設定。 したがって、実行モードで暗黙的にターゲットにされる可能性があり、AEM オーサーと AEM パブリッシュサービスの Repo Init スクリプトの違い、または環境（開発、ステージ、実稼動）間での違いが考えられます。

Repo Init OSGi の設定は、複数行をサポートするため [`.config`OSGi 設定形式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)で書き込むのが最適です。これは、[`.cfg.json`OSGi 設定の定義](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)に使用するベストプラクティスの例外です。

ユーザーとグループを定義する場合、グループのみがアプリケーションの一部と見なされ、その機能に不可欠です。 AEMでは、実行時に組織のユーザーとグループを定義し続けます。 例えば、カスタムワークフローが名前付きのグループに作業を割り当てる場合、AEMアプリケーションで Repo Init を使用してそのグループを定義します。 ただし、グループ化が単に組織的なもの（「Wendy&#39;s Team」や「Sean&#39;s Team」など）の場合、AEMでは、これらのグループが最も適切に定義され、実行時に管理されます。

>[!TIP]
>
>Repo Init スクリプト *必須* インラインで定義される `scripts` フィールド、または `references` 設定が機能しません。

Repo Init スクリプトの全語彙は、[Apache Sling Repo Init ドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)で入手できます。

>[!TIP]
>
>完全なスニペットについては、この後の [Repo Init スニペット](#snippet-repo-init) の節を参照してください。

## リポジトリー構造パッケージ {#repository-structure-package}

コードパッケージでは、 `<repositoryStructurePackage>` これにより、（あるコードパッケージが別のコードパッケージをオーバーライドしないように）構造的な依存関係を正しく設定できます。 [プロジェクト用に独自のリポジトリー構造パッケージを作成](repository-structure-package.md)することができます。

**必須のみ** コードパッケージの場合は、「 `<packageType>application</packageType>`.

アプリケーション用のリポジトリー構造パッケージの作成方法については、[リポジトリー構造パッケージの作成](repository-structure-package.md)を参照してください。

コンテンツパッケージ (`<packageType>content</packageType>`) **しない** このリポジトリ構造パッケージが必要です。

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-repository-structure-package) の節を参照してください。

## コンテナパッケージへのサブパッケージの埋め込み{#embeddeds}

コンテンツパッケージまたはコードパッケージは、特別な「サイドカー」フォルダーに格納され、FileVault Maven プラグインの `<embeddeds>` 設定を使用して、AEM オーサーと AEM パブリッシュのどちらか一方または両方へのインストールの対象とすることができます。次を使用しない `<subPackages>` 設定。

一般的な使用例は次のとおりです。

+ AEM オーサーユーザーと AEM パブリッシュユーザーで異なる ACL／権限
+ AEM オーサーでのみアクティビティをサポートするために使用される設定
+ AEM オーサーでのみ実行する必要があるコード（バックオフィスシステムとの統合など）

![パッケージの埋め込み](assets/embeddeds.png)

AEMオーサーかAEMパブリッシュかその両方をターゲットにするには、パッケージを `all` コンテナパッケージを次の形式で、特別なフォルダーの場所に配置します。

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

このフォルダー構造の分類：

+ 第 1 レベルのフォルダーは `/apps` に&#x200B;**する必要があります**。
+ 第 2 レベルのフォルダーは、フォルダー名の末尾に `-packages` が付いたアプリケーションを表します。多くの場合、すべてのサブパッケージが埋め込まれる第 2 レベルのフォルダーは 1 つだけですが、アプリケーションの論理構造を最適に表すために、第 2 レベルのフォルダーをいくつでも作成できます。
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >慣例により、サブパッケージが埋め込まれるフォルダーの名前には、というサフィックスが付きます。 `-packages`. この命名方法により、デプロイメントコードパッケージとコンテンツパッケージが確実に **not** 任意のサブパッケージのターゲットフォルダーをデプロイしました `/apps/<app-name>/...`  これにより、破壊的な循環的なインストール動作が発生します。

+ 第 3 レベルのフォルダーは、
  `application`、`content`、`container`
   + `application` フォルダーにはコードパッケージが格納されます。
   + `content` フォルダーにはコンテンツパッケージが格納されます。
   + `container` フォルダーには、AEM アプリケーションに含まれる可能性のある[追加のアプリケーションパッケージ](#extra-application-packages)が格納されます。
このフォルダー名は、 [パッケージの種類](#package-types) を含める必要があります。
+ 第 4 レベルのフォルダーにはサブパッケージが格納され、次のいずれかである必要があります。
   + `install` そのため、をにインストールします。 **両方** AEM author とAEM publish
   + `install.author` そのため、 **のみ** AEMオーサー環境
   + `install.publish` そのため、 **のみ** AEM公開専用 `install.author` および `install.publish` はサポートされるターゲットです。 その他の実行モードはサポートされて&#x200B;**いません**。

例えば、AEM オーサーおよびパブリッシュに固有のパッケージを含んだデプロイメントは、次のようになります。

+ `all` コンテナパッケージに次のパッケージが埋め込まれて、単一のデプロイメントアーティファクトが作成されます。
   + `ui.apps` が `/apps/my-app-packages/application/install` に埋め込まれると、AEM オーサーと AEM パブリッシュの両方にコードがデプロイされます
   + `ui.apps.author` が `/apps/my-app-packages/application/install.author` に埋め込まれると、AEM オーサーにのみコードがデプロイされます
   + `ui.content` が `/apps/my-app-packages/content/install` に埋め込まれると、AEM オーサーと AEM パブリッシュの両方にコンテンツと設定がデプロイされます
   + `ui.content.publish` が `/apps/my-app-packages/content/install.publish` に埋め込まれると、AEM パブリッシュにのみコンテンツと設定がデプロイされます

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-embeddeds) の節を参照してください。

### コンテナパッケージのフィルター定義 {#container-package-filter-definition}

コンテナパッケージにコードおよびコンテンツサブパッケージが埋め込まれるので、埋め込まれたターゲットパスをコンテナプロジェクトの `filter.xml`. これにより、組み込みパッケージがビルド時にコンテナパッケージに確実に含まれるようになります。

単に `<filter root="/apps/<my-app>-packages"/>` デプロイするサブパッケージを含む第 2 レベルのフォルダーのエントリ。

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-container-package-filters) の節を参照してください。

## サードパーティパッケージの埋め込み {#embedding-3rd-party-packages}

すべてのパッケージは、 [Adobeの公開 Maven アーティファクトリポジトリ](https://repo1.maven.org/maven2/com/adobe/) または、公開されている参照可能なサードパーティ Maven アーティファクトリポジトリーにもアクセスできます。

サードパーティパッケージがに含まれている場合 **Adobeの公開 Maven アーティファクトリポジトリ**&#x200B;の場合は、Cloud Manager でアーティファクトを解決するためのAdobeを追加設定する必要はありません。

サードパーティパッケージが **パブリックサードパーティ Maven アーティファクトリポジトリ**&#x200B;の場合、このリポジトリをプロジェクトの `pom.xml` およびメソッドの後に埋め込まれました [上記の](#embeddeds).

サードパーティのアプリケーション/コネクタは、そのを使用して埋め込む必要があります `all` プロジェクトのコンテナ (`all`) パッケージに含まれます。

Maven の依存関係を追加する場合は、Maven の標準的な手法に従います。サードパーティアーティファクト（コードパッケージとコンテンツパッケージ）の埋め込みは、次のとおりです。 [上記の](#embedding-3rd-party-packages).

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-3rd-party-maven-repositories) の節を参照してください。

## `ui.apps` パッケージと `ui.content` パッケージの依存関係  {#package-dependencies}

パッケージを適切にインストールするために、パッケージ間の依存関係を確立することをお勧めします。

一般的なルールとしては、可変コンテンツを格納したパッケージ（`ui.content`）は、可変コンテンツのレンダリングと使用をサポートする不変コード（`ui.apps`）に依存します。

この一般的なルールの例外として重要なのは、不変コードパッケージ（`ui.apps` など）に OSGi バンドル&#x200B;__のみ__&#x200B;含まれている場合です。この場合、AEM パッケージでは不変コードパッケージへの依存関係を宣言する必要はありません。これは、不変コードパッケージに次のような理由からです。 __のみ__ に OSGi バンドルが含まれ、AEMに登録されていない [パッケージマネージャー](/help/implementing/developing/tools/package-manager.md). そのため、依存するAEMパッケージには、依存関係が満たされず、インストールに失敗します。

>[!TIP]
>
>完全なスニペットについては、この後の [POM XML スニペット](#xml-package-dependencies) の節を参照してください。

コンテンツパッケージの依存関係の一般的なパターンは以下のとおりです。

### デプロイメントパッケージ間のシンプルな依存関係 {#simple-deployment-package-dependencies}

シンプルな依存関係は、可変コンテンツパッケージ `ui.content` が不変コードパッケージ `ui.apps` に依存するように設定する場合です。

+ `all` には依存関係がありません
   + `ui.apps` には依存関係がありません
   + `ui.content` は `ui.apps` に依存しています

### デプロイメントパッケージ間の複雑な依存関係 {#complex-deploxment-package-dependencies}

複雑なデプロイメントは、シンプルなケースをさらに拡張したもので、対応する可変コンテンツパッケージと不変コードパッケージの間に依存関係を設定します。必要に応じて、不変コードパッケージ間にも依存関係を設定できます。

+ `all` には依存関係がありません
   + `common.ui.apps.common` には依存関係がありません
   + `site-a.ui.apps` は `common.ui.apps` に依存しています
   + `site-a.ui.content` は `site-a.ui.apps` に依存しています
   + `site-b.ui.apps` は `common.ui.apps` に依存しています
   + `site-b.ui.content` は `site-b.ui.apps` に依存しています

## ローカル開発とデプロイメント {#local-development-and-deployment}

この記事で概要を説明しているプロジェクト構造および編成は、ローカル開発 AEM インスタンスに&#x200B;**完全に対応**&#x200B;しています。

## POM XML スニペット {#pom-xml-snippets}

上記の推奨事項に合わせて Maven プロジェクトに追加できる Maven `pom.xml` 設定スニペットを以下に示します。

### パッケージタイプ {#xml-package-types}

サブパッケージとしてデプロイされるコードパッケージとコンテンツパッケージでは、次のパッケージタイプを宣言する必要があります。 **アプリ** または **コンテンツ**&#x200B;含まれる内容に応じて。

#### コンテナパッケージタイプ {#container-package-types}

コンテナ `all/pom.xml` プロジェクトでは `<packageType>` を宣言&#x200B;**しません**。

#### コード（不変）パッケージタイプ {#immutable-package-types}

コードパッケージでは、`packageType` を `application` に設定する必要があります。

`ui.apps/pom.xml` では、プラグイン宣言 `filevault-package-maven-plugin` のビルド設定ディレクティブ `<packageType>application</packageType>` でパッケージタイプを宣言します。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.apps</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### コンテンツ（可変）パッケージタイプ {#mutable-package-types}

コンテンツパッケージでは、`packageType` を `content` に設定する必要があります。

`ui.content/pom.xml` では、プラグイン宣言 `filevault-package-maven-plugin` のビルド設定ディレクティブ `<packageType>content</packageType>` でパッケージタイプを宣言します。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Adobe Cloud Manager によるデプロイメント用のパッケージのマーク {#cloud-manager-target}

コンテナ（`all`）プロジェクトを&#x200B;**除き**、パッケージを生成するすべてのプロジェクトでは、プラグイン宣言 `filevault-package-maven-plugin` の `<properties>` 設定に `<cloudManagerTarget>none</cloudManagerTarget>` を追加して、プロジェクトが Adobe Cloud Manager でデプロイ&#x200B;**されない**&#x200B;ようにします。コンテナ（`all`）パッケージは、Cloud Manager を通じてデプロイされる単一のパッケージでなければなりません。このパッケージに、必要なすべてのコードパッケージとコンテンツパッケージが埋め込まれます。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Repo Init {#snippet-repo-init}

Repo Init スクリプトを含む Repo Init スクリプトは、`scripts` プロパティを介して `RepositoryInitializer` OSGi ファクトリ設定で定義されます。OSGi 設定内で定義されるこれらのスクリプトは、通常の `../config.<runmode>` フォルダーセマンティクス。

スクリプトは通常複数行の宣言なので、 `.config` ファイルを、JSON ベースの `.cfg.json` 形式

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

`scripts` OSGi プロパティには、[Apache Sling の Repo Init 言語](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)で定義されたディレクティブが含まれます。

### リポジトリー構造パッケージ {#xml-repository-structure-package}

`ui.apps/pom.xml` と、コードパッケージ（`<packageType>application</packageType>`）を宣言する他の任意の `pom.xml` で、次のリポジトリー構造パッケージ設定を FileVault Maven プラグインに追加します。[プロジェクト用に独自のリポジトリー構造パッケージを作成](repository-structure-package.md)することができます。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### コンテナパッケージへのサブパッケージの埋め込み {#xml-embeddeds}

`all/pom.xml` で、次の `<embeddeds>` ディレクティブをプラグイン宣言 `filevault-package-maven-plugin` に追加します。忘れないで下さい **しない** を使用します。 `<subPackages>` 設定。 これは、 `/etc/packages` ではなく `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

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

### コンテナパッケージのフィルター定義 {#xml-container-package-filters}

内 `all` プロジェクトの `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **含める** 任意 `-packages` デプロイするサブパッケージを含むフォルダー：

```xml
<filter root="/apps/my-app-packages"/>
```

埋め込まれるターゲットで複数の `/apps/*-packages` が使用されている場合は、それらをすべてここに列挙する必要があります。

### サードパーティ Maven リポジトリ {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>Maven リポジトリをさらに追加すると、Maven リポジトリの依存関係がチェックされるので、Maven のビルド時間が長くなる場合があります。

原子炉プロジェクトの `pom.xml`に設定し、必要なサードパーティ公開 Maven リポジトリディレクティブがあれば追加します。 フル `<repository>` 設定は、サードパーティのリポジトリプロバイダーから入手できる必要があります。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### `ui.apps` パッケージと `ui.content` パッケージの依存関係  {#xml-package-dependencies}

`ui.content/pom.xml` で、次の `<dependencies>` ディレクティブをプラグイン宣言 `filevault-package-maven-plugin` に追加します。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### コンテナプロジェクトのターゲットフォルダーのクリーンアップ {#xml-clean-container-package}

内 `all/pom.xml`、 `maven-clean-plugin` Maven ビルドの前にターゲットディレクトリをクリーンアップするプラグインです。

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## その他のリソース {#additional-resources}

+ [Maven を使用したパッケージの管理](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault コンテンツパッケージ Maven プラグイン](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
