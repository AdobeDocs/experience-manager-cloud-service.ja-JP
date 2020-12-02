---
title: 設定と設定ブラウザ
description: AEM設定と、AEMでのワークスペース設定の管理方法について理解します。
translation-type: tm+mt
source-git-commit: 47d2ff211b5c00457793dc7bd321df1139cfc327
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# 構成と構成ブラウザ{#configuration-browser}

AEM設定は、AEMの設定を管理し、ワークスペースとして機能します。

## 設定とは{#what-is-a-configuration}

設定は、2つの異なる視点から考察できます。

* [設定は、](#configurations-administrator) 管理者がAEM内のワークスペースとして設定のグループを定義および管理するために使用します。
* [開発者は、AEMで設定を保持および検索する設定を実装する基本的な設定メカニズムを](#configurations-developer) 使用します。

まとめ：管理者の表示上、設定とは、AEMで設定を管理するワークスペースの作成方法を指します。一方、開発者は、AEMがリポジトリ内でこれらの設定を使用および管理する方法を理解する必要があります。

設定は、ユーザーの視点に関係なく、AEMでは2つの主な目的を果たします。

* 設定により、特定のユーザーグループに対して特定の機能が有効になります。
* 設定によって、これらの機能のアクセス権が定義されます。

## 管理者としての設定{#configurations-administrator}

AEM管理者と作成者は、設定をワークスペースと見なすことができます。 これらのワークスペースは、これらの機能のアクセス権を実装することで、組織の目的のために、設定のグループと関連するコンテンツをまとめて収集するのに使用できます。

設定は、AEM内の多くの異なる機能に対して作成できます。

* [クラウド設定](/help/implementing/developing/introduction/configurations.md)
* [コンテキストハブセグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [編集可能なテンプレート](/help/sites-cloud/authoring/features/templates.md)

### 例 {#administrator-example}

例えば、管理者が編集可能なテンプレートの2つの設定を作成できます。

* WKND-General
* WKNDマガジン

その後、WKND-General設定を使用して一般的なページテンプレートを作成し、WKND-Magazineの下の雑誌専用のテンプレートを作成できます。

その後、管理者はWKND-GeneralをWKNDサイトのすべてのコンテンツに関連付けることができます。 ただし、WKND-Magazine設定は、雑誌サイトにのみ関連付けられます。

次の操作を行います。

* コンテンツ作成者が雑誌の新しいページを作成するとき、作成者は「一般」テンプレート（WKND — 一般）または「雑誌」テンプレート（WKND — 雑誌）から選択できます。
* コンテンツ作成者が、雑誌以外のサイトの別の部分に対して新しいページを作成した場合、作成者は一般テンプレート(WKND-General)からのみ選択できます。

編集可能なテンプレートだけでなく、クラウド設定、ContextHubセグメント、コンテンツフラグメントモデルに対しても同様の設定が可能です。

### 設定ブラウザーの使用 {#using-configuration-browser}

設定ブラウザを使用すると、管理者はAEMの設定に対するアクセス権を簡単に作成、管理および設定できます。

>[!NOTE]
>
>ユーザーに`admin`権限がある場合にのみ、設定ブラウザーを使用して設定を作成できます。 `admin` アクセス権を設定に割り当てたり、設定を変更したりするには、権限も必要です。

#### 構成の作成{#creating-a-configuration}

設定ブラウザーを使用してAEMで新しい設定を作成する方法は、非常に簡単です。

1. AEMにCloud Serviceとしてログインし、メインメニューで&#x200B;**ツール** -> **一般** -> **構成ブラウザー**&#x200B;を選択します。
1. 「**作成**」をタップまたはクリックします。
1. 設定に&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;を指定します。

   ![設定の作成](assets/configuration-create.png)

   * **タイトル**&#x200B;は説明的にします。
   * **Name**&#x200B;がリポジトリのノード名になります。
      * タイトルに基づいて自動的に生成され、[AEMの命名規則に従って調整されます。](naming-conventions.md)
      * 必要に応じて調整できます。
1. 許可する設定のタイプを確認します。
   * [クラウド設定](/help/implementing/developing/introduction/configurations.md)
   * [コンテキストハブセグメント](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
   * [編集可能なテンプレート](/help/sites-cloud/authoring/features/templates.md)
1. 「**作成**」をタップまたはクリックします。

>[!TIP]
>
>構成は入れ子にできます。

#### 設定とそのアクセス権の編集{#access-rights}

設定をワークスペースと考える場合、これらの設定にアクセス権を設定して、それらのワークスペースにアクセスできるユーザーとアクセスできないユーザーを強制できます。

1. AEMにCloud Serviceとしてログインし、メインメニューで&#x200B;**ツール** -> **一般** -> **構成ブラウザー**&#x200B;を選択します。
1. 変更する設定を選択し、ツールバーの&#x200B;**プロパティ**&#x200B;をタップまたはクリックします。
1. 設定に追加する追加機能を選択します
   >[!NOTE]
   >
   >設定が作成された後は、フィーチャの選択を解除することはできません。
1. **有効な権限**ボタンを使用して、ロールの一覧と、現在設定されている設定に対する権限を表示します。
   ![有効な権限ウィンドウ](assets/configuration-effective-permissions.png)
1. 新しい権限を割り当てるには、**「新しい権限**」セクションの「**ユーザーまたはグループを選択**」フィールドにユーザーまたはグループ名追加を入力します。
   * **Select user or group**&#x200B;フィールドのオファーは、既存のユーザーと役割に基づいて自動入力されます。
1. オートコンプリートの結果から適切なユーザーまたは役割を選択します。
   * 複数のユーザーまたはロールを選択できます。
1. 選択したユーザーまたはロールに必要なアクセスオプションを確認し、**追加**をクリックします。
   ![設定追加へのアクセス権](assets/configuration-edit.png)
1. 手順を繰り返して、ユーザーまたはロールを選択し、必要に応じて追加のアクセス権を割り当てます。
1. 終了したら、「**保存して閉じる**」をタップまたはクリックします。

## 開発者としての設定{#configurations-developer}

開発者として、Cloud ServiceとしてのAEMの設定との連携、および設定解決の処理方法を知ることが重要です。

### 構成とコンテンツの分離{#separation-of-config-and-content}

[管理者とユーザーは、設定を職場](#configurations-administrator)と考えて異なる設定やコンテンツを管理できますが、設定とコンテンツはリポジトリ内のAEMで別々に保存および管理されることを理解することが重要です。

* `/content` はすべてのコンテンツのホームページです。
* `/conf` は、すべての設定のホームページです。

コンテンツは`cq:conf`プロパティを介して関連する設定を参照します。 AEMは、コンテンツとコンテキスト`cq:conf`プロパティに基づいてルックアップを実行し、適切な設定を見つけます。

### 例 {#developer-example}

この例では、DAM設定に関心のあるアプリケーションコードがあるとします。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

すべての設定参照の開始点は、コンテンツリソースで、通常は`/content`の下に配置されます。 これは、ページ、ページ内のコンポーネント、アセット、またはDAMフォルダーの場合があります。 これは、この状況で適用される適切な設定を探している実際のコンテンツです。

`Conf`オブジェクトを用意したら、特定の設定項目を取得できます。 この場合、`dam/imageserver`です。これは`imageserver`に関連する設定の集まりです。 `getItem`呼び出しは`ValueMap`を返します。 次に、`bgkcolor`文字列プロパティを読み取り、プロパティ（または設定項目全体）が存在しない場合に備えて、デフォルト値の「FFFFF」を指定します。

次に、対応するJCRコンテンツを見てみましょう。

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

この例では、WKND固有のDAMフォルダーと、対応する設定があると仮定します。 このフォルダー`/content/dam/wknd`から始まると、サブツリーに適用する設定を参照する`cq:conf`という名前の文字列プロパティがあることがわかります。 このプロパティは通常、アセットフォルダーまたはアセットページの`jcr:content`に設定されます。 これらの`conf`リンクは明示的なので、CRXDE内のコンテンツを見るだけで簡単にリンク先を追うことができます。

`/conf`の中に飛び込み、参照をたどって`/conf/wknd`ノードがあるのが見えます。 これは設定です。 この参照は、アプリケーションコードに対して完全に透過的であることに注意してください。 この例のコードは、専用の参照を持たないので、`Conf`オブジェクトの背後に隠れています。 どの設定が適用されるかは、JCRコンテンツを介して完全に制御されます。

この設定には、実際の項目を含む固定名の`settings`ノードが含まれています。この例では、`dam/imageserver`が必要です。 このようなアイテムは「設定ドキュメント」と考えることができ、通常は`jcr:content`を含む`cq:Page`で表されます。

最後に、サンプルコードに必要なプロパティ`bgkcolor`が表示されます。 `getItem`から戻る`ValueMap`は、ページの`jcr:content`ノードに基づいています。

### 構成の解決{#configuration-resolution}

上記の基本的な例は、1つの設定を示しています。 しかし、デフォルトのグローバル設定、ブランドごとに異なる設定、サブプロジェクト用に特定の設定など、多くの場合、異なる設定を使用したいと思われます。

これをサポートするために、AEMでの設定参照には継承とフォールバックのメカニズムが次の優先順に用意されています。

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * `cq:conf`から`/content`のどこかで参照された特定の設定
   * 階層は任意であり、サイト構造と同様にデザインできます。これを知るのはアプリケーションコードのビジネスではありません。
   * 設定権限を持つユーザーが実行時に変更できる
1. `/conf/<siteconfig>/<parentconfig>`
   * 代替設定のために親をトラバース
   * 設定権限を持つユーザーが実行時に変更できる
1. `/conf/<siteconfig>`
   * 代替設定のために親をトラバース
   * 設定権限を持つユーザーが実行時に変更できる
1. `/conf/global`
   * システムのグローバル設定
   * 通常、インストールのグローバルなデフォルト
   * `admin`ロールによって設定
   * 設定権限を持つユーザーが実行時に変更できる
1. `/apps`
   * アプリケーションのデフォルト
   * アプリケーションのデプロイメントに関する修正
   * 実行時の読み取り専用
1. `/libs`
   * AEMの製品デフォルト
   * Adobeによって変更できるのみ、プロジェクトへのアクセスは許可されていません
   * アプリケーションのデプロイメントに関する修正
   * 実行時の読み取り専用

### 構成の使用{#using-configurations}

AEMの設定は、Sling Context-Aware設定に基づいています。 Slingバンドルには、コンテキストに応じた設定の取得に使用できるサービスAPIが用意されています。 コンテキスト対応構成とは、前の例で説明したように、コンテンツリソースまたはリソースツリーに関連する構成です。[](#developer-example)

コンテキスト対応の設定、例、およびその使用方法の詳細については、[Slingのドキュメントを参照してください。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Webコンソール{#confmgr-web-console}

デバッグおよびテストの目的で、**ConfMgr** Webコンソールが`https://<host>:<port>/system/console/conf`にあり、これは特定のパス/項目の設定を示すことができます。

![ConfMgr](assets/configuration-confmgr.png)

以下を提供するだけです。

* **コンテンツのパス**
* **Item**
* **User**

**解決**&#x200B;をクリックして、解決される構成を確認し、それらの構成を解決するサンプルコードを受け取ります。

### コンテキスト対応構成Webコンソール{#context-aware-web-console}

デバッグおよびテストの目的で、**Context-Aware Configuration** Webコンソールが`https://<host>:<port>/system/console/slingcaconfig`にあります。これにより、リポジトリ内のコンテキスト対応設定にクエリーを実行し、そのプロパティを表示できます。

![コンテキスト対応設定Webコンソール](assets/configuration-context-aware-console.png)

以下を提供するだけです。

* **コンテンツのパス**
* **構成名**

「**Resolve**」をクリックして、選択した構成に関連付けられたコンテキストパスとプロパティを取得します。
