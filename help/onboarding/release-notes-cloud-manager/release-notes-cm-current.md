---
title: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
translation-type: tm+mt
source-git-commit: 968775b24441457143f497c2cfb1f9ece392d475
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 18%

---


# Adobe Experience Manager as a Cloud Service 2021.2.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* Cloud Manager実稼働パイプラインに、カスタムUIテスト機能が含まれるようになりました。

* アセットのお客様は、Cloud Manager UIを使用してセルフサービスの方法でBrand Portalインスタンスをいつ、どこにデプロイするかを選択できるようになります。 アセットソリューションを使用する通常の（Sandbox以外の）プログラムの場合、Brand Portalを実稼働環境でプロビジョニングできるようになりました。 プロビジョニングは、実稼働環境で1回だけ実行できます。

* プロジェクトとサンドボックスの作成で使用されるAEMプロジェクトアーキタイプがバージョン25に更新されました。

* コードスキャン中に識別された非推奨のAPIのリストが絞り込まれ、最新Cloud ServiceのSDKリリースで非推奨となった追加のクラスとメソッドが含まれるようになりました。

* SonarQubeプロファイル（Cloud Manager用）が更新され、squid:S2142というSonarルールが削除されました。 これは、スレッド割り込みチェックと競合しなくなります。

* Cloud Manager UIは、ドメイン名を一時的に追加/更新できない可能性があるユーザーに通知します。関連付けられた環境には実行中のパイプラインが割り当てられているか、現在、承認手順を待機中です。

* sonarのプリフィックスが付いた顧客`pom.xml`ファイルに設定されたプロパティは、ビルドおよび品質スキャンの失敗を回避するために、動的に削除されるようになりました。

* Cloud Manager UIには、現在展開中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* Cloud Serviceの互換性の問題をカバーするため、コード品質ルールが追加されました。

### バグ修正 {#bug-fixes}

* ドメイン名に対するSSL証明書の一致で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が2048ビットの制限を満たさない場合に、適切なエラーメッセージが表示されるように、Cloud Manager UIからユーザーに通知されるようになりました。

* Cloud Manager UIには、現在デプロイ中のドメイン名でSSL証明書が使用されている場合、SSL証明書を一時的に選択できない可能性があるユーザーに通知されます。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* 一部のパイプラインエラーは、誤ってパイプラインエラーとして報告されました。
