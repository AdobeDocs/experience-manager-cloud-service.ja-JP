---
title: AEM as a Cloud Service Release 2022.9.0 の移行ツールのリリースノート
description: AEM as a Cloud Service リリース 2022.9.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 100%

---

# AEM as a Cloud Service リリース 2022.9.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.9.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.34 のリリース日は 2022年9月12日（PT）です。

### 新機能 {#what-is-new-bpa}

* BPA は、顧客がカスタムロガー設定を追加したかどうかを検出し、レポートできるようになりました。 AEM as a Cloud Service は、カスタムログファイルをサポートしていません。すべてのログ ファイルを `error.log` にパイプ処理する必要があります
* BPA は、顧客のリポジトリに存在するさまざまなバイナリ MIME タイプと、それらに関連付けられたカウントについてレポートできるようになりました。

### バグの修正 {#bug-fixes-bpa}

* BPA UI には、1 つのパターンで多数の調査結果を表示する際に、レンダリングの問題がありました。この問題が修正されました。
* BPA は、重大な緊急度を持つ非互換性の変更として、一部の調査結果を誤って報告していました。この問題が修正されました。
