---
title: Configure Translation Rules
description: Learn how to define translation rules to identify content for translation.
exl-id: 878ffd5d-0f10-4990-9779-bdf55cd95fac
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 2%

---

# Configure Translation Rules {#configure-translation-rules}

Learn how to define translation rules to identify content for translation.

## これまでの説明内容 {#story-so-far}

[](configure-connector.md)

* Understand the important parameters of the Translation Integration Framework in AEM.
* Be able to set up your own connection to your translation service.

Now that your connector is set up, this article takes you through the next step of identifying what content you need to translate.

## 目的 {#objective}

This document helps you understand how to use AEM&#39;s translation rules to identify your translation content. 読み終えると、以下を達成できます。

* Understand what the translation rules do.
* Be able to define your own translation rules.

## 翻訳ルール {#translation-rules}

Content Fragments, which represent your headless content, can contain much information organized by structured fields. Depending on your project needs, it is likely that not all of the fields within a Content Fragment must to be translated.

Translation rules identify the content that is included in, or excluded from, translation projects. When content is translated, AEM extracts or harvests the content based on these rules. In this way only content that must be translated is sent to the translation service.

Translation rules include the following information:

* The path of the content to which the rule applies
   * The rule also applies to the descendants of the content
* The names of the properties that contain the content to translate
   * The property can be specific to a specific resource type or to all resource types

Because Content Fragment Models, which define the structure of your Content Fragments, are unique to your own project, it is vital to set up translation rules so AEM knows what elements of your content models to translate.

>[!TIP]
>
>**** These names are needed to configure translation rules. [****](getting-started.md#content-modlels)

## Creating Translation Rules {#creating-rules}

Multiple rules can be created to support complex translation requirements. For example, one project you may be working on requires all fields of the model to be translated, but on another only description fields must be translated while titles are left untranslated.

Translation rules are designed to handle such scenarios. However in this example we illustrate how to create rules by focusing on a simple, single configuration.

****&#x200B;コンソールにアクセスするには：

1. ********
1. ****

**** Here we highlight the most necessary and typical steps required for a basic headless localization configuration.

1. ****This is the path of the content that is be affected by the rule.
   ![](assets/add-translation-context.png)
1. ****`/content/dam/<your-project>`
   ![](assets/select-context.png)
1. AEM saves the configuration.
1. ********
   ![](assets/translation-rules-editor.png)
1. `/content/dam`**`/content/dam`**
1. ****[](getting-started.md#content-models)
   1. ****
   1. ********
   1. ****
   1. Repeat these steps for all of the fields that you must translate.
   1. 「**保存して閉じる**」をタップまたはクリックします。
      ![](assets/add-property.png)

You have now configured your translation rules.

## Advanced Usage {#advanced-usage}

There are a number of additional properties that can be configured as part of your translation rules. In addition, you can specify your rules by hand as XML, which allows for more specificity and flexibility.

[](#additional-resources)

## 次の手順 {#what-is-next}

Now that you have completed this part of the headless translation journey you should:

* Understand what the translation rules do.
* Be able to define your own translation rules.

[](translate-content.md)

## その他のリソース {#additional-resources}

[](translate-content.md)

* [](/help/sites-cloud/administering/translation/rules.md)
