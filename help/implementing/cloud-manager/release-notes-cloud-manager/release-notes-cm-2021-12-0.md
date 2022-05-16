---
title: AEM as a Cloud Service リリース 2021.12.0 の Cloud Manager のリリースノート
description: これらは、AEM as a Cloud Service リリース 2021.12.0 の Cloud Manager のリリースノートです。
feature: Release Information
source-git-commit: bd31dc0ca5b0f4cd84314dba67c8a611f490d377
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Experience Manager as a Cloud Service 2021.12.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2021.12.0 の Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.12.0の Cloud Manager のリリース日は 2021 年 12 月 16 日です。 次回のリリースは 2022 年 1 月 20 日に予定されています。

## 新機能 {#what-is-new}

* UI ではすでに表示されているコミットハッシュも、API で提供されるようになりました。
* アクティビティページにパイプラインを実行中のポップオーバーが追加され、パイプラインの詳細が一目でわかるようになりました。
* アクティビティページに表示される追加の詳細を含める更新を行いました。
* Cloud Manager の「学習」タブに、API ガイドと関連リソースへのクイックアクセスが追加されました。
* Deployment Manager のロールを持つユーザーは、リポジトリページのアクションメニューから、ブランチのないリポジトリに対してプロジェクト/ブランチ作成ウィザードを開始できるようになりました。
* パイプラインの追加または編集ワークフローにいる Deployment Manager は、選択したリポジトリにブランチがない場合、ブランチまたはプロジェクトを作成する方法を通知されるようになりました。
* 新しい Cloud Manager セルフサービス機能が追加され、 [環境レベルで自由形式の変数とシークレットを追加](/help/implementing/cloud-manager/environment-variables.md) できるようになりました。
* 新しい [参照デモアドオン](/help/journey-sites/demos-add-on/overview.md) （2021年12月17日（PT）に公開）を使用すると、AEM 製品の最新のデモコードベースをインストールして、Sites の新しい [クイックサイト作成ツール](/help/journey-sites/quick-site/overview.md) でデプロイ準備を整えることができます。
* フロントエンドパイプラインでパイプライン変数がサポートされるようになりました。
* プログラムを編集ダイアログで、すべてのサンドボックスに対して Screens を有効にできるようになりました。
* 概要ページのコールトゥアクションカードで示されるガイダンスが更新され、実稼動フルスタックパイプラインとの関連が正確に反映されました。
* ソースコードやコミット ID など、パイプラインに適用できる追加の詳細を表示するため、アクティビティページが強化されました。
* TXT エントリ（「TXT レコード」ではなく「TXT 値」）をコピーする際の UI が若干更新され、混乱が生じる可能性がなくなりました。
* [証明書エラーに関するドキュメント](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) を更新し、トラブルシューティング手順と共にその他の例を取り上げました。
* 実稼動環境へのデプロイメント前に拒否または承認するためのオプションが、フロントエンドパイプラインの実行で使用できるようになりました。
* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 32 に更新されました。


## バグの修正 {#bug-fixes}

* 機能テストおよび UI テストアーティファクトがビルドステップログに含まれていませんでした。
* 製品、機能、UI のテスト手順のログに、パブリック API からアクセスできませんでした。
* まれに、環境の詳細ページでパブリッシュサービスまたはプレビューサービスへのリンクが機能しないことがありました。
* フルスタック実稼動パイプラインの名前が、ユーザーが名前フィールドに別の名前を入力した場合でも、「実稼動パイプライン」のまま変わりません。
