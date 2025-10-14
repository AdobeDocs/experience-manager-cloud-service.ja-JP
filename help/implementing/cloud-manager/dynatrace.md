---
title: Dynatrace
description: Dynatrace を AEM as a Cloud Service で使用する方法を説明します。
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 498a58c89910f41e6b86c5429629ec9282028987
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 69%

---

# Dynatrace {#dynatrace}

アドビは、Dynatrace を使用して、エンタープライズ展開の一環として AEM as a Cloud Service を監視し、潜在的な問題の原因を特定し、必要に応じて問題を修復するための措置を講じる機能を提供します。

Dynatrace を使用すると、すべての AEM アプリケーションのシームレスな可観測性を実現できます。Dynatraceは、AEM アプリを検出し、web サイトからコンテナ、cloud service へのパスを表示して、ユーザーエクスペリエンスを明らかにします。 すべての層にわたるエンドツーエンドのトレースと実際の使用のモニタリングを組み合わせることで、ギャップや盲点のない AEM コンテンツ主導のエクスペリエンスを次のレベルに引き上げます。異常が発生した場合、Dynatraceは Davis AI エンジンを使用してリアルタイムで診断を行います。 顧客が影響を受ける前に、破損したコードまで根本原因を特定し、平均修復時間を最小限に抑えます。

Dynatrace について詳しくは、[Adobe AEM Cloud Service の統合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/)を参照してください。

![AEM オーサーとパブリッシャーのパフォーマンス指標](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Dynatrace と AEM as a Cloud Service の統合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace のお客様は、カスタマーサポートチケットを通じて接続をリクエストすることで、AEM 環境を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace 環境の URL。<br><br>Dynatrace SaaS のお客様の場合、形式は `https://<your-environment-id>.live.dynatrace.com` です。<br><br>Dynatrace Managed のお客様の場合、形式は `https://<your-managed-url>/e/<environmentId>` です。 |
| [!DNL Dynatrace Environment ID] | Dynatrace 環境 ID。詳しくは、[Dynatrace 接続の詳細を取得する方法入手方法については、](#how-do-i-get-my-dynatrace-connection-details) を参照してください。 |
| [!DNL Dynatrace Environment Token] | Dynatrace 環境トークン。詳しくは、[Dynatrace 接続の詳細を取得する方法入手方法については、](#how-do-i-get-my-dynatrace-connection-details) を参照してください。<br><br> このトークンは秘密鍵と見なされるべきなので、適切なセキュリティ対策を講じてください。 例えば、**zerobin.net** などの web サイトでパスワードで保護します。カスタマーサポートチケットはパスワードとともに参照できます。 |
| [!DNL Dynatrace API access token] | Dynatrace 環境の API アクセストークン。作成方法については、[Dynatrace API アクセストークンの作成 &#x200B;](#create-dynatrace-access-token) を参照してください。<br><br> このトークンは秘密鍵と見なされるべきなので、適切なセキュリティ対策を講じてください。 例えば、カスタマーサポートチケットが参照できる **zerobin.net** などの web サイトで、パスワードと共にパスワード保護します。<br> |
| [!DNL Dynatrace ActiveGate Port] | AEM 統合の接続先となる Dynatrace ActiveGate ポート。<br><br> このポートは、Dynatrace Managed にのみ必要です。 |
| [!DNL Dynatrace ActiveGate Network Zone] | [Dynatrace ActiveGate ネットワークゾーン](https://docs.dynatrace.com/docs/manage/network-zones)を使用して、データセンターとネットワークリージョン間で AEM 監視データを効率的にルーティングします。<br><br>メモ：Dynatrace ActiveGate ネットワークゾーンはオプションです。 |
| [!DNL AEM Environment IDs] | Dynatraceが監視するAEM環境 ID または ID。 |

>[!NOTE]
>
>Dynatraceが統合されると、以前に有効になっていた場合、データはNew Relicなどの他の APM ツールに送られなくなります。

## FAQ {#faq}

### Dynatrace AEM Monitoring にはどのライセンスが必要ですか。 {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM Monitoring には Dynatrace ライセンスが必要です。Dynatrace AEM ライセンスは、[Kubernetes コンテナのフルスタック監視](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring)に基づいています。監視対象の AEM コンテナ（オーサーサービスおよびパブリッシャーサービス）のメモリサイズは自動的に検出されます。

AEM 環境別のアドビデプロイメント仕様は、次のとおりです。

* 実稼動：平均で 4 つのコンテナ、それぞれ 16 GB のメモリ
* 実稼動以外：平均で 4 つのコンテナ、それぞれ 8 GB のメモリ

Dynatrace ライセンスについて詳しくは、[Dynatrace プラットフォームのサブスクリプション](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription)を参照してください。

### Dynatrace 接続の詳細を取得するにはどうすればよいですか。 {#how-do-i-get-my-dynatrace-connection-details}

1. Dynatrace 環境に対して次の API リクエストを実行します。

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   `<environmentUrl>` を Dynatrace 環境 URL に置き換え、`<accessToken>` を作成した API アクセストークンに置き換えます。

1. レスポンスペイロードから `<environmentId>` と `<environmentToken>` をコピーし、保護された場所に保存します。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Dynatrace API アクセス トークンを作成する {#create-dynatrace-access-token}

1. Dynatrace環境にログインします。
1. **[!DNL Access tokens]** に移動し、オプション **[!DNL Generate new token]** をクリックします。
1. [!DNL token name] を定義します。
1. トークンの範囲を **[!DNL PaaS integration - Installer download]** に設定します。
1. **[!DNL Generate token]** を選択します。
1. 生成されたアクセストークンをコピーし、安全な場所に保存します。





