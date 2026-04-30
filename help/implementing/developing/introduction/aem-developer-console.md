---
title: AEM as a Cloud Service Developer Console - Beta
description: AEM as a Cloud Service Developer Consoleと、クラウド環境のデバッグ用の読み取り専用ツールについて説明します。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 15%

---


# AEM as a Cloud Service Developer Console（Beta） {#developer-console}

AEM as a Cloud Service Developer Consoleには、クラウド環境のデバッグ用の読み取り専用ツールのセットが含まれています。 Cloud Managerの環境ごとのリンクからアクセスでき、バンドル、OSGi設定、サービス、サーブレットなどを表示する機能を提供しています。

>[!NOTE]
>
>この記事では、現在ベータ版となっている AEM Cloud Service Developer Console の改良されたエクスペリエンスについて説明します。
>
>* 一部のユーザーは、現在のDeveloper Consoleの上部にあるボタンを使用して、新しいコンソールにアクセスできます。
>* Adobeでは、`aemcs-new-devconsole-ui-beta@adobe.com`さんに送信できるフィードバックを歓迎します。
>* 現在のAEM Developer Consoleに関するドキュメントについては、[この記事を参照してください。](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* AEM as a Cloud Service Developer Consoleは、同様の名前の&#x200B;[*Adobe Developer Console*.](https://developer.adobe.com/developer-console/)と混同しないでください。

>[!TIP]
>
>Developer Consoleは読み取り専用です。 SDKを使用してローカル開発に取り組んでおり、OSGi設定またはリポジトリコンテンツを変更する必要がある場合は、次を使用できます。
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

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

## 前提条件 {#prerequisites}

Developer Consoleには、特定のプログラムで特定の役割を持つユーザーのみがアクセスできます。

* 実稼動プログラムの場合、Adobe Admin Consoleの「Cloud Manager – 開発者ロール」によってDeveloper Consoleへのアクセスが制御されます。
* サンドボックスプログラムの場合、AEM へのアクセス権を付与する製品プロファイルを持つすべてのユーザーが Developer Console を使用できます。
* すべてのプログラムの場合、ステータスダンプとリポジトリブラウザーへのアクセスには「Cloud Manager - 開発者の役割」が必要です。

オーサーサービスとパブリッシュサービスの両方のデータを表示するには、両方のサービスで「AEM Users」または「AEM Administrators Product Profile」にユーザーを割り当てる必要があります。

ユーザー権限の設定について詳しくは、[Cloud Manager ドキュメントを参照してください。](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## 「OSGi バンドル」タブ {#osgi-bundles}

「**OSGi バンドル**」タブには、選択した環境にデプロイされたOSGi バンドルの概要が表示され、フルテキスト検索が提供されます。

Developer Consoleの![新しいOSGi バンドル画面](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* このタブには、書き出されたパッケージ、読み込まれたパッケージ、使用済みのサービスなど、環境内のバンドルの実際の状態に関する情報が表示されます。
* バンドルのステータスを確認して、バンドルが期待どおりに動作するかどうかを確認するのが理想的です。

**使用例：** バンドルの依存関係のバージョン範囲を指定するとします。 ただし、依存関係に問題があり、実際にバンドルで使用されている依存関係のバージョンを確認する必要があります。 確認するには、Developer Consoleを開き、**OSGi バンドル** タブのバンドル名をクリックしてバンドルの詳細にアクセスし、**バンドルの読み込み** アコーディオンを使用して、実行時に使用されているバンドルバージョンまたはパッケージバージョンを確認します。 この情報を使用して、Maven 依存関係のバージョン範囲やコードを調整できます。

## 「Java パッケージ」タブ {#java-packages}

**Java パッケージ** タブには、環境のOSGi システムでアクティブなパッケージを検索するための検索フィールドが用意されています。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)の「Java パッケージ」タブ

* パッケージを書き出す（または提供する）バンドルと、パッケージを読み込む（または使用する）バンドルを確認できます。
* また、場合によっては、問題を引き起こす可能性のある重複パッケージ（同じパッケージ、異なるバージョン）を確認することもできます。

**使用例：** [動的クラスローダー](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)を使用するカスタムサービスが、バージョンを指定せずにクラスを読み込むとします。 複数のバンドルが異なるバージョンを書き出すので、実装が異なり、動作が変わります。 機能モデルを分析せずに、環境内のどのパッケージにあるかを確認する必要があります。 このタブを使用すると、パッケージを検索して書き出したすべてのバージョンを表示し、より良いバージョン範囲を使用できます。

## 「設定」タブ {#configurations}

「**設定**」タブには、環境でアクティブな設定の検索可能なリストが表示されます。 クリックして詳細ページを表示すると、各設定で提供されるプロパティを確認できます。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/configurations-dev-console.png)の「設定」タブ

* **使用例：**&#x200B;指定した設定が実際に環境に存在することを確認するとします。 コンソールで「**設定**」タブを検索し、設定が見つからない場合は、機能モデル、設定実行モード、フォルダーを確認できます。

## 「サーブレット」タブ {#servlets}

「**サーブレット**」タブには、セレクターを使用したパスと、GETまたはPOSTを使用した拡張機能を指定できる検索フィールドがあります。 次に、Slingでリクエストを処理するサーブレットのリストを優先順に提供します。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)の「 サーブレット」タブ

**使用例：** リクエスト時にアクティブ化し、応答に出力を出力するOSGi サーブレットがあるとします。 ただし、期待される出力の代わりに、空の応答が返されます。 より特定のセレクター、`resourceType`、拡張機能、またはランキングにより、サーブレットよりも他のサーブレットが優先されているかどうかを確認する必要があります。 予想されるパスを検索すると、別のサーブレットがより高いランクでアクティブであることがわかります。 次に、例えばセレクターを追加して、サーブレットのランクを上げることができるかどうかを判断できます。

## 「サービス」タブ {#services}

「**サービス**」タブには、選択した環境に存在するサービスの概要が表示され、全文検索が提供されます。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/services-dev-console.png)の「 サービス」タブ

サービスをクリックして、その詳細を表示します。

## 「OSGi コンポーネント」タブ {#osgi-components}

「**OSGi コンポーネント**」タブには、選択した環境タイプに存在するOSGi コンポーネントの概要が表示され、フルテキスト検索が可能です。 環境内のOSGi コンポーネントのライブ状態と、それが満たすサービス、提供するバンドル、およびアクティベーションタイプ（即時または遅延）を確認できます。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)の「OSGi コンポーネント」タブ

* **ユースケースの例1:**&#x200B;設定でアクティブ化されたコンポーネントが、予期しない動作が発生したため、特定の環境でアクティブであるかどうかを確認する必要があるとします。 検索でコンポーネントを検索し、そのコンポーネントがアクティブかどうかを確認するだけです。
* **ユースケースの例2:** Adobe Experience Manager as a Cloud Serviceの詳細を知るために、環境内で使用できる標準のコンポーネントを確認し、サポートしているサービスを特定するとします。 コンポーネントリストでコンポーネントを確認できます。

## 「統合」タブ {#integrations}

「**統合**」タブでは、管理者がサービス資格情報と開発者トークンを生成、名前変更、削除できます。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)の「統合」タブ

## 「リポジトリ」タブ {#repository}

「**リポジトリ**」タブは、[&#x200B; リポジトリブラウザーを開きます。](/help/implementing/developing/tools/repository-browser.md)

## ステータスダンプ/クエリタブ {#status-dumps-queries}

「**ステータスダンプ / クエリ**」タブを使用すると、バンドル、パッケージ、設定、サービス、コンポーネント、Sling ジョブ、またはOak定義の現在の状態のフルテキストまたはJSON ダンプをダウンロードできます。

Developer Console UI![&#128279;](/help/implementing/developing/introduction/assets/status-dumps-queries.png)の「 ステータスダンプ / クエリ」タブ

[Query Performance ツールを開くこともできます。](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **使用例：**&#x200B;このタブは、予期しない状態が発生し、他の開発者に通知または文書化したい場合に特に便利です。 ダンプをダウンロードすることで、状態のスナップショットを取得し、後で参照できます。
