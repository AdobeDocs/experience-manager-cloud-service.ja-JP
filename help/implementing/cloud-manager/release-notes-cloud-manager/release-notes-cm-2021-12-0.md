---
title: AEM as a Cloud Service Release 2021.12.0 Cloud Manager のリリースノート
description: AEM as a Cloud Serviceリリース2021.12.0の Cloud Manager のリリースノートです。
feature: Release Information
source-git-commit: e402578fc95fd97f808fde01a860d4c583af4c9b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 40%

---


# Adobe Experience Manager as a Cloud Service 2021.12.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.12.0の Cloud Manager のリリースノートの概要を説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 2021.12.0の Cloud Manager のリリース日は 2021 年 12 月 16 日です。 次回のリリースは 2022年1月（PT）の予定です。

## 新機能 {#what-is-new}

* UI ではすでに表示されているコミットハッシュも、API で提供されるようになりました。
* アクティビティページにパイプラインを実行中のポップオーバーが追加され、パイプラインの詳細が一目でわかるようになりました。
* アクティビティページに表示される追加の詳細を含める更新を行いました。
* Cloud Manager の「学習」タブに、API ガイドと関連リソースへのクイックアクセスが追加されました。
* Deployment Manager のロールを持つユーザーは、リポジトリページのアクションメニューから、ブランチのないリポジトリに対してプロジェクト/ブランチ作成ウィザードを開始できるようになりました。
* パイプラインの追加または編集ワークフローにいる Deployment Manager は、選択したリポジトリにブランチがない場合、ブランチまたはプロジェクトを作成する方法を通知されるようになりました。
* 次の目的で、新しい Cloud Manager セルフサービス機能が追加されました。 [環境レベルでの自由形式の変数とシークレットの追加](/help/implementing/cloud-manager/environment-variables.md)
* 新しい [参照デモアドオン](/help/journey-sites/demos-add-on/overview.md) （2021 年 12 月 17 日から利用可能）AEM製品の最新のデモコードベースをインストールし、新しい [クイックサイト作成ツール](/help/journey-sites/quick-site/overview.md) （サイト内）
* フロントエンドパイプラインでパイプライン変数がサポートされるようになりました。
* すべてのサンドボックスに対して、プログラムの編集ダイアログで Screens を有効にできるようになりました。
* 概要ページのコールトゥアクションカードで提供されるガイダンスが更新され、実稼動フルスタックパイプラインとの関連が正確に反映されました。
* ソースコード、コミット ID などのパイプラインに適用できる追加の詳細を表示するため、アクティビティページが強化されました。
* TXT エントリ（「TXT レコード」ではなく「TXT 値」）をコピーする際に、UI が若干更新され、混乱が生じる可能性がなくなりました。
* [証明書エラーに関するドキュメント](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) のを更新し、トラブルシューティング手順と共にその他の例を取り上げました。
* フロントエンドパイプラインの実行で、実稼動環境へのデプロイメント前にオプションを拒否または承認できるようになりました。
* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 32 に更新されました。


## バグ修正 {#bug-fixes}

* 機能および UI テストアーティファクトがビルドステップログに含まれていませんでした。
* 製品、機能、UI のテスト手順のログに、パブリック API からアクセスできなかった問題を修正しました。
* まれに、環境の詳細ページからパブリッシュまたはプレビューサービスへのリンクが機能しないことがありました。
* 完全なスタック実稼動パイプラインの名前は、ユーザーが名前フィールドに別の名前を入力した場合でも、「実稼動パイプライン」のままです。
