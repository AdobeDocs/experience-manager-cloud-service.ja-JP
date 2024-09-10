---
title: AEM as a Cloud ServiceDeveloper Console（Beta）
description: CRX/DE Lite とAEM as a Cloud Service Developer Consoleについて
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ea631743af99879d2a76d3a4a78ecf5883f39c69
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 27%

---


# AEM as a Cloud ServiceDeveloper Console（Beta） {#developer-console}

>[!NOTE]
>
>この記事では、AEM Cloud Service Developer Consoleの機能強化について説明します。現在はベータ版であり、一部のお客様はクラシック UI の上部にあるボタンをクリックして使用できます。 ご意見をお寄せください `aemcs-new-devconsole-ui-beta@adobe.com`。 従来のAEM Developer Consoleについては、[ この記事 ](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) を参照してください。

## AEM as a Cloud Service の開発ツール {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>AEM as a Cloud Service Developer Console を、同様の名前の [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) と混同しないでください。
>

ユーザーはオーサー層の開発環境では CRXDE Lite にアクセスできますが、ステージ環境や実稼動環境ではアクセスできません。不変リポジトリー（`/libs`、`/apps`）に実行時に書き込むことはできないので、書き込もうとするとエラーが発生します。

代わりに、AEM as a Cloud Service Developer Console からリポジトリブラウザーを起動して、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対してリポジトリへの読み取り専用ビューを提供できます。詳しくは、[リポジトリブラウザー](/help/implementing/developing/tools/repository-browser.md)を参照してください。

AEM as a Cloud Service 開発者環境をデバッグするための一連のツールは、RDE 環境、開発環境、ステージ環境、実稼動環境の AEM as a Cloud Service Developer Console で利用できます。URL は、次のようにオーサーサービス URL またはパブリッシュサービス URL を調整して決定できます。

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

ショートカットとして、次の Cloud Manager CLI コマンドを使用して、下記の環境パラメーターに基づいて AEM as a Cloud Service Developer Console を起動できます。

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

詳しくは、[リリース情報](/help/release-notes/home.md)を参照してください。

開発者は、ステータス情報を生成し、様々なリソースを解決できます。

下図に示すように、使用可能なステータス情報には、バンドルの状態、コンポーネント、OSGi 設定、Oak インデックス、OSGi サービス、Sling ジョブなどがあります。

### OSGi バンドル {#osgi-bundles}

![ 開発コンソールの新しい OSGi バンドル画面 ](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* これにより、選択した環境タイプにデプロイされている OSGi バンドルの概要が生成されます。 全文検索が可能になります。
* 環境内のバンドルの実際の状態を取得すると便利です。 書き出されたパッケージ、読み込まれたパッケージ、使用されたサービスなどの情報を取得できます。
* 開発者は、実際の環境でを検証し、バンドルが期待どおりに動作するかどうかを確認します。
* **ユースケースの例：** 依存関係のバージョン範囲がバンドルで指定される。 依存関係で問題が発生しています。 バンドルにワイヤリングされている依存関係のバージョンを確認します。 これを確認するには、バンドルの詳細に移動し、バンドルまたはパッケージの読み込みを使用して、実行時にどのバンドルバージョンまたはパッケージバージョンが使用されているかを確認します。 この情報を使用して、Maven 依存関係のバージョン範囲を調整したり、コードを調整したりできます。

### Java パッケージ {#java-packages}

![ 開発コンソール UI の「Java パッケージ」タブ ](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* これにより、環境の OSGI システムでアクティブなパッケージを検索するために使用できる検索プロンプトが表示されます。 この場所には、パッケージを書き出す（または提供する）バンドルと、パッケージを読み込む（または使用する）バンドルが表示されます。 パッケージの重複（同じパッケージ、異なるバージョン）をチェックすることもできます。これにより、問題が発生する場合があります。
* **ユースケースの例**[ 動的クラスローダー ](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) を使用しているカスタムサービスが、バージョンを指定せずにクラスを読み込んでいる。これは、異なるバージョンの複数のバンドルによって書き出され、実装が異なり、動作が変更される。 開発者は、機能モデルを分析せずに環境に存在するパッケージを確認したいので、このパッケージを検索して、書き出されるすべてのバージョンを確認します。 これにより、より良いバージョン範囲を入力するための情報が提供されます。

### サーブレット {#servlets}

![ 開発コンソール UI の「サーブレット」タブ ](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* これにより、セレクターを使用してパスを指定し、GETまたはPOSTで拡張子を指定できる検索プロンプトが表示されます。 次に、Sling でリクエストを処理する優先順位の高いサーブレットの結果を提供します。
* **ユースケースの例：** リクエスト時にアクティブ化し、応答に何かを出力する必要がある OSGI サーブレットがありますが、代わりに空の応答が返されます。 より具体的なセレクター、`resourceType`、拡張機能またはランキングが原因で、サーブレットよりも他のサーブレットが優先されているかどうかを確認する必要があります。 期待されるパスを検索し、別のサーブレットがアクティブで、よりランクの高いことがわかります。 次に、例えばセレクターを追加して、上記のランクのサーブレットを取得できるかどうかを決定します。

### サービス {#services}

![ 開発コンソール UI の「サービス」タブ ](/help/implementing/developing/introduction/assets/services-dev-console.png)

* OSGI コンポーネントビューに似ていますが、サービスに基づいています。 特定のプロパティが設定されているサービスをすばやく検索できます。

### OSGi コンポーネント {#osgi-components}

![ 開発コンソール UI の「OSGi コンポーネント」タブ ](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 選択した環境タイプに存在する OSGI コンポーネントの概要が生成されます。 全文検索が可能になります。
* OSGI コンポーネントのライブ状態は、環境で取得できます。 サービスが満たすサービス、サービスを提供するバンドルおよびアクティベーションタイプ（即時または遅延）を確認できます。
* **使用例 1:** 開発者は、期待する動作を取得していないので、設定でアクティブ化されたコンポーネントが特定の環境でアクティブになっているかどうかを確認します。 検索でコンポーネントを参照し、そのコンポーネントがアクティブかどうかを確認するだけです。
* **ユースケース 2:** 例Adobe Experience Manager as a Cloud Serviceについて詳しくは、どの標準搭載コンポーネントが環境に存在し、どのサービスを満たしているかを確認したい場合。 これらは、コンポーネントリストでチェックアウトできます。

### 統合 {#integrations}

![ 開発コンソール UI の「統合」タブ ](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 管理者は、サービス資格情報と開発者トークンを生成、名前変更、削除できます。

### リポジトリ {#repository}

* [ リポジトリブラウザー ](/help/implementing/developing/tools/repository-browser.md) を開きます。

### ステータスダンプ/クエリ {#status-dumps-queries}

![ 開発コンソール UI の「ステータスダンプ/クエリ」タブ ](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* バンドル、パッケージ、設定、サービス、コンポーネント、Sling ジョブまたは Oak 定義の現在の状態のフルテキストまたは JSON ダンプを提供します。
* これは、特に開発者が予期しない状態を発見し、他の開発者に対してこれを伝えたり、ドキュメント化したりする場合に役立ちます。 ダンプをダウンロードすると、後で参照できるように、状態のスナップショットが表示されます。

### 設定 {#configurations}

![ 開発コンソール UI の「設定」タブ ](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* これにより、その環境でアクティブな設定の検索可能なリストが表示されます。 設定で提供されているプロパティを確認するには、詳細ページをチェックアウトします。
* **ユースケースの例：** 指定した設定が実際に環境に存在することを確認したい場合。 設定が不足している場合は、機能モデルや設定実行モードまたはフォルダーを確認できます。

実稼働プログラムの場合、AEM as a Cloud Service Developer Console へのアクセスは Adobe Admin Console の「Cloud Manager - 開発者の役割」で定義されます。一方、サンドボックスプログラムの場合、AEM as a Cloud Service Developer Console は、AEM as a Cloud Service へのアクセス権を付与する製品プロファイルを持つすべてのユーザーが利用できます。すべてのプログラムで、ステータスダンプとリポジトリブラウザーには「Cloud Manager - デベロッパーの役割」が必要です。また、オーサーサービスとパブリッシュサービスの両方のサービスからデータを表示するには、両方のサービスで AEM ユーザーまたはAEM 管理者製品プロファイルでもユーザーが定義されている必要があります。ユーザー権限の設定について詳しくは、 [Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja) を参照してください。