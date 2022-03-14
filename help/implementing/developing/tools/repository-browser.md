---
title: リポジトリブラウザ
seo-title: Repository Browser
description: リポジトリブラウザーは、オーサー層、パブリッシュ層、プレビュー層のすべての環境に対して、リポジトリへの読み取り専用ビューを提供します。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
source-git-commit: 76e28ca5628fb985df21f53d1c3e9898985dc736
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 3%

---


# リポジトリブラウザ {#repository-browser}

>[!NOTE]
>
>リポジトリブラウザーは、AEMバージョン 6582 以降で使用できます。

## はじめに {#introduction}

リポジトリブラウザーは、オーサー層、パブリッシュ層、プレビュー層のすべての環境で、リポジトリに対する読み取り専用ビューを提供する開発者ツールです。 コンテンツ構造を見やすく、またはデバッグしやすくするように設計されています。

開発者コンソールからアクセスでき、選択した環境のオーサーインスタンスまたはパブリッシュインスタンスのリポジトリを参照するために使用できます。

### アクセスの前提条件 {#access-prerequisites}

開発者コンソールまたはリポジトリブラウザーにアクセスするには、次の条件を満たす必要があります

開発者コンソールにアクセスするには：

* 実稼動プログラムの場合、ユーザーは **Cloud Manager — デベロッパーロール** Admin Console
* サンドボックスプログラムの場合、AEM as a Cloud Serviceへのアクセス権を付与する製品プロファイルを持つ任意のユーザーが使用できます。

リポジトリブラウザにアクセスするには：

* ユーザーは、 **Cloud Manager — 開発者** オーサーインスタンスとパブリッシュAdmin Consoleを表示するためのインスタンス内の役割。
* さらに、作成者の場合、AEM Users 製品プロファイルを持つユーザーは、最小限の読み取りアクセスでリポジトリブラウザーを表示できます。ユーザーの権限は、リポジトリを参照する際に考慮されます。 AEM Administrators 製品プロファイルを持つユーザーは、完全な読み取りアクセス権を持つリポジトリブラウザーを表示できます。

ユーザー権限の設定について詳しくは、 [Cloud Manager ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=ja).

### リポジトリブラウザの起動 {#launching-the-repository-browser}

リポジトリブラウザーは、次の手順に従って起動できます。

1. Cloud Manager で、目的の環境の横にある 3 つのドットをクリックし、「 」を選択します。 **開発者コンソール**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 次に、 **リポジトリブラウザ** タブ
1. 「 **ポッド** ドロップダウンリスト。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 次をクリックして、リポジトリブラウザーを起動します： **リポジトリブラウザを開く** リンクを下にします。 これにより、選択した層の代表インスタンス（ポッド）に対応するブラウザーが起動します。 これにより、選択した層の代表インスタンス（ポッド）に対応するブラウザーが起動します。 起動されたその層の特定のポッドは制御できないことに注意してください。

## 機能 {#features}

### 階層のナビゲート {#navigate-the-hierarchy}

左側のナビゲーションパネルを使用して、コンテンツ階層を移動できます。 各フォルダーまたはノードをクリックすると、その子が表示されます。 フォルダー構造には、JCR ノードツリーのスーパーセットである Sling リソースツリーが反映されます。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

公開の場合、デフォルトでは、リポジトリブラウザーには公開コンテンツのみが表示されます。したがって、次のような特定のフォルダーが存在します。 `/conf` または `/home` は表示されません。

これらの場所を表示するには、次の手順に従う必要があります。

1. 選択した環境の横にある 3 つのドットをクリックし、「 」を選択します。 **アクセスを管理**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. パブリッシュインスタンスを見つけて、クリックします。

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 公開管理者用の新しい製品プロファイルを作成します。 以下の例では、と呼ばれています。 **DEV - AEM管理者公開**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. フルアクセス権を持つパブリッシュリポジトリブラウザーをナビゲートできるユーザーに対応する適切なユーザーを、新しい製品プロファイルに追加します。

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 数分待ってから、 **AEM author** コンソール
1. 新しい製品プロファイルに対応するグループを、 administrators グループのメンバーとして追加します。 これを行うには、 **ツール/セキュリティ/作成者のグループ**&#x200B;をクリックし、 **管理者** グループ化します。 次に、以下に示すようにグループを追加します。

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. をアクティブにする **管理者** 新しい **DEV - AEM管理者公開** グループ化して、公開時に使用できるようにします。

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. セキュリティを強化するため、新しい **DEV - AEM管理者公開** グループを管理者グループから **作成者** したがって、新しいグループは公開用に分離されます

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. パブリッシュインスタンスのリポジトリブラウザーにアクセスすると、次を含むすべてのフォルダーが表示されます。 `/home` および `/conf`.

### JCR プロパティの表示 {#view-jcr-properties}

ノードをクリックすると、ナビゲーションブラウザーの右側のパネルに JCR プロパティが表示されます。 以下に、 `experience-fragments` ノード。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### コンテンツを表示 {#view-content}

リポジトリブラウザーを使用して、ナビゲーションペインでリソースをクリックして、コンテンツを表示できます。 これにより、ブラウザーの右側で、それぞれのリソースの名前が付いたタブの下にプレビューが開きます。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

現在、以下のリストの画像タイプでプレビューを使用できます。

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

また、次のテキストベースの MIME タイプの場合も同様です。

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### コンテンツをダウンロード {#download-content}

また、リポジトリブラウザーを使用してコンテンツをダウンロードすることもできます。 次の例では、 **ダウンロード** ダウンロードするためのリンク `jcr:data` 選択したノードに関連付けられています。 この機能は、プロパティ定義を含むノードに移動すると、すべてのバイナリプロパティで使用できます。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
