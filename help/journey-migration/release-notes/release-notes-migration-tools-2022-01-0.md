---
title: AEM as a Cloud Service Release 2022.1.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.1.0 の移行ツールのリリースノート
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: ht
source-wordcount: '133'
ht-degree: 100%

---

# AEM as a Cloud Service Release 2022.1.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.1.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.7.18 のリリース日は 2022年1月18日（PT）です。

### 新機能 {#what-is-new-ctt}

* コンテンツ転送ツールの抽出段階に切替スイッチが追加され、ユーザーが抽出中に [事前コピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja) を無効にできるようになりました。最適な抽出速度を得るには、小さな移行セットの場合、または最後の抽出以降に追加された BLOB が数個しかない場合は、抽出中の事前コピーを無効にする必要があります。

### バグの修正 {#bug-fixes-ctt}

* 抽出時の実行タイムアウトを減らすために更新されたデフォルト設定。
