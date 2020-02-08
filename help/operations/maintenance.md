---
title: クラウドサービスとしてのAEMのメンテナンスタスク
description: 'クラウドサービスとしてのAEMのメンテナンスタスク '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# クラウドサービスとしてのAEMのメンテナンスタスク

メンテナンスタスクは、リポジトリを最適化するためにスケジュールに従って実行されるプロセスです。 AEMをクラウドサービスとして使用する場合、お客様がメンテナンスタスクの運用プロパティを設定する必要は最小限に抑えられます。 お客様は、アプリケーションレベルの懸念にリソースを集中させ、インフラストラクチャの運用をアドビに委ねることができます。

メンテナンスタスクに関するその他の情報については、次のページを参照してください。

* [AEMメンテナンスガイド](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [操作ダッシュボードのメンテナンスタスク](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## メンテナンスタスクの設定

以前のバージョンのAEMでは、メンテナンスカード（ツール/操作/メンテナンス）を使用してメンテナンスタスクを設定できました。 クラウドサービスとしてのAEMの場合、メンテナンスカードは使用できなくなったので、設定をソース管理にコミットし、Cloud Managerを使用してデプロイする必要があります。 アドビは、お客様が決定する必要のないメンテナンスタスク（データストアのガベージコレクションなど）を管理し、他のメンテナンスタスクはお客様が設定できます（下の表を参照）。

>[!CAUTION]
>
>アドビは、パフォーマンスの低下などの問題を緩和するために、お客様のメンテナンスタスクの設定を上書きする権利を留保します。

次の表に、AEMのクラウドサービスとしてのリリース時に使用できるメンテナンスタスクを示します。

| メンテナンスタスク | 設定の所有者 | 設定方法（オプション） |
|---|---|---|
| データストアのガベージコレクション | アドビ | 該当なし — 完全にアドビが所有 |
| バージョンのパージ | アドビ | アドビが完全に所有していますが、将来は、お客様が特定のパラメーターを設定できるようになる予定です。 |
| 監査ログの削除 | アドビ | アドビが完全に所有していますが、将来は、お客様が特定のパラメーターを設定できるようになる予定です。 |
| Lucene バイナリクリーンアップ | アドビ | 未使用のため、アドビでは無効にしています。 |
| アドホックタスクの削除 | 顧客 | githubで行う必要があります。 <br> との下のメンテナンスウィンドウ設定ノードを、または `/libs` で上 `/apps` 書き `/conf/global/settings/granite/operations/maintenance/granite_weekly` しま `granite_daily`す。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上記のノードの下に別のノードを追加し（名前を付け）、適切なプロパティを持たせて、メンテナ `granite_TaskPurgeTask`ンスタスクを有効にします。 <br> OSGIプロパティの設定については、 [AEM 6.5メンテナンスタスクのドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| ワークフローのパージ | 顧客 | githubで行う必要があります。 <br> との下のメンテナンスウィンドウ設定ノードを、または `/libs` で上 `/apps` 書き `/conf/global/settings/granite/operations/maintenance/granite_weekly` しま `granite_daily`す。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上記のノードの下に別のノードを追加し（名前を付け）、適切なプロパティを持たせて、メンテナ `granite_WorkflowPurgeTask`ンスタスクを有効にします。 <br> OSGIプロパティの設定について詳しくは、 [AEM 6.5メンテナンスタスクのドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| プロジェクトのパージ | 顧客 | githubで行う必要があります。 <br> との下のメンテナンスウィンドウ設定ノードを、または `/libs` で上 `/apps` 書き `/conf/global/settings/granite/operations/maintenance/granite_weekly` しま `granite_daily`す。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上記のノードの下に適切なプロパティを持つノードを追加して（名前を付けて）、メンテナンス `granite_ProjectPurgeTask`タスクを有効にします。 <br> OSGIプロパティの設定については、 [AEM 6.5メンテナンスタスクのドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

お客様は、毎日、毎週、または毎月のメンテナンス期間中に実行されるワークフローの削除、アドホックタスクの削除、およびプロジェクトの削除のメンテナンスの各タスクをスケジュールできます。 これらの設定は、ソース管理で直接編集する必要があります。 次の表に、各ウィンドウで使用可能な設定パラメータを示します。

<table>
  <tr>
    <th>メンテナンスウィンドウの設定</th>
    <th>設定の所有者</th>
    <th>設定タイプ</th>
    <th>場所</th>
    <th>例</th>
    <th>パラメーター</th>
  </tr>
  <tr>
    <td>毎日</td>
    <td>顧客</td>
    <td>JCRノード定義</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_daily </code> (これはとのノードを上書 <code>/apps</code> きしま <code>/libs</code>す)</td>
    <td>以下のコードサンプル1を参照してください。</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 日別メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 日別メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、そのタスクの実行を停止するタイミングを定義します。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎週</td>
    <td>顧客</td>
    <td>JCRノード定義</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code> (これはとのノードを上書 <code>/apps</code> きしま <code>/libs</code>す)</td>
    <td>以下のコードサンプル2を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 週別メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 週別メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、そのタスクの実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7の2つの値の配列。 例：[5,5].</strong> 配列の最初の値はジョブがスケジュールされた開始日で、2番目の値はジョブが停止される終了日です。 開始と終了の正確な時刻は、それぞれwindowStartTimeとwindowEndTimeによって制御されます。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎月</td>
    <td>顧客</td>
    <td>JCRノード定義</td>
    <td><code>/conf/global/settings/granite/operations/maintenance/granite_monthly</code> (これはとのノードを上書 <code>/apps</code> きしま <code>/libs</code>す)</td>
    <td>以下のコードサンプル3を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 月別メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 月別メンテナンスウィンドウに関連付けられたメンテナンスタスクがまだ完了していない場合に、そのタスクの実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7の2つの値の配列。 例：[5,5].</strong> 配列の最初の値はジョブがスケジュールされた開始日で、2番目の値はジョブが停止される終了日です。 開始と終了の正確な時刻は、それぞれwindowStartTimeとwindowEndTimeによって制御されます。</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0で月の最初の週にスケジュールを設定し、1で月の最後の週にスケジュールを設定します。 値がないと、毎月windowScheduleWeekdaysの規定に従って、ジョブが毎日効果的にスケジュールされます。</li>
    </ul> </td> 
  </tr>
</table>

コード例1

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

コード例2

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

コード例3

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
