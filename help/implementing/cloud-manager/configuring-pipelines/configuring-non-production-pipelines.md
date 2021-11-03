---
title: 実稼動以外のパイプラインの設定
description: このページでは、Cloud Manager での非実稼動パイプラインの設定について説明します
index: false
source-git-commit: 7d45179093366dda2d035b5a8eed219e4846f777
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 21%

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

1. 選択 **フルスタックコード** または **フロントエンドコード**. 次を選択できます。 **リポジトリ** そして **Git ブランチ**. 「**保存**」をクリックします。

   >[!NOTE]
   >フロントエンドパイプラインの設定を開始する前に、使いやすいAEMクイックサイト作成ツールを使用して、エンドツーエンドのワークフローに対するAEMクイックサイト作成ジャーニーを参照してください。 このドキュメントサイトは、AEMサイトのフロントエンド開発を合理化し、AEMのバックエンドに関する知識を持たずに、すばやくサイトをカスタマイズするのに役立ちます。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 新しく作成した非実稼動パイプラインが **パイプライン** カード。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   パイプラインは、次に示すように、3 つのアクションと共にホーム画面のカードに表示されます。

   * **追加**  — 新しいパイプラインを追加できます。
   * **リポジトリー情報へアクセス** - Cloud Manager Git リポジトリーへのアクセスに必要な情報をユーザーが取得できるようにします.
   * **詳細情報** - CI／CD パイプラインのドキュメントリソースの概要に移動します。