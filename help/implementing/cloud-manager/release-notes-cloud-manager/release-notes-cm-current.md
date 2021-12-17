---
title: AEM as a Cloud Service Release 2021.12.0 Cloud Manager のリリースノート
description: AEM as a Cloud Serviceリリース2021.12.0の Cloud Manager のリリースノートです。
feature: Release Information
source-git-commit: fc1eae86097f0cc928860ff7f43e3177f2e8f3a1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---


# Adobe Experience Manager as a Cloud Service 2021.12.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.12.0の Cloud Manager のリリースノートの概要を説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 2021.12.0の Cloud Manager のリリース日は 2021 年 12 月 16 日です。 次回のリリースは 2022 年 1 月に予定されています。

### 新機能 {#what-is-new}

* UI に既に表示されているコミットハッシュも API で提供されるようになりました。
* アクティビティページに、パイプラインの詳細の概要を一目で確認できる、実行中のパイプラインのポップオーバーが含まれるようになりました。
* アクティビティページに表示される追加の詳細を含めるための更新が追加されました。
* Cloud Manager の「学習」タブで、API ガイドと関連リソースにすばやくアクセスできるようになりました。
* デプロイメントマネージャーの役割を持つユーザーは、リポジトリページのアクションメニューから、ブランチのないリポジトリのプロジェクト/ブランチ作成ウィザードを開始できるようになりました。
* パイプラインの追加または編集ワークフローに属するデプロイメントマネージャーが、選択したリポジトリにブランチがない場合のブランチまたはプロジェクトの作成方法に関する情報を受け取るようになりました。
* 次の目的で、新しい Cloud Manager セルフサービス機能が追加されました。 [環境レベルでの自由形式の変数とシークレットの追加](/help/implementing/cloud-manager/environment-variables.md)
* 新しい [参照デモアドオン](/help/journey-sites/demos-add-on/overview.md) （2021 年 12 月 17 日から利用可能）AEM製品の最新のデモコードベースをインストールし、新しい [クイックサイト作成ツール](/help/journey-sites/quick-site/overview.md) （サイト内）
* フロントエンドパイプラインでパイプライン変数がサポートされるようになりました。
* すべてのサンドボックスに対して、プログラムの編集ダイアログで Screens を有効にできるようになりました。
* 概要ページのコールトゥアクションカードで提供されるガイダンスが更新され、実稼動フルスタックパイプラインとの関連が正確に反映されました。
* ソースコード、コミット ID などのパイプラインに適用できる追加の詳細を表示するため、アクティビティページが強化されました。
* TXT エントリ（「TXT レコード」ではなく「TXT 値」）をコピーする際に、UI が若干更新され、混乱が生じる可能性がなくなりました。
* [証明書エラーに関するドキュメント](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) のを更新し、トラブルシューティング手順と共にその他の例を取り上げました。
* フロントエンドパイプラインの実行で、実稼動環境へのデプロイメント前にオプションを拒否または承認できるようになりました。

### バグ修正 {#bug-fixes}

* 機能および UI テストアーティファクトがビルドステップログに含まれていませんでした。
* 製品、機能、UI のテスト手順のログに、パブリック API からアクセスできなかった問題を修正しました。
* まれに、環境の詳細ページからパブリッシュまたはプレビューサービスへのリンクが機能しないことがありました。
* ユーザーが名前フィールドに別の名前を入力した場合でも、完全なスタック実稼動パイプラインの名前は「実稼動パイプライン」のままです。
