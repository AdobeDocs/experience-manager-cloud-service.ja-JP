---
title: Edge Delivery パイプラインの追加
description: Edge Delivery パイプラインを追加し、コードをビルドして実稼動環境にデプロイする方法について説明します。
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="プライベートベータ版" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 99%

---



# Edge Delivery パイプラインの追加 {#configure-production-pipeline}

Edge Delivery パイプラインを設定し、コードをビルドして本番環境にデプロイする方法について説明します。本番パイプラインは、最初にコードをステージング環境にデプロイします。承認時に、同じコードが本番環境にデプロイされます。

本番パイプラインを設定するには、ユーザーに&#x200B;**[デプロイメントマネージャー](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;の役割が必要です。

>[!NOTE]
>
>本番パイプラインは、以下の条件が満たされるまで設定できません。
>
>* プログラムが作成されます。
>* Git リポジトリには 1 つ以上の分岐があります。
>* 本番環境とステージング環境が作成されます。

コードのデプロイを開始する前に、[!UICONTROL Cloud Manager] からパイプライン設定を行う必要があります。

>[!NOTE]
>
>初期設定後に、[パイプライン設定を編集](managing-pipelines.md)できます。

## 新しいEdge Delivery パイプラインを追加する {#adding-production-pipeline}

[!UICONTROL Cloud Manager] UI を使用してプログラムをセットアップし、1 つ以上の環境を用意したら、次の手順に従って本番パイプラインを追加する準備が整います。

>[!TIP]
>
>フロントエンドパイプラインを設定する前に、[AEM クイックサイト作成ジャーニー](/help/journey-sites/quick-site/overview.md)を参照して、使いやすい AEM クイックサイト作成ツールのエンドツーエンドのガイドを確認してください。このジャーニーを活用すると、AEM サイトのフロントエンド開発を効率化できるだけでなく、AEM のバックエンドに関する知識がなくても、サイトをすばやくカスタマイズすることができます。

**新しいEdge Delivery パイプラインを追加するには：**

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織を選択します。

1. **[マイプログラム](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;コンソールで、プログラムを選択します。

1. **プログラムの概要**&#x200B;ページから&#x200B;**パイプライン**&#x200B;カードに移動し、「**追加**」をクリックして「**実稼動パイプラインを追加**」を選択します。

   ![プログラムの概要ページのパイプラインカード](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **実稼動パイプラインを追加**&#x200B;ダイアログボックスが表示されます。パイプラインを識別するための「**パイプライン名**」のほか、以下のオプションを指定します。「**続行**」をクリックします。

   **デプロイメントトリガー** - パイプラインを開始するデプロイメントトリガーを定義する際には、次のオプションがあります。

   * **手動** - パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git 分岐にコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを使用すると、必要に応じてパイプラインを手動で開始できます。

   **重要な指標のエラー動作** - パイプラインの設定または編集中に、**デプロイメントマネージャー**&#x200B;には、品質ゲートのいずれかで重要なエラーが発生した場合のパイプラインの動作を定義するオプションがあります。使用できるオプションは以下のとおりです。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出された場合は手動で介入する必要があります。
   * **直ちに失敗** - 重要なエラーが検出されると、パイプラインがキャンセルされます。このプロセスでは、基本的に、ユーザーが各エラーを手動で拒否する状況をエミュレートします。
   * **直ちに続行** - 重要なエラーが検出されても、パイプラインが自動的に続行されます。このプロセスでは、基本的に、ユーザーが各エラーを手動で承認する状況をエミュレートします。

   ![本番パイプライン設定](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 「**ソースコード**」タブでは、パイプラインで処理するコードのタイプを選択します。

   * **[フルスタックコードパイプラインの設定](#full-stack-code)**
   * **[ターゲットデプロイメントパイプラインの設定](#targeted-deployment)**

このタイプのパイプラインについて詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

実稼動パイプラインを作成する手順は、選択したソースコードのタイプによって異なります。上記のリンクをたどって、このドキュメントの次の節に移動し、パイプラインの設定を完了します。

