---
title: リポジトリーブラウザー
seo-title: Repository Browser
description: リポジトリーブラウザーは、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対して、リポジトリーへの読み取り専用ビューを提供します。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 46d8d78bd14f6e311d62266aa19825f82f82030d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 90%

---

# リポジトリーブラウザー {#repository-browser}

>[!NOTE]
>
>リポジトリーブラウザーは、AEM バージョン 6582 以降で使用できます。

>[!INFO]
>
>また、[このクリップ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=ja)で、リポジトリーブラウザーを使用して AEM as a Cloud Service をデバッグする方法に関する概要ビデオをご覧ください。

## はじめに {#introduction}

リポジトリーブラウザーは、オーサー層、パブリッシュ層およびプレビュー層でのすべての環境に対してリポジトリーへの読み取り専用ビューを提供する開発者ツールです。コンテンツ構造が見やすくなるように、またデバッグしやすくなるように設計されています。

開発者コンソールからアクセスでき、選択した環境のオーサーインスタンスまたはパブリッシュインスタンスのリポジトリーを参照するために使用できます。

### アクセスのための前提条件 {#access-prerequisites}

開発者コンソールまたはリポジトリーブラウザーにアクセスするには、次の条件を満たす必要があります。

開発者コンソールにアクセスするには：

* 実稼動プログラムの場合、ユーザーは Admin Console で「**Cloud Manager - デベロッパーロール**」に割り当てられている必要があります。
* サンドボックスプログラムの場合、AEM as a Cloud Service へのアクセス権を付与する製品プロファイルを持つ任意のユーザーが使用できます。

リポジトリーブラウザーにアクセスするには：

* オーサーインスタンスとパブリッシュインスタンスを表示するには、ユーザーは Admin Console で「**Cloud Manager - デベロッパーロール**」に割り当てられている必要があります。
* さらに、オーサー層の場合、「AEM ユーザー」製品プロファイルを持つユーザーは最小限の読み取りアクセス権でリポジトリーブラウザーを表示できます。ユーザーの権限は、リポジトリーを参照する際に考慮されます。「AEM 管理者」製品プロファイルを持つユーザーは、完全な読み取りアクセス権でリポジトリーブラウザーを表示できます。

ユーザー権限の設定について詳しくは、[Cloud Manager のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja)を参照してください。

### リポジトリーブラウザーの起動 {#launching-the-repository-browser}

リポジトリーブラウザーは、次の手順に従って起動できます。

1. Cloud Manager で、目的の環境の横にある 3 ドットアイコンをクリックし、「**開発者コンソール**」を選択します。

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 次に、「**リポジトリーブラウザー**」タブをクリックします。
1. 「**ポッド**」ドロップダウンリストをクリックして、オーサー層、パブリッシュ層、プレビュー層のいずれかに対応する任意のポッドを選択します。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 下方の「**リポジトリーブラウザーを開く**」リンクをクリックして、リポジトリーブラウザーを起動します。これで、選択した階層の代表的なインスタンス（ポッド）に対応するブラウザーが起動します。これで、選択した階層の代表的なインスタンス（ポッド）に対応するブラウザーが起動します。その階層の特定のポッドは起動後は制御できないことに注意してください。

## 機能 {#features}

### 階層のナビゲーション {#navigate-the-hierarchy}

左側のナビゲーションパネルを使用して、コンテンツ階層内を移動できます。各フォルダーまたはノードをクリックすると、そのフォルダーまたはノードの子が表示されます。フォルダー構造には、JCR ノードツリーのスーパーセットである Sling リソースツリーが反映されています。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

または、 **パス** フィールドに含まれる値を指定します。 これにより、左側のコンテンツ階層ビューでの場所も展開されます。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

左側のフォルダーをクリックするたびに、「パス」フィールドにその場所が自動的に入力されます。 これは、後で使用するために値をコピー&amp;ペーストする場合に便利です。

さらに、フォルダーをクリックすると、そのフォルダーのパスが含まれるように URL が動的に変更されます。 これにより、ブックマーク可能な URL を作成できます。

パブリッシュ層の場合、デフォルトでは、リポジトリーブラウザーには公開コンテンツのみが表示されます。したがって、`/conf` や `/home` などの特定のフォルダーは表示されません。

これらの場所を表示するには、次の手順に従う必要があります。

1. 目的の環境の横にある 3 ドットアイコンをクリックし、「**アクセスを管理**」を選択します。

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. パブリッシュインスタンスを見つけて、クリックします。

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. パブリッシュインスタンス管理者用の新しい製品プロファイルを作成します。以下の例では、**DEV - AEM Administrators Publish** という名前が付いています。

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. フルアクセス権でパブリッシュリポジトリーブラウザーをナビゲートできるユーザーに対応する適切なユーザーを新しい製品プロファイルに追加します。

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 数分待ってから、**AEM オーサー**&#x200B;コンソールを開きます。
1. 新しい製品プロファイルに対応するグループを、administrators グループのメンバーとして追加します。それには、オーサーインスタンスで&#x200B;**ツール／セキュリティ／グループ**&#x200B;を選択したあと、**administrators** グループをクリックします。次に、以下に示すようにグループを追加します。

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. **administrators** グループと新しい **DEV - AEM Administrators Publish** グループをアクティブにして、パブリッシュインスタンスで使用できるようにします。

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. セキュリティを強化するため、新しい **DEV - AEM Administrators Publish** グループを&#x200B;**オーサー**&#x200B;インスタンス上の administrators グループから削除して、新しいグループがパブリッシュインスタンス専用になるようにします。

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. パブリッシュインスタンスのリポジトリーブラウザーにアクセスすると、`/home` や `/conf` などを含むすべてのフォルダーが表示されます。

### JCR プロパティの表示 {#view-jcr-properties}

ノードをクリックすると、ナビゲーションブラウザーの右側のパネルに JCR プロパティが表示されます。以下は、`experience-fragments` ノードの例です。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### コンテンツを表示 {#view-content}

リポジトリーブラウザーを使用すると、ナビゲーションペインでリソースをクリックしてコンテンツを表示できます。これにより、ブラウザーの右側で、それぞれのリソースの名前が付いたタブにプレビューが開きます。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

現時点では、以下のリストに含まれる画像タイプでプレビューを使用できます。

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
