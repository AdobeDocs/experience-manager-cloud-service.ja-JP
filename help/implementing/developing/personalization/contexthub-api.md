---
title: ContextHub JavaScript API リファレンス
description: ContextHub コンポーネントをページに追加すると、ContextHub JavaScript API がスクリプトで使用できるようになります
translation-type: tm+mt
source-git-commit: 3277d7470c1abdcc1f759c87e2c1a7ffb3390f47
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 100%

---


# ContextHub JavaScript API リファレンス {#contexthub-javascript-api-reference}

[ContextHub コンポーネントをページに追加](adding-contexthub.md)すると、ContextHub JavaScript API がスクリプトで使用できるようになります。

## ContextHub 定数 {#contexthub-constants}

ContextHub JavaScript API によって定義される定数値です。

### イベント定数 {#event-constants}

ContextHub ストアに対して発生する名前付きイベントを次の表に示します。[ContextHub.Utils.Eventing](#contexthub-utils-eventing) も参照してください。

| 定数 | 説明 | 値 |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | ContextHub のイベント名前空間 | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | 必要なすべてのストアが登録、初期化され、使用可能な状態であることを示します | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | 指定されたタイムアウト内に一部のストアが初期化されなかったことを示します | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | ストアの登録時に実行されます | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | ストアの動作準備ができていることを示します。データが取得されると実行される JSONP ストアを除いて、登録後すぐにトリガーされます。 | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | ストアが永続性を更新した場合に実行されます | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | 永続コンテナ名 | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | 未加工の JSON 結果が格納される特定の永続キー名を格納します | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | JSON データがフェッチされた日時を示す特定のタイムスタンプを格納します | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | 前回の呼び出しで使用された JSON サービスの特定の URL を格納 | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | ContextHub の UI が展開されているかどうかを示します | `/_/container-expanded` |

### UI イベント定数 {#ui-event-constants}

次の表に、ContextHub UI に関して発生するイベントの名前を示します。

| **定数** | **説明** | **値** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | モードが登録されると実行されます | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | モードが未登録の場合に実行されます | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | モードレンダラーが登録されると実行されます | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | モードレンダラーの登録が解除されると実行されます | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | 新しいモードが追加されると実行されます | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | モードが削除されると実行されます | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | ユーザーがモードを選択した場合に実行されます | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | 新しいモジュールが登録されると実行されます | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | モジュールの登録が解除されると実行されます | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | モジュールレンダラーが登録されると実行されます | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | モジュールレンダラーの登録が解除されると実行されます | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | 新しいモジュールが追加されると実行されます | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | モジュールが削除されると実行されます | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | UI コンテナがページに追加されると実行されます | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | ContextHub UI が開かれると実行されます | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | ContextHub UI が折りたたまれると実行されます | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | プロパティが変更されると実行されます | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | ContextHub UI がレンダリングされるたび（例：プロパティの変更後）に実行されます | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | UI コンテナが初期化されると実行されます | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | アクティブな UI モードを示します。 | `/_/active-ui-mode` |

## ContextHub JavaScript API リファレンス {#contexthub-javascript-api-reference-2}

ContextHub オブジェクトを使用して、すべてのストアにアクセスできます。

### 関数（ContextHub）  {#functions-contexthub}

#### getAllStores() {#getallstores}

登録されている ContextHub ストアをすべて返します。

この関数にパラメーターはありません。

##### 戻り値 {#returns-}

すべての ContextHub ストアを格納したオブジェクト。各ストアは、ストアと同じ名前を使用するオブジェクトです。

##### 例 {#example-}

次の例では、すべてのストアを取得してから、geolocation ストアを取得しています。

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name)  {#getstore-name}

ストアを JavaScript オブジェクトとして取得します。

##### パラメーター {#parameters-}

* **`name`：**&#x200B;ストアが登録された名前。

##### 戻り値 {#returns-getstore-name}

ストアを表すオブジェクト。

##### 例 {#example-getstore-name}

次の例では、geolocation ストアを取得します。

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment  {#contexthub-segmentengine-segment}

ContextHub セグメントを表します。`ContextHub.SegmentEngine.SegmentManager` を使用して、セグメントを取得します。

### 関数（ContextHub.ContextEngine.Segment）{#functions-contexthub-contextengine-segment}

#### getName() {#getname}

セグメント名を String 値として返します。

#### getPath()  {#getpath}

セグメント定義のリポジトリパスを String 値として返します。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

ContextHub セグメントへのアクセスを提供します。

### 関数（ContextHub.SegmentEngine.SegmentManager）  {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

現在のコンテキストで解決されたセグメントを返します。この関数にパラメーターはありません。

##### 戻り値 {#returns-getresolvedsegments}

`ContextHub.SegmentEngine.Segment` オブジェクトの配列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub ストアのベースクラス。

### プロパティ（ContextHub.Store.Core）{#properties-contexthub-store-core}

#### eventing {#eventing}

[`ContextHub.Utils.Eventing`](#contexthub-utils-eventing) オブジェクト。このオブジェクトを使用して、関数をストアイベントにバインドします。デフォルト値と初期化については、[`init(name,config)`](#init-name-config) を参照してください。

#### name {#name}

ストアの名前。

#### persistence {#persistence}

`ContextHub.Utils.Persistence` オブジェクト。デフォルト値と初期化については、[`init(name,config)`](#init-name-config) を参照してください。

### 関数（ContextHub.Store.Core）{#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

データオブジェクトまたは配列とストアデータを結合します。オブジェクトのキーと値の各ペアまたは配列が（`setItem` 関数を使用して）ストアに追加されます。

* **オブジェクト：**&#x200B;キーはプロパティ名です。
* **配列：**&#x200B;キーは配列のインデックスです。

値にオブジェクトを使用できます。

##### パラメーター {#parameters-addallitems}

* **`tree`：**（Object または Array）ストアに追加するデータ。
* **`options`：**（Object）setItem 関数に渡すオプションからなる任意のオブジェクト。詳しくは、[`setItem(key,value,options)`](#setitem-key-value-options) の `options` パラメーターを参照してください。

##### 戻り値 {#returns-addallitems}

`boolean` 値：

* 値 `true` は、データオブジェクトが保存されたことを示します。
* 値 `false` は、データストアが変更されていないことを示します。

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

1 つのキーから別のキーへの参照を作成します。キーは自分自身を参照できません。

##### パラメーター {#parameters-addreference}

* **`key`：**`anotherKey` を参照するキー。

* **`anotherkey`：**`key` に参照されるキー。

##### 戻り値 {#returns-addreference}

`boolean` 値：

* `true` 値は、参照が追加されたことを示します。
* `false` 値は、参照が追加されなかったことを示します。

#### announceReadiness() {#announcereadiness}

このストアに対する `ready` イベントを発生させます。この関数にパラメーターはなく、値を返しません。

#### clean()  {#clean}

すべてのデータをストアから削除します。この関数にパラメーターおよび戻り値はありません。

#### getItem(key) {#getitem-key}

キーに関連付けられている値を返します。

##### パラメーター {#parameters-getitem}

* **`key`：**（String）値を返すキー。

##### 戻り値 {#returns-getitem}

キーの値を表すオブジェクト。

#### getKeys(includeInternals)  {#getkeys-includeinternals}

ストアからキーを取得します。オプションで、ContextHub フレームワークが内部的に使用するキーを取得できます。

##### パラメーター {#parameters-getkeys}

* **`includeInternals`：**&#x200B;値 `true` は、内部的に使用されているキーを結果に含めます。このようなキーは、アンダースコア（`_`）文字で始まります。デフォルト値は `false` です。

##### 戻り値 {#returns-getkeys}

キー名（`string` 値）の配列。

#### getReferences() {#getreferences}

ストアから参照を取得します。

##### 戻り値 {#returns-getreferences}

参照キーを被参照キーのインデックスとして使用する配列。

* 参照キーは、`key` 関数の `addReference` パラメーターに対応しています。
* 被参照キーは、`anotherKey` 関数の `addReference` パラメーターに対応しています。

#### getTree(includeInternals) {#gettree-includeinternals}

データツリーをストアから取得します。オプションで、ContextHub フレームワークが内部的に使用しているキーと値のペアを含めることができます。

##### パラメーター {#parameters-gettree}

* `includeInternals:`：値 `true` は、内部的に使用されているキーと値のペアを結果に含めます。このデータのキーは、アンダースコア（`_`）文字で始まります。デフォルト値は `false` です。

##### 戻り値 {#returns-gettree}

データツリーを表すオブジェクト。キーは、オブジェクトのプロパティ名です。

#### init(name, config) {#init-name-config}

ストアを初期化します。

* ストアデータを空のオブジェクトに設定します。
* ストア参照を空のオブジェクトに設定します。
* `eventChannel` は `data:<name>` です。`<name>` はストア名です。
* `storeDataKey` は `/store/<name>` です。`<name>` はストア名です。

##### パラメーター {#parameters-init}

* **`name`：**&#x200B;ストアの名前。
* **`config`：**&#x200B;設定プロパティを格納したオブジェクト。
   * `eventDeferring`：デフォルト値は 32 です。
   * `eventing`：このストアの [ContextHub.Utils.Eventing](#contexthub-utils-eventing) オブジェクト。デフォルト値は `ContextHub.eventing` オブジェクトを使用します。
   * `persistence`：このストアの `ContextHub.Utils.Persistence` オブジェクト。デフォルト値は `ContextHub.persistence` オブジェクトです。

#### isEventingPaused() {#iseventingpaused}

このストアに対するイベンティングが一時停止されているかどうかを判断します。

##### 戻り値 {#returns-iseventingpaused}

次の boolean 値。

* `true`：イベンティングが一時停止されているので、このストアに対するイベントは発生しません。
* `false`：イベンティングが一時停止されていないので、このストアに対するイベントが発生します。

#### pauseEventing() {#pauseeventing}

このストアに対するイベンティングを一時停止して、イベントが発生しないようにします。この関数にパラメーターは必要なく、値を返しません。

#### removeItem(key, options) {#removeitem-key-options}

キーと値のペアをストアから削除します。

キーが削除されると、この関数が `data` イベントを発生させます。イベントデータには、ストア名、削除されたキーの名前、削除された値、キーの新しい値（null）およびアクションタイプ「remove」が含まれます。

オプションで、`data` イベントを発生させないようにすることができます。

##### パラメーター {#parameters-removeitem}

* **`key`：**（String）削除するキーの名前。
* **`options`：**（Object）オプションからなるオブジェクト。次のオブジェクトプロパティが有効です。
   * silent：値 `true` は、`data` イベントが発生しないようにします。デフォルト値は `false` です。

##### 戻り値 {#returns-removeitem}

`boolean` 値：

* `true` 値は、キーと値のペアが削除されたことを示します。
* `false` 値は、キーがストアに見つからなかったのでデータストアが変更されていないことを示します。

#### removeReference(key) {#removereference-key}

参照をストアから削除します。

##### パラメーター {#parameters-removereference}

* **`key`：**&#x200B;削除するキー参照。このパラメーターは、`key` 関数の `addReference` パラメーターに対応しています。

##### 戻り値 {#returns-removereference}

`boolean` 値：

* `true` 値は、参照が削除されたことを示します。
* `false` 値は、キーが有効ではなかったのでストアが変更されていないことを示します。

#### reset(keepRemainingData) {#reset-keepremainingdata}

ストアの永続データの初期値を再設定します。オプションで、その他すべてのデータをストアから削除できます。ストアが再設定されている間、このストアに対するイベンティングは一時停止されます。この関数は値を返しません。

初期値は、ストアオブジェクトのインスタンス化に使用される config オブジェクトの `initialValues` プロパティで提供されます。

##### パラメーター {#parameters-reset}

* **`keepRemainingData`**：（Boolean）値が true の場合、初期値以外のデータは保持されます。値が false の場合、初期値以外のすべてのデータが削除されます。

#### resolveReference(key, retry)  {#resolvereference-key-retry}

被参照キーを取得します。オプションで、最良一致の解決に使用する繰り返し回数を指定できます。

##### パラメーター {#parameters-resolvereference}

* **`key`：**（String）参照を解決するためのキー。この `key` パラメーターは、`key` 関数の `addReference` パラメーターに対応しています。
* **`retry`：**（Number）使用する繰り返し回数。

##### 戻り値 {#returns-resolvereference}

被参照キーを表す `string` 値。参照が解決されない場合は、`key` パラメーターの値が返されます。

#### resumeEventing() {#resumeeventing}

このストアに対するイベンティングを再開し、イベントが発生するようにします。この関数はパラメーターを定義せず、値を返しません。

#### setItem(key, value, options) {#setitem-key-value-options}

キーと値のペアをストアに追加します。

キーの値がそのキーに対して現在保存されている値と異なる場合にのみ `data` イベントを発生させます。オプションで、`data` イベントを発生させないようにすることができます。

イベントデータには、ストア名、キー、前の値、新しい値およびアクションタイプ `set` が含まれます。

##### パラメーター {#parameters-setitem}

* **`key`：**（String）キーの名前。
* **`options`：**（Object）オプションからなるオブジェクト。次のオブジェクトプロパティが有効です。
   * `silent`：値 `true` は、`data` イベントが発生しないようにします。デフォルト値は `false` です。
* **`value`：**（Object）キーに関連付ける値。

##### 戻り値 {#returns-setitem}

`boolean` 値：

* 値 `true` は、データオブジェクトが保存されたことを示します。
* 値 `false` は、データストアが変更されていないことを示します。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

JSON データを格納するストア。データは外部の JSONP サービスから取得されるか、オプションで JSON データを返すサービスから取得されます。このクラスのインスタンスを作成する際に、[`init`](#init-name-config) 関数を使用してサービスの詳細を指定します。

ストアは、インメモリパーシスタンス（JavaScript 変数）を使用します。ストアデータは、ページが持続している間のみ使用可能です。

ContextHub.Store.JSONPStore は [ContextHub.Store.Core](#contexthub-store-core) を拡張したものなので、このクラスの関数を継承しています。

### 関数（ContextHub.Store.JSONPStore）{#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

このオブジェクトが使用する JSONP サービスへの接続の詳細を設定します。既存の設定を更新または置換できます。この関数は値を返しません。

##### パラメーター {#parameters-configureservice}

* **`serviceConfig`：**&#x200B;次のプロパティを格納したオブジェクト。
   * `host`：（String）サーバーの名前または IP アドレス。
   * `jsonp`：（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。true の場合、{callback: &quot;ContextHub.Callbacks.*Object.name*} オブジェクトが service.params オブジェクトに追加されます。
   * `params`：（Object）オブジェクトのプロパティとして表される URL パラメーター。パラメーター名はプロパティ名で、パラメーター値はプロパティ値です。
   * `path`：（String）サービスへのパス。
   * `port`：（Number）サービスのポート番号。
   * `secure`：（String または Boolean）サービス URL に使用するプロトコルを決定します。
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **override：**（Boolean）値が `true` の場合、既存のサービス設定を `serviceConfig` のプロパティで置き換えます。値が `false` の場合、既存のサービス設定プロパティを `serviceConfig` のプロパティと結合します。

#### getRawResponse() {#getrawresponse}

JSONP サービスへの最後の呼び出し以降キャッシュされている未加工の応答を返します。この関数にパラメーターは必要ありません。

##### 戻り値 {#returns-getrawresponse}

未加工の応答を表すオブジェクト。

#### getServiceDetails()  {#getservicedetails}

この ContextHub.Store.JSONPStore オブジェクトのサービスオブジェクトを取得します。サービスオブジェクトには、サービス URL を作成するのに必要なすべての情報が格納されています。

##### 戻り値 {#returns-getservicedetails}

次のプロパティを持つオブジェクト。

* **`host`：**（String）サーバーの名前または IP アドレス。
* **`jsonp`：**（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。true の場合、{callback: &quot;ContextHub.Callbacks.*Object.name*} オブジェクトが service.params オブジェクトに追加されます。
* **`params`：**（Object）オブジェクトのプロパティとして表される URL パラメーター。パラメーター名はプロパティ名で、パラメーター値はプロパティ値です。
* **`path`：**（String）サービスへのパス。
* **`port`：**（Number）サービスのポート番号。
* **`secure`：**（String または Boolean）サービス URL に使用するプロトコルを決定します。
   * `auto`://
   * `true`:https://
   * `false`:http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

JSONP サービスの URL を取得します。

##### パラメーター {#parameters-getserviceurl}

* **`resolve`：**（Boolean）解決されたパラメーターを URL に含めるかどうかを判断します。値 `true` はパラメーターを解決し、`false` は解決しません。

##### 戻り値 {#returns-getserviceurl}

サービス URL を表す `string` 値。

#### init(name, config) {#init-name-config-1}

`ContextHub.Store.JSONPStore` オブジェクトを初期化します。

##### パラメーター {#parameters-init-1}

* **`name`：**（String）ストアの名前。
* **`config`：**（Object）サービスプロパティを格納するオブジェクト。JSONPStore オブジェクトは、`service` オブジェクトのプロパティを使用して、JSONP サービスの URL を組み立てます。
   * `eventDeferring`：32。
   * `eventing`：このストアの ContextHub.Utils.Eventing オブジェクト。デフォルト値は `ContextHub.eventing` オブジェクトです。
   * `persistence`：このストアの ContextHub.Utils.Persistence オブジェクト。デフォルトでは、メモリパーシスタンスが使用されます（JavaScript オブジェクト）。
   * `service`: (Object)
      * `host`：（String）サーバーの名前または IP アドレス。
      * `jsonp`：（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。true の場合、`{callback: "ContextHub.Callbacks.*Object.name*}` オブジェクトは `service.params` に追加されます。
      * `params`：（Object）オブジェクトのプロパティとして表される URL パラメーター。パラメーターの名前と値は、それぞれオブジェクトのプロパティの名前と値です。
      * `path`：（String）サービスへのパス。
      * `port`：（Number）サービスのポート番号。
      * `secure`：（String または Boolean）サービス URL に使用するプロトコルを決定します。
         * `auto`://
         * `true`:https://
         * `false`:http://
      * `timeout`：（Number）タイムアウトまでに JSONP サービスの応答を待機する時間（ミリ秒単位）。
         * `ttl`：JSONP サービスの最小呼び出し間隔（ミリ秒単位）。（[queryService](#queryservice-reload) 関数を参照）。

#### queryService(reload)  {#queryservice-reload}

リモート JSONP サービスをクエリーし、応答をキャッシュします。この関数の前回の呼び出しからの時間が `config.service.ttl` の値より小さい場合、サービスは呼び出されず、キャッシュされた応答は変更されません。オプションで、サービスを強制的に呼び出すことができます。`config.service.ttl` プロパティは、ストアを初期化するために [init](#init-name-config) 関数を呼び出すと設定されます。

クエリーが完了すると、ready イベントが発生します。JSONP サービス URL が設定されていない場合、この関数は何もしません。

##### パラメーター {#parameters-queryservice}

* **`reload`：**（Boolean）値が true の場合、キャッシュされた応答を削除し、JSONP サービスを強制的に呼び出します。

#### reset {#reset}

ストアの永続データを初期値にリセットしてから、JSONP サービスを呼び出します。オプションで、その他すべてのデータをストアから削除できます。初期値が再設定されている間、このストアに対するイベンティングは一時停止されます。この関数は値を返しません。

初期値は、ストアオブジェクトのインスタンス化に使用される config オブジェクトの initialValues プロパティで提供されます。

##### パラメーター {#parameters-reset-1}

* **`keepRemainingData`：**（Boolean）値が true の場合、初期値以外のデータは保持されます。値が false の場合、初期値以外のすべてのデータが削除されます。

#### resolveParameter(f)  {#resolveparameter-f}

指定されたパラメーターを解決します。

## ContextHub.Store.PersistedJSONPStore  {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` は [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore) を拡張したものなので、このクラスのすべての関数を継承しています。ただし、JSONP サービスから取得されるデータは、ContextHub の永続性に応じて保持されます（[永続モード](adding-contexthub.md#persistence-modes)：を参照）

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` は [ContextHub.Store.Core](#contexthub-store-core) を拡張したものなので、このクラスのすべての関数を継承しています。このストアのデータは、ContextHub の永続性の設定に応じて保持されます。

## ContextHub.Store.SessionStore  {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` は [ContextHub.Store.Core](#contexthub-store-core) を拡張したものなので、このクラスのすべての関数を継承しています。このストアのデータは、インメモリパーシスタンス（JavaScript オブジェクト）を使用して保持されます。

## ContextHub.UI  {#contexthub-ui}

UI モジュールおよび UI モジュールレンダラーを管理します。

### 関数（ContextHub.UI）  {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

UI モジュールレンダラーを ContextHub に登録します。登録後、レンダラーを使用して [UI モジュールを作成](configuring-contexthub.md#adding-a-ui-module)できます。`ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) を拡張[してカスタム UI モジュールレンダラーを作成する場合は、この関数を使用します。

##### パラメーター {#parameters-registerrenderer}

* **`moduleType`：**（String）UI モジュールレンダラーの識別子。指定された値でレンダラーが既に登録されている場合、既存のレンダラーが登録解除されてから、このレンダラーが登録されます。
* **`renderer`：**（String）UI モジュールをレンダリングするクラスの名前。
* **`dontRender`：**（Boolean）レンダラーの登録後に ContextHub UI がレンダリングされないようにするには、`true` に設定します。デフォルト値は `false` です。

##### 例 {#example-registerrenderer}

次の例では、レンダラーを `contexthub.browserinfo` モジュールタイプとして登録します。

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

cookie とやり取りするユーティリティクラス。

### 関数（ContextHub.Utils.Cookie）  {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

cookie が存在するかどうかを判断します。

##### パラメーター {#parameters-exists}

* **`key`：**&#x200B;テストする cookie のキーを格納した `String`。

##### 戻り値 {#returns-exists}

`boolean` 値 true は、cookie が存在することを示します。

##### 例 {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

フィルターに一致するキーを持つすべての cookie を返します。

##### パラメーター {#parameters-getallitems}

* **`filter`：**（オプション）cookie のキーを照合する条件。すべての cookie を返すには、値を指定しないでください。次のタイプがサポートされています。
   * String：文字列を cookie のキーと比較します。
   * Array：配列内の各項目はフィルターです。
   * 正規表現オブジェクト：オブジェクトのテスト関数を使用して cookie のキーを照合します。
   * 関数：cookie のキーが一致するかどうかをテストする関数。関数は、cookie のキーをパラメーターとして取り、テストで一致するｋとが確認された場合は true を返す必要があります。

##### 戻り値 {#returns-getallitems}

cookie からなるオブジェクト。オブジェクトのプロパティは cookie のキーで、キー値は cookie の値です。

##### 例 {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

cookie の値を返します。

##### パラメーター {#parameters-getitem-1}

* **`key`：**&#x200B;値を取得する cookie のキー。

##### 戻り値 {#returns-getitem-1}

cookie の値、またはそのキーの cookie が見つからなかった場合は `null`。

##### 例 {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

フィルターに一致する既存の cookie のキーからなる配列を返します。

##### パラメーター {#parameters-getkeys-1}

* **`filter`：** cookie のキーを照合する条件。次のタイプがサポートされています。
   * String：文字列を cookie のキーと比較します。
   * Array：配列内の各項目はフィルターです。
   * 正規表現オブジェクト：オブジェクトのテスト関数を使用して cookie のキーを照合します。
   * 関数：cookie のキーが一致するかどうかをテストする関数。関数は、cookie のキーをパラメーターとして取り、テストによって一致が確認された場合は `true` を返す必要があります。

##### 戻り値 {#returns-getkeys-1}

それぞれがフィルターに一致する cookie のキーである文字列からなる配列。

##### 例 {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

cookie を削除します。cookie を削除するには、値を空の文字列に設定し、有効期限を現在の日付より前の日に設定します。

##### パラメーター {#parameters-removeitem-1}

* **`key`：**&#x200B;削除する cookie のキーを表す `String` 値。
* **`options`：** cookie の属性を設定するプロパティ値を格納したオブジェクト。詳しくは、[`setItem`](#setitem-key-value-options) 関数を参照してください。`expires` プロパティは無効です。

##### 戻り値 {#returns-removeitem-1}

この関数は値を返しません。

##### 例 {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

指定されたキーと値の cookie を作成し、その cookie を現在のドキュメントに追加します。オプションで、cookie の属性を設定するオプションを指定できます。

##### パラメーター {#parameters-setitem-1}

* **`key`：** cookie のキーを格納した String。
* **`value`：** cookie の値を格納した String。
* **`options`：**（オプション）cookie の属性を設定する、次のいずれかのプロパティを格納したオブジェクト。
   * `expires`：cookie の有効期限を指定する `date` 値または `number` 値。date 値は、有効期限の絶対時間を指定します。number（日数）は、有効期限を現在時刻 + その日数に設定します。デフォルト値は `undefined` です。
   * `secure`：cookie の `boolean` 属性を指定する `Secure` 値。デフォルト値は `false` です。
   * `path`：cookie の `String` 属性として使用する `Path` 値。デフォルト値は `undefined` です。

##### 戻り値 {#returns-setitem-1}

値が設定された cookie。

##### 例 {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

指定されたフィルターに一致するすべての cookie を削除します。cookie は、`getKeys` 関数を使用して照合され、`removeItem` 関数を使用して削除されます。

##### パラメーター {#parameters-vanish}

* **`filter`：**`filter` 関数への呼び出しに使用する [`getKeys`](#getkeys-filter) 引数。
* **`options`：**`options` 関数への呼び出しに使用する [`removeItem`](#removeitem-key-options) 引数。

##### 戻り値 {#returns-vanish}

この関数は値を返しません。

## ContextHub.Utils.Eventing  {#contexthub-utils-eventing}

関数を ContextHub ストアイベントにバインドおよびバインド解除できます。ストアの [eventing](#eventing) プロパティを使用して、ストアの `ContextHub.Utils.Eventing` オブジェクトにアクセスします。

### 関数（ContextHub.Utils.Eventing）{#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

イベントから関数をバインド解除します。

##### パラメーター {#parameters-off}

* **`name`：**&#x200B;関数をバインド解除する[イベントの名前](#contexthub-utils-eventing)。
* **`selector`：**&#x200B;バインドを識別するセレクター（`selector` 関数と [`on`](#on-name-handler-selector-triggerforpastevents) 関数の [`once`](#once-name-handler-selector-triggerforpastevents) パラメーターを参照）。

##### 戻り値 {#returns-off}

この関数は値を返しません。

#### on(name, handler, selector, triggerForPastEvents)  {#on-name-handler-selector-triggerforpastevents}

関数をイベントにバインドします。この関数は、イベントが発生するたびに呼び出されます。オプションで、過去にバインドが確立される前に発生したイベントに対して関数を呼び出すことができます。

##### パラメーター {#parameters-on}

* **`name`：**（String）関数をバインドする[イベントの名前](#contexthub-utils-eventing)。
* **`handler`：**（Function）イベントにバインドする関数。
* **`selector`：**（String）バインドの一意の識別子。`off` 関数を使用してバインドを削除する場合は、セレクターでバインドを識別する必要があります。
* **`triggerForPastEvents`：**（Boolean）過去に発生したイベントに対してハンドラーを実行するかどうかを示します。`true` 値は、過去のイベントに対してハンドラーを呼び出します。`false` 値は、未来のイベントに対してハンドラーを呼び出します。デフォルト値は `true` です。

##### 戻り値 {#returns-on}

`triggerForPastEvents` 引数が `true` の場合、この関数はイベントが過去に発生したかどうかを示す `boolean` 値を返します。

* `true`：イベントが過去に発生しており、ハンドラーが呼び出されます。
* `false`：イベントが過去に発生していません。

`triggerForPastEvents` が `false` の場合、この関数は値を返しません。

##### 例 {#example-on}

次の例では、関数を geolocation ストアの data イベントにバインドします。この関数は、ページ上の要素にストアの緯度データ項目の値を設定しています。

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

関数をイベントにバインドします。関数は、最初に発生したイベントに対して一度だけ呼び出されます。オプションで、過去にバインドが確立される前に発生したイベントに対して関数を呼び出すことができます。

##### パラメーター {#parameters-once}

* **`name`：**（String）関数をバインドする[イベントの名前](#contexthub-utils-eventing)。
* **`handler`：**（Function）イベントにバインドする関数。
* **`selector`：**（String）バインドの一意の識別子。`off` 関数を使用してバインドを削除する場合は、セレクターでバインドを識別する必要があります。
* **`triggerForPastEvents`：**（Boolean）過去に発生したイベントに対してハンドラーを実行するかどうかを示します。`true` 値は、過去のイベントに対してハンドラーを呼び出します。`false` 値は、未来のイベントに対してハンドラーを呼び出します。デフォルト値は `true` です。

##### 戻り値 {#returns-once}

`triggerForPastEvents` 引数が `true` の場合、この関数はイベントが過去に発生したかどうかを示す `boolean` 値を返します。

* `true`：イベントが過去に発生しており、ハンドラーが呼び出されます。
* `false`：イベントが過去に発生していません。

`triggerForPastEvents` が `false` の場合、この関数は値を返しません。

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

オブジェクトが別のオブジェクトのプロパティとメソッドを継承できるようにするユーティリティクラス。

### 関数（ContextHub.Utils.inheritance）  {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

オブジェクトに別のオブジェクトのプロパティとメソッドを継承させます。

##### パラメーター {#parameters-inherit}

* **`child`：**（Object）継承するオブジェクト。
* **`parent`：**（Object）継承するプロパティとメソッドを定義するオブジェクト。

## ContextHub.Utils.JSON {#contexthub-utils-json}

オブジェクトを JSON 形式にシリアライズし、JSON 文字列をオブジェクトにデシリアライズするための関数を提供します。

### 関数（ContextHub.Utils.JSON）  {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

文字列値を JSON として解析し、JavaScript オブジェクトに変換します。

##### パラメーター {#parameters-parse}

* **`data`：** JSON 形式の文字列値。

##### 戻り値 {#returns-parse}

JavaScript オブジェクト。

##### 例 {#example-parse}

コード：

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

次のオブジェクトを返します。

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

JavaScript の値およびオブジェクトを JSON 形式の文字列値にシリアライズします。

##### パラメーター {#parameters-stringify}

* **`data`：**&#x200B;シリアライズする値またはオブジェクト。この関数は、boolean、array、number、string および date 値をサポートします。

##### 戻り値 {#returns-stringify}

シリアライズされた文字列値。`data` が `egExp` 値の場合、この関数は空のオブジェクトを返します。`data` が関数の場合は、`undefined` を返します。

##### 例 {#example-stringify}

次のコード：

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

戻り値:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

このクラスは、ContextHub ストアに保存または ContextHub ストアから取得するデータオブジェクトの操作を容易にします。

### 関数（ContextHub.Utils.JSON.tree）  {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

データオブジェクトのコピーを作成し、2 つ目のオブジェクトのデータツリーに追加します。この関数はコピーを返し、元のオブジェクトはどちらも変更されません。2 つのオブジェクトのデータツリーに同一のキーが含まれる場合、2 つ目のオブジェクトの値によって最初のオブジェクトの値が上書きされます。

##### パラメーター {#parameters-addallitems-1}

* **`tree`：**&#x200B;コピーするオブジェクト。
* **`secondTree`：**`tree` オブジェクトのコピーと結合されるオブジェクト。

##### 戻り値 {#returns-addallitems-1}

結合されたデータを格納したオブジェクト。

#### cleanup()  {#cleanup}

オブジェクトのコピーを作成し、値を含まないか、null 値または undefined 値を含むデータツリーの項目を探して削除し、コピーを返します。

##### パラメーター {#parameters-cleanup}

* **`tree`：**&#x200B;クリーンアップするオブジェクト。

##### 戻り値 {#returns-cleanup}

クリーンアップされたツリーのコピー。

#### getItem()  {#getitem}

キーに対する値をオブジェクトから取得します。

##### パラメーター {#parameters-getitem-2}

* **`tree`：**&#x200B;データオブジェクト。
* **`key`：**&#x200B;取得する値のキー。

##### 戻り値 {#returns-getitem-2}

キーに対応する値。キーに子キーがある場合、この関数は複合オブジェクトを返します。キーの値のタイプが `undefined` の場合、`null` が返されます。

##### 例 {#example-getitem-2}

次の JavaScript オブジェクトについて考えてみます。

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

次のサンプルコードは、値 `260` を返します。

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

次のサンプルコードは、子キーを持つキーの値を取得します。

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

この関数は次のオブジェクトを返します。

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys()  {#getkeys}

オブジェクトのデータツリーからすべてのキーを取得します。オプションで、特定のキーの子のキーのみを取得できます。オプションで、取得したキーのソート順を指定することもできます。

##### パラメーター {#parameters-getkeys-2}

* **`tree`：**&#x200B;データツリーのキーの取得元となるオブジェクト。
* **`parent`：**（オプション）子項目のキーを取得するデータツリー内の項目のキー。
* **`order`：**（オプション）返されたキーのソート順を判断する関数（Mozilla Developer Network の [`Array.prototype.sort`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) を参照）。

##### 戻り値 {#returns-getkeys-2}

キーからなる配列。

##### 例 {#example-getkeys-2}

次のオブジェクトについて考えてみます。

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

`ContextHub.Utils.JSON.tree.getKeys(myObject);` スクリプトは、次の配列を返します。

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

指定されたオブジェクトのコピーを作成し、指定されたブランチをデータツリーから削除し、変更されたコピーを返します。

##### パラメーター {#parameters-removeitem-2}

* **`tree`：**&#x200B;データオブジェクト。
* **`key`：**&#x200B;削除するキー。

##### 戻り値 {#returns-removeitem-2}

キーが削除された元のデータオブジェクトのコピー。

##### 例 {#example-removeitem-2}

次のオブジェクトについて考えてみます。

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

次のサンプルスクリプトでは、データツリーから /one/two/three/four ブランチを削除しています。

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

この関数は次のオブジェクトを返します。

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key)  {#sanitizekey-key}

文字列値の不要部分を削除して、キーとして使用できるようにします。文字列の不要部分を削除するために、この関数は次のアクションを実行します。

* 複数の連続するフォワードスラッシュを 1 つのスラッシュにまとめます。
* 文字列の先頭および末尾から空白を削除します。
* 結果をスラッシュで区切られた文字列の配列に分割します。

作成された配列を使用して、使用可能なキーを作成します。

##### パラメーター {#parameters-sanitizekey}

* **`key`：**&#x200B;不要部分を削除する `string`。

##### 戻り値 {#returns-sanitizekey}

`string` 値からなる配列で、各文字列はスラッシュで区切られた `key` の一部です。不要部分が削除されたキーを表します。不要部分が削除された配列の長さがゼロの場合、この関数は `null` を返します。

##### 例 {#example-sanitizekey}

次のコードは、文字列の不要部分を削除して `["this", "is", "a", "path"]` という配列を作成し、その配列からキー `"/this/is/a/path"` を生成します。

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

オブジェクトのコピーのデータツリーにキーと値のペアを追加します。データツリーについて詳しくは、[永続性](contexthub.md#persistence)を参照してください。

##### パラメーター {#parameters-setitem-2}

* **`tree`：**&#x200B;データオブジェクト。
* **`key`：**&#x200B;追加する値に関連付けるキー。キーは、データツリー内の項目へのパスです。この関数は、`ContextHub.Utils.JSON.tree.sanitize` を呼び出して、キーを追加する前に不要部分を削除します。
* **`value`：**&#x200B;データツリーに追加する値。

##### 戻り値 {#returns-setitem-2}

`key` と `value` のペアを含む `tree` オブジェクトのコピー。

##### 例 {#example-setitem-2}

次の JavaScript コードについて考えてみます。

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

ストア候補を登録したり、登録されたストア候補を取得したりできるようにします。

### 関数（ContextHub.Utils.storeCandidates）  {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

ストア候補として登録されているストアタイプを返します。特定のストアタイプまたはすべてのストアタイプの登録されている候補を取得します。

##### パラメーター {#parameters-getregisteredcandidates}

* **`storeType`：**（String）ストアタイプの名前。`storeType` 関数の [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) パラメーターを参照してください。

##### 戻り値 {#returns-getregisteredcandidates}

ストアタイプのオブジェクト。オブジェクトのプロパティはストアタイプ名で、プロパティ値は登録されているストア候補からなる配列です。

#### getStoreFromCandidates(storeType)  {#getstorefromcandidates-storetype}

登録されている候補からストアタイプを返します。複数のストアタイプが同じ名前で登録されている場合、この関数は最も優先度が高いストアタイプを返します。

##### パラメーター {#parameters-getstorefromcandidates}

* `storeType`：（String）ストア候補の名前。`storeType` 関数の [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies) パラメーターを参照してください。

##### 戻り値 {#returns-getstorefromcandidates}

登録されているストア候補を表すオブジェクト。要求されたストアタイプが登録されていない場合は、エラーがスローされます。

#### getSupportedStoreTypes()  {#getsupportedstoretypes}

ストア候補として登録されているストアタイプの名前を返します。この関数にパラメーターは必要ありません。

##### 戻り値 {#returns-getsupportedstoretypes}

文字列値からなる配列で、各文字列はストア候補と一緒に登録されたストアタイプです。`storeType` 関数の [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates) パラメーターを参照してください。

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

名前と優先度を使用して、ストアオブジェクトをストア候補として登録します。

優先度は、同じ名前のストアの重要度を示す数字です。既に登録されているストア候補と同じ名前を使用してストア候補を登録した場合、優先度の高い候補が使用されます。ストア候補を登録する場合、同じ名前の登録済みストア候補より優先度が高い場合にのみストアが登録されます。

##### パラメーター {#parameters-registerstorecandidate}

* **`store`：**（Object）ストア候補として登録するストアオブジェクト。
* **`storeType`：**（String）ストア候補の名前。この値は、ストア候補のインスタンスを作成する際に必要です。
* **`priority`：**（Number）ストア候補の優先度。
* **`applies`：**（Function）現在の環境内でのストアの適用可能性を評価するために呼び出す関数。この関数は、ストアを適用できる場合は `true`、それ以外の場合は `false` を返す必要があります。デフォルト値は、true を返す関数 `function() {return true;}` です。

##### 例 {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
