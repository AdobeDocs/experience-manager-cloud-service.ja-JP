---
title: 運用開始後段階
description: 運用開始後段階
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 100%

---

# 運用開始後 {#post-go-live}

運用開始後段階では、一時ファイルの確実なクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理が必要です。

AEM as a Cloud Service 環境のトラブルシューティングには、次のツールを使用できます。

* **デベロッパーコンソール**
* **CRX/DE Lite**
* **ログの管理**


## 開発者コンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージ環境、実稼動環境の開発者コンソールでおこなえます。

開発ツールについて詳しくは、[AEM as a Cloud Service 向けの実装](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)を参照してください。

## CRX/DE Lite {#crxde-lite}

ユーザーは開発環境では CRX/DE Lite にアクセスできますが、ステージング環境や実稼動環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。また、ユーザーはステージング環境と実稼動環境用の開発者ツールにはアクセスできません。

CRX/DE Lite を使用して AEM アプリケーションを開発する方法については、[CRX/DE Lite による開発](/help/implementing/developing/tools/crxde.md)を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

UI を使用して、または Cloud Manager 経由で API を使用してログにアクセスしログを管理する方法については、[ログへのアクセスと管理](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html)を参照してください。

### その他のサポート {#additional-support}

Cloud Service へのアクセスに関するご質問は、アドビ担当者または Adobe AEM CQ サポートポータルにお問い合わせください。
