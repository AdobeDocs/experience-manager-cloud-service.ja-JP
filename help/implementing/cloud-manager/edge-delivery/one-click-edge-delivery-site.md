---
title: ワンクリックでCloud ManagerにEdge Delivery サイトを作成
description: ボタンをクリックするだけで Cloud Manager で Edge Delivery サイトをすばやく作成する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 71%

---


# ワンクリックでCloud ManagerにEdge Delivery サイトを作成する方法について {#about-one-click-edge-delivery-site}

ワンクリック Edge Delivery Service（EDS）は、Cloud Manager 内での Edge Delivery サイトのオンボーディングとデプロイメントを自動処理するように設計されています。ボタン 1 回をクリックするだけで、プロセスが大幅に簡素化されます。この 1 回のクリックで、必要なインフラストラクチャがプロビジョニングされ、GitHub と統合してバージョン管理を行い、Google Drive でドキュメントとアセットのストレージが設定されます。

この自動処理により、最初のサイトを設定するのに必要な手作業の労力が軽減されます。エッジでのコンテンツ管理に関して、シームレスなワークフローとスケーラビリティが確保され、チームのパフォーマンスが向上します。

## 主な概念 {#key-concepts}

ワンクリックでEdge Delivery サイトを作成する場合の主要な概念。

| 主な概念 | 説明 |
| --- | --- |
| 自動処理されたエッジのデプロイメント | <ul><li>ユーザーは、Edge Delivery サイトをすぐに作成および設定できます。</li><li>Cloud Managerと CI/CD ワークフローの統合を使用することで、手動でのオンボーディングプロセスの必要性を減らすか排除します。</li><li>Cloud Managerとの統合により、シームレスな CI/CD ワークフローが実現します。</li></ul> |
| Cloud Manager との統合 | <ul><li>Cloud Manager のユーザーインターフェイスを使用して、ワンクリック Edge Delivery プロセスをトリガーします。</li><li>自動処理されたリポジトリの作成とデプロイメントへのアクセスを提供します。</li></ul> |
| GitHub ベースのバージョン管理 | <ul><li>事前定義済みのボイラープレートテンプレートを使用して、組織内に GitHub リポジトリを作成し、デプロイメントを標準化します。</li><li>コンテンツ更新に AEM ボットとリンクします。</li></ul> |
| ドキュメントとアセットのストレージ統合 | <ul><li>ストレージ用の Google Drive フォルダーを生成します。<li>AEM コード同期アプリケーションをリポジトリにインストールし、シームレスな同期とデプロイメントを確保します。</li></li><li>複数の共同作業者がドキュメントを簡単に管理できます。</li></ul> |
| セキュリティとスケーラビリティ | <ul><li>大規模法人向けのセキュリティ標準へのコンプライアンスを確保します。</li><li>異なる Cloud Manager テナントの複数の Edge Delivery サイトをサポートします。</li></ul> |



## ワンクリックでCloud ManagerにEdge Delivery サイトを作成 {#one-click-edge-delivery-site}

ワンクリックで Adobe Edge 配信サイトを作成するには、利用可能なEdge Delivery Services ライセンスが必要です。 このライセンスはAdobe Experience Manager（AEM）の一部であり、Cloud Manager内でEdge Delivery Servicesを作成するために必要です。

権限に関しては、ビジネス所有者の役割のメンバーであるか、Cloud Manager でプログラムを追加または編集する適切な権限が付与されている必要があります。このアクセスレベルでは、Edge Delivery Services のプログラムへの統合を管理できます。

詳しくは、[Cloud Manager の Edge Delivery Services の概要](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)も参照してください。

コンテンツの自動更新を行うには、まず適切な AEM ボット設定を行う必要がありますか？正解ですか？不正解ですか？

**Cloud ManagerでワンクリックでEdge Delivery サイトを作成するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のサイドメニューの&#x200B;**サービス**&#x200B;見出しで、![web ページアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery Sites**」をクリックします。
1. Edge Delivery ページの **Edge Delivery の TODO リスト**&#x200B;ダイアログボックスの「**前提条件を完了**」グループボックスで、「**プロビジョニング**」をクリックします。
1. **Edge Delivery サイトをプロビジョニング**&#x200B;ダイアログボックスの「**プロジェクト名**」テキストフィールドに、サイトの名前を入力し、「**プロビジョニング**」をクリックします。
画面の上部中央付近にトーストが表示され、Edge Delivery サイトのプロビジョニングが開始されたことが通知されます。
プロビジョニングが完了し、サイトを検証すると、Edge Delivery ページの **Edge Delivery サイト**&#x200B;領域にサイト名が表示されます。

### 新しく作成されたEdge Delivery サイトを探索します


1. サイト名の右側にある Git リポジトリリンクをクリックします。

公開。

サイト名をクリックし、

変更を加えてから公開する

プレビューでページを表示し、URL を変更して、ライブバージョンを表示します。

共同作業者を追加します。


## ワンクリックでEdge Delivery サイトをプレビュー

## ワンクリックでEdge Delivery サイトを公開





## ワンクリックEdge Deliveryサイトに共同作業者を追加


































これらの機能強化は、自動化の改善、設定プロセスの簡素化、Edge Delivery Services ユーザーの共同作業の強化を目的としています。<!-- CMGR-59362 -->

![ ワンクリックでEdge Delivery サイトを作成する ](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Edge Delivery サイトをプロビジョニングダイアログボックス](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)