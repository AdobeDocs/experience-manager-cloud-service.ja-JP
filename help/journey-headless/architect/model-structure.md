---
title: Learn about Creating Content Fragment Models in AEM
description: Learn about the concepts and mechanics of modeling content for your Headless CMS using Content Fragments Models.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 16%

---

# Learn about Creating Content Fragment Models in AEM {#architect-headless-content-fragment-models}

## The Story so Far {#story-so-far}

[](overview.md)[](basics.md)

This article builds on these so you understand how to create your own Content Fragment Models for your AEM headless project.

## 目的 {#objective}

* **オーディエンス**：初心者
* ****

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## コンテンツフラグメントモデルの作成 {#creating-content-fragment-models}

その後、コンテンツフラグメントモデルを作成し、構造を定義できます。これは、ツール／アセット／コンテンツフラグメントモデルで実行できます。

![](assets/cfm-tools.png)

**** Here you can enter various key details.

**** This means that your model will be available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![](/help/assets/content-fragments/assets/cfm-models-02.png)

********

## Defining Content Fragment Models {#defining-content-fragment-models}

****

![](/help/assets/content-fragments/assets/cfm-models-03.png)

So - what&#39;s to be done?

****

![](/help/assets/content-fragments/assets/cfm-models-04.png)

**** These depend on the type being used. 次に例を示します。

![](/help/assets/content-fragments/assets/cfm-models-05.png)

You can add as many fields as you need. 次に例を示します。

![コンテンツフラグメントモデル](/help/assets/content-fragments/assets/cfm-models-07.png)

### Your Content Authors {#your-content-authors}

Your content authors do not see the actual Data Types and Properties that you&#39;ve used to create your models. This means that you might have to provide help and information on how they complete specific fields. For basic information you can use the Field Label and Default Value, but more complex cases project specific documentation might need to be considered.

>[!NOTE]
>
>「その他のリソース - コンテンツフラグメントモデル」を参照してください。

## Managing Content Fragment Models {#managing-content-fragment-models}

<!-- needs more details -->

Managing your Content Fragment Models involves:

* Enabling (or disabling) them - this makes them available for authors when creating Content Fragments.
* Deleting - deletion is always needed, but you need to be aware of deleting a model that is already used for Content Fragments, in particular fragments that are already published.

## 公開 {#publishing}

<!-- needs more details -->

コンテンツフラグメントモデルは、依存するコンテンツフラグメントの公開時または公開前に公開する必要があります。

>[!NOTE]
>
>If an author tries to publish a content fragment for which the model has not yet been published, a selection list will indicate this and the model will be published with the fragment.

** This aims to prevent changes that would result in errors to existing GraphQL schemas and queries, especially on the publish environment. ****

********

## 次の手順 {#whats-next}

Now that you have learned the basics, the next step is to start creating your own Content Fragment Models.

## その他のリソース {#additional-resources}

* [オーサリングに関する概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [](/help/sites-cloud/authoring/getting-started/basic-handling.md)************

* [コンテンツフラグメントの操作](/help/assets/content-fragments/content-fragments.md)

   * [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)

      * [コンテンツフラグメントモデルの定義](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [コンテンツフラグメントモデルの有効化または無効化](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [アセットフォルダーでのコンテンツフラグメントモデルの許可](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [コンテンツフラグメントモデルの削除](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [コンテンツフラグメントモデルの公開](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [コンテンツフラグメントモデルを非公開にする](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [Locked (Published) Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* 「はじめる前に」ガイド 

   * [コンテンツフラグメントモデルのヘッドレス作成のクイック開始ガイド](/help/implementing/developing/headless/getting-started/create-content-model.md)
