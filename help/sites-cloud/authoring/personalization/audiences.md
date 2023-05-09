---
title: オーディエンスの管理
description: オーディエンスコンソールを使用して、Adobe Target アカウント用のオーディエンスを作成、整理および管理したり、ContextHub 用のセグメントを管理したりできます。
exl-id: dff72c15-afcd-4b16-a711-e9ca3010e3ec
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 57%

---

# オーディエンスの管理{#managing-audiences}

オーディエンスコンソールを使用して、Adobe Target アカウント用のオーディエンスを作成、整理および管理したり、ContextHub 用のセグメントを管理したりできます。

* オーディエンスの追加 — Adobe Targetオーディエンスまたは ContextHub セグメント。
* オーディエンスの管理 

オーディエンス（ContextHub では「*セグメント*」と呼ぶ）とは、特定の条件によって定義される訪問者のクラスで、ターゲットアクティビティが表示される対象を決定します。アクティビティをターゲット設定する場合は、ターゲット設定プロセスで直接オーディエンスを選択するか、オーディエンスコンソールで新しいオーディエンスを作成できます。

オーディエンスコンソールでは、オーディエンスはブランド別に整理されます。

オーディエンスは、ターゲット設定モードで[ターゲットコンテンツのオーサリング](/help/sites-cloud/authoring/personalization/targeted-content.md)に使用できます。その際、オーディエンスを作成することもできます（ただし、オーディエンスコンソールで Adobe Target オーディエンスを作成する必要があります）。ターゲットモードで作成したオーディエンスは、オーディエンスコンソールに表示されます。

オーディエンスは、定義されているオーディエンスの種類を示すラベルと共に表示されます。

* CH - ContextHub セグメント
* AT - Adobe Targetオーディエンス

## オーディエンスコンソールでの ContextHub セグメントの作成 {#creating-a-contexthub-segment-in-the-audiences-console}

ContextHub セグメントは、オーディエンスコンソールまたはターゲット設定プロセスで作成できます。

オーディエンスコンソールで ContextHub セグメントを作成するには：

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。
1. 「**ContextHub セグメントを作成**」をタップまたはクリックします。

   ![セグメントの作成](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. **新しい ContextHub セグメント**&#x200B;ダイアログボックスで、タイトルを入力し、ブーストを調整して、「**作成**」をクリックします。新しい ContextHub セグメントがオーディエンスリストに表示されます。

   >[!NOTE]
   >
   >新しく作成したオーディエンスがあるか確認するために降順に並べ替えるには、「**変更済み**」をタップまたはクリックして、変更済みのリストを並べ替えることができます。

ContextHub を使用するセグメント作成の詳細については、「ContextHub によるセグメント化の設定」ドキュメントを参照してください。<!--For further detail about creating segments using ContextHub, please see the [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) documentation.-->

## オーディエンスコンソールを使用した Adobe Target オーディエンスの作成 {#creating-an-adobe-target-audience-using-the-audience-console}

オーディエンスコンソールを使用して、Adobe TargetオーディエンスをAEMで直接作成できます。

オーディエンスは、誰がターゲットアクティビティに含まれるかを決定するルールによって定義されます。 オーディエンス定義には複数のルールを含めることができ、各ルールには複数のパラメーターを含めることができます。

複数のルールを使用する場合、これらのルールはブール演算子 AND で結合されます。つまり、任意の潜在的なオーディエンスメンバーが、アクティビティに含めるために定義された条件をすべて満たす必要があります。 例えば、AND を使用して OS ルールとブラウザールールを定義した場合、定義された OS と定義されたブラウザーの両方を使用する訪問者のみがアクティビティに含まれます。

>[!NOTE]
>
>**作成**&#x200B;メニューに「**Target オーディエンスを作成**」が表示されない場合は、オーディエンスの作成に必要な権限がありません。オーディエンスを作成するには、`/etc/segmentation` 下の書き込み権限が必要です。content-authors グループには、デフォルトで書き込み権限があります。

Adobe Target オーディエンスを作成するには：

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。

   ![オーディエンスへの移動](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. オーディエンスコンソールで、「**作成**」、「**ターゲットオーディエンスを作成**」の順にタップまたはクリックします。

   ![ターゲットオーディエンスの作成](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. **Adobe Target 設定**&#x200B;ダイアログボックスで、Target 設定を選択し、「**OK**」をタップまたはクリックします。
1. 「ルール#1」領域で、属性タイプをタップまたはクリックし、使用可能なフィールドに属性情報を入力します。 終了したら、属性の右側にあるチェックマークを選択して保存します。 詳しくは、 [属性とそのオプション](#attributes-and-their-options) を参照してください。
1. 「**ルールを追加**」をクリックして、別のルールを追加します。必要な数だけルールを入力します。複数のルールを指定した場合は、ルールがブール演算子 AND で結合されます。これは、各ルールの要件をすべて満たすオーディエンスだけが、そのアクティビティの対象になるということです。
1. 「**次へ**」をタップまたはクリックします。
1. オーディエンスの名前を入力し、タップまたはクリックします **保存**.
1. 「**保存**」をタップまたはクリックします。オーディエンスがオーディエンスリストに表示されます。

### 属性とそのオプション {#attributes-and-their-options}

次の各属性に対して、ターゲット設定ルールを作成できます。

| **属性** | **説明** | **詳しくは、** |
|---|---|---|
| **モバイル** | モバイルデバイス、デバイスの種類、デバイスのベンダー、画面の寸法（ピクセル単位）などのパラメーターに基づく Target モバイルデバイス。 | 詳しくは、 [モバイルドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=ja) Adobe Targetで |
| **カスタム** | カスタムパラメーターは、mbox パラメーターです。mbox に対して mbox パラメーターを渡した場合、または targetPageParams 関数を使用した場合、それらのパラメーターはここに表示され、オーディエンスで使用できます。 | 詳しくは、 [カスタムパラメータードキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=ja) Adobe Targetで |
| **OS** | 特定のオペレーティングシステムを使用している訪問者をターゲットに設定することができます。 | Linux、Macintosh または Windows を使用しているユーザーをターゲットにします。 |
| **サイトページ** | 特定のページを閲覧している、または特定の mbox パラメーターを持つ訪問者をターゲットに設定します。 | Adobe Target で[サイトページに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=ja)を参照してください。 |
| **ブラウザー** | ページの訪問時に特定のブラウザーまたは特定のブラウザーオプションを使用しているユーザーをターゲットに設定できます。 | Adobe Target で[ブラウザーオプションに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=ja)を参照してください。 |
| **訪問者プロファイル** | 特定のプロファイルパラメーターに一致する訪問者をターゲット設定します。 | Adobe Target で[訪問者プロファイルに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=ja)を参照してください。 |
| **トラフィックソース** | サイトに導いた検索エンジンやランディングページに基づいて訪問者をターゲット設定します。 | Adobe Target で[トラフィックソースに関するドキュメント](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=ja)を参照してください。 |

## オーディエンスコンソールでのオーディエンスの変更 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>編集中のAEMインスタンスと同じ AEM インスタンスで作成されたAdobe Targetオーディエンスのみを編集できます。 異なるAEM環境で作成された Target オーディエンスは編集できません。

ContextHub オーディエンスは、オーディエンスコンソールから編集できます。また、次のように Adobe Target オーディエンスも編集できますが、AEM で作成された Adobe Target オーディエンスのみです。

1. ナビゲーションコンソールで、「**パーソナライズ機能**」をクリックまたはタップします。「**オーディエンス**」をクリックまたはタップします。
1. 編集する ContextHub セグメントの横のアイコンをタップまたはクリックして、「**編集**」をタップまたはクリックします。
1. セグメントエディターで編集を行います。詳しくは、ContextHub のドキュメントを参照してください。<!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
