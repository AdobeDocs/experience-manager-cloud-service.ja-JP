---
title: Sling サービスユーザーマッピングおよびサービスユーザー定義のベストプラクティス
description: Sling サービスユーザーマッピングおよびサービスユーザー定義のベストプラクティスについて説明します
source-git-commit: b6f7b6996b377ecfa372742ce1ad22139547ebdd
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---


# Sling サービスユーザーマッピングおよびサービスユーザー定義のベストプラクティス {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## サービスユーザーマッピング {#service-user-mapping}

サービスから対応するシステムユーザーへのマッピングを追加するには、のファクトリ設定を作成する必要があります `ServiceUserMapper` サービス。 このモジュールを維持するために、Sling の「修正」メカニズムを使用して、このような設定を行うことができます（ [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) 詳しくは、「」を参照してください。 このような設定をバンドルと共にインストールする場合は、次の例で説明するように、クイックスタートのプロビジョニングモデルに追加します。

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
>この `userName` は非推奨のため、使用しないでください。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` および `subserviceName` サービスの特定 `userName/principalNames` サービスユーザーを特定し、 `principalNames` はコンマ区切りのリストです。

また、次のことにも注意してください `principalNames` は、標準提供の id と同じサービスユーザープリンシパル名のリストです。


**ベストプラクティス**

* 様々なタスクのサブサービス名 – バンドルのサービスで異なるタスクを実行する場合は、識別することをお勧めします `subserviceNames` タスク別にグループ化するには
* 特定のサービスが異なる操作を実行する場合（例えば、アセットのコンテンツの読み取りや、サブツリーの下の情報の更新） `/var`）に設定し、共通のものを集約する場合と同様に、個々の操作を反映した様々なサービスプリンシパルを集約して、これを反映することをお勧めします `dam-reader-service` （機能固有） `assetreport-writer-service`
* 各サービスは、非常に具体的で限定的な一連の操作に結び付くのが理想的です
* を使用した新しい形式 `[one,or,multiple,principalNames]` は、AEM 6.4 以降でサービスユーザーマッピングを定義する方法をお勧めします。

以下に、形式を変更する理由と、Adobeが 1 つの userID に対してのみバージョンマッピングの代わりに形式を使用することをお勧めする理由を一覧表示します。

* お客様の特別なニーズと一般的なタスクを組み合わせて、サービス・ユーザーを再利用する機能
* 権限設定の重複を避ける
* 特定のサービスが実際に実行する効果的な権限（およびタスク）に関する理解を深める
* サービスユーザーの明示的なグループメンバーシップは不要です。 グループ権限が変更されると、厄介な副作用が生じる可能性があります
* パフォーマンスの向上と拡張性

## 解決とサービスログインのマッピング {#mapping-resolution-and-service-login}

### サービスマッピングの解決 {#service-mapping-resolution}

以下に説明するサービスマッピングを解決するための一連の呼び出し。

1. アクティブのを検索 `principalNames` 特定ののマッピング `bundleId` および `subserviceName`
1. `principalNames` のマッピング `bundleId` および null `subserviceName`
1. `userName` のマッピング `bundleId` および `subserviceName`
1. `userName` マッピング : `bundleId` および null `subserviceName`
1. デフォルトのマッピング
1. デフォルトのユーザー

### SlingRepository - サービスログイン {#slingrepository-servicelogin}

サービスを取得するためのシーケンス `Session/ResourceResolver` は次のように動作します。

1. からプリンシパル名を取得 `ServiceUserMapper` => 以下に説明する認証前のリポジトリログイン
1. からのユーザー ID の取得 `ServiceUserMapper`
1. 現在のユーザー ID について、非推奨の 1ServiceUserConfiguration&#39;がないか確認します
1. ユーザー ID を使用したデフォルトの Sling サービスログイン（例えば、のシーケンス） `createAdministrativeSession` およびサービスユーザー id で別のユーザーとして実行）

プリンシパル名を使用した新しいマッピングにより、次のようなシンプルなリポジトリログインが実現します。

* プリンシパル名のセットは、の入力に使用される有効なプリンシパルとして扱われます `Subject`
* その結果、リポジトリへのログインを事前認証できます
* グループメンバーシップの解決なし

  >[!NOTE]
  >
  >サービスユーザーに対して、必要なすべての権限を宣言する必要があります。 &#39;everyone&#39;とその他のグループの権限は継承されなくなります。

* サービスを利用するための追加の admin-login はありません。`Session/ResourceResolver` が作成されます。

### 非推奨の ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

マッピングで単一のユーザー名を指定すると、既存の `ServiceUserConfiguration.simpleSubjectPopulation`. 新しい形式では、によって提供される回避策 `ServiceUserConfiguration` サービスユーザーマッピングを使用して直接反映できます。 この `ServiceUserConfiguration` したがって、はAEMでは非推奨（廃止予定）となり、既存の使用方法はすべて置き換えられます。

## サービスユーザー {#service-users}

### 既存のサービスユーザーの再利用 {#reusing-existing-service-users}

次の条件を満たす場合は、既存のサービスユーザーを再利用することをお勧めします。

* ニーズは、既存のサービスユーザーの意図と一致します
* サービスは、既存の共通サービスユーザーが担当する共通タスクを実行する必要があります。 この場合、重複を導入する代わりに、サービスユーザーを再利用することをお勧めします
* サービスには、既存のサービスユーザーがカバーする特定のタスクが必要です。 不明な場合は、機能を所有する機能チームにお問い合わせください。

次の場合は、既存のサービスユーザーを再利用しません。

* 機能させるには、無関係な方法でその権限を変更する必要があります
* 提供される権限のごく一部のみが必要で、それが本当の一致だからではなく、機能が機能するので、それを再利用する場合です
* その名前があなたが必要とするものとは全く異なる意図を示すならば。 特定のサービスを所有する機能チームが権限を変更し、機能を破損する可能性があるので、これが機能するので、問題が発生する可能性があります。

### サービスユーザーの作成 {#creating-a-service-user}

AEMの既存のサービスユーザーがユースケースに適用できず、対応する RTC の問題が承認されたことを確認したら、続行して、新しいユーザーをデフォルトコンテンツに追加できます。 拡張セキュリティチームのメンバーが RTC 投票に関与するのが理想なので、適切な関係者の協力も必要です。

**命名規則**

AEM セキュリティチームは、新しいサービスユーザーに一貫性を持たせ、読みやすさと保守性を向上させるために、サービスユーザーの命名規則を次のように定義しました。

サービスユーザー名は、ダッシュで区切られた 3 つの要素で構成されます **&#39;-&#39;**:

1. サービス操作の対象となる論理エンティティ /機能（変更される可能性のあるパス要素を避けます）
1. サービスが実行するタスク
1. 末尾 **&#39;サービス&#39;** id とプリンシパル名からユーザーがサービスユーザーであることを容易に特定できるようにする

**ベストプラクティス**

* 異なるエンティティ/フィーチャーを混在させないでください。 サービスのニーズが異なる場合は、個々のサービスユーザーに分割し、マッピングで集約します
* サービスユーザーごとに 1 つの適切に定義されたタスクに制限します。 権限の付与数が多すぎる、または無関係な場合に分割します
* サービスの真のニーズを特定するために時間を費やす
* 時間をかけて、適切で意味のある、わかりやすいサービスユーザー名を見つけます
* フィードバックとレビューを依頼：あなたの機能に慣れていない開発者は、あなたの意図を読み、理解できるはずです。 将来的には、修正またはメンテナンスの依頼を受ける可能性があります。

最後に、サービスユーザー名は次のようになります。

* 使用方法と再利用の可否：

   * 非常に一般的： `content-writer-service`. サービスがすべてのコンテンツを読み取る必要がある場合、集計で安全に再利用できます
   * 非常に具体的： `asset-linkshare-service`. サービスがアセットのリンク共有も実際に行わない限り、再利用しても安全ではありません。

* 機能セットおよび権限の設定は、次のようになります。

   * 論理エンティティは、権限設定と一致する必要があります。

      * A `content-foo-service` は、コンテンツに対する操作にのみ関連付ける必要があります。 設定やユーザーなど、他のエンティティを操作する権限を IT に付与するのは適切ではありません
      * のような特定のサービス `personalization-foo-service` には、特定の権限も付属している必要があります。 すべてのコンテンツに対する権限を付与することになると、その権限は特定されなくなります。 それを名前で反映するか、集計で一般的なユーザーを再利用します
      * のような機能固有のサービス `msm-xyz-service` には、msm 関連の権限のみを割り当ててください。 コミュニティ設定や Screens ユーザーの管理など、無関係な機能に対して権限を拡張しないでください。

   * タスクは、権限と一致する必要があります。

      * A `foo-reader-service` は、通常の項目の読み取りのみ可能です。 書き込み権限を付与しない
      * A `foo-writer-service` 書き込み操作の実行が期待できます。 ただし、アクセス制御コンテンツを読み取り/変更する権限は付与しないでください
      * A `foo-replicator-service` 期待される可能性がある `crx:replicate` 許可されました。

**例**

の例 `configuration-reader-service`:

* この名前は、DM 統合の設定など、特定の機能の設定ではなく、一般的な設定を参照していることを示しています。 このような統合の設定を読み取ることを特別にターゲットとするサービスユーザーには、次のような名前を付けます `dmconfig-reader-service` または `s7config-reader-service`

  >[!NOTE]
  >
  >名前にパス情報は含まれません。 設定が次から移動しました `/etc` 対象： `/conf`.

* task-element は、そのユーザーにバインドされたサービスが読み取り操作のみを実行することを示します。

の例 `userproperties-copy-service`:

* このサービスユーザーにバインドされたサービスは、プロファイルや環境設定などのユーザー/グループのプロパティで動作します
* のような名前とは対照的に、単にその情報をコピーすることをターゲットとしています。 `userproperties-writer-service` これはあらゆる種類の書き込み操作を含みます。 したがって、これらのコピータスクの権限設定では、ある場所での項目の追加と別の場所での項目の削除のみが許可される場合があります。

**権限の設定のベストプラクティス**

* サービスユーザーには、常にプリンシパルベースのアクセス制御設定を使用します。 詳しくは、以下の例を参照してください。

   * サービス ユーザーとその権限を不変アプリケーション コンテンツとして Skyline にマークすることを許可します
   * パスやツリー構造を作成する必要がありません

* 権限のみを付与し、拒否しない
* 権限を制限します。

   * 必要な最小限の権限セットのみを付与します
   * 詳しくは、を参照してください [項目への権限のマッピング](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) および [API 呼び出しの権限へのマッピング](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) 詳細を見る
   * 次の権限を付与しない： `jcr:all`. これは最小限のセットではないでしょう。

* 範囲を減らす

   * 機能固有のサブツリーにアクセス制御ポリシーを配置する
   * 配布済みアイテムの場合：制限を使用して範囲を制限します（を参照） [ドキュメント](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) （組み込み制限のリストの場合）。

* 一貫性の確保

   * サービスユーザー名で使用したエンティティとタスクに対して権限の一貫性を持たせる
   * 無関係な権限を追加しないでください。 例えば、 `workflow-administration-service` でユーザー管理操作を実行する権限を it に付与します。 `/home/users/screens` または、s7-config と読ませます。

* 完全性

   * サービスが意図したタスクの実行に必要なすべての権限を持っていることを確認します。 お客様の環境でも、サービスが標準で動作する必要があります。
   * 次に示すような権限の設定を、顧客が展開することを期待したり、依頼したりしないでください `/apps`）

* 権限設定の重複を避ける

   * 一般的なサービスユーザーの再利用
   * さらに、必要な特定の権限を提供する機能固有のサービスユーザーと集計します

* 権限設定を異なる機能に分割しないでください。 これが必要なのは、サービスユーザーが適切に定義されていないか、様々な処理が多すぎることを示しています
* サービスユーザーをグループに配置しないでください。理由は次のとおりです。

   * サービスユーザーからの実装の詳細を「公開」グループと混在させます。
   * 権限の変更を制御できない（リグレッションや権限のエスカレーションが発生する傾向がある）
   * ログインと評価のパフォーマンス
   * プリンシパルベースの ac セットアップでは動作しません

* home （`userId`）に設定します。 Sling repo init を参照してください。 [詳細を見る](https://sling.apache.org/documentation/bundles/repository-initialization.html) を参照してください。
* RTC：既存のサービスユーザーの権限を変更し、セキュリティチームにレビューしてもらったら、専用の RTC イシューを作成します。

**リポジトリの初期化を使用した作成**

常に使用 `repo-init` サービスユーザーとその権限の設定を定義し、両方をクイックスタート機能モデルの正しいセクションに配置するには：

**ベストプラクティス**

* 常に使用 `repo-init` サービスユーザーを作成するには
* サービスユーザー作成の中間パスを常に指定する
* AEMのビルトインサービスユーザーはすべて、の下に配置する必要があります `system/cq:services/internal`
* さらに、を機能ごとにサービスユーザーをグループ化するための中間相対パスに追加します。 `system/cq:services/internal/<your-feature>`
* お客様定義のサービスユーザーは、次の場所に配置する必要があります `system/cq:services/<customer-intermediate-rel-path>` 内部ツリーの下には配置しない
* 使用方法 **強制パスを使用** の代わりに **パスを使用** ユーザーがすでに存在し、プリンシパルベースの認証をサポートする新しい場所に移動する必要がある場合。

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

### サービスのユーザーと権限のクリーンアップ {#cleanup-service-users-and-permissions}

次の repo init コマンドを使用して、未使用のサービスユーザーとその権限をクリーンアップできます。

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

サービスユーザーとその権限設定を対象としたサーバーサイドテストを作成することが重要です。 これにより、設定が実際に機能することを確認できるだけでなく、アクセス制御コンテンツやサービスユーザーを変更する際にリグレッションや意図しないミスを見つけるのに役立ちます。

この `com.adobe.granite.testing.clients` ライブラリには、サービスユーザー向けの SST の記述を容易にする多くのユーティリティが用意されています。





