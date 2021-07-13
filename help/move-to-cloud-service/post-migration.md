---
title: 移行後段階
description: 移行後段階
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 96%

---


# 移行後 {#post-migration}

移行後段階では、一時ファイルの確実なクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理が必要です。

AEM as a Cloud Service 環境のトラブルシューティングには、次のツールを使用できます。

* **開発者コンソール**
* **CRXDE Lite**
* **ログの管理**

## デベロッパーコンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージ環境、実稼動環境の開発者コンソールでおこなえます。

開発ツールについて詳しくは、[AEM as a Cloud Service 向けの実装](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools)を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは開発環境では **CRXDE Lite** にアクセスできますが、ステージング環境や実稼働環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。また、ユーザーはステージング環境と実稼動環境用の開発者ツールにはアクセスできません。

CRXDE Lite を使用して AEM アプリケーションを開発する方法については、[CRXDE Lite による開発](/help/implementing/developing/tools/crxde.md)を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

UI を使用して、または Cloud Manager 経由で API を使用してログにアクセスしログを管理する方法については、[ログへのアクセスと管理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja)を参照してください。

### その他のサポート {#additional-support}

Cloud Service へのアクセスに関するご質問は、アドビ担当者または Adobe AEM CQ サポートポータルにお問い合わせください。
