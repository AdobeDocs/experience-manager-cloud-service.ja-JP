---
title: フォームへの繰り返し可能なセクションの追加
description: EDS フォームへの繰り返し可能なセクションの追加
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: ht
source-wordcount: '531'
ht-degree: 100%

---

# フォームへの繰り返し可能なセクションの追加

アダプティブフォームブロックには、フォームのセクションまたはコンポーネントを追加する機能や繰り返し可能にする機能が用意されています。これにより、ユーザーは同じタイプのデータに対して複数回情報を入力し、職歴や学歴などの情報を簡単に収集できるようになります。

例えば、ある人物の職歴に関する情報を収集するために使用するフォームについて考えてみましょう。前の各職務の詳細を取得するための繰り返し可能なセクションがある場合があります。繰り返し可能なセクションには、通常、会社名、役職、雇用日、職務責任などのフィールドが含まれます。繰り返し可能なセクションの複数のインスタンスを追加して、保持している各ジョブに関する情報を入力できます。

この記事を最後まで読むと、以下の操作を実行できるようになります。

- [フォームでの繰り返し可能なセクションの作成](#add-repeatable-sections-to-a-form)
- [フォームへの最小繰り返し回数と最大繰り返し回数の設定](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 繰り返し可能なセクションの作成

フォームに繰り返し可能なセクションを作成すると、ユーザーは同じデータセットの複数のインスタンスを入力し、繰り返し情報を効率的に収集できます。フォームに繰り返し可能なセクションを作成するには、次の手順に従います。

1. Microsoft SharePoint または Google Workspace 上の Edge 配信プロジェクトフォルダーに移動し、スプレッドシートを開きます。

1. `type` プロパティを `fieldset` に設定してフォームフィールドを追加します。
1. フィールドの `Name` を指定します。名前プロパティは、繰り返し可能なセクションの作成に使用します。
1. `repeatable` を `true` に設定して繰り返し可能を有効にします。
1. フィールドに `label` の説明を指定します。これは、繰り返し可能なセクションの見出しとして機能します。

   求人申込フォーム内の職歴セクションの図については、以下の画像を参照してください。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. セクションに含めるフィールドごとに、その `Fieldset` プロパティを手順 3 で選択したのと同じ名前に設定します。

   例えば、`employment history` セクションに含めるすべての関連フィールドの Fieldset プロパティに `experience` を指定します。

   ![繰り返し可能なセクションフィールドとそのプロパティの例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してシートをプレビューし、公開します。繰り返し可能なセクションがフォームに追加されます。

   繰り返し可能なセクションの下には、直感的な「**追加**」ボタンがあり、複数のセクションを簡単に追加できます。

   ![繰り返し可能なセクションの「追加」ボタンで複数のセクションを追加](/help/edge/assets/repeatable-section-example.png)


## 最小繰り返し回数と最大繰り返し回数の設定

フォームデザインでは、繰り返し可能なセクションの最小繰り返し回数と最大繰り返し回数を設定すると有益です。これにより、ユーザーを効果的にガイドしながら、制御と一貫性を確立できます。最小繰り返し回数または最大繰り返し回数を設定するには、以下の手順に従います。

1. Microsoft SharePoint または Google Workspace 上の Edge 配信プロジェクトフォルダーに移動し、スプレッドシートを開きます。

1. `type` が `fieldset` で、`repeatable` プロパティが `true` に設定されているフィールドの場合：

   - `min` プロパティを設定して、セクションを繰り返すことができる最小回数を指定します。

   - `max` プロパティを設定して、セクションを繰り返すことができる最大回数を指定します。

   ![min プロパティと max プロパティを設定して、セクションを繰り返すことができる回数を指定](/help/edge/assets/repeatable-section-set-min-max.png)

1. [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) を使用してシートをプレビューし、公開します。

   繰り返し可能なセクションを追加すると、ユーザーは直感的な「**削除**」アイコンを見つけて、繰り返し可能なセクションを簡単に削除できます。これらのセクションを追加すると、`min` プロパティで指定したインスタンス数よりも少ないインスタンスに減らすことはできません。これにより、フォームの完成のために設定された最小要件が確実に遵守されます。


