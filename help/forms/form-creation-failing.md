---
title: フォーム作成の失敗のトラブルシューティング方法
description: AEM Formsas a Cloud Service環境でのフォーム作成の失敗のトラブルシューティング。
feature: Adaptive Forms
role: User
exl-id: 169ea727-0941-4a1d-bc33-d9fe208b27ab
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 5%

---

# フォームの公開中の問題{#form-creation-fails}

ユーザーがAEM Formsのas a Cloud Service版に更新した後 `2024.5.16461`:

**一部のユーザー** フォームの作成中に問題が発生する場合がある問題は、ユーザーがフォームを作成すると、作成ダイアログボックスに次のエラーメッセージがポップアップ表示されるというものです。

`A server error occurred. Try again after sometime.`

## 原因 {#cause-form-creation-fails}

この問題は、作成者がフォームをなしで公開したために発生します **最初にテンプレートを公開** その中で使用されます。 この結果、 `jcr:uuid` 保護されたプロパティやシステム生成プロパティを以下に追加しました： `<template-path>/initial/jcr:content` ノードが含まれ、後続のフォーム作成でエラーが発生する。

## 対処方法 {#resolution-form-creation-fails}

問題を解決するには、次の手順に従います。

1. フォームで使用するテンプレートに、が含まれていないことを確認します `jcr:uuid` およびその他のシステム生成パスの保護されたプロパティ `<template-path>/initial/jcr:content node`.
1. テンプレートコンソールを使用して、テンプレートを明示的にPublishします。
1. 次に、テンプレートが公開されたら、テンプレートを使用して新しいフォームを作成してみてください。
1. 使用したテンプレートが今後のリリースで更新される場合は、（手順 2 で指定したように）テンプレートを再度Publishして、フォーム作成の失敗の問題を防ぎます。


<!--

# Issue {#form-creation-fails}

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
