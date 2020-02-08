---
title: マルチサイトでのターゲットコンテンツの操作
description: アクティビティ、エクスペリエンス、オファーなどのターゲットコンテンツを複数のサイトにまたがって管理する必要がある場合は、AEM に組み込まれているターゲットコンテンツ用マルチサイトサポートを利用できます。
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# マルチサイトでのターゲットコンテンツの操作 {#working-with-targeted-content-in-multisites}

アクティビティ、エクスペリエンス、オファーなどのターゲットコンテンツを複数のサイトにまたがって管理する必要がある場合は、AEM に組み込まれているターゲットコンテンツ用マルチサイト管理機能を利用できます。

>[!NOTE]
>
>ターゲットコンテンツ用マルチサイト管理は、上級者向けの機能です。この機能を使用するには、マルチサイトマネージャーとAEMとのAdobe targetの統合について理解しておく必要があります。
<!--
>Working with Multisite support for targeted content is an advanced feature. To use this feature, you should be familiar with [Multi Site Manager](/help/sites-administering/msm.md) and the [Adobe Target integration](/help/sites-administering/target.md) with AEM.
-->

このドキュメントでは次の内容について説明します。

* AEM のターゲットコンテンツ用マルチサイト管理の概要
* 1 つのブランドに属する複数のサイトをリンクする場合のシナリオ
* この機能の使用手順の例
* ターゲットコンテンツ用マルチサイト管理の実装方法

パーソナライズされたコンテンツをサイト間で共有するには、以下の手順を実行する必要があります。

1. [新しい領域を作成](#creating-new-areas)するか、[新しい領域をライブコピーとして作成](#creating-new-areas)します。領域には、ページ内の領域&#x200B;**&#x200B;で使用可能なすべてのアクティビティが含まれます。つまり、ページ内のこの場所が、コンポーネントのターゲットになります。新しい領域を作成した場合は空の領域が作成されますが、新しい領域をライブコピーとして作成した場合は、サイト構造をまたがってコンテンツを継承できます。

1. 領域に[サイトまたはページをリンク](#linking-sites-to-an-area)します。

継承はいつでも休止または復元できます。さらに、継承を休止せずに、ローカルなエクスペリエンスを作成することもできます。デフォルトでは、特に指定しない限り、すべてのページがマスター領域を使用します。

## ターゲットコンテンツ用マルチサイト管理の概要 {#introduction-to-multisite-support-for-targeted-content}

ターゲットコンテンツ用マルチサイト管理はすぐに利用可能です。この機能を使用して、MSM で管理されるマスターページからローカルなライブコピーにターゲットコンテンツをプッシュしたり、ターゲットコンテンツのグローバルな変更とローカルな変更を管理したりできます。

You manage this in an **Area**. 領域によって、別々のサイトで使用されるターゲットコンテンツ（アクティビティ、エクスペリエンスおよびオファー）を切り分けたり、ターゲットコンテンツの継承をサイトの継承と関連付けて設定、管理する MSM ベースのメカニズムを実現したりすることができます。これにより、AEM 6.2 より前のバージョンとは異なり、継承されたサイトでのターゲットコンテンツの再作成が不要になります。

領域内では、その領域にリンクされているアクティビティのみがライブコピーにプッシュされます。デフォルトでは、マスター領域が選択されます。追加の領域を作成したら、その領域にプッシュするターゲットコンテンツを指示するために、領域をサイトまたはページにリンクできます。

サイトまたはライブコピーを領域にリンクするときは、そのサイトまたはライブコピーで使用するアクティビティを含む領域にリンクします。デフォルトでは、サイトまたはライブコピーのリンクはマスター領域に対して行われますが、マスター領域以外の領域にもリンクを行うことができます。

>[!NOTE]
>
>ターゲットコンテンツ用マルチサイト管理を使用する際は、以下の点に注意してください。
>
>* ロールアウトまたはライブコピーを利用する場合は MSM ライセンスが必要です。
>* Adobe Target への同期を利用する場合は、Adobe Target ライセンスが必要です。
>



## 使用例 {#use-cases}

ターゲットコンテンツ用マルチサイト管理は、目的に応じて様々な方法で使用できます。このセクションでは、この機能を 1 つのブランドで使用する場合の仕組みを説明します。In addition, in [Example: Targeting Content Based on Geography](#example-targeting-content-based-on-geography), you can see a real-world application of targeting content in multiple sites.

ターゲットコンテンツは領域の中に配置されます。つまり、領域はサイトまたはページの範囲を定義します。こうした領域はブランドレベルで定義されます。1 つのブランドに複数の領域を含めることができます。領域の設定がブランドごとに異なる場合もあります。あるブランドがマスター領域のみを含み、そのマスター領域がすべてのブランド間で共有される一方で、別のブランドが（例えば地域別の）複数のブランドを含んでいる場合も考えられます。そのため、ブランド間で同じ領域セットを使用する必要はありません。

ターゲットコンテンツ用マルチサイト管理を利用すると、**1 つの**&#x200B;ブランドで 2 つ（以上）のサイトを持つことができます。このとき、2 つのサイトは以下のいずれかのターゲットコンテンツセットを持ちます。

* それぞれが完全に異なる&#x200B;**&#x200B;ターゲットコンテンツセットを持つ - 一方のセットでターゲットコンテンツを編集しても、他方のセットに影響はありません。別の領域にリンクするサイトは、独自の構成領域に対して読み取りと書き込みを行います。 次に例を示します。
   * サイト A が領域 X にリンク
   * サイト B が領域 Y にリンク
* 両者がターゲットコンテンツセットを共有する&#x200B;** - 一方を編集すると、両方のサイトに直接的な影響が及びます。この形は、2 つのサイトに同じ領域を参照させることによって実現されます。同じ領域にリンクするサイトは、この領域内のターゲットコンテンツを共有します。 次に例を示します。
   * サイト A が領域 X にリンク
   * サイト B が領域 X にリンク
* A distinct set of targeted content *inherited* from another site via MSM - Content can be unidirectionally rolled out from master to live copy. 次に例を示します。
   * サイト A が領域 X にリンク
   * サイト B が領域 Y（領域 X のライブコピー）にリンク

1 つのサイトで&#x200B;**複数の**&#x200B;ブランドを使用することもできます。その場合は、上記の例よりも話が複雑になります。

![マルチサイトの例](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## 例：地域に基づくコンテンツのターゲット設定 {#example-targeting-content-based-on-geography}

ターゲットコンテンツ用マルチサイト管理を使用して、パーソナライゼーションコンテンツを共有、ロールアウトまたは分離できます。この機能の使用方法をわかりやすく説明するために、以下のシナリオのように、地域に基づいてターゲットコンテンツをロールアウトするシナリオを考えてみましょう。

同じサイトを、地域ごとに異なる 4 つのバージョンとして運用します。

* 左上の&#x200B;**米国**&#x200B;サイトがマスターサイトです。この例では、ターゲットモードで開かれています。
* 他の 3 つのバージョンは、**カナダ**、**英国**&#x200B;および&#x200B;**オーストラリア**&#x200B;向けのサイトで、すべてライブコピーです。これらのサイトはプレビューモードで開かれています。

![マルチサイトバージョン](/help/sites-cloud/authoring/assets/multisite-versions.png)

各地域のサイトは、パーソナライズされたコンテンツを次のように共有します。

* カナダは米国のマスター領域を共有します。
* イギリスはヨーロッパ地域と結びついており、その主領地域を継承している。
* オーストラリアは南半球にあり、米国の季節商品をそのまま適用することができないので、コンテンツを独自にパーソナライズします。

![マルチサイト図](/help/sites-cloud/authoring/assets/multisite-diagram.png)

このブランドで、北半球向けに冬用アクティビティを作成しました。しかし北米のマーケティング担当者は、男性オーディエンスには別の冬用画像を表示したいと考えたので、米国サイトでその画像を変更しました。

![米国版](/help/sites-cloud/authoring/assets/multisite-us.png)

タブを更新すると、何もしなくても、カナダのサイトが新しい画像に変更されます。これは、カナダのサイトが米国のサイトとマスター領域を共有しているからです。英国やオーストラリアのサイトでは、画像は変わりません。

![バージョンの変更](/help/sites-cloud/authoring/assets/multisite-us-change.png)

マーケティング担当者はこの変更をヨーロッパ地域にもロールアウトしたいと考え、「**ページをロールアウト**」をタップまたはクリックして、ライブコピーをロールアウトしました。After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout). <!--The marketer would like to roll out these changes to the European region and [rolls out the live copy](/help/sites-administering/msm-livecopy.md) by tapping or clicking **Rollout Page**. After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout).-->

![ライブコピーをロールアウト](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

オーストラリアのサイトの画像は変更されないままです。オーストラリアは夏で、マーケティング担当者はこのコンテンツを変更したくないので、これが望ましい動作です。オーストラリアのサイトは、他の地域と領域を共有しておらず、別の地域のライブコピーではないので、変更されません。そのため、マーケティング担当者は、オーストラリアのサイトのターゲットコンテンツが上書きされるのではないかと心配する必要ありません。

さらに、英国のサイトでは、この領域がマスター領域のライブコピーになっているので、アクティビティ名の横の緑色のインジケーターで継承ステータスを確認できます。継承されたアクティビティは、ライブコピーを休止または分離しない限り変更できません。

継承は、いつでも休止または完全に分離できます。継承を休止せずに、ローカルなエクスペリエンス専用のエクスペリエンスを追加することも随時可能です。

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### 新しい領域の作成と新しい領域をライブコピーとして作成 {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

AEM では、新しい領域を作成するか、新しい領域をライブコピーとして作成するかを選択できます。新しい領域を作成すると、アクティビティと、そのアクティビティに属するすべてのもの（オファー、エクスペリエンスなど）がグループ化されます。新しい領域は、完全に別個のターゲットコンテンツセットを作成したい場合や、ターゲットコンテンツセットを共有したい場合に作成します。

ただし、MSM を使用して 2 つのサイト間の継承を設定すれば、アクティビティを継承できます。この場合は、新しい領域をライブコピーとして作成します。Y は X のライブコピーなので、アクティビティもすべて継承されます。

>[!NOTE]
>
>デフォルトのロールアウトは、ページが、ページのBlueprintにリンクされた領域のライブコピーである領域にリンクするライブコピーである場合に、ターゲットコンテンツの後続のロールアウトをトリガーします。

例えば、次の図に示す 4 つのサイトを見てください。2 つのサイトはマスター領域（およびその領域の一部であるすべてのアクティビティ）を共有しています。1 つのサイトは、領域のライブコピーである領域を含んでいるので、ロールアウト時にアクティビティを共有します。もう 1 つのサイトは完全に独立しています（そのため、そのサイトのアクティビティ用の領域が必要です）。

![図の詳細](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

AEM でこれを実現するには、次の作業をおこないます。

* サイト A をマスター領域にリンク - 領域の作成は不要です。AEM では、デフォルトでマスター領域が選択されます。サイト A と B がアクティビティなどを共有します。
* サイト B をマスター領域にリンク - 領域の作成は不要です。AEM では、デフォルトでマスター領域が選択されます。サイト A と B がアクティビティなどを共有します。
* サイト C をマスター領域のライブコピーである継承領域にリンク - マスター領域をベースとしてライブコピーを作成する「領域をライブコピーとして作成」を実行します。継承領域は、ロールアウト時にマスター領域からアクティビティを継承します。
* サイト D を独自の分離領域にリンク - アクティビティがまだ定義されていないまったく新しい領域を作成する「領域を作成」を実行します。分離領域は、他のサイトとアクティビティを共有しません。

## 新しい領域の作成 {#creating-new-areas}

領域はアクティビティとオファーにまたがることができます。そのどちらか（例えばアクティビティ）に領域を作成すると、もう一方（例えばオファー）でもこの領域を使用できるようになります。

>[!NOTE]
>
>別の領域が&#x200B;**作成されるまでは**、ブランド名をタップまたはクリックすると、マスター領域と呼ばれるデフォルトの領域がデフォルトで展開されます。Then, when you select a brand in either the **Activity** or **Offers** console, you see the **Area** console.

新しい領域を作成するには：

1. Navigate to **Personalization** > **Activities** or **Offers** or and then to your brand.
1. 「**領域を作成**」をタップまたはクリックします。

   ![作成領域](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. 「**領域**」アイコンをクリックして、「**次へ**」をクリックします。
1. 「**タイトル**」フィールドに新しい領域名を入力します。オプションでタグを選択します。
1. 「**作成**」をタップまたはクリックします。

   作成済みの領域がすべて表示されたブランドウィンドウにリダイレクトされます。マスター領域以外の領域が存在する場合は、ブランドコンソールで直接領域を作成できます。

   ![作成](/help/sites-cloud/authoring/assets/multisite-create.png)

## 領域をライブコピーとして作成 {#creating-areas-as-live-copies}

サイト構造をまたがってターゲットコンテンツを継承するには、領域をライブコピーとして作成します。

領域をライブコピーとして作成するには：

1. Navigate to **Personalization** > **Activities** or **Offers** and then to your brand.
1. 「**領域をライブコピーとして作成**」をタップまたはクリックします。

   ![領域をライブコピーとして作成](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. ライブコピーの作成元とする領域を選択し、「**次へ**」をクリックします。

   ![ライブコピーの作成](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. 「**名前**」フィールドにライブコピーの名前を入力します。デフォルトではサブページも含まれますが、「**サブページを除外**」チェックボックスをオンにすると除外されます。

   ![ライブコピーの作成](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. **ロールアウトの設定**&#x200B;ドロップダウンメニューで、適切な設定を選択します。

   See Installed Rollout Configurations for descriptions of each option. <!--See [Installed Rollout Configurations](/help/sites-administering/msm-sync.md#installed-rollout-configurations) for descriptions of each option.-->

   See Creating and Synchronizing Live Copies for more information on live copies. <!--See [Creating and Synchronizing Live Copies](/help/sites-administering/msm-livecopy.md) for more information on live copies.-->

   >[!NOTE]
   >
   >When a page is rolled out to a Live Copy and the area configured for the Blueprint page is also the Blueprint for the area configured for the Pages Live Copy, the LiveAction **personalizationContentRollout** triggers a synchronous subRollout, which is part of the **Standard rollout config**.

1. 「**作成**」をタップまたはクリックします。

   作成済みの領域がすべて表示されたブランドウィンドウにリダイレクトされます。マスター領域以外の領域が存在する場合は、ブランドウィンドウから直接領域を作成できます。

   ![作成領域](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## 領域へのサイトのリンク {#linking-sites-to-an-area}

領域をページまたはサイトにリンクできます。領域は、サブページ上のマッピングによってオーバーレイされない限り、すべてのサブページに継承されます。 ただし、一般的にはサイトレベルでリンクします。

リンクすると、選択した領域からのアクティビティ、エクスペリエンス、オファーだけが使用可能になります。そのため、独立して管理されているコンテンツを誤って使用するおそれはなくなります。設定されている領域が他にない場合は、各ブランドのマスター領域が使用されます。

>[!NOTE]
>
>Pages or sites that reference the same area are using the *same* shared set of activities, experiences, and offers. 複数のサイトで共有されるアクティビティ、エクスペリエンスまたはオファーを編集すると、すべてのサイトに影響します。

サイトを領域にリンクするには：

1. 領域にリンクするサイト（またはページ）に移動します。
1. サイトまたはページを選択し、「**プロパティを表示**」をタップまたはクリックします。
1. Tap or click the **Personalization** tab.
1. **ブランド**&#x200B;メニューで、領域をリンクするブランドを選択します。ブランドを選択すると、使用可能な領域が&#x200B;**領域参照**&#x200B;メニューに表示されます。

   ![サイトのリンク](/help/sites-cloud/authoring/assets/multisite-english.png)

1. **領域参照**&#x200B;ドロップダウンメニューから領域を選択し、「**保存**」をタップまたはクリックします。

   ![エリア参照](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## ライブコピーの分離またはターゲットコンテンツの継承の休止 {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

ターゲットコンテンツの継承を休止または分離したいことがあります。ライブコピーの休止または分離は、アクティビティごとに実行します。例えば、アクティビティ内のエクスペリエンスを変更したいと思っても、そのアクティビティがまだ継承されたコピーにリンクされている場合は、エクスペリエンスまたはそのアクティビティのプロパティを変更できません。

ライブコピーを休止すると、継承が一時的に解除されますが、後で継承を復元できます。ライブコピーを分離すると、継承が恒久的に解除されます。

アクティビティ内で復元することで、ターゲットコンテンツの継承を休止または分離します。ページまたはサイトがライブコピーである領域にリンクしている場合、アクティビティの継承ステータスを表示できます。

別のサイトから継承しているアクティビティは、アクティビティ名の横に緑色でマークされます。休止されている継承は赤色でマークされます。ローカルに作成されたアクティビティにはアイコンが表示されません。

>[!NOTE]
>
>* 休止または分離できるのは、アクティビティ内のライブコピーだけです。
>* 継承されたアクティビティを拡張するために、ライブコピーを休止または分離する必要はありません。そのアクティビティ用の&#x200B;**新しい**&#x200B;ローカルなエクスペリエンスやオファーをいつでも作成できます。既存のアクティビティを変更する場合は、継承を休止する必要があります。
>



### 継承の休止 {#suspending-inheritance}

アクティビティ内のターゲットコンテンツの継承を休止または分離するには：

1. 継承を分離または休止するページに移動して、モードのドロップダウンメニューで「**ターゲット設定**」をタップまたはクリックします。
1. ページがライブコピーの領域にリンクしている場合は、継承ステータスが表示されます。「**ターゲット設定を開始**」をタップまたはクリックします。
1. アクティビティを休止するには、次のどちらかを実行します。

   1. オーディエンスなど、アクティビティの要素を選択します。ライブコピーを休止確認ボックスが自動的に表示されます（ターゲット設定プロセスのどこかで任意の要素をタップまたはクリックして、ライブコピーを休止することができます）。
   1. ツールバーのドロップダウンメニューで「**ライブコピーを休止**」を選択します。
   ![ライブコピーの中断](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Tap or click **Suspend** to suspend the activity. 休止されたアクティビティが赤色でマークされます。

   ![停止されたライブコピー](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### 継承の解除 {#breaking-inheritance}

アクティビティ内のターゲットコンテンツの継承を解除するには：

1. マスターからライブコピーを分離するページに移動して、モードのドロップダウンメニューで「**ターゲット設定**」をタップまたはクリックします。
1. ページがライブコピーの領域にリンクしている場合は、継承ステータスが表示されます。「**ターゲット設定を開始**」をタップまたはクリックします。
1. ツールバーのドロップダウンメニューで「**ライブコピーを添付解除**」を選択します。ライブコピーを分離するかどうか確認されます。
1. 「**添付を解除**」をタップまたはクリックして、アクティビティからライブコピーを分離します。ライブコピーが分離されると、継承に関するドロップダウンメニューは表示されなくなります。これで、このアクティビティはローカルアクティビティになりました。

   ![ローカルアクティビティ](/help/sites-cloud/authoring/assets/multisite-winter.png)

## ターゲットコンテンツの継承の復元 {#restoring-inheritance-of-targeted-content}

アクティビティ内のターゲットコンテンツの継承を休止した場合は、いつでも継承を復元できます。それに対して、ライブコピーを分離した場合は、継承を復元できません。

アクティビティ内のターゲットコンテンツの継承を復元するには：

1. Navigate to the page where you want to restore inheritance and tap or click **Targeting** in the mode drop-down menu.
1. 「**ターゲット設定を開始**」をタップまたはクリックします。
1. Select **Resume Live Copy** from the drop-down menu in the toolbar.

   ![ライブコピーの再開](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. 「**再開**」をタップまたはクリックして、ライブコピーの継承を再開するかどうかを確認します。継承を再開すると、現在のアクティビティに加えていた変更は失われます。

## 領域の削除 {#deleting-areas}

領域を削除すると、その領域内のアクティビティがすべて削除されます。領域を削除する前に警告が表示されます。サイトがリンクされている領域を削除すると、このブランドのマッピングが自動的にマスター領域に再マップされます。

領域を削除するには：

1. Navigate to **Personalization** > **Activities** or **Offers** and then your brand.
1. 削除する領域の横のアイコンをタップまたはクリックします。
1. 「**削除**」をタップまたはクリックし、その領域を削除することを確認します。
