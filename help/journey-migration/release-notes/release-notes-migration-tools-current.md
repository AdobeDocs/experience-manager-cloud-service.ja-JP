---
title: AEM as a Cloud Service Release 2022.9.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.9.0 の移行ツールのリリースノート
feature: Release Information
source-git-commit: 6b58b253c554fc2958fdff2b246f341f56b1639f
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 41%

---

# AEM as a Cloud Service Release 2022.9.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.9.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.34 のリリース日は 2022 年 9 月 12 日です。

### 新機能 {#what-is-new-bpa}

* BPA は、顧客がカスタムロガー設定を追加したかどうかを検出し、レポートできるようになりました。 AEM as a Cloud Serviceはカスタムログファイルをサポートしていません。 すべてのログファイルをパイプ経由で `error.log`
* BPA は、顧客のリポジトリに存在する様々なバイナリ MIME タイプと、それらに関連付けられたカウントをレポートできるようになりました。

### バグの修正 {#bug-fixes-bpa}

* BPA UI で、1 つのパターンで多数の結果を表示する際に、レンダリングの問題が発生していました。 この問題が修正されました。
* BPA は、一部の結果を重大度が重大な非互換性の変更と誤ってレポートしていました。 この問題が修正されました。