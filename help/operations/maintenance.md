---
title: AEM as a Cloud Service のメンテナンスタスク
description: 'AEM as a Cloud Service のメンテナンスタスク '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 100%

---


# AEM as a Cloud Service のメンテナンスタスク

メンテナンスタスクとは、リポジトリーを最適化するためにスケジュールに従って実行されるプロセスです。AEM as a Cloud Service を使用すると、顧客がメンテナンスタスクの運用プロパティを設定する必要が最小限になります。顧客は、インフラストラクチャの運用をアドビに任せて、リソースをアプリケーションレベルの懸念事項に集中させることができます。

メンテナンスタスクの詳細については、次のページを参照してください。

* [AEM メンテナンスガイド](https://helpx.adobe.com/jp/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [運用ダッシュボードのメンテナンスタスク](https://helpx.adobe.com/jp/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## メンテナンスタスクの設定

以前のバージョンの AEM では、メンテナンスカード（ツール／操作／メンテナンス）を使用してメンテナンスタスクを設定できました。AEM as a Cloud Service を使用する場合、メンテナンスカードは使用できなくなったので、Cloud Manager を使用して設定をソース管理にコミットし、デプロイする必要があります。アドビは、顧客の判断を必要としないメンテナンスタスク（データストアのガベージコレクションなど）を管理します。他のメンテナンスタスクは顧客が設定できます（下の表を参照）。

>[!CAUTION]
>
>アドビは、パフォーマンスの低下などの問題を軽減するために、顧客のメンテナンスタスク設定を上書きする権利を保留します。

次の表に、AEM as a Cloud Service のリリース時に使用できるメンテナンスタスクを示します。

| メンテナンスタスク | 設定の所有者 | 設定方法（オプション） |
|---|---|---|
| データストアのガベージコレクション | アドビ | 該当なし - アドビが完全所有 |
| バージョンのパージ | アドビ | アドビが完全に所有していますが、将来は、顧客が特定のパラメーターを設定できるようになります。 |
| 監査ログの削除 | アドビ | アドビが完全に所有していますが、将来は、顧客が特定のパラメーターを設定できるようになります。 |
| Lucene バイナリクリーンアップ | アドビ | 未使用で、アドビによって無効にされています。 |
| アドホックタスクの削除 | 顧客 | Github でおこなう必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br> 上記のノードの下に別のノードを追加し（`granite_TaskPurgeTask` という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクのドキュメント](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |
| ワークフローのパージ | 顧客 | Github でおこなう必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br> 上記のノードの下に別のノードを追加し（`granite_WorkflowPurgeTask` という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクドキュメント](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |
| プロジェクトのパージ | 顧客 | Github でおこなう必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br>上記のノードの下に適切なプロパティを持つノードを追加し（`granite_ProjectPurgeTask` と命名します）、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクドキュメント](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |

ユーザーは、ワークフローの削除、アドホックタスクの削除およびプロジェクトの削除のメンテナンスタスクのそれぞれを、日別、週別、月別の保守期間中に実行するようにスケジュールできます。これらの設定は、ソース管理で直接編集する必要があります。次の表に、各ウィンドウで使用可能な設定パラメータを示します。

<table>
  <tr>
    <th>メンテナンスウィンドウの設定</th>
    <th>設定の所有者</th>
    <th>設定の種類</th>
    <th>場所</th>
    <th>例</th>
    <th>パラメーター</th>
  </tr>
  <tr>
    <td>毎日</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_daily </code></td>
    <td>以下のコードサンプル 1 を参照してください。</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24 時間形式）  日次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24 時間形式）日次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎週</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_weekly</code></td>
    <td>以下のコードサンプル 2 を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24 時間形式）週次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24 時間形式）週次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7 の 2 つの値の配列（例：[5,5]）</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎月</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_monthly</code></td>
    <td>以下のコードサンプル 3 を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行をいつ開始するかを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7 の 2 つの値の配列（例：[5,5]）</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</li>
    <li><strong>windowFirstLastStartDay - 0 または 1</strong> 0（月の最初の週にスケジュールを設定）、1（月の最後の週にスケジュールを設定）。値を指定しないと、毎月 windowScheduleWeekdays の規定に従って、事実上ジョブを毎日スケジュールします。</li>
    </ul> </td> 
  </tr>
</table>

コードサンプル 1

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

コードサンプル 2

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

コードサンプル 3

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
