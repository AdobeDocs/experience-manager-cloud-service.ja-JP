---
title: 非表示条件の使用
description: 非表示の条件を使用して、コンポーネントリソースをレンダリングするかどうかを決定できます。
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 100%

---

# 非表示条件の使用 {#using-hide-conditions}

非表示の条件を使用して、コンポーネントリソースをレンダリングするかどうかを決定できます。その一例として、テンプレート作成者が[テンプレートエディター](/help/sites-cloud/authoring/page-editor/templates.md)でコアコンポーネントの[リストコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=ja)を設定し、子ページに基づいてリストを作成するオプションの無効化を決定する場合があります。デザインダイアログでこのオプションを無効にすると、リストコンポーネントのレンダリング時に非表示の条件が評価され、子ページを表示するオプションが表示されないようにプロパティが設定されます。

## 概要 {#overview}

オプションのごく一部しか使用しないユーザーにとって、多数のオプションが表示されたダイアログは非常に複雑になります。これにより、ユーザーが圧倒されるようなユーザーインターフェイスのエクスペリエンスになってしまう可能性があります。

管理者、デベロッパー、スーパーユーザーは、非表示の条件を使用することで、一連のルールに基づいてリソースを非表示にできます。この機能を使用すると、作成者がコンテンツを編集する際に表示されるリソースを決定できます。

>[!NOTE]
>
>式に基づいたリソースの非表示は、ACL アクセス権限の代わりにはなりません。コンテンツは編集可能なまま、表示されなくなるだけです。

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
* 関数（必要な場合）は、サービスによって提供される所定のセットに限られます。

## 例 {#example}

非表示の条件の例は、AEM 全体（特に、[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)）で確認できます。例えば、[WKND チュートリアル](/help/implementing/developing/introduction/develop-wknd-tutorial.md)で実装されている[リストコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=ja)について考えてみましょう。

[テンプレートエディターを使用](/help/sites-cloud/authoring/page-editor/templates.md)した場合、テンプレート作成者は、ページ作成者が利用できるリストコンポーネントのオプションをデザインダイアログで定義できます。リストを静的リストにするか、子ページのリストにするか、タグ付きページのリストにするかなどを指定するオプションを有効または無効にできます。

テンプレート作成者が子ページオプションを無効にすると、デザインプロパティが設定され、非表示の条件がそのプロパティに対して評価されます。その結果、このオプションはページ作成者には表示されません。

1. デフォルトでは、ページ作成者は、リストコアコンポーネントでオプション「**子ページ**」を選択して、子ページを使用したリストを作成できます。

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
