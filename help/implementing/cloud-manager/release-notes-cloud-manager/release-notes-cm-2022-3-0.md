---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.3.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2022.3.0 のリリースノートです。
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 88%

---

# Adobe Experience Manager as a Cloud Service の Cloud Manager 2022.3.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager 2022.3.0 のリリースノートです。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service の最新のリリースノートについては、[このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) を参照してください。

## リリース日 {#release-date}

AEM as a Cloud Serviceの Cloud Manager リリース 2022.3.0 のリリース日は 2022 年 3 月 10 日です。 次回のリリースは 2022 年 4 月 8 日に予定されています。

## 新機能 {#what-is-new}

* AEM 環境ログにアクセスするには、開発者の役割を使用します。

## バグの修正 {#bug-fixes}

* 手動で作成した Git リポジトリのサブセットで名前の値が間違っていたので、ビルドアーティファクトの再利用機能が有効に働きませんでした。これらのリポジトリの名前が変更され、Cloud Manager API／UI では修正された名前がユーザーに表示されます。
* 実稼動以外のパイプラインから得られたビルドアーティファクトが、実稼動のフルスタックパイプラインで不適切に再利用されていました。
* コード品質パイプラインを追加または編集する際に、指標の失敗を処理するためのオプションが表示されなくなりました。
* 予期しないパイプライン変数設定がビルドステップで一部生じる可能性がありました。
