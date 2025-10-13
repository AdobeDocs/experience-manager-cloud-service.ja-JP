---
title: ユニバーサルエディターを使用したフォームの作成
description: API 統合を使用して、カスケードドロップダウンリストをテストするアダプティブフォームを作成します。
feature: Edge Delivery Services
role: User
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '202'
ht-degree: 100%

---

# ユニバーサルエディターを使用したフォームの作成

ユニバーサルエディターを使用して、次のフォームを作成します。フォームには 3 つのドロップダウンリストがあり、その値は API 統合を使用して入力されます
![アダプティブフォーム](assets/address-form.png)

## 居住国

初期化時に、居住国ドロップダウンに API 呼び出しの結果が入力されます。
![初期化イベント](assets/initialize-event.png)

## 成功ハンドラー

成功ハンドラーは、geonames 配列の適切な値を使用して、国ドロップダウンリストの enum と enumNames を設定するように定義されました。geonames 配列は、イベントペイロードオプションで使用できます
![イベントペイロード](assets/event-payload.png)
![成功ハンドラー](assets/success-handler.png)

## 子の値の取得

ユーザーが居住国ドロップダウンリストで選択を行うと、都道府県ドロップダウンリストに値が入力されます。選択した国に関連付けられた geonameId は、GetChildren API 統合への入力パラメーターとして渡されます

![子を取得](assets/invoke-service-get-children.png)

成功ハンドラーは、StateOrProvince ドロップダウンフィールドの enum／enumNames を設定するために定義されました
![子を取得成功ハンドラー](assets/child-success-handler.png)

都道府県を選択すると、都道府県ドロップダウンリストに入力するために使用される上記のパターンに従って、市区町村ドロップダウンリストに入力できます。