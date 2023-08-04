---
title: リリースノート（2020.2.0）
description: 「[!DNL Adobe Experience Manager] as a Cloud Service 2020.2.0 のリリースノート」
exl-id: 005c4756-44c6-4af5-9b0c-0fc07bd211a0
source-git-commit: 9ceec0401b91bba2408bda89d4f2c486e2d51eec
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---

# AEM as a Cloud Service 2020.2.0 のリリースノート {#release-notes}

このページでは、Experience Manager as a Cloud Service 2020.2.0 の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

Experience Manager as a Cloud Service 2020.2.0 のリリース日は 2020 年 2 月 13 日です。

## Cloud Manager {#cloud-manager}

AEM as a Cloud Service リリース 2020.2.0 の Cloud Manager の新機能と更新点について説明します。

### 新機能 {#what-is-new}

* Adobe Experience Manager のアーキタイプのバージョンがバージョン 22 に更新されました。
* サンドボックス／デモプログラムのステージ環境と実稼動環境は、Cloud Manager UI を使用して更新できるようになりました。
* 余分なリダイレクトを避けるため、Experience Cloud 通知で使用される URL を最適化しました。
* タイムアウトしたパイプラインの実行ステップで、この状態が明示的に示されるようになりました。
* コードスキャン手順に、ダウンロード可能なログが追加されました。
* コードスキャン中に検出された問題を含むスプレッドシートに、特定のルールに関するドキュメントへのリンクを含む列が表示されるようになりました。

### バグ修正  {#bug-fixes}

* ブラウザーのセキュリティポリシーにより、パイプライン実行画面の特定のボタンが正しく機能しない場合があります。
* Cloud Manager のランディングページで、概要、環境、アクティビティのリンクを利用できる場合がありました。
* デプロイ時に一部のエラーが発生すると、新しいパイプラインの作成が誤って妨げられる可能性があります。
