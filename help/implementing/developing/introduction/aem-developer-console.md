---
title: AEM as a Cloud Service Developer Console - Beta
description: CRXDE Lite と AEM as a Cloud Service Developer Console について説明します。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 100%

---

# AEM as a Cloud Service Developer Console（Beta） {#developer-console}

>[!NOTE]
>
>この記事では、現在ベータ版となっている AEM Cloud Service Developer Console の改良されたエクスペリエンスについて説明します。一部の顧客は、クラシック UI の上部にあるボタンをクリックしてアクセスできます。アドビでは、皆様からのフィードバックを `aemcs-new-devconsole-ui-beta@adobe.com` までお送りいただければ幸いです。従来の AEM Developer Console について詳しくは、[この記事](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)を参照してください。

AEM as a Cloud Service Developer Console には、クラウド環境でデバッグするツールセットが含まれます。Cloud Manager の環境ごとのリンクからアクセスできます。

>[!NOTE]
>AEM as a Cloud Service Developer Console を、同様の名前の [*Adobe Developer Console*](https://developer.adobe.com/developer-console/) と混同しないでください。
>


<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

開発者は、以下に説明する機能にアクセスできます。

## OSGi バンドル {#osgi-bundles}

![Developer Console の新しい OSGi バンドル画面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 選択した環境タイプにデプロイされている OSGI バンドルの概要。全文検索が可能です。
* 環境内のバンドルの実際の状態に関する情報を取得するのに役立ちます。書き出されたパッケージ、読み込まれたパッケージ、使用されたサービスなどの情報を取得できます。
* 開発者は、実際の環境で検証し、バンドルが期待どおりに動作するかどうかを確認したいと考えています。
* **ユースケースの例：**&#x200B;バンドル内で依存関係のバージョン範囲が指定されています。依存関係に問題が発生しています。バンドルに紐付けられている依存関係のバージョンを確認したいとします。確認するには、バンドルの詳細に移動し、「バンドル／パッケージを読み込み」を使用して、実行時に使用されているバンドルバージョンまたはパッケージバージョンを確認します。この情報を使用して、Maven 依存関係のバージョン範囲やコードを調整できます。

## Java パッケージ {#java-packages}

![Developer Console UI の「Java パッケージ」タブ](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 環境の OSGi システムでアクティブなパッケージを検索するための検索プロンプト。この場所では、どのバンドルがパッケージを書き出す（または提供する）バンドルと、パッケージを読み込む（または使用する）バンドルを確認できます。また、場合によっては、問題を引き起こす可能性のある重複パッケージ（同じパッケージ、異なるバージョン）を確認することもできます。
* **ユースケースの例：**[動的クラスローダー](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)を使用するカスタムサービスが、バージョンを指定せずにクラスを読み込みます。複数のバンドルが異なるバージョンを書き出すので、実装が異なり、動作が変わります。開発者は、機能モデルを分析することなく、環境内のパッケージを確認したいと考えています。パッケージを検索し、書き出されたすべてのバージョンを確認します。この機能により、より適切なバージョン範囲を入力するための情報が得られます。

## サーブレット {#servlets}

![Developer Console UI の「サーブレット」タブ](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* セレクターでパスを指定し、GET または POST で拡張子を指定できる検索プロンプト。次に、Sling でリクエストを処理するサーブレットの結果を、優先順位に従って表示します。
* **ユースケースの例：**&#x200B;リクエストに応じてアクティブ化し、応答に出力を印刷する OSGi サーブレットがあります。ただし、期待される出力ではなく、応答では空を返します。より具体的なセレクター、`resourceType`、拡張機能またはランキングにより、他のサーブレットが自分のサーブレットよりも優先されていないか確認する必要があります。期待されるパスを検索すると、より高いランクでアクティブになっている別のサーブレットが見つかります。次に、セレクターを追加するなどして、自分のサーブレットを上位ランクにできるかどうかを判断します。

## サービス {#services}

![Developer Console UI の「サービス」タブ](/help/implementing/developing/introduction/assets/services-dev-console.png)

* OSGi コンポーネントビューに類似していますが、サービスに基づいています。特定のプロパティで指定されているサービスを簡単に検索できます。

## OSGi のコンポーネント {#osgi-components}

![Developer Console UI の「OSGi コンポーネント」タブ](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 選択した環境タイプに存在するOSGi コンポーネントの概要。全文検索が可能です。
* 環境内の OSGi コンポーネントのライブ状態を取得できます。コンポーネントが満たすサービス、コンポーネントを提供するバンドル、アクティブ化タイプ（即時または遅延）を確認できます。
* **ユースケースの例 1：**&#x200B;開発者として、設定でアクティブ化されたコンポーネントが特定の環境でアクティブかどうかを確認する必要があります。その理由は、期待される動作が発生していないからです。検索でコンポーネントを検索し、そのコンポーネントがアクティブかどうかを確認するだけです。
* **ユースケースの例 2：**&#x200B;環境で使用可能な標準コンポーネントを確認し、そのコンポーネントがサポートするサービスを特定したいと考えています。この機能は、Adobe Experience Manager as a Cloud Service について詳しく理解するのに役立ちます。これらは、コンポーネントリストでチェックアウトできます。

## 統合 {#integrations}

![Developer Console UI の「統合」タブ](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 管理者は、サービス資格情報と開発者トークンを生成、名前変更、削除する権限を持ちます。

## リポジトリ {#repository}

* [リポジトリブラウザー](/help/implementing/developing/tools/repository-browser.md)を開きます。

## ステータスダンプ／クエリ {#status-dumps-queries}

![Developer Console UI の「ステータスダンプ／クエリ」タブ](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* バンドル、パッケージ、設定、サービス、コンポーネント、Sling ジョブまたは Oak 定義の現在の状態の完全なテキストまたは JSON ダンプ。
* 特に、開発者が予期せぬ状態を発見し、その状態を他の開発者に通信したり、文書化したりしたい場合に役立ちます。ダンプをダウンロードすることで、状態のスナップショットを取得し、後で参照できます。

## 設定 {#configurations}

![Developer Console UI の「設定」タブ ](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 環境内でアクティブな設定の検索可能なリスト。詳細ページをチェックアウトすることで、設定で提供されるプロパティを確認できます。
* **ユースケースの例：**&#x200B;開発者は、指定した設定が環境に実際に存在するかどうかを確認したいと考えています。設定が不足している場合は、機能モデル、設定の実行モードまたはフォルダーを確認できます。

実稼動プログラムの場合、Adobe Admin Console の「Cloud Manager - 開発者の役割」が AEM as a Cloud Service Developer Console へのアクセスを制御します。 サンドボックスプログラムの場合、AEM へのアクセス権を付与する製品プロファイルを持つすべてのユーザーが Developer Console を使用できます。すべてのプログラムの場合、ステータスダンプとリポジトリブラウザーへのアクセスには「Cloud Manager - 開発者の役割」が必要です。 オーサーサービスとパブリッシュサービスの両方のデータを表示するには、両方のサービスでユーザーが AEM ユーザーまたは AEM 管理者の製品プロファイルに割り当てられている必要もあります。

ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)を参照してください。

