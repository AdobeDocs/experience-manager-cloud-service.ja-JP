---
title: 設定と設定ブラウザー
description: Adobe Experience Manager(AEM) の設定と、AEMでの Workspace 設定の管理方法について説明します。
exl-id: 0ade04df-03a9-4976-a4b7-c01b4748474d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 55%

---

# 設定と設定ブラウザー {#configuration-browser}

Adobe Experience Manager(AEM) の設定は、AEMの設定を管理し、ワークスペースとして機能します。

## 設定とは  {#what-is-a-configuration}

設定には、2 つの異なる観点があります。

* [管理者](#configurations-administrator)は、設定グループを定義および管理するために、AEM 内のワークスペースとして AEM の設定を使用します。
* [デベロッパー](#configurations-developer)は、AEM の設定を保持および参照するための設定を実装する基本的な設定メカニズムを使用します。

まとめ：管理者の観点からの設定とは、AEM で設定を管理するワークスペースの作成方法を指します。一方、デベロッパーは、AEM がリポジトリー内でこれらの設定を使用および管理する方法を理解する必要があります。

設定は、上記の観点に関係なく、AEM で 2 つの主な目的を果たします。

* 設定により、特定のユーザーグループに対して特定の機能が有効になります。
* 設定によって、これらの機能のアクセス権が定義されます。

## 管理者にとっての設定 {#configurations-administrator}

AEM 管理者と作成者は、設定をワークスペースと見なすことができます。これらのワークスペースは、機能のアクセス権を実装することで、組織的な目的で設定のグループと関連コンテンツを収集するために使用できます。

設定は、AEM 内の多くの異なる機能に対して作成できます。

* [ContextHub セグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [編集可能なテンプレート](/help/sites-cloud/authoring/features/templates.md)
* 各種クラウド設定

### 例 {#administrator-example}

例えば、管理者は編集可能なテンプレートの 2 つの設定を作成できます。

* WKND-General
* WKND-Magazine

WKND-General の設定を使用して一般的なページテンプレートを作成し、WKND-Magazine の設定で雑誌専用のテンプレートを作成できます。

WKND-General を WKND サイトのすべてのコンテンツに関連付けることができますが、WKND-Magazine は、雑誌サイトにのみ関連付けられます。

これににより、次のことができます。

* コンテンツ作成者が雑誌のページを作成する際に、作成者は一般テンプレート (WKND-General) または雑誌テンプレート (WKND-Magazine) から選択できます。
* コンテンツ作成者がサイトの他の部分（雑誌ではない部分）のページを作成した場合、作成者は一般テンプレート (WKND-General) からのみ選択できます。

編集可能なテンプレートだけでなく、クラウド設定、ContextHub セグメント、コンテンツフラグメントモデルに対しても同様の設定が可能です。

### 設定ブラウザーの使用 {#using-configuration-browser}

設定ブラウザーを使用すると、管理者は AEM 設定に対するアクセス権を簡単に作成、管理、設定できます。

>[!NOTE]
>
>設定ブラウザーを使用して設定を作成できるのは、ユーザーが `admin` 権限。 そのような `admin` アクセス権を設定に割り当てたり、設定を変更したりするには、権限も必要です。

#### 設定の作成 {#creating-a-configuration}

設定ブラウザーを使用してAEMで設定を簡単に作成できます。

1. AEM as a Cloud Serviceにログインし、メインメニューからを選択します。 **ツール** > **一般** > **設定ブラウザー**.
1. 「**作成**」を選択します。
1. 設定に&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;を指定します。

   ![設定の作成](assets/configuration-create.png)

   * **タイトル**&#x200B;は内容がわかるように付けます。
   * 「**名前**」はリポジトリ内のノード名になります。
      * タイトルに基づいて自動的に生成され、[AEM の命名規則](naming-conventions.md)に従って調整されます。
      * 必要に応じて調整できます。
1. 許可する設定のタイプを確認します。
   * [ContextHub セグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [コンテンツフラグメントモデル](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
   * [編集可能なテンプレート](/help/sites-cloud/authoring/features/templates.md)
   * 各種クラウド設定
1. 「**作成**」を選択します。

>[!TIP]
>
>設定は入れ子にできます。

#### 設定とそのアクセス権の編集 {#access-rights}

設定をワークスペースと考える場合、これらの設定にアクセス権を設定して、それらのワークスペースにアクセスできるユーザーとアクセスできないユーザーを指定することができます。

1. AEM as a Cloud Serviceにログインし、メインメニューからを選択します。 **ツール** > **一般** > **設定ブラウザー**.
1. 編集する設定を選択し、「 」を選択します。 **プロパティ** 」をクリックします。
1. 設定に追加する追加機能を選択します。

   >[!NOTE]
   >
   >設定の作成後は、機能の選択を解除することはできません。

1. 「**有効な権限**」ボタンを使用すると、役割の一覧と、現在設定されている設定に対する権限が表示されます。
   ![有効な権限ウィンドウ](assets/configuration-effective-permissions.png)
1. 新しい権限を割り当てるには、**新しい権限の追加**&#x200B;セクションの「**ユーザーまたはグループを選択**」フィールドにユーザーまたはグループ名を入力します。
   * 「**ユーザーまたはグループを選択**」フィールドは、既存のユーザーと役割に基づいて自動入力されます。
1. オートコンプリートの結果から適切なユーザーまたは役割を選択します。
   * 複数のユーザーまたは役割を選択できます。
1. 1 人または複数の選択したユーザーまたはロールのアクセスオプションをチェックし、 **追加**.
   ![設定へのアクセス権の追加](assets/configuration-edit.png)
1. 手順を繰り返して、ユーザーまたはロールを選択し、必要に応じて追加のアクセス権を割り当てることができます。
1. 選択 **保存して閉じる** 終了したとき。

## デベロッパーにとっての設定 {#configurations-developer}

デベロッパーは、AEM as a Cloud Service と設定との連携、および設定の処理方法を知ることが重要です。

### 設定とコンテンツの分離 {#separation-of-config-and-content}

管理者とユーザーは、設定を、異なる設定やコンテンツを管理するための[ワークスペースと考る](#configurations-administrator)かもしれませんが、AEM では設定とコンテンツはリポジトリー内で別々に保存および管理されることを理解しておくことが重要です。

* `/content` はすべてのコンテンツのホームページです。
* `/conf` はすべての設定のホームです。

コンテンツは、 `cq:conf` プロパティ。 AEMは、コンテンツとそのコンテキストに基づいて検索を実行します `cq:conf` プロパティを使用して適切な設定を検索します。

### 例 {#developer-example}

この例では、DAM 設定に関心のあるアプリケーションコードがあるとします。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

すべての設定参照の開始点は、以下の場所にあるコンテンツリソースです。 `/content`. これは、ページ、ページ内のコンポーネント、アセット、DAM フォルダーのいずれかです。 これは、このコンテキストで適用される適切な設定を探している実際のコンテンツです。

次に、 `Conf` オブジェクトを使用して、目的の特定の設定項目を取得できます。 この場合、 `dam/imageserver`: `imageserver`. `getItem` を呼び出すと `ValueMap` が返されます。その後、 `bgkcolor` 文字列プロパティに値を指定し、プロパティ（または設定項目全体）が存在しない場合に使用するデフォルト値「FFFFFF」を指定します。

次に、対応する JCR コンテンツを見てみましょう。

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wknd
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

この例では、WKND 固有の DAM フォルダーと、対応する設定があるとします。 そのフォルダーから開始 `/content/dam/wknd`を見ると、 `cq:conf` サブツリーに適用される設定を参照する プロパティは `jcr:content` の名前を指定します。 これらの `conf` リンクは明示的なので、CRXDE 内のコンテンツを見るだけで簡単にリンク先を追うことができます。

内へのジャンプ `/conf`をクリックし、参照に従って、 `/conf/wknd` ノード。 これは設定です。その参照は、アプリケーションコードに対して透過的です。 この例のコードは、専用の参照を持たないので、`Conf` オブジェクトの背後に隠れています。適用される設定は、JCR コンテンツを通じて制御します。

設定には、固定名の `settings` 実際の項目 ( `dam/imageserver` この場合、が必要です。 このような項目は、「設定ドキュメント」と見なすことができ、 `cq:Page` 次を含む `jcr:content` 実際の内容を保持している

最後に、プロパティが表示されます `bgkcolor` このサンプルコードに必要な情報を含めます。 The `ValueMap` ～から戻って来る `getItem` は、ページの `jcr:content` ノード。

### 設定の解決 {#configuration-resolution}

上記の基本的な例は、1 つの設定を示しています。デフォルトのグローバル設定、ブランドごとに異なる設定、サブプロジェクト用に特定の設定など、様々な設定を使用したい場合が多くあります。

これをサポートするために、AEMでは、次の優先順で継承とフォールバックメカニズムを使用できます。

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * `cq:conf` から `/content` のどこかで参照された特定の設定
   * 階層は任意であり、サイト設定と同様にデザインできます。階層はアプリケーションコードには知らされません。
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/<siteconfig>/<parentconfig>`
   * 代替構成設定のために親をトラバース
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/<siteconfig>`
   * 代替構成設定のために親をトラバース
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/conf/global`
   * システムのグローバル設定
   * インストールのグローバルデフォルト
   * `admin` の役割によって設定
   * 設定の権限を持つユーザーが実行時に変更可能
1. `/apps`
   * アプリケーションのデフォルト
   * アプリケーションのデプロイメントで固定
   * 実行時は読み取り専用
1. `/libs`
   * AEM 製品のデフォルト
   * アドビによってのみ変更可能、プロジェクトへのアクセス許可なし
   * アプリケーションのデプロイメントで固定
   * 実行時は読み取り専用

### 設定の使用 {#using-configurations}

AEM の設定は、Sling コンテキスト対応設定に基づいています。Sling バンドルには、コンテキスト対応設定の取得に使用できるサービス API が用意されています。コンテキスト対応設定とは、コンテンツリソースまたはリソースツリーに従来どおりに関連する設定です [前の例で説明した](#developer-example).

コンテキスト対応の設定、例、その使用方法の詳細については、 [Sling ドキュメント。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html).

### ConfMgr Web コンソール {#confmgr-web-console}

デバッグおよびテストの目的で、`https://<host>:<port>/system/console/conf` には **ConfMgr** Web コンソールがあり、特定のパス／項目の設定を表示することができます。

![ConfMgr](assets/configuration-confmgr.png)

以下を提供するだけです。

* **コンテンツのパス**
* **項目**
* **ユーザー**

クリック **解決** そのため、解決された設定を確認し、それらの設定を解決するのに役立つコードサンプルを取得できます。

### コンテキスト対応設定の Web コンソール {#context-aware-web-console}

デバッグおよびテストの目的で、`https://<host>:<port>/system/console/slingcaconfig` に&#x200B;**コンテキスト対応設定の** Web コンソールがあり、リポジトリー内のコンテキスト対応設定にクエリを実行し、そのプロパティを表示できます。

![コンテキスト対応設定の Web コンソール](assets/configuration-context-aware-console.png)

以下を提供するだけです。

* **コンテンツのパス**
* **設定名**

クリック **解決** 選択した設定に関連付けられたコンテキストパスとプロパティを取得できます。
