---
title: ユニバーサルエディターを使用したフォームの作成
description: API 統合を使用してカスケードドロップダウンリストをテストするアダプティブフォームを作成する
feature: Edge Delivery Services
role: User
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# ユニバーサルエディターを使用したフォームの作成

ユニバーサルエディターを使用して、次のフォームを作成します。 フォームには 3 つのドロップダウンリストがあり、その値は API 統合を使用して入力されます
![ アダプティブフォーム ](assets/address-form.png)

## 居住国

初期化時に、「居住国」ドロップダウンに API 呼び出しの結果が入力されます。
![initialize-event](assets/initialize-event.png)

## 成功ハンドラー

成功ハンドラーは、geonames 配列の適切な値を使用して国ドロップダウンリストの enum と enumNames を設定するように定義されました。 geonames 配列は、イベントペイロード オプションの下で使用できます
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## 子の値の取得

都道府県ドロップダウンリストは、ユーザーが「居住国」ドロップダウンリストで選択すると入力されます。 選択した国に関連付けられている geonameId が、入力パラメーターとして GetChildren API 統合に渡されます

![get-children](assets/invoke-service-get-children.png)

StateOrProvince ドロップダウンフィールドの enum/enumNames を設定するために、サクセスハンドラーが定義されました。
![get-children-success-handler](assets/child-success-handler.png)

州または都道府県が選択されている場合、上記の州または都道府県の入力に使用されるパターンに従うことで、都市のドロップダウンリストを入力できます。