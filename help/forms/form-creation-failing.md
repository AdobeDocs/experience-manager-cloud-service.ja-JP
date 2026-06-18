---
title: フォーム作成のエラーをトラブルシューティングする方法
description: AEM Forms as a Cloud Service環境でのフォーム作成エラーのトラブルシューティング。
feature: Adaptive Forms
role: User
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 169ea727-0941-4a1d-bc33-d9fe208b27ab
source-git-commit: a0d2982cff40cd8a9826eb22304f16b14a44d631
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 6%

---

# フォームの公開中に問題が発生する

ユーザーがAEM Forms as a Cloud Service バージョン `2024.5.16461`に更新した後：

**一部のユーザー**&#x200B;は、フォームの作成中に問題が発生する可能性があります。ユーザーがフォームを作成すると、作成ダイアログボックスに次のエラーメッセージが表示されます。

`A server error occurred. Try again after sometime.`

## 原因 {#cause-form-creation-fails}

この問題は、作成者がフォームを公開し、そのフォームで使用されているテンプレート **を最初に公開しないために発生します。**&#x200B;この結果、`jcr:uuid`およびその他の保護およびシステム生成プロパティが`<template-path>/initial/jcr:content` ノードに追加され、後続のフォーム作成でエラーが発生します。

## 対処方法 {#resolution-form-creation-fails}

問題を解決するには、次の手順に従います。

1. フォームで使用するテンプレートに`jcr:uuid`およびその他のシステムで生成された保護されたプロパティがパス `<template-path>/initial/jcr:content node`にないことを確認してください。
1. テンプレートコンソールを使用して、テンプレートを明示的に公開します。
1. テンプレートが公開されたら、テンプレートを使用して新しいフォームを作成してみましょう。
1. 今後のリリースで更新を使用したテンプレートの場合は、フォーム作成エラーの問題を防ぐために、（手順2で説明したように）テンプレートを再度公開します。


<!--

# Issue

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->
