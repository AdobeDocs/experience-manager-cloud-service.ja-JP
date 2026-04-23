---
title: MSM およびライブコピーを使用したコンテンツフラグメントの再利用
description: MSM のライブコピー機能を使用して、ソースコンテンツと同期しながら、同じまたは類似のコンテンツフラグメントコンテンツを複数の場所で使用する方法について説明します。
badgeSaas: label="AEM Sites" type="Positive" tooltip="AEM Sitesに適用）。"
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
source-git-commit: 85b72909597a95531aea51719c841bc5db9c1a21
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 28%

---

# MSM を使用したコンテンツフラグメントの再利用 {#reuse-content-fragments-using-msm}

マルチサイトマネージャー（MSM）とライブコピー機能を使用すると、ソースコンテンツと同期しながら、複数の場所で同じコンテンツを使用できます。

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>コンテンツフラグメントコンソールのMSMは現在、Beta機能であり、特定のお客様のみが利用できます。
>
>コンテンツフラグメントのMSMは、**Assets** コンソールでコンテンツフラグメントを使用する場合にも使用できます。

* MSM ライブコピーを使用すると、次のことができます。
   * コンテンツを一度作成
   * 同じサイトの他の領域、他のサイト、またはアプリケーションで、このコンテンツを再利用します。
* その後、MSM は次の目的でソースコンテンツとライブコピーの間のライブ関係を維持します。
   * ソースコンテンツを変更すると、ソースコピーとライブコピーが同期されます。
   * 個々のサブフラグメントやコンポーネントのライブ関係を切断することで、ライブコピーのコンテンツのみを調整できます。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

MSMの概念の詳細な概要については、「コンテンツの再利用：マルチサイトマネージャーとライブコピー」を参照してください。

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>Adobe Experience Managerのマルチサイトマネージャー（MSM）機能では、一度作成したコンテンツを複数のweb サイトで再利用できます。

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

コンテンツフラグメント用 MSM を使用すると、次のことができます。

* コンテンツフラグメントを 1 回作成してから、これらのフラグメントの（リンクされた）コピーを作成して、サイトまたはアプリケーションの他の領域で再利用する。
* ソースコピーを 1 回更新してから、変更を（ライブ）コピーにプッシュして、複数のコピーの同期を維持する。
* 親フラグメントと子フラグメントの間のリンクを完全に、またはそのバリエーションやフィールドに関して、一時的または永続的に休止し、ローカルに変更を行う。

MSM for Content Fragments をコンテンツフラグメントエディター内の機能と組み合わせると、フィールドレベルで継承を解除および復元できます。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>このページでは、**コンテンツフラグメント** コンソールを使用する場合のMSM機能について説明します。
>
>コンテンツフラグメントのMSMは、**Assets** コンソールでコンテンツフラグメントを使用する場合にも使用できます。

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## ライブコピーの作成 {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

コンテンツフラグメントのライブコピーを作成するには：

1. コンテンツフラグメントコンソールで、フラグメントの場所に移動します。
1. フラグメントを選択します。
1. 上部のツールバーから「**ライブコピーを作成**」を選択します。
1. 開いたダイアログで、宛先を指定し、**次へ**&#x200B;に進みます。
1. プロパティを指定します。 タイトル、名前、およびライブコピーで子（ネストされたフラグメント）を除外するかどうかを指定できます。
1. **次**&#x200B;へ進みます。
1. ライブコピーをすぐに作成するか（**今**）、**後**&#x200B;の日時に作成するかを選択します。
1. **ライブコピーの作成**&#x200B;を確認します。

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >MSMを使用してコンテンツフラグメントのコピーを作成する場合）は、それぞれのコンテンツフラグメントモデルで使用されているすべてのデータタイプから、**一意の**&#x200B;制約を削除する必要があります。

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## プロパティとステータスの表示 {#view-properties-and-status}

ソースとライブコピーのプロパティとステータスを表示するには、次の手順に従います。

1. コンテンツフラグメントコンソールで、フラグメントの場所に移動します。
1. フラグメントを選択します。
1. フラグメントの「**タイトル**」列で「情報（i）」アイコンを選択します。
右側の情報パネルが開きます。
1. **ライブコピーの詳細**&#x200B;のタブを選択します。

   ![&#x200B; ライブコピーに関する情報](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## 変更を反映 {#propagate-modifications}

ソースとライブコピー間で変更を反映します。

### 同期 {#synchronize}

ライブコピーからソースにコンテンツ更新を取り込む同期をトリガーするには、次の手順を実行します。

1. コンテンツフラグメントコンソールで、フラグメントソースの場所に移動します。
1. フラグメントを選択します。
1. ツールバーの「**同期**」を選択します。
1. ダイアログで「**同期**」を確認します。

### ロールアウト {#rollout}

ソース更新をライブコピーにプッシュするロールアウトをトリガーするには：

1. コンテンツフラグメントコンソールで、フラグメントライブコピーの場所に移動します。
1. フラグメントを選択します。
1. ツールバーから「**ロールアウト**」を選択します。 ウィザードが開き、プロセスをガイドします。
1. ロールアウトに含めるライブコピーを選択し、**続行**&#x200B;します。
1. 直ちに（**今**）または&#x200B;**後**&#x200B;のロールアウトをスケジュールします。
1. 必要に応じて&#x200B;**続行**&#x200B;します。

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## エディターでの継承をキャンセルして元に戻す {#cancel-and-revert-to-inheritance-in-the-editor}

継承とは、コンポーネントからコンポーネントへコンテンツを自動的にプッシュできるメカニズムです。継承されたフィールドとバリエーションは、マルチサイト管理の製品にすることができます。

コンテンツフラグメントエディターで継承をキャンセル（その後に戻す）できます。 フラグメントがライブコピーの一部である場合は、コンテキストに応じて、これをバリエーションに対して使用できます。個々のフィールドに対して使用することもできます。

次に例を示します。

* 継承のキャンセル

  ![継承のキャンセルアイコン](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* 継承に戻す（継承が既にキャンセルされている場合）

  ![継承アイコンに戻す](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## コンテンツフラグメントとサイトページのMSMの比較 {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

ほとんどのシナリオでは、コンテンツフラグメント用MSMは、サイトページ用MSM機能の動作と一致します。 注意すべき重要な違いは次のとおりです。

* MSM for Sites ページのブループリントは、MSM for Content Fragmentsのライブコピーソースと呼ばれます。
* Sites ページでは、ブループリントとそのライブコピーを比較できますが、コンテンツフラグメントでソースをライブコピーと比較することはできません。
* コンテンツフラグメントコンソールでライブコピーを編集することはできません。
* サイトページには通常、子が含まれますが、コンテンツフラグメントは参照フラグメントを含まない場合があります。 子を含めるまたは除外するオプションは、これらの参照先フラグメントを参照します。
* コンテンツフラグメントのMSMでは、サイトを作成ウィザードのチャプターステップの削除はサポートされていません。
* ページプロパティでのMSM ロックの設定は、コンテンツフラグメントのMSMではサポートされていません。
* コンテンツフラグメントのMSMの場合は、**標準ロールアウト設定**&#x200B;のみを使用します。 その他のロールアウト設定は、コンテンツフラグメント用MSMでは使用できません。

>[!NOTE]
>
>コンテンツフラグメントコンソールを介してアクセスされるコンテンツフラグメントのMSMは、Assets機能に基づいています。これは、Assetsとして保存されているためです（Sites機能と見なされます）。

## 制限事項 {#limitations}

* 変更時のトリガーと関連するロールアウト設定は、コンテンツフラグメントには存在しません。
