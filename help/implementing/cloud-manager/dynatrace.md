---
title: ダイナトレース
description: AEM as a Cloud Serviceでの Dynatrace の使用方法を説明します。
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: a234f2a00c51bcb23b0c52feac9971259d26b8c3
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# ダイナトレース {#dynatrace}

Adobeでは、AEM as a Cloud Serviceを企業のデプロイメントの一環として監視し、潜在的な問題の原因を特定し、必要に応じて修正を行うことができます。

Dynatrace を使用すると、すべてのAEMアプリケーションをシームレスに監視できます。 AEMアプリケーションを自動的に検出し、Web サイトからコンテナ、クラウドサービスへの依存関係を視覚化することで、エンドユーザーエクスペリエンスを包括的に表示できます。 あらゆる層のエンドツーエンドのトレースと Real User Monitoring が組み合わされ、AEMのコンテンツ主導のエクスペリエンスを、隙間や盲点のない次のレベルに引き上げます。 異常が発生した場合、Dynatrace は Davis AI エンジンを使用してそれらをリアルタイムに診断し、顧客が影響を受ける前に、根本原因を破損したコードに突き止め、平均修復時間を最小限に抑えます。

Dynatrace について詳しくは、 [AdobeAEM Cloud Serviceの統合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEMオーサーとパブリッシャーのパフォーマンス指標](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Dynatrace とAEM as a Cloud Serviceの統合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynater のお客様は、カスタマーサポートチケットを通じて接続をリクエストすることで、AEM環境を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| 動的環境 URL | Dynatrace 環境の URL。<br><br>Dynatrace SaaS のお客様の場合、形式は次のようになります。 `https://<your-environment-id>.live.dynatrace.com`.<br><br>Dynatrace が管理するお客様の場合、形式は次のようになります。 `https://<your-managed-url>/e/<environmentId>` |
| 動的環境 ID | 動的環境 ID。 詳しくは、 [Dynaterace 環境情報の取得](#get-dynatrace-env-info) これを手に入れる方法を |
| 動的環境トークン | Dynaterace 環境トークンです。 詳しくは、 [Dynaterace 環境情報の取得](#get-dynatrace-env-info) これを手に入れる方法を<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。 |
| Dynatrace API アクセストークン | Dynatrace 環境の API アクセストークン。  詳しくは、 [Dynaterce API アクセストークンの作成](#create-dynatrace-access-token) を参照してください。<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| Dynatrace ActiveGate ポート | AEM統合の接続先となる Dynace ActiveGate ポート。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| Dynatrace ActiveGate ネットワークゾーン | お使いの [Dynatrace ActiveGate ネットワークゾーン](https://docs.dynatrace.com/docs/manage/network-zones) データセンターとネットワーク地域をまたいでAEM監視データを効率的にルーティングする。<br><br>注意： Dynatrace ActiveGate ネットワークゾーンはオプションです。 |
| AEM環境 ID | Dynace が監視するAEM環境 ID。 |

>[!NOTE]
>
>統合された Dynatrace は、以前に有効になっていた場合、New Relicなどの他の APM ツールにデータを送信しなくなります。


## Dynaterce API アクセストークンの作成 {#create-dynatrace-access-token}

1. Dynaterace 環境にログインします。
1. 動的メニューで、管理/アクセストークンに移動します。
1. 「新規トークンを生成」を選択します。
1. トークン名を定義します。

1. オプション：有効期限を設定します。 有効期限が切れる前に、新しいトークンを必ず生成してください。
1. トークンの範囲を PaaS 統合に設定する — インストーラーのダウンロード
1. 「トークンを生成」を選択します。
1. 生成されたアクセストークンをコピーし、安全な場所に保存します。


## Dynaterace 環境情報の取得 {#get-dynatrace-env-info}

1. Dynace 環境に対して、次の API リクエストを実行します。

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

\を置換&lt;environmenturl> を、Dynatrace 環境 URL と\&lt;accesstoken> 作成した API アクセストークンを使用して、

1. \&lt;environmentid> と\&lt;environmenttoken> 応答ペイロードから取得し、保護された場所に保存します。

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


