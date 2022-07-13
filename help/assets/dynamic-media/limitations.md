---
title: Dynamic Mediaの制限
description: 画像セットやスピンセットを作成したり、画像をアップロードしたりする際の、ベストプラクティスと適用される制限について説明します。PDF また、Dynamic Media Viewers でサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせについても説明します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: 8eac5e9453e130e0b3c007132d4a11324feef8a8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---

# Dynamic Mediaの制限

次の節では、Dynamic Mediaの制限について説明します。

このトピックには、次の節が含まれます。

* アセットタイプに関するDynamic Mediaのベストプラクティスと適用される制限

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## アセットタイプに関するDynamic Mediaのベストプラクティスと適用される制限

Adobeでは、ページ抽出用にスピンセットや画像セットを作成したり、PDFをアップロードしたりする際に、次のベストプラクティスを推奨し、次の制限を適用します。

| アセット — 制限タイプ | ベストプラクティス | 制限が適用されました | 2022 年 12 月 31 日の制限に変更 |
| --- | --- | --- | --- |
| **画像**  — 画像あたりのスマート切り抜き数 | 5 | 100 | 20 |
| **すべてのセット**  — セットあたりの重複アセット数 | 重複なし | 20 | 適用なし |
| **すべてのセット**  — セットあたりの最大アセット数 | 1 セットあたり 5～10 個の画像 | 1000 | 適用なし |
| **スピンセット** - 2D セットあたりの最大行数/列数 | 1 セットあたり 12～18 個の画像 | 1000 | 適用なし |
| **PDF**  — 抽出対象となるPDFの最大ページ数 |  | 5000（新しいアップロード用） | 100( すべてのPDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->
