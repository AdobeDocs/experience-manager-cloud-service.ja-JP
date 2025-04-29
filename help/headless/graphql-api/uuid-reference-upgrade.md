---
title: UUID 参照用のコンテンツフラグメントのアップグレード
description: ヘッドレスコンテンツ配信の Adobe Experience Manager as a Cloud Service で最適化された UUID 参照用にコンテンツフラグメントをアップグレードする方法について説明します。
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: fdfe0291ca190cfddf3bed363a8c2271a65593a1
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 100%

---

# UUID 参照用のコンテンツフラグメントのアップグレード {#upgrade-content-fragments-for-UUID-references}

GraphQL フィルターの安定性を最適化するには、コンテンツフラグメント内のコンテンツとフラグメント参照をアップグレードして、Universally Unique Identifier（UUID）を使用するようにします。

コンテンツフラグメントモデルは元々、**コンテンツ参照**&#x200B;と&#x200B;**フラグメント参照**&#x200B;のデータタイプを提供していました。これらの参照はどちらも、参照先のリソースを指すのにパスを使用し、リソースを移動すると、このパスは古くなる可能性があります。このような参照は、ほとんどのシナリオでは十分すぎるほどですが、コンテンツフラグメントモデルは、次の UUID に基づく参照も提供するように拡張されています。

* **コンテンツ参照（UUID）**
* **フラグメント参照（UUID）**

これらの新しい参照タイプは、新しいコンテンツフラグメントモデルとフラグメントの両方で使用でき、既存のインスタンスの拡張にも使用できます。

既存のコンテンツフラグメントとモデルをアップグレードするには、こちらに記載されている手順を実行できます。

>[!CAUTION]
>
>アップグレード手順を実行する前に、常に[ドライランを実行](#execute-a-dry-run)して、コンテンツの潜在的な問題をハイライト表示する必要があります。

## アップグレードされる内容 {#what-is-upgraded}

次の更新が行われます。

* データタイプのフィールド：
   * **コンテンツ参照**&#x200B;を&#x200B;**コンテンツ参照（UUID）**&#x200B;に変換されます。
   * **フラグメント参照**&#x200B;を&#x200B;**フラグメント参照（UUID）**&#x200B;に変換されます。
* これらのフィールドに保持されているパスベースの参照の値は、対応する UUID に置き換えられます。

>[!NOTE]
>
>アップグレード後も、コンテンツフラグメントモデルエディターでは両方のデータタイプが引き続き使用できます。両方のタイプに基づいて新しいフィールドを作成し（ただし、UUID ベースのタイプを使用することを想定）、必要に応じてアップグレードを再実行できます。

## アップグレードされない内容 {#what-is-not-upgraded}

次の参照はアップグレードされません。

* ページ参照 - UUID はまだサポートされていません。
* 無効な参照。例えば、コンテンツフラグメントパスのターゲットやアセットパスが存在しない場合です。

   * コンテンツフラグメントパスまたはアセットパスが無効である場合、割り当てる対応する UUID がないので、無効な参照はアップグレードされません。元の参照はそのまま残ります。

   * 無効な参照を検出するには、[ドライラン](#execute-a-dry-run)を使用します。

  >[!NOTE]
  >
  >無効なので、アップグレードに関係なく使用できません。

## アップグレードする必要がない場合 {#when-you-should-not-upgrade}

次の場合はアップグレードしないでください。

* コンテンツフラグメントのいずれかでページ参照が使用されている場合、UUID はまだページ参照でサポートされていません。

## UUID 参照の制限事項 {#limitations-of-uuid-references}

現在、UUID に基づく参照を使用する場合、次の制限が適用されます。

* モデル

   * コンテンツフラグメント UUID またはコンテンツ参照 UUID フィールドを持つ新しいコンテンツフラグメントモデルは、OpenAPI 経由では作成できません。
   * モデルの `id` フィールドは UUID ベースに変更されていません。これは、モデルの base64 デコードされたパスを使用します。モデルは移動できないので、この値は引き続き安定します。

* アセット

   * OpenAPI 経由でコンテンツフラグメントを作成する際、UUID ベースの参照フィールドの値を設定する場合でも、フラグメントまたはアセットへの参照を指定するには、それぞれ `fragment-reference` または `content-reference` フィールドタイプを使用する必要があります。

## アップグレードの計画 {#upgrade-planning}

アップグレードを実行する前に、いくつかの準備手順があります。

### ドライランの実行 {#execute-a-dry-run}

コンテンツをアップグレードする&#x200B;*たび*&#x200B;に、最初にドライランを実行することをお勧めします。これにより、潜在的な問題をハイライト表示するエントリを含むログファイルが作成されます。

* 参照が無効です
* ページ参照

コンテンツのアップグレードを `dryRun` モードで実行して、次の操作を行います。

* 無効な参照をログファイルにリストして特定
その後、実際のコンテンツアップグレードを実行する前に、これらの参照を修正できます。
* ページ参照をログファイルにリストして特定
ページ参照が検出された場合、[コンテンツアップグレードを実行する必要はありません](#when-you-should-not-upgrade)。


### コンテンツの凍結を適用 {#enforce-a-content-freeze}

コンテンツのアップグレードの実行は、コンテンツの凍結期間中に計画する必要があります。

コンテンツの凍結期間は、アップグレードするコンテンツフラグメントの量に応じて異なります。したがって、アップグレードには数分から数時間かかる場合があり、コンテンツのアップグレードの開始時に使用するパラメーターによっても異なります。

## コンテンツのアップグレードの実行 {#running-the-content-upgrade}

コンテンツのアップグレードは、エンドポイント `/libs/dam/cfm/maintenance.json` を使用して管理できます。

>[!NOTE]
>
>エンドポイントにアクセスするには、アカウントに `Administrator` の役割が必要です。

### コンテンツのアップグレードの開始 {#start-a-content-upgrade}

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **リクエストパラメーター** | **値** | |
| action | `start` | |
| serviceTypeId | `uuidUpgradeService` | サービスタイプ ID（定義済みの固定値）。 |
| segmentSize | `1000` | 1 つのセグメント（バッチ）でアップグレードされるコンテンツフラグメントまたはモデルの数。 |
| basePath | `/conf` | 次のいずれかを指定します。<ul><li>すべての AEM 設定をアップグレードするルート `/conf`。</li><li>選択された AEM 設定パス。コンテンツのアップグレードが実行される対象<br>例：`/conf/wknd-shared` は、シングルテナント `wknd-shared` のみをアップグレードします。</li></ul> |
| interval | `10` | コンテンツフラグメントまたはモデルの次のセグメントがアップグレードされるまでの間隔（秒）。 |
| mode | `replicate`、`noReplicate` | <ul><li>`replicate`：すべての AEM パブリッシュインスタンスで同じジョブをレプリケートします。</li><li>`noReplicate`：AEM オーサーインスタンスでのみジョブを実行します。</li></ul> |
| dryRun |  `true`、`false` | <ul><li>`false`：コンテンツの変更を保存せずに、コンテンツのアップグレードをシミュレートします。</li><li>`true`：コンテンツのアップグレードを実行し、コンテンツの変更を保存します。</li></ul> |
| **応答の詳細** | **値** | |
| jobId | `UUID` | コンテンツのアップグレードを実行するジョブの ID。<ul><li>この ID は、この実行に関連する後続のすべての呼び出しで必要になります。</li><li>`mode` 値が `replicate` に設定されている場合、AEM パブリッシュインスタンスでの実行も同じ `jobId` で行う必要があります。</li></ul> |
| パラメーター | コンテンツのアップグレードのパラメーター | これらには、コンテンツのアップグレードを開始するのに提供される初期パラメーターと、いくつかの内部デフォルトが含まれます。 |


### コンテンツのアップグレードのリクエストの例 {#example-content-upgrade-request}

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

### コンテンツのアップグレードのステータスの取得 {#get-the-status-of-a-content-upgrade}

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **リクエストパラメーター** | **値** | |
| action | status | |
| jobId | `<UUID>` | コンテンツのアップグレードを開始する呼び出しから返された `jobId`。 |
| **応答の詳細** | **値** | |
| status | JSON 値 | コンテンツのアップグレードの詳細なステータスが含まれます。<ul><li>間隔（秒）ごとに更新されます。</li><li>`uuidUpgradeService` の実行には次の 2 つのフェーズがあります。<ol><li>フェーズ 0：コンテンツフラグメントモデルをアップグレード</li><li>フェーズ 1：コンテンツフラグメントをアップグレード</li></ol></li><li>各フェーズでは、間隔ごとに統計が更新されます。</li><li>「jobStatus」:「COMPLETED」は、アップグレードが正常に完了したことを示します。</li><li>その他のステータス値は説明不要です。</li></ul> |

### コンテンツのアップグレードのステータスリクエストの例 {#example-content-upgrade-status-request}

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

HTTP エンドポイントから取得された実行中のコンテンツのアップグレードのステータスに加えて、AEM ログではコンテンツレベルでの進行状況の詳細情報を提供します。例：

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

また、コンテンツフラグメントとモデルの各セグメント（バッチ）の処理後に、これまでの進行状況をまとめた累積ステータスがログに記録されます。例：

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### コンテンツのアップグレードの中止 {#abort-a-content-upgrade}

>[!CAUTION]
>
>次の場合、コンテンツのアップグレードを中止します（ドライランではありません）。
>
>* 既に行われた変更が元に戻らない。
>* コンテンツが混在した状態になる可能性がある。
>
>このアクションは慎重に行ってください。

| エンドポイント | HTTP リクエストタイプ | コメント |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **リクエストパラメーター** | **値** | |
| action | abort | |
| jobId | `<UUID>` | コンテンツのアップグレードを開始する呼び出しから返された `jobId`。 |
| **応答の詳細** | **値** | |
| status | JSON 値 | コンテンツのアップグレードの詳細なステータスが含まれます。<ul><li>注意するステータスは「jobStatus」:「ABORTED」です。<br>中止アクションの後、保留中のデータセグメントは処理されません。</li><li>中止前に jobStatus が「COMPLETED」の場合、呼び出しは効果がありません。</li></ul> |

### コンテンツのアップグレードのリクエストの中止の例 {#example-abort-content-upgrade-request}

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
