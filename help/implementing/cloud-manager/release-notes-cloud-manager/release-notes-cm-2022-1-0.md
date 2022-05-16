---
title: AEM as a Cloud Service リリース 2022.01.0 における Cloud Manager のリリースノート
description: AEM as a Cloud Service リリース 2022.01.0 における Cloud Manager のリリースノートです。
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service 2022.01.0 における Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.01.0 における Cloud Manager のリリースノートの概要を説明します。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service 2022.01.0の Cloud Manager のリリース日は 2022 年 1 月 20 日です。 次回のリリースは 2022年2月10日（PT）の予定です。

## 新機能 {#what-is-new}

* Cloud Manager は、複数のフルスタックパイプライン実行で [同じ git コミットが使用されていることを検出した場合、コードベースの再ビルドを避けます](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* AEM 環境ログにアクセスするには、**Deployment Manager** 製品プロファイルが必要になりました。このプロファイルを持たないユーザーには、ユーザーインターフェイスに無効なボタンが表示されます。
* UI は、Sites がソリューションとして有効化されていないプログラムのフロントエンドパイプライン設定を許可しません。
* Git パスワードの生成時に、有効期限が表示されます。

## バグの修正 {#bug-fixes}

* 一部のフロントエンドパイプラインデプロイメントで発生した null ポインター例外が修正されました。
* 古いバージョンの AEM が実行されている環境で、環境変数を追加、更新、削除できるようになりました。
* まれに、スケジュールされたステップを使用したパイプラインでは、イメージのビルドステップが「エラー」としてマークされなくなりました。
* リポジトリが 1 つだけのプログラムの場合、パイプライン実行画面にリポジトリ名が表示されるようになりました。
