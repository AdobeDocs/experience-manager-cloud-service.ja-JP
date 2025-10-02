---
title: Edge Delivery パイプラインの追加
description: Edge Delivery パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: 9ad50747b46b75c33cb5b034e8b8e41d5079e967
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 64%

---

# Edge Delivery パイプラインの追加 {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Edge Delivery パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。Edge Delivery パイプラインを使用すると、ログ転送やAdobeの管理による CDN などの機能を設定できます。

サポートされる設定のリストについては、[&#x200B; 設定パイプラインの使用 – サポートされる設定 &#x200B;](/help/operations/config-pipeline.md#configurations) を参照してください。

本番パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!IMPORTANT]
>
>以下の条件が満たされるまで、Edge Delivery パイプラインは設定できません。
>
>* 1 つの Edge Delivery Services サイトと 1 つのマッピングされたドメインを含むプログラムが作成されます。それ以外の場合は、「**Edge Delivery パイプラインを追加** というオプションがユーザーインターフェイスで無効になっているように見え、不足している要件に関するツールチップが表示されます。 [Cloud ManagerでのEdge Delivery サイトの作成 &#x200B;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md) を参照してください。
>* Git リポジトリーには少なくとも 1 つのブランチがあります。 [Cloud Managerでのリポジトリの管理 &#x200B;](/help/implementing/cloud-manager/managing-code/managing-repositories.md) を参照してください。
>* 実稼動環境とステージング環境が作成されます。 [CI/CD パイプラインの概要 &#x200B;](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) を参照してください。

<!-- CMGR‑69680 -->

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を行う必要があります。

>[!NOTE]
>
>初期設定後に[パイプライン設定を編集](managing-pipelines.md)できます。

**Edge Delivery パイプラインを追加するには：**

1. [experience.adobe.com](https://experience.adobe.com) でCloud Managerにログインします。
1. 「**クイックアクセス**」セクションで、「**Experience Manager**」をクリックします。
1. 左側のパネルで、「**Cloud Manager**」をクリックします。
1. 必要な組織を選択します。
1. **マイプログラム** コンソールで、プログラムをクリックします。

   ![Cloud Manager のマイプログラムページ](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. 次のいずれかの操作を行います。

   * **パイプラインカードから Edge Delivery パイプラインを追加**

      1. 左側のパネルの&#x200B;**プログラム**&#x200B;の下にある「**![概要アイコン](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [概要](/help/implementing/cloud-manager/navigation.md#my-programs)**」をクリックします。
      1. **プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの下にある「**![プラス記号](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) 追加**」をクリックし、「**Edge Delivery パイプラインを追加**」を選択します。

         ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >上のスクリーンショットに示すように、**パイプライン** カードを使用する以外に、**パイプライン** ページからパイプラインを管理することもできます。
         >
         >![パイプライン名、ステータス、リポジトリー、ブランチを表示する「Edge Delivery パイプライン」ウィジェット](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **パイプラインページから Edge Delivery パイプラインを追加**

      1. 左側のパネルの&#x200B;**プログラム**&#x200B;の下にある「**![ワークフローアイコンまたはパイプラインアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) パイプライン**」をクリックします。
      1. パイプラインページの右上隅付近にある&#x200B;**パイプラインを追加**／**Edge Delivery パイプラインを追加**&#x200B;をクリックします。

         ![「パイプラインを追加」ボタンを含むパイプラインページ](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >左上隅付近で「**フィルター** をクリックし、「**配信タイプ**」セクションで「**Edge配信**」チェックボックスをオンにして、リストをEdge Delivery パイプライン（Edge Delivery Servicesを使用するパイプライン）のみにフィルタリングします。<!-- (CMGR-69682) -->
         >
         >![Edge DeliveryとPublish Deliveryの新しい配信タイプを示すフィルターパネル](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

1. **Edge Delivery パイプラインを追加**&#x200B;ダイアログボックスの「**パイプライン名**」テキストフィールドに、わかりやすいパイプラインラベルを入力します。

   ![Edge Delivery パイプラインを追加ダイアログボックス](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. 必要なパイプライン **デプロイメントトリガー** オプションを選択します。

   * **手動** - デプロイメントを開始します。
   * **Git の変更時** - Git コミットによりデプロイメントが自動的に開始されます。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. 「**続行**」をクリックします。

1. **ソースコード**&#x200B;で、次のオプションを設定します。

   * **デプロイメント環境** - ターゲット環境フィールドを表示します。読み取り専用のままです。

   * **リポジトリ** - ドロップダウンリストを使用して、Edge Delivery 設定を保存する正確な Git リポジトリをパイプラインに指定します。

     また、Cloud Manager でリポジトリを追加および管理する方法について詳しくは、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)も参照してください。

   * **Git 分岐** - ドロップダウンリストを使用して、選択したリポジトリ内の特定の分岐を選択します。必要に応じて、![&#x200B; アイコンまたは更新アイコンをリサイクル &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) をクリックして、最近のプッシュ後に Git ブランチのドロップダウンリストをリロードします。
   * **コードの場所** - パイプライン対応コードが開始されるリポジトリ内のフォルダーパスを定義します（`/` はリポジトリのルートと同じです）。

   ![設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. 「**保存**」をクリックします。

[&#x200B; プログラムの概要 &#x200B;](managing-pipelines.md) ページの **パイプライン** カードから、または **パイプライン** ページから **パイプライン** 管理できるようになりました。


![パイプライン名、ステータス、リポジトリー、ブランチを表示する「Edge Delivery パイプライン」ウィジェット](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



