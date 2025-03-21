---
title: Dynamic Media の制限
description: 画像セットやスピンセットを作成したり、PDF をアップロードしたりする際の、ベストプラクティスと適用される制限について説明します。また、Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせについても学びます。
contentOwner: Rick Brough
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 92%

---

# Dynamic Media の制限

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

次のセクションでは、Dynamic Media の制限について説明します。

このトピックには、次のセクションが含まれます。

* [アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限](#best-practice-enforced-limits)
* [Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせ](#unsupported-browser-os)

## アセットタイプに関する Dynamic Media のベストプラクティスと適用される制限 {#best-practice-enforced-limits}

アドビでは、スピンセットや画像セットを作成したり、ページ抽出用に PDF をアップロードしたりする際、次のベストプラクティスを推奨し、次の制限を適用します。

| アセット - 制限タイプ | ベストプラクティス | 適用される制限 |
| --- | --- | --- |
| **画像** - 画像あたりのスマート切り抜き数 | 5 | 100 |
| **すべてのセット** - 1 セットあたりの重複アセット数 | 重複なし | 20 |
| **すべてのセット** - 1 セットあたりの最大アセット数 | 1 セットあたり 5～10 個の画像 | 1000 |
| **スピンセット** - 2D セットあたりの最大行数／列数 | 1 セットあたり 12～18 個の画像 | 1000 |
| **PDF** - 抽出対象となる PDF の最大ページ数 |  | 100（すべての PDF 用） |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media でサポートしていない web ブラウザーとオペレーティングシステムの組み合わせ {#unsupported-browser-os}

Dynamic Media では、次の web ブラウザーとオペレーティングシステムの組み合わせをサポートしていません。

* Internet Explorer 11 と Windows 7
* Internet Explorer 11 と Windows 8.1
* Internet Explorer 11 と Windows Phone 8.1
* Internet Explorer 11 と Windows Phone 8.1 Update
* Safari 6 と iOS 6.0.1
* Safari 7 と iOS 7.1
* Safari 7 と OS X 10.9 Mavericks
* Safari 8 と iOS 8.4
* Safari 8 と OS X 10.10 Yosemite

## Secure Socket Layer 2.0 および 3.0 と Transport Layer Security 1.0 および 1.1 のサポート終了 {#tls}

<!-- CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->

2024年4月30日（PT）を以て、Adobe Dynamic Media は以下のサポートを終了します。

* SSL（Secure Socket Layer）2.0
* SSL 3.0
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
