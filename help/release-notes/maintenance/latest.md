---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のメンテナンスリリースノート'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 8a1ed1e44db0154854af73a96339d8e416afd3b4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 36%

---

# メンテナンスリリースノート {#maintenance-release-notes}

次の節では、Experience Manager as a Cloud Service の最新のメンテナンスリリースに関する技術リリースノートの概要を説明します。

## リリース 13420 {#release-13420}

2023 年 9 月 12 日に公開されたメンテナンスリリース13420の継続的な改善点を以下にまとめます。 このメンテナンスリリースは、リリース13323に代わるものです。

2023.9.0 機能のアクティベーションでは、このメンテナンスリリースの機能がすべて提供されます。 詳しくは、 [Experience Managerリリースロードマップ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=ja) を参照してください。

### 機能強化 {#enhancements-13420}

- ASSETS-19544：プロパティによって最終変更されたアセットが、処理をリクエストするユーザーに設定されるようになりました。

### 修正された問題 {#fixed-issues-13420}

- ASSETS-27628：アセット検索パネルのカスタマイズ時に誤った「チャネル」ノードが作成される
- ASSETS-27539：制限付き正規表現照合をアップロードします。
- ASSETS-26530：統合シェルで、ユーザーが元のページに戻りません。
- ASSETS-22719：スマート切り抜きブレークポイントの命名でブラケットが表示されると、スマート切り抜き編集機能が壊れます。
- ASSETS-27726: linkshare.html のインデックスは、Googleでは作成できません。
- ASSETS-27791：メタデータスキーマの検証は、最初のフィールドに対してのみおこなわれます。
- ASSETS-25544：無効になっている CDN キャッシュの無効化ボタンを修正しました。
- ASSETS-26575：画像セット作成時の名前の切り捨てを修正しました。
- ASSETS-26705:DM 以外のフォルダーアセットとコンテンツフラグメントで不要な処理を修正しました。
- ASSETS-25740：下向き矢印キーを使用して、「スマート切り抜きを編集」ページの編集/切り抜きコントロールの名前と役割を読み上げないスクリーンリーダーを修正しました。
- CQ-4354266：インボックス項目を開けません。
- CQ-4354347: AEM Translations を更新しました。
- DISP-1009: User-Agent as non first header trims X-Forwarded-Host.
- 様々なアクセシビリティおよびセキュリティ関連の修正。

### 既知の問題 {#known-issues-13420}

なし。

### 組み込みテクノロジー {#embedded-tech-13420}

| テクノロジー | バージョン | リンク |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | バージョン 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Version 1.4.20-1.4.0 | [HTML テンプレート言語仕様](https://github.com/adobe/htl-spec) |
| AEM コアコンポーネント | バージョン 2.23.2 | [AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components) |
