---
title: 運用開始後段階
description: 運用開始後段階
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 73%

---

# 運用開始後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM のトラブルシューティング"
>abstract="AEMの問題のトラブルシューティングに役立つ開発者コンソールやCRXDE Liteなどのツールと共に、継続的な開発とログの管理に関するベストプラクティスを確認します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="ログへのアクセスと管理"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service の開発ツール"


運用開始後段階では、一時ファイルの確実なクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理が必要です。

AEM as a Cloud Service 環境のトラブルシューティングには、次のツールを使用できます。

* **デベロッパーコンソール**
* **CRX/DE Lite**
* **ログの管理**


## 開発者コンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージ環境、実稼動環境の開発者コンソールでおこなえます。

開発ツールについて詳しくは、[AEM as a Cloud Service 向けの実装](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)を参照してください。

## CRX/DE Lite {#crxde-lite}

ユーザーは開発環境では CRX/DE Lite にアクセスできますが、ステージング環境や実稼動環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。また、ユーザーはステージング環境と実稼動環境用の開発者ツールにはアクセスできません。

CRX/DE Lite を使用して AEM アプリケーションを開発する方法については、[CRX/DE Lite による開発](/help/implementing/developing/tools/crxde.md)を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

UI を使用して、または Cloud Manager 経由で API を使用してログにアクセスしログを管理する方法については、[ログへのアクセスと管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja)を参照してください。

### その他のサポート {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="ヘルプとサポート"
>abstract="アドビのAEMサポートチームに連絡して、詳細を確認したり、懸念事項に対処したりします。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Experience Cloudのサポート"

Cloud Serviceへのアクセスに関してご質問がある場合は、Adobe担当者または[Experience Cloudのサポート](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。
