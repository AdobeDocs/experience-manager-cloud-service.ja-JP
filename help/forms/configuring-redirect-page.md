---
title: リダイレクトページの設定方法
description: フォームの作成者がフォームの作成中に設定できる Web ページにユーザーをリダイレクトする方法を説明します。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---

# リダイレクトページの設定 {#configuring-redirect-page}

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

1. 編集モードで、コンポーネントを選択し、![フィールドレベル](assets/select_parent_icon.svg)／**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;をクリックしてから、 ![cmppr](assets/configure-icon.svg) をクリックします。

1. サイドバーで、「**[!UICONTROL 送信]**」をクリックします。

1. 「**[!UICONTROL 送信]**」セクションの&#x200B;**[!UICONTROL リダイレクト URL／パス]**&#x200B;にリダイレクトページの URL を指定します。
1. オプションとして、「送信アクション」で、「REST エンドポイントへの送信」の送信アクションについて、リダイレクトページに渡されるパラメーターを設定することができます。

   ![リダイレクトページ設定](assets/redirect-url.png)

   リダイレクトページ設定

フォーム作成者は、「ありがとうございます」ページに渡される次のパラメーターを使用することができます。使用可能なすべての送信アクションに対して、`status` と `owner` のパラメーターが渡されます。これら 2 つのパラメーターの他に、追加のパラメーターが次の送信アクションに渡されます。

* **[!UICONTROL REST エンドポイントへの送信]**：フィールド内にパラメーターマッピングのため追加されたパラメータが渡されます。`status` と `owner` のパラメーターは、この送信アクションでは渡されません。詳しくは、[送信アクション「REST エンドポイントへの送信」の設定](configuring-submit-actions.md)を参照してください。
