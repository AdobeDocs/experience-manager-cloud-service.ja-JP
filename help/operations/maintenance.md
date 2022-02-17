---
title: AEM as a Cloud Service のメンテナンスタスク
description: AEM as a Cloud Service のメンテナンスタスク
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 7ff9cabe239c8e474b03c4ecce6d32bf659665a7
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 97%

---

# AEM as a Cloud Service のメンテナンスタスク

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="メンテナンスタスク"
>abstract="メンテナンスタスクとは、リポジトリーを最適化するためにスケジュールに従って実行されるプロセスです。AEM as a Cloud Service を使用すると、顧客がメンテナンスタスクの運用プロパティを設定する必要が最小限になります。顧客は、インフラストラクチャの運用をアドビに任せて、リソースをアプリケーションレベルの懸念事項に集中させることができます。"

メンテナンスタスクとは、リポジトリーを最適化するためにスケジュールに従って実行されるプロセスです。AEM as a Cloud Service を使用すると、顧客がメンテナンスタスクの運用プロパティを設定する必要が最小限になります。顧客は、インフラストラクチャの運用をアドビに任せて、リソースをアプリケーションレベルの懸念事項に集中させることができます。

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
| アドホックタスクの削除 | 顧客 | Github で行う必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br> 上記のノードの下に別のノードを追加し（`granite_TaskPurgeTask` という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクのドキュメント](https://helpx.adobe.com/jp/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |
| ワークフローのパージ | 顧客 | Github で行う必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br> 上記のノードの下に別のノードを追加し（`granite_WorkflowPurgeTask` という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクドキュメント](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |
| プロジェクトのパージ | 顧客 | Github で行う必要があります。<br> `/apps/settings/granite/operations/maintenance/granite_weekly` フォルダーまたは `granite_daily` フォルダーにプロパティを作成することで、`/libs` 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。<br>上記のノードの下に適切なプロパティを持つノードを追加し（`granite_ProjectPurgeTask` と命名します）、メンテナンスタスクを有効にします。<br> OSGI プロパティの設定については、[AEM 6.5 メンテナンスタスクドキュメント](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)を参照してください。 |

ユーザーは、ワークフローの削除、アドホックタスクの削除およびプロジェクトの削除のメンテナンスタスクのそれぞれを、日別、週別、月別の保守期間中に実行するようにスケジュールできます。これらの設定は、ソース管理で直接編集する必要があります。次の表に、各ウィンドウで使用可能な設定パラメータを示します。また、表の後に示す場所とコードサンプルも参照してください。

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
    <td>アドビが完全に所有していますが、将来は、顧客が特定のパラメーターを設定できるようになります。</td>
  </td>
  </tr>
  <tr>
    <td>監査ログの削除</td>
    <td>アドビ</td>
    <td>アドビが完全に所有していますが、将来は、顧客が特定のパラメーターを設定できるようになります。</td>
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
    <p>Github で行う必要があります。 <code>/libs</code> フォルダーまたは <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> フォルダーにプロパティを作成することで、<code>granite_daily</code> 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。</p>
    <p>詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 上記のノードの下に別のノードを追加し（<code>granite_TaskPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。OSGi プロパティを設定する場合は、 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5 メンテナンスタスクドキュメント</a>.</p>
  </td>
  </tr>
    <tr>
    <td>ワークフローのパージ</td>
    <td>顧客</td>
    <td>
    <p>Github で行う必要があります。 <code>/libs</code> フォルダーまたは <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> フォルダーにプロパティを作成することで、<code>granite_daily</code> 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。</p>
    <p> 上記のノードの下に別のノードを追加し（<code>granite_WorkflowPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。OSGi プロパティの設定については、 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5 メンテナンスタスクドキュメント</a>.</p>
  </td>
  </tr>
  <tr>
    <td>プロジェクトのパージ</td>
    <td>顧客</td>
    <td>
    <p>Github で行う必要があります。 <code>/libs</code> フォルダーまたは <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> フォルダーにプロパティを作成することで、<code>granite_daily</code> 内にある標準のメンテナンスウィンドウ設定ノードを上書きします。詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。</p>
    <p> 上記のノードの下に別のノードを追加し（<code>granite_ProjectPurgeTask</code> という名前を付けて）、適切なプロパティを追加して、メンテナンスタスクを有効にします。OSGi プロパティの設定については、 <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">AEM 6.5 メンテナンスタスクドキュメント</a>.</p>
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
    <p><strong>windowScheduleWeekdays= 1 から 7 までの 2 つの値の配列（例： [5,5]）</strong>配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</p>
    </td>
  </tr>
  <tr>
    <td>毎月</td>
    <td>顧客</td>
    <td>JCR ノード定義</td>
    <td>
    <p><strong>windowSchedule=daily</strong>（この値は変更しないでください）</p>
    <p><strong>windowStartTime=HH:MM</strong>（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行をいつ開始するかを定義します。</p>
    <p><strong>windowEndTime=HH:MM</strong>（24 時間形式）月次メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、その実行を停止するタイミングを定義します。</p>
    <p><strong>windowScheduleWeekdays= 1 から 7 までの 2 つの値の配列（例： [5,5]）</strong>配列の最初の値はジョブがスケジュールされる開始日で、2 番目の値はジョブが停止される終了日です。開始と終了の正確な時刻は、それぞれ windowStartTime と windowEndTime で管理されます。</p>
    <p><strong>windowFirstLastStartDay = 0 または 1</strong> 0（月の最初の週にスケジュールを設定）、1（月の最後の週にスケジュールを設定）。値を指定しないと、毎月 windowScheduleWeekdays の規定に従って、事実上ジョブを毎日スケジュールします。</p>
    </td> 
    </tr>
    </tbody>
</table>

**ロケーション**:

* 日単位 - /apps/settings/granite/operations/maintenance/granite_daily
* 週単位 - /apps/settings/granite/operations/maintenance/granite_weekly
* 月単位 — /apps/settings/granite/operations/maintenance/granite_monthly

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
