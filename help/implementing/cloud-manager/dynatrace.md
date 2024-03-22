---
title: Dynatrace
description: Dynatrace を AEM as a Cloud Service で使用する方法を説明します。
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: 4fe8ed9c3f7b6589878da3317d15fede819bad54
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 73%

---

# Dynatrace {#dynatrace}

アドビは、Dynatrace を使用して、エンタープライズ展開の一環として AEM as a Cloud Service を監視し、潜在的な問題の原因を特定し、必要に応じて問題を修復するための措置を講じる機能を提供します。

Dynatrace を使用すると、すべての AEM アプリケーションのシームレスな可観測性を実現できます。Dynatrace は、AEM アプリケーションを自動的に検出し、web サイトからコンテナ、クラウドサービスに至る依存関係を表示することで、エンドユーザーエクスペリエンスを包括的に可視化します。すべての層にわたるエンドツーエンドのトレースとリアルユーザーモニタリングを組み合わせることで、ギャップや盲点のない AEM コンテンツ主導のエクスペリエンスを次のレベルに引き上げます。異常が発生した場合、Dynatrace は Davis AI エンジンを使用してリアルタイムで異常を診断し、顧客が影響を受ける前に壊れたコードに至るまで根本原因を特定することで、平均修復時間を最小限に抑えます。

Dynatrace について詳しくは、[Adobe AEM Cloud Service の統合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/)を参照してください。

![AEM オーサーとパブリッシャーのパフォーマンス指標](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Dynatrace と AEM as a Cloud Service の統合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace のお客様は、カスタマーサポートチケットを通じて接続をリクエストすることで、AEM 環境を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace 環境の URL。<br><br>Dynatrace SaaS のお客様の場合、形式は `https://<your-environment-id>.live.dynatrace.com` です。<br><br>Dynatrace Managed のお客様の場合、形式は `https://<your-managed-url>/e/<environmentId>` です。 |
| [!DNL Dynatrace Environment ID] | Dynatrace 環境 ID。詳しくは、 [Dynatrace Connection Details を取得するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details) これを手に入れる方法を |
| [!DNL Dynatrace Environment Token] | Dynatrace 環境トークン。詳しくは、 [Dynatrace Connection Details を取得するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details) これを手に入れる方法を<br><br>これはシークレットと見なす必要があるので、適切なセキュリティプラクティスを使用してください。例えば、**zerobin.net** などの web サイトでパスワードで保護します。カスタマーサポートチケットはパスワードとともに参照できます。 |
| [!DNL Dynatrace API access token] | Dynatrace 環境の API アクセストークン。これを作成する方法について詳しくは、[Dynatrace API アクセストークンを作成](#create-dynatrace-access-token)を参照してください。<br><br>これはシークレットと見なす必要があるので、適切なセキュリティプラクティスを使用してください。例えば、**zerobin.net** などの web サイトでパスワードで保護します。カスタマーサポートチケットはパスワードとともに参照できます。<br><br>メモ：これは、Dynatrace Managed でのみ必要です。 |
| [!DNL Dynatrace ActiveGate Port] | AEM 統合の接続先となる Dynatrace ActiveGate ポート。<br><br>メモ：これは、Dynatrace Managed でのみ必要です。 |
| [!DNL Dynatrace ActiveGate Network Zone] | [Dynatrace ActiveGate ネットワークゾーン](https://docs.dynatrace.com/docs/manage/network-zones)を使用して、データセンターとネットワークリージョン間で AEM 監視データを効率的にルーティングします。<br><br>メモ：Dynatrace ActiveGate ネットワークゾーンはオプションです。 |
| [!DNL AEM Environment ID(s)] | Dynatrace が監視する AEM 環境 ID。 |

>[!NOTE]
>
>Dynatrace が統合されると、以前に有効になっていた場合、データは New Relic などの他の APM ツールに流れなくなります。

## FAQ {#faq}

### Dynatrace AEM Monitoring に必要なライセンス {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEMの監視には、Dynatraceライセンスが必要です。 Dynatrace AEMのライセンスは、 [Kubernetes コンテナのフルスタック監視](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). 監視対象のAEMコンテナ（オーサーサービスおよびパブリッシャーサービス）のメモリサイズが自動的に検出されます。

各AEM環境のAdobeデプロイメント仕様は、次のとおりです。

* 実稼働：平均で 4 つのコンテナ、それぞれ 16 GB のメモリ
* 非実稼動：平均で 4 つのコンテナ、それぞれ 8 GB のメモリ

Dynatraceライセンスについて詳しくは、 [Dynatrace Platform Subscription](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Dynatrace Connection Details を取得するにはどうすればよいですか？ {#how-do-i-get-my-dynatrace-connection-details}

1. Dynatrace 環境に対して次の API リクエストを実行します。

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

### Dynatrace API アクセス トークンを作成する {#create-dynatrace-access-token}

1. Dynatrace 環境にログインします。
1. に移動します。 **[!DNL Access tokens]** を選択し、 **[!DNL Generate new token]**.
1. [!DNL token name] を定義します。
1. トークンのスコープをに設定します。 **[!DNL PaaS integration - Installer download]**.
1. **[!DNL Generate token]** を選択します。
1. 生成されたアクセストークンをコピーし、安全な場所に保存します。





