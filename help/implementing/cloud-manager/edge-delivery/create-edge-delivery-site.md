---
title: Cloud ManagerでEdge Delivery サイトを作成します
description: ボタンをクリックするだけでCloud ManagerでEdge Delivery サイトをすばやく作成する方法を説明します。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1e4e07d2690bcbd44ffe994a571ffc0a8ae7eb50
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 24%

---


# Cloud ManagerでのEdge Delivery サイトの作成について {#about-one-click-edge-delivery-site}

Edge Delivery サイトの作成機能は、Cloud Manager内でEdge Delivery サイトを自動的にオンボーディングおよびデプロイするのに役立つように設計されています。 ボタン 1 回をクリックするだけで、プロセスが大幅に簡素化されます。この 1 回のクリックで、必要なインフラストラクチャがプロビジョニングされ、GitHub と統合してバージョン管理を行い、Google Drive でドキュメントとアセットのストレージが設定されます。

この自動処理により、最初のサイトを設定するのに必要な手作業の労力が軽減されます。エッジでのコンテンツ管理に関して、シームレスなワークフローとスケーラビリティが確保され、チームのパフォーマンスが向上します。

## 主な概念 {#key-concepts}

Cloud ManagerでワンクリックでEdge Delivery サイトを作成する際の主要な概念。

| 主な概念 | 説明 |
| --- | --- |
| 自動処理されたエッジのデプロイメント | <ul><li>ユーザーは、Edge Delivery サイトをすぐに作成および設定できます。</li><li>Cloud Managerと CI/CD ワークフローの統合を使用することで、手動によるオンボーディングプロセスの必要性を減らすか、不要にします。</li><li>Cloud Managerとの統合により、シームレスな CI/CD ワークフローが実現します。</li></ul> |
| Cloud Manager との統合 | <ul><li>Cloud Manager のユーザーインターフェイスを使用して、ワンクリック Edge Delivery プロセスをトリガーします。</li><li>リポジトリの作成とデプロイメントを自動化するためのアクセスを提供します。</li></ul> |
| GitHub ベースのバージョン管理 | <ul><li>事前定義済みのボイラープレートテンプレートを使用して、組織内に GitHub リポジトリを作成し、デプロイメントを標準化します。</li><li>コンテンツ更新に AEM ボットとリンクします。</li></ul> |
| ドキュメントとアセットのストレージ統合 | <ul><li>ストレージ用の Google Drive フォルダーを生成します。<li>AEM コード同期アプリケーションをリポジトリにインストールし、シームレスな同期とデプロイメントを確保します。</li></li><li>共同作業者は、ドキュメントを簡単に管理できます。</li></ul> |
| セキュリティとスケーラビリティ | <ul><li>大規模法人向けのセキュリティ標準へのコンプライアンスを確保します。</li><li>は、異なるEdge Delivery テナント配下にある複数のCloud Manager サイトをサポートします。</li></ul> |

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

## ワンクリックでCloud ManagerにEdge Delivery サイトを作成 {#one-click-edge-delivery-site}

ワンクリックで Adobe Edge 配信サイトを作成するには、利用可能なEdge Delivery Services ライセンスが必要です。 このライセンスはAdobe Experience Manager（AEM）の一部であり、Cloud Manager内でEdge Delivery Servicesを作成するために必要です。

権限に関しては、ビジネス所有者の役割のメンバーであるか、Cloud Manager でプログラムを追加または編集する適切な権限が付与されている必要があります。このアクセスレベルでは、Edge Delivery Services のプログラムへの統合を管理できます。

詳しくは、[Cloud Manager の Edge Delivery Services の概要](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)も参照してください。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Cloud ManagerでワンクリックでEdge Delivery サイトを作成するには：**

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のメニューの **プログラム** 見出しの下の **概要** をクリックします。
1. **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。
1. Edge Delivery ページの [**Edge Deliveryのタスク リスト**] ダイアログ ボックスの [**Edge Delivery サイトの追加** グループ ボックスで、[**今すぐサイトを作成**] をクリックします。
1. **Edge Delivery サイトを作成** ダイアログボックスの **プロジェクト名** テキストフィールドにサイトの名前を入力し、「**サイトを今すぐ作成**」をクリックします。

   画面の上部中央の近くにトーストが表示され、Edge Delivery サイトのプロビジョニングが開始されたことが示されます。

Cloud Managerによるサイトの準備と検証が完了すると、以前に入力した **サイト名** がEdge Delivery ページの [**Edge Deliveryのサイト**] リスト ボックスに表示されます。 また、リポジトリー URL の左側には、緑色のチェックマークが表示されます。


### ワンクリックで作成されたEdge Delivery サイトを参照 {#explore-one-click-ed-site}

1. [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切なプログラムを選択します。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のメニューの **プログラム** 見出しの下の **概要** をクリックします。
1. **プログラムの概要** ページで、「**Edge Delivery**」タブをクリックします。
1. Edge Deliveryページで、次のいずれかの操作を行います。

   | 調査の対象 | ステップ |
   | --- | --- |
   | サイトの GitHub リポジトリ | <ul><li>**Edge Delivery サイト** リストボックスの **リポジトリ** 列見出しの下で、作成したサイトの URL をクリックします。<br> 場合によっては、ユーザー名またはメールアドレスとパスワードを使用して GitHub にログインする必要があります。</li> |
   | サイトの公開 | <ul><li> **Edge Delivery サイト** リストボックスで、サイト名の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューの ![ 公開チェックアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg)**サイトを公開** をクリックします。<br> サイトの公開が正常に開始されたことを知らせるトーストメッセージが表示されます。</li></ul> |
   | 公開済みサイトのプレビュー | <ul><li>[**Edge Deliveryのサイト**] ボックスの [**サイト名** 列見出しの下で、作成して発行したサイトの URL をクリックします。<br> ブラウザーの URL アドレスバーに、サイトの URL が `.page` で終わり、サイトのプレビューが表示されていることを示していることに注意してください。</li><li>サイトをライブで表示するには、URL アドレスバーで `.page` を `.live` に手動で変更します。</li></ul> |
   | Google Drive 上のコンテンツリポジトリへのアクセス権をユーザーに付与します | <ul><li> **Edge Delivery サイト** リストボックスで、サイト名の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![ ユーザー追加アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg)**コンテンツリポジトリへのアクセス権を取得** をクリックします。</li><li>**サイトに共同作業者を追加** ダイアログボックスで、投稿者のメールアドレスを入力し、![ チェックマークアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックします。</li><li>必要に応じて、コントリビューターメールの追加を続けます。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li><li>コンテンツ共同作業者とリンクを共有するには、「**Collaborationが正常に追加されました**」ダイアログボックスで **OK** をクリックします。</li><li>Collaborationが正常に追加されましたダイアログボックスで、![ コピーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックしてリンクをコピーし、共同作業者と共有します。<br> リンクを共有する前に、共同作業者が IMS アカウントに関連付けられたメールアドレスでログインしていることを確認します。 IMS メールアカウントを使用できない場合は、共同作業者として追加されたメールアドレスを使用する必要があります。 これにより、共同作業者がリンクにアクセスし、Google Drive 上で編集または更新するコンテンツを確認できるようになります。</li><li>編集が完了したら、前述の説明に従って、Cloud Managerで「**サイトを公開**」をクリックします。<br> または、上記のように変更をプレビューします。</li></ul> |
   | GitHub のベースリポジトリへのアクセス権をユーザーに付与します | <ul><li> **Edge Delivery サイト** リストボックスで、サイト名の右端にある ![ その他アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![ コードアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)**ベースリポジトリへのアクセスを取得** をクリックします。</li><li>**サイトのベースリポジトリにアクセス** ダイアログボックスで、共同作業者の GitHub ユーザー名を入力し、![ チェックマークアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックします。</li><li>必要に応じて、GitHub ユーザー名の追加を続行します。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li>ユーザーは、リポジトリを表示するために独自の GitHub ユーザー名へのアクセス権を付与する必要があります。 |


