---
title: コンポーネントコンソール
description: コンポーネントコンソールを使用すると、インスタンスに対して定義されたすべてのコンポーネントを参照できます
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# コンポーネントコンソール {#components-console}

コンポーネントコンソールでは、インスタンスに対して定義されたすべてのコンポーネントを参照し、各コンポーネントの主要な情報を表示できます。

It can be accessed from **Tools ->** **General ->** **Components**. コンポーネントにはツリー構造がないので、リストビューのみを使用できます。

![コンポーネントコンソール](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>コンポーネントコンソールには、システム内のすべてのコンポーネントが表示されます。 The [Component Browser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) shows components that are available to authors and hides any component groups that begin with a period ( `.`).

## 検索 {#search-field}

**コンテンツのみ**&#x200B;アイコン（左上）を使用して&#x200B;**検索**&#x200B;パネルを開き、コンポーネントを検索およびフィルタリングできます。

![コンポーネントコンソールでの検索](/help/sites-cloud/authoring/assets/components-console-search.png)

### コンポーネントの詳細 {#component-details}

特定のコンポーネントの詳細を表示するには、必要なリソースをタップまたはクリックします。次の 3 つのタブが表示されます。

* **プロパティ**

   ![コンポーネントコンソールのプロパティ](/help/sites-cloud/authoring/assets/components-console-properties.png)

   「プロパティ」タブでは、次のことができます。

   * コンポーネントの一般的なプロパティの表示。
      * View how the icon or abbreviation has been defined for the component. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * アイコンのソースをクリックすると、そのコンポーネントが表示されます。
   * コンポーネントの&#x200B;**リソースタイプ**&#x200B;および&#x200B;**リソースのスーパータイプ**（定義されている場合）の表示。
      * リソースのスーパータイプをクリックすると、そのコンポーネントが表示されます。
   >[!NOTE]
   >
   >Because `/apps` is not editable at runtime, the Components Console is read-only.

* **ポリシー**

   ![コンポーネントコンソールポリシー](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **ライブ使用状況**

   ![コンポーネントのライブ使用](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >この表示で収集される情報の性質から、照合および表示には時間がかかることがあります。

* **ドキュメント**

   開発者がコンポーネント用ドキュメントを提供している場合、「**ドキュメント**」タブに表示されます。If there is no documentation available, the **Documentation** tab will not be shown. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![コンポーネントドキュメント](/help/sites-cloud/authoring/assets/components-console-documentation.png)
