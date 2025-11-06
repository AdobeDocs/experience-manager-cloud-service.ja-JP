---
title: リポジトリーブラウザー
seo-title: Repository Browser
description: リポジトリーブラウザーは、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対して、リポジトリーへの読み取り専用ビューを提供します。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 100%

---

# リポジトリーブラウザー {#repository-browser}

>[!NOTE]
>
>リポジトリーブラウザーは、AEM バージョン 6582 以降で使用できます。

>[!INFO]
>
>また、[このクリップ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=ja)で、リポジトリーブラウザーを使用して AEM as a Cloud Service をデバッグする方法に関する概要ビデオをご覧ください。

## はじめに {#introduction}

リポジトリブラウザーは、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対してリポジトリへの読み取り専用ビューを提供する開発者ツールです。コンテンツの確認やデバッグを容易にするように、コンテンツ構造が見やすく設計されています。

[AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)からアクセスでき、選択した環境のオーサーインスタンスまたはパブリッシュインスタンスのリポジトリを参照するために使用できます。

### アクセスのための前提条件 {#access-prerequisites}

AEM as a Cloud Service Developer Console またはリポジトリブラウザーにアクセスするには、次の条件を満たす必要があります。

AEM as a Cloud Service Developer Console にアクセスするには、[Developer Console へのアクセス](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access)を参照してください。

リポジトリブラウザーにアクセスするための条件は、AEM as a Cloud Service Developer Console（上記で指定）の場合と同じです。特定のインスタンスのリポジトリブラウザーのコンテンツを表示するには：

* オーサーインスタンス：**オーサーインスタンス**&#x200B;の AEM ユーザー製品プロファイルを持つユーザーは、最小限の読み取りアクセス権でリポジトリブラウザーを表示できます。リポジトリを参照する際は、ユーザーの権限が適用されます。「AEM 管理者」製品プロファイルを持つユーザーは、完全な読み取りアクセス権でリポジトリブラウザーを表示できます。

* パブリッシュインスタンス：**パブリッシュインスタンス**&#x200B;の AEM ユーザー製品プロファイルを持つユーザーは、最小限の読み取りアクセス権でリポジトリブラウザーを表示できます。製品プロファイルを設定していない場合、ユーザーは匿名ユーザーとして移動することになり、権限が制限されるので、一部のパスが表示されません。

ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html?lang=ja)を参照してください。

### リポジトリーブラウザーの起動 {#launching-the-repository-browser}

リポジトリーブラウザーは、次の手順に従って起動できます。

1. Cloud Manager で、目的の環境の横にある 3 ドットアイコンをクリックし、「**開発者コンソール**」を選択します。

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 次に、「**リポジトリーブラウザー**」タブをクリックします。
1. 「**ポッド**」ドロップダウンリストをクリックして、オーサー、パブリッシュ、プレビューに対応する任意のポッドを選択します。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 下方の「**リポジトリブラウザーを開く**」リンクをクリックして、リポジトリブラウザーを起動します。選択した層の代表的なインスタンス（ポッド）に対応するブラウザーが起動します。起動されたその階層の特定のポッドは制御できません。

## 機能 {#features}

### 階層のナビゲーション {#navigate-the-hierarchy}

左側のナビゲーションパネルを使用して、コンテンツ階層内を移動できます。各フォルダーまたはノードをクリックすると、その子が表示されます。フォルダー構造には、JCR ノードツリーのスーパーセットである Sling リソースツリーが反映されています。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

または、以下に示すように、「**パス**」フィールドにパスを入力して、パスに直接移動することもできます。このパスにより、左側のコンテンツ階層表示での場所も拡張されます。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

左側のフォルダーをクリックすると、「パス」フィールドにその場所が自動的に入力されます。この機能は、後で使用するために値をコピーおよびペーストする場合に便利です。

また、フォルダーをクリックすると、そのパスがクリックしたフォルダーに含まれるように URL が動的に変更されます。この機能により、ブックマーク可能な URL が可能になります。

パブリッシュ層の場合、デフォルトでは、リポジトリブラウザーには公開コンテンツのみが表示されます。したがって、`/conf` や `/home` などの特定のフォルダーは表示されません。

これらの場所を表示するには、次の操作を実行します。

1. 目的の環境の横にある 3 ドットアイコンをクリックし、「**アクセスを管理**」を選択します。

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. パブリッシュインスタンスを見つけて、クリックします。

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. パブリッシュ管理者用の製品プロファイルを作成します。以下の例では、**DEV - AEM Administrators Publish** という名前が付いています。

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. フルアクセス権でパブリッシュリポジトリーブラウザーをナビゲートできるユーザーに対応する適切なユーザーを新しい製品プロファイルに追加します。

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 数分待ってから、**AEM オーサー**&#x200B;コンソールを開きます。
1. 新しい製品プロファイルに対応するグループを管理者のグループのメンバーとして追加するには、**ツール／セキュリティ／オーサー環境でのグループ**&#x200B;をクリックし、**管理者**&#x200B;グループをクリックします。次に、以下に示すようにグループを追加します。

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. **administrators** グループと新しい **DEV - AEM Administrators Publish** グループをアクティブにして、パブリッシュインスタンスで使用できるようにします。

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. よいセキュリティプラクティスとして、新しい **DEV - AEM Administrators Publish** グループを&#x200B;**オーサー**&#x200B;環境の管理者のグループから削除して、新しいグループがパブリッシュ環境から分離されるようにします。

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. パブリッシュインスタンスのリポジトリーブラウザーにアクセスすると、`/home` や `/conf` などを含むすべてのフォルダーが表示されます。

### JCR プロパティの表示 {#view-jcr-properties}

ノードをクリックすると、ナビゲーションブラウザーの右側のウィンドウに JCR プロパティが表示されます。以下は、`experience-fragments` ノードの例です。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### コンテンツを表示 {#view-content}

リポジトリブラウザーを使用して、コンテンツを表示できます。ナビゲーションウィンドウでリソースをクリックすると、ブラウザーの右側で、各リソースの名前が付いたタブの下にプレビューが開きます。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

プレビューは、次の画像タイプで使用できます。

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

また、次のテキストベースの MIME タイプの場合もプレビューを使用できます。

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### コンテンツのダウンロード {#download-content}

リポジトリーブラウザーを使用して、コンテンツをダウンロードすることもできます。次の例では、「**ダウンロード**」リンクをクリックして、選択したノードに関連する `jcr:data` をダウンロードできます。この機能は、プロパティ定義を含んだノードに移動することで、すべてのバイナリプロパティで使用できます。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
