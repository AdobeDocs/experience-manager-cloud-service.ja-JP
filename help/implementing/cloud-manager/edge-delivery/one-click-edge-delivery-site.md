---
title: ワンクリックでCloud ManagerにEdge Delivery サイトを作成
description: ボタンをクリックするだけで、Cloud ManagerでEdge Delivery サイトをすばやく作成する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---


# ワンクリックでCloud ManagerにEdge Delivery サイトを作成する方法について {#about-one-click-edge-delivery-site}

ワンクリックEdge Deliveryサービス（EDS）は、Cloud Manager内のEdge Delivery サイトのオンボーディングとデプロイメントを自動化するように設計されています。 ボタン 1 つをクリックするだけで、プロセスを大幅に簡略化できます。 この 1 回のクリックで必要なインフラストラクチャをプロビジョニングし、バージョン管理のために GitHub と統合し、Google Drive にドキュメントとアセットストレージを設定します。

この自動処理により、初期サイトの設定に必要な手動の手間を軽減できます。 エッジでのコンテンツ管理に関して、シームレスなワークフロー、スケーラビリティを確保し、チームのパフォーマンスを向上させます。

## 主な概念 {#key-concepts}

ワンクリックでEdge Delivery サイトを作成する場合の主要な概念。

| 重要な概念 | 説明 |
| --- | --- |
| Edgeの自動デプロイメント | <ul><li>ユーザーは、Edge Delivery サイトをすぐに作成および設定できます。</li><li>Cloud Managerと CI/CD ワークフローの統合を使用することで、手動でのオンボーディングプロセスの必要性を減らすか排除します。</li><li>Cloud Managerとの統合により、シームレスな CI/CD ワークフローが実現します。</li></ul> |
| Cloud Managerとの統合 | <ul><li>Cloud Managerのユーザーインターフェイスを使用して、ワンクリックEdge Delivery プロセスをトリガーします。</li><li>リポジトリの作成とデプロイメントを自動化するためのアクセスを提供します。</li></ul> |
| GitHub ベースのバージョン管理 | <ul><li>デプロイメントを標準化するために、事前定義済みのボイラープレートテンプレートを使用して、組織内に GitHub リポジトリを作成します。</li><li>コンテンツ更新のためのAEM ボットとのリンク。</li></ul> |
| ドキュメントとアセットストレージの統合 | <ul><li>ストレージ用のGoogle Drive フォルダーを生成します。<li>AEM コード同期アプリケーションをリポジトリにインストールして、シームレスな同期とデプロイメントを確実に行います。</li></li><li>複数の共同作業者がドキュメントを簡単に管理できるようにします。</li></ul> |
| セキュリティと拡張性 | <ul><li>エンタープライズセキュリティ標準へのコンプライアンスを確保します。</li><li>は、異なるEdge Delivery テナント配下にある複数のCloud Manager サイトをサポートします。</li></ul> |



## ワンクリックでCloud ManagerにEdge Delivery サイトを作成 {#one-click-edge-delivery-site}

ワンクリックで Adobe Edge 配信サイトを作成するには、利用可能なEdge Delivery Services ライセンスが必要です。 このライセンスはAdobe Experience Manager（AEM）の一部であり、Cloud Manager内でEdge Delivery Servicesを作成するために必要です。

権限に関しては、ビジネスオーナーの役割のメンバーであるか、Cloud Manager内のプログラムを追加または編集するための適切な権限を付与されている必要があります。 このアクセスレベルを使用すると、プログラムへのEdge Delivery Servicesの統合を管理できます。

詳しくは、[Cloud Manager の Edge Delivery Services の概要](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)も参照してください。

コンテンツの自動更新を行うには、最初にAEMの適切なボット設定を行う必要がありますか？ 本当？ 違う？

**Cloud ManagerでワンクリックでEdge Delivery サイトを作成するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のメニューの「**サービス**」見出しで、「![Web ページアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**」をクリックします。
1. Edge Delivery ページの [**Edge Delivery To-Do リスト**] ダイアログ ボックスで、[**前提条件を満たす**] グループ ボックスの [**準備**] をクリックします。
1. **Edge Delivery サイトをプロビジョニング** ダイアログボックスで、「**プロジェクト名**」テキストフィールドにサイトの名前を入力し、「**プロビジョニング**」をクリックします。
画面の上部中央の近くにトーストが表示され、Edge Delivery サイトのプロビジョニングが開始されたことが示されます。
プロビジョニングが完了し、サイトが検証されると、サイト名がEdge Delivery ページの **0}Edge Delivery sites} 領域に表示されます。**

### 新しく作成されたEdge Delivery サイトを探索します


1. サイト名の右側にある「Git リポジトリー」リンクをクリックします。

公開。

サイト名をクリックし、

変更を加えてから公開する

ページをプレビューで表示し、URL を変更してライブバージョンを表示します。

共同作業者を追加します。


## ワンクリックでEdge Delivery サイトをプレビュー

## ワンクリックでEdge Delivery サイトを公開





## ワンクリックEdge Deliveryサイトに共同作業者を追加


































これらの機能強化は、自動化の改善、設定プロセスの簡素化、Edge Delivery Services ユーザーの共同作業の強化を目的としています。<!-- CMGR-59362 -->

![ ワンクリックでEdge Delivery サイトを作成する ](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Edge Delivery サイトをプロビジョニングダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)