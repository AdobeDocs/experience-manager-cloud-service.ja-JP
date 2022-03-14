---
title: 運用開始後
description: 問題を監視し、パフォーマンスを向上させる方法を説明します
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 44%

---

# 運用開始後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM のトラブルシューティング"
>abstract="AEM に関する問題のトラブルシューティングに役立つ、開発者コンソールや CRXDE Lite などのツールと共に、継続的な開発とログの管理に関するベストプラクティスについて説明します。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=ja" text="ログへのアクセスと管理"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=ja#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service の開発ツール"

これはジャーニーの最後の部分なので、問題を監視し、移行が完了したらパフォーマンスを向上させる方法を学びます。 一時ファイルのクリーンアップ、継続的な開発に関するベストプラクティスの確認、ログの管理をおこなう必要があります。

## これまでの説明内容 {#story-so-far}

ジャーニーの前のステップで、移行の実行方法と [運用開始](/help/journey-migration/go-live.md) コードとコンテンツをAEM as a Cloud Serviceに移動する準備が整ったら、

## 目的 {#objective}

このドキュメントでは、AEMas a Cloud Service環境のトラブルシューティングに使用できるツールについて説明します。

* **デベロッパーコンソール**
* **CRXDE Lite**
* **ログの管理**

## デベロッパーコンソール {#developer-console}

開発環境、ステージ環境、実稼動環境では、AEMas a Cloud Serviceの開発者環境のデバッグを開発者コンソールで利用できます。

開発ツールについて詳しくは、[AEM as a Cloud Service 向けの実装](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは開発環境では CRXDE Lite にアクセスできますが、ステージング環境や実稼働環境ではアクセスできません。

>[!IMPORTANT]
>次のような不変リポジトリへの書き込み `/libs` および `/apps` 実行時にはエラーが発生します。 また、ステージング環境と実稼動環境用の開発者ツールにアクセスすることはできません。

CRXDE Lite を使用して AEM アプリケーションを開発する方法については、[CRXDE Lite による開発](/help/implementing/developing/tools/crxde.md)を参照してください。

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

## ドキュメントの学習 {#document-learnings}

移行が完了したら、このプロセスで得られた知識を文書化する必要があります。 ドキュメントの処理に役立つ質問を以下に示します。

* 何がうまくいき、何がしなかったのか？
* 主な痛みのポイントは何でしたか？
* 今後の移行の場合はRecommendations。

その後、これらの移行後の学習を、組織内の関係者やチームと共有する必要があります。

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEMas a Cloud Service移行ジャーニーが完了しました。 以下の方法を理解しておく必要があります。

* AEM as a Cloud Serviceへの移行の基本を学ぶ
* デプロイメントをAEM as a Cloud Serviceに移行する準備ができているかどうかを確認します。
* コードとコンテンツクラウドの準備
* 移行の実行
* 問題を監視し、パフォーマンスを向上
