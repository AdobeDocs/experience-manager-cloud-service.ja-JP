---
title: Adobe Experience Manager as a Cloud Service の概要 - 用語
description: 'Adobe Experience Manager as a Cloud Service の概要 - 用語。 '
translation-type: ht
source-git-commit: 465172db5bbc3b1dc3b42164d759a45e0ff13a8e
workflow-type: ht
source-wordcount: '336'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service - 用語 {#adobe-experience-manager-as-a-cloud-service-terminology}

Adobe Experience Manager (AEM) as a Cloud Service に関連して、次の用語が使用されます。

## 製品 {#products}

| 製品 | 説明 |
|---|---|
| AEM as a Cloud Service | AEM アプリケーションのクラウドネイティブな利用手段 |
| AEM Assets as a Cloud Service | クラウドネイティブかつ拡張可能なソリューションとしてのデジタルアセット管理（DAM）機能。デジタルアセットの取り込み、処理、管理をおこなうと同時に、より広範な Adobe Experience Cloud および Adobe Creative Cloud エコシステムとも統合されています。 |
| AEM Sites as a Cloud Service | AEM Sites アプリケーションを備えた AEM as a Cloud Service インスタンスです。 |

## インスタンスとパイプライン {#instances-and-pipelines}

| インスタンス | 説明 |
|---|---|
| Adobe パイプライン | コンテンツをオーサーからパブリッシュに公開するためのメカニズムです。 |
| AEM オーサー層 | Sites と Assets のオーサリング環境を表しています。 |
| AEM パブリッシュ層 | Sites のパブリッシュ環境を表しています。 |


<!-- This section of the table must be alphabetic -->

## 用語 {#terminology}

| 用語 | 説明 |
|---|---|
| AEM イメージ | AEM 製品コードとカスタムコードを一緒に含んだデプロイ可能なアーティファクトです。 |
| アセットマイクロサービス | レンディション生成、PDF 処理、サブアセット処理、テキスト抽出など、アセット処理の様々な使用例に対応する、クラウドベースのデジタルアセット処理サービスです。詳しくは、[アセットマイクロサービスの概要](/help/assets/asset-microservices-overview.md)を参照してください。 |
| Cloud Manager の Git リポジトリ | ユーザーがコードと設定を保存する場所です。 |
| クラウドプロバイダー | AEM as a Cloud Service は現在 Azure をサポートしています。AWS のサポートはロードマップ項目です。 |
| コンテンツ配信ネットワーク（CDN） | AEM as a Cloud Service の出荷時には、デフォルトの CDN が設定されています。その主な目的は、ブラウザーの近くの CDN エッジノードからキャッシュ可能なコンテンツを配信することで、待ち時間を減らすことです。AEM アプリケーションの最適なパフォーマンスを得るために、完全に管理および設定されています。 |
| コンテンツリポジトリ | コンテンツが永続的に保存される場所です。 |
| エンタープライズレベルの分離 | AEM as a Cloud Service の各インスタンスは、他のインスタンスとは切り離されています。 |
| ゴールデンマスター | AEM パブリッシュ層です。 |
| オーケストレーションエンジン | AEM as a Cloud Service では、オーケストレーションエンジンを使用して、すべてのオーサーサービスとパブリッシュサービスが必要に応じて確実に拡大／縮小されるようにします。 |
