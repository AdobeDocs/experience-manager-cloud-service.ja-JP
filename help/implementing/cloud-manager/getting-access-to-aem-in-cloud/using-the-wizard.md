---
title: プロジェクト作成ウィザード
description: 実稼働プログラムを作成した後、プロジェクトをすばやく設定するのに役立つプロジェクト作成ウィザードについて説明します。
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 4%

---

# プロジェクト作成ウィザード {#project-creation-wizard}

実稼働用プログラムを作成した後、Cloud Manager には、 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja) 早く始めるために

ウィザードを使用して Cloud Manager でAEMアプリケーションプロジェクトを作成するには、次の手順に従います。

1. ドキュメント内の手順に従って、実稼働用プログラムを作成します [実稼働プログラムの作成](creating-production-programs.md)

1. プログラムの設定が完了したら、 **概要** プログラムの画面と **ブランチとプロジェクトを作成** コールトゥアクションカードを上部に表示します。

   ![ウィザードのコールトゥアクションケア](assets/create-wizard1.png)

1. クリック **作成** ウィザードを起動し、プロジェクトの **タイトル** および **新しいブランチ名** 内 **ブランチとプロジェクトの作成** ウィンドウ

   ![ブランチとプロジェクトの作成](assets/create-wizard2.png)

1. 必要に応じて、ディバイダをクリックして、プロジェクトの追加のパラメータを表示します。 デフォルト値はAEMプロジェクトアーキタイプで提供され、通常は変更する必要はありません。

   ![追加のプロジェクトパラメーター](assets/create-wizard5.png)

1. クリック **作成** をクリックして、プロジェクト作成プロセスを開始します。


A **プロジェクトを作成中** カードが **ブランチとプロジェクトを作成** コールトゥアクションカードを **プログラムの概要** 画面

![プロジェクト作成中](assets/create-wizard3.png)

プログラムの作成が完了したら、 **環境を追加** カードが **プロジェクトを作成中** の一番上にあるカード **プログラムの概要** 画面

![環境を追加](assets/create-wizard4.png)

これで、AEMアーキタイプに基づくAEMプロジェクトが Git リポジトリに追加され、独自のプロジェクトの開発の基礎となります。 次に、プロジェクトコードをデプロイできる環境を作成できます。

ドキュメントを参照してください [環境の管理](/help/implementing/cloud-manager/manage-environments.md) 環境を追加または管理する方法について説明します。

>[!NOTE]
>
>このウィザードは、実稼働プログラムでのみ使用できます。 理由： [サンドボックスプログラム](introduction-sandbox-programs.md#auto-creation) プロジェクトの自動作成を含めるので、ウィザードは不要です。