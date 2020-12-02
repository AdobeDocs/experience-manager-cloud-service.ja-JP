---
title: Cloud Serviceリリース2020.3.0としてのAEMのCloud Managerのリリースノート
description: Cloud Serviceリリース2020.3.0としてのAEMのCloud Managerのリリースノート
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 73%

---


# Cloud Service2020.3.0 {#release-notes}としてのAdobe Experience ManagerのCloud Managerのリリースノート

このページでは、AEMのCloud ManagerのリリースノートをCloud Service2020.3.0として概要を説明しています。

## リリース日 {#release-date}

AEMのCloud ManagerのCloud Service2020.3.0のリリース日は2020年3月6日です。

### 最新情報 {#what-is-new}

* ビルドステップのログを、ビルドステップの実行中に使用できるようになりました。
* パイプライン実行の詳細ページの一部のメッセージを編集し、わかりやすくしました。

### バグ修正  {#bug-fixes}

* カスタムおよび製品の機能テスト手順のログファイルを UI からダウンロードできなかった。
* Cloud Services プログラムの git リポジトリを作成できなかった場合、Deployment Manager の役割を持つユーザーが、このエラーから回復できないことがありました。
* サンドボックスアクティビティの作成中に特定のプログラムプログラムが発生すると、非実稼動パイプラインの作成前にユーザーの作成に失敗する可能性がありました。
* ビルド手順で使用される揮発性 SonarQube インスタンスが、設定されたタイムアウト内での開始に失敗する場合がありました。
* 同じ Cloud Service プログラムで開発環境を同時に作成すると、1 つだけ正常に作成できたという状況が発生する場合がありました。
* Cloud Service プログラムの Experience Cloud 通知が一貫して受信されなかった。
* 特定のプロジェクトでは、*ResourceResolver オブジェクトを常に閉じる必要があり*、Null Pointer 例外が発生していましたが、パイプラインの実行には影響しませんでした。