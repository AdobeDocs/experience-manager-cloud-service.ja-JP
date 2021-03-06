---
title: 'IP許可リストの適用と適用解除 '
description: 環境に IP許可リストを適用および適用解除する方法を説明します。
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
source-git-commit: 7632a9fef71e95238d149ec5318903757bb2a326
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 14%

---


# IP許可リストの適用と適用解除 {#apply-allow-list}

IP許可リストを適用する場合、リストの定義に含まれるすべての IP 範囲が環境内のオーサーサービスまたはパブリッシュサービスに関連付けられます。 リストの適用を解除すると、この処理の逆になります。

## IP許可リストの適用 {#applying}

ユーザーの **ビジネスオーナー** または **デプロイメントマネージャー** 役割は、次の手順に従って IP許可リストを適用できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 次に移動： **環境** 画面から **概要** ページ。
1. 上の特定の環境の詳細ページに移動します。 **環境** 画面に移動して、 **IP許可リスト** 表。
1. テーブル上部の入力フィールドを使用して、IP許可リストと、その IP オプションを適用するオーサーサービスまたはパブリッシュサービスを選択します。
   * IP許可リストを適用するには、Cloud Manager に IP アドレスが存在する必要があります。
1. クリック **適用** 送信を確認します。

## 未適用許可リスト {#un-applying}

ユーザーの **ビジネスオーナー** または **デプロイメントマネージャー** ロールは、次の手順に従って IP許可リストの適用を解除できます。

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。
1. 次に移動： **環境** 画面から **概要** ページ。
1. 上の特定の環境の詳細ページに移動します。 **環境** 画面に移動して、 **IP許可リスト** 表。
1. 適用を解除する IP許可リストの行を特定します。
1. 行の右端にある省略記号ボタンを選択します。
1. 「**適用解除**」オプションを選択し、送信を確認します。
