---
title: AEM as a Cloud Service リリース 2024.07 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2024.07.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 34%

---

# AEM as a Cloud Service リリース 2024.07.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2024.07.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v3.0.16 のリリース日は 2024 年 7 月です。

### 新機能 {#what-is-new-ctt}

* 失敗時の CTT 抽出ログの自動アップロード。
* ユーザーは、抽出キーの更新時に取り込みを正常に実行できるようになりました。
* Azure アクセスキーと AzureDataStore の秘密鍵を使用して CTT 抽出を実行するためのサポートを追加しました。
* 無効なキーを使用して移行セットを作成すると、正しいエラーメッセージが表示されるようになりました。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.50 のリリース日は 2024 年 5 月です。

### バグ修正 {#bug-fixes-bpa}

* ベストプラクティスアナライザーで 16 MB を超えるすべてのノードが検出されるようになりました
* NCC 結果が不規則に発生する競合状態が修正されました。
