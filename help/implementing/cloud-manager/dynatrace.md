---
title: ダイナトレース
description: AEM as a Cloud ServiceでDynatraceを使用する方法を学ぶ
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: 4fe8ed9c3f7b6589878da3317d15fede819bad54
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# ダイナトレース {#dynatrace}

Adobeでは、Dynatraceを使用して、エンタープライズデプロイメントの一環としてAEM as a Cloud Serviceを監視し、潜在的な問題の原因を特定し、必要に応じて修正をおこなうことができます。

Dynatraceを使用すると、すべてのAEMアプリケーションをシームレスに監視できます。 Dynatraceは、AEMアプリケーションを自動的に検出し、Web サイトからコンテナ、クラウドサービスへの依存関係を視覚化することで、エンドユーザーエクスペリエンスを包括的に表示します。 あらゆる層のエンドツーエンドのトレースと Real User Monitoring が組み合わされ、AEMのコンテンツ主導のエクスペリエンスを、隙間や盲点のない次のレベルに引き上げます。 異常が発生した場合、Dynatraceは Davis AI エンジンを使用してリアルタイムに診断し、顧客が影響を受ける前に根本原因を破損したコードに突き止め、平均修復時間を最小限に抑えます。

Dynatraceについて詳しくは、 [AdobeAEM Cloud Serviceの統合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEMオーサーとパブリッシャーのパフォーマンス指標](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## DynatraceとAEM as a Cloud Serviceの統合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatraceのお客様は、カスタマーサポートチケットを通じて接続をリクエストすることで、AEM環境を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace環境 URL。<br><br>Dynatrace SaaS のお客様の場合、形式は次のようになります。 `https://<your-environment-id>.live.dynatrace.com`.<br><br>Dynatraceが管理するお客様の場合、形式は次のようになります。 `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Dynatrace環境 ID。 詳しくは、 [Dynatrace Connection Details を取得するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details) これを手に入れる方法を |
| [!DNL Dynatrace Environment Token] | Dynatrace環境トークン。 詳しくは、 [Dynatrace Connection Details を取得するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details) これを手に入れる方法を<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。 |
| [!DNL Dynatrace API access token] | Dynatrace環境の API アクセストークン。  詳しくは、 [Dynatrace API アクセストークンの作成](#create-dynatrace-access-token) を参照してください。<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| [!DNL Dynatrace ActiveGate Port] | AEM統合の接続先となるDynatrace ActiveGate ポート。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| [!DNL Dynatrace ActiveGate Network Zone] | お使いの [Dynatrace ActiveGate ネットワークゾーン](https://docs.dynatrace.com/docs/manage/network-zones) データセンターとネットワーク地域をまたいでAEM監視データを効率的にルーティングする。<br><br>注意： Dynatrace ActiveGate ネットワークゾーンはオプションです。 |
| [!DNL AEM Environment ID(s)] | Dynatraceが監視するAEM環境 ID。 |

>[!NOTE]
>
>Dynatraceが統合されると、以前に有効になっていた場合、データはNew Relicなどの他の APM ツールに送られなくなります。

## FAQ {#faq}

### Dynatrace AEM Monitoring に必要なライセンス {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEMの監視には、Dynatraceライセンスが必要です。 Dynatrace AEMのライセンスは、 [Kubernetes コンテナのフルスタック監視](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). 監視対象のAEMコンテナ（オーサーサービスおよびパブリッシャーサービス）のメモリサイズが自動的に検出されます。

各AEM環境のAdobeデプロイメント仕様は、次のとおりです。

* 実稼働：平均で 4 つのコンテナ、それぞれ 16 GB のメモリ
* 非実稼動：平均で 4 つのコンテナ、それぞれ 8 GB のメモリ

Dynatraceライセンスについて詳しくは、 [Dynatrace Platform Subscription](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Dynatrace Connection Details を取得するにはどうすればよいですか？ {#how-do-i-get-my-dynatrace-connection-details}

1. Dynatrace環境に対して、次の API リクエストを実行します。

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   置換 `<environmentUrl>` Dynatrace環境 URL と `<accessToken>` 作成した API アクセストークンを使用して、

1. をコピーします。 `<environmentId>` および `<environmentToken>` 応答ペイロードから取得し、保護された場所に保存します。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Dynatrace API アクセストークンの作成 {#create-dynatrace-access-token}

1. Dynatrace環境にログインします。
1. に移動します。 **[!DNL Access tokens]** を選択し、 **[!DNL Generate new token]**.
1. を定義 [!DNL token name].
1. トークンのスコープをに設定します。 **[!DNL PaaS integration - Installer download]**.
1. 選択 **[!DNL Generate token]**.
1. 生成されたアクセストークンをコピーし、安全な場所に保存します。





