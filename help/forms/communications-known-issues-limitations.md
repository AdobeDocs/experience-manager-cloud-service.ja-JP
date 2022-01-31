---
title: '既知の問題 '
description: コミュニケーションのベストプラクティス、既知の問題、制限事項
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 79%

---


# よくある質問、ベストプラクティス、既知の問題、制限事項 {#best-practices-known-issues-and-limitations}

通信 API の使用を開始する前に、よくある質問と、次の既知の問題と制限事項を確認してください。

## 既知の問題

- 特定のレンダリングタイプ (PDF、印刷 ) は、印刷オプションリストで 1 回だけ使用できます。 例えば、PCL レンダリングタイプを指定する PRINT オプションを 2 つ設定することはできません。

- バッチ設定の場合、OutputType（PDF、PRINT）と RenderType（PostScript、PCL、IPL、ZPL など）の値の組み合わせのインスタンスは 1 つだけ許可されています。

## ベストプラクティス

- AEM Cloud Service が使用するクラウド領域で、データファイルの blob コンテナストアをホストすることをお勧めします。

## よくある質問  {#faq}

**監視フォルダーやその他のストレージメカニズムを使用して、入出力を保存することはできますか？**

現時点では、Microsoft Azure ストレージを使用して、入力データと生成されたドキュメントを保存できます。Microsoft Azure ストレージは、[データ移動操作の自動化](https://docs.microsoft.com/ja-jp/azure/storage/common/storage-use-azcopy-v10)に対する様々なオプションを提供しています。

**Microsoft Azure ストレージアカウントは Experience Manager Forms Cloud Service ライセンスに含まれていますか？**

Microsoft Azure ストレージアカウントは、Experience Manager Forms Cloud Service ライセンスとは独立したものです。

**通信 API はデータを Experience Manager Forms Cloud Service サーバーに保存しますか？**

入力および出力データは、Microsoft Azure ストレージにのみ保存されます。

**通信 API は Experience Manager Forms Cloud Service でのみ使用できますか？オンプレミス環境でも同様の機能を利用できますか？**

AEM Forms Output サービスを使用すると、テンプレート（XFA または PDF）と顧客データを組み合わせて、PDF、PS、PCL、ZPL 形式のドキュメントを生成できます。

オンプレミス環境と比較すると、Cloud Service は、自動スケーリングとコスト効率のメリットがさらに大きくなります。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**複数のバッチ操作を同時に実行できますか？**
はい、複数のバッチ操作を同時に実行できます。競合を避けるために、操作ごとに異なるソースフォルダーと出力先フォルダーを常に使用するようにします。
