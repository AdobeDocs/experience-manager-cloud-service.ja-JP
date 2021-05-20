---
title: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 19%

---

# Adobe Experience Manager as a Cloud Service 2021.2.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* Assetsのお客様は、Cloud Manager UIを使用して、セルフサービス方式でBrand Portalインスタンスをデプロイするタイミングと場所を選択できるようになりました。 Assetsソリューションを使用する通常の（サンドボックス以外の）プログラムの場合、Brand Portalを実稼動環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼動環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に特定された非推奨APIのリストが絞り込まれ、最新のCloud ServiceSDKリリースで廃止された追加のクラスとメソッドが含まれるようになりました。

* Cloud ManagerのSonarQubeプロファイルが更新され、Sonarルールsquidが削除されました：S2142。 これは、スレッドの中断のチェックと競合しなくなります。

* 関連する環境に実行中のパイプラインが関連付けられているか、現在承認ステップの待機中であるため、Cloud Manager UIから、ドメイン名を一時的に追加/更新できない可能性があるユーザーに通知されます。

* ビルドと品質のスキャンの失敗を避けるために、 sonarのプレフィックスが付いた顧客`pom.xml`ファイルで設定されたプロパティが動的に削除されるようになりました。

* Cloud ManagerのUIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、一時的にSSL証明書を選択できない可能性があるユーザーに通知されます。

* コード品質ルールが追加され、Cloud Serviceの互換性の問題に対応できるようになりました。

### バグ修正 {#bug-fixes}

* ドメイン名とのSSL証明書の一致で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が適切なエラーメッセージを含む2048ビット制限を満たさない場合、Cloud Manager UIからユーザーに通知されるようになりました。

* Cloud ManagerのUIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、一時的にSSL証明書を選択できない可能性があるユーザーに通知されます。

* 内部の問題が原因で、環境の削除が停止する場合があります。

* 一部のパイプラインエラーは、誤ってパイプラインエラーとして報告されました。
