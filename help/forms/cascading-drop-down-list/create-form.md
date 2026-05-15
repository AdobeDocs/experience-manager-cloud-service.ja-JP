---
title: ユニバーサルエディターを使用したフォームの作成
description: アダプティブフォームの式を使用して、自動検証や演算を追加したり、セクションの表示のオン／オフを切り替えたりします。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 76%

---

# ユニバーサルエディターを使用したフォームの作成

ユニバーサルエディターを使用して、次のフォームを作成します。 フォームには3つのドロップダウンリストがあり、その値はAPI統合を使用して入力されます
![adaptive-form](assets/address-form.png)

## 居住国

初期化時に、居住国ドロップダウンに API 呼び出しの結果が入力されます。
![初期化イベント](assets/initialize-event.png)

## 成功ハンドラー

成功ハンドラーは、geonames 配列の適切な値を使用して、国ドロップダウンリストの enum と enumNames を設定するように定義されました。 geonames配列は、イベントペイロードオプションで使用できます
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## 子の値の取得

ユーザーが居住国ドロップダウンリストで選択を行うと、都道府県ドロップダウンリストに値が入力されます。 選択した国に関連付けられた geonameId は、GetChildren API 統合への入力パラメーターとして渡されます

![子を取得](assets/invoke-service-get-children.png)

次のハンドラーは、StateOrProvince ドロップダウンフィールドのenum/enumNamesを設定するために定義されました
![get-children-success-handler](assets/child-success-handler.png)

都道府県を選択すると、都道府県ドロップダウンリストに入力するために使用される上記のパターンに従って、市区町村ドロップダウンリストに入力できます。