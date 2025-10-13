---
title: API 統合を使用した Salesforce リードオブジェクトの作成
description: API 統合を使用して Salesforce リードオブジェクトを作成する方法について説明します。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: ルールエディターでの API の統合, サービス拡張機能の呼び出し
exl-id: 55835ffe-1b77-449b-b76d-16c0a343cf5c
hide: true
hidefromtoc: true
index: false
source-git-commit: 3a09a3fa9b8fb3dacef4c900979c4cc256551941
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 100%

---

# API 統合を使用した Salesforce リードオブジェクトの作成

このユースケースでは、API 統合を使用して Salesforce でリードを作成する方法について説明します。プロセスを完了すると、次のことができるようになります。

[Salesforce で接続済みアプリケーション](https://help.salesforce.com/s/articleView?id=platform.ev_relay_create_connected_app.htm&type=5)を設定し、安全な API アクセスを有効にする。

CORS （クロスオリジンリソース共有）を設定して、web ブラウザーで実行されるコード（JavaScript など）が特定のオリジンから Salesforce と通信できるようにし、次に示すように、そのオリジンを許可リストに追加する

![CORS](assets/salesforce-cors.png)

## 接続済みアプリケーションの設定

接続済みアプリケーションでは、次の設定が使用されます。要件に応じて、OAuth 範囲を割り当てることができます。
![接続済みアプリケーションの設定](assets/salesforce-connected-app-settings.png)

## API 統合を作成

| 名前 | 値 |
|--------------------------------|------------------|
| API URL | https://`<your-domain>`d.my.salesforce.com/services/data/v32.0/sobjects/Lead |
| クライアント ID | 接続済みアプリケーションに固有 |
| クライアントの秘密鍵 | 接続済みアプリケーションに固有 |
| OAuth URL | https://login.salesforce.com/services/oauth2/authorize |
| トークン URL にアクセス | https://`<your-domain>`/services/oauth2/token |
| 更新トークン URL | https://`<your-domain>`/services/oauth2/token |
| 認証範囲 | api chatter_api full id openid refresh_token visualforce web |
| 認証ヘッダー | 認証 Bearer |

![API 統合](assets/salesforce-api-integration-create-lead.png)

## 入力および出力パラメーター

次の JSON を使用して、API 呼び出しの入力パラメーターを定義し、出力パラメーターをマッピングします

```json
{
    "id": "00QKY000001LyJR2A0",
    "success": true
}
```

![入力および出力](assets/create-lead-api-integration-input-output.png)

## フォームの作成

次に示すように、ユニバーサルエディターを使用してシンプルなアダプティブフォームを作成し、リードオブジェクトの詳細をキャプチャします
![リードオブジェクトフォーム](assets/create-lead.png)

ルールエディターを使用して、「リードを作成」チェックボックスのクリックイベントを処理します。次に示すように、入力パラメーターを適切なフォームオブジェクトの値にマッピングします。新しく作成したリードオブジェクトの ID を `leadid` TextField オブジェクトに表示します。
![ルールエディター](assets/create-leade-rule-editor.png)

## 統合のテスト

- フォームをプレビューします
- 意味のある値を入力します
- 「`Create Lead`」チェックボックスをオンにして、API 呼び出しをトリガーします
- 新しく作成したリードオブジェクトのリード ID が `Lead ID` テキストフィールドに表示されます。
