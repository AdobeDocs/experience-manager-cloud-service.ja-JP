---
title: 運用開始後
description: 問題を監視し、パフォーマンスを向上させる方法を説明します。
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 100%

---

# 運用開始後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM のトラブルシューティング"
>abstract="継続的な開発とログの管理に関するベストプラクティスを確認します。AEM に関する問題のトラブルシューティングに役立つ、Developer Console や CRXDE Lite などのツールについて説明します。"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs" text="ログへのアクセスと管理"
>additional-url="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service の開発ツール"

このジャーニーは最後の部分です。移行が完了した後で、問題を監視してパフォーマンスを向上させる方法を確認します。一時ファイルを確実にクリーンアップ、継続的な開発のベストプラクティスを確認し、ログを管理します。

## これまでの説明内容 {#story-so-far}

ジャーニーの前のステップでは、コードとコンテンツを AEM as a Cloud Service に移行する準備が整ったら、移行を実施して [運用を開始](/help/journey-migration/go-live.md) する方法を確認しました。

## 目的 {#objective}

このドキュメントでは、AEM as a Cloud Service 環境のトラブルシューティングに使用できるツールを説明します。

* **デベロッパーコンソール**
* **CRXDE Lite**
* **ログの管理**

## デベロッパーコンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージング環境、実稼動環境の開発者コンソールで実行できます。

開発ツールについて詳しくは、[AEM as a Cloud Service 向けの実装](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージング環境や実稼動環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。ユーザーは、ステージング環境と実稼動環境用の開発者ツールにもアクセスできません。

CRXDE Lite を使用して AEM アプリケーションを開発する方法について詳しくは、[CRXDE Lite による開発](/help/implementing/developing/tools/crxde.md)を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

ユーザーインターフェイスを通じて、または Cloud Manager を使用して API からログにアクセスしログを管理する方法について詳しくは、[ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

## サポートへの問い合わせ {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="ヘルプ＆サポート"
>abstract="明確な情報を入手したり、懸念事項に対処したりするには、アドビの AEM サポートチームにお問い合わせください。"
>additional-url="https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud のサポート"

Cloud Service へのアクセスに関するご質問については、アドビ担当者または [Experience Cloud のサポート](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。

## 習得事項の文書化 {#document-learnings}

移行が完了したら、このプロセスで得られた知識を文書化してください。文書化には次の質問が役立つでしょう。

* 何がうまくいき、何がうまくいかなかったのか？
* 主な問題点は何でしたか？
* 推奨事項（今後の移行がある場合）。

移行後に得られたこれらの気づきを組織内の関係者やチームと共有してください。

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM as a Cloud Service 移行ジャーニーを完了しました。以下の方法を理解しておく必要があります。

* AEM as a Cloud Service への移行を開始する
* デプロイメントを AEM as a Cloud Service に移行する準備ができているかどうかを確認する
* コードとコンテンツをクラウド用に準備する
* 移行を実行する
* 問題を監視し、パフォーマンスを向上させる
