---
title: Dynamic Media の制限
description: 画像セットやスピンセットを作成したり、PDF をアップロードしたりする際の、ベストプラクティスと適用される制限について説明します。また、Dynamic Mediaでサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせについても説明します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: e669fc821402f84fae58f457d5d9d1680c39ffaf
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 79%

---

# Dynamic Media の制限

次のセクションでは、Dynamic Media の制限について説明します。

このトピックには、次のセクションが含まれます。

* [アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限](#best-practice-enforced-limits)
* [Dynamic Mediaでサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせ](#unsupported-browser-os)

## アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限 {#best-practice-enforced-limits}

アドビでは、スピンセットや画像セットを作成したり、ページ抽出用に PDF をアップロードしたりする際、次のベストプラクティスを推奨し、次の制限を適用します。

| アセット - 制限タイプ | ベストプラクティス | 適用される制限 | 2022年12月31日（PT）の制限に変更 |
| --- | --- | --- | --- |
| **画像** - 画像あたりのスマート切り抜き数 | 5 | 100 | 20 |
| **すべてのセット** - 1 セットあたりの重複アセット数 | 重複なし | 20 | 適用なし |
| **すべてのセット** - 1 セットあたりの最大アセット数 | 1 セットあたり 5～10 個の画像 | 1000 | 適用なし |
| **スピンセット** - 2D セットあたりの最大行数／列数 | 1 セットあたり 12～18 個の画像 | 1000 | 適用なし |
| **PDF** - 抽出対象となる PDF の最大ページ数 |  | 5000（新しいアップロード用） | 100（すべての PDF 用） |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Mediaでサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせ {#unsupported-browser-os}

Dynamic Mediaでは、次の Web ブラウザーとオペレーティングシステムの組み合わせはサポートされていません。

* Internet Explorer 11 と Windows 7
* Internet Explorer 11 と Windows 8.1
* Internet Explorer 11 と Windows Phone 8.1
* Internet Explorer 11 と Windows Phone 8.1 Update
* Safari 6 と iOS 6.0.1
* Safari 7 と iOS 7.1
* Safari 7 と OS X 10.9 Mavericks
* Safari 8 と iOS 8.4
* Safari 8 と OS X 10.10 Yosemite

## TLS 1.0 および 1.1 のサポート終了 {#tls}

<!-- CQDOC-19433 -->

AdobeDynamic Mediaは、2022 年 9 月 30 日に以下のサポートを終了します。

* TLS（Transport Layer Security）1.0 および 1.1
* TLS 1.2 での以下の脆弱な暗号：
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

