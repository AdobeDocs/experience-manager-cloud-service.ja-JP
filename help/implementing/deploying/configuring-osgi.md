---
title: Adobe Experience Manager as a Cloud Service の OSGi の設定
description: シークレット値と環境固有の値を使用する OSGi 設定
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3321'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service の OSGi の設定 {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) は Adobe Experience Manager（AEM）のテクノロジースタックの基本要素です。AEM とその設定の複合バンドルを制御するために使用されます。

OSGi で提供されている標準化されたプリミティブにより、サイズが小さく再利用やコラボレーションが可能なコンポーネントからアプリケーションを構築できます。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。これにより、OSGi バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネントは、様々なバンドルの 1 つに含まれています。詳しくは、[OSGi の仕様](https://help.eclipse.org/latest/index.jsp)を参照してください。

AEM コードプロジェクトに含まれる設定ファイルを使用して、OSGi コンポーネントの設定を管理できます。

>[!TIP]
>
>Cloud Manager を使用して環境変数を設定できます。詳しくは、 [こちら](/help/implementing/cloud-manager/environment-variables.md) のドキュメントを参照してください。

## OSGi の設定ファイル {#osgi-configuration-files}

設定の変更は、 AEM プロジェクトのコードパッケージ（`ui.config`）で、実行モード固有の config フォルダーの下に設定ファイル（`.cfg.json`）として定義されます。

`/apps/example/config.<runmode>`

OSGi 設定ファイルは、Apache Sling プロジェクトで定義されている `.cfg.json` 形式を使用した JSON ベース形式です。

OSGi 設定は Persistent Identity（PID）を介して OSGi コンポーネントをターゲットに設定します。デフォルトは、OSGi コンポーネントの Java™ クラス名です。例えば、OSGi サービス用の OSGi 設定を提供するには、次のように実装します。

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi 設定ファイルは次の場所で定義されます。

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

`cfg.json` OSGi 設定形式に従います。

>[!NOTE]
>
>以前のバージョンの AEM では、`.cfg`、`.config` などの様々なファイル形式を使用し、XML `sling:OsgiConfig` リソース定義として OSGi 設定ファイルをサポートしていました。これらの形式は、`.cfg.json` OSGi 設定形式に置き換えられています。

>[!NOTE]
>
>OSGi 設定は、クラウドの一般的な AEM インスタンスのように /apps 下ではなく、外部の場所に格納されます。Cloud Manager [Developer Console](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#configurations) にチェックインして、OSGi 設定を表示します。

## 実行モードの解決 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x はカスタム実行モードをサポートしていますが、AEM as a Cloud Service はサポートしていません。AEM as a Cloud Service は、[実行モードの正確なセット](./overview.md#runmodes)をサポートします。AEM as a Cloud Service 環境間の OSGi 設定の違いは、[OSGi 設定の環境変数](#environment-specific-configuration-values)を使用して処理する必要があります。

実行モードを使用すると、特定の OSGi 設定を特定の AEM インスタンスにターゲット設定できます。実行モードを使用するには、次の形式で、`/apps/example`（「example」はプロジェクト名）の下に config フォルダーを作成します。

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

config フォルダー名で定義された実行モードが AEM で使用される実行モードと一致する場合、このようなフォルダー内の OSGi 設定が使用されます。

例えば、AEM がオーサーと開発の実行モードを使用している場合、`/apps/example/config.author/` および `/apps/example/config.author.dev/` の設定ノードが適用され、`/apps/example/config.publish/` および `/apps/example/config.author.stage/` の設定ノードは適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

このルールの精度は PID レベルです。つまり、`/apps/example/config.author/` で同じ PID の一部のプロパティと、`/apps/example/config.author.dev/` で同じ PID のより具体的なプロパティを定義することはできません。一致する実行モードの数が最も多い設定は、PID 全体に対して効果的です。

>[!NOTE]
>
>`config.preview` OSGI 設定フォルダーは、`config.publish` フォルダーを宣言する場合と同じようには宣言&#x200B;**できません**。代わりに、プレビュー層はパブリッシュ層の値から OSGI 設定を継承します。

ローカルで開発する場合、実行モードの起動パラメーター `-r` を使用して、実行モードの OSGI 設定を指定します。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 実行モードの検証

AEM as a Cloud Service の実行モードは、環境のタイプとサービスに基づいて適切に定義されています。[使用可能な AEM as a Cloud Service 実行モードの完全なリスト](./overview.md#runmodes)をご確認ください。

実行モードで指定された OSGi 設定値は、次の方法で検証できます。

1. AEM as a Cloud Services 環境の[開発者コンソール](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=ja)を開きます
1. __ポッド__&#x200B;ドロップダウンリストを使用して、検査するサービス層を選択します
1. 「__ステータス__」タブを選択します
1. __ステータスダンプ__&#x200B;ドロップダウンリストから「__設定__」を選択します
1. 「__ステータスの取得__」ボタンを選択します

結果には、選択した層のすべての OSGi コンポーネント設定と、該当する OSGi 設定値が表示されます。 これらの値は、`/apps/example/osgiconfig/config.<runmode(s)>` の下にある AEM プロジェクトのソースコード内の OSGi 設定値と相互参照できます


適切な OSGi 設定値が適用されていることを確認するには：

1. 開発者コンソールの設定出力で
1. 検証する OSGi 設定を表す `pid` を見つけます。これは、AEM プロジェクトのソースコード内の OSGi 設定ファイルの名前です。
1. `pid` の `properties` リストを検査し、キーと値が検査対象の実行モードの AEM プロジェクトソースコードの OSGi 設定ファイルと一致することを確認します。


## OSGi 設定値のタイプ {#types-of-osgi-configuration-values}

Adobe Experience Manager as a Cloud Service で使用できる OSGi 設定値は 3 種類あります。

1. **インライン値**：OSGi 設定にハードコーディングされ、Git に保存される値です。例：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **シークレット値**：セキュリティ上の理由から Git に保存してはいけない値です。例：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境固有値**：開発環境間で変化する値なので、実行モードで正確にターゲットを設定できません（Adobe Experience Manager as a Cloud Service には 1 つの `dev` 実行モードのみ存在するため）。例：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   1 つの OSGi 設定ファイルで、これらの設定値タイプを任意に組み合わせて使用できます。例：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 適切な OSGi 設定値タイプの選択方法 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi では、インライン OSGi 設定値を使用する場合が多くあります。環境固有の設定は、開発環境間で値が異なる特定の使用例に対してのみ使用します。

![適切な設定値タイプの使用方法に関する決定ツリー](assets/choose-configuration-value-type_res1.png)

環境固有の設定は、インライン値を含む、従来の静的に定義された OSGi 設定を拡張し、Cloud Manager API を介して OSGi 設定値を外部で管理できるようにします。インライン値を定義して Git に保存する一般的で従来の方法を使用する必要がある場合と、値を環境固有の設定に抽象化する必要がある場合を理解することが重要です。

次のガイダンスは、非シークレットの場合とシークレットの場合の環境固有の設定を使用する手順を示しています。

### インライン設定値を使用する場合 {#when-to-use-inline-configuration-values}

インライン設定の値は標準的なアプローチと見なされるので、可能であればこの設定を使用してください。インライン設定には次のような利点があります。

* Git でガバナンスとバージョン履歴に基づいて管理される
* 値はコードデプロイメントに暗黙的に結び付けられる
* デプロイメントに関する検討事項や調整を追加する必要がない

OSGi 設定値を定義する場合は、インライン値から開始し、必要な場合にのみシークレット設定または環境固有の設定を選択します。

### 非シークレットの環境固有の設定値を使用する場合 {#when-to-use-non-secret-environment-specific-configuration-values}

非シークレットの設定値に対しては、プレビュー層で値が異なる場合や、開発環境間で値が異なる場合にのみ、環境固有の設定（`$[env:ENV_VAR_NAME]`）を使用してください。これには、ローカル開発インスタンスと、Adobe Experience Manager as a Cloud Service 開発環境が含まれます。プレビュー層に一意の値を設定する場合を除き、Adobe Experience Manager as a Cloud Service の非シークレットの環境固有の設定をステージ環境または実稼動環境で使用しないでください。

* パブリッシュ層とプレビュー層で異なる設定値や、開発環境間（ローカル開発インスタンスを含む）で異なる値には、非シークレット環境固有の設定値のみを使用します。
* プレビュー層とパブリッシュ層が異なる必要がある場合のシナリオを除き、ステージと実稼動の非シークレット値の OSGi 設定では標準のインライン値を使用します。これに関連して、ステージング環境と実稼働環境に対して、環境固有の設定を使用して、実行時に設定を変更しやすくすることは勧められません。これらの変更は、ソースコード管理を通じて導入する必要があります。

### シークレットの環境固有の設定値を使用する場合 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service では、セキュリティ上の理由から、パスワード、プライベート API キー、Git に保存できない他の値など、シークレットの OSGi 設定値に対して環境固有の設定（`$[secret:SECRET_VAR_NAME]`）を使用する必要があります。

シークレットの環境固有の設定を使用して、ステージングや実稼働などのあらゆる Adobe Experience Manager as a Cloud Service 環境にシークレットの値を保存します。

## OSGi 設定の作成 {#creating-osgi-configurations}

以下に説明するように、OSGi 設定を作成する方法は 2 とおりあります。前者の方法は、通常、開発者によってよく知られている OSGi のプロパティと値を持つカスタム OSGi コンポーネントの設定に使用され、後者は AEM が提供する OSGi コンポーネントの設定に使用されます。

### OSGi 設定の書き込み {#writing-osgi-configurations}

JSON 形式の OSGi 設定ファイルは、AEM プロジェクト内から直接手動で書き込むことができます。これは、よく知られている OSGi コンポーネント、特に、設定を定義した同じ開発者により設計および開発されたカスタム OSGi コンポーネントに対して、OSGi 設定をすばやく作成する方法です。この方法は、同じ OSGi コンポーネントの設定を様々な実行モードフォルダーにコピー／貼り付け、更新する場合にも使用できます。

1. IDE で `ui.apps` プロジェクトを開き、新しい OSGi 設定が有効となる実行モードをターゲットに設定する config フォルダー（`/apps/.../config.<runmode>`）を探すか作成します。
1. この config フォルダーで、`<PID>.cfg.json` ファイルを作成します。PID は OSGi コンポーネントの永続 ID です。通常は、OSGi コンポーネント実装の完全なクラス名になります。例：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
OSGi 設定ファクトリのファイル名には `<factoryPID>-<name>.cfg.json` 命名規則を使用します。
1. 新しい `.cfg.json` ファイルを開き、[JSON OSGi 設定形式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)に従って、OSGi プロパティと値のペアのキー／値の組み合わせを定義します。
1. 変更を新しい `.cfg.json` ファイルに保存します。
1. 新しい追加 OSGi 構成ファイルを Git にコミットします。

### AEM SDK Quickstart を使用した OSGi 設定の生成 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jar の AEM Web コンソールは、OSGi コンポーネントの設定、および JSON として OSGi 設定を書き出すために使用できます。これが役に立つのは、AEM 提供の OSGi コンポーネントを設定する際に、その OSGi プロパティと値の形式を、AEM プロジェクトで OSGi 設定を定義する開発者がよく理解できない可能性がある場合です。

>[!NOTE]
>
>AEM Web コンソールの設定 UI では、`.cfg.json` ファイルをリポジトリーに書き込みます。したがって、AEM プロジェクトで定義した OSGi 設定が、生成された設定と異なる可能性がある場合は、ローカル開発時に予期しない動作が発生するのを避けるために、このワークフローに注意してください。

1. AEM SDK Quickstart Jar の AEM webコンソール（`https://<host>:<port>/system/console`）にadmin ユーザーでログインする。
1. **OSGi**／**設定**&#x200B;に移動する。
1. 設定するには、OSGi コンポーネントを見つけて、編集するタイトルを選択します。
   ![OSGi 設定](./assets/configuring-osgi/configuration.png)
1. 必要に応じて Web UI を使用して OSGi 設定プロパティの値を編集します。
1. 永続 ID（PID）を安全な場所に記録します。これは後で OSGi 設定 JSON の生成に使用します。
1. 「保存」を選択します。
1. OSGi／OSGi インストーラー設定プリンターに移動します。
1. 手順 5 でコピーした PID に貼り付け、シリアル化形式が「OSGi Configurator JSON」に設定されていることを確認します。
1. 「印刷」を選択します。
1. JSON 形式の OSGi 設定は、「シリアライズされた設定プロパティ」セクションに表示されます。
   ![OSGi インストーラー設定プリンター](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. IDE で `ui.apps` プロジェクトを開き、新しい OSGi 設定が有効となる実行モードをターゲットに設定する config フォルダー（`/apps/.../config.<runmode>`）を探すか作成します。
1. この config フォルダーで、`<PID>.cfg.json` ファイルを作成します。PID は、手順 5 と同じ値です。
1. 手順 10 のシリアライズされた設定プロパティを `.cfg.json` ファイルに貼り付けます。
1. 変更を新しい `.cfg.json` ファイルに保存します。
1. 新しい追加 OSGi 構成ファイルを Git にコミットします。


## OSGi 構成プロパティの形式 {#osgi-configuration-property-formats}

### インライン値 {#inline-values}

インライン値は、標準の JSON 構文に従って、標準の名前と値のペアとして形式設定されます。例：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境固有の設定値 {#environment-specific-configuration-values}

OSGi 設定では、環境ごとに定義する変数にプレースホルダーを割り当てる必要があります。

```
use $[env:ENV_VAR_NAME]
```

顧客は、カスタムコードに関連する OSGi 設定プロパティに対してのみ、この手法を使用する必要があります。アドビ定義の OSGi 設定を上書きする場合は使用しないでください。

>[!NOTE]
>
>[repoinit ステートメント](/help/implementing/deploying/overview.md#repoinit)ではプレースホルダーを使用できません。

### シークレットの設定値 {#secret-configuration-values}

OSGi 設定では、環境ごとに定義するシークレットにプレースホルダーを割り当てる必要があります。

```
use $[secret:SECRET_VAR_NAME]
```

### 変数の命名 {#variable-naming}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

変数名は、次の規則に従う必要があります。

* 最小長：2
* 最大長：100
* 正規表現 `[a-zA-Z_][a-zA-Z_0-9]*` と一致する必要があります。

変数の値は 2048 文字を超えないようにします。

>[!CAUTION]
>
>変数名に特定のプレフィックスを使用することに関連するルールがあります。
>
>1. `INTERNAL_`、`ADOBE_` または `CONST_` のプレフィックスが付いた変数名は、アドビによって予約されています。これらのプレフィックスで始まる顧客設定変数は無視されます。
>
>1. お客様は、プレフィックスが `INTERNAL_` または `ADOBE_` の変数を参照しないでください。
>
>1. `AEM_` のプレフィックスが付いた環境変数は、お客様が使用および設定するパブリック API として製品で定義されています。
>   お客様はプレフィックスが `AEM_` で始まる環境変数を使用および設定できますが、このプレフィックスを使用して独自の変数を定義しないでください。

### デフォルト値 {#default-values}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

環境単位の値を設定しない場合、補間が行われないので、プレースホルダーは実行時に置き換えられず、配置されたままになります。これを回避するには、プレースホルダーの一部として次の構文でデフォルト値を指定します。

```
$[env:ENV_VAR_NAME;default=<value>]
```

デフォルト値を指定すると、プレースホルダーは、環境ごとの値（指定した場合）または指定したデフォルト値に置き換えられます。

### ローカル開発 {#local-development}

環境固有の設定値とシークレットの設定値の両方に次のことが適用されます。

変数は、実行時にローカル AEM によって取得されるように、ローカル環境で定義できます。例えば、Linux® の場合は次のようになります。

```bash
export ENV_VAR_NAME=my_value
```

設定で使用される環境変数を設定し、AEM を起動する前に実行する、単純な bash スクリプトを記述することをお勧めします。[https://direnv.net/](https://direnv.net/) などのツールを使うと、このアプローチを簡略化できます。すべてのユーザー間で共有できる場合は、値のタイプに応じて、値をソースコード管理にチェックインできることがあります。

シークレットの値はファイルから読み取られます。したがって、シークレットを使用するプレースホルダーごとに、シークレット値を含むテキストファイルを作成する必要があります。

例えば、`$[secret:server_password]` を使用する場合は、**server_password** という名前のテキストファイルを作成する必要があります。これらのシークレットファイルはすべて同じディレクトリに保存する必要があり、フレームワークプロパティ `org.apache.felix.configadmin.plugin.interpolation.secretsdir` は、そのローカルディレクトリを使用して設定する必要があります。

>[!CAUTION]
>
>テキストファイルにファイル拡張子は使用できません。
>
>上記の例では、テキストファイルの名前は **server_password** にする必要があります（ファイル拡張子は付けません）。

`org.apache.felix.configadmin.plugin.interpolation.secretsdir` は Sling フレームワークのプロパティです。そのため、このプロパティは felix コンソール（/system/console）では設定しませんが、システムの起動時に使用する sling.properties ファイルで設定します。このファイルは、抽出された Jar/install フォルダー（crx-quickstart/conf）の /conf サブディレクトリにあります。

例：「crx-quickstart/conf/sling.properties」ファイルの末尾に次の行を追加して、「crx-quickstart/secretsdir」をシークレットフォルダーとして設定します。

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### オーサーとパブリッシュの設定 {#author-vs-publish-configuration}

OSGi プロパティで、オーサーとパブリッシュで異なる値が必要な場合：

* [実行モードの解決](#runmode-resolution)のセクションで説明したように、`config.author` と `config.publish` の別個の OSGi フォルダーを使用する必要があります。
* 独立した変数名を作成する場合、次の 2 つのオプションを使用できます。
   * 最初のオプション（推奨）：異なる値を定義するように宣言されたすべての OSGI フォルダー（`config.author` と `config.publish` など）で、同じ変数名を使用します。例：
     `$[env:ENV_VAR_NAME;default=<value>]`：デフォルトは、その層（オーサーまたはパブリッシュ）のデフォルト値です。環境変数を [Cloud Manager API](#cloud-manager-api-format-for-setting-properties) またはクライアントを使用して設定する場合は、[Cloud Manager API リファレンスドキュメント](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)で説明されているように、「service」パラメーターを使用して層を区別します。「service」パラメーターは、変数の値を適切な OSGI 層にバインドします。「author」、「publish」、「preview」のいずれかです。
   * 2 つ目のオプション：`author_<samevariablename>` や `publish_<samevariablename>` などのプレフィックスを使用して個別の変数を宣言します。

### 設定例 {#configuration-examples}

以下の例では、ステージング環境と実稼働環境に加えて、3 つの開発環境があると仮定します。

**例 1**

OSGi プロパティ `my_var1` の値を、ステージング環境と実稼働環境では同じ値にしつつ、3 つの開発環境ではそれぞれ異なる値にします。

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

OSGi プロパティ `my_var1` の値をステージング環境、実稼働環境、3 つの開発環境でそれぞれ異なる値にします。したがって、開発環境ごとに `my_var1` の値を設定するには、Cloud Manager API を呼び出す必要があります。

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
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**例 3**

OSGi プロパティ `my_var1` の値をステージング環境、実稼働環境、1 つの開発環境では同じ値、他の 2 つの開発環境では異なる値にします。この場合は、ステージング環境および実稼働環境と同じ値にする必要がある開発環境も含め、Cloud Manager API を呼び出して各開発環境の `my_var1` の値を設定する必要があります。フォルダー **config** に設定された値は継承されません。

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
 "my_var1": "val1",
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

これを行う別の方法は、config.dev フォルダーの置き換えトークンのデフォルト値を、**config** フォルダーと同じ値に設定することです。

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
 "my_var1": "val1",
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
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

## プロパティ設定用の Cloud Manager API 形式 {#cloud-manager-api-format-for-setting-properties}

Cloud Manager API とその設定方法について詳しくは、[Adobe Developer web サイトの Adobe Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) を参照してください。

>[!NOTE]
>
>使用している Cloud Manager API に「デプロイメントマネージャー - Cloud Service」というロールが割り当てられていることを確認します。その他のロールでは、必ずしも以下のすべてのコマンドを実行できるわけではありません。

>[!TIP]
>
>また、Cloud Manager を使用して環境変数を設定できます。詳しくは、[Cloud Manager 環境変数](/help/implementing/cloud-manager/environment-variables.md)を参照してください。

### API を使用した値の設定 {#setting-values-via-api}

API を呼び出すと、一般的なカスタマーコードのデプロイメントパイプラインと同様に、新しい変数と値がクラウド環境にデプロイされます。オーサーサービスおよびパブリッシュサービスが再起動され、新しい値が参照されます（通常、数分かかります）。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```json
[
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
>デフォルトの変数は API 経由ではなく、OSGi プロパティ自体に設定されます。
>
>詳しくは、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) を参照してください。

### API を使用した値の取得 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

詳しくは、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) を参照してください。

### API を使用した値の削除 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

変数を削除するには、空の値を含めます。

詳しくは、[Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) を参照してください。

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
>Adobe I/O CLI の Cloud Manager プラグインを使用して値を設定する方法について詳しくは、[GitHub の aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) を参照してください。

### 変数の数 {#number-of-variables}

1 つの環境につき最大 200 個の変数を宣言できます。

## シークレットおよび環境固有の設定値のデプロイメントに関する考慮事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

シークレットと環境に固有の設定値は Git の外部に存在するので、Adobe Experience Manager as a Cloud Service の正式なデプロイメントメカニズムには含まれません。そのため、顧客が管理および統括し、Adobe Experience Manager as a Cloud Service のデプロイメントプロセスに統合する必要があります。

前述したように、API を呼び出すと、一般的なカスタマーコードのデプロイメントパイプラインと同様に、新しい変数と値がクラウド環境にデプロイされます。オーサーサービスおよびパブリッシュサービスが再起動され、新しい値が参照されます（通常、数分かかります）。通常のコードのデプロイメント中に Cloud Manager によって実行される品質ゲートおよびテストは、このプロセス中は実行されません。

通常、Cloud Manager で API を使用するコードをデプロイする前に、API を呼び出して環境変数を設定します。場合によっては、コードが既にデプロイされた後で既存の変数を変更する必要があります。

>[!NOTE]
>
>パイプラインが AEM の更新または顧客向けのデプロイメントで使用中の場合、その時点でエンドツーエンドパイプラインで実行されている部分によっては、API が正常に動作しない可能性があります。エラーの応答は、リクエストが成功しなかったことを示しますが、理由は示しません。

予定されている顧客コードのデプロイメントが、新しい値を持つ既存の変数に依存している場合があります。これは、現在のコードには適していません。これが問題となる場合は、変数の変更を追加方式で行うことをお勧めします。そのためには、古いコードが新しい値を参照しないように、古い変数の値を変更する代わりに、新しい変数名を作成します。後日、新しいカスタマーリリースが安定したら、古い値を削除できます。

同様に、変数の値はバージョン管理されないので、コードのロールバックによって、新しい値を参照することで問題を引き起こす場合があります。上記の変数追加方式戦略は、この場合にも役に立ちます。

このような変数の追加方式戦略は、数日前のコードを再デプロイする必要がある災害復旧シナリオにも役に立ちます。コードが参照する変数名と値は変わりません。これは、顧客が古い変数を削除する前に数日間待機するという手法に依存しています。この手法を使用していない場合、古いコードには参照できる適切な変数はありません。
