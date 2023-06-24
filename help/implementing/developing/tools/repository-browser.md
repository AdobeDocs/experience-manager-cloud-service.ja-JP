---
title: リポジトリーブラウザー
seo-title: Repository Browser
description: リポジトリーブラウザーは、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対して、リポジトリーへの読み取り専用ビューを提供します。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 56%

---

# リポジトリーブラウザー {#repository-browser}

>[!NOTE]
>
>リポジトリーブラウザーは、AEM バージョン 6582 以降で使用できます。

>[!INFO]
>
>また、[このクリップ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=ja)で、リポジトリーブラウザーを使用して AEM as a Cloud Service をデバッグする方法に関する概要ビデオをご覧ください。

## はじめに {#introduction}

リポジトリブラウザーは、オーサー層、パブリッシュ層、プレビュー層のすべての環境で、リポジトリに対する読み取り専用ビューを提供する開発者ツールです。 コンテンツ構造を見やすくし、コンテンツの表示やデバッグを容易にするように設計されています。

開発者コンソールからアクセスでき、選択した環境のオーサーインスタンスまたはパブリッシュインスタンスのリポジトリーを参照するために使用できます。

### アクセスのための前提条件 {#access-prerequisites}

開発者コンソールまたはリポジトリブラウザーにアクセスするには、次の条件を満たす必要があります

開発者コンソールにアクセスするには：

* 実稼動プログラムの場合、ユーザーは Admin Console で「**Cloud Manager - デベロッパーロール**」に割り当てられている必要があります。
* サンドボックスプログラムの場合、AEM as a Cloud Service へのアクセス権を付与する製品プロファイルを持つ任意のユーザーが使用できます。

リポジトリ・ブラウザにアクセスするには、次の手順に従います。

* オーサーインスタンスとパブリッシュインスタンスを表示するには、ユーザーは Admin Console で「**Cloud Manager - デベロッパーロール**」に割り当てられている必要があります。
* さらに、オーサー層の場合、「AEM ユーザー」製品プロファイルを持つユーザーは最小限の読み取りアクセス権でリポジトリーブラウザーを表示できます。ユーザーの権限は、リポジトリーを参照する際に考慮されます。「AEM 管理者」製品プロファイルを持つユーザーは、完全な読み取りアクセス権でリポジトリーブラウザーを表示できます。

ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html)を参照してください。

### リポジトリーブラウザーの起動 {#launching-the-repository-browser}

リポジトリーブラウザーは、次の手順に従って起動できます。

1. Cloud Manager で、目的の環境の横にある 3 ドットアイコンをクリックし、「**開発者コンソール**」を選択します。

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 次に、「**リポジトリーブラウザー**」タブをクリックします。
1. 作成者、公開、またはプレビューに対応するポッドを選択するには、 **ポッド** ドロップダウンリスト。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 次をクリックして、リポジトリブラウザーを起動します： **リポジトリブラウザを開く** リンクを下にします。 選択した層の代表インスタンス（ポッド）に対応するブラウザーが起動します。 起動されたその層の特定のポッドは制御できません。

## 機能 {#features}

### 階層のナビゲーション {#navigate-the-hierarchy}

左側のナビゲーションペインを使用して、コンテンツ階層間を移動できます。 各フォルダーまたはノードをクリックすると、その子が表示されます。 フォルダー構造には、JCR ノードツリーのスーパーセットである Sling リソースツリーが反映されています。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

または、以下に示すように、「**パス**」フィールドにパスを入力して、パスに直接移動することもできます。このパスは、左側のコンテンツ階層ビューでも場所を展開します。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

左側のフォルダーをクリックすると、「パス」フィールドにその場所が自動的に入力されます。 この機能は、後で使用するために値をコピー&amp;ペーストする場合に役立ちます。

また、フォルダーをクリックすると、そのフォルダーのパスが含まれるように URL が動的に変更されます。 この機能を使用すると、ブックマーク可能な URL を作成できます。

パブリッシュの場合、デフォルトでは、リポジトリブラウザーに公開コンテンツのみが表示されるので、 `/conf` または `/home` は表示されません。

これらの場所を表示するには、次の操作を行います。

1. 目的の環境の横にある 3 ドットアイコンをクリックし、「**アクセスを管理**」を選択します。

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. パブリッシュインスタンスを見つけて、クリックします。

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 公開管理者用の製品プロファイルを作成します。 以下の例では、**DEV - AEM Administrators Publish** という名前が付いています。

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. フルアクセス権でパブリッシュリポジトリーブラウザーをナビゲートできるユーザーに対応する適切なユーザーを新しい製品プロファイルに追加します。

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 数分待ってから、**AEM オーサー**&#x200B;コンソールを開きます。
1. 新しい製品プロファイルに対応するグループを管理者のグループのメンバーとして追加するには、次のボタンをクリックします。 **ツール/セキュリティ/作成者のグループ**&#x200B;をクリックし、 **管理者** グループ化します。 次に、以下に示すようにグループを追加します。

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. **administrators** グループと新しい **DEV - AEM Administrators Publish** グループをアクティブにして、パブリッシュインスタンスで使用できるようにします。

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. セキュリティを強化するため、新しい **DEV - AEM管理者公開** ～に関する管理者のグループからのグループ **作成者** したがって、新しいグループは公開用に分離されます

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. パブリッシュインスタンスのリポジトリーブラウザーにアクセスすると、`/home` や `/conf` などを含むすべてのフォルダーが表示されます。

### JCR プロパティの表示 {#view-jcr-properties}

ノードをクリックすると、ナビゲーションブラウザーの右側のウィンドウに JCR プロパティが表示されます。 以下は、`experience-fragments` ノードの例です。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### コンテンツを表示 {#view-content}

リポジトリブラウザーを使用して、コンテンツを表示できます。 ナビゲーションウィンドウでリソースをクリックすると、ブラウザーの右側で、各リソースの名前が付いたタブの下にプレビューが開きます。

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
