---
title: Translate Content
description: Use the translation connector and rules to translate your headless content.
exl-id: 3bfbf186-d684-4742-8c5c-34c34ff3adb5
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '2174'
ht-degree: 2%

---

# Translate Content {#translate-content}

Use the translation connector and rules to translate your headless content.

## これまでの説明内容 {#story-so-far}

[](translation-rules.md)You should now:

* Understand what the translation rules do.
* Be able to define your own translation rules.

Now that your connector and translations rules are set up, this article takes you through the next step of translating your headless content.

## 目的 {#objective}

This document helps you understand how to use AEM&#39;s translation projects along with the connector and your translations rules to translate content. 読み終えると、以下を達成できます。

* Understand what a translation project is.
* Be able to create new translation projects.
* Use translation projects to translate your headless content.

## Creating a Translation Project {#creating-translation-project}

Translation projects enable you to manage the translation of headless AEM content. A translation project gathers the content to be translated into other languages in one location for a central view of the translation effort.

When content is added to a translation project, a translation job is created for it. リソースで実行される人間による翻訳と機械翻訳のワークフローの管理に使用するコマンドとステータス情報がジョブによって提供されます。

Translation projects can be created in two ways:

1. Select the language root of the content and have AEM automatically create the translation project based on the content path.
1. Create an empty project and manually select the content to add to the translation project

Both are valid approaches usually only differing based on the persona performing the translation:

* The translation project manager (TPM) often needs the flexibility of manually selecting the content to the translation project.
* If the content owner is also responsible for translation, letting AEM automatically create the project based on the selected content path is often easier.

Both approaches are explored in the following sections.

### Automatically Creating a Translation Project Based on Content Path {#automatically-creating}

For content owners who are also responsible for translation, it is often easier to have AEM automatically create the translation project automatically. To have AEM automatically create a translation project based on your content path:

1. ************ Remember that headless content in AEM is stored as assets known as Content Fragments.
1. Select the language root of your project. `/content/dam/wknd/en`
1. ****
1. ****
1. ****
1. ****
1. ********
1. Provide an appropriate title for your translation project.
1. ****

![翻訳プロジェクトを作成](assets/create-translation-project.png)

You receive a message that the project was created.

>[!NOTE]
>
>[](getting-started.md#content-structure)
>
>If the language folders are not created ahead of time, you will not be able to create language copies as described in the previous steps.

### Manually Creating a Translation Project by Selecting Your Content {#manually-creating}

For translation project managers, it is often necessary to manually select specific content to include in a translation project. To create such a manual translation project, you must start by creating an empty project and then select the content to add to it.

1. ********
1. ********
   * This is optional, but helpful to organize your translation efforts.
1. ************

   ![](assets/create-project-folder.png)

1. Tap or click the folder to open the folder.
1. ********
1. Projects are based on templates. ********

   ![](assets/select-translation-project-template.png)

1. ****

   ![](assets/project-basic-tab.png)

1. ********「**作成**」をタップまたはクリックします。

   ![](assets/project-advanced-tab.png)

1. ****

   ![](assets/project-confirmation-dialog.png)

The project has been created, but contains no content to translate. The next section details how the project is structured and how to add content.

## Using a Translation Project {#using-translation-project}

Translation projects are designed to collect all of the content and tasks related to a translation effort in one place to make your translation simple and easy to manage.

To view the translation project:

1. ********
1. Tap or click the project that was created in the previous section.

![翻訳プロジェクト](assets/translation-project.png)

The project is divided into multiple cards.

* ****
* **** Generally there is one job per language with the ISO-2 language code appended to the job name.
* **** This journey does not cover this topic.
* **** This journey does not cover this topic.

How you use a translation project depends on how it was created: either automatically by AEM or manually.

### Using an Automatically Created Translation Project {#using-automatic-project}

When automatically creating the translation project, AEM evaluates the headless content under the path you selected  based on the translation rules that you previously defined. Based on that evaluation, it extracts the content that requires translation into a new translation project.

To see the detail of the headless content included in this project:

1. ****
1. ****
   ![](assets/translation-job-detail.png)
1. Tap or click a line to see the detail of that line, keeping in mind that one line may represent multiple content items to translate.
1. Tap or click the selection checkbox for a line item to see further options such as the option to delete it from the job or view it in the Content Fragments or Assets consoles.

![](assets/translation-job-options.png)

************

********

![](assets/start-translation-job.png)

AEM now communicates with your translation configuration and connector to send the content to the translation service. ********

![](assets/translation-job-approved.png)

**** Human translation allows for more interaction, but is beyond the scope of this journey.

### Using a Manually Created Translation Project {#using-manual-project}

When manually creating a translation project, AEM creates the necessary jobs, but does not automatically select any content to include. This allows the translation project manager the flexibility to pick-and-chose what content to translate.

To add content to a translation job:

1. ****
1. See that the job contains no content. ********

   ![](assets/empty-translation-job.png)

1. A path browser opens allowing you to select specifically which content to add. Locate your content and tap or click to select.

   ![](assets/path-browser.png)

1. ****
1. ********

   ![言語コピーを作成](assets/translate-copy-master.png)

1. The content is now included in the job.

   ![](assets/content-added.png)

1. Tap or click the selection checkbox for a line item to see further options such as the option to delete it from the job or view it in the Content Fragments or Assets consoles.

![](assets/translation-job-options.png)

1. Repeat these steps to include all required content in the job.

>[!TIP]
>
>The path browser is a powerful tool allowing you to search, filter, and navigate your content. ************
>
>[](#additional-resources)

You can use the prior steps to add the necessary content to all of the languages (jobs) for the project. Once you have selected all of the content, you can start the translation.

************

********

![](assets/start-translation-job.png)

AEM now communicates with your translation configuration and connector to send the content to the translation service. ********

![](assets/translation-job-approved.png)

**** Human translation allows for more interaction, but is beyond the scope of this journey.

## Reviewing Translated Content {#reviewing}

[](#using-translation-project)**** However it is of course still possible to review the translated content.

Simply go to the completed translation job and select a line item by tapping or clicking the checkbox. ****

![](assets/reveal-in-content-fragment.png)

Tap or click that icon to open the translated content fragment in its editor console to see the details of the translated content.

![](assets/translated-content-fragment.png)

You can further modify the content fragment as necessary, providing you have the proper permission, but editing content fragments is beyond the scope of this journey. [](#additional-resources)

The project&#39;s purpose is to collect all the resources related to a translation in one place for easy access and a clear overview. However as you can see by viewing the detail of a translated item, the translations themselves flow back into the asset folder of the translation language. In this example the folder is

```text
/content/dam/wknd/es
```

************

![](assets/translated-file-content.png)

AEM&#39;s translation framework receives the translations from the translation connector and then automatically creates the content structure based on the language root and using the translations provided by the connector.

It is important to understand that this content is not published and therefore not available to your headless services. We will learn about this author-publish structure and see how to publish our translated content in the next step of the translation journey.

## 人間翻訳 {#human-translation}

If your translation service provides human translation, the review process offers more options. ****

Human translation is beyond the scope of this localization journey. [](#additional-resources)However beyond the additional approval options, the workflow for human translations is the same as machine translations as described in this journey.

## 次の手順 {#what-is-next}

Now that you have completed this part of the headless translation journey you should:

* Understand what a translation project is.
* Be able to create new translation projects.
* Use translation projects to translate your headless content.

[](publish-content.md)

## その他のリソース {#additional-resources}

[](publish-content.md)

* [](/help/sites-cloud/administering/translation/managing-projects.md)
* [](/help/sites-cloud/authoring/fundamentals/environment-tools.md##path-selection)
