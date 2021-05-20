---
title: Adobe Experience Manager用のOSGiのCloud Service
description: 'シークレット値と環境固有の値を使用する OSGi 設定 '
feature: デプロイ
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: 7baacc953c88e1beb13be9878b635b6e5273dea2
workflow-type: tm+mt
source-wordcount: '2850'
ht-degree: 56%

---

# Adobe Experience Manager用のOSGiをCloud Serviceとして設定{#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) は Adobe Experience Manager（AEM）のテクノロジースタックの基本要素です。AEM とその設定の複合バンドルを制御するために使用されます。

OSGiは、小規模で再利用可能な協調コンポーネントからアプリケーションを構築できる、標準化されたプリミティブを提供します。これらのコンポーネントは、アプリケーションに構成し、デプロイできます。 これにより、OSGi バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネントは、様々なバンドルの 1 つに含まれています。詳しくは、[OSGi の仕様](https://www.osgi.org/Specifications/HomePage)を参照してください。

AEM コードプロジェクトに含まれる設定ファイルを使用して、OSGi コンポーネントの設定を管理できます。

## OSGi の設定ファイル {#osgi-configuration-files}

設定の変更は、 AEM プロジェクトのコードパッケージ（`ui.apps`）で、実行モード固有の config フォルダーの下に設定ファイル（`.cfg.json`）として定義されます。

`/apps/example/config.<runmode>`

OSGi設定ファイルの形式は、Apache Slingプロジェクトで定義されている`.cfg.json`形式を使用したJSONベースです。

OSGi設定は、永続ID(PID)を介してOSGiコンポーネントをターゲットに設定します。デフォルトは、OSGiコンポーネントのJava™クラス名です。 例えば、OSGi サービス用の OSGi 設定を提供するには、次のように実装します。

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi 設定ファイルは次の場所で定義されます。

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

cfg.json OSGi 設定形式に従います。

>[!NOTE]
>
>以前のバージョンの AEM は、.cfg、.config、XML sling:OsgiConfig リソース定義など、様々なファイル形式の OSGi 設定ファイルをサポートしていました。これらの形式は、cfg.json OSGi 設定形式に置き換えられます。

## 実行モードの解決 {#runmode-resolution}

実行モードを使用すると、特定の OSGi 設定を特定の AEM インスタンスにターゲット設定できます。実行モードを使用するには、次の形式で、`/apps/example`（「example」はプロジェクト名）の下に config フォルダーを作成します。

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

configフォルダー名で定義された実行モードがAEMで使用される実行モードと一致する場合は、このようなフォルダー内のOSGi設定が使用されます。

例えば、AEMがオーサーと開発の実行モードを使用している場合、`/apps/example/config.author/`と`/apps/example/config.author.dev/`の設定ノードが適用され、`/apps/example/config.publish/`と`/apps/example/config.author.stage/`の設定ノードは適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

このルールの精度は PID レベルです。つまり、`/apps/example/config.author/` で同じ PID の一部のプロパティと、`/apps/example/config.author.dev/` で同じ PID のより具体的なプロパティを定義することはできません。一致する実行モードの数が最も多い設定は、PID全体に対して有効です。

ローカルで開発する場合は、実行モード起動パラメーターを渡して、使用する実行モードOSGI設定を指定できます。

## OSGi 設定値のタイプ {#types-of-osgi-configuration-values}

Adobe Experience ManagerをCloud Serviceとして使用できるOSGi設定値は3種類あります。

1. **インライン値**：OSGi 設定にハードコーディングされ、Git に保存される値です。次に例を示します。

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **シークレット値**：セキュリティ上の理由からGitに保存しない値です。以下に例を示します。

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境固有の値**：開発環境間で異なる値なので、実行モードで正確にターゲットを設定できません(Adobe Experience ManagerにはCloud Serviceとしての実行モードが1つだけあるの `dev` で)。次に例を示します。

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   1 つの OSGi 設定ファイルで、これらの設定値タイプの任意の組み合わせを併用できます。次に例を示します。

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 適切な OSGi 設定値タイプの選択方法 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi では、インライン OSGi 設定値を使用する場合が多くあります。環境固有の設定は、開発環境間で値が異なる特定の使用例に対してのみ使用します。

![](assets/choose-configuration-value-type_res1.png)

環境固有の設定は、インライン値を含む、従来の静的に定義されたOSGi設定を拡張し、Cloud Manager APIを介してOSGi設定値を外部で管理できるようにします。 インライン値を定義して Git に保存する一般的で従来の方法を使用する必要がある場合と、値を環境固有の設定に抽象化する必要がある場合を理解することが重要です。

次のガイダンスは、非シークレットの場合とシークレットの場合の環境固有の設定を使用する手順を示しています。

### インライン設定値を使用する場合 {#when-to-use-inline-configuration-values}

インライン設定の値は標準的なアプローチと見なされるので、可能であればこの設定を使用してください。インライン設定には次のような利点があります。

* Git でガバナンスとバージョン履歴に基づいて管理される
* 値はコードデプロイメントに暗黙的に結び付けられる
* デプロイメントに関する検討事項や調整を追加する必要がない

OSGi設定値を定義する場合は、インライン値で始め、必要に応じてシークレット設定または環境固有の設定を選択する必要があります。

### 非シークレットの環境固有の設定値を使用する場合 {#when-to-use-non-secret-environment-specific-configuration-values}

非シークレットの設定値に対しては、開発環境間で値が異なる場合にのみ、環境固有の設定（`$[env:ENV_VAR_NAME]`）を使用してください。これには、ローカル開発インスタンスと、Cloud Service開発環境としてのAdobe Experience Managerが含まれます。 Adobe Experience Managerの非シークレットの環境固有の設定を、環境ステージ環境または実稼動環境として使用するCloud Serviceは避けてください。

* ローカル開発インスタンスなど、開発環境間で異なる設定値に対しては、非シークレットの環境固有の設定のみを使用します。
* 代わりに、ステージングと実稼働の非シークレット値の OSGi 設定では、標準のインライン値を使用します。関連して、実行時にステージ環境と実稼動環境に対して設定を変更しやすくするために、環境固有の設定を使用することはお勧めしません。これらの変更は、ソースコード管理を通じて導入する必要があります。

### シークレットの環境固有の設定値を使用する場合 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as aCloud Serviceでは、セキュリティ上の理由から、パスワード、プライベートAPIキー、Gitに保存できないその他の値など、シークレットのOSGi設定値に対して環境固有の設定(`$[secret:SECRET_VAR_NAME]`)を使用する必要があります。

シークレットの環境固有の設定を使用して、ステージングや実稼動を含むCloud Service環境としてすべてのAdobe Experience Managerにシークレットの値を保存します。

## OSGi 設定の作成 {#creating-sogi-configurations}

OSGi設定を作成する方法は2つあります（以下で説明します）。 前者の方法は、通常、開発者によってよく知られている OSGi のプロパティと値を持つカスタム OSGi コンポーネントの設定に使用され、後者は AEM が提供する OSGi コンポーネントの設定に使用されます。

### OSGi 設定の書き込み  {#writing-osgi-configurations}

JSON 形式の OSGi 設定ファイルは、AEM プロジェクト内から直接手動で書き込むことができます。これは、多くの場合、よく知られているOSGiコンポーネント、特に、設定を定義する同じ開発者が設計および開発したカスタムOSGiコンポーネントのOSGi設定をすばやく作成する方法です。 この方法は、同じOSGiコンポーネントの設定を様々な実行モードフォルダーにコピー/貼り付け、更新する場合にも使用できます。

1. IDEで`ui.apps`プロジェクトを開き、新しいOSGi構成を有効にする必要がある実行モードをターゲットに設定するconfigフォルダー(`/apps/.../config.<runmode>`)を探すか作成します
1. この config フォルダーに、新しい `<PID>.cfg.json` ファイルを作成します。PIDは、OSGiコンポーネントの永続的なIDです。通常、OSGiコンポーネントの実装の完全なクラス名です。 以下に例を示します。
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
OSGi設定ファクトリのファイル名には、命名規則が使用さ `<PID>-<factory-name>.cfg.json` れます。
1. 新しい `.cfg.json` ファイルを開き、[JSON OSGi 設定形式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)に従って、OSGi プロパティと値のペアのキー／値の組み合わせを定義します。
1. 変更を新しい `.cfg.json` ファイルに保存します。
1. 新しい追加 OSGi 構成ファイルを Git にコミットします。

### AEM SDK Quickstart を使用した OSGi 設定の生成  {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jar の AEM Web コンソールは、OSGi コンポーネントの設定、および JSON として OSGi 設定を書き出すために使用できます。これは、OSGi プロパティとその値の形式が AEM プロジェクトで OSGi 設定を定義する開発者には理解されない可能性のある、AEM が提供する OSGi コンポーネントを設定する場合に役立ちます。

>[!NOTE]
>
>AEM Webコンソールの設定UIは、`.cfg.json`ファイルをリポジトリに書き込みます。 したがって、AEMプロジェクト定義のOSGi設定が生成された設定と異なる場合に、ローカル開発中に予期しない動作が発生する可能性を回避するために、この点に注意してください。

1. AEM SDK Quickstart Jar の AEM Web コンソールに管理者ユーザーとしてログインします。
1. OSGi／設定に移動します。
1. 設定するには、OSGiコンポーネントを探し、タイトルをタップして編集します
   ![OSGi 設定](./assets/configuring-osgi/configuration.png)
1. 必要に応じて Web UI を使用して OSGi 設定プロパティの値を編集します。
1. 安全な場所に永続ID(PID)を記録します。 これは、後でOSGi設定JSONを生成するために使用されます
1. 「保存」をタップします。
1. OSGi／OSGi インストーラー設定プリンターに移動します。
1. 手順 5 でコピーした PID に貼り付け、シリアル化形式が「OSGi Configurator JSON」に設定されていることを確認します。
1. 印刷をタップ
1. JSON 形式の OSGi 設定は、「シリアライズされた設定プロパティ」セクションに表示されます。
   ![OSGi インストーラー設定プリンター](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. IDEで`ui.apps`プロジェクトを開き、新しいOSGi構成を有効にする実行モードをターゲットに設定するconfigフォルダー(`/apps/.../config.<runmode>`)を探すか作成します。
1. この config フォルダーに、新しい `<PID>.cfg.json` ファイルを作成します。PID は、手順 5 と同じ値です。
1. 手順 10 のシリアライズされた設定プロパティを `.cfg.json` ファイルに貼り付けます。
1. 変更を新しい `.cfg.json` ファイルに保存します。
1. 新しい追加 OSGi 構成ファイルを Git にコミットします。


## OSGi 構成プロパティの形式  {#osgi-configuration-property-formats}

### インライン値 {#inline-values}

インライン値は、標準のJSON構文に従って、標準の名前と値のペアとして形式設定されます。 以下に例を示します。

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境固有の設定値{#environment-specific-configuration-values}

OSGi 設定では、環境ごとに定義する変数にプレースホルダーを割り当てる必要があります。

```
use $[env:ENV_VAR_NAME]
```

この手法は、カスタムコードに関連するOSGi設定プロパティにのみ使用する必要があります。Adobe定義のOSGI設定を上書きする場合は、このメソッドを使用しないでください。

>[!NOTE]
>
>[repoinitステートメント](/help/implementing/deploying/overview.md#repoinit)ではプレースホルダーを使用できません。

### シークレットの設定値 {#secret-configuration-values}

OSGi 設定では、環境ごとに定義するシークレットにプレースホルダーを割り当てる必要があります。

```
use $[secret:SECRET_VAR_NAME]
```

### 変数の命名 {#variable-naming}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

変数名は、次のルールに従う必要があります。

* 最小長：2
* 最大長：100
* 正規表現と一致する必要があります。`[a-zA-Z_][a-zA-Z_0-9]*`

変数の値は2048文字以下にする必要があります。

>[!NOTE]
>
>`INTERNAL_`のプレフィックスが付いた変数名は、Adobeで予約されます。 このプレフィックスで始まる顧客セット変数は無視されます。

### デフォルト値 {#default-values}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

環境単位の値を設定しない場合、補間がおこなわれないので、プレースホルダーは実行時に置き換えられず、配置されたままになります。 これを回避するには、プレースホルダーの一部として次の構文でデフォルト値を指定します。

```
$[env:ENV_VAR_NAME;default=<value>]
```

デフォルト値を指定すると、プレースホルダーは環境ごとの値（指定した場合）または指定したデフォルト値に置き換えられます。

### ローカル開発 {#local-development}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

変数は、実行時にローカル AEM によって取得されるように、ローカル環境で定義できます。Linux®の場合：

```bash
export ENV_VAR_NAME=my_value
```

設定で使用される環境変数を設定し、AEM を起動する前に実行する、単純な bash スクリプトを記述することをお勧めします。[https://direnv.net/](https://direnv.net/) などのツールを使うと、このアプローチを簡略化できます。すべてのユーザー間で共有できる場合は、値のタイプに応じて、値をソースコード管理にチェックインできることがあります。

シークレットの値はファイルから読み取られます。したがって、シークレットを使用するプレースホルダーごとに、シークレット値を含むテキストファイルを作成する必要があります。

例えば、`$[secret:server_password]`を使用する場合は、**server_password**&#x200B;という名前のテキストファイルを作成する必要があります。 これらのシークレットファイルはすべて同じディレクトリに保存する必要があり、フレームワークプロパティ`org.apache.felix.configadmin.plugin.interpolation.secretsdir`は、そのローカルディレクトリを使用して設定する必要があります。

### オーサーとパブリッシュの設定 {#author-vs-publish-configuration}

OSGi プロパティで、作成者とパブリッシュで異なる値が必要な場合：

* [実行モードの解決の節](#runmode-resolution)で説明しているように、個別の`config.author`と`config.publish` OSGiフォルダーを使用する必要があります。
* 独立変数名を作成する場合、次の2つのオプションを使用できます。
   * 最初のオプション（推奨）:異なる値を定義するように宣言されたすべてのOSGIフォルダー（`config.author`と`config.publish`など）で、同じ変数名を使用します。 例：
      `$[env:ENV_VAR_NAME;default=<value>]`：デフォルトは、その層（オーサーまたはパブリッシュ）のデフォルト値です。環境変数を[Cloud Manager API](#cloud-manager-api-format-for-setting-properties)またはクライアントを使用して設定する場合は、この[APIリファレンスドキュメント](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)で説明されているように、「service」パラメーターを使用して層を区別します。 「service」パラメーターは、変数の値を適切なOSGI層にバインドします。
   * 2つ目のオプション。`author_<samevariablename>`や`publish_<samevariablename>`などのプレフィックスを使用して個別の変数を宣言します。

### 設定例 {#configuration-examples}

以下の例では、ステージ環境と実稼動環境に加えて、3つの開発環境があると仮定します。

**例 1**

OSGiプロパティ`my_var1`の値を、ステージングと実稼動環境で同じ値、3つの開発環境でそれぞれ異なる値にします。

<table>
<tr>
<td>
<b>Folder</b>
</td>
<td>
<b>myfile.cfg.json の内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**例 2**

OSGiプロパティ`my_var1`の値を、ステージング、実稼働、3つの開発環境でそれぞれ異なる値にします。 したがって、各開発環境の`my_var1`の値を設定するには、Cloud Manager APIを呼び出す必要があります。

<table>
<tr>
<td>
<b>フォルダー</b>
</td>
<td>
<b>myfile.cfg.json の内容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1": "val2",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

**例 3**

OSGi プロパティ `my_var1` の値をステージング、実稼働、1 つの開発環境で同じ値、他の 2 つの開発環境では異なる値にします。この場合、Cloud Manager APIを呼び出して各開発環境の値`my_var1`を設定する必要があります。この値は、ステージングと実稼動と同じ値にする必要がある開発環境も含まれます。 フォルダー **config** に設定された値は継承されません。

<table>
<tr>
<td>
<b>フォルダー</b>
</td>
<td>
<b>myfile.cfg.json の内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1":"val1",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

これをおこなう別の方法は、config.dev フォルダーの置き換えトークンのデフォルト値を、**config** フォルダーと同じ値に設定することです。

<table>
<tr>
<td>
<b>フォルダー</b>
</td>
<td>
<b>myfile.cfg.json の内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ 
 "my_var1":"val1",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

## プロパティ設定用の Cloud Manager API 形式 {#cloud-manager-api-format-for-setting-properties}

API の設定方法については、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)を参照してください。
>[!NOTE]
>
>使用している Cloud Manager API に「デプロイメントマネージャー - Cloud Service」という役割が割り当てられていることを確認します。その他の役割では、必ずしも以下のすべてのコマンドを実行できるわけではありません。

### API を使用した値の設定 {#setting-values-via-api}

APIを呼び出すと、一般的な顧客コードのデプロイメントパイプラインと同様に、新しい変数と値がクラウド環境にデプロイされます。 オーサーとパブリッシュサービスは再起動され、新しい値が参照されます（通常、数分かかります）。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>デフォルトの変数はAPI経由ではなく、OSGiプロパティ自体に設定されます。
>
>詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)を参照してください。

### API を使用した値の取得 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables)を参照してください。

### API を使用した値の削除 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

変数を削除するには、空の値を含めます。

詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)を参照してください。

### コマンドラインを使用した値の取得 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### コマンドラインを使用した値の設定 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### コマンドラインを使用した値の削除 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>Adobe I/O CLI 用の Cloud Manager プラグインを使用した値の設定方法の詳細については、[こちらのページ](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)を参照してください。

### 変数の数 {#number-of-variables}

1 つの環境につき最大 200 個の変数を宣言できます。

## シークレットおよび環境固有の設定値のデプロイメントに関する考慮事項{#deployment-considerations-for-secret-and-environment-specific-configuration-values}

秘密鍵や環境固有の設定値はGitの外部に存在するので、Cloud Serviceデプロイメントメカニズムとしての正式なAdobe Experience Managerには含まれていないので、Cloud ServiceデプロイメントプロセスとしてAdobe Experience Managerを管理、管理、統合する必要があります。

前述したように、 APIを呼び出すと、一般的な顧客コードのデプロイメントパイプラインと同様に、新しい変数と値がクラウド環境にデプロイされます。 オーサーとパブリッシュサービスは再起動され、新しい値が参照されます（通常、数分かかります）。通常のコードのデプロイメント中に Cloud Manager によって実行される品質ゲートおよびテストは、このプロセス中は実行されません。

通常、Cloud Manager で API を使用するコードをデプロイする前に、API を呼び出して環境変数を設定します。場合によっては、コードが既にデプロイされた後で既存の変数を変更する必要があります。

>[!NOTE]
>
>APIは、AEMの更新または顧客のデプロイメントなど、パイプラインが使用中の場合、その時点でエンドツーエンドパイプラインのどの部分が実行されているかに応じて、成功しない場合があります。 エラーの応答は、リクエストが成功しなかったことを示しますが、理由は示しません。

予定されている顧客コードのデプロイメントが、新しい値を持つ既存の変数に依存している場合があります。これは、現在のコードには適していません。これが問題となる場合は、変数の変更を加えることをお勧めします。 そのためには、古いコードが新しい値を参照しないように、古い変数の値を変更する代わりに、新しい変数名を作成します。後日、新しいカスタマーリリースが安定したら、古い値を削除できます。

同様に、変数の値はバージョン管理されないので、コードのロールバックによって、新しい値を参照することで問題を引き起こす場合があります。前述の変数の加算方法もここで役立ちます。

この変数の加算方式戦略は、数日前のコードを再デプロイする必要がある災害復旧シナリオにも役立ちます。コードが参照する変数名と値は変わりません。これは、顧客が古い変数を削除する前に数日間待機するという手法に依存しています。この手法を使用していない場合、古いコードには参照できる適切な変数はありません。
