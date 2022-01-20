---
title: AEM as a Cloud Service Release 2022.01.0 Cloud Manager のリリースノート
description: AEM as a Cloud Serviceリリース2022.01.0の Cloud Manager のリリースノートです。
feature: Release Information
source-git-commit: 8da3976250c94d5858d07a83b0eb395fab9a3eda
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 12%

---


# Adobe Experience Manager as a Cloud Service 2022.01.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.01.0の Cloud Manager のリリースノートの概要を説明します。

>[!NOTE]
>
>参照： [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service 2022.01.0の Cloud Manager のリリース日は 2022 年 1 月 20 日です。 次回のリリースは 2022 年 2 月 10 日に予定されています。

## 新機能 {#what-is-new}

* Cloud Manager では次の処理がおこなわれます。 [同じ git コミットが使用されたことを検出した場合は、コードベースを再構築しないでください](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 複数のフルスタックパイプライン実行で実行する場合。
* AEM環境ログにアクセスするには、 **デプロイメントマネージャー** 製品プロファイル。 このプロファイルを持たないユーザーには、ユーザーインターフェイスに無効なボタンが表示されます。
* Sites がソリューションとして有効になっていないプログラムに対しては、UI ではフロントエンドパイプライン設定を許可しません。
* Git パスワードを生成すると、有効期限が表示されます。

## バグ修正 {#bug-fixes}

* 一部のフロントエンドパイプラインデプロイメントで発生した Null ポインターの例外が修正されました。
* 環境で古いバージョンのAEMが実行されている場合に、環境変数を追加、更新および削除できるようになりました。
* まれに、スケジュール済みステップを使用したパイプラインでは、イメージのビルドステップがエラーとしてマークされなくなりました。
* リポジトリが 1 つだけのプログラムの場合、パイプライン実行画面にリポジトリ名が表示されるようになりました。
