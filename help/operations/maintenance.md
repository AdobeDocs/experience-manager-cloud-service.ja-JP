---
title: AEM as a Cloud Service のメンテナンスタスク
description: AEM as a Cloud Serviceのメンテナンスタスクと、その設定方法について説明します。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: 5de6ff7e6ac777c90b41bfeb9a56b909c83ed7d3
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 96%

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

### メンテナンスタスク {#maintenance-tasks}

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
    <td>バージョンのパージは現在、デフォルトで無効になっていますが、<a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">バージョンのパージと監査ログのパージのメンテナンスタスク</a>の節の説明に従うことで、ポリシーを設定できます。<br/><br/>パージはすぐにデフォルトで有効になり、これらの値は上書き可能になります。<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>監査ログのパージ</td>
    <td>顧客</td>
    <td>監査ログののパージは現在、デフォルトで無効になっていますが、<a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">バージョンのパージと監査ログのパージのメンテナンスタスク</a>の節の説明に従うことで、ポリシーを設定できます。<br/><br/>パージはすぐにデフォルトで有効になり、これらの値は上書き可能になります。<br>
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
    <p>上記のノードの下に別のノードを追加し（<code>granite_WorkflowPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。OSGi プロパティの設定については、「<a href="/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances"> ワークフローインスタンスの定期的なパージ </a>」を参照してください。</p>
  </td>
  </tr>
  <tr>
    <td>プロジェクトのパージ</td>
    <td>顧客</td>
    <td>
    <p>Git で行う必要があります。フォルダー <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code> または <code>granite_monthly</code> の下でプロパティを作成することで、<code>/libs</code> の下にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。</p>
    <p>上記のノードの下に別のノードを追加し（<code>granite_ProjectPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。<b>アドビプロジェクトのパージ設定</b>の <a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">OSGi プロパティ</a>のリストを参照してください。</p>
  </td>
  </tr>
  </tbody>
</table>

### メンテナンスウィンドウの設定 {#maintenance-window-configurations}

次の表に、使用可能なメンテナンスウィンドウ設定を示します。

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

### ロケーション {#locations}

* 日単位 - /apps/settings/granite/operations/maintenance/granite_daily
* 週単位 - /apps/settings/granite/operations/maintenance/granite_weekly
* 月単位 - /apps/settings/granite/operations/maintenance/granite_monthly

### コードサンプル {#code-samples}

**コードサンプル 1 （毎日）**

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

**コードサンプル 2 （毎週）**

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

**コードサンプル 3 （毎月）**

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

## バージョンパージと監査ログパージのメンテナンスタスク {#purge-tasks}

バージョンと監査ログをパージすると、リポジトリのサイズが小さくなり、シナリオによってはパフォーマンスが向上する場合があります。

>[!NOTE]
>
>AEM Guides のお客様は、バージョンパージを設定しないでください。

### デフォルト {#defaults}

現在、デフォルトではパージが有効になっていませんが、今後変更される予定です。
デフォルトのパージが有効になる前に作成された環境では、予期せずパージが行われないように、より保守的なしきい値が設定されます。デフォルトのパージポリシーについて詳しくは、以下のバージョンパージおよび監査ログパージの節を参照してください。
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

デフォルトのパージ値は、以下で説明するように、設定ファイルを宣言してデプロイすることで上書きできます。

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### 設定の適用 {#configure-purge}

次の手順に従って、設定ファイルを宣言し、デプロイします。

>[!NOTE]
>設定ファイルにバージョンのパージノードをデプロイしたら、それを削除せずに宣言したままにしておく必要があります。実行しようとすると、設定パイプラインが失敗します。
> 
>同様に、設定ファイルに監査ログのパージノードをデプロイしたら、それを削除せずに宣言したままにする必要があります。

1. `mt.yaml` などの名前のファイルを作成します。

1. `config` 設定パイプラインの使用 [ の説明に従って、ファイルを ](/help/operations/config-pipeline.md#folder-structure) または類似の名前の最上位フォルダーの下のどこかに配置します。

1. 設定ファイルのプロパティを宣言します。次にプロパティを示します。

   * データノードの上のいくつかのプロパティ -- 説明については、[設定パイプラインの使用](/help/operations/config-pipeline.md#common-syntax)を参照してください。`kind`プロパティの値は *MaintenanceTasks* に、バージョンは *1* に設定する必要があります。

   * `versionPurge` と `auditLogPurge` オブジェクトの両方を含むデータオブジェクト。

   以下の `versionPurge` と `auditLogPurge` オブジェクトの定義と構文を参照してください。

   次の例のように設定を構築する必要があります。

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

   * すべてのプロパティを定義する必要があります。デフォルトは継承されません。
   * 以下のプロパティテーブルのタイプ（整数、文字列、ブール値など）を考慮する必要があります。

1. [config パイプラインの記事 ](/help/operations/config-pipeline.md#managing-in-cloud-manager) の説明に従って、Cloud Managerで config パイプラインを作成します。

### バージョンのパージ {#version-purge}

>[!NOTE]
>
>AEM Guides のお客様は、バージョンパージを設定しないでください。

#### バージョンパージのデフォルト {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

現在、デフォルトではパージが有効になっていませんが、今後変更される予定です。


デフォルトのパージが有効になった後に作成した環境には、次のデフォルト値が設定されます。

* 30 日より古いバージョンは削除されます。
* 過去 30 日間で最新 5 つのバージョンが保持されます。
* 上記のルールに関係なく、（現在のファイルに加えて）最新バージョンが保持されます。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

デフォルトのパージが有効になる前に作成した環境には、以下に示すデフォルト値が設定されますが、パフォーマンスを最適化するために、これらの値を小さくすることをお勧めします。

* 7 年より古いバージョンは削除されます。
* 過去 7 年間のすべてのバージョンが保持されます。
* 7 年後、最新バージョン以外のバージョン（現在のファイルに加えて）が削除されます。

#### バージョンパージのプロパティ {#version-purge-properties}

許可されるプロパティを以下に示します。

*デフォルト*&#x200B;を示す列は、デフォルトが適用される今後のデフォルト値を示します。*未定*&#x200B;は、まだ決定されていない環境 ID を反映します。

| プロパティ | TBD 以降の環境の今後のデフォルト | TBD 以前の環境の今後のデフォルト | 必須 | タイプ | 値 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| パス | [「/content」] | [「/content」] | はい | 文字列の配列 | 新しいバージョンが作成された際にバージョンをパージする、パスを指定します。お客様はこのプロパティを宣言する必要がありますが、使用できる値は「/content」のみです。 |
| maximumAgeDays | 30 | 2557（7 年 + 2 日のうるう日） | はい | 整数 | 設定した値より古いバージョンは、すべて削除されます。この値が 0 の場合、バージョンの経過期間に基づいたパージは実行されません。 |
| maximumVersions | 5 | 0（制限なし） | はい | 整数 | n 番目に新しいバージョンより古いバージョンは、すべて削除されます。この値が 0 の場合、バージョンの数に基づいたパージは実行されません。 |
| minimumVersions | 1 | 1 | はい | 整数 | 期間にかかわらず保持するバージョン数の最小数。1 つ以上のバージョンが常に保持されます。値は 1 以上にする必要があります。 |
| retainLabeledVersioned | false | false | はい | ブール値 | 明示的にラベル付けされたバージョンをパージから除外するかどうかを決定します。リポジトリの最適化を向上させるには、この値を false に設定することをお勧めします。 |

**プロパティのインタラクション**

次の例は、プロパティを組み合わせた場合の操作を示しています。

例：

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

23 日目に 11 個のバージョンがある場合、`maximumVersions` プロパティが 10 に設定されているので、次にパージメンテナンスタスクを実行する際には最も古いバージョンがパージされます。

31 日目に 5 個のバージョンがある場合、`minimumVersions` プロパティが 2 に設定されているので、パージされるのは 3 個だけです。

例：

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

`maximumVersions` プロパティが 0 に設定されているので、30 日より新しいバージョンはパージされません。

30 日より古いバージョンが 1 つ保持されます。

### 監査ログのパージ {#audit-purge}

#### 監査ログのパージのデフォルト {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

現在、デフォルトではパージが有効になっていませんが、今後変更される予定です。


デフォルトのパージが有効になった後に作成した環境には、次のデフォルト値が設定されます。

* 7 日より古いレプリケーション、DAM、ページの監査ログは削除されます。
* 考えられるすべてのイベントがログに記録されます。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

デフォルトのパージが有効になる前に作成した環境には、以下に示すデフォルト値が設定されますが、パフォーマンスを最適化するために、これらの値を小さくすることをお勧めします。

* 7 年より古いレプリケーション、DAM 、ページの監査ログは削除されます。
* 考えられるすべてのイベントがログに記録されます。

>[!NOTE]
>編集不可能な監査ログを作成し、専門の外部サービスと統合するという規制要件があるお客様にお勧めします。

#### 監査ログのパージのプロパティ {#audit-purge-properties}

許可されるプロパティを以下に示します。

*デフォルト*&#x200B;を示す列は、デフォルトが適用される今後のデフォルト値を示します。*未定*&#x200B;は、まだ決定されていない環境 ID を反映します。

| プロパティ | TBD 以降の環境の今後のデフォルト | TBD 以前の環境の今後のデフォルト | 必須 | タイプ | 値 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| ルール | - | - | はい | オブジェクト | レプリケーション、ページ、DAM の 1 つ以上のノード。これらの各ノードは、以下のプロパティでルールを定義します。すべてのプロパティを宣言する必要があります。 |
| maximumAgeDays | 7 日 | すべて、2557（7 年 + 2 日のうるう日） | はい | 整数 | レプリケーション、ページ、DAM のいずれかの場合：監査ログが保持される日数。設定された値より古い監査ログはパージされます。 |
| contentPath | 「/content」 | 「/content」 | はい | 文字列 | 関連するタイプについて、監査ログがパージされるパス。「/content」に設定する必要があります。 |
| types | すべての値 | すべての値 | はい | 列挙の配列 | **レプリケーション**&#x200B;の場合、列挙値は次のとおりです：Activate、Deactivate、Delete、Test、Reverse、Internal Poll。**ページ**&#x200B;の場合、列挙値は次のとおりです：PageCreated、PageModified、PageMoved、PageDeleted、VersionCreated、PageRestored、PageRolled Out、PageValid、PageInvalid。**DAM** の場合、列挙値は次のとおりです：ASSET_EXPIRING、METADATA_UPDATED、ASSET_EXPIRED、ASSET_REMOVED、RESTORED、ASSET_MOVED、ASSET_VIEWED、PROJECT_VIEWED、PUBLISHED_EXTERNAL、COLLECTION_VIEWED、VERSIONED、ADDED_COMMENT、RENDITION_UPDATED、ACCEPTED、DOWNLOADED、SUBASSET_UPDATED、SUBASSET_REMOVED、ASSET_CREATED、ASSET_SHARED、RENDITION_REMOVED、ASSET_PUBLISHED、ORIGINAL_UPDATED、RENDITION_DOWNLOADED、REJECTED。 |
