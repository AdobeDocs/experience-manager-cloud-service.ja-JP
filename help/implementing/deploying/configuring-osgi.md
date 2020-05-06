---
title: AEM用のOSGiをクラウドサービスとして設定する
description: 'シークレット値と環境固有の値を使用するOSGi設定 '
translation-type: tm+mt
source-git-commit: 48a19fb1bb7657d34f31605a3b4a85e656393918
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 3%

---


# AEM用のOSGiをクラウドサービスとして設定する {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) はAdobe Experience Manager(AEM)の技術スタックの基本要素です。 AEMとその設定の複合バンドルを制御するために使用されます。

OSGiは、小規模で再利用可能なコラボレーションコンポーネントからアプリケーションを構築できるように、標準化されたプリミティブを提供します。 これらのコンポーネントは、アプリケーションに組み込んでデプロイすることができます。 これにより、OSGiバンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。 相互依存関係は自動的に処理されます。 各OSGiコンポーネントは、様々なバンドルの1つに含まれています。 詳しくは、 [OSGiの仕様を参照してください](https://www.osgi.org/Specifications/HomePage)。

AEMコードプロジェクトに含まれる設定ファイルを使用して、OSGiコンポーネントの設定を管理できます。

## OSGi Configuration Files {#osgi-configuration-files}

設定の変更は、AEM Projectのコードパッケージ(`ui.apps`)で、実行モード固有の設定フォルダーの下に設定ファイル(`.cfg.json`)として定義されます。

`/apps/example/config.<runmode>`

OSGi設定ファイルの形式は、Apache Slingプロジェクトで定義されている `.cfg.json` 形式を使用したJSONベースです。

OSGi設定ターゲットOSGiコンポーネントは、Persistent Identity(PID)を介してコンポーネントを設定します。デフォルトでは、OSGiコンポーネントのJavaクラス名です。 例えば、次の方法で実装されるOSGiサービス用のOSGi設定を提供するには：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi設定ファイルは次の場所で定義されます。

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

次の [cfg.json OSGi設定形式]（cfg.json OSGi設定形式に従います）。

> [!NOTE]
>
> 以前のバージョンのAEMでサポートされていたOSGi設定ファイルは、.cfg.、.config、XML sling:OsgiConfigリソース定義など、様々なファイル形式を使用しています。 これらの形式は、cfg.json OSGi設定形式に置き換えられました。

## Runmode Resolution {#runmode-resolution}

ランモードを使用すると、特定のOSGi設定を特定のAEMインスタンスにターゲット設定できます。 runmodeを使用するには、次の形式で、 `/apps/example` （例えばプロジェクト名）の下にconfigフォルダーを作成します。

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

configフォルダー名で定義された実行モードがAEMで使用される実行モードと一致する場合、このようなフォルダー内のOSGi設定が使用されます。

例えば、AEMがrunmodes author and devを使用している場合、およびの設定ノードは適用され `/apps/example/config.author/` 、およびの設定ノードは `/apps/example/config.author.dev/``/apps/example/config.publish/``/apps/example/config.author.stage/` 適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

このルールの精度はPIDレベルです。 つまり、同じPIDの一部のプロパティと、同じPIDのより具体的なプロパティ `/apps/example/config.author/` を定義す `/apps/example/config.author.dev/` ることはできません。  一致する実行モードの数が最も多い設定は、PID全体に対して有効です。

ローカルで開発する場合は、実行モード起動パラメーターを渡して、使用する実行モード OSGi 設定を指定できます。

## OSGi設定値のタイプ {#types-of-osgi-configuration-values}

AEMでクラウドサービスとして使用できるOSGi設定値には3種類あります。

1. **インライン値**。OSGi設定にハードコードされ、Gitに保存される値です。 次に例を示します。

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **シークレット値**。セキュリティ上の理由からGitに保存しない値です。 次に例を示します。

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境固有の値**。開発環境間で変化する値であり、したがって実行モードで正確にターゲットにすることはできません(AEMではクラウドサービスとして `dev` 1つの実行モードが存在するため)。 次に例を示します。

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   1つのOSGi設定ファイルで、これらの設定値タイプの任意の組み合わせを併用できます。 次に例を示します。

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 適切なOSGi設定値タイプの選択方法 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGiでは、インラインOSGi設定値を使用する場合が多くあります。 環境固有の設定は、開発環境間で値が異なる特定の使用例に対してのみ使用します。

![](assets/choose-configuration-value-type_res1.png)

環境固有の設定は、インライン値を含む、従来の静的に定義されたOSGi設定を拡張し、Cloud Manager APIを介してOSGi設定値を外部で管理できるようにします。 インライン値を定義してGitに保存する一般的で従来の方法を使用する必要がある場合、値を環境固有の設定に抽象化する必要がある場合を理解することが重要です。

次のガイダンスは、非秘密の構成と秘密の環境固有の構成を使用する場合の手順を示しています。

### インライン設定値を使用するタイミング {#when-to-use-inline-configuration-values}

インライン設定の値は標準的な方法と見なされるので、可能な場合は使用する必要があります。 インライン設定には次のような利点があります。

* Gitでのガバナンスとバージョン履歴に基づいて管理されます。
* 値はコードデプロイメントに暗黙的に結び付けられます
* 配置に関する考慮事項や調整を追加する必要はありません。

OSGi設定値を定義する場合は、インライン値を持つ開始は、必要に応じてシークレット設定または環境固有の設定を選択するだけです。

### 非秘密環境固有の設定値を使用する場合 {#when-to-use-non-secret-environment-specific-configuration-values}

非秘密の設定値に対しては、開発環境間で値が異なる場合にのみ、環境固有の設定(`$[env:ENV_VAR_NAME]`)を使用してください。 これには、ローカル開発インスタンスと、クラウドサービス開発環境としてのAEMが含まれます。 AEMの非秘密環境固有の設定を、クラウドサービスの段階または実稼働環境として使用しないでください。

* ローカル開発インスタンスなど、開発環境間で異なる設定値に対しては、秘密の環境固有でない設定のみを使用します。
* 代わりに、StageとProductionの非秘密値のOSGi設定で、標準のインライン値を使用します。  これに関連して、実行時にステージ環境と実稼働環境に対して設定を簡単に変更するために、環境固有の設定を使用しないことをお勧めします。 これらの変更は、ソースコード管理を通じて導入する必要があります。

### シークレット環境固有の設定値を使用するタイミング {#when-to-use-secret-environment-specific-configuration-values}

AEM as a Cloud Serviceでは、セキュリティ上の理由から、パスワード、プライベートAPIキー、Gitに保存できない他の値など、秘密のOSGi設定値に対して環境固有の設定(`$[secret:SECRET_VAR_NAME]`)を使用する必要があります。

秘密の環境固有の設定を使用して、StageやProductionなどのクラウドサービス環境としてすべてのAEMに秘密の値を保存します。

<!-- ### Adding a New Configuration to the Repository {#adding-a-new-configuration-to-the-repository}

#### What You Need to Know {#what-you-need-to-know}

To add a new configuration to the repository you need to know the following:

1. The **Persistent Identity** (PID) of the service.

   Reference the **Configurations** field in the Web console. The name is shown in brackets after the bundle name (or in the **Configuration Information** towards the bottom of the page).

   For example, create a node `com.day.cq.wcm.core.impl.VersionManagerImpl.` to configure **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Whether a specific runmode is required. Create the folder:

    * `config` - for all run modes
    * `config.author` - for the author environment
    * `config.publish` - for the publish environment
    * `config.<run-mode>` - as appropriate

1. Whether a **Configuration** or **Factory Configuration** is necessary.
1. The individual parameters to be configured; including any existing parameter definitions that will need to be recreated.

   Reference the individual parameter field in the Web console. The name is shown in brackets for each parameter.

   For example, create a property
   `versionmanager.createVersionOnActivation` to configure **Create Version on Activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Does a configuration already exist in `/libs`? To list all configurations in your instance, use the **Query** tool in CRXDE Lite to submit the following SQL query:

   `select * from sling:OsgiConfig`

   If so, this configuration can be copied to ` /apps/<yourProject>/`, then customized in the new location.

## Creating the Configuration in the Repository {#creating-the-configuration-in-the-repository}

To actually add the new configuration to the repository:

1. In your ui.apps project, create a `/apps/…/config.xxx` folder as needed based on the runmode you are using

1. Create a new JSON file with the name of the PID and add the `.cfg.json` extension


1. Populate the JSON file with the OSGi configuration key value pairs

   >[!NOTE]
   >
   >If you are configuring an out of the box OSGi service, you can look up the OSGi property names via `/system/console/configMgr`


1. Save the JSON file to your project. -->

## ソース管理の設定プロパティの形式 {#configuration-property-format-in-source-control}

<!-- Creating a new OSGI configuration property is described in the [Adding a new configuration to the repository](#creating-the-configuration-in-the-repository) section above. -->

次の手順に従い、次のサブセクションで説明されている構文を変更します。

### インライン値 {#inline-values}

予想通り、インライン値は、標準のJSON構文に従って、標準の名前と値のペアとして形式設定されます。 次に例を示します。

```json
 {

 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500

}
```

### 環境固有の設定値 {#environment-specific-configuration-values}

OSGi設定では、環境ごとに定義する変数にプレースホルダを割り当てる必要があります。

```
use $[env:ENV_VAR_NAME]
```

お客様は、カスタムコードに関連するOSGI設定プロパティに対してのみ、この手法を使用する必要があります。 アドビ定義のOSGI設定を上書きする場合は使用しないでください。

### シークレットの設定値 {#secret-configuration-values}

OSGi設定では、環境ごとに定義するシークレットのプレースホルダを割り当てる必要があります。

```
use $[secret:SECRET_VAR_NAME]
```

### 変数の命名 {#variable-naming}

環境固有の設定値とシークレットの設定値の両方に適用されます。

変数名は、次の規則に従う必要があります。

* 最小長： 2
* 最大長： 100
* はregexと一致する必要があります。 `[a-zA-Z_][a-zA-Z_0-9]*`

変数の値は2048文字を超えないようにしてください。

### デフォルト値 {#default-values}

環境固有の設定値とシークレットの設定値の両方に適用されます。

環境単位の値を設定しない場合、補間が行われないので、プレースホルダは実行時に置き換えられず、配置されたままになります。 これを回避するには、プレースホルダーの一部として次の構文でデフォルト値を指定します。

```
$[env:ENV_VAR_NAME;default=<value>]
```

デフォルト値を指定すると、プレースホルダーは、環境ごとの値（指定した場合）または指定したデフォルト値に置き換えられます。

### ローカル開発 {#local-development}

環境固有の設定値とシークレットの設定値の両方に適用されます。

変数は、実行時にローカルAEMによって取得されるように、ローカル環境で定義できます。 例えば、Linuxの場合：

```bash
export ENV_VAR_NAME=my_value
```

設定で使用される環境変数を設定し、AEMを起動する前にそれを実行する、単純なbashスクリプトを記述することをお勧めします。 https://direnv.net/などのツール [を使って](https://direnv.net/) 、このアプローチを簡略化できます。 値のタイプに応じて、すべてのユーザー間で共有できる場合は、値をソースコード管理にチェックインできます。

シークレットの値はファイルから読み取られます。 したがって、シークレットを使用するプレースホルダごとに、シークレット値を含むテキストファイルを作成する必要があります。

例えば、を使用 `$[secret:server_password]` する場合は、 **server_password** という名前のテキストファイルを作成する必要があります。 これらのシークレットファイルはすべて同じディレクトリに保存する必要があり、フレームワークのプロパティはそのローカルディレクトリを使用して設定する必要 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` があります。

### 作成者と発行の設定 {#author-vs-publish-configuration}

OSGIプロパティで、作成者とパブリッシュで異なる値が必要な場合：

* 「 `config.author` 実行モードの解決」の節で説明したように、個別の `config.publish` OSGiフォルダーとOSGiフォルダーを使用する必要があり [](#runmode-resolution)ます。
* 独立変数名を使用する必要があります。 変数名が同じである場合は、 `author_<variablename>` およびなどのプレフィックス `publish_<variablename>` を使用することをお勧めします。

### 設定例 {#configuration-examples}

以下の例では、ステージ環境とprod環境に加えて、3つの開発環境があると仮定します。

**例1**

この意図は、OSGIプロパティの値がstageとprod `my_var1` で同じになることですが、3つの開発環境ごとに異なります。

<table>
<tr>
<td>
<b>Folder</b>
</td>
<td>
<b>myfile.cfg.jsonの内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**例2**

この目的は、OSGIプロパティの値がステージ、prod、および3つの開発環境 `my_var1` ごとに異なることです。 したがって、各開発環境の値を設定するには、Cloud Manager APIを呼び出す必要 `my_var1` があります。

<table>
<tr>
<td>
<b>Folder</b>
</td>
<td>
<b>myfile.cfg.jsonの内容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**例3**

この意図は、OSGiプロパティの値がステージ、実稼働、および開発環境の1つ `my_var1` に対して同じであることを前提としていますが、他の2つの開発環境に対しては異なる点が前提となっています。 この場合、Cloud Manager APIを呼び出して各開発環境の値を設定する必要があります。この値は、開発環境の場合を含め、ステージと実稼働と同じ値にする必要があります。 `my_var1` フォルダー **configに設定された値は継承されません**。

<table>
<tr>
<td>
<b>Folder</b>
</td>
<td>
<b>myfile.cfg.jsonの内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

これを行う別の方法は、config.devフォルダーの置き換えトークンのデフォルト値を、config **** フォルダーと同じ値に設定することです。

<table>
<tr>
<td>
<b>Folder</b>
</td>
<td>
<b>myfile.cfg.jsonの内容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

## プロパティ設定用のCloud Manager API形式 {#cloud-manager-api-format-for-setting-properties}

### APIを使用した値の設定 {#setting-values-via-api}

APIを呼び出すと、一般的なカスタマーコードの導入パイプラインと同様に、新しい変数と値がクラウド環境に導入されます。 作成者サービスと発行サービスは再起動され、新しい値が参照されます（通常、数分かかります）。

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

デフォルトの変数はAPI経由ではなく、OSGiプロパティ自体に設定されることに注意してください。

詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)を参照してください。

### APIを使用した値の取得 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables)を参照してください。

### APIを使用した値の削除 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

変数を削除するには、空の値を含めます。

詳しくは、[こちらのページ](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)を参照してください。

### コマンドラインから値を取得する {#getting-values-via-cli}

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

> [!NOTE]
>
> Adobe I/O CLI用 [のCloud Managerプラグインを使用した値の設定方法の詳細については、このページを参照してください](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 。

### 変数の数 {#number-of-variables}

最大20個の変数を宣言できます。

## シークレットおよび環境固有の設定値のデプロイメントに関する考慮事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

秘密と環境に固有の設定値はGitの外部に存在するので、クラウドサービスの展開メカニズムとしての正式なAEMには含まれないので、お客様はクラウドサービスの展開プロセスとしてAEMに管理、管理および統合する必要があります。

前述したように、APIを呼び出すと、一般的なカスタマーコードの導入パイプラインと同様に、新しい変数と値がクラウド環境に導入されます。 作成者サービスと発行サービスは再起動され、新しい値が参照されます（通常、数分かかります）。 通常のコードのデプロイメント中にCloud Managerによって実行される品質ゲートおよびテストは、このプロセス中は実行されません。

通常、Cloud ManagerでAPIを使用するコードを導入する前に、APIを呼び出して環境変数を設定します。 場合によっては、コードが既に導入された後で既存の変数を変更する必要があります。

パイプラインが使用中の場合、AEMの更新またはお客様向けのデプロイメントは、その時点でエンドツーエンドパイプラインのどの部分が実行されているかに応じて、APIが正常に動作しない可能性があります。 エラーの応答は、リクエストが成功しなかったことを示しますが、理由は示しません。

予定されている顧客コードの導入が、新しい値を持つ既存の変数に依存している場合があります。これは、現在のコードでは適しません。 これが問題となる場合は、変数の変更を加える方法をお勧めします。 そのためには、古いコードが新しい値を参照しないように、古い変数の値を変更する代わりに、新しい変数名を作成します。 その後、新しいリリースの顧客が安定した状態になった場合は、古い値を削除することを選択できます。

同様に、変数の値はバージョン管理されないので、コードのロールバックによって、問題を引き起こす新しい値が参照される場合があります。 上記の加算変数戦略もこの場合に役立ちます。

この加算変数戦略は、数日前のコードを再展開する必要がある場合でも、そのコードが参照する変数名と値が変わらない場合の災害復旧シナリオにも役立ちます。 これは、お客様が古い変数を削除する数日前に待機する方法に依存しています。そうしないと、古いコードで参照する適切な変数がなくなります。