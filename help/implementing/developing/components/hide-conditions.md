---
title: 非表示条件の使用
description: 非表示条件を使用して、コンポーネントリソースがレンダリングされるかどうかを判断できます。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 60%

---

# 非表示条件の使用 {#using-hide-conditions}

非表示条件を使用して、コンポーネントリソースがレンダリングされるかどうかを判断できます。 例えば、テンプレート作成者がコアコンポーネントを設定する際に、このような状況が発生します [リストコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=ja) 内 [テンプレートエディター](/help/sites-cloud/authoring/features/templates.md) とは、子ページに基づいてリストを作成するためのオプションを無効にすることを決定します。 デザインダイアログでこのオプションを無効にすると、リストコンポーネントのレンダリング時に非表示の条件が評価され、子ページを表示するオプションが表示されないようにプロパティが設定されます。

## 概要 {#overview}

オプションのごく一部しか使用しないユーザーにとって、多数のオプションが表示されたダイアログは非常に複雑になります。これにより、ユーザーのユーザーインターフェイスエクスペリエンスが圧倒的に高まる可能性があります。

非表示条件を使用すると、管理者、開発者およびスーパーユーザーは、一連のルールに基づいてリソースを非表示にできます。 この機能を使用すると、作成者がコンテンツを編集したときに表示するリソースを決定できます。

>[!NOTE]
>
>式に基づいてリソースを非表示にしても、ACL 権限は置き換えられません。 コンテンツは編集可能なままですが、表示されません。

## 実装と使用の詳細 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` は、フィルタリング対象のフィールドの `granite:hide` プロパティの有無と値に基づいてリソースをフィルタリングします。`/libs/cq/gui/components/authoring/dialog/dialog.jsp` の実装には、`FilteringResourceWrapper.` のインスタンスが含まれます。

この実装では、Granite [ELResolver API](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) を利用し、ExpressionCustomizer を介して `cqDesign` カスタム変数を追加します。

以下に、`etc/design` 内かコンテンツポリシーとして配置されているデザインノードの非表示の条件の例をいくつか示します。

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

非表示式を定義する際は、以下の点に留意してください。

* 式を有効にするには、プロパティの検索範囲を表します（例：`cqDesign.myProperty`）。
* 値は読み取り専用です。
* 関数（必要に応じて）は、サービスが提供する特定のセットに限定する必要があります。

## 例 {#example}

非表示の条件の例は、AEM 全体（特に、[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)）で確認できます。例えば、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)で実装されている[リストコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=ja)について考えてみましょう。

[テンプレートエディターを使用](/help/sites-cloud/authoring/features/templates.md)した場合、テンプレート作成者は、ページ作成者が利用できるリストコンポーネントのオプションをデザインダイアログで定義できます。リストを静的リスト、子ページのリスト、タグ付きページのリストなどにするかどうかを指定するオプション。 は、有効または無効にすることができます。

テンプレート作成者が子ページオプションを無効にする場合、デザインプロパティが設定され、非表示の条件がそれに対して評価されるので、ページ作成者に対してオプションがレンダリングされません。

1. デフォルトでは、ページ作成者は、リストコアコンポーネントを使用し、「 」オプションを選択することで、子ページを使用したリストを作成できます **子ページ**.

   ![リストコンポーネントの設定](assets/hide-conditions-list-settings.png)

1. テンプレート作成者は、リストコアコンポーネントのデザインダイアログでオプション「**子の無効化**」を選択して、子ページに基づいたリストを生成するオプションがページ作成者に対して表示されないようにできます。

   ![リストコンポーネントデザインのダイアログ](assets/hide-conditions-list-design.png)

1. `/conf/wknd/settings/wcm/policies/wknd/components/list` の下にポリシーノードが作成され、`disableChildren` プロパティが `true` に設定されます。

   ![非表示条件のノード構造](assets/hide-conditions-node-structure.png)

1. 非表示条件は、ダイアログのプロパティノード `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children` の `granite:hide` プロパティの値として定義されます。

   ![非表示条件の評価](assets/hide-conditions-evaluation.png)

1. `disableChildren` の値がデザイン設定から取得され、式 `${cqDesign.disableChildren}` が `false` と評価されます。つまり、そのオプションはコンポーネントの一部としてレンダリングされません。

1. ページ作成者がリストコンポーネントを使用するときに、オプション「**子ページ**」が表示されなくなりました。

   ![子オプションが無効なリストコンポーネント](assets/hide-conditions-child-disabled.png)
