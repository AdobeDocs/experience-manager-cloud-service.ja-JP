---
title: 運用開始後
description: 問題を監視し、パフォーマンスを向上させる方法を説明します
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 1b9d49ce1ef8ad4b0a11400b41d8c9b880cbf884
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 73%

---

# 運用開始後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM のトラブルシューティング"
>abstract="AEM に関する問題のトラブルシューティングに役立つ、開発者コンソールや CRXDE Lite などのツールと共に、継続的な開発とログの管理に関するベストプラクティスについて説明します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=ja" text="ログへのアクセスと管理"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=ja#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service の開発ツール"

このジャーニーは最後の部分なので、移行が完了した後に、問題を監視し、パフォーマンスを向上させる方法を学びます。 一時ファイルを確実にクリーンアップし、継続的な開発のベストプラクティスを確認し、ログを管理する必要があります。

## これまでの説明内容 {#story-so-far}

ジャーニーの前のステップでは、コードとコンテンツを AEM as a Cloud Service に移行する準備が整ったら、移行を実施して [運用を開始](/help/journey-migration/go-live.md) する方法を確認しました。

## 目的 {#objective}

このドキュメントでは、AEM as a Cloud Service 環境のトラブルシューティングに使用できるツールを説明します。

* **デベロッパーコンソール**
* **CRXDE Lite**
* **ログの管理**

## デベロッパーコンソール {#developer-console}

AEM as a Cloud Service 開発者環境でのデバッグは、開発環境、ステージング環境、実稼動環境の開発者コンソールで実行できます。

詳しくは、 [AEM as a Cloud Service向けの実装](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) 開発ツールの詳細を確認するには、を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージング環境や実稼動環境ではアクセスできません。

>[!IMPORTANT]
>実行時に `/libs` や `/apps` などの不変リポジトリに書き込むと、エラーが発生します。また、ステージング環境と実稼動環境用の開発者ツールにアクセスすることはできません。

詳しくは、 [開発とCRXDE Lite](/help/implementing/developing/tools/crxde.md) を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

詳しくは、 [ログへのアクセスと管理](/help/implementing/cloud-manager/manage-logs.md) ユーザーインターフェイスを通じて、または Cloud Manager を使用して API からログにアクセスしログを管理する方法について説明します。

## サポートへの問い合わせ {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="ヘルプ＆サポート"
>abstract="明確な情報を入手したり、懸念事項に対処したりするには、アドビの AEM サポートチームにお問い合わせください。"
>additional-url="https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud のサポート"

Cloud Service へのアクセスに関するご質問については、アドビ担当者または [Experience Cloud のサポート](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。

## 習得事項の文書化 {#document-learnings}

移行が完了したら、このプロセスで得られた知識を文書化します。 文書化には次の質問が役立つでしょう。

* 何がうまくいき、何がうまくいかなかったのか？
* 主な問題点は何でしたか？
* Recommendations（将来の移行がある場合）

移行後の学習内容を、組織内の関係者やチームと共有します。

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM as a Cloud Service 移行ジャーニーを完了しました。以下の方法を理解しておく必要があります。

* AEM as a Cloud Service への移行を開始する
* デプロイメントを AEM as a Cloud Service に移行する準備ができているかどうかを確認する
* コードとコンテンツをクラウド用に準備する
* 移行を実行する
* 問題を監視し、パフォーマンスを向上させる
