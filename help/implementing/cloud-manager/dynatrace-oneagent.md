---
title: Dynatrace OneAgent
description: AEM as a Cloud Serviceでの Dynatrace の OneAgent の使用方法を学ぶ
source-git-commit: 2e70c8be73915bea860b98e02c08772bb4f5dcd2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

Adobeは、Dynatrace の OneAgent を使用して、企業の展開の一環としてAEMas a Cloud Serviceを監視し、潜在的な問題の原因を特定し、必要に応じて修正を行う機能を提供します。 <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## OneAgent とAEM as a Cloud Serviceの統合 {#integrating-oneagent-with-aem-as-a-cloud-service}

Dynatic OneAgent のお客様は、カスタマーサポートチケットを通じて接続をリクエストすることで、AEMの使用状況を監視できます。

接続要求に必要な詳細を以下に示します。

| **フィールド** | **説明** |
|---|---|
| 動的環境 URL | Dynatrace 環境の URL。<br><br>Dynatrace SaaS のお客様の場合、形式は次のようになります。 `https://<environment>.live.dynatrace.com`.<br><br>Dynatrace が管理するお客様の場合、形式は次のようになります。 `https://<your-managed-url>/e/<environmentId>` |
| 動的環境 ID | 動的環境 ID（環境 URL にあります） |
| 動的環境トークン | OneAgent 環境トークンです。 この作成方法については、 Dynaterace のドキュメントを参照してください。<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。 |
| Dynatrace API アクセストークン | Dynatrace 環境の API アクセストークン。 この作成方法については、 Dynaterace のドキュメントを参照してください。<br><br>これは秘密と見なす必要があるので、適切なセキュリティプラクティスを使用します。 例えば、Web サイト ( 例： **zerobin.net**：カスタマーサポートチケットで参照できる、パスワードと共に。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| ダイナトレースの宛先のポート | ダイナトレースの宛先のポート。<br><br>注意：これは、Dynatrace Managed でのみ必要です。 |
| AEM環境 ID | 監視する Dynater Cloud のAEM環境 ID。 |


