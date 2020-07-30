---
title: リリースノート（2020.2.0）
description: リリースノート（2020.2.0）
translation-type: tm+mt
source-git-commit: 3dc0d1d77595f7b3e890fb4b390eef5bcf84ecd8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 92%

---


# AEM as a Cloud Service 2020.2.0 のリリースノート {#release-notes}

このページでは、Experience Manager向けの一般的なリリースノートをCloud Service2020.2.0として概要を説明しています。

## リリース日 {#release-date}

Experience Manager as a Cloud Service 2020.2.0 のリリース日は 2020 年 2 月 13 日です。

## Cloud Manager {#cloud-manager}

AEM as a Cloud Service リリース 2020.2.0 の Cloud Manager の新機能と更新点について説明します。

### 最新情報 {#what-is-new}

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
