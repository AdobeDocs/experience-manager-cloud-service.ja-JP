---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: CRXDE LiteとAEM as a Cloud Service Developer Consoleについて説明します。
feature: Developing
role: Admin, Architect, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 11c52f6782df3b608bedd4b120c145a7a80a0702
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 4%

---

# AEM as a Cloud Service Developer Console（Beta） {#developer-console}

>[!NOTE]
>
>この記事では、ベータ版になった AEM Cloud Service Developer Consoleの機能強化について説明します。 一部のお客様は、クラシック UI の上部にあるボタンをクリックしてアクセスできます。 Adobeから `aemcs-new-devconsole-ui-beta@adobe.com` へのフィードバックをお待ちしています。 従来のAEM Developer Consoleについては、[ この記事 ](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) を参照してください。

AEM as a Cloud Service Developer Consoleには、クラウド環境でデバッグするための一連のツールが含まれています。 Cloud Managerの環境ごとのリンクからアクセスできます。

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

![ 開発コンソールの新しい OSGi バンドル画面 ](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 選択した環境タイプでデプロイされている OSGi バンドルの概要です。 全文検索が可能になります。
* 環境内のバンドルの実際の状態に関する情報を取得すると便利です。 書き出されたパッケージ、読み込まれたパッケージ、使用されたサービスなどの情報を取得できます。
* 開発者は、実際の環境でを検証し、バンドルが期待どおりに動作するかどうかを確認します。
* **ユースケースの例：** 依存関係のバージョン範囲がバンドルで指定される。 依存関係で問題が発生しています。 バンドルにワイヤリングされている依存関係のバージョンを確認します。 確認するには、バンドルの詳細に移動し、バンドル/パッケージの読み込みを使用して、実行時に使用されているバンドルのバージョンまたはパッケージバージョンを確認します。 この情報を使用して、Maven 依存関係のバージョン範囲を調整したり、コードを調整したりできます。

## Java パッケージ {#java-packages}

![ 開発コンソール UI の「Java パッケージ」タブ ](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 環境の OSGI システムでアクティブなパッケージを検索するために使用できる検索プロンプト。 この場所には、パッケージを書き出す（または提供する）バンドルと、パッケージを読み込む（または使用する）バンドルが表示されます。 パッケージの重複（同じパッケージ、異なるバージョン）をチェックすることもできます。これにより、問題が発生する場合があります。
* **ユースケースの例：**&#x200B;[ 動的クラスローダー ](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) を使用するカスタムサービスが、バージョンを指定せずにクラスを読み込む。 複数のバンドルが異なるバージョンを書き出すので、実装が異なり、動作が変更されます。 開発者は、機能モデルを分析せずに、環境内にどのパッケージがあるかを確認したいと考えています。 パッケージを検索し、書き出されたすべてのバージョンを表示します。 この機能により、より良いバージョン範囲を入力するための情報が提供されます。

## サーブレット {#servlets}

![ 開発コンソール UI の「サーブレット」タブ ](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* セレクターでパスを、GETまたは POST で拡張子を指定できる検索プロンプト。 次に、Sling でリクエストを処理する優先順位に従ってサーブレットの結果が提供されます。
* **ユースケースの例：** 要求時にアクティブ化し、出力を応答に出力する OSGI サーブレットがある。 ただし、期待される出力ではなく、応答は空を返します。 より具体的なセレクター、`resourceType`、拡張機能またはランキングが原因で、サーブレットよりも他のサーブレットが優先されているかどうかを確認する必要があります。 期待されるパスを検索し、別のサーブレットがアクティブで、よりランクの高いことがわかります。 次に、例えばセレクターを追加して、上記のランクのサーブレットを取得できるかどうかを決定します。

## サービス {#services}

![ 開発コンソール UI の「サービス」タブ ](/help/implementing/developing/introduction/assets/services-dev-console.png)

* OSGI コンポーネントビューに似ていますが、サービスに基づいています。 特定のプロパティが設定されているサービスをすばやく検索できます。

## OSGi コンポーネント {#osgi-components}

![ 開発コンソール UI の「OSGi コンポーネント」タブ ](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 選択した環境タイプに存在する OSGi コンポーネントの概要です。 全文検索が可能になります。
* OSGI コンポーネントのライブ状態は、環境で取得できます。 サービスが満たすサービス、サービスを提供するバンドルおよびアクティベーションタイプ（即時または遅延）を確認できます。
* **使用例 1:** 開発者は、設定を使用してアクティブ化されたコンポーネントが特定の環境でアクティブかどうかを確認する必要があります。 これは、想定される動作が行われていないからです。 検索でコンポーネントを検索するだけで、そのコンポーネントがアクティブかどうかを確認できます。
* **使用例 2:** 環境で使用可能な標準搭載コンポーネントを確認し、そのコンポーネントがサポートするサービスを特定します。 この機能は、Adobe Experience Manager as a Cloud Serviceの詳細を理解するのに役立ちます。 これらは、コンポーネントリストでチェックアウトできます。

## 統合 {#integrations}

![ 開発コンソール UI の「統合」タブ ](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 管理者は、サービス資格情報と開発者トークンを生成、名前変更、削除する機能を持っています。

## リポジトリ {#repository}

* [ リポジトリブラウザー ](/help/implementing/developing/tools/repository-browser.md) を開きます。

## ステータスダンプ/クエリ {#status-dumps-queries}

![ 開発コンソール UI の「ステータスダンプ/クエリ」タブ ](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* バンドル、パッケージ、設定、サービス、コンポーネント、Sling ジョブまたはOak定義の現在のステータスのフルテキストまたは JSON ダンプ。
* 特に、デベロッパーが予期しない状態を発見し、他のデベロッパーに対してこの状態を通信またはドキュメント化したい場合に役立ちます。 ダンプをダウンロードすると、後で参照できるように、状態のスナップショットが表示されます。

## 設定 {#configurations}

![ 開発コンソール UI の「設定」タブ ](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 環境内でアクティブな設定の検索可能なリスト。 設定で提供されているプロパティを確認するには、詳細ページをチェックアウトします。
* **ユースケースの例：** 指定した設定が実際に環境に存在することを確認したい場合。 設定が不足している場合は、機能モデルまたは設定実行モードまたはフォルダーを確認できます。

実稼動プログラムの場合、Adobe Admin Consoleの「Cloud Manager – 開発者ロール」がAEM as a Cloud Service Developer Consoleへのアクセスを制御します。 サンドボックスプログラムの場合、AEM アクセス権を付与する製品プロファイルを持つすべてのユーザーがDeveloper Consoleを使用できます。 すべてのプログラムで、ステータスダンプとリポジトリブラウザーへのアクセスに「Cloud Manager - デベロッパーロール」が必要です。 オーサーサービスとパブリッシュサービスの両方のデータを表示するには、ユーザーを両方のサービスの「AEM ユーザー」または「AEM管理者」製品プロファイルに割り当てる必要もあります。

ユーザー権限の設定について詳しくは、 [Cloud Manager のドキュメント](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles) を参照してください。

