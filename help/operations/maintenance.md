---
title: Cloud ServiceとしてのAEMのメンテナンスタスク
description: 'Cloud ServiceとしてのAEMのメンテナンスタスク '
translation-type: tm+mt
source-git-commit: e9ee1064c5fa62b56c822a18ad6ca8cc4d09fa75
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# Cloud ServiceとしてのAEMのメンテナンスタスク

メンテナンスタスクとは、リポジトリを最適化するためにスケジュールに従って実行されるプロセスです。 AEMをCloud Serviceとして使用する場合、メンテナンスタスクの運用プロパティを設定する必要性は最小限に抑えられます。 お客様は、リソースをアプリケーションレベルの懸念事項に絞り込み、インフラストラクチャの運用をアドビに委ねることができます。

メンテナンスタスクの詳細については、次のページを参照してください。

* [AEMメンテナンスガイド](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [運用ダッシュボードの保守タスク](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## メンテナンスタスクの設定

AEMの以前のバージョンでは、メンテナンスカード（ツール/操作/メンテナンス）を使用してメンテナンスタスクを設定できました。 Cloud ServiceとしてのAEMの場合、メンテナンスカードは使用できなくなり、設定はCloud Managerを使用してソース管理に委任し、デプロイする必要があります。 アドビは、お客様が決定する必要のないメンテナンスタスク（データストアガベージコレクションなど）を管理し、他のメンテナンスタスクはお客様が設定できます（下の表を参照）。

>[!CAUTION]
>
>アドビは、パフォーマンスの低下などの問題を軽減するために、お客様のメンテナンスタスク設定を上書きする権利を保留します。

次の表に、AEMのリリース時にCloud Serviceとして使用可能なメンテナンスタスクを示します。

| メンテナンスタスク | 設定の所有者 | 設定方法（オプション） |
|---|---|---|
| データストアのガベージコレクション | アドビ | 該当なし — 完全にアドビが所有 |
| バージョンのパージ | アドビ | アドビが完全に所有していますが、将来は、お客様は特定のパラメーターを設定できるようになります。 |
| 監査ログの削除 | アドビ | アドビが完全に所有していますが、将来は、お客様は特定のパラメーターを設定できるようになります。 |
| Lucene バイナリクリーンアップ | アドビ | 未使用のため、アドビで無効にされています。 |
| アドホックタスクの削除 | 顧客 | Githubで行う必要があります。 <br> フォルダーまたはの下にプロパティを作成することで、の下にあ `/libs` る標準のメンテナンスウィンドウ設定ノードを上書き `/apps/settings/granite/operations/maintenance/granite_weekly` し `granite_daily`ます。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上記のノードの下に別のノードを追加し（名前を付けて）、適切なプロパティを追加して、メンテナンスタスク `granite_TaskPurgeTask`を有効にします。 <br> OSGIプロパティの設定については、 [AEM 6.5メンテナンスタスクドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| ワークフローのパージ | 顧客 | Githubで行う必要があります。 <br> フォルダー `/libs` またはの下にプロパティを作成することで、の下にある標準搭載のメンテナンスウィンドウ設定ノードを上書き`/apps/settings/granite/operations/maintenance/granite_weekly``granite_daily`します。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上記のノードの下に別のノードを追加し（名前を付けて）、適切なプロパティを追加して、メンテナンスタスク `granite_WorkflowPurgeTask`を有効にします。 <br> OSGIプロパティの設定については、 [AEM 6.5メンテナンスタスクドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| プロジェクトのパージ | 顧客 | Githubで行う必要があります。 <br> フォルダーまたはの下にプロパティを作成することで、の下にあ `/libs` る標準のメンテナンスウィンドウ設定ノードを上書き `/apps/settings/granite/operations/maintenance/granite_weekly` し `granite_daily`ます。 詳細な設定については、以下の「メンテナンスウィンドウ」の表を参照してください。 <br> 上のノードの下に適切なプロパティを持つノードを追加(名前を付ける `granite_ProjectPurgeTask`)して、メンテナンスタスクを有効にします。 <br> OSGIプロパティの設定については、 [AEM 6.5メンテナンスタスクドキュメントを参照してください](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

ユーザーは、ワークフローの削除、アドホックタスクの削除およびプロジェクトの削除の保守タスクのそれぞれを、日別、週別、月別の保守期間中に実行するようにスケジュールできます。 これらの設定は、ソース管理で直接編集する必要があります。 次の表に、各ウィンドウで使用可能な設定パラメータを示します。

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
    <td>JCRノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_daily </code></td>
    <td>以下のコードサンプル1を参照してください。</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 日別メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 日次メンテナンスウィンドウに関連付けられたメンテナンスタスクが、まだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎週</td>
    <td>顧客</td>
    <td>JCRノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_weekly</code></td>
    <td>以下のコードサンプル2を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = weekly（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 週別のメンテナンスウィンドウに関連付けられたメンテナンスタスクの実行を開始するタイミングを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 週単位のメンテナンスウィンドウに関連付けられたメンテナンスタスクが、まだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7の2つの値の配列。 例えば [5,5].</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2番目の値はジョブが停止される終了日です。 開始と終了の正確な時刻は、それぞれwindowStartTimeとwindowEndTimeで管理されます。</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>毎月</td>
    <td>顧客</td>
    <td>JCRノード定義</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_monthly</code></td>
    <td>以下のコードサンプル3を参照してください。</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = daily（この値は変更しないでください）</li>
    <li><strong>windowStartTime</strong> = HH:MM（24時間形式） 月別メンテナンスウィンドウに関連付けられたメンテナンスタスクの実行をいつ開始するかを定義します。</li>
    <li><strong>windowEndTime</strong> = HH:MM（24時間形式） 月別メンテナンスウィンドウに関連付けられたメンテナンスタスクが、まだ完了していない場合に、その実行を停止するタイミングを定義します。</li>
    <li><strong>windowScheduleWeekdays = 1 ～ 7の2つの値の配列。 例えば [5,5].</strong> 配列の最初の値はジョブがスケジュールされる開始日で、2番目の値はジョブが停止される終了日です。 開始と終了の正確な時刻は、それぞれwindowStartTimeとwindowEndTimeで管理されます。</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0（月の最初の週にスケジュールを設定）、1は月の最後の週にスケジュールを設定（設定）。 値を指定しないと、毎月windowScheduleWeekdaysの規定に従って、ジョブを毎日効果的にスケジュールします。</li>
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
