---
title: リリースノート（2020.3.0）
description: リリースノート（2020.3.0）
exl-id: 0393c789-3999-4e51-be83-269d6eabd3f3
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# AEM as a Cloud Service 2020.3.0 のリリースノート {#release-notes}

このページでは、Experience Manager as a Cloud Service 2020.3.0 の一般的なリリースノートの概要を説明します。

## リリース日 {#release-date}

Experience Manager as a Cloud Service 2020.3.0 のリリース日は 2020 年 3 月 5 日です。

## Cloud Manager {#cloud-manager}

AEM as a Cloud Service リリース 2020.3.0 の Cloud Manager の新機能と更新点について説明します。

### 新機能 {#what-is-new}

* ビルドステップのログを、ビルドステップの実行中に使用できるようになりました。
* パイプライン実行の詳細ページの一部のメッセージを編集し、わかりやすくしました。

### バグ修正  {#bug-fixes}

* カスタムおよび製品の機能テスト手順のログファイルを UI からダウンロードできなかった。
* Cloud Services プログラムの Git リポジトリーを作成できなかった場合、Deployment Manager の役割を持つユーザーが、このエラーから回復できないことがありました。
* サンドボックスアクティビティの作成中に特定のプログラムプログラムが発生すると、非実稼動パイプラインの作成前にユーザーの作成に失敗する可能性がありました。
* ビルド手順で使用される揮発性 SonarQube インスタンスが、設定されたタイムアウト内での開始に失敗する場合がありました。
* 同じ Cloud Service プログラムで開発環境を同時に作成すると、1 つだけ正常に作成できたという状況が発生する場合がありました。
* Cloud Service プログラムの Experience Cloud 通知が一貫して受信されなかった。
* 特定のプロジェクトでは、*ResourceResolver オブジェクトを常に閉じる必要があり*、Null Pointer 例外が発生していましたが、パイプラインの実行には影響しませんでした。
