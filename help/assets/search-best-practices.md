---
title: 検索のベストプラクティス： [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: アプリケーション内でアセットのメタデータを検索、検索および取得するためのベストプラクティス。
contentOwner: KK
exl-id: 446692de-5cea-4dbd-a98e-ec5177c7017e
source-git-commit: a3f7564932e7f9318841623376f62dad91ceca18
workflow-type: tm+mt
source-wordcount: '2544'
ht-degree: 11%

---

# AEM Search のベストプラクティス

[!DNL Adobe Experience Manager Assets] は、コンテンツ速度の向上に役立つ堅牢なアセット検索方法を備えています。適切なアセットの検索が困難で時間がかかる場合があります。 したがって、でのアセット検索機能 [!DNL Adobe Experience Manager Assets] は、デジタルアセット管理システムの中心となる役割を果たします。クリエイティブによるさらなる使用、ビジネスユーザーやマーケターによるアセットの堅牢な管理、DAM 管理者による管理のために使用されます。

このヘルプドキュメントには、AEMユーザーが基本レベルから高度なレベルの検索を実行するのに役立つ様々なシナリオを支援する、AEM検索のベストプラクティスが含まれています。

## アクセスExperience Manager検索 {#access-experience-manager-search}

検索を開始する前にExperience Managerで実行する基本的な手順は次のとおりです。

* Adobe Analytics の **管理ビュー**で、アセット/Experience Manager内のファイルに移動し、上部のバーにある検索アイコンをクリックします。 または、スラッシュ (/) を使用してオムニサーチフィールドを開きます。
Adobe Analytics の **Assets ビュー**&#x200B;の場合、検索バーは上部に表示され、直接アクセスできます。
* `Location:Assets` および `Path:/content/dam` 検索範囲をExperience Manager Assetsリポジトリに制限するように事前に選択されています。 他のフォルダーに移動する場合は、 `Path:/content/dam/<folder name>` をオムニサーチフィールドに表示して、検索範囲を現在のフォルダーに制限します。

## 基本検索 {#basic-search}

**シナリオ 1: `classic car` を検索キーワードとして使用します。**

キーワード検索では、大文字と小文字が区別されず、アセットに含まれているメタデータフィールド全体の全文検索です *全文検索* index （インデックス定義で設定可能） 複数のキーワードを使用する場合は、 **AND はキーワード間のデフォルトの演算子なので、「クラシックカー」の検索を「クラシック AND カー」と見なします**.

メタデータフィールド内のすべての検索語句に一致する検索結果がまず表示され、次にスマートタグ内のいずれかの検索語句に一致する検索結果が表示されます。検索結果の表示順は、次のとおりです。

1. 各種メタデータフィールド内の「`Classic Car`」に一致するもの。
2. スマートタグ内の「`Classic Car`」に一致するもの。
3. スマートタグ内の「`Classic`」または「`Car`」に一致するもの。

指定 `classic car` を検索キーワードとして選択し、「検索」をクリックします。 サーチクエリは、キーワードを入力するとドロップダウンリストに表示されます。 検索候補は、Experience Managerデプロイメント上の検索インデックスの内容に基づいて表示されます。 ドロップダウンメニューに適切なアセットが表示されない場合は、Enter キーを押して結果のリストを表示します。 結果は、最も近い一致から順に、関連度の高い順に並べ替えられます。

![基本検索方法 1 の実行](assets/simple-search-1.png)

検索キーワードを二重引用符 (&quot; &quot;) で囲むと、より具体的に検索できます。 この検索には、指定した用語をまとめて含むアセットのみが含まれます。 検索条件は次のようになります。 `"classic car"`. したがって、両方の語句で検索結果が一致します `classic` および `car` が表示されます。

![完全一致の検索](assets/simple-search-2.png)

検索では、 **[!UICONTROL Assets ビュー]** 同様に。

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3425489)
-->

## ファイルとフォルダー {#files-folders}

**シナリオ 2: `classic car` キーワードを `automobile` フォルダー。**

ファイルとフォルダーのフィルターを使用して、検索を絞り込むことができます。 必要に応じて、ドロップダウンリストの「ファイル」、「フォルダー」、「ファイルとフォルダー」オプションを使用します。 [ ファイル ]、[ フォルダ ]、[ ファイルとフォルダ ] から選択するオプションは、 **[!UICONTROL 管理ビュー]** のみ。 Adobe Analytics の **[!UICONTROL Assets ビュー]**&#x200B;に移動します。 [!UICONTROL パス] をクリックし、検索を実行するフォルダを参照します。

* 以下を使用します。 **[!UICONTROL ファイル]** 」オプションを使用します。 定義されたパス内でフォルダーを検索する必要はありません。
* 以下を使用します。 **[!UICONTROL フォルダー]** 」オプションを使用します。
* 以下を使用します。 **[!UICONTROL ファイルとフォルダー]** 」オプションを使用します。

このシナリオを実現するには、次の手順を実行します。

1. 指定 `classic car` を検索キーワードとして選択し、「検索」をクリックします。
2. 「フィルター」をクリックし、 `automobile` フォルダー。 例： `/content/dam/multiple-assets/automobile`
パスからフォルダーを選択し、特定のフォルダー内を検索する場合は必要なフォルダーに移動します。
3. ドロップダウンリストから「ファイル」を選択して、キーワードを含むすべてのファイルを表示します。 `classic car`.

![ファイルとフォルダーを使用した検索](assets/files-folders.png)

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3425487)
-->

## 演算子 {#operators}

**シナリオ 3：を検索する `Classic Car` または `Car` キーワードを使用して検索を絞り込むことができます。**

上記のシナリオを **[!UICONTROL 管理ビュー]**&#x200B;を使用すると、様々な演算子を組み合わせて検索エクスペリエンスを強化できます。 次の演算子がサポートされます。

### AND 演算子 {#and-operator}

AND 演算子は、オムニサーチの 2 つのキーワード間のデフォルトの演算子です。 例えば、 `classic car` 検索バーで、 `classic` および `car` キーワードは、デフォルトで検索結果に表示されます。

![AND 演算子を使用した検索](assets/simple-search-1.png)

### OR 演算子 {#or-operator}

検索結果に特定の値を指定し、検索結果にオプションを含める場合は、OR 演算子を使用できます。 例えば、 `classic OR car` キーワードは、検索結果のメタデータにキーワードのいずれかを含めて表示します。

![OR 演算子を使用した検索](assets/or-operator.png)

### NOT 演算子 {#not-operator}

一部のキーワードを除く結果を取得する場合は、NOT 演算子を使用できます。 NOT 演算子は、ハイフン (-) 記号を使用して、検索結果から除外する対象をAEMで検索するよう指示します。 例えば、 `car - classic` を含むメタデータを指定する検索クエリ `car` ただし、 `classic`.

![NOT 演算子を使用した検索](assets/not-operator.png)

同様に、すべての車を検索できますが、ジープは検索できません。 クエリは次のようになります。 `car - jeep`. メタデータを含むすべてのアセットが表示されます `car` ただし、メタデータを含むアセットは除外されます `jeep`.

![NOT 演算子を使用した検索](assets/images-jeep.png)

**[!UICONTROL Assets ビュー]** は演算子の使用をサポートしていません。

## ワイルドカード {#wildcards}

検索で 1 つ以上の文字を置き換える場合は、ワイルドカードを使用します。 上記のシナリオを **[!UICONTROL 管理ビュー]**&#x200B;の場合は、様々なワイルドカードを組み合わせて使用し、検索機能を強化できます。 検索の実行に使用するワイルドカードは 2 つあります。疑問符 (?) アスタリスク (*) 疑問符記号は 1 文字を検索するために使用され、アスタリスク記号は複数の文字を検索するために使用されます。

### 疑問符 (?) {#question-mark}

疑問符記号を条件演算子として使用して、検索を容易にすることができます。Experience Manager

* `car?` クエリは、car の後に 1 文字がある単語と一致します。 例：買い物かご。
* `?car` クエリは、car の前に 1 文字ある単語と一致します。 例えば、傷。
* `car????` クエリは、car の後に 4 文字がある単語と一致します。 例えば、洗濯。

### アスタリスク (*) {#asterisk}

アスタリスクは、文字数を少なく入力して検索の範囲を広げるために使用するワイルドカード演算子です。 検索するアセットの開始文字がわかっていて、その他の文字がわからない場合は、検索でアスタリスク演算子を使用できます。 例えば、 `*car` クエリの場合、メタデータで使用可能な postfix car を含むすべてのアセットが返されます。 結果は、クラシックカー、スポーツカー、クラシックカー、スポーツカーなどです。 次に、様々な方法でアスタリスク演算子を使用した例をいくつか示します。

* `*car*`：可能なあらゆる組み合わせを含んだアセットを返します。
* `car*` は、カーウォッシュ、運送業者、運送業者などを含むアセットを返します。
* `*car` は、最新の車やスポーツカーなどのアセットを返します。

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3425488)
-->

**[!UICONTROL Assets ビュー]** では、ワイルドカードの使用はサポートされていません。

## フィルター {#filters}

Adobe Experience Managerには様々な検索フィルターが用意されており、スコープクエリを使用して検索を絞り込み、セグメント化できます。 アセットのタイトルやメタ説明が不明な場合は、様々な検索フィルターを使用して、より関連性の高い検索をおこなうことができます。 検索フィルターは、キーワードを入力した場合と入力しなかった場合でも使用できます。 でフィルターパネルを開くには、以下を実行します。 **[!UICONTROL 管理ビュー]**&#x200B;をクリックし、 **GlobalNav** アイコンと選択 **[!UICONTROL フィルター]**. 一方、でフィルターパネルを開くには、 **[!UICONTROL Assets ビュー]**&#x200B;をクリックし、 [!UICONTROL フィルター] をクリックします。

![フィルターパネル](assets/filters.png)

1 つまたは複数のフィルターを選択して、Adobe Experience Managerでの検索を絞り込むことができます。
<!--The following filters are available out of the box for all the users of Experience Manager:

* File Type Search Filters  
* File Size Search Filters 
* Date of Creation 
* Created by 
* Last Modified date 
* Last Modified by 
* Search by Language 
* Search by Status 
* Search based on Orientation 
* Search by Style 
* Search based on insights 
* Search by Adobe Stock 
* Color specific Asset search 
* Content fragment model 
 -->

<!--**Scenario 5: Search for an Asset named 'classic car' in Black color which has either meta description or a similar asset in Japanese language.**  
 
To perform a search on such a requirement, type 'classic car' in the search bar.  Navigate to the filters panel and expand the language search filter drop-down. Type "ja-jp", which represents the Japanese language. Expand the 'Asset Color' filter and select black color or add the hexadecimal code for the black color (#000000).

![Filter example 1](assets/filter-1.png)
-->

**シナリオ 4：を使用して、未公開のPDFファイルタイプのドキュメントを検索する `classic car` キーワードを含めています。**

で次の手順を実行します。 **[!UICONTROL 管理ビュー]**:

1. タイプ `classic car` をクリックします。
1. 「フィルター」に移動します。 の下 [!UICONTROL ファイルタイプ]、展開 [!UICONTROL ドキュメント]を展開します。 [!UICONTROL ワードプロセッシング].
1. 選択 [!UICONTROL PDF].
1. に移動します。 [!UICONTROL ステータス] > [!UICONTROL 公開] > [!UICONTROL 非公開].

![フィルターの例 2](assets/filter-2.png)

で次の手順を実行します。 **[!UICONTROL Assets ビュー]**:

1. タイプ `classic car` をクリックします。
1. 「フィルター」に移動します。 の下 [!UICONTROL MIME タイプ]を選択します。 [!UICONTROL PDF].
1. に移動します。 [!UICONTROL アセットステータス]を選択します。 [!UICONTROL すべて] をクリックして、公開済みおよび非公開のアセットをすべて含めます。

**シナリオ 5:PNG を除くすべての画像を検索する**

アセットのタイトルやメタ説明が不明な場合は、様々な検索フィルターを使用して、より関連性の高い検索をおこなうことができます。 例えば、でアセットを検索するには、次のようにします。 **[!UICONTROL 管理ビュー]**、次の手順に従います。

1. 検索フィルターに移動します。
1. 「フィルター」に移動します。 の下 [!UICONTROL ファイルタイプ]、展開 [!UICONTROL 画像] を選択し、 [!UICONTROL Web 有効]
1. 「PNG」の選択を解除します。

![ジープ以外のすべての画像を検索](assets/images-png.png)

の前述のシナリオを使用してアセットを検索するには **[!UICONTROL Assets ビュー]**、次の手順に従います。

1. 検索フィルターに移動します。
1. 「フィルター」に移動します。 の下 [!UICONTROL MIME タイプ]「 」を選択し、「 PNG の選択を解除」を除くすべての指定した MIME タイプを選択します。

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3425486)
-->

## 詳細検索 {#advanced-search}

AEM検索を使用すると、手間をかけずに複雑な検索クエリを作成できます。 複雑な検索クエリを作成する際に役立つ様々な例を次に示します。

**シナリオ 6：を使用して、Experience Managerリポジトリ内のすべてのドキュメントを検索する `classic car` をメタデータに含めます。 ドキュメントのコンテンツには、 `classic car` キーワードを含めています。**

Adobe Experience Managerでは、検索に複数の条件を追加できます。 キーワード、演算子およびフィルターを組み合わせて使用して、検索結果を絞り込むことができます。

シナリオ 6 の検索を実行するには：

1. 次を入力します。 `classic car` キーワードを使用します。
2. フィルターパネルに移動し、「ファイルタイプ」の下の「ドキュメント」を選択します。
3. アスタリスクワイルドカードを使用して検索を絞り込みます。 タイプ `"classic car"` を含むすべてのアセットを検索するには `classic car` キーワード。

![シナリオ 6](assets/scenario-6.png)

シナリオ 6 はで実行できません **[!UICONTROL Assets ビュー]** ワイルドカードの使用はサポートされていないので、

**シナリオ 7：ドキュメントのコンテンツに含める必要があるExperience Managerリポジトリ内のすべてのドキュメントを検索する `car` 除外する `classic`. 同じ条件がアセットのメタデータにも当てはまります。**

シナリオ 7 の検索を実行するには：

次を入力します。 `car - classic` キーワードを使用します。 フィルターパネルに移動し、「ファイルタイプ」の下の「ドキュメント」を選択します。 検索の優先順位は、次の順序に基づきます。優先度 1：メタデータ優先度 2：スマートタグ

![シナリオ 7](assets/scenario-7.png)

シナリオ 7 はで実行できません **[!UICONTROL Assets ビュー]** ワイルドカードの使用はサポートされていないので、

<!--
**Scenario 9: Search for all images except PNG**

When you are unsure about the title or meta description of an asset, you can use various search filters to make your search more relevant. Follow the steps below:

1. Go to search filters. 
1. Under [!UICONTROL File Type], expand [!UICONTROL Images] and select [!UICONTROL Web enabled]
1. Deselect PNG.

**Method 1:** Go to search bar and type `images - PNG`. All the images appear excluding PNG.

**Method 2:** Go to search filters. Under [!UICONTROL File Type], expand [!UICONTROL Images] > select [!UICONTROL Web enabled] > deselect PNG.

![Search all images except jeep](assets/images-jeep.png)
-->

**シナリオ 8：メタデータジープを含むメタデータタグの検索**

様々な検索フィルターを使用して、特定の条件をキャプチャできます。 タグとは、多数のアセットの中で識別可能にするためにアセットに割り当てられるキーワードです。 例えば、このシナリオでは、を含むアセットを検索します。 *ジープ* タグを追加します。 これをおこなうには、次のように入力します。 `tags:jeep` をクリックします。 この条件を満たすアセットのみが検索結果に表示されます。

![タグを使用した検索](assets/search-tags.png)

検索では、 **[!UICONTROL Assets ビュー]** 同様に。

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3425490)  
-->

**シナリオ 9：赤い色の車に類似した一致を見つける**

AEMで検索を実行する際に、選択したアセットに類似したアセットを表示することで、結果をフィルタリングできます。 以下を使用すると、 **類似を検索** 」オプションを使用して、検索したアセットの完全一致または類似一致に検索を絞り込みます。 これは、選択したアセットと類似したスマートタグを持つアセットを検索するのに役立ちます。 例えば、類似したアセットを検索する場合は、次の手順を実行します。

1. 必要に応じてアセットを検索します。
1. アセットの上にマウスポインターを置き、省略記号/選択をクリックします。 [!UICONTROL 類似を検索].
または、アセットを選択し、右上の省略記号に移動して「 」を選択します。 [!UICONTROL 類似を検索].

   ![類似を検索](assets/find-similar.png)

1. 検索バーに注目してください。 選択したアセットのサムネールが、検索要件を示す検索バーに表示されます。 その結果、類似したスマートタグを持つアセットが返されます。

**[!UICONTROL Assets ビュー]** はをサポートしていません [!UICONTROL 類似を検索] オプション。

## カスタム検索ファセット {#custom-search-facets}

Adobe Experience Managerの検索ファセットを使用すると、事前に決定された単一の検索や分類上の順序ではなく、複数の方法でアセットを検索できます。 必要に応じて、検索ファセットをカスタマイズし、述語を追加できます。 読み取り [検索ファセット](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=ja#) カスタム述語の追加手順を説明するガイドです。

<!--**Scenario 10: Search assets based on Sku ID**
to be added later
-->

**シナリオ 10：最終変更日または有効期限に基づいて特定のアセットを検索する**

日付制約を使用すると、例えば期間検索フィルターを使用して、カスタム検索を特定の期間に絞り込むことができます。 上記の要件を検索するには、「 」と入力します。 `classic car` をクリックします。 期間を [!UICONTROL 作成日] および [!UICONTROL 最終変更日] 日付フィルター。

![日付フィルター](assets/date-filters.png)

検索では、 [!UICONTROL Assets ビュー] 同様に。

## キーワードの関連性の向上 {#boosting-keywords}

特定のアセットに対するキーワードの関連性を高めることで、キーワードに基づいた検索を強化できます。つまり、特定のキーワードに基づいて検索すると、それらのキーワードの対象となる画像が検索結果の最上部に表示されます。

1. Assets ユーザーインターフェイスから、アセットのプロパティページを開きます。「[!UICONTROL 詳細]」をクリックし、「[!UICONTROL 検索キーワードに採用]」の下の「[!UICONTROL 追加]」をクリックします。
2. 「昇格を検索」ボックスで、画像検索時の強化の対象となるキーワードを指定し、「[!UICONTROL 追加]」をクリックします。同じ方法で複数のキーワードを指定できます。
3. 「[!UICONTROL 保存して閉じる]」をクリックします。昇格したこのキーワードの対象となるアセットが、検索結果の上位に表示されます。

## 検索を実行する際の主なExperience Manager {#notable-things}

* アセットのメタデータ情報を提供し、オムニサーチアルゴリズムで検索可能なアセットを準備します。 アセットのメタデータ情報が更新されていることを確認します。
* 二重引用符 (&quot; &quot;) を使用して、検索を正確にし、ポイントを指定します。
* 探しているパスをクロスチェックします。 フォルダー、ファイル、またはファイルとフォルダーの中から適切なオプションを選択し、適切な場所で検索クエリを実行します。
* オムニサーチバーで、検索に適用するフィルターを確認できます。
* 結果が得られない場合は、探しているパスをクロスチェックします。 また、検索元のフォルダーを確認します。 例えば、「自動車のフォルダー」内で検索を実行しているが、使用しているキーワードが「アパレル」に関連している場合、検索結果は不適切です。
* 検索するキーワードの前に空白が追加された場合は、チェックインします。
* キーワード、演算子、フィルターを組み合わせて使用すると、検索操作を容易にし、レベルアップできます。

<!--
* Use stemming search approach while searching for the asset. It means using an exact keyword that you are looking for.
* Specify Smart tags to the asset properties to boost the ranking of the search results.
The newly added assets are not indexed.
-->

## の違い [!UICONTROL 管理ビュー] および [!UICONTROL Assets ビュー] 検索 {#differences-asset-and-admin-view}

<table>
    <tr>
        <th> パラメーター </th>
        <th> 管理ビュー </th>
        <th> アセットビュー </th>
    </tr>
    <tr>
        <td> カスタムファセット </td>
        <td> 次の項目を追加できます。 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=ja">必要に応じて、カスタム検索ファセットを設定します。</td>
        <td> カスタムファセットは Assets ビューで部分的にサポートされています。 サポートされるファセットは次のとおりです。
            <ul>
            <li> 予測されたタグ
            <li> 名前
            <li> 予測されたタグの信頼性
            <li> アセットサイズ
            <li> タイトル
            </ul>
        </td>
    </tr>
    <tr>
        <td> 演算子 </td>
        <td> AND、OR、NOT をサポート </td>
        <td> サポート対象外 </td>
    </tr>
    <tr>
        <td> ワイルドカード </td>
        <td> 疑問符 (?) をサポート アスタリスク (*)</td>
        <td> サポート対象外 </td>
    </tr>
    <tr>
        <td> 検索結果の向上 </td>
        <td> サポート対象 </td>
        <td> サポート対象外 </td>
    </tr>
     <tr>
        <td> すべてのフィルターを一度にクリア </td>
        <td> サポート対象外 </td>
        <td> サポート対象</td>
    </tr>
     <tr>
        <td> ファイル/フォルダー/ファイルとフォルダー </td>
        <td> サポート対象 </td>
        <td> フォルダを選択するオプションは、「ファイルの種類」の下に表示されます。 </td>
    </tr>
     <tr>
        <td> アセットのステータス </td>
        <td> 
            次のオプションがサポートされています。
            <ul>
            <li> パブリッシュ
            <li> 発行日
            <li> 最終公開者
            <li> 承認 
            <li> チェックアウト
            <li> 有効期限
            <li> Dynamic Media
            </ul>
        </td>
        <td>
        次のオプションがサポートされています。
            <ul>
            <li> すべて
            <li> 承認済み
            <li> 却下
            <li> ステータスなし
            </ul> 
        </td>
    </tr>
     <tr>
        <td> ファイルタイプ </td>
        <td>
        次のオプションがサポートされています。
            <ul>
            <li> 画像
            <li> ドキュメント
            <li> マルチメディア
            <li> アーカイブ 
            </ul>
            これらには、さらに階層的なオプションがあります。
        </td>
        <td>
        次のオプションがサポートされています。
            <ul>
            <li> 画像
            <li> ドキュメント
            <li> ビデオ
            <li> フォルダー 
            </ul> 
        その他のオプションは、「MIME タイプ」の下に表示されます。
        </td>
    </tr>
     <tr>
        <td> ファイルサイズ </td>
        <td>
        次のオプションがサポートされています。
            <ul>
            <li> 開始 — 終了
            <li> サイズ（バイト、KB、MB、GB）
            </ul> 
        </td>
        <td> サポート対象外 </td>
    </tr>
     <tr>
        <td> その他のフィルター </td>
        <td>
            <ul>
            <li> 言語
            <li> ステータス
            <li> 向き
            <li> スタイル 
            <li> インサイト
            <li> Stock
            <li> アセットカラー
            <li> コンテンツフラグメントモデル
            </ul> 
        </td>
        <td> サポート対象外 </td>
    </tr>
     <tr>
        <td> 類似を検索 </td>
        <td> サポート対象 </td>
        <td> サポート対象外 </td>
    </tr>
</table>

>[!MORELIKETHIS]
>
>* [アセットの検索](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/search-assets.html?lang=ja)
>* [検索ファセット](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=ja)
