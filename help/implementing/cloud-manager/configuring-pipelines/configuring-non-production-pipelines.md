---
title: 実稼動以外のパイプラインの設定
description: このページでは、Cloud Manager での非実稼動パイプラインの設定について説明します
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 33%

---


# 実稼動以外のパイプラインの設定 {#configure-non-production-pipeline}

ステージングおよび実稼動環境にデプロイするメインパイプラインに加えて、顧客は、実稼動以外のパイプラインと呼ばれる追加のパイプラインを設定できます。

非実稼動パイプラインには 2 つのタイプがあります。

1. コード品質：Git ブランチのコードに対して、コード品質スキャンを実行します。 このパイプラインは、ビルドおよびコード品質ステップを実行します。
1. 導入：このパイプラインは、ビルドおよびコード品質手順の実行に加えて、選択した非実稼動環境にAEMas a Cloud Service環境にコードをデプロイします。

## 実稼動以外の新しいパイプラインの追加 {#adding-non-production-pipeline}

ホーム画面には、このパイプラインが新しいカードに一覧表示されます。

1. 次にアクセス： **パイプライン** カードを Cloud Manager のホーム画面から削除します。 クリック **+追加** を選択し、 **実稼動以外のパイプラインを追加**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **実稼動以外のパイプラインを追加**  ダイアログボックスが表示されます。 作成するパイプラインのタイプを選択します。 **コード品質パイプライン** または **デプロイメントパイプライン**.

   >[!NOTE]
   >デプロイメントパイプラインの場合は、デプロイメント環境を選択する必要があります。

   また、 **デプロイメントトリガー** および **重要な指標の失敗の動作** から **デプロイメントオプション**. クリック **続行**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   次のデプロイメントトリガーを定義して、パイプラインを開始できます。

   * **手動** - UI を使用して、パイプラインを手動で開始します。
   * **Git の変更時** - 設定された Git ブランチにコミットが追加されるたびに CI/CD パイプラインを開始します。このオプションを選択しても、常にパイプラインを手動で開始できます。

      パイプラインのセットアップまたは編集中に、デプロイメントマネージャーは、品質ゲートのいずれかで重要なエラーが検出された場合のパイプラインの動作を定義できます。

      これは、より自動化されたプロセスを求めるお客様に役に立ちます。使用できるオプションは以下のとおりです。
   重要な失敗指標の動作を定義して、パイプラインを開始できます。

   * **毎回確認する** - デフォルトの設定。重要なエラーが検出されたときに手動で介入する必要があります。
   * **すぐに失敗**  — 重要なエラーが発生すると、常にパイプラインはキャンセルされます。 このオプションでは、基本的に、各エラーをユーザーが手動で拒否する状況をエミュレートします。
   * **すぐに続行**  — 重要なエラーが発生した場合は常に、パイプラインは自動的に続行されます。 このオプションでは、基本的に、各エラーをユーザーが手動で承認する状況をエミュレートします。


1. 選択 **[フルスタックコード](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** または **[フロントエンドコード](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   選択した場合 **フロントエンドコード**&#x200B;を選択する場合は、 **リポジトリ**, **Git ブランチ** および **コードの場所**（下の図を参照）。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   選択した場合 **フルスタックコード**&#x200B;を選択する場合は、 **リポジトリ** および **Git ブランチ**（図を参照）
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >選択した環境にフルスタックコードパイプラインが既に存在する場合、この選択は無効になります。

   >[!NOTE]
   >フロントエンドパイプラインの設定を開始する前に、 [AEMクイックサイト作成ジャーニー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) 使いやすいAEM Quick Site Creation ツールを使用してエンドツーエンドのワークフローを実現する このドキュメントサイトは、AEMサイトのフロントエンド開発を合理化し、AEMのバックエンドに関する知識を持たずに、すばやくサイトをカスタマイズするのに役立ちます。

1. 新しく作成した非実稼動パイプラインが **パイプライン** カード。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   パイプラインは、次に示すように、4 つのアクションと共にホーム画面のカードに表示されます。

   * **追加**  — 新しいパイプラインを追加できます。
   * **すべて表示** ：ユーザーがすべてのパイプラインを表示できます。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。