---
title: Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.8.0 のリリースノート
description: AEM as a Cloud Service の Cloud Manager 2023.8.0 のリリースノートです。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: d1640c14c796d7b7b6a7b236b38077e360559966
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 27%

---


# Adobe Experience Manager as a Cloud Service の Cloud Manager 2023.8.0 のリリースノート {#release-notes}

このページは、AEM as a Cloud Service の Cloud Manager リリース 2023.8.0 のリリースノートです。

>[!NOTE]
>
>詳しくは、 [このページ](/help/release-notes/release-notes-cloud/release-notes-current.md) (Adobe Experience Manager as a Cloud Serviceの最新のリリースノート )

## リリース日 {#release-date}

AEM as a Cloud Service の Cloud Manager 2023.8.0 のリリース日は 2023年8月10日（PT）です。次回のリリースは 2023年7月9日（PT）に予定されています。

## 新機能 {#what-is-new}

* コンテンツセットを [コンテンツをコピー](/help/implementing/developing/tools/content-copy.md) [コンテキスト対応の設定](/help/implementing/developing/introduction/configurations.md) が UI のコンテンツセットで許可されるようになりました。
* Cloud Manager UI でのエラーメッセージの理解しやすく表示を改善するための機能強化がおこなわれました。

## セルフ・サービス・コンテンツ・リストアの早期導入プログラム {#early-adoption}

[新しいセルフ・サービス・コンテンツ・リストア機能](/help/operations/restore.md) は、最大 7 日間のバックアップ復元を提供し、次の機能を備えた評価用に早期導入者が利用できるようになりました。

* 過去 24 時間のポイント・イン・タイム・バックアップのリストア
* 最大 7 日間の固定時間の復元

この新機能のテストとフィードバックの共有に関心がある場合は、に電子メールを送信してください。 `aemcs-restorefrombackup-adopter@adobe.com` Adobe IDに関連付けられた電子メールから。 注：

* アーリーアダプタープログラムは開発環境のみに限定されます。
* アーリーアダプタープログラムの提供は限られています。
* この機能は、誤って削除されたコンテンツをリカバリするためのもので、災害復旧を目的としたものではありません。

## バグの修正 {#bug-fixes}

* The **環境** トリガー後にメニューが閉じるようになりました **[コンテンツをコピー](/help/implementing/developing/tools/content-copy.md)** モーダルです。
* [パイプラインの再実行](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) は、以前の実行に `commitId` ビルドフェーズの状態に設定します。
* ユーザーが **アクティビティ** または **パイプライン** スクリーン。
* The `contentSetName` の値がログになくなり、の開始時に入力で提供されるようになりました。 [コンテンツコピー](/help/implementing/developing/tools/content-copy.md) 操作。
* まれな状況で、同じパイプラインから 2 回の実行を開始して「停止」状態になると、実行できなくなりました。
* 証明書の有効期限が切れると、証明書に関連付けられているドメイン名と IP 許可リストは CDN から削除されなくなります。
   * このような場合でも、サイトには引き続きアクセスできます。
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)Cloud Manager UI には、SSL 証明書の有効期限が近づいていることを示す事前警告がよりわかりやすく表示されます。
* Sites が Assets 専用プログラムのソリューションとして追加された場合に、AEMが公開エンドポイントへのアクセスを失う問題が修正されました。
