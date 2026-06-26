---
title: Dynatrace
description: AEM as a Cloud ServiceでDynatraceを使用する方法について説明します。
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: d007b33ba41a791242c1ea1c8264984b9182fa54
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 44%

---

# Dynatrace {#dynatrace}

アドビは、Dynatrace を使用して、エンタープライズ展開の一環として AEM as a Cloud Service を監視し、潜在的な問題の原因を特定し、必要に応じて問題を修復するための措置を講じる機能を提供します。

Dynatrace を使用すると、すべての AEM アプリケーションのシームレスな可観測性を実現できます。 Dynatraceは、AEM アプリケーションを検出し、web サイトからコンテナ、Cloud Serviceまでのパスを表示して、ユーザーエクスペリエンスをモニタリングします。 あらゆる階層をまたいだエンドツーエンドのトレースとリアルユーザーモニタリングを組み合わせることで、ギャップやモニタリングの制限なしに、AEMのコンテンツ主導のエクスペリエンスを向上できます。 異常が発生した場合は、DynatraceがDavis AI エンジンを使用してリアルタイムで診断します。 顧客が影響を受ける前に問題の原因を特定し、解決に必要な時間を短縮します。

Dynatrace について詳しくは、[Adobe AEM Cloud Service の統合](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/)を参照してください。

![AEM オーサーとパブリッシャーのパフォーマンス指標](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## DynatraceとAEM as a Cloud Serviceの統合 {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatraceをご利用のお客様は、カスタマーサポートチケットを通じて接続性をリクエストすることで、AEM環境を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| [!DNL Dynatrace Environment URL] | Dynatrace環境のURL。<br><br>Dynatrace SaaSのお客様の場合、書式は`https://<your-environment-id>.live.dynatrace.com`です。<br><br>Dynatrace Managedのお客様の場合、書式は`https://<your-managed-url>/e/<environmentId>`です |
| [!DNL Dynatrace Environment ID] | Dynatrace 環境 ID。 [Dynatrace Connectionの詳細を確認するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details)を参照してください。 お勧めします。 |
| [!DNL Dynatrace Environment Token] | Dynatrace 環境トークン。 [Dynatrace Connectionの詳細を確認するにはどうすればよいですか？](#how-do-i-get-my-dynatrace-connection-details)を参照してください。 お勧めします。<br><br>このトークンは秘密鍵とみなされるので、適切なセキュリティ対策を行ってください。 例えば、**zerobin.net** などの web サイトでパスワードで保護します。カスタマーサポートチケットはパスワードとともに参照できます。 |
| [!DNL Dynatrace API access token] | Dynatrace 環境の API アクセストークン。 作成方法については、[Dynatrace API アクセストークンの作成](#create-dynatrace-access-token)を参照してください。<br><br>このトークンは秘密鍵と見なされるので、適切なセキュリティ対策を行ってください。 例えば、**zerobin.net**&#x200B;などのweb サイトでパスワードを保護します。このweb サイトは、パスワードと共に、カスタマーサポートチケットが参照できます。<br> |
| [!DNL Dynatrace ActiveGate Port] | AEM 統合の接続先となる Dynatrace ActiveGate ポート。<br><br>このポートは、Dynatrace Managedでのみ必要です。 |
| [!DNL Dynatrace ActiveGate Network Zone] | [Dynatrace ActiveGate ネットワーク ゾーン &#x200B;](https://docs.dynatrace.com/docs/manage/network-zones)を使用すると、データセンターとネットワーク リージョン間でAEM モニタリング データを効率的にルーティングできます。<br><br>注：Dynatrace ActiveGate ネットワーク ゾーンはオプションです。 |
| [!DNL AEM Environment IDs] | AEM環境IDまたはDynatraceのIDを監視します。 |

>[!NOTE]
>
>Dynatraceが統合されると、以前に有効になっていた場合、New Relicなどの他のAPM ツールにデータが流れなくなります。

## FAQ {#faq}

### Dynatrace AEM Monitoring にはどのライセンスが必要ですか。 {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM Monitoring には Dynatrace ライセンスが必要です。 Dynatrace AEM ライセンスは、[Kubernetes コンテナのフルスタック監視](https://docs.dynatrace.com/docs/license/capabilities/app-infra-observability#gib-hour-calculation-for-containers-and-application-only-monitoring)に基づいています。 監視対象の AEM コンテナ（オーサーサービスおよびパブリッシャーサービス）のメモリサイズは自動的に検出されます。

AEM 環境別のアドビデプロイメント仕様は、次のとおりです。

* 実稼動：平均で 4 つのコンテナ、それぞれ 16 GB のメモリ
* 実稼動以外：平均で 4 つのコンテナ、それぞれ 8 GB のメモリ

Dynatrace ライセンスについて詳しくは、[Dynatrace プラットフォームのサブスクリプション](https://docs.dynatrace.com/docs/license)を参照してください。

### Dynatrace 接続の詳細を取得するにはどうすればよいですか。 {#how-do-i-get-my-dynatrace-connection-details}

1. Dynatrace環境に対して次のAPI リクエストを実行します。

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   `<environmentUrl>` を Dynatrace 環境 URL に置き換え、`<accessToken>` を作成した API アクセストークンに置き換えます。

1. 応答ペイロードから`<environmentId>`と`<environmentToken>`をコピーし、それらを安全な場所に保存します。

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Dynatrace API アクセス トークンを作成する {#create-dynatrace-access-token}

1. Dynatraceにログインします。
1. **[!DNL Access tokens]**&#x200B;に移動し、オプション **[!DNL Generate new token]**&#x200B;をクリックします。
1. [!DNL token name] を定義します。
1. トークンの範囲を **[!DNL PaaS integration - Installer download]** に設定します。
1. **[!DNL Generate token]** を選択します。
1. 生成されたアクセストークンをコピーし、安全な場所に保存します。





