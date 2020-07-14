---
title: Adobe AEMTargetHTTPウィンドウ
description: 'Adobe AEMTargetHTTPウィンドウ '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# 概要 {#introduction}

このページでは、Adobe AEMTargetのHTTPウィンドウに表示される設定可能なパラメーターについて説明します。

## パラメーター {#parameters}

![TargetHTTP](assets/httpwindow.png "WindowTarget HTTPウィンドウ")

このウィンドウには、次の設定可能なパラメーターが含まれています。

| パラメーター | 説明 |
|---|---|
| Adobe TargetAPI URL | Adobe TargetAPIのURL。 |
| 絶対URLを有効にする | URLのホスト部分または完全なURLのいずれかを使用するかどうかを決定します。 完全な（完全な）URLを使用する場合は、このチェックボックスをオンにします。 デフォルトでは、このチェックボックスは無効になっています。 |
| 接続タイムアウト | 接続が確立されるまでのタイムアウト（ミリ秒）。 デフォルト値は60000ミリ秒です。 値0は、無限タイムアウトと解釈されます。 |
| ソケットのタイムアウト | データを待機するタイムアウト（ミリ秒）、または2つの連続したデータパケットの間に無操作状態が最大まで続く時間（ミリ秒）。 デフォルト値は30000ミリ秒です。 |
| Adobe TargetレコメンデーションURL正規表現トークンの置換 | Adobe TargetエンドポイントURL内のトークンを制御します。このトークンは、Target再命令API URLを指すように置き換える必要があります。 |
| Adobe Target推奨URLをトークンに置き換える | 上記のパラメーターで説明した正規表現に置き換えたものなので、結果のURLはTargetの修正APIを指します。 |
