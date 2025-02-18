---
title: ユニバーサルエディター 2025.02.17 リリースノート
description: ユニバーサルエディターの 2025.02.17 リリースのリリースノートです。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c88aa13c6bc75c8f9cd624d00ef768290981c840
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 23%

---


# ユニバーサルエディター 2025.02.17 リリースノート {#release-notes}

ユニバーサルエディターの 2025 年 2 月 17 日リリースのリリースノートです。

>[!TIP]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについて詳しくは、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md)を参照してください。

## 新機能 {#what-is-new}

* **プレビューへの公開** - [ コンテンツを公開（または非公開）する際に ](/help/sites-cloud/authoring/universal-editor/publishing.md) ユニバーサルエディターを使用して、パブリッシュ環境に加えて、[ プレビュー環境 ](/help/sites-cloud/authoring/sites-console/previewing-content.md) に公開するかどうかを選択できるようになりました
   * これにより、公開する前にコンテンツをレビューできます。
* **モデルとフィルターはコンポーネント定義で定義できます** - コンポーネントが使用するモデルとフィルターをコンポーネント定義で定義できるようになりました [。](/help/implementing/universal-editor/component-definition.md#template)
   * この情報は、定義内で一元的に管理でき、実装を指定する必要はありません。
   * これにより、コンテナ間でコンポーネントを移動できます。
* **コンテナの子要素は、暗黙的にコンポーネントと見なされます** - [`data-aue-resource`](/help/implementing/universal-editor/attributes-types.md#data-properties) コンテナを持つ項目が直接の子としてコンテナに配置される場合、その項目はコンポーネントと見なされ、`data-aue-behavior="component"` を指定せずに移動できます。

## その他の改善点 {#other-improvements}

* **AEM 6.5 アセットセレクター** - [AEM 6.5 でユニバーサルエディターを実行 ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) すると、6.5 アセットセレクターが正しく開くようになりました
