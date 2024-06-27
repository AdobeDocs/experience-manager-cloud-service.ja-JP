---
title: AEM as a Cloud Service のメンテナンスタスク
description: AEM as a Cloud Serviceのメンテナンスタスクと、その設定方法について説明します。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: 4113bb47dee5f3a2c7743f9a79c60654e58cb6bd
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 43%

---

# AEM as a Cloud Service のメンテナンスタスク {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="メンテナンスタスク"
>abstract="メンテナンスタスクとは、リポジトリを最適化するためにスケジュールに従って実行されるプロセスです。AEM as a Cloud Service を使用すると、顧客がメンテナンスタスクの運用プロパティを設定する必要が最小限になります。顧客は、インフラストラクチャの運用をアドビに任せて、リソースをアプリケーションレベルの懸念事項に集中させることができます。"

メンテナンスタスクとは、リポジトリを最適化するためにスケジュールに従って実行されるプロセスです。AEM as a Cloud Service を使用すると、顧客がメンテナンスタスクの運用プロパティを設定する必要が最小限になります。顧客は、インフラストラクチャの運用をアドビに任せて、リソースをアプリケーションレベルの懸念事項に集中させることができます。

## メンテナンスタスクの設定 {#maintenance-tasks-configuring}

以前のバージョンの AEM では、メンテナンスカード（ツール／操作／メンテナンス）を使用してメンテナンスタスクを設定できました。AEM as a Cloud Service を使用する場合、メンテナンスカードは使用できなくなったので、Cloud Manager を使用して設定をソース管理にコミットし、デプロイする必要があります。顧客側で行えない設定を含むメンテナンスタスク（データストアのガベージコレクションなど）はアドビが管理します。その他のメンテナンスタスクは顧客側で設定できます（下表を参照）。

>[!CAUTION]
>
>アドビは、パフォーマンスの低下などの問題を軽減するために、顧客のメンテナンスタスク設定を上書きする権利を保留します。

次の表に、使用可能なメンテナンスタスクを示します。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>メンテナンスタスク</th>
    <th>設定の所有者</th>
    <th>設定方法（オプション）</th>
  </tr>  
  <tr>
    <td>データストアのガベージコレクション</td>
    <td>アドビ</td>
    <td>該当なし - アドビが完全所有</td>
  </td> 
  </tr>
  <tr>
    <td>バージョンのパージ</td>
    <td>顧客</td>
    <td>バージョンのパージは現在、デフォルトで無効になっていますが、ポリシーは次の説明に従って設定できます <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">バージョンのパージと監査ログのパージのメンテナンスタスク</a> セクション。<br/><br/>間もなくデフォルトでパージが有効になり、これらの値は上書き可能になります。<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->
   </td>
  </td>
  </tr>
  <tr>
    <td>監査ログの削除</td>
    <td>顧客</td>
    <td>監査ログのパージは、現在デフォルトでは無効になっていますが、ポリシーは次のセクションで説明するように設定できます <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">バージョンのパージと監査ログのパージのメンテナンスタスク</a> セクション。<br/><br/>間もなくデフォルトでパージが有効になり、これらの値は上書き可能になります。<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->
   </td>
   </td>
  </tr>
  <tr>
    <td>Lucene バイナリクリーンアップ</td>
    <td>アドビ</td>
    <td>未使用で、アドビによって無効にされています。</td>
  </td>
  </tr>
  <tr>
    <td>アドホックタスクの削除</td>
    <td>顧客</td>
    <td>
    <p>Git で行う必要があります。フォルダー <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code> または <code>granite_monthly</code> の下でプロパティを作成することで、<code>/libs</code> 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。</p>
    <p>詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。上記のノードの下に別のノードを追加して、メンテナンスタスクを有効にします。 属性 <code>sling:resourceType</code> を <code>granite/operations/components/maintenance/task</code> に設定し、属性 <code>granite.maintenance.name</code> を <code>TaskPurge</code> に設定して、<code>granite_TaskPurgeTask</code> という名前を付けます。OSGi プロパティを設定します。プロパティのリストについては <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> を参照してください。</p>
  </td>
  </tr>
    <tr>
    <td>ワークフローのパージ</td>
    <td>顧客</td>
    <td>
    <p>Git で行う必要があります。フォルダー <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code> または <code>granite_monthly</code> の下でプロパティを作成することで、<code>/libs</code> の下にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。</p>
    <p> 上記のノードの下に別のノードを追加し（<code>granite_WorkflowPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。OSGi プロパティの設定については、<a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances?lang=ja">AEM 6.5 メンテナンスタスクのドキュメント</a>を参照してください。</p>
  </td>
  </tr>
  <tr>
    <td>プロジェクトのパージ</td>
    <td>顧客</td>
    <td>
    <p>Git で行う必要があります。フォルダー <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code> または <code>granite_monthly</code> の下でプロパティを作成することで、<code>/libs</code> の下にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。</p>
    <p>上記のノードの下に別のノードを追加し（<code>granite_ProjectPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。「アドビプロジェクトのパージ設定」の OSGI プロパティの一覧を参照してください。</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>メンテナンスウィンドウの設定</th>
    <th>設定の所有者</th>
    <th>設定の種類</th>
    <th>パラメーター</th>
  </tr>
  <tr>
    <td>毎日</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
  <td>
  <p><strong>windowSchedule=daily</strong>（この値は変更しないでください）</p>
  <p><strong>windowStartTime=HH:MM</strong>（24 時間形式）日次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</p>
  <p><strong>windowEndTime=HH:MM</strong>（24 時間形式）日次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</p>
  <p>この期間中は、メンテナンスタスクを複数回実行することはできません。</p>
  </td> 
  </tr>
  <tr>
    <td>毎週</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td>
    <p><strong>windowSchedule=weekly</strong>（この値は変更しないでください）</p>
    <p><strong>windowStartTime=HH:MM</strong>（24 時間形式）週次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</p>
    <p><strong>windowEndTime=HH:MM</strong>（24 時間形式）週次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</p>
    <p>この期間中は、メンテナンスタスクを複数回実行することはできません。</p>
    <p><strong>windowScheduleWeekdays= 1 から 7 までの 2 つの値の配列（例：[5,5]）</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</p>
    </td>
  </tr>
  <tr>
    <td>毎月</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td>
    <p><strong>windowSchedule=monthly</strong>（この値は変更しないでください）</p>
    <p><strong>windowStartTime=HH:MM</strong>（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行をいつ開始するかを定義します。</p>
    <p><strong>windowEndTime=HH:MM</strong>（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</p>
    <p>この期間中は、メンテナンスタスクを複数回実行することはできません。</p>
    <p><strong>windowScheduleWeekdays= 1 から 7 までの 2 つの値の配列（例：[5,5]）</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</p>
    <p><strong>windowFirstLastStartDay = 0 または 1</strong> 0（月の最初の週にスケジュールを設定）、1（月の最後の週にスケジュールを設定）。値を指定しない場合は、毎月 windowScheduleWeekdays の規定に従って、効果的にジョブを毎日スケジュールします。</p>
    </td>
    </tr>
    </tbody>
</table>

**ロケーション**:

* 日単位 - /apps/settings/granite/operations/maintenance/granite_daily
* 週単位 - /apps/settings/granite/operations/maintenance/granite_weekly
* 月単位 - /apps/settings/granite/operations/maintenance/granite_monthly

**コードサンプル**：

コードサンプル 1（日単位）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

コードサンプル 2（週単位）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

コードサンプル 3（月単位）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## バージョンのパージと監査ログのパージのメンテナンスタスク {#purge-tasks}

バージョンと監査ログをパージすると、リポジトリのサイズが小さくなり、シナリオによってはパフォーマンスが向上することがあります。

>[!NOTE]
>
>Adobeでは、バージョンのパージを設定しないことをお勧めします。

### デフォルト {#defaults}

現在、パージはデフォルトでは有効になっていませんが、今後変更される可能性があります。 デフォルトのパージが有効になる前に作成された環境では、予期せずパージが行われないように、より保守的なしきい値が設定されます。 デフォルトのパージポリシーについて詳しくは、以下のバージョンのパージおよび監査ログのパージの節を参照してください。
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

デフォルトのパージ値は、設定ファイルを宣言して以下のようにデプロイすることで上書きできます。

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### 設定の適用 {#configure-purge}

次の手順の説明に従って、設定ファイルを宣言し、デプロイします。

>[!NOTE]
>設定ファイルにバージョンのパージノードをデプロイしたら、そのノードを宣言されたままにし、削除しないようにする必要があります。 設定パイプラインを実行しようとすると、失敗します。
> 
>同様に、設定ファイルに監査ログのパージノードをデプロイしたら、そのノードを宣言されたままにし、削除しないようにする必要があります。

**1** - Git のプロジェクトの最上位フォルダーに、次のフォルダーとファイル構造を作成します。

```
config/
     mt.yaml
```

**2**  – 設定ファイルのプロパティを宣言します。これには次が含まれます。

* 値が「MaintenanceTasks」の「kind」プロパティ。
* 「version」プロパティ（現在バージョン 1 です）。
* プロパティを持つオプションの「metadata」オブジェクト `envTypes` と、この設定が有効な環境タイプ（開発、ステージ、実稼動）のコンマ区切りリストを追加します。 メタデータオブジェクトが宣言されていない場合、設定はすべての環境タイプに対して有効です。
* 両方が含まれているデータオブジェクト `versionPurge` および `auditLogPurge` オブジェクト。

の定義と構文を参照してください `versionPurge` および `auditLogPurge` 下のオブジェクト。

次の例のように、設定を構築する必要があります。

```
kind: "MaintenanceTasks"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  versionPurge:
    maximumVersions: 15
    maximumAgeDays: 20
    paths: ["/content"]
    minimumVersions: 1
    retainLabelledVersions: false
  auditLogPurge:
    rules:
      - replication:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
      - pages:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
      - dam:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
```

設定を有効にするには、次の点に注意してください。

* すべてのプロパティを定義する必要があります。 継承されたデフォルトはありません。
* 以下のプロパティテーブルのタイプ（整数、文字列、ブール値など）を考慮する必要があります。

>[!NOTE]
>次を使用できます `yq` 設定ファイルの YAML 形式をローカルで検証するには（例：） `yq mt.yaml`）に設定します。

**3**  – 実稼動以外の設定パイプラインと実稼動設定パイプラインを設定します。

迅速な開発環境（RDE）では、パージはサポートされていません。 実稼動（サンドボックス以外）プログラムに他の環境タイプを使用する場合は、Cloud Managerでターゲットデプロイメント設定パイプラインを作成します。

参照： [実稼動パイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) および [実稼動以外のパイプラインの設定](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) を参照してください。

### バージョンのパージ {#version-purge}

>[!NOTE]
>
>Adobeでは、バージョンのパージを設定しないことをお勧めします。

#### バージョンの消去の既定値 {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

現在、パージはデフォルトでは有効になっていませんが、今後変更される可能性があります。

デフォルトのパージが有効になった後に作成された環境には、次のデフォルト値が設定されます。

* 30 日より古いバージョンは削除されます。
* 過去 30 日間の最新の 5 つのバージョンが保持されます。
* 上記のルールに関係なく、（現在のファイルに加えて）最新バージョンが保持されます。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

デフォルトのパージが有効になる前に作成された環境では、以下に示すデフォルト値が使用されますが、パフォーマンスを最適化するには、これらの値を下げることをお勧めします。

* 7 年以上前のバージョンは削除されます。
* 過去 7 年間のすべてのバージョンが保持されます。
* 7 年後に、最新バージョン以外のバージョン（現在のファイルに加えて）が削除されます。

#### バージョンのパージプロパティ {#version-purge-properties}

許可されるプロパティを以下に示します。

を示す列 *default* デフォルトが適用された場合に、今後デフォルト値を指定する。 *未定* まだ決定されていない環境 id を反映します。

| プロパティ | 環境の今後のデフォルト > 未定 | 環境の今後のデフォルト &lt;=未定 | 必須 | タイプ | 値 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| パス | [「/content」] | [「/content」] | はい | 文字列の配列 | 新しいバージョンが作成された際にバージョンをパージするパスを指定します。  顧客はこのプロパティを宣言する必要がありますが、許可されている値は「/content」のみです。 |
| maximumAgeDays | 30 | 2557 （7 年+2 閏日） | はい | 整数 | 設定された値より古いバージョンはすべて削除されます。 この値が 0 の場合、バージョンの期間に基づいたパージは実行されません。 |
| maximumVersions | 5 | 0 （制限なし） | はい | 整数 | n 番目に新しいバージョンより古いバージョンはすべて削除されます。 この値が 0 の場合、バージョンの数に基づいたパージは実行されません。 |
| minimumVersions | 1 | 1 | はい | 整数 | 期間にかかわらず保持するバージョンの最小数。 少なくとも 1 つのバージョンが常に保持されることに注意してください。値は 1 以上にする必要があります。 |
| retainLabeledVersioned | false | false | はい | ブーリアン | 明示的にラベル付けされたバージョンをパージから除外するかどうかを決定します。 リポジトリの最適化を高めるには、この値を false に設定することをお勧めします。 |


**プロパティの操作**

以下の例は、プロパティを組み合わせた場合の相互作用を示しています。

例：

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

23 日目に 11 のバージョンがある場合、最も古いバージョンは、次回メンテナンスタスクをパージするときにパージされます。これは、 `maximumVersions` プロパティは 10 に設定されます。

31 日目に 5 つのバージョンがある場合、次の理由から 3 のみがパージされます `minimumVersions` プロパティは 2 に設定されます。

例：

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

以下の場合、30 日より新しいバージョンはパージされません。 `maximumVersions` プロパティは 0 に設定されます。

30 日より古いバージョンが 1 つ保持されます。

### 監査ログの削除 {#audit-purge}

#### 監査ログの消去の既定値 {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

現在、パージはデフォルトでは有効になっていませんが、今後変更される可能性があります。

デフォルトのパージが有効になった後に作成された環境には、次のデフォルト値が設定されます。

* 7 日以上前のレプリケーション、DAM およびページ監査ログは削除されます。
* 考えられるすべてのイベントがログに記録されます。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

デフォルトのパージが有効になる前に作成された環境では、以下に示すデフォルト値が使用されますが、パフォーマンスを最適化するには、これらの値を下げることをお勧めします。

* 7 年以上前のレプリケーション、DAM およびページ監査ログは削除されます。
* 考えられるすべてのイベントがログに記録されます。

>[!NOTE]
>編集不可能な監査ログを作成するという規制要件があるお客様は、専門の外部サービスと統合することをお勧めします。

#### 監査ログのパージプロパティ {#audit-purge-properties}

許可されるプロパティを以下に示します。

を示す列 *default* デフォルトが適用された場合に、今後デフォルト値を指定する。 *未定* まだ決定されていない環境 id を反映します。


| プロパティ | 環境の今後のデフォルト > 未定 | 環境の今後のデフォルト &lt;=未定 | 必須 | タイプ | 値 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| ルール | - | - | はい | オブジェクト | レプリケーション、ページ、dam の 1 つ以上のノード。 これらの各ノードは、ルールを定義し、以下のプロパティを設定します。 すべてのプロパティを宣言してください。 |
| maximumAgeDays | 7 日 | 2557 （7 年+2 うるう日） | はい | integer | レプリケーション、ページ、dam のいずれかの場合：監査ログが保持される日数。 設定された値より古い監査ログはパージされます。 |
| contentPath | 「/content」 | 「/content」 | はい | 文字列 | 関連するタイプについて、監査ログがパージされるパス。 「/content」に設定する必要があります。 |
| タイプ | すべての値 | すべての値 | はい | 列挙の配列 | の場合 **複製**&#x200B;列挙値は Activate、Deactivate、Delete、Test、Reverse、Internal Poll です。 の場合 **ページ**、列挙値は次のとおりです。PageCreated、PageModified、PageMoved、PageDeleted、VersionCreated、PageRestored、PageRolled Out、PageValid、PageInvalid。 の場合 **dam**、列挙値は次のとおりです。ASSET_EXPIRING、METADATA_UPDATED、ASSET_EXPIRED、ASSET_REMOVED、RESTORED、ASSET_MOVED、ASSET_VIEWED、PROJECT_VIEWED、PUBLISHED_EXTERNAL、COLLECTION_VIEWED、VERSIONED、ADDED_COMMENT、RENDITION_UPDATED、ACCEPTED、DOWNLOADED、SUBASSET_UPDATED、SUBASSET_REMOVED、ASSET_CREATED、ASSET_ASSET_CREATED、ASSET ASSET RENDITION_REMOVED、ASSET_PUBLISHED、ORIGINAL_UPDATED、RENDITION_DOWNLOADED、REJECTED。 |
