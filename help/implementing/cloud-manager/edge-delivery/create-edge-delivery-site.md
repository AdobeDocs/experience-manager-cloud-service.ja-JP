---
title: 最初の Edge Delivery サイトをワンクリックで作成
description: ボタンをクリックするだけで Cloud Manager で Edge Delivery サイトをすばやく作成する方法について説明します。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '1373'
ht-degree: 62%

---

# 最初の Edge Delivery サイトをワンクリックで作成{#about-one-click-edge-delivery-site}

最初の Edge Delivery サイトをワンクリックで作成する機能は、Cloud Manager 内で Edge Delivery サイトのオンボーディングとデプロイメントを自動処理できるように設計されています。ボタン 1 回をクリックするだけで、プロセスが大幅に簡素化されます。この 1 回のクリックで、必要なインフラストラクチャがプロビジョニングされ、GitHub と統合してバージョン管理を行い、Google Drive でドキュメントとアセットのストレージが設定されます。

この自動処理により、最初のサイトを設定するのに必要な手作業の労力が軽減されます。エッジでのコンテンツ管理に関して、シームレスなワークフローとスケーラビリティが確保され、チームのパフォーマンスが向上します。

<!--
 Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on)
-->



<!--
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

1. [experience.adobe.com](https://experience.adobe.com)でCloud Managerにログインします。
   1. **クイックアクセス** セクションで、**Experience Manager**&#x200B;をクリックします。
   1. 左側のサイドパネルで、「**Cloud Manager**」をクリックします。
   1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、プログラムをクリックします。
1. ページの左上隅にある ![メニューを表示アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) をクリックして、左サイドメニューを表示します。
1. 左側のサイドメニューの&#x200B;**プログラム**&#x200B;見出しの下にある「**概要**」をクリックします。
1. **プログラムの概要**&#x200B;ページで、「**Edge Delivery**」タブをクリックします。
1. Edge Delivery ページの&#x200B;**Edge Delivery To Do リスト** ダイアログボックスの&#x200B;**Edge Delivery サイトを追加** グループボックスで、**今すぐサイトを作成**&#x200B;をクリックします。
1. **Edge Delivery サイトを作成** ダイアログボックスの「**プロジェクト名**」テキストフィールドに、サイトの名前を入力します。
1. **オーサリングオプション**&#x200B;で、次のいずれかを選択します。
   * **ドキュメントオーサリング** — Google ドライブまたはSharePointでコンテンツを作成します。 このオプションはデフォルトで、AEM環境は必要ありません。
   * **AEM オーサリング （Beta）** — ユニバーサルエディターを使用してAEMでコンテンツを作成します。 このオプションを選択した場合、**テンプレートを選択**&#x200B;で、Edge Delivery サイトの初期テンプレートを選択します。

   ![AEM オーサリングを選択した状態でEdge Delivery サイトを作成ダイアログ ボックス。](/help/implementing/cloud-manager/edge-delivery/assets/eds-create-aem-authoring.png)

1. 「**オーサリング環境**」ドロップダウンリストで、オーサリングに使用するAEM環境を選択します。 この環境は既にプログラムに存在している必要があります。 オーサー層のみが必要です。Edge Deliveryで配信を処理する場合、パブリッシュ層は必要ありません。 [柔軟なパブリッシュ層（Beta） &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)を参照してください。

1. 「**今すぐサイトを作成**」をクリックします。

   画面の上部中央付近にトーストが表示され、Edge Delivery サイトのプロビジョニングが開始されたことが通知されます。

Cloud Manager によるサイトのプロビジョニングと検証が完了すると、**サイト名**（以前に入力したプロジェクト名）が Edge Delivery ページの **Edge Delivery サイト**&#x200B;リストボックスに表示されます。また、「検証済み」ステータス列の左側には、緑色のドットが表示されます。

[AEM オーサーからEdge Deliveryへのコンテンツの公開](#publish-from-aem-author)も参照してください。

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
   | ユーザーに Google Drive のコンテンツリポジトリへのアクセス権を付与 | <ul><li> **Edge Delivery サイト**&#x200B;リストボックスで、サイト名の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![ユーザー追加アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg)「**コンテンツリポジトリへのアクセス権を取得**」をクリックします。</li><li>**`Add collaborators to your site`** ダイアログボックスで、コントリビューターの電子メールアドレスを入力し、![&#x200B; チェックマークアイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)をクリックします。</li><li>必要に応じて、引き続きコントリビューターのメールを追加します。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li><li>コンテンツの共同作業者とリンクを共有するには、**共同作業が正常に追加されました**&#x200B;ダイアログボックスで「**OK**」をクリックします。</li><li>共同作業が正常に追加されましたダイアログボックスで、![コピーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) をクリックしてリンクをコピーし、共同作業者と共有します。<br>リンクを共有する前に、共同作業者が IMS アカウントに関連付けられたメールアドレスを使用してログインしていることを確認します。IMS メールアカウントが使用できない場合は、共同作業者として追加されたメールアドレスを使用する必要があります。これにより、共同作業者はリンクにアクセスして、Google Drive で編集または更新するコンテンツを表示できます。</li><li>編集が完了したら、上記の説明に従って、Cloud Manager で「**サイトを公開**」をクリックします。<br>または、上記の説明に従って、変更をプレビューします。</li></ul> |
   | ユーザーに GitHub のベースリポジトリへのアクセス権を付与 | <ul><li> **Edge Delivery サイト**&#x200B;リストボックスで、サイト名の右端にある ![その他アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) をクリックして、ドロップダウンメニューを開きます。</li><li>ドロップダウンメニューで ![コードアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg)「**ベースリポジトリへのアクセス権を取得**」をクリックします。</li><li>**サイトのベースリポジトリへのアクセス**&#x200B;ダイアログボックスで、共同作業者の GitHub ユーザー名を入力し、![チェックマークアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) をクリックします。</li><li>必要に応じて、引き続き GitHub ユーザー名を追加します。</li><li>完了したら、「**共同作業者を追加**」をクリックします。</li>ユーザーは、リポジトリを表示するのに独自の GitHub ユーザー名へのアクセス権を付与する必要があります。 |

## AEM オーサーからEdge Delivery（Beta）へのコンテンツの公開 {#publish-from-aem-author}

>[!NOTE]
>
>ここで説明する公開機能はBetaにあります。 Betaに参加するには、[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)にAdobeの組織IDとプログラム IDをメールで送信してください。

この機能は、AEM オーサリングオプションで作成されたEdge Delivery サイトでのみ使用できます。

Edge Delivery サイトを作成し、Cloud Managerで&#x200B;**検証済み**&#x200B;したら、AEM ユニバーサルエディターを使用してコンテンツをオーサリングおよび公開できます。

**Cloud Managerからユニバーサルエディターにアクセスするには：**

1. 「Edge Delivery」タブの「Edge Delivery サイト」リストで、サイトを見つけます。

   ![AEM オーサーからEdge Deliveryへのコンテンツの公開](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. サイトの行にある&#x200B;**コンテンツSource** リンクをクリックします。 このリンクをクリックすると、AEM ユニバーサルエディターページが開き、サイトのコンテンツを作成および編集できます。

**コンテンツを公開するには：**

* **Cloud Managerから** -

   1. **概要** ページの&#x200B;**配信を公開** タブの&#x200B;**環境** カードで、強調表示された![情報または情報アイコン &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg)をクリックします。

   1. 情報ポップアップで「**クリックしてアクティブ化**」を選択し、Cloud Manager ユーザーインターフェイスでパブリッシュ層のプロビジョニングを有効にします。

      ![&#x200B; クリックしてパブリッシュ層プロビジョニングをアクティブ化](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

   1. パブリッシュ層をアクティブ化ダイアログボックスで、**アクティブ化**&#x200B;をクリックします。

      ![&#x200B; パブリッシュ層をアクティブ化ダイアログボックス &#x200B;](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

      アクティブ化すると、パブリッシュ層が自動的にプロビジョニングされます。 または、作成者がAEM ユーザーインターフェイスからコンテンツを直接公開しようとすると、パブリッシュ層を自動的にプロビジョニングできます。

      パブリッシュ層がアクティブ化され、正常にプロビジョニングされると、**クリックしてアクティブ化** リンクがグレー表示または使用できなくなります。

* **AEM オーサー**&#x200B;から – AEM オーサリングインターフェイスで、**クイック公開**&#x200B;をクリックして、コンテンツをEdge Delivery サイトに直接公開します。 Edge Deliveryで配信を処理する場合、この操作に公開層は必要ありません。

公開後、サイトの`.page` URLでコンテンツをプレビューするか、`.live` URLでライブ表示します。—>

