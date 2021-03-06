---
title: AEM as a Cloud Service Release 2022.4.0 の移行ツールのリリースノート
description: AEM as a Cloud Service Release 2022.4.0 の移行ツールのリリースノート
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 31%

---

# AEM as a Cloud Service Release 2022.4.0 の移行ツールのリリースノート {#release-notes}

このページでは、AEM as a Cloud Service 2022.4.0 の移行ツールのリリースノートの概要を説明しています。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.28 のリリース日は 2022 年 4 月 22 日です。

### 新機能 {#what-is-new-bpa}

* サポートされていない Asset Manager API の使用状況を検出し、レポートする機能。 AEM as a Cloud Serviceではサポートされなくなった API は 4 つあります。 お客様は、これらの API を使用しなくなり、新しいアセットアップロード方法を使用する必要があります。

* コンテンツフラグメントテンプレートの使用を検出する機能。 AEM as a Cloud Serviceでの新しいコンテンツフラグメントの作成で、コンテンツフラグメントテンプレートがサポートされなくなりました。 コンテンツフラグメントテンプレートを置き換えるには、コンテンツフラグメントモデルを作成する必要があります。

* リポジトリ内のアセットの metadate ノードの下に 100 を超える子孫を持つアセットを検出できます。 このようなアセットで構成されるフォルダーを読み込む際に、パフォーマンスを向上させるために必要でないメタデータノードを削除することをお勧めします。

* 使用されるデータストアのタイプを検出し、レポートする機能。

* AEM Form Portal のパターンが更新されました。

### バグ修正 {#bug-fixes-bpa}

* BPA は、お客様のコンポーネントに対してのみレポートするのではなく、コアコンポーネントの結果をレポートしていました。 この問題が修正されました。
