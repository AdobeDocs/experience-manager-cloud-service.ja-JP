---
title: フォームに繰り返し可能なセクションを追加する
description: EDS フォームに繰り返し可能なセクションを追加する
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 13%

---

# フォームへの繰り返し可能なセクションの追加

アダプティブFormsブロックには、フォームのセクションやコンポーネントを追加または作成する機能が用意されています。 これにより、ユーザーは同じタイプのデータに対して複数回情報を入力でき、職歴や教育的背景などの情報を簡単に収集できます。

例えば、ある人物の職歴に関する情報を収集するために使用するフォームについて考えてみましょう。前の各職務の詳細を取得するための繰り返し可能なセクションがある場合があります。繰り返し可能なセクションには、通常、会社名、役職、雇用日、職務責任などのフィールドが含まれます。繰り返し可能なセクションの複数のインスタンスを追加して、保持している各ジョブに関する情報を入力できます。



この記事を最後まで読むと、以下の操作を実行できるようになります。

* [フォーム内に繰り返し可能なセクションを作成する](#add-repeatable-sections-to-a-form)
* [フォーム内の繰り返しの最小数または最大数を設定する](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 繰り返し可能なセクションの作成

フォーム内に繰り返し可能なセクションを作成すると、ユーザーは同じデータセットの複数のインスタンスを入力でき、繰り返し情報を効率的に収集できます。 フォーム内に繰り返し可能なセクションを作成するには：

1. Microsoft SharePointまたはGoogle Workspace の Edge Deliver プロジェクトフォルダーに移動し、スプレッドシートを開きます。

1. フォームフィールドを追加し、 `type` プロパティをに設定 `fieldset`
1. 指定 `Name` 」と入力します。 name プロパティは、繰り返し可能なセクションの作成に使用されます。
1. 次の設定で再現性を有効にする `repeatable` から `true`.
1. 説明的な `label` フィールドの。 繰り返し可能なセクションの見出しとして機能します。

   以下の画像は、求人申込フォーム内の雇用履歴の節の図を参照してください。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. セクションに含める各フィールドに対して、 `Fieldset` プロパティを手順 3 で選択したのと同じ名前に設定します。

   例えば、 `experience` （すべての関連フィールドの Fieldset プロパティ）を選択し、 `employment history` 」セクションに入力します。

   ![繰り返し可能なセクションフィールドとそのプロパティの例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューおよびパブリッシュします。 繰り返し可能なセクションがフォームに追加されます。

   繰り返し可能なセクションの下では、ユーザーは直感的な **追加** 複数のセクションを簡単に追加できるボタン。

   ![繰り返し可能なセクション、追加ボタン、複数のセクションを追加 ](/help/edge/assets/repeatable-section-example.png)


## 繰り返しの最小値と最大値の設定

フォームデザインでは、繰り返し可能なセクションの繰り返しの最小値と最大値を設定すると便利です。 これにより、ユーザーを効果的に導きながら、制御と一貫性を確立できます。 繰り返しの最小数または最大数を設定する手順は、次のとおりです。

1. Microsoft SharePointまたはGoogle Workspace の Edge Deliver プロジェクトフォルダーに移動し、スプレッドシートを開きます。

1. 次のフィールド： `type` `fieldset` および `repeatable` プロパティをに設定 `true`:

   * を設定します。 `min` プロパティを使用して、セクションを繰り返し可能な最小回数を指定します。

   * を設定します。 `max` プロパティを使用して、セクションを繰り返し可能な最大回数を指定します。

   ![min プロパティと max プロパティを設定して、セクションを繰り返す回数を指定します。](/help/edge/assets/repeatable-section-set-min-max.png)

1. 用途 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) をクリックして、シートをプレビューおよびパブリッシュします。

   繰り返し可能なセクションを追加すると、ユーザーは直感的に **削除** アイコンを使用して、繰り返し可能なセクションを簡単に削除できます。 追加後は、これらのセクションを減らして、 `min` プロパティ。 これにより、フォームの完成に必要な最小要件を確実に満たすことができます。

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Forms Block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## 詳細を表示する

* [フォームの作成とプレビュー](/help/edge/docs/forms/create-forms.md)
* [フォームからデータを送信できるようにする](/help/edge/docs/forms/submit-forms.md)
* [サイトページにフォームを発行する](/help/edge/docs/forms/publish-forms.md)
* [フォームフィールドに検証機能を追加する](/help/edge/docs/forms/validate-forms.md)
* [フォームのテーマとスタイルを変更する](/help/edge/docs/forms/style-theme-forms.md)
* [フォームコンポーネントとそのプロパティ](/help/edge/docs/forms/form-components.md)
