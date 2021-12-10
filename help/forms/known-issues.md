---
title: 既知の問題と制限事項
description: ' [!DNL AEM Forms] as a Cloud Service 環境の既知の問題と制限事項'
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 100%

---

# 既知の問題と制限事項 {#known-issues-and-limitations}

[!DNL AEM Forms] as a Cloud Service を使用する前に、以下の既知の問題と制限事項を確認してください。

## 既知の問題 {#known-issues}

* アダプティブフォームをパブリッシュインスタンスからオーサーインスタンスで実行される AEM ワークフローに送信するテストは、通知があるまで追加および実行しないでください。

* 「**[!UICONTROL 保存]**」ボタンを含むテンプレートを使用しているアダプティブフォームを読み込むと、対応するテンプレートから削除された後も、「**[!UICONTROL 保存]**」ボタンが引き続きアダプティブフォームに表示されます。アダプティブフォームを公開する前に、「**[!UICONTROL 保存]**」ボタンを削除してください。フォームポータルと「ドラフトとして保存」機能を使用して復元し、ボタンを使用する場合は、リリースノートを確認してください。

* AEM ワークフローの&#x200B;**[!UICONTROL 変数設定]**&#x200B;の手順は、配列リストタイプの変数をサポートしていません。配列リストタイプの変数を設定するための処理手順を使用できます。

* 標準の HTML アップロードフィールドを含んだアダプティブフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信します。この問題は断続的に発生し、同期送信を使用した場合にのみ発生します。Apple iOS では、これは[既知の問題](https://feedbackassistant.apple.com/feedback/9117687)です。

* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS では、これは既知の問題です。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## 制限事項 {#limitations}

* XFA ベースのアダプティブフォームのサポートは、初期設定では利用できません。XFA ベースのアダプティブフォームを使用する場合は、使用事例と具体的な要件の詳細をアドビサポートにお問い合わせください。

