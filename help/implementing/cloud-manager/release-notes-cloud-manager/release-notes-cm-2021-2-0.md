---
title: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノート
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: ht
source-wordcount: '388'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.2.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.2.0 Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.2.0 Cloud Manager のリリース日は 2021 年 2 月 11 日です。

## Cloud Manager {#cloud-manager}

### 新機能 {#what-is-new}

* Assets ユーザーは、Brand Portal インスタンスをデプロイするタイミングと場所を、Cloud Manager UI を使用してセルフサービス方式で選択できるようになりました。Assets ソリューションを使用する通常の（サンドボックス以外の）プログラムの場合は、Brand Portal を実稼働環境にプロビジョニングできるようになりました。プロビジョニングは、実稼働環境で 1 回だけ行えます。

* プロジェクトとサンドボックスの作成で使用される AEM プロジェクトアーキタイプがバージョン 25 に更新されました。

* コードスキャン中に特定される非推奨（廃止予定）API のリストが改善され、最新の Cloud Service SDK リリースで新たに非推奨となったクラスとメソッドが含まれるようになりました。

* Cloud Manager の SonarQube プロファイルが更新され、squid:S2142 の Sonar ルールが削除されました。これは、スレッド割り込みチェックと競合しなくなりました。

* 関連付けられた環境で、実行中のパイプラインが割り当てられているか、現在、承認ステップ待ちの状態にあるため、一時的にドメイン名を追加／更新できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* ユーザーの `pom.xml` ファイルで設定されたプロパティのうち、先頭に sonar が付いているものは、ビルドおよび品質スキャン時のエラーを避けるために、動的に削除されるようになりました。

* 現在デプロイ中のドメイン名で使用されている SSL 証明書を一時的に選択できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* Cloud Service の互換性の問題に対応するため、コード品質ルールが追加されました。

### バグ修正  {#bug-fixes}

* ドメイン名に対する SSL 証明書の照合で、大文字と小文字が区別されなくなりました。

* 証明書の秘密鍵が 2048 ビット制限を満たさない場合は、Cloud Manager UI から適切なエラーメッセージでユーザーに通知されるようになりました。

* 現在デプロイ中のドメイン名で使用されている SSL 証明書を一時的に選択できない可能性がある場合は、Cloud Manager UI からユーザーに通知されるようになりました。

* 場合によっては、内部の問題が原因で環境の削除が停止することがあります。

* パイプラインの不具合が誤ってパイプラインエラーとして報告されることがありました。
