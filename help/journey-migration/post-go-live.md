---
title: 運用開始後
description: 問題を監視し、パフォーマンスを向上させる方法を説明します
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 100%

---

# 運用開始後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM のトラブルシューティング"
>abstract="AEM に関する問題のトラブルシューティングに役立つ、開発者コンソールや CRXDE Lite などのツールと共に、継続的な開発とログの管理に関するベストプラクティスについて説明します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja" text="ログへのアクセスと管理"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service の開発ツール"

これはジャーニーの最後の部分です。移行が完了したので、問題を監視してパフォーマンスを向上させる方法を確認します。一時ファイルを確実にクリーンアップし、継続的な開発のベストプラクティスを確認し、ログを管理する必要があります。

## これまでの説明内容 {#story-so-far}

ジャーニーの前のステップでは、コードとコンテンツを AEM as a Cloud Service に移行する準備が整ったら、移行を実施して [運用を開始](/help/journey-migration/go-live.md) する方法を確認しました。

## 目的 {#objective}

このドキュメントでは、AEM as a Cloud Service 環境のトラブルシューティングに使用できるツールを説明します。

* **デベロッパーコンソール**
* **CRXDE Lite**
* **ログの管理**

## デベロッパーコンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージング環境、実稼動環境の開発者コンソールで実行できます。

開発ツールについて詳しくは、 [AEM as a Cloud Service 向けの実装](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージング環境や実稼動環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。ユーザーは、ステージング環境と実稼動環境用の開発者ツールにもアクセスできません。

CRXDE Lite を使用して AEM アプリケーションを開発する方法については、 [CRXDE Lite による開発](/help/implementing/developing/tools/crxde.md) を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

UI を使用して、または Cloud Manager 経由で API を使用してログにアクセスしログを管理する方法については、[ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md)を参照してください。

## サポートへの問い合わせ {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="ヘルプ＆サポート"
>abstract="詳しい説明が必要な場合や、懸念事項の対応については、AEM サポートチームまでお問い合わせください。"
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud のサポート"

Cloud Service へのアクセスに関するご質問については、アドビ担当者または [Experience Cloud のサポート](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。

## 習得事項の文書化 {#document-learnings}

移行が完了したら、このプロセスで得られた知識を文書化する必要があります。文書化には次の質問が役立つでしょう。

* 何がうまくいき、何がうまくいかなかったのか？
* 主な問題点は何でしたか？
* 今後の移行における推奨事項は？

次に、移行後に得られたこれらの気づきを組織内の関係者やチームと共有する必要があります。

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM as a Cloud Service 移行ジャーニーを完了しました。以下の方法を理解しておく必要があります。

* AEM as a Cloud Service への移行を開始する
* デプロイメントを AEM as a Cloud Service に移行する準備ができているかどうかを確認する
* コードとコンテンツをクラウド用に準備する
* 移行を実行する
* 問題を監視し、パフォーマンスを向上させる
