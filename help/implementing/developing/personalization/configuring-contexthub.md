---
title: ContextHub の設定
description: コンテキストデータを保存、操作、表示するためのフレームワークである Context Hub の設定方法について説明します。
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 87%

---

# ContextHub の設定 {#configuring-contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。ContextHub について詳しくは、[ContextHub デベロッパー向け概要](contexthub.md)を参照してください。

ContextHub ツールバーを設定して、プレビューモードで表示するかどうかを制御し、ContextHub ストアを作成したり UI モジュールを追加したりできます。

## ContextHub UI の表示と非表示 {#showing-and-hiding-the-contexthub-ui}

Adobe Granite ContextHub OSGi サービスを設定して、ページで [ContextHub UI](/help/sites-cloud/authoring/personalization/targeted-content.md) を表示または非表示にします。このサービスの PID は、`com.adobe.granite.contexthub.impl.ContextHubImpl.` です。

このサービスは、[Web コンソール](/help/implementing/deploying/configuring-osgi.md)またはリポジトリー内の JCR ノードを使用して設定できます。

* **Web コンソール：** UI を表示するには、「表示 UI」プロパティを選択します。UI を非表示にするには、「非表示 UI」プロパティをクリアします。
* **JCR ノード：** UI を表示するには、`com.adobe.granite.contexthub.show_ui` ブール値プロパティを `true` に設定します。UI を非表示にするには、プロパティを `false` に設定します。

ContextHub UI を表示する場合は、AEM オーサーインスタンスのページにのみ表示されます。この UI は、パブリッシュインスタンスのページには表示されません。

## ContextHub UI のモードとモジュールの追加 {#adding-contexthub-ui-modes-and-modules}

ContextHub ツールバーに表示される UI のモードとモジュールをプレビューモードで設定します。

* UI モード：関連モジュールのグループ
* モジュール：ストアからのコンテキストデータを公開し、オーサーがそのコンテキストを操作できるようにするウィジェット

UI モードは、ツールバーの左側に一連のアイコンとして表示されます。選択すると、UI モードのモジュールが右側に表示されます。

![ContextHub ツールバー](assets/contexthub-toolbar.png)

アイコンは、[Coral UI アイコンライブラリ](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)からの参照です。

### UI モードの追加 {#adding-a-ui-mode}

UI モードを追加すると、関連する ContextHub モジュールをグループ化できます。UI モードの作成時に、ContextHub ツールバーに表示されるタイトルとアイコンを指定します。

1. Experience Managerレールで、ツール/サイト/ContextHub を選択します。
1. デフォルトの設定コンテナを選択します。
1. 「ContextHub 設定」を選択します。
1. 「作成」ボタンを選択し、「ContextHub UI モード」を選択します。

   ![UI モードの追加](assets/contexthub-ui-mode.png)

1. 次のプロパティの値を指定します。

   * UI モードのタイトル：UI モードを識別するタイトル。
   * モードアイコン：使用する [Coral UI アイコン](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)のセレクター（例：`coral-Icon--user`）。
   * 有効：ContextHub ツールバーに UI モードを表示する場合に選択します

1. 「保存」を選択します。

### UI モジュールの追加 {#adding-a-ui-module}

ContextHub UI モジュールを UI モードに追加し、それを ContextHub ツールバーに表示して、ページコンテンツをプレビューできるようにします。UI モジュールを追加する場合は、ContextHub に登録されているモジュールタイプのインスタンスを作成します。UI モジュールを追加するには、関連するモジュールタイプの名前がわかっている必要があります。

AEM には、基本 UI モジュールタイプと、UI モジュールのベースとなる複数のサンプル UI モジュールタイプが用意されています。次の表には、各モジュールタイプについての簡単な説明が示されています。カスタム UI モジュールの開発について詳しくは、[ContextHub UI モジュールの作成](extending-contexthub.md#creating-contexthub-ui-module-types)を参照してください。

UI モジュールのプロパティには、モジュール固有のプロパティの値を指定できる詳細設定が含まれています。詳細設定は JSON 形式で指定します。表の「モジュールタイプ」列は、各 UI モジュールタイプに必要な JSON コードに関する情報へのリンクを示します。

| モジュールの種類 | 説明 | ストア |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | 汎用の UI モジュールタイプ | UI モジュールのプロパティで設定されます |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | ブラウザーに関する情報が表示されます | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | 日付と時間の情報が表示されます | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | クライアントの緯度と経度、およびマップ上の位置が表示されます。位置は変更できます。 | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | デバイスの画面の向きが表示されます（横置きまたは縦置き） | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | ページのタグに関する統計が表示されます | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | `authorizableID`、`displayName`、`familyName` など、現在のユーザーのプロファイル情報が表示されます。`displayName` と `familyName` の値は変更できます。 | `profile` |

1. Experience Managerレールで、ツール/サイト/ContextHub を選択します。
1. UI モジュールを追加する設定コンテナを選択します。
1. UI モジュールを追加する ContextHub 設定コンテナをクリックまたはタップします。
1. UI モジュールを追加する UI モードを選択します。
1. 「作成」ボタンを選択し、「 ContextHub UI モジュール（汎用） 」を選択します。

   ![ContextHub UI モジュール](assets/contexthub-ui-module.png)

1. 次のプロパティの値を指定します。

   * UI モジュールのタイトル：UI モジュールを識別するタイトル。
   * モジュールタイプ：そのモジュールのタイプ。
   * 有効：オンにすると ContextHub ツールバーに UI モジュールが表示されます。

1. （オプション）デフォルトのストアの設定をオーバーライドするには、UI モジュールを設定する JSON オブジェクトを入力します。
1. 「保存」を選択します。

## ContextHub ストアの作成 {#creating-a-contexthub-store}

ContextHub ストアを作成してユーザーデータを保持し、必要に応じてそのデータにアクセスします。ContextHub ストアは、登録済みのストア候補に基づきます。ストアを作成する際には、ストア候補が登録された storeType の値が必要です（[カスタムストア候補の作成を参照してください](extending-contexthub.md#creating-custom-store-candidates)）。

### ストアの詳細設定 {#detailed-store-configuration}

ストアを設定すると、詳細設定プロパティによりストア固有のプロパティの値を指定できます。値は、ストアの `config` 関数の `init` パラメーターに基づきます。このため、この値を指定する必要があるかどうかと、指定する値の形式はストアによって変わります。

詳細設定プロパティの値は、JSON 形式の `config` オブジェクトです。

### サンプルのストア候補 {#sample-store-candidates}

AEM には、ストアのベースにできる次のサンプルのストア候補が用意されています。

| ストアの種類 | 説明 |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | 解決済みおよび未解決の ContextHub セグメント用のストア。ContextHub SegmentManager からセグメントを自動的に取得します |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | ブラウザーの場所の緯度と経度を格納します。 |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | 複数のデバイスのプロパティと機能を定義し、現在のクライアントデバイスを検出します |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | 現在のユーザーのプロファイルデータを格納します |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | デバイス情報、ブラウザーの種類、画面の向きなど、クライアントに関する情報を格納します |

1. Experience Managerレールで、ツール/サイト/ContextHub を選択します。
1. デフォルトの設定コンテナを選択します。
1. Contexthub 設定を選択
1. ストアを追加するには、作成アイコンを選択し、「 ContextHub ストア設定」を選択します。

   ![ContextHub ストアの設定](assets/contexthub-store-configuration.png)

1. 基本的な設定プロパティの値を指定し、「次へ」を選択します。

   * **設定タイトル：**&#x200B;ストアを識別するタイトル。
   * **ストアタイプ：**&#x200B;ストアのベースとなるストア候補の storeType プロパティの値。
   * **必須：**&#x200B;オン。
   * **有効：**&#x200B;オンにするとストアが有効になります。

1. （オプション）デフォルトのストアの設定をオーバーライドするには、「詳細設定（JSON）」ボックスに JSON オブジェクトを入力します。
1. 「保存」を選択します。

## JSONP サービスの使用例  {#example-using-a-jsonp-service}

この例は、ストアを設定して UI モジュールにデータを表示する方法を示します。この例では、ストアのデータソースとして jsontest.com サイトの MD5 サービスが使用されています。サービスが指定の文字列の MD5 ハッシュコードを JSON 形式で返します。

contexthub.generic-jsonp ストアがサービスコール `https://md5.jsontest.com/?text=%22text%20to%20md5%22` のデータを格納するように設定されます。サービスが UI モジュールに表示される次のデータを返します。

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### contexthub.generic-jsonp ストアの作成 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp のサンプルのストア候補を使用すると、JSON データを返す JSONP サービスや Web サービスからデータを取得できます。このストア候補では、そのストア設定を使用して、使用する JSONP サービスに関する詳細を指定します。

`ContextHub.Store.JSONPStore` Javascript クラスの [init](contexthub-api.md#init-name-config) 関数は、このストア候補を初期化する `config` オブジェクトを定義します。`config` オブジェクトには JSONP サービスに関する情報が含まれる `service` オブジェクトが含まれています。ストアを設定するには、詳細設定プロパティの値として `service` オブジェクトを JSON 形式で指定します。

jsontest.com サイトの MD5 サービスからのデータを保存するには、次のプロパティを使用して [ContextHub ストアの作成](#creating-a-contexthub-store)の手順に従います。

* **設定のタイトル：** md5
* **ストアの種類：** contexthub.generic-jsonp
* **必須：**&#x200B;オン。
* **有効：**&#x200B;オン
* **詳細設定（JSON）：**

  ```javascript
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### md5 データの UI モジュールの追加 {#adding-a-ui-module-for-the-md-data}

ContextHub ツールバーに UI モジュールを追加して、サンプルの md5 ストアに格納されているデータを表示します。この例では、contexthub.base module が次の UI モジュールの生成に使用されています。

![ContextHub MD5 ストア](assets/contexthub-md5-store.png)

[UI モジュールの追加](#adding-a-ui-module)手順に従って、既存の UI モジュールに、サンプルのペルソナ UI モードなどの UI モジュールを追加します。UI モジュールには、次のプロパティ値を使用します。

* **UI モジュールのタイトル：** MD5
* **モジュールの種類：** contexthub.base
* **詳細設定（JSON）：**

  ```javascript
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Conversion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## ContextHub のデバッグ {#debugging-contexthub}

ContextHub のデバッグモードを有効にして、トラブルシューティングに対応できます。デバッグモードは、ContextHub 設定または CRXDE のいずれかを利用して有効にできます。

### 設定による有効化 {#via-the-configuration}

ContextHub の設定を編集し、「**デバッグ**」オプションをオンにします。

1. レールで、を選択します。 **ツール/サイト/ ContextHub**
1. デフォルトを選択 **設定コンテナ**
1. を選択します。 **ContextHub 設定** を選択し、 **選択した要素を編集**
1. 選択 **デバッグ** を選択し、 **保存**

### CRXDE による有効化 {#via-crxde}

CRXDE Lite を使用して、`debug` プロパティを **true** に設定します。

* `/conf/global/settings/cloudsettings` または
* `/conf/<site>/settings/cloudsettings`

### ContextHub のデバッグメッセージのログ {#logging-debug-messages-for-contexthub}

開発時に役立つ詳細なデバッグメッセージをログに記録するように、Adobe Granite ContextHub OSGi サービス（PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`）を設定します。

このサービスは、[Web コンソール](/help/implementing/deploying/configuring-osgi.md)またはリポジトリー内の JCR ノードを使用して設定できます。

* Web コンソール：デバッグメッセージをログに記録するには、Debug プロパティを選択します。
* JCR ノード：デバッグメッセージをログに記録するには、`com.adobe.granite.contexthub.debug` ブールプロパティを `true` に設定します。

### サイレントモード {#silent-mode}

サイレントモードでは、すべてのデバッグ情報が無効になります。各 ContextHub 設定に対して個別に設定可能な通常のデバッグオプションとは異なり、サイレントモードは、ContextHub 設定レベルのあらゆるデバッグ設定より優先されるグローバル設定です。

これは、デバッグ情報をまったく必要としないパブリッシュインスタンスに便利なモードです。これはグローバル設定なので、OSGi を介して有効にします。

1. `http://<host>:<port>/system/console/configMgr` で **Adobe Experience Manager Web コンソール設定**&#x200B;を開きます。
1. **Adobe Granite ContextHub** を検索します。
1. 設定「**Adobe Granite ContextHub**」をクリックして、そのプロパティを編集します。
1. 「**サイレントモード**」チェックボックスをオンにし、「**保存**」をクリックします。

## ContextHub の無効化 {#disabling-contexthub}

ContextHub を無効にすると、js／css の読み込みと初期化を回避できます。ContextHub を無効にする方法は 2 つあります。

* ContextHub の設定を編集し、「**ContextHub を無効にする**」チェックボックスをオンにします。

   1. レールで、を選択します。 **ツール/サイト/ ContextHub**
   1. デフォルトを選択 **設定コンテナ**
   1. を選択します。 **ContextHub 設定** を選択し、 **選択した要素を編集**
   1. 選択 **ContextHub を無効にする** を選択し、 **保存**

または

* CRXDE Lite を使用して、`/conf/global/settings/cloudsettings/<configName>/contexthub` の `disabled` プロパティを **true** に設定します。
