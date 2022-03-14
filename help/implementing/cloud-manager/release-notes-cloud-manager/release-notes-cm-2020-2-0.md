---
title: AEM as a Cloud Service Release 2020.2.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2020.2.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: 3f3324d9-53db-458d-9523-2e0d5d6dc3f7
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2020.2.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2020.2.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2020.2.0 Cloud Manager のリリース日は 2020 年 2 月 13 日です。

## Cloud Manager {#cloud-manager}

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
