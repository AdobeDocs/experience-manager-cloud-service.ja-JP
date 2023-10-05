---
title: AEM as a Cloud Service リリース 2023.09.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.09.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
source-git-commit: c89ca7320d8f31d2545cadf98f39e577337b8918
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 38%

---

# AEM as a Cloud Service リリース 2023.09.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.09.0 の移行ツールのリリースノートの概要を説明しています。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v3.0.0 のリリース日は 2023 年 9 月 7 日です。

### 新着情報 {#what-is-new-ctt}

コンテンツ転送ツールが大幅に改善され、次の利点があります。
* AzCopy を利用して、すべての blob ID をコピーする代わりに、必要な blob ID のみをコピーすることで、コンテンツリポジトリのサブセットを移行する際の転送時間を短縮しました。
* Oak-upgrade を使用した差分コンテンツ追加の高速化
* インデックス作成プロセスをコンテンツ取り込みプロセスから分離することで、堅牢性を向上しました。 インデックス作成に失敗した場合、コンテンツを再度取り込む必要はありません。 インデックス作成のみが自動的に再起動し、時間と労力を大幅に節約
