---
title: Sling サービスユーザーマッピングとサービスユーザー定義のベストプラクティス
description: Sling サービスユーザーマッピングとサービスユーザー定義のベストプラクティスについて説明します
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 99%

---

# Sling サービスユーザーマッピングとサービスユーザー定義のベストプラクティス {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## サービスユーザーマッピング {#service-user-mapping}

サービスから対応するシステムユーザーへのマッピングを追加するには、`ServiceUserMapper` サービスのファクトリ設定を作成する必要があります。このモジュラーを維持するために、Sling の「修正」メカニズムを使用してこのような設定を指定できます（詳しくは、[SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) を参照してください）。このような設定をバンドルと共にインストールするには、次の例で説明するように、クイックスタートプロビジョニングモデルに追加することをお勧めします。

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### マッピング形式 {#mapping-format}

AEM 6.4 以降、マッピング形式は次のように定義されます。

>[!NOTE]
>
>`userName` は非推奨（廃止予定）なので、使用しないでください。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` と `subserviceName` はサービスを識別し、`userName/principalNames` はサービスユーザーを識別します。`principalNames` はコンマ区切りのリストです。

また、`principalNames` は、標準では ID と同じであるサービスユーザープリンシパル名のリストです。


**ベストプラクティス**

* 様々なタスクのサブサービス名 - バンドルのサービスが様々なタスクを実行する場合は、`subserviceNames` を識別してタスク別にグループ化することをお勧めします
* 特定のサービスが様々な操作（例えば、アセットコンテンツの読み取りや `/var` のサブツリー以下の情報の更新）を実行する場合は、共通の `dam-reader-service` と機能固有の `assetreport-writer-service` を集約するなど、個々の操作を反映する様々なサービスプリンシパルを集約して、反映することをお勧めします
* 各サービスは理想的には、非常に具体的で限定された一連の操作にバインドされます。
* AEM 6.4 では、サービスユーザーマッピングを定義する方法として `[one,or,multiple,principalNames]` を使用した新しい形式をお勧めします。

形式を変更する理由と、単一のユーザー ID に対してのみバージョンマッピングの代わりにその形式を使用することをアドビがお勧めする理由のリストを以下に示します。

* お客様の特別なニーズと一般的なタスクを組み合わせて、サービスユーザーを再利用する機能
* 権限設定の重複を回避します
* 特定のサービスが実際に実行する効果的な権限（およびタスク）に関する理解を深めます
* サービスユーザーの明示的なグループメンバーシップは不要です。グループの権限を変更すると、問題となる副作用が生じる可能性があります
* パフォーマンスの向上とスケーラビリティ

## マッピングの解決とサービスログイン {#mapping-resolution-and-service-login}

### サービスマッピングの解決 {#service-mapping-resolution}

サービスマッピングを解決するための呼び出しのシーケンスは、次のようになります。

1. 指定された `bundleId` と `subserviceName` に対するアクティブな `principalNames` マッピングを検索します
1. `bundleId` と null `subserviceName` の `principalNames` マッピング
1. `bundleId` と `subserviceName` の `userName` マッピング
1. `bundleId` と null `subserviceName` の `userName` マッピング
1. デフォルトのマッピング
1. デフォルトのユーザー

### SlingRepository - サービスログイン {#slingrepository-servicelogin}

サービス `Session/ResourceResolver` を取得するシーケンスは次のようになります。

1. 以下の説明に従って、`ServiceUserMapper`／事前認証リポジトリログインからプリンシパル名を取得します。
1. `ServiceUserMapper` からユーザー ID を取得します
1. 現在のユーザー ID について非推奨（廃止予定）の `1ServiceUserConfiguration` を確認
1. ユーザー ID を使用したデフォルトの Sling サービスログイン（例えば、`createAdministrativeSession` のシーケンスと、サービスユーザー ID の別のユーザーとしての実行）

プリンシパル名を使用した新しいマッピングにより、リポジトリへのログインが次のように簡素化されます。

* プリンシパル名のセットは、`Subject` の入力に使用される有効なプリンシパルとして処理されます
* その結果、リポジトリへのログインを事前認証できます
* グループメンバーシップの解決はありません

  >[!NOTE]
  >
  >必要なすべての権限をサービスユーザーに対して宣言する必要があります。「everyone」とその他のグループ権限は継承されなくなります。

* サービス `Session/ResourceResolver` を作成するための追加の管理者ログインは作成されません。

### 非推奨（廃止予定）の ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

マッピングで単一のユーザー名を指定することは、既存の `ServiceUserConfiguration.simpleSubjectPopulation` と同等であることに注意してください。新しい形式では、`ServiceUserConfiguration` によって提供される回避策をサービスユーザーマッピングに直接反映できます。したがって、`ServiceUserConfiguration` は AEM では非推奨（廃止予定）となり、既存の使用法はすべて置き換えられました。

## サービスユーザー {#service-users}

### 既存のサービスユーザーの再利用 {#reusing-existing-service-users}

次の条件を満たす場合は、既存のサービスユーザーを再利用することをお勧めします。

* ニーズが既存のサービスユーザーの意図と一致する
* サービスでは、既存の共通サービスユーザーが担当する共通タスクを実行する必要がある。この場合、重複を導入する代わりに、サービスユーザーを再利用することをお勧めします
* サービスでは、既存のサービスユーザーが担当する特定のタスクが必要である。不明な場合は、所有する機能チームにお問い合わせください。

次の場合は、既存のサービスユーザーを再利用しません。

* 機能させるには、関係のない方法で権限を変更する必要がある
* 提供される権限の小さなサブセットのみが必要で、実際に一致するからではなく、機能が動作するので、これを再利用するのみの場合
* その名前が必要とするものとはまったく異なる意図を示している場合。機能するからといってこれを選択すると、特定のサービスを所有する機能チームが権限を変更して機能を破損する場合があるので、将来的に問題が発生する可能性があります。

### サービスユーザーの作成 {#creating-a-service-user}

AEM の既存のサービスユーザーがユースケースに適していないことを確認し、対応する RTC の問題が承認されたら、引き続きデフォルトコンテンツに新しいユーザーを追加できます。拡張セキュリティチームのメンバーが RTC 投票に参加するのが理想的です。そのため、適切な関係者の参加も必要です。

**命名規則**

AEM セキュリティチームは、新しいサービスユーザーに一貫性を与え、読みやすさと保守性を向上させるために、サービスユーザー向けに次の命名規則を定義しました。

サービスユーザー名は、ダッシュ&#x200B;**「-」**&#x200B;で区切られた次の 3 つの要素で構成されます。

1. サービス操作のターゲットとなる論理エンティティ／機能（変更される可能性のあるパス要素を回避します）
1. サービスが実行するタスク
1. ID とプリンシパル名からユーザーがサービスユーザーであることを簡単に特定できる、末尾の&#x200B;**「service」**

**ベストプラクティス**

* 異なるエンティティ／機能を混在させないでください。サービスのニーズが異なる場合は、個々のサービスユーザーに分割し、マッピングで集約します
* サービスユーザーごとに、明確に定義されたタスクを 1 つに制限します。多すぎる権限や無関係な権限を付与することになった場合は分割します
* 時間をかけて、サービスの真のニーズを特定します
* 時間をかけて、意味があり、わかりやすいサービスユーザー名を見つけます
* フィードバックとレビューを依頼します。機能に詳しくない開発者でも、意図を読んで理解できる必要があります。将来的には、修正または保守する任務を負う可能性があります。

最後に、サービスユーザー名によって次の内容が明確になります。

* 使用目的と再利用の可否：

   * 非常に一般的：`content-writer-service`。サービスもすべてのコンテンツを読み取る必要がある場合は、集約で安全に再利用できます
   * 非常に具体的：`asset-linkshare-service`。サービスがアセットのリンク共有も実際に行わない限り、再利用は安全ではありません。

* 機能セットおよび権限の設定は、次のようになります。

   * 論理エンティティは、次の権限設定と一致する必要があります。

      * `content-foo-service` は、コンテンツに対する操作にのみ関連付ける必要があります。設定やユーザーなどの他のエンティティを操作する権限を付与するのは適切ではありません
      * `personalization-foo-service` などの特定のサービスには、特定の権限も付与する必要があります。すべてのコンテンツに権限を付与することになった場合、その権限は具体的ではなくなります。これを名前に反映するか、集約で共通のユーザーを再利用します
      * `msm-xyz-service` などの機能固有のサービスには、msm 関連の権限のみが必要です。Communities 設定や Screens ユーザーの管理など、無関係な機能に対して権限を拡張しないでください。

   * タスクは、以下の権限と一致する必要があります。

      * `foo-reader-service` は、通常の項目のみ読み取り可能である必要があります。書き込み権限を付与しないでください
      * `foo-writer-service` は、書き込み操作を実行することが想定できます。ただし、アクセス制御コンテンツを読み取り／変更する権限は付与しないでください
      * `foo-replicator-service` には `crx:replicate` が付与されることが想定できます。

**例**

`configuration-reader-service` の例：

* この名前は、DM 統合の設定など、特定の機能の設定ではなく、一般的な設定を参照していることを示しています。このような統合の設定を読み取ることを特別にターゲットとするサービスユーザーには、`dmconfig-reader-service` または `s7config-reader-service` という名前が付けられます

  >[!NOTE]
  >
  >名前付けにはパス情報は含まれません。設定は `/etc` から `/conf` に移行しました。

* タスク要素は、そのユーザーにバインドされたサービスが読み取り操作のみを実行することを示します。

`userproperties-copy-service` の例：

* このサービスユーザーにバインドされたサービスは、プロファイルや環境設定などのユーザー／グループのプロパティに基づいて動作します
* あらゆる種類の書き込み操作を含む `userproperties-writer-service` のような名前とは対照的に、その情報をコピーすることだけを目的としています。したがって、これらのコピータスクの権限設定では、ある場所での項目の追加と別の場所での項目の削除のみが許可されている可能性があります。

**権限設定のベストプラクティス**

* サービスユーザーには、常にプリンシパルベースのアクセス制御設定を使用します。詳しくは、以下の例を参照してください。

   * Skyline でサービスユーザーとその権限を不変アプリケーションコンテンツとしてマークできるようにします
   * パスやツリー構造を作成する必要はありません

* 権限のみを付与し、拒否しないでください
* 権限を制限します。

   * 必要な最小限の権限セットのみを付与します
   * 詳しくは、[項目への権限のマッピング](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html)および [API 呼び出しの権限へのマッピング](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html)のドキュメントを参照してください
   * `jcr:all` に権限を付与しないでください。これは、最小限のセットではない可能性があります。

* 範囲を減らします

   * 機能固有のサブツリーにアクセス制御ポリシーを配置します
   * 配布済み項目の場合：制限を使用して範囲を制限します（ビルトインの制限のリストについては、[ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)を参照してください）。

* 一貫性を確保します

   * サービスユーザー名で使用したエンティティとタスクに対して権限の一貫性を持たせます
   * 無関係な権限を追加することは回避します。例えば、`workflow-administration-service` があり、これに `/home/users/screens` でユーザー管理操作を実行する権限を付与したり、s7-config を読み取らせたりするのは奇妙です。

* 完全性

   * サービスが意図したタスクの実行に必要なすべての権限を持っていることを確認します。サービスは、顧客環境でも標準で機能させる必要があります。
   * お客様に権限設定（例えば、`/apps` 以下）を拡張することを期待したり要求したりしないでください。

* 権限設定の重複を回避します

   * 共通のサービスユーザーを再利用します
   * さらに必要な特定の権限を提供する機能固有のサービスユーザーを集約します

* 異なる機能間で権限設定を分割しないでください。これが必要なのは、サービスユーザーが適切に定義されていないか、様々な処理が多すぎることを示しています
* サービスユーザーをグループに配置しないでください。理由は次のとおりです。

   * サービスユーザーと「パブリック」グループからの実装の詳細が混在してしまう
   * 権限の変更を制御できない（回帰や権限のエスカレーションが発生しやすい）
   * ログインと評価のパフォーマンス
   * プリンシパルベースの ac-setup では機能しません

* 予測可能なパスを持たないユーザーホームノード（またはそこに含まれる任意のサブツリー）へのアクセスは、リポジトリ初期化でホーム（`userId`）を使用して実現されます。詳しくは、Sling リポジトリ初期化の[ドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html)を参照してください。
* RTC：既存のサービスユーザーの権限を変更する場合は専用の RTC の問題を作成し、セキュリティチームによるレビューを受ける必要があります。

**リポジトリ初期化を使用した作成**

常に `repo-init` を使用してサービスユーザーとその権限設定を定義し、両方をクイックスタート機能モデルの正しいセクションに配置します。

**ベストプラクティス**

* 必ず `repo-init` を使用してサービスユーザーを作成します
* 必ずサービスユーザー作成用に中間パスを指定します
* AEM のすべてのビルトインのサービスユーザーは、`system/cq:services/internal` の下に配置する必要があります
* また、機能ごとにサービスユーザーをグループ化するための中間相対パス（`system/cq:services/internal/<your-feature>`）に追加します
* 顧客定義のサービスユーザーは `system/cq:services/<customer-intermediate-rel-path>` の下に配置する必要があります。内部ツリーの下には配置しないでください
* ユーザーが既に存在し、プリンシパルベースの認証をサポートする新しい場所に移動する必要がある場合は、**パスあり**&#x200B;の代わりに&#x200B;**適用パスあり**&#x200B;を使用します。

**例**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### サービスユーザーと権限のクリーンアップ {#cleanup-service-users-and-permissions}

次の repo init コマンドを使用すると、未使用のサービスユーザーとその権限をクリーンアップできます。

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### サービスユーザーのテスト {#testing-service-users}

サービスユーザーとその権限設定のサーバーサイドテストを作成することが重要です。これは、設定が実際に機能することを検証するだけでなく、アクセス制御コンテンツやサービスユーザーを変更する際の回帰や意図しない間違いを特定するのにも役立ちます。

`com.adobe.granite.testing.clients` ライブラリには、サービスユーザー向けの SST の記述を簡単にする多くのユーティリティが用意されています。
