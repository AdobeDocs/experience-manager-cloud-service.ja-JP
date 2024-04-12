---
title: AEM as a Cloud Service のメンテナンスタスク
description: AEM as a Cloud Serviceのメンテナンスタスクと、その設定方法について説明します。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 4ac5ec2a2b8da90820734e4fc06c084c810c0724
workflow-type: ht
source-wordcount: '1129'
ht-degree: 100%

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

次の表に、AEM as a Cloud Service のリリース時に使用できるメンテナンスタスクを示します。

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
    <td>アドビ</td>
    <td>既存の環境（2024年4月15日（PT）より前に作成された環境）の場合、パージは無効になっており、今後はデフォルトを 7年間として有効になる予定です。顧客は、より低いカスタム値（30 日など）で設定できるようになります。<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->新しい環境（2024年4月15日（PT）以降に作成された環境）では、デフォルトで以下の値でパージが有効になり、顧客はカスタム値を使用して設定できます。
     <ol>
       <li>31 日以上前のバージョンは削除されます</li>
       <li>過去 30 日間の最新の 5 つのバージョンが保持されます</li>
       <li>上記のルールに関係なく、最新バージョンが保持されます</li>
       <br>規制要件があるお客様は、特定の日付に表示されたとおりにサイトページをレンダリングし、専門の外部サービスと統合することをお勧めします。
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>監査ログの削除</td>
    <td>アドビ</td>
    <td>既存の環境（2024年4月15日（PT）より前に作成された環境）の場合、パージは無効になっており、今後はデフォルトを 7年間として有効になる予定です。顧客は、より低いカスタム値（30 日など）で設定できるようになります。<br><br> <!-- See above for the two line breaks -->新しい環境（2023年4月1日（PT）以降に作成された環境）では、次の動作に従って、リポジトリの <code>/content</code> ノードでデフォルトでパージが有効になります。
     <ol>
       <li>レプリケーション監査の場合、4 日以上前の監査ログは削除されます</li>
       <li>DAM（アセット）監査の場合、31 日以上前の監査ログは削除されます</li>
       <li>ページ監査の場合、4 日以上前のログは削除されます</li>
       <br>編集不可能な監査ログを作成し、専門の外部サービスと統合するという規制要件があるお客様にお勧めします。
     </ol></td>
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
