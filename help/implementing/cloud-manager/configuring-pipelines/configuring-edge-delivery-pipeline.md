---
title: Edge Delivery パイプラインの追加
description: Edge Delivery パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Private Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: false
hidefromtoc: false
source-git-commit: 96a619c6ab8f71034914b72a57bdb1e7f363fbc6
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 26%

---


# Edge Delivery パイプラインの追加 {#configure-production-pipeline}

Edge Delivery パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。本番パイプラインは、最初にコードをステージング環境にデプロイします。承認時に、同じコードが本番環境にデプロイされます。

本番パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>Edge Delivery パイプラインは、次の状況が発生するまで設定できません。
>
>* 1 つのEdge Delivery Services サイトと 1 つのマッピングされたドメインを含むプログラムが作成されます。 それ以外の場合は、「Edge Delivery パイプラインを追加 **オプションがユーザーインターフェイスで無効に表示され** ツールチップに不足している要件が説明されます。<!-- CMGR‑69680 -->
>* Git リポジトリには 1 つ以上の分岐があります。
>* 本番環境とステージング環境が作成されます。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を行う必要があります。

>[!NOTE]
>
>初期設定後に [ パイプライン設定を編集 ](managing-pipelines.md) できます。

**Edge Delivery パイプラインを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) でCloud Managerにログインし、必要な組織を選択します。

1. **マイプログラム** ページで、必要なプログラムを選択します。

   ![Cloud Managerのマイプログラムページ ](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. 次のいずれかの操作を行います。

   * **パイプライン カードからのEdge Delivery パイプラインの追加**

      1. 左側のパネルの **プログラム** で、「概要アイコン **![](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [ 概要](/help/implementing/cloud-manager/navigation.md#my-programs)** をクリックします。
      1. **プログラムの概要** ページの **パイプライン** カードの下の「**![プラス記号 ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) 追加**」をクリックし、「**Edge Delivery パイプラインを追加**」を選択します。

         ![ プログラムの概要ページのパイプライン カード ](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

   * **パイプライン ページからのEdge Delivery パイプラインの追加**

      1. 左側のパネルの **プログラム** で、**![ワークフローアイコンまたはパイプラインアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) パイプライン** をクリックします。
      1. パイプライン ページで、右上隅付近の **パイプラインを追加**/**Edge Delivery パイプラインを追加** をクリックします。

         ![ 「パイプラインを追加」ボタンを含んだパイプラインページ ](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

1. **Edge Delivery パイプラインを追加** ダイアログボックスで、「**パイプライン名**」テキストフィールドにわかりやすいパイプラインラベルを入力します。

   ![Edge Delivery パイプラインを追加ダイアログボックス ](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. 必要なパイプライン **デプロイメントトリガー** オプションを選択します。

   * **手動** - デプロイメントを開始します。
   * **Git の変更時** - Git コミットによってデプロイメントが自動的に開始されます。 このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

1. 「**続行**」をクリックします。

1. 「**Source コード**」で、次のオプションを設定します。

   * **デプロイメント環境** - ターゲット環境フィールドを表示します。読み取り専用のままです。

   * **リポジトリー** - ドロップダウンリストを使用して、Edge Delivery設定を格納する正確な Git リポジトリーをパイプラインで指定します。

     Cloud Managerでリポジトリを追加および管理する方法については、[ リポジトリの追加と管理 ](/help/implementing/cloud-manager/managing-code/managing-repositories.md) も参照してください。

   * **Git ブランチ** - ドロップダウンリストを使用して、選択したリポジトリ内の特定のブランチを選択します。 必要に応じて、![ アイコンまたは更新アイコンをリサイクル ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) をクリックして、最近のプッシュ後に Git ブランチのドロップダウンリストをリロードします
   * **コードの場所** - パイプライン対応コードが開始するリポジトリ内のフォルダーパスを定義します（`/` はリポジトリルートと同じ）。

   ![設定パイプライン](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. 「**保存**」をクリックします。

[ プログラムの概要 ](managing-pipelines.md) ページの **パイプライン** カードまたは **パイプライン** ページから **パイプライン** 管理できるようになりました。
