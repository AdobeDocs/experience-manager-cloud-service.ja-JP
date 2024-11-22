---
title: UUID 参照のコンテンツフラグメントのアップグレード
description: ヘッドレスコンテンツ配信用にAdobe Experience Manager as a Cloud Serviceで最適化された UUID 参照のために、コンテンツフラグメントをアップグレードする方法を説明します。
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 5aa04f3b042f8e9f9af97148ceab0288ff210238
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# UUID 参照のコンテンツフラグメントのアップグレード {#upgrade-content-fragments-for-UUID-references}

>[!IMPORTANT]
>
>コンテンツフラグメントで使用するGraphQL API の様々な機能は、早期導入プログラムを通じて利用できます。
>
>ステータスと、関心のあるユーザーへの適用方法を確認するには、[ リリースノート ](/help/release-notes/release-notes-cloud/release-notes-current.md) を確認してください。

GraphQL フィルターの安定性を最適化するには、コンテンツフラグメント内のコンテンツとフラグメント参照をアップグレードして、ユニバーサル固有識別子（UUID）を使用するようにします。

コンテンツフラグメントモデルは元々、**コンテンツ参照** と **フラグメント参照** のデータタイプを提供していました。 これらの参照はどちらも、参照先のリソースを指すパスを使用しており、リソースを移動すると、このパスが古くなる可能性があります。 このような参照は、ほとんどのシナリオでは十分ですが、コンテンツフラグメントモデルが拡張されて、UUID に基づく参照も提供されるようになりました。

* **コンテンツ参照（UUID）**
* **フラグメント参照（UUID）**。

これらの新しい参照タイプは、新しいコンテンツフラグメントモデルとフラグメントの両方で使用することができ、既存のインスタンスを拡張することもできます。

既存のコンテンツフラグメントとモデルをアップグレードするには、ここに記載されている手順を実行します。

>[!CAUTION]
>
>アップグレード手順を実行する前に、必ず [ ドライランを実行 ](#execute-a-dry-run) して、コンテンツに発生する可能性のある問題をハイライト表示する必要があります。

## アップグレード対象 {#what-is-upgraded}

次の更新が行われました。

* データタイプのフィールド：
   * **コンテンツ参照** が **コンテンツ参照（UUID）に変換される**
   * **フラグメント参照** は **フラグメント参照（UUID）に変換されます**
* これらのフィールドに保持されているパスベースの参照の値は、対応する UUID に置き換えられます

>[!NOTE]
>
>アップグレード後も、両方のデータタイプをコンテンツフラグメントモデルエディターで引き続き使用できます。 両方のタイプに基づいて新しいフィールドを作成し（UUID ベースのタイプを使用することが想定されています）、必要に応じてアップグレードを再実行できます。

## アップグレードされないもの {#what-is-not-upgraded}

次の参照はアップグレードされません。

* ページ参照 – UUID はまだサポートされていません
* 無効な参照。例えば、コンテンツフラグメントパスのターゲットやアセットパスが存在しない場合です

   * コンテンツフラグメントパスまたはアセットパスが無効で、対応する UUID が割り当てられていない場合と同様に、無効な参照はアップグレードされません。 元の参照は変更されません。

   * [ ドライラン ](#execute-a-dry-run) を使用して、無効な参照を取り除きます。

  >[!NOTE]
  >
  >無効なので、アップグレードに関係なく使用できません。

## アップグレードすべきでない場合 {#when-you-should-not-upgrade}

アップグレードしない：

* コンテンツフラグメントでページ参照を使用する場合。UUID はまだページ参照でサポートされていません

## UUID 参照の制限事項 {#limitations-of-uuid-references}

現在、UUID に基づく参照を使用する場合は、次の制限が適用されます。

* モデル

   * コンテンツフラグメント UUID またはコンテンツ参照 UUID フィールドのいずれかを持つ新しいコンテンツフラグメントモデルを、OpenAPI を使用して作成することはできません。
   * モデルの `id` フィールドが UUID ベースに変更されていません。 モデルの base64 デコードされたパスを使用します。 モデルは移動できないので、この値は安定しています。

* アセット

   * OpenAPI を使用してコンテンツフラグメントを作成する場合、UUID ベースの参照フィールドの値を設定する場合でも、フラグメントまたはアセットへの参照を指定するには、それぞれ `fragment-reference` または `content-reference` のフィールドタイプを使用する必要があります。

## アップグレードの計画 {#upgrade-planning}

アップグレードを実行する前に、いくつかの準備手順があります。

### ドライランを実行 {#execute-a-dry-run}

コンテンツをアップグレードする *たびに* 最初にドライランを実行することをお勧めします。 これにより、潜在的な問題をハイライト表示するエントリを含んだログファイルが作成されます。

* 参照が無効です
* ページ参照

`dryRun` モードでコンテンツのアップグレードを実行して、次の操作を行います。

* 無効な参照を特定するには、ログファイルにリストします。
その後、実際のコンテンツアップグレードを実行する前に、これらの参照を修正できます。
* ページ参照を識別します。参照をログファイルにリストします。
ページの参照が検出された場合は [ コンテンツのアップグレードを実行しないでください ](#when-you-should-not-upgrade)。


### コンテンツの凍結の適用 {#enforce-a-content-freeze}

コンテンツのアップグレードの実行は、コンテンツの凍結期間中に計画する必要があります。

コンテンツの凍結期間は、アップグレードするコンテンツフラグメントの量に応じて異なります。 したがって、アップグレードにかかる時間は数分から数時間までの幅があり、またその幅は、コンテンツのアップグレードを開始する際に使用するパラメーターによっても異なります。

## コンテンツアップグレードの実行 {#running-the-content-upgrade}

コンテンツのアップグレードは、エンドポイント `/libs/dam/cfm/maintenance.json` を使用して管理できます。

>[!NOTE]
>
>エンドポイントにアクセスするには、アカウントに `Administrator` の役割が必要です。

### コンテンツのアップグレードの開始 {#start-a-content-upgrade}

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **リクエストパラメーター** | **値** | |
| アクション | `start` | |
| serviceTypeId | `uuidUpgradeService` | サービスタイプ ID （事前定義された固定値）。 |
|  segmentSize | `1000` | 1 つのセグメント（バッチ）でアップグレードされるコンテンツフラグメントまたはモデルの数です。 |
| basePath | `/conf` | 次のいずれかを指定します。<ul><li>すべてのAEM設定をアップグレードするためのルート `/conf`</li><li>選択されたAEM設定パス。 コンテンツのアップグレードが実行される対象 <br> 例：`/conf/wknd-shared` は、シングルテナント `wknd-shared` のみをアップグレードします</li></ul> |
| 間隔 | `10` | コンテンツフラグメントまたはモデルの次のセグメントがアップグレードされるまでの間隔（秒）。 |
| mode | `replicate`、`noReplicate` | <ul><li>`replicate`：すべてのAEM Publish インスタンスに同じジョブをレプリケートする</li><li>`noReplicate`:AEM オーサーインスタンスでのみジョブを実行します</li></ul> |
| dryRun |  `true`、`false` | <ul><li>`false`：コンテンツの変更を保存せずに、コンテンツのアップグレードをシミュレートします</li><li>`true`：コンテンツのアップグレードを実行し、コンテンツの変更を保存する</li></ul> |
| **応答の詳細** | **値** | |
| jobId | `UUID` |  コンテンツのアップグレードを実行するジョブの ID。<ul><li>この ID は、この実行に関連する後続の呼び出しで必要になります。</li><li>`mode` の値が `replicate` に設定されている場合、AEM Publish インスタンスの実行も同じ `jobId` 下にする必要があります。</li></ul> |
| パラメーター | コンテンツのアップグレードパラメーター | これには、コンテンツのアップグレードを開始するために提供される初期パラメーターや、内部デフォルトが含まれます。 |


### コンテンツアップグレードリクエストの例 {#example-content-upgrade-request}

+++リクエスト

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++応答

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### コンテンツのアップグレードのステータスを取得 {#get-the-status-of-a-content-upgrade}

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **リクエストパラメーター** | **値** | |
| アクション | status | |
| jobId | `<UUID>` | コンテンツのアップグレードを開始するために呼び出しから返された `jobId`。 |
| **応答の詳細** | **値** | |
| status | JSON 値 | コンテンツアップグレードの詳細なステータスが含まれます。<ul><li>間隔（秒）ごとに更新されます。</li><li>実行 `uuidUpgradeService` は次の 2 つのフェーズがあります。<ol><li>フェーズ 0 でコンテンツフラグメントモデルをアップグレード</li><li>フェーズ 1：コンテンツフラグメントをアップグレードする</li></ol></li><li>各フェーズでは、統計は間隔ごとに更新されます。</li><li>「jobStatus」:「COMPLETED」は、アップグレードが正常に完了したことを示します。</li><li>その他のステータス値は自明です。</li></ul> |

### コンテンツアップグレードステータスリクエストの例 {#example-content-upgrade-status-request}

+++リクエスト

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++応答

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++サンプルログファイル

AEM ログには、HTTP エンドポイントから取得した実行中のコンテンツアップグレードのステータスに加えて、コンテンツレベルでの進行状況の詳細情報が記録されます。 例：

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

さらに、コンテンツフラグメントとモデルの各セグメント（バッチ）の処理が完了すると、累積ステータスがログに記録され、これまでの進行状況がまとめられます。 例：

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### コンテンツのアップグレードを中止 {#abort-a-content-upgrade}

>[!CAUTION]
>
>コンテンツのアップグレードを中止します（ドライランではありません）。
>
>* 既に行われた変更は元に戻しません
>* コンテンツが混在した状態になる場合があります
>
>この操作は慎重に行ってください。

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **リクエストパラメーター** | **値** | |
| アクション | 中止 | |
| jobId | `<UUID>` | コンテンツのアップグレードを開始するために呼び出しから返された `jobId`。 |
| **応答の詳細** | **値** | |
| status | JSON 値 | コンテンツアップグレードの詳細なステータスが含まれます。<ul><li>メモするステータスは「jobStatus」:「ABORTED」です。<br> 中止アクションの後は、保留中のデータセグメントは処理されません。</li><li>中止の前に jobStatus が「COMPLETED」の場合、呼び出しは無効です。</li></ul> |

### 例コンテンツのアップグレードリクエストを中止する {#example-abort-content-upgrade-request}

+++リクエスト

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++応答

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
