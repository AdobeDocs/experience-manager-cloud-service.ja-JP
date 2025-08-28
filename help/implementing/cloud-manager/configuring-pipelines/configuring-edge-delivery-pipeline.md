---
title: Edge Delivery パイプラインの追加
description: Edge Delivery パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Private Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: e1922bd862a2106a274694ea1d3a98da9c186049
workflow-type: ht
source-wordcount: '489'
ht-degree: 100%

---

# Edge Delivery パイプラインの追加 {#configure-production-pipeline}

Edge Delivery パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。本番パイプラインは、最初にコードをステージング環境にデプロイします。承認時に、同じコードが本番環境にデプロイされます。

本番パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>以下の条件が満たされるまで、Edge Delivery パイプラインは設定できません。
>
>* 1 つの Edge Delivery Services サイトと 1 つのマッピングされたドメインを含むプログラムが作成されます。そうでない場合、「**Edge Delivery パイプラインを追加**」オプションはユーザーインターフェイスで無効として表示され、ツールチップで不足している要件が説明されます。
>* Git リポジトリには 1 つ以上の分岐があります。
>* 本番環境とステージング環境が作成されます。

<!-- CMGR‑69680 -->


コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を行う必要があります。

>[!NOTE]
>
>初期設定後に[パイプライン設定を編集](managing-pipelines.md)できます。

**Edge Delivery パイプラインを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、必要な組織を選択します。

1. **マイプログラム**&#x200B;ページで、必要なプログラムを選択します。

   ![Cloud Manager のマイプログラムページ](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. 次のいずれかの操作を行います。

   * **パイプラインカードから Edge Delivery パイプラインを追加**

      1. 左側のパネルの&#x200B;**プログラム**&#x200B;の下にある「**![概要アイコン](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [概要](/help/implementing/cloud-manager/navigation.md#my-programs)**」をクリックします。
      1. **プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードの下にある「**![プラス記号](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) 追加**」をクリックし、「**Edge Delivery パイプラインを追加**」を選択します。

         ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

   * **パイプラインページから Edge Delivery パイプラインを追加**

      1. 左側のパネルの&#x200B;**プログラム**&#x200B;の下にある「**![ワークフローアイコンまたはパイプラインアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) パイプライン**」をクリックします。
      1. パイプラインページの右上隅付近にある&#x200B;**パイプラインを追加**／**Edge Delivery パイプラインを追加**&#x200B;をクリックします。

         ![「パイプラインを追加」ボタンを含むパイプラインページ](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

1. **Edge Delivery パイプラインを追加**&#x200B;ダイアログボックスの「**パイプライン名**」テキストフィールドに、わかりやすいパイプラインラベルを入力します。

   ![Edge Delivery パイプラインを追加ダイアログボックス](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. 必要なパイプラインの「**デプロイメントトリガー**」オプションを選択します。

   * **手動** - デプロイメントを開始します。
   * **Git の変更時** - Git コミットによりデプロイメントが自動的に開始されます。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. 「**続行**」をクリックします。

1. **ソースコード**&#x200B;で、次のオプションを設定します。

   * **デプロイメント環境** - ターゲット環境フィールドを表示します。読み取り専用のままです。

   * **リポジトリ** - ドロップダウンリストを使用して、Edge Delivery 設定を保存する正確な Git リポジトリをパイプラインに指定します。

     また、Cloud Manager でリポジトリを追加および管理する方法について詳しくは、[リポジトリの追加と管理](/help/implementing/cloud-manager/managing-code/managing-repositories.md)も参照してください。

   * **Git 分岐** - ドロップダウンリストを使用して、選択したリポジトリ内の特定の分岐を選択します。必要に応じて、![リサイクルアイコンまたは更新アイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) をクリックして、最近のプッシュ後に Git 分岐ドロップダウンリストをリロードします。
   * **コードの場所** - パイプライン対応コードが開始されるリポジトリ内のフォルダーパスを定義します（`/` はリポジトリのルートと同じです）。

   ![設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. 「**保存**」をクリックします。

**プログラムの概要**&#x200B;ページの&#x200B;**パイプライン**&#x200B;カードまたは&#x200B;**パイプライン**&#x200B;ページから[パイプラインを管理](managing-pipelines.md)できるようになりました。
