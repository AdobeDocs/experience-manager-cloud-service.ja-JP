---
title: ワンクリックでCloud ManagerにEdge Delivery サイトを作成
description: ボタンをクリックするだけで Cloud Manager で Edge Delivery サイトをすばやく作成する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: 767b1f89f42340cc9307a43ff9e97e9a074e592e
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 97%

---

# ワンクリックでCloud ManagerのEdge Delivery サイトを作成する方法について{#about-one-click-edge-delivery-site}

Edge Delivery サイトの作成機能は、Cloud Manager 内での Edge Delivery サイトのオンボーディングとデプロイメントを自動処理できるように設計されています。ボタン 1 回をクリックするだけで、プロセスが大幅に簡素化されます。この 1 回のクリックで、必要なインフラストラクチャがプロビジョニングされ、GitHub と統合してバージョン管理を行い、Google Drive でドキュメントとアセットのストレージが設定されます。

この自動処理により、最初のサイトを設定するのに必要な手作業の労力が軽減されます。エッジでのコンテンツ管理に関して、シームレスなワークフローとスケーラビリティが確保され、チームのパフォーマンスが向上します。

<!-- >
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->

## ワンクリックでの Cloud Manager への Edge Delivery サイトの作成 {#one-click-edge-delivery-site}

Adobe Edge Delivery サイトをワンクリックで作成するには、組織に使用可能な Edge Delivery Services ライセンスが必要です。このライセンスは、Adobe Experience Manager（AEM）の一部であり、Cloud Manager 内で Edge Delivery Services を作成するのに必要です。

権限に関しては、ビジネス所有者の役割のメンバーであるか、Cloud Manager でプログラムを追加または編集する適切な権限が付与されている必要があります。このアクセスレベルでは、Edge Delivery Services のプログラムへの統合を管理できます。

詳しくは、[Cloud Manager の Edge Delivery Services の概要](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)も参照してください。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**ワンクリックで Cloud Manager に Edge Delivery サイトを作成するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のサイドメニューの&#x200B;**プログラム**&#x200B;見出しの下にある「**概要**」をクリックします。
1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。
1. Edge Delivery ページの **Edge Delivery の TODO リスト**&#x200B;ダイアログボックスの「**Edge Delivery サイトを追加**」グループボックスで、「**今すぐサイトを作成**」をクリックします。
1. **Edge Delivery サイトを作成**&#x200B;ダイアログボックスの「**プロジェクト名**」テキストフィールドに、サイトの名前を入力し、「**今すぐサイトを作成**」をクリックします。

   画面の上部中央付近にトーストが表示され、Edge Delivery サイトのプロビジョニングが開始されたことが通知されます。

Cloud Manager によるサイトのプロビジョニングと検証が完了すると、**サイト名**（以前に入力したプロジェクト名）が Edge Delivery ページの **Edge Delivery サイト**&#x200B;リストボックスに表示されます。また、リポジトリ URL の左側に緑色のチェックマークが表示されます。


### ワンクリックで作成された Edge Delivery サイトの探索 {#explore-one-click-ed-site}

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のサイドメニューの&#x200B;**プログラム**&#x200B;見出しの下にある「**概要**」をクリックします。
1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。
1. Edge Delivery ページで、次のいずれかの操作を行います。

   | 探索内容 | ステップ |
   | --- | --- |
   | サイトの GitHub リポジトリ | <ul><li>**Edge Delivery サイト**&#x200B;リストボックスの&#x200B;**リポジトリ**&#x200B;列見出しの下で、作成したサイトの URL をクリックします。<br>ユーザー名またはメールアドレスとパスワードを使用して GitHub にログインする必要がある場合があります。</li> |
   | サイトを公開 | <ul><li> **Edge Delivery サイト**&#x200B;リストボックスで、サイト名の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューの ![公開チェックアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg)「**サイトを公開**」をクリックします。<br>サイトの公開が正常に開始されたことを知らせるトーストメッセージが表示されます。</li></ul> |
   | 公開済みサイトをプレビュー | <ul><li>**Edge Delivery サイト**&#x200B;リストボックスの&#x200B;**サイト名**&#x200B;列見出しの下で、作成および公開したサイトの URL をクリックします。<br>ブラウザーの URL アドレスバーで、サイトの URL が `.page` で終わっていることに注意してください。これは、サイトのプレビューが表示されていることを示します。</li><li>サイトをライブで表示するには、URL アドレスバーで `.page` を `.live` に手動で変更します。</li></ul> |
   | ユーザーに Google Drive のコンテンツリポジトリへのアクセス権を付与 | <ul><li> **Edge Delivery サイト**&#x200B;リストボックスで、サイト名の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![ユーザー追加アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg)「**コンテンツリポジトリへのアクセス権を取得**」をクリックします。</li><li>**サイトに共同作業者を追加**&#x200B;ダイアログボックスで、コントリビューターのメールアドレスを入力し、![チェックマークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックします。</li><li>必要に応じて、引き続きコントリビューターのメールを追加します。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li><li>コンテンツの共同作業者とリンクを共有するには、**共同作業が正常に追加されました**&#x200B;ダイアログボックスで「**OK**」をクリックします。</li><li>共同作業が正常に追加されましたダイアログボックスで、![コピーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックしてリンクをコピーし、共同作業者と共有します。<br>リンクを共有する前に、共同作業者が IMS アカウントに関連付けられたメールアドレスを使用してログインしていることを確認します。IMS メールアカウントが使用できない場合は、共同作業者として追加されたメールアドレスを使用する必要があります。これにより、共同作業者はリンクにアクセスして、Google Drive で編集または更新するコンテンツを表示できます。</li><li>編集が完了したら、上記の説明に従って、Cloud Manager で「**サイトを公開**」をクリックします。<br>または、上記の説明に従って、変更をプレビューします。</li></ul> |
   | ユーザーに GitHub のベースリポジトリへのアクセス権を付与 | <ul><li> **Edge Delivery サイト**&#x200B;リストボックスで、サイト名の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![コードアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)「**ベースリポジトリへのアクセス権を取得**」をクリックします。</li><li>**サイトのベースリポジトリへのアクセス**&#x200B;ダイアログボックスで、共同作業者の GitHub ユーザー名を入力し、![チェックマークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックします。</li><li>必要に応じて、引き続き GitHub ユーザー名を追加します。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li>ユーザーは、リポジトリを表示するのに独自の GitHub ユーザー名へのアクセス権を付与する必要があります。 |
