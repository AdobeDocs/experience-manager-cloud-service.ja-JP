---
title: ページの整理
description: AEM で web サイトを整理する方法について説明します。
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 9a700e9eb3116252f42bb08db9dadc0e8a6adbf7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 100%

---


# ページの整理 {#creating-and-organizing-pages}

AEM で web サイトを整理する方法について説明します。ページをどのように整理する必要があるかを理解したら、[新しいページを作成](/help/sites-cloud/authoring/sites-console/creating-pages.md)し、[既存のページを管理](/help/sites-cloud/authoring/sites-console/managing-pages.md)できます。

## サイトの管理 {#organizing-your-site}

作成者は、AEM 内でサイトを整理する必要があります。この作業中に、次の目的でコンテンツページを作成して名前を付けます。

* 作成者がオーサー環境でコンテンツページを容易に検索できるようにする
* サイトへの訪問者がパブリッシュ環境でコンテンツページを容易に閲覧できるようにする

コンテンツの整理に役立つ[フォルダー](#creating-a-new-folder)を使用することもできます。

Web サイトの構造は、コンテンツページを保持するツリーと見なすことができます。これらのコンテンツページの名前は、URL の作成に使用されます。一方、タイトルは、ページコンテンツを表示したときに表示されます。

以下に、スケートパーク（`la-skateparks`）に関する記事にアクセスする [WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)サイトの例を示します。

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

この構造は [**Sites** コンソール](/help/sites-cloud/authoring/sites-console/introduction.md)から表示でき、web サイトのページ間を移動したり、ページ上でアクションを実行したりできます。

## ページ命名規則 {#page-naming-conventions}

ページを作成する際の主要なフィールドは 2 つあります。

* **[タイトル](#title)**：
   * これはコンソール内のユーザーに、編集中のページコンテンツの上部に表示されます。
   * このフィールドは必須です。
* **[名前](#name)**：
   * これは URI の生成に使用されます。
   * このフィールドへの入力はオプションです。指定しない場合、名前はタイトルから派生します。詳しくは、次の節、[ページ名の制限事項とベストプラクティス](#page-name-restrictions-and-best-practices)を参照してください。

### ページ名の制限事項とベストプラクティス {#page-name-restrictions-and-best-practices}

ページの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;は個別に作成できますが、次のように関連しています。

* ページを作成する場合、「**タイトル**」フィールドは必須です。ページの作成時に&#x200B;**名前**&#x200B;が指定されない場合、AEM はタイトルの最初の 64 文字から名前を生成します（以下で設定する条件に従う）。ページ名を短くするというベストプラクティスに対応するため、最初の 64 文字のみが使用されます。
* 作成者がページ名を手動で指定する場合は、64 文字の制限は適用されませんが、ページ名の長さに関するその他の技術的制限が適用されることがあります。

>[!TIP]
>
>ページ名を定義するときは、ページ名をできるだけ簡潔にしつつ、読者がわかりやすいようにできるだけ表現力のある覚えやすいものにすることをお勧めします。詳しくは、[ 要素の ](https://www.w3.org/Provider/Style/TITLE.html)W3C スタイルガイド`title`を参照してください。
>
>また、一部のブラウザー（旧バージョンの IE など）では、特定の長さまでの URL しか受け付けないので、ページ名を短くするには技術的な理由もあります。

ページを作成するとき、AEM では AEM と JCR によって課された[規則に基づいてページ名が検証](/help/implementing/developing/introduction/naming-conventions.md)されます。

使用できる最低限の文字は次のとおりです。

* `a` から `z` まで
* `A` から `Z` まで
* `0` から `9` まで
* `_`（アンダースコア）
* `-`（ハイフン／マイナス記号）

許可されるすべての文字について詳しくは、[命名規則](/help/implementing/developing/introduction/naming-conventions.md)を参照してください。

>[!NOTE]
>
>ページ名は 150 文字までに制限されています。

### タイトル {#title}

ページを作成するときにページの&#x200B;**タイトル**&#x200B;のみを指定した場合、AEM ではページの&#x200B;**名前**&#x200B;がこの文字列から派生され、AEM と JCR によって課された[規則に基づいてページ名が検証](/help/implementing/developing/introduction/naming-conventions.md)されます。

「**タイトル**」フィールドに無効な文字が含まれていてもエラーにはなりませんが、派生された名前では、無効な文字が別の文字に置き換えられます。次に例を示します。

| タイトル | 派生した名前 |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### 名前 {#name}

ページを作成するときにページの&#x200B;**名前**&#x200B;を指定すると、AEM では AEM と JCR によって課された[規則に基づいてページ名が検証](/help/implementing/developing/introduction/naming-conventions.md)されます。「**名前**」フィールドに無効な文字は指定できません。AEM で無効な文字が検出されると、フィールドが強調表示され、説明メッセージが表示されます。

![無効なページ名の入力例](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>ISO-639-1 で定義されている 2 文字コードをページ名として使用することは避けてください（言語ルートの場合を除く）。
>
>詳しくは、[翻訳するコンテンツの準備](/help/sites-cloud/administering/translation/preparation.md)を参照してください。

## テンプレート {#templates}

AEM では、[テンプレート](/help/sites-cloud/authoring/page-editor/templates.md)は、作成中のあらゆる新規ページの基礎として使用される特殊なタイプのページです。

テンプレートによって、サムネール画像やその他のプロパティなど、ページの構造が定義されます。例えば、商品ページ、サイトマップおよび問い合わせ先に、それぞれ別のテンプレートを使用することができます。テンプレートは、[コンポーネント](#components)で構成されています。

AEM では、複数のテンプレートが標準提供されています。使用できるテンプレートは、個々の web サイトによって異なります。主なフィールドは次のとおりです。

* **タイトル** - 生成される web ページに表示されるタイトルです。
* **名前** - ページに名前を付ける際に使用されます。
* **テンプレート** - 新しいページを生成する際に使用できるテンプレートのリストです。

## コンポーネント {#components}

[コンポーネント](/help/implementing/developing/components/overview.md)は、AEM で提供される、特定のタイプのコンテンツを追加できる要素です。AEM には、包括的な機能を提供する[コアコンポーネント](/help/implementing/developing/components/overview.md#core-components)と呼ばれる、一連のコンポーネントが標準提供されています。コンポーネントの例を以下に示します。

* テキスト
* 画像
* タイトル
* カルーセル
* その他多数

ページを作成して開くと、[コンポーネントブラウザー](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)から使用可能な[コンポーネントを使用してコンテンツを追加](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component)できます。

>[!TIP]
>
>[コンポーネントコンソール](/help/sites-cloud/authoring/components-console.md)は、インスタンス上のコンポーネントの概要を示します。
