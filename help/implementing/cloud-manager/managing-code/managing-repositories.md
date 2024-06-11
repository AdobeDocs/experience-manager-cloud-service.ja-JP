---
title: Cloud Manager でのリポジトリの管理
description: Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: e467c8058531441524fedd37e14b82b7fb255c69
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 30%

---


# Cloud Manager でのリポジトリの管理 {#managing-repos}

Cloud Manager で Git リポジトリを作成、表示および削除する方法について説明します。

## 概要 {#overview}

リポジトリは、Git を使用してプロジェクトのコードを保存および管理するために使用されます。 Cloud Manager で作成するすべてのプログラムには、Adobeが管理するリポジトリが作成されます。

Adobeが管理するリポジトリーを別途作成したり、独自のプライベートリポジトリーを追加したりできます。 プログラムに関連付けられているすべてのリポジトリーは、 **リポジトリ** ウィンドウ。

Cloud Manager で作成されたリポジトリは、パイプラインの追加や編集の際にも選択できます。 詳しくは、[CI／CD パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を参照してください。

どのパイプラインにも 1 つのプライマリリポジトリまたはブランチがあります。（を使用） [git サブモジュールのサポート、](git-submodules.md) ビルド時に多数のセカンダリブランチを含めることができます。

## リポジトリーウィンドウ {#repositories-window}

1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) で Cloud Manager にログインし、適切な組織とプログラムを選択します。

1. **プログラムの概要**&#x200B;ページで、「**リポジトリ**」タブをクリックして「**リポジトリ**」ページに切り替えます。

1. この **リポジトリ** ウィンドウには、プログラムに関連付けられているすべてのリポジトリが表示されます。

   ![リポジトリーウィンドウ](assets/repositories.png)

この **リポジトリ** ウィンドウには、リポジトリに関する次の詳細が表示されます。

* リポジトリのタイプ
   * **Adobe** Adobeが管理するリポジトリを示します
   * **GitHub** 管理するプライベート GitHub リポジトリを示します
* 作成時
* リポジトリに関連付けられているパイプライン

ウィンドウでリポジトリを選択し、省略記号ボタンをクリックして、選択したリポジトリに対するアクションを実行できます。

* **[ブランチを確認/ プロジェクトを作成](#check-branches)** （Adobeリポジトリーでのみ使用可能）
* **[リポジトリー URL をコピー](#copy-url)**
* **[表示と更新](#view-update)**
* **[削除](#delete)**

![リポジトリのアクション](assets/repository-actions.png)

## リポジトリの追加 {#adding-repositories}

「」をタップまたはクリックします **リポジトリを追加** のボタン **リポジトリ** を開始するウィンドウ **リポジトリを追加** ウィザード。

![リポジトリーを追加ウィザード](assets/add-repository-wizard.png)

Cloud Manager は、Adobe（**Adobeリポジトリ**）と、独自に管理されるリポジトリ（**プライベートリポジトリ**）に設定します。 必須フィールドは、追加するリポジトリのタイプによって異なります。 詳しくは、次のドキュメントを参照してください。

* [Cloud Manager でのAdobeリポジトリーの追加](adobe-repositories.md)
* [Cloud Manager でのプライベートリポジトリの追加](private-repositories.md)

>[!NOTE]
>
>* リポジトリを追加するには、**デプロイメントマネージャー**&#x200B;または&#x200B;**ビジネスオーナー**&#x200B;の役割が必要です。
>* 特定の企業または IMS 組織のすべてのプログラムで、使用できるリポジトリは 300 個までです。

## リポジトリー情報へアクセス {#repo-info}

でリポジトリを表示する場合 **リポジトリ** Adobe ウィンドウを使用すると、 **リポジトリ情報にアクセス** ボタンをクリックします。

![リポジトリ情報](assets/repo-info.png)

この **リポジトリ情報** ウィンドウが開き、詳細が表示されます。 リポジトリ情報へのアクセスについて詳しくは、ドキュメントを参照してください [リポジトリ情報へのアクセス。](accessing-repos.md)

## 分岐を確認 / プロジェクトを作成 {#check-branches}

この **ブランチを確認/ プロジェクトを作成** アクションは、リポジトリの状態に応じて 2 つの機能を実行します。

* リポジトリーを新しく作成する場合、このアクションにより基づいてサンプルプロジェクトが作成されます [AEM プロジェクトアーキタイプ。](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/overview)
* サンプルプロジェクトがリポジトリで既に作成されている場合は、リポジトリとそのブランチの状態を確認し、サンプルプロジェクトが既に存在するかどうかを報告します。

![ブランチの確認アクション](assets/check-branches.png)

## リポジトリ URL を作成 {#copy-url}

この **リポジトリー URL をコピー** アクションは、 **リポジトリ** 他の場所で使用するクリップボードのウィンドウです。

## 表示と更新 {#view-update}

この **表示と更新** アクションを実行すると、 **リポジトリーの更新** ダイアログ。 これを使用すると、 **名前** および **リポジトリ URL のプレビュー** を更新し、 **説明** を表示します。

![リポジトリ情報の表示と更新](assets/view-update.png)

## 削除 {#delete}

この **削除** アクションがプロジェクトからリポジトリを削除します。 リポジトリは、パイプラインに関連付けられている場合、削除できません。

![削除](assets/delete.png)

リポジトリを削除すると、次のようになります。

* 削除したリポジトリ名は、今後作成される可能性のある新しいリポジトリに使用できなくなります。
   * このような場合、「`Repository name should be unique within organization.`」というエラーメッセージが表示されます。
* 削除したリポジトリを Cloud Manager で使用不可にし、パイプラインにリンクできないようにします。
