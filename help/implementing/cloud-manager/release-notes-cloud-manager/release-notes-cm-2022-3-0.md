---
title: Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート
description: AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートです。
feature: Release Information
source-git-commit: 437be8c82a4dee6c9e56af09afa7e9048c8cb3c0
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 58%

---


# Adobe Experience Manager as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノート {#release-notes}

このページでは、AEM as a Cloud Serviceの Cloud Manager 2022.3.0 のリリースノートについて説明します。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Service 10 2022 年 3 月 10 日にリリースされた Cloud Manager リリース 2022.3.0 のリリース日です。 次回のリリースは 2022年4月7日（PT）に予定されています。

## 新機能 {#what-is-new}

* AEM環境ログへのアクセスは、開発者ロールを使用しておこなうことができます。

## バグの修正 {#bug-fixes}

* 手動で作成した Git リポジトリのサブセットで名前の値が間違っていたので、ビルドアーティファクトの再利用機能が有効に働きませんでした。これらのリポジトリの名前が変更され、Cloud Manager API／UI では修正された名前がユーザーに表示されます。
* 実稼動以外のパイプラインから得られたビルドアーティファクトが、実稼動のフルスタックパイプラインで不適切に再利用されていました。
* コード品質パイプラインを追加または編集する際に、指標の失敗を処理するためのオプションが表示されなくなりました。
* 予期しないパイプライン変数設定がビルドステップで一部生じる可能性がありました。
