---
title: 複数サイト管理のレポート
description: 単一のコードベースをリポジトリで活用して多言語サイトのプロジェクトを設定する方法に関するベストプラクティスの推奨事項について説明します。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 複数サイト管理のレポート {#repoless-msm}

このドキュメントでは、「`my-aem-site`」というプロジェクトのベースサイトが既に作成されていて、AEM MSM 機能を使用してローカライズすることを前提としています。

レポートユースケースに対して既にプロジェクトを設定している場合、クラウド設定はルートページ `/content/my-aem-site` のレベルで割り当てられます。 多言語サイトの場合、この設定の割り当てを `/content/my-aem-site/language-master/de` などの言語ルートに変更する必要があります。

